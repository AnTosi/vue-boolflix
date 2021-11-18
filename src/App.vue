<template>
  <div id="app">
    <div class="searchBar">
      
    </div>
    <div class="main">
      <SiteMain />
    </div>
  </div>
</template>

<script>

import SiteMain from './components/SiteMain.vue';

export default {
  name: 'App',
  components: {
    SiteMain
  },
  
  

}
</script>

<style lang="scss">

@import "../node_modules/bootstrap/dist/css/bootstrap-grid.css";
@import "./assets/common.scss";


#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}


</style>
