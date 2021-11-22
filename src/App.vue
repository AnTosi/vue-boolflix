<template>
  <div id="app">
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
@import "./assets/variables.scss";


#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  // text-align: center;
  color: #2c3e50;
  // margin-top: 60px;
}

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  background-color:  $main-grey;
  
}
</style>
