<template>
  <div class="movies-index">
    Search by title: <input v-model="titleFilter" list="titles">
    <datalist id="titles">
	    <option v-for="movie in movies">{{ movie.title }}</option>
    </datalist>
    <button
        v-on:click="setSortAttribute('title')"
        class="btn btn-success mr-2"
      >
        Sort Alphabetically
      </button> 

<!-- 
     <div v-for="movie in orderBy(filterBy(movies, titleFilter, 'title'), 'title')">
      <h2>Title: {{ movie.title }}</h2>
      <p>Year: {{ movie.year }}</p>
      <p>Plot: {{ movie.plot }}</p>
      <button v-on:click="showMovie(movie)">More Info</button> -->
      <div class="card-columns">
      <div class="card" v-for="movie in movies">
        <router-link :to="`/movies/${movie.id}`">
        </router-link>
        <div class="card-body">
          <h5 class="card-title">{{ movie.title }}</h5>
          <p class="card-text">Year: {{ movie.year}}</p>
          <p class="card-text">Plot: {{ movie.plot }}</p>
        </div>
      </div>

    </div>
  </div>
</template>

<style>
</style>

<script>
import axios from "axios";
import Vue2Filters from "vue2-filters";

export default {
  mixins: [Vue2Filters.mixin],
  data: function() {
    return {
      movies: [],
      titleFilter: '',
      sortAttribute: "title"
     
    
    };
  },
  created: function() {
    axios.get("/api/movies").then((response) => {
      console.log(response.data);
      this.movies = response.data;
    });
  },
  methods: {
    setSortAttribute: function(attribute) {
      this.sortAttribute = attribute;
    },
  },
  
};
</script>