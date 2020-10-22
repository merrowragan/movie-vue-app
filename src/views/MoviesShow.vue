<template>
  <div class="movies-show">
 
      

      <h3>Title: {{ movie.title }}</h3>
      <p>Year: {{ movie.year }}</p>
      <p>Plot: {{ movie.plot }}</p>

      <!-- <router-link to="`/posts/${post.id}/edit`">Edit </router-link> | -->
   

   
  </div>
</template>

<style>
</style>

<script>
import axios from "axios";

export default {
  data: function() {
    return {
      movie: {}
     
    };
  },
  created: function() {
    axios.get(`/api/movies/${this.$route.params.id}`).then(response => {
      console.log(response.data);
      this.movie = response.data;
    });
  },
  methods: {}
};
</script>