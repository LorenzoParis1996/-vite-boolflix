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
      <label for="search">Search</label>
      <input type="text" name="movie-name" id="movie-name" v-model="searchInput"
         @keyup.enter="$emit('searched', searchInput)">
      <button @click="$emit('searched', searchInput)"><i class="fa-solid fa-magnifying-glass"></i></button>
   </div>
</template>

<style lang="scss" scoped>
label,
input,
button {
   margin: 0 0.5rem;
}

label {
   color: white;
   text-transform: uppercase;
   font-size: 15px;
}


button {
   background-color: black;
   color: white;
   border: none;
   border-radius: 5px;
   font-size: 20px;
   padding: 0.5rem;

   &:hover {
      color: black;
      background-color: white;
   }
}
</style>