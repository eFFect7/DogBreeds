<template>
  <v-container>
    <!-- Search input-->
    <v-row>
      <v-col cols="12">
        <v-text-field
          v-model="searchQuery"
          label="Search Dog Breeds"
          outlined
          class="mb-4"
        ></v-text-field>
      </v-col>
    </v-row>

    <!-- Breed cards -->
    <v-row>
      <!-- Loop through and filter breeds based on searchQuery -->
      <v-col
        v-for="breed in filteredBreeds"
        :key="breed.id"
        cols="4"
      >
        <!-- Breed card content (same as before) -->
        <v-card class='breed-card' height="200" @mouseenter="hoveredBreed = breed" @mouseleave="hoveredBreed = null">
          <!-- Set a fixed height for the card -->
          <v-img :src="breedImages[breed.id]" alt="Slika pasmine" class="breed-image"></v-img>
          <v-card-title>{{ breed.name }}</v-card-title>
          <v-card-text>
            <v-card-text :class="{ 'breed-info': true, 'active': hoveredBreed === breed }">
              <strong>Origin:</strong> {{ breed.origin }}
            </v-card-text>
          </v-card-text>
        </v-card>
      </v-col>
    </v-row>

    <!-- Pagination controls -->
    <v-row>
      <v-col cols="12">
        <pagination :page-count="Math.ceil(filteredBreeds.length / perPage)" v-model="currentPage" :prev-text="'Previous'" :next-text="'Next'" :container-class="'pagination'"></pagination>
      </v-col>
    </v-row>
  </v-container>
</template>


<script>
import axios from "axios";
import config from "@/config.js";
import Pagination from 'vue-pagination-2';

export default {
  name: 'HomeView',
  components: {
    Pagination,
  },
  data() {
    return {
      breeds: [],
      breedImages: {},
      hoveredBreed: null,
      searchQuery: '', // Add searchQuery data property
      currentPage: 1,
      perPage: 6,
    };
  },
  computed: {
    filteredBreeds() {
      const query = this.searchQuery.toLocaleLowerCase();
      const filtered = this.breed.filter(breed => breed.name.toLocaleLowerCase().includes(query));

      const startIndex = (this.currentPage - 1) * this.perPage;
      const endIndex = startIndex + this.perPage;

      return filtered.slice(startIndex, endIndex);
    },
  },
  created() {
    axios
      .get("https://api.thedogapi.com/v1/breeds", {
        headers: {
          "x-api-key": config.dogApiKey,
        },
      })
      .then((response) => {
        this.breeds = response.data;

        // Fetch images for each breed
        this.breeds.forEach((breed) => {
          axios
            .get(`https://api.thedogapi.com/v1/images/search?breed_ids=${breed.id}`, {
              headers: {
                "x-api-key": config.dogApiKey,
              },
            })
            .then((imageResponse) => {
              if (imageResponse.data.length > 0) {
                this.$set(this.breedImages, breed.id, imageResponse.data[0].url);
              }
            })
            .catch((error) => {
              console.error(`Greška pronalaska slike pasmine ${breed.name}:`, error);
            });
        });
      })
      .catch((error) => {
        console.error("Greška potrage pasmina:", error);
      });
  },
  computed: {
    filteredBreeds() {
      // Filter breeds based on searchQuery
      const query = this.searchQuery.toLowerCase();
      return this.breeds.filter(breed => breed.name.toLowerCase().includes(query));
    },
  },
};
</script>

<style>
.breed-info::before {
  content: "";
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(147, 112, 219, 0.9);
  z-index: -1;
}
.breed-info {
  opacity: 0;
  transition: opacity 0.3s;
  position: relative;
  z-index: 1;
}
.breed-info.active {
  opacity: 1;
}
.breed-card {
  margin: 10px;
}

/* dimenzije */
.breed-image {
  max-width: 100%;
  max-height: 100%;
  object-fit: cover;
}
</style>
