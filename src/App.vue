<template>
  <v-app id="inspire">
    <v-app-bar extended>
      <v-app-bar-nav-icon></v-app-bar-nav-icon>

      <v-app-bar-title>Informatički Projekt 2 - Pasmine</v-app-bar-title>

      <v-spacer></v-spacer>

      <!-- Add a button/link to the About page -->
      <router-link to="/about">
        <v-btn icon>
          <v-icon>mdi-dots-vertical</v-icon>
        </v-btn>
      </router-link>
    </v-app-bar>

    <v-main>
      <router-view />
    </v-main>
  </v-app>
</template>



<script>

export default {
  name: 'App',

  data: () => ({
    //
  }),
};
</script>
