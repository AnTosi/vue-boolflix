<template>
    <div>
        <header class="d-flex align-items-center justify-content-between py-2 px-4">
            <h4>
                BOOLFLIX
            </h4>
            <Searchbar 
                @search="callApi"
            />
        </header>
        <div class="main">
            <section class="movies">
                <div>
                    <h2 class="my-3 px-2 my_container text-white">
                        Movies:
                    </h2>
                    <!-- <div class="selectMovie">
                        <label for="filterByGenre">
                            Filter the movies by genre
                        </label>
                        <select name="filterByGenre" id="filterByGenre">
                            <option value="genre" v-for="genre in genres" :key="genre">
                                
                            </option>
                        </select>

                    </div> -->
                </div>
                
                <div class="my_container d-flex flex-wrap">
                    <div v-for="movie in movies" :key="movie.id" class="py-2 my-2">
                        <MovieElement

                        :result="movie"
                        :title="movie.title"
                        :original_title="movie.original_title"
                        :image="movie.poster_path"
                        :language="movie.original_language"
                        :vote="movie.vote_average"
                        :id="movie.id"
                        :overview="movie.overview"
                        
                        />       
                    </div>
                </div>
            </section>
            <section class="TVshows">
                <h2 class="my-3 px-2 my_container text-white">TV Shows:</h2>
                <div class="my_container d-flex flex-wrap">
                    <div v-for="tvShow in tv_shows" :key="tvShow.id" class="py-2 my-2">
                        <TVElement

                        :result="tvShow"
                        :title="tvShow.name"
                        :original_title="tvShow.original_name"
                        :image="tvShow.poster_path"
                        :language="tvShow.original_language"
                        :vote="tvShow.vote_average"
                        :id="tvShow.id"
                        :overview="tvShow.overview"
                        
                        />       
                    </div>
                </div>
            </section>
        </div>
    </div>
</template>

<script>
import MovieElement from './MovieElement.vue';
import Searchbar from './Searchbar.vue';
import TVElement from './TVElement.vue';
import axios from 'axios';


export default {
    components: {
        MovieElement,
        Searchbar,
        TVElement
    },

    data() {
        return {
        movies: [],
        tv_shows: [],
        searchText: "",
        movies_url: 'https://api.themoviedb.org/3/search/movie',
        api_key: '84b0b6316c205b8b763bc2ee40ce3b0d',
        tv_url: 'https://api.themoviedb.org/3/search/tv',
        // searchedText: "",
        genres: [],
        genresName: [],
        }
    },

    methods: {
        callApi(searchText) {
            let movieQuery = `${this.movies_url}?api_key=${this.api_key}&language=it-IT&query=${searchText}&page=1&include_adult=true`;
            let tvQuery = `${this.tv_url}?api_key=${this.api_key}&language=it-IT&query=${searchText}&page=1&include_adult=true`;
            const axiosMovieQuery = axios.get(movieQuery);
            const axiosTvQuery = axios.get(tvQuery);
            axiosMovieQuery
            .then((response) => {

                this.movies = response.data.results;
            // console.log(movieQuery);
                
                // .get(movieQuery)
                // .get(`https://api.themoviedb.org/3/search/movie?api_key=84b0b6316c205b8b763bc2ee40ce3b0d&language=en-US&query=dog&page=1&include_adult=false`)
                // .then((response) => {
                    // console.log(searchedText);
                    // this.movies = response.data.results;
                    // console.log(this.movies);
                    // console.log(`https://api.themoviedb.org/3/search/movie?api_key=84b0b6316c205b8b763bc2ee40ce3b0d&language=it-IT&query=` + searchText + `&page=1&include_adult=true`);
                    // console.log(this.searchText);
                    // console.log(this.api_url);
            
                });
            axiosTvQuery
            .then((response) => {

                this.tv_shows = response.data.results;
                // console.log(this.tv_shows);
                }
            )
        },

        // genresMoviesCallApi() {
        //     for (let i = 0; i < this.movies.length; i++) {
        //         const movie = this.movies[i];
        //         let genresMovieQuery = `https://api.themoviedb.org/3/movie/${movie.id}?api_key=${this.api_key}&language=en-US`;
        //         const axiosGenreMovieQuery = axios.get(genresMovieQuery);
        //         axiosGenreMovieQuery
        //         .then((response) => {

        //             this.genres += response.data.genres;
        //             // console.log(this.genres);

        //             for (let i = 0; i < this.genres.length; i++) {
        //                 const genreName = this.genres[i].name;
        //                 this.genresName.push(genreName);
        //             }

        //             console.log(this.genresName);
        //         })
                
        //     }
            
        // }
    },

}
</script>

<style lang="scss">

    @import "../assets/common.scss";
    @import "../assets/variables.scss";

    .my_container {
        max-width: 1440px;
        margin: auto;
    }

    section {
        margin-top: 2rem;
        margin-bottom: 1rem;
    }

    h2 {
        text-align: left;
    }

    header {
        background-color: black;
    }

    h4 {
        font-size: 2rem;
        color: $main-red;
    }

    .language {
        margin-right: 1rem;
    }

    .fallback_image {
        background-image: url("../assets/JT185.jpg");
        background-size: cover;
        height: 516px;
    }

    .element {
        border: none;
        width: 342px;
        height: 516px;
        .image img {
            height: 516px;
            width: 342px;
        }
        .info {
            
            height: 515px;
            width: 342px;
            background-color: rgba(0, 0, 0, 0.616);
        }

    }
    
    h3 {
        margin-top: 0;
        padding-top: 3rem;
        font-size: 1.5rem;
        padding-bottom: 1rem;
    }

    .overview {
        max-height: 160px;
        overflow: auto;
    }

    .fa-star {
        color: gold;
    }

    .bold {
        font-size: 1.1rem;
        font-weight: 700;
    }

    h6 {
        background: rgba(255, 235, 205, 0.26);
        font-size: 2rem;
        color: black;
        text-align: center;
        top: 50%;
        left: 0;
        width: 100%;
        transform: translate(0, -50%);
    }

    span.vote {
        margin-right: 0.5rem;
    }
    
</style>