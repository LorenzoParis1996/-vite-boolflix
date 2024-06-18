<script>
import axios from 'axios';
import HeaderSearchBar from './HeaderSearchBar.vue';
import AppHeader from './AppHeader.vue';



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
    HeaderSearchBar,
    AppHeader
  }
  
}

</script>

<template>
  <section class="header">
  <AppHeader/>
  <HeaderSearchBar @searched="searchBoth"/>
  </section>
 
 <div class="main">
   <section class="wrapper">
   
   <article v-for="movie in movies" :key="movie.id">
     <img class="no-poster" v-if="movie.poster_path == null" src="https://www.psdmockups.com/wp-content/uploads/2019/10/Movie-Poster-Advertising-PSD-Mockup.jpg" alt="poster not available">
     <img v-else :src="`https://image.tmdb.org/t/p/w342${movie.poster_path}`" :alt="`${movie.title}`">
    <p></p>
    <p></p>
    <p></p>
    <p></p>
    <p></p>
   </article>


   <article v-for="serie in series" :key="serie.id">
     <img class="no-poster" v-if="serie.poster_path == null" src="https://www.psdmockups.com/wp-content/uploads/2019/10/Movie-Poster-Advertising-PSD-Mockup.jpg" alt="poster not available">
     <img v-else :src="`https://image.tmdb.org/t/p/w342${serie.poster_path}`" :alt="`${serie.title}`">
    <div class="overview">
    <p></p>
    <p></p>
    <p></p>
    <p></p>
    <p></p>
    </div>
   </article>
  
   
 

  </section>
 </div>
 
</template>

<style lang="scss" scoped>
@use '../styles/partials/flags' as *;

ul {
  
  list-style: none;
}

.lang-icon {
  background-image: url(../../node_modules/@textabledev/langs-flags-list/lang-flags.png);
}

.header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 1rem;
  background-color: black;
}

.main {
  background-color: rgb(67, 67, 67);
  
  

  .wrapper {
    display: flex;
    justify-content: center;
    flex-wrap: wrap;
    padding: 5rem;
    
   
    article {
      width: calc(100% / 6);
      padding: 1rem;


      img {
        width: 100%;
        aspect-ratio: 1/1.5;
        
      }

      .no-poster {
        width: 100%;
        height: 99%;
        
      }
    }
    
  }
}

</style>