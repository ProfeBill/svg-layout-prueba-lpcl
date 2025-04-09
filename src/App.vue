<template>
  <div id="app">
    <button @click="loadMap" ref="loadBtn">Build Map</button>
    <SVGLayout ref="map" location="./img/TableLayout_no_animations.svg" prefix="" idfield="name"
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

  },

  created() {
    this.fetchData();
  },

  mounted() {
    setTimeout(() => {this.loadMap();}, 2000);
  },

  methods : {
    async fetchData() {
      try {
        let response = await fetch("http://l3af-mesites.llego.co/api/l3af-map/chili");
            let data = await response.json();
            /// status_obj = {...data}; 

            this.status = data,
            this.status_map = {
                "empty": "#356bcf",
                "occupied": "#eee539"
              }
      } catch (error) {
        console.error('Error fetching data:', error);
      }
    },

    clicked( e ){
      window.alert( "Selected : " + e.id );
    },
    
    loadMap : async function (){
      await this.fetchData();
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
