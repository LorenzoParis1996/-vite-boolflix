<script>
import axios from 'axios';
import HeaderSearchBar from './HeaderSearchBar.vue';
import AppHeader from './AppHeader.vue';



export default {
  data() {
    return {
      movies: [{

      }],
      series: [{

      }],
      hasSearched: false
    }
  },
  methods: {
    getMovies(movieName) {
      axios.get('https://api.themoviedb.org/3/search/movie?api_key=38b525462acbdcf4ec457c833e004566&query=' + movieName)
        .then((response) => {
          this.movies = response.data.results;
          this.hasSearched = true;
          console.log(this.movies);
        })
        .catch(function (error) {
          console.log(error);
        })
    },
    searchMovie(searchInput) {
      this.getMovies(searchInput);
    },
    getSeries(seriesName) {
      axios.get('https://api.themoviedb.org/3/search/tv?api_key=38b525462acbdcf4ec457c833e004566&query=' + seriesName)
        .then((response) => {
          this.series = response.data.results;
          this.hasSearched = true;
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
    //this.getMovies();
    //this.getSeries();
  },
  components: {
    HeaderSearchBar,
    AppHeader
  }

}

</script>

<template>
  <section class="header">
    <AppHeader />
    <HeaderSearchBar @searched="searchBoth" />
  </section>

  <div class="main">
    <section class="wrapper">

      <div v-if="!hasSearched" class="search-message">
        <h1>Start searching</h1>
      </div>

      <article v-for="movie in movies" :key="movie.id" v-if="hasSearched">

        <img class="no-poster" v-if="movie.poster_path == null"
          src="https://www.shutterstock.com/image-illustration/red-wall-words-coming-soon-260nw-2285307157.jpg"
          alt="poster not available">
        <img v-else :src="`https://image.tmdb.org/t/p/w342${movie.poster_path}`" :alt="`${movie.title}`">

        <div class="overview">
          <p><strong>Type Media: </strong>Movie</p>
          <p><strong>Title: </strong>{{ movie.title }}</p>
          <p><strong>Original title: </strong>{{ movie.original_title }}</p>
          <p><strong>Language: </strong><i class="lang-icon" :class="`lang-icon-${movie.original_language}`"></i></p>
          <p><strong>Vote: </strong><i v-for="star in parseInt(Math.round(movie.vote_average) / 2)"
              class="fa-solid fa-star" style="color: #ffd43b;"></i>
            <i v-for="star in (5 - parseInt(Math.round(movie.vote_average) / 2))" class="fa-regular fa-star"></i>
          </p>
          <p><strong>Overview: </strong>{{ movie.overview ? movie.overview : "No info available" }}</p>
        </div>
      </article>


      <article v-for="serie in series" :key="serie.id" v-if="hasSearched">

        <img class="no-poster" v-if="serie.poster_path == null"
          src="https://www.psdmockups.com/wp-content/uploads/2019/10/Movie-Poster-Advertising-PSD-Mockup.jpg"
          alt="poster not available">
        <img v-else :src="`https://image.tmdb.org/t/p/w342${serie.poster_path}`" :alt="`${serie.title}`">

        <div class="overview">
          <p><strong>Type Media:</strong> TV Serie</p>
          <p><strong>Title: </strong>{{ serie.name }}</p>
          <p><strong>Original title: </strong>{{ serie.original_name }}</p>
          <p><strong>Vote: </strong><i class="lang-icon" :class="`lang-icon-${serie.original_language}`"></i></p>
          <p><strong>Vote: </strong><i v-for="star in parseInt(Math.round(serie.vote_average) / 2)"
              class="fa-solid fa-star" style="color: #ffd43b;"></i>
            <i v-for="star in (5 - parseInt(Math.round(serie.vote_average) / 2))" class="fa-regular fa-star"></i>
          </p>
          <p><strong>Overview: </strong>{{ serie.overview ? serie.overview : "No info available" }}</p>
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
  display: flex;
  flex-direction: column;
  min-height: 100vh;



  .wrapper {
    display: flex;
    justify-content: center;
    flex-wrap: wrap;
    gap: 1rem;
    padding: 5rem;
    flex-grow: 1;


    .search-message {
      color: white;
      display: flex;
      justify-content: center;
      align-items: center;
      font-size: 3rem;
    }


    article {
      width: calc(100% / 6);
      position: relative;




      img {
        width: 100%;
        aspect-ratio: 1/1.5;
        vertical-align: bottom;

      }

      .no-poster {
        width: 100%;
        height: auto;
      }

      .overview {
        visibility: hidden;
        color: white;
        font-size: 13px;
        position: absolute;
        top: 0;
        right: 0;
        left: 0;
        bottom: 0;
        padding: 1rem;
        background-color: black;
        border: 2px solid white;
        opacity: 0.9;
        overflow-y: auto;
      }


    }

    article:hover .overview {
      visibility: visible;
    }

  }
}
</style>