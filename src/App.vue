<template>
  <div id="app">
    
    <SVGLayout location="./img/sample-layout.svg" v-bind:status="status" v-bind:status_map="status_map" v-on:select="clicked"/>
  </div>
</template>

<script>
import SVGLayout from './components/SVGLayout.vue'

export default {
  name: 'App',
  components: {
    SVGLayout
  },
  data : function(){ return {

    status :  {
          "TABLE_1" : {
            
            "capacity": 4,
            "customer_count": 2,
            "table_status" : "empty",
            "order_status": "no_order"
        },
        "TABLE_2" :
        {
            "capacity": 4,
            "customer_count": 3,
            "table_status" : "occupied",
            "order_status": "cooking"
        }

      },

      // eslint-disable-next-line 
      status_map : {
        "empty": "cyan",
        "occupied": "yellow"
      }

  }; },
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
