<template>
    <div class="container">
        <Searchbar 
            @search="callApi"
        />
        <div class="d-flex flex-wrap row">
            <div v-for="movie in movies" :key="movie.id" class="col-2 py-2 my-2">
                <MovieElement

                :result="movie"
                :title="movie.title"
                :original_title="movie.original_title"
                :language="movie.original_language"
                :vote="movie.vote_average"
                
                />       
            </div>
        </div>
    </div>
</template>

<script>
import MovieElement from './MovieElement.vue';
import Searchbar from './Searchbar.vue';
import axios from 'axios';

export default {
    components: {
        MovieElement,
        Searchbar
    },

    data() {
        return {
        movies: [],
        searchText: "",
        movies_url: 'https://api.themoviedb.org/3/search/movie',
        api_key: '84b0b6316c205b8b763bc2ee40ce3b0d',
        // searchedText: "",
        }
    },

    methods: {
        callApi(searchText) {
        let movieQuery = `${this.movies_url}?api_key=${this.api_key}&language=en-US&query=${searchText}&page=1&include_adult=true`;
        // console.log(movieQuery);
            axios
            .get(movieQuery)
            // .get(`https://api.themoviedb.org/3/search/movie?api_key=84b0b6316c205b8b763bc2ee40ce3b0d&language=en-US&query=dog&page=1&include_adult=false`)
            .then((response) => {
                // console.log(searchedText);
                this.movies = response.data.results;
                console.log(this.movies);
                console.log(`https://api.themoviedb.org/3/search/movie?api_key=84b0b6316c205b8b763bc2ee40ce3b0d&language=it-IT&query=` + searchText + `&page=1&include_adult=true`);
                // console.log(this.searchText);
                // console.log(this.api_url);
            })
        }
    }
}
</script>