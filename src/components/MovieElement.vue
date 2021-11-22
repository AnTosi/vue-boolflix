<template>
        
    <div  @mouseover="showInfo = true" @mouseleave="showInfo=false" class="m-2 element">
        <div v-show="!showInfo" class="image">
            <img v-show="!noImage" v-bind:src="'https://image.tmdb.org/t/p/w342/' + image" alt="">
            <img class="fallback_image" v-show="noImage" alt="">
        </div>

        <div v-show="showInfo" class="info px-4 text-white">
            <h3>
                {{title}}
            </h3>
            <h5>
                {{original_title}}
            </h5>
            <div class="text_left mt-3">
                <flag class="flag" :iso="flag" />
                <span class="language">
                    {{flag}}
                </span>
                <div class="py-3">
                    <span class="bold text-white">Vote:</span>
                    <span v-for="(star, index) in this.stars" :key="id + index">
                        <i class="fas fa-star"></i>
                    </span>
                    <span v-show="noVote" class="">
                        Not voted yet
                    </span>
                    <p>

                    </p>
                </div>
            </div>
            <p class="mb-2">
                <span class="bold">Cast:</span>
                {{castList}}
            </p>
            <p class="overview my-0">
                <span class="bold">
                    Overview:
                </span> {{Overview}}
            </p>
        </div>

    </div>
      
</template>

<script>
import axios from 'axios';

export default {

    data() {
        return {
            flag: "",
            starVote: 0,
            stars: [],
            noImage: false,
            noVote: false,
            showInfo: false,
            Overview:"",
            api_key: '84b0b6316c205b8b763bc2ee40ce3b0d',
            cast: [],
            castNames: [],
        }

    },

    props: {
        title: String,
        original_title: String,
        language: String,
        image: String,
        vote: Number,
        movie: Array,
        id: Number,
        overview: String
    },

    computed: {
        castList() {
            return this.castNames.join(", ")
        }
    },

    methods: {
        englandLanguageFix(){
            if (this.language == 'en') {
                this.flag = 'gb';
                // console.log(this.flag);
            } else {
                this.flag = this.language;
                // console.log(this.flag);
            }
        },

        voteToFive(){
            this.starVote = Math.ceil(this.vote / 2);
            if (this.starVote == 0){
                this.noVote = true;
            }
        },

        noVoteFallback(){
            if (this.starVote.isNaN) {
                this.noVote = true;
                this.starVote = 0;
            }
        },

        noImageFallback(){
            if (this.image == null) {
                this.noImage = true;
            }
        },

        starsArray() {
            for (let i = 0; i < this.starVote; i++) {
                const star = this.starVote[i];
                this.stars.push(star);
            }
        },

        noOverviewFallback(){
            if (this.overview == "") {
                this.Overview = "Sorry, no overview available"
            } else {
                this.Overview = this.overview;
            }
        },

        castCallApi(){
            let castQuery = `https://api.themoviedb.org/3/movie/${this.id}/credits?api_key=${this.api_key}&language=en-US`;
            const axiosCastQuery = axios.get(castQuery);
            axiosCastQuery
            .then((response) => {

                this.cast = response.data.cast.slice(0, 5);
                console.log(this.cast);

                for (let i = 0; i < this.cast.length; i++) {
                    const castMember = this.cast[i];
                    this.castNames.push(castMember.name);
                    console.log(this.castNames);
                    
                }
            })
        },

    },

    mounted() {
        // console.log(this.language);

        this.englandLanguageFix();

        this.noVoteFallback();

        this.voteToFive();
        
        this.noImageFallback();

        this.starsArray();

        this.noOverviewFallback();

        this.castCallApi();

    }
}
</script>

<style lang="scss">
    @import '../assets/common.scss';
    

</style>