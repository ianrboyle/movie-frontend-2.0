<template>
  <div class="movies-edit">
    <h1>{{ message }}</h1>
    <form v-on:submit.prevent="updateMovie()">
      <ul>
        <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
      </ul>
      <div>
        <label>Title:</label>
        <input type="text" v-model="currentMovieParams.title" />
      </div>
      <div>
        <label>Year:</label>
        <input type="text" v-model="currentMovieParams.year" />
      </div>
      <div>
        <label>Plot:</label>
        <input type="text" v-model="currentMovieParams.plot" />
      </div>

      <input type="submit" value="Submit" />
      |
      <button v-on:click="deleteMovie()">Delete</button>
    </form>
  </div>
</template>
<script>
import axios from "axios";
export default {
  data: function () {
    return {
      message: "Welcome to the edit movies page.",
      currentMovieParams: {},
      errors: [],
    };
  },
  created: function () {
    axios.get(`http://localhost:3000/movies/${this.$route.params.id}`).then((response) => {
      console.log("My Movie: ", response.data);
      this.currentMovieParams = response.data;
    });
  },
  methods: {
    updateMovie: function () {
      axios
        .patch(`http://localhost:3000//movies/${this.$route.params.id}`, this.currentMovieParams)
        .then((response) => {
          this.currentMoviearams = response.data;
          this.$router.push(`/movies/${this.$route.params.id}`);
        })
        .catch((error) => console.log(error.response));
    },
    deleteMovie: function () {
      axios.delete("http://localhost:3000/movies/" + this.$route.params.id).then((response) => {
        console.log("Destroyed!", response.data);
        this.$router.push("/movies");
      });
    },
  },
};
</script>
