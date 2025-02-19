<template>
  <div id="app">
    <button @click="loadMap">Build Map</button>
    <SVGLayout ref="map" location="./img/sample-layout-bg.svg" prefix="TABLE_"
    v-bind:status="status" v-bind:status_map="status_map" v-on:select="clicked" />
  </div>
</template>

<script>
import SVGLayout from './components/SVGLayout.vue'

export default {
  name: 'App',
  components: {
    SVGLayout
  },
  data : function(){
    
    let res = {
      status : [],
      status_map : {
        "empty": "cyan",
        "occupied": "yellow"
      }
    }; 
    return res; 
    // return {};
  },

  created() {
    this.fetchData();
  },

  methods : {
    async fetchData() {
      try {
        let response = await fetch("http://l3af-mesites.llego.co/api/l3af-map/chili");
            let data = await response.json();
            /// status_obj = {...data}; 

            this.status = data,
            this.status_map = {
                "empty": "cyan",
                "occupied": "yellow"
              }
      } catch (error) {
        console.error('Error fetching data:', error);
      }
    },

    clicked( e ){
      window.alert( "Selected : " + e.id );
    },
    
    loadMap : function (){
      this.$forceUpdate();
      this.$refs["map"].update() ;
    },


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
