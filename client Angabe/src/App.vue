<template>
  <v-app>
    <v-app-bar app color="teal lighten-1">
      <div class="d-flex align-center">
        <img src="./assets/books.png" />
        <v-toolbar-title class="d-inline mx-2 white--text text-h6"
          >Books'n More</v-toolbar-title
        >
        <img src="./assets/books.png" />
      </div>

      <v-spacer></v-spacer>

      <v-btn
        small
        to="/"
        class="teal lighten-2 white--text me-2"
        active-class="deep-orange darken-1"
        >Home</v-btn
      >
      <v-btn
        small
        to="/about"
        class="teal lighten-2 white--text"
        active-class="deep-orange darken-1"
        >About</v-btn
      >
    </v-app-bar>

    <v-main>
      <v-container> <router-view :books="books" /></v-container>
    </v-main>
  </v-app>
</template>

<script>
import books from './assets/books.json';

export default {
  name: 'App',

  data: () => ({
    books: books,
  }),
};
</script>

<style scoped>
img {
  height: 50px;
}
</style>
