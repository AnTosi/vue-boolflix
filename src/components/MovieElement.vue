<template>
        
    <ul class="black_border m-2 height_200">
        <li>
            {{title}}
        </li>
        <li>
            {{original_title}}
        </li>
        <li>
            {{language}}
        </li>
        <li>
            {{vote}}
        </li>            
    </ul>
      
</template>

<script>
export default {
    props: {
        title: String,
        original_title: String,
        language: String,
        vote: Number,
    }
}
</script>

<style lang="scss">
    @import '../assets/common.scss'
</style>