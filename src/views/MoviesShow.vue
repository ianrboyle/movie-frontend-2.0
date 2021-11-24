<template>
  <div class="movies-show">
    <h3>{{ movie.title }}</h3>
    <p>{{ movie.plot }}</p>
    <p>{{ movie.year }}</p>
    <router-link v-bind:to="`/movies/${movie.id}/edit`">Edit Movie Info</router-link>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      movie: {},
    };
  },
  created: function () {
    axios.get("http://localhost:3000/movies/" + this.$route.params.id).then((response) => {
      this.movie = response.data;
      console.log("Movies:", response.data);
    });
  },
};
</script>
