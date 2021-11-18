<template>
  <div id="app">
    <div class="searchbar">
      <input type="text" placeholder="Inserisci una ricerca">
      <button><i class="fas fa-search"></i></button>
    </div>
  </div>
</template>

<script>

import axios from 'axios';

export default {
  name: 'App',
  components: {
  },
  
  data() {
    return {
      movies: [],
      api_url: `https://api.themoviedb.org/3/search/movie?api_key=<<api_key>>&language=it-IT&query=&page=1&include_adult=true`
    }
  },

  methods: {
    callApi() {
      axios
      .get
      .then((response) => {
        this.movies = response.data;
      })
    }
  }

}
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
