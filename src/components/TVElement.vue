<template>
        
    <div class="black_border m-2 height_200">
        <h3>
            {{title}}
        </h3>
        <h5>
            {{original_title}}
        </h5>
        <img v-bind:src="'https://image.tmdb.org/t/p/w185/' + image" alt="">
        <img v-show="noImage" src="../assets/JT185.jpg" alt="">
        
        <div class="text_left py-2">
            <flag class="px-2" :iso="flag" />
            <span v-for="(star, index) in this.stars" :key="id + index">
                <i class="fas fa-star"></i>
            </span>
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
        }
    },

    props: {
        title: String,
        original_title: String,
        language: String,
        vote: Number,
        movie: Array,
        image: String,
        id: Number,
    },

    mounted() {
        // console.log(this.language);
        if (this.language == 'en') {
            this.flag = 'gb';
            // console.log(this.flag);
        } else {
            this.flag = this.language;
            // console.log(this.flag);
        }

        this.starVote = Math.ceil(this.vote / 2);
        if (this.starVote.isNaN) {
            this.starVote = 0;
        }

        console.log(this.starVote);

        for (let i = 0; i < this.starVote; i++) {
            const star = this.starVote[i];
            this.stars.push(star);
        }

        if (this.image == null) {
            this.noImage = true;
        }
    }
}
</script>

<style lang="scss">
    @import '../assets/common.scss';
</style>