<template>
  <div id="app">
    
    <SVGLayout location="./img/sample-layout.svg" v-on:select="clicked"/>
  </div>
</template>

<script>
import SVGLayout from './components/SVGLayout.vue'

export default {
  name: 'App',
  components: {
    SVGLayout
  },
  data : function(){ return {}; },
  methods : {
    clicked( e ){
      window.alert( "Selected : " + e.id );
    }
  }

}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
