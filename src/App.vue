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
  data : async function(){
    let status_obj = {};

   /* {

          "1" : {
            
            "capacity": 4,
            "customer_count": 2,
            "table_status" : "empty",
            "order_status": "no_order"
        },
        "2" :
        {
            "capacity": 4,
            "customer_count": 3,
            "table_status" : "occupied",
            "order_status": "cooking"
        }

      } */

    let response = await fetch("https://pos.vizipp.com/pos/tables");
    let data = await response.json();
    status_obj = (data);

    return {

    status : status_obj,
      // eslint-disable-next-line 
      status_map : {
        "empty": "cyan",
        "occupied": "yellow"
      }

  }; },
  methods : {
    clicked( e ){
      window.alert( "Selected : " + e.id );
    },
    
    loadMap : function (){
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
