<template>
        
    <ul>
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
    ul {
        list-style: none;
    }
</style>