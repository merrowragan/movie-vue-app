<template>
  <div class="recipes-index">
     <div v-for="movie in movies">
      <h2>Title: {{ movie.title }}</h2>
      <p>Year: {{ movie.year }}</p>
      <p>Plot: {{ movie.plot }}</p>
      <button v-on:click="showMovie(movie)">More Info</button>

    </div>
  </div>
</template>

<style>
</style>

<script>
import axios from "axios";

export default {
  data: function() {
    return {
      movies: [],
    
    };
  },
  created: function() {
    axios.get("/api/movies").then((response) => {
      console.log(response.data);
      this.movies = response.data;
    });
  },
  methods: {}
};
</script>