<script>
import axios from 'axios';



export default {
  data() {
     return {
        movies: [{

        }]
     }
  },
  methods: {
    getMovies () {
       axios.get('https://api.themoviedb.org/3/search/movie?api_key=38b525462acbdcf4ec457c833e004566&query=jurassic+park')
       .then((response) => {
         this.movies= response.data.results;
         console.log(this.movies);
       })
       .catch(function (error) {
                    console.log(error);
       })
    }
  },
  created() {
    this.getMovies();
  }
  
}

</script>

<template>
 <h1>main</h1>
 <div>
  <ul v-for="movie in movies" :key="movie.id">
    <li>{{ movie.title }}</li>
 
    
  </ul>
 </div>
 
</template>

<style lang="scss" scoped>




</style>