<template>
  <div class="movies-edit">
    <form v-on:submit.prevent="updateMovie()">
      <h1>Edit Movie</h1>
      <ul>
        <li class="text-danger" v-for="error in errors">{{ error }}</li>
      </ul>
      <div class="form-group">
        <label>Title:</label> 
        <input type="text" class="form-control" v-model="movie.title">
      </div>
      <div class="form-group">
        <label>Year:</label>
        <input type="text" class="form-control" v-model="movie.year">
      </div>
      <div class="form-group">
        <label>Plot:</label>
        <input type="text" class="form-control" v-model="movie.plot">
      </div>
      <input type="submit" class="btn btn-warning" value="Update">
    </form>
     <button class="btn btn-danger" v-on:click="destroyMovie()">Delete</button>
   
  </div>
</template>

<style>
</style>

<script>
import axios from "axios";

export default {
  data: function() {
    return {
      movie: {},
      errors: []
      
    };
  },
  created: function() {
    axios.get(`/api/movies/${this.$route.params.id}`).then(response => {
      console.log(response.data);
      this.movie = response.data
    });
   

  },

  methods: {
    updateMovie: function () {
    var params = {
      title: this.movie.title,
      year: this.movie.year,
      plot: this.movie.plot
      };
    axios.patch(`/api/movies/${this.movie.id}`, params).then(response => {
      this.$router.push(`/movies/${this.movie.id}`);
    })
    .catch(error => {
      this.errors = error.response.data.errors;
    });
  },
  destroyMovie: function () {
    if(confirm("Are you sure you want to delete this movie?")) {
      axios.delete(`/api/movies/${this.movie.id}`).then(response => {
        console.log("Success!", response.data);
        this.$router.push("/movies");
      });
    }
   }
  }
};
</script>