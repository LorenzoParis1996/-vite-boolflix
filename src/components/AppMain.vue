<script>
import axios from 'axios';
import HeaderSearchBar from './HeaderSearchBar.vue';


export default {
  data() {
     return {
        movies: [{

        }]
     }
  },
  methods: {
    getMovies (movieName) {
       axios.get('https://api.themoviedb.org/3/search/movie?api_key=38b525462acbdcf4ec457c833e004566&query=' + movieName)
       .then((response) => {
         this.movies= response.data.results;
         console.log(this.movies);
       })
       .catch(function (error) {
                    console.log(error);
       })
    },
    searchMovie(searchInput) {
      this.getMovies(searchInput);
    }
  },
  created() {
    this.getMovies();
  },
  components: {
    HeaderSearchBar
  }
  
}

</script>

<template>
  <HeaderSearchBar @searchedMovie="searchMovie"/>
 <h1>main</h1>
 <div>
  <ul v-for="movie in movies" :key="movie.id">
    <li>{{ movie.title }}</li>
    <li>{{ movie.original_title }}</li>
    <li>{{ movie.original_language }}</li>
    <li>{{ movie.vote_average }}</li>
  </ul>
 </div>
 
</template>

<style lang="scss" scoped>




</style>