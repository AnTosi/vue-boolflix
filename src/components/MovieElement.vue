<template>
        
    <ul class="black_border m-2 height_200">
        <h3>
            {{title}}
        </h3>
        <h5>
            {{original_title}}
        </h5>
        <img v-bind:src="'https://image.tmdb.org/t/p/w154/' + image" alt="">
        <div class="text_left py-2">
            <flag class="px-2" :iso="flag" />
            <span class="px-2">
                {{vote}}
            </span>
        </div>

    </ul>
      
</template>

<script>
export default {

    data() {
        return {
            flag: "",
        }
    },

    props: {
        title: String,
        original_title: String,
        language: String,
        image: String,
        vote: Number,
        movie: Array,
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

    }
}
</script>

<style lang="scss">
    @import '../assets/common.scss';
</style>