<template>
  <div class="movies-index">
    <h1>{{ message }}</h1>
    <div v-for="movie in movies" v-bind:key="movie.id">
      {{ movie.title }}
      <router-link v-bind:to="`/movies/${movie.id}`">Movie Info</router-link>
    </div>
  </div>
</template>
<script>
import axios from "axios";

export default {
  data: function () {
    return {
      message: "Welcome to the movies index page.",
      movies: [],
    };
  },
  created: function () {
    axios.get("http://localhost:3000/movies").then((response) => {
      this.movies = response.data;
      console.log("Movies:", response.data);
    });
  },
};
</script>
