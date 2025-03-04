<template>
  <div class="app font-monospace">
    <div class="content">
      <!-- Movie Info -->
      <AppInfo 
        :allMoviesCount="movies.length" 
        :favoriteMovieCount="movies.filter(c => c.favorite).length"
      />
      
      <!-- Search & Filter Section -->
      <div class="search-panel">
        <SearchPanel @updateTerm="updateTermHandler"/>
        <AppFilter @updateFilter="updateFilterHandler"/> <!-- 🔥 Fixed event listener -->
      </div> 

      <!-- Movie List -->
      <MovieList 
        :movies="onFilterHandler(filteredMovies, filter)" 
        @onToggle="onToggleHandler" 
        @onRemove="onRemoveHandler"
      />   

      <!-- Add New Movie -->
      <MovieAddForm @createMovie="createMovie"/>
    </div>
  </div>
</template>

<script>
import AppFilter from '../app-filter/AppFilter.vue';
import AppInfo from '../app-info/AppInfo.vue';
import MovieAddForm from '../movie-add-form/MovieAddForm.vue';
import MovieList from '../movie-list/MovieList.vue';
import SearchPanel from '../search-panel/SearchPanel.vue';

export default {
  components: {
    AppInfo,
    SearchPanel,
    AppFilter,
    MovieList,
    MovieAddForm,
  },
  data() {
    return {
      movies: [
        { name: "Avengers", viewers: 901, favorite: false, like: true, id: 1 },
        { name: "Captain America", viewers: 902, favorite: true, like: false, id: 2 },
        { name: "Spider-Man", viewers: 903, favorite: false, like: false, id: 3 }
      ],
      term: '',
      filter: 'all', // Default filter state
    };
  },
  computed: {
    filteredMovies() {
      if (!this.term) {
        return this.movies;
      }
      return this.movies.filter(movie => 
        movie.name.toLowerCase().includes(this.term.toLowerCase())
      );
    }
  },
  methods: {
    createMovie(item) {
      this.movies.push(item);
    },
    onToggleHandler({ id, prop }) {
      this.movies = this.movies.map(item => 
        item.id === id ? { ...item, [prop]: !item[prop] } : item
      );
    },
    onRemoveHandler(id) {
      this.movies = this.movies.filter(movie => movie.id !== id);
    },
    updateTermHandler(term) {
      this.term = term; // Update the search term
    },
    onFilterHandler(arr, filter) {
      switch (filter) {
        case "popular":
          return arr.filter(c => c.favorite);
        case "mostViewers":
          return arr.filter(c => c.viewers > 500);
        default:
          return arr;
      }
    },
    updateFilterHandler(filter) {
      this.filter = filter; // Update filter state when user selects a filter
    }
  }
};
</script>

<style>
.app {
  height: 100vh;
  color: #101010;
}

.content {
  width: 1000px;
  min-height: 700px;
  background-color: #fff;
  margin: 0 auto;
  padding: 5rem 0;
}

.search-panel {
  margin-top: 2rem;
  padding: 1.5rem;
  background-color: #fcfaf5;
  border-radius: 4px;
  box-shadow: 15px 15px 15px rgba(0, 0, 0, 0.15);
}
</style>
