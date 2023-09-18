<template>
  <v-app id="inspire">
    <v-main class="bg-grey-lighten-3">
      <v-container>
        <v-row>
          <v-col cols="12" md="6">
            <v-sheet min-height="70vh" rounded="lg" class="text-center">
              <div>
                <h1>Ova je stranica rezultat rada na kolegiju Informatički projekt II.</h1>
                <p>Cilj je koristiti tehnologije Vue, Vuetify CSS framework, Vue router, integriranje izabranoga, javno dostupnog, API-ja za prikaz, traženje i filtriranje željenih podataka...</p>
              </div>
              <v-img
                src="../friendly_dog.png"
                alt="Filler Dog"
                max-width="700"
                class="mx-auto mt-4"
              ></v-img>
              <!-- Button to go back to the home page -->
              <router-link to="/" class="mt-4">
                <v-btn color="primary">Back to Home</v-btn>
              </router-link>
            </v-sheet>
          </v-col>
          <v-col cols="12" md="6">
            <v-sheet min-height="70vh" rounded="lg" class="text-center">
              <div>
                <h2>Kontakt informacije:</h2>
                <p>Ime i prezime studenta: Faruk Mešanović</p>
                <p>Studij: Informatika</p>
                <p>Lokacija: Orašje / Odžak</p>
                <p>Index: 14098</p>
              </div>
              <div class="mt-4">
                <p>Hvala na pregledu projekta, puni repozitorij se nalazi na <a href="https://github.com/eFFect7/DogBreeds.git" target="_blank">GitHub-u</a></p>
              </div>
            </v-sheet>
          </v-col>
        </v-row>
      </v-container>
    </v-main>
  </v-app>
</template>
