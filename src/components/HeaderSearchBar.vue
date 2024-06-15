<script>
export default {
  data() {
     return {
        searchInput: ''
     }
  }
 
  
}
</script>

<template>
  <div>
  <label for="search">search movie</label>
  <input type="text" name="movie-name" id="movie-name" v-model="searchInput">
  <button @click="$emit('searched', searchInput)">search</button>
 </div>
</template>

<style>

</style>