<template>
        
    <ul class="black_border m-2 height_200">
        <li>
            {{title}}
        </li>
        <li>
            {{original_title}}
        </li>
        <li>
            <flag :iso="flag" />
        </li>
        <li>
            {{vote}}
        </li>
        <li>
            {{movie}}
        </li>          
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
        vote: Number,
        movie: Array
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
    @import '../assets/common.scss'
</style>