<template>
  <div id="app">
    <div class="searchbar">
      <input v-model="searchText" type="text" placeholder="Inserisci una ricerca">
      <button @click="callApi"><i class="fas fa-search"></i></button>
      <div class="d-flex flex-wrap">
        <div v-for="movie in movies" :key="movie.title" class="px-2 py-2 black_border m-2">
          <MovieElement
            :title="movie.title"
            :original_title="movie.original_title"
            :language="movie.original_language"
            :vote="movie.vote_average"
            />       
        </div>
      </div>
    </div>
  </div>
</template>

<script>

import axios from 'axios';
import MovieElement from './components/MovieElement.vue'

export default {
  name: 'App',
  components: {
    MovieElement
  },
  
  data() {
    return {
      movies: [],
      searchText: "",
      searchedText: "",
    }
  },

  methods: {
    callApi() {
      let searchedText = this.searchText;
      axios
      .get(`https://api.themoviedb.org/3/search/movie?api_key=84b0b6316c205b8b763bc2ee40ce3b0d&language=en-US&query=` + searchedText + `&page=1&include_adult=false`)
      // .get(`https://api.themoviedb.org/3/search/movie?api_key=84b0b6316c205b8b763bc2ee40ce3b0d&language=en-US&query=dog&page=1&include_adult=false`)
      .then((response) => {
        console.log(searchedText);
        this.movies = response.data.results;
        console.log(this.movies);
        console.log(`https://api.themoviedb.org/3/search/movie?api_key=84b0b6316c205b8b763bc2ee40ce3b0d&language=it-IT&query=` + searchedText + `&page=1&include_adult=true`);
        // console.log(this.searchText);
        // console.log(this.api_url);
      })
    }
  }

}
</script>

<style lang="scss">

@import "../node_modules/bootstrap/scss/bootstrap.scss";

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.black_border {
  border: 1px solid black;
}
</style>
