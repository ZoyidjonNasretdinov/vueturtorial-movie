<template lang="">
  <ul class="movie-list list-group">
    <MovieListItem  v-for="movie in movies" v-bind:movie="movie"/>
  </ul>
</template>
<script>
import MovieListItem from "@/components/movie-list-item/MovieListItem.vue"
export default {
  components: {
    MovieListItem,
  },
  data() {
    return {
      movies: [
        { 
          name: "Avengers",
          viewers: 901,
          favorite: false, 
          like: true,
        },
        { 
          name: "Captain America", 
          viewers: 902, 
          favorite: true, 
          like: false,
        },
        { 
          name: "Spider-Man", 
          viewers: 903, 
          favorite: false,
          like: false, 
        }
      ],
    };
  }
}
</script>
<style scoped>
.movie-list {
  margin-top: 2rem;
  padding: 1.5rem;
  border-radius: 4px;
  background-color: #fcfaf5;
  box-shadow: 15px 15px 15px rgba(0, 0, 0, 0.15);
}
</style>