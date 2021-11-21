<template>
        
    <div  @mouseover="showInfo = true" @mouseleave="showInfo=false" class="m-2 element">
        <div v-show="!showInfo" class="image">
            <img v-show="!noImage" v-bind:src="'https://image.tmdb.org/t/p/w342/' + image" alt="">
            <img class="fallback_image" v-show="noImage" alt="">
        </div>

        <div v-show="showInfo" class="info">
            <h3>
                {{title}}
            </h3>
            <h5>
                {{original_title}}
            </h5>
            <div class="text_left py-2">
                <flag class="px-2" :iso="flag" />
                <span v-for="(star, index) in this.stars" :key="id + index">
                    <i class="fas fa-star"></i>
                </span>
                <span v-show="noVote" class="">
                    Not voted
                </span>
            </div>
            <p class="overview">
                <span class="bold">
                    Overview:
                </span> {{overview}}
            </p>
        </div>

    </div>
      
</template>

<script>
export default {

    data() {
        return {
            flag: "",
            starVote: 0,
            stars: [],
            noImage: false,
            noVote: false,
            showInfo: false,
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
        }
    },

    mounted() {
        // console.log(this.language);

        this.englandLanguageFix();

        this.noVoteFallback();

        this.voteToFive();
        
        this.noImageFallback();

        this.starsArray();

    }
}
</script>

<style lang="scss">
    @import '../assets/common.scss';
    
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
        }

    }
    
    h3 {
        margin-top: 0;
        padding-top: 3rem;
    }


</style>