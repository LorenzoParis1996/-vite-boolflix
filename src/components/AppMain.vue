<script>
import axios from 'axios';
import HeaderSearchBar from './HeaderSearchBar.vue';


export default {
  data() {
     return {
        movies: [{

        }],
        series:[{

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
    },
    getSeries (seriesName) {
      axios.get('https://api.themoviedb.org/3/search/tv?api_key=38b525462acbdcf4ec457c833e004566&query=' + seriesName)
      .then((response) => {
        this.series = response.data.results;
        console.log(this.series);
      })
      .catch(function (error) {
        console.log(error);
      })
    },
    searchSeries(searchInput) {
      this.getSeries(searchInput);
    },
    searchBoth(searchInput) {
      this.getMovies(searchInput);
      this.getSeries(searchInput);
    }
  },
  created() {
    this.getMovies();
    this.getSeries();
  },
  components: {
    HeaderSearchBar
  }
  
}

</script>

<template>
  <HeaderSearchBar @searched="searchBoth"/>
 <h1>main</h1>
 <div>
  <ul v-for="movie in movies" :key="movie.id">
    <li>{{ movie.title }}</li>
    <li>{{ movie.original_title }}</li>
    <li class="lang-icon" :class="`lang-icon-${movie.original_language}`"></li>
    <li>{{ movie.vote_average }}</li>
  </ul>
  <ul v-for="serie in series" :key="serie.id">
    <li>{{ serie.name }}</li>
    <li>{{ serie.original_name }}</li>
    <li class="lang-icon" :class="`lang-icon-${serie.original_language}`"></li>
    <li>{{ serie.vote_average }}</li>

  </ul>
 </div>
 
</template>

<style lang="scss" scoped>
@use '../styles/partials/flags' as *;

ul {
  padding: 1rem;
  list-style: none;
}

.lang-icon {
  background-image: url(../../node_modules/@textabledev/langs-flags-list/lang-flags.png);
}

</style>