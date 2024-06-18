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
  <h1>Movies</h1>
  <ul v-for="movie in movies" :key="movie.id">
    <li>
      <img :src="`https://image.tmdb.org/t/p/w154${movie.poster_path}`" :alt="`${movie.title}`">
    </li>
    <li>{{ movie.title }}</li>
    <li>{{ movie.original_title }}</li>
    <li class="lang-icon" :class="`lang-icon-${movie.original_language}`"></li>
    <li>{{ parseInt(Math.round(movie.vote_average) / 2) }}</li>
  </ul>
  <h1>Series</h1>
  <ul v-for="serie in series" :key="serie.id">
    <li>
      <img :src="`https://image.tmdb.org/t/p/w154${serie.poster_path}`" :alt="`${serie.title}`">
    </li>
    <li>{{ serie.name }}</li>
    <li>{{ serie.original_name }}</li>
    <li class="lang-icon" :class="`lang-icon-${serie.original_language}`"></li>
    <li>{{ parseInt(Math.round(serie.vote_average) / 2) }}</li>

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