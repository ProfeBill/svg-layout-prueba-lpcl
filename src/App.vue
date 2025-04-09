<template>
  <div id="app">
    <button @click="loadMap" ref="loadBtn">Build Map</button>
    <!-- 
    
    SVGLayout component usage:
    
    location: change this to the customer table map file URL
    idfield: is the field on the status web service that will be matched to the ids on the SVG
    v-on:select :  Event handler function to be called when user clicks on a table
    -->
    <SVGLayout ref="map" location="./img/TableLayout_no_animations.svg" prefix="" idfield="name"
    v-bind:status="status" v-bind:status_map="status_map" v-on:select="clicked" />
  </div>
</template>

<script>
/****************
Import Table Map component from local folder
****************/
import SVGLayout from './components/SVGLayout.vue'

export default {
  name: 'App',
  components: {
    SVGLayout
  },
  data : function(){
    /****************
    Data object for table map.
    Properties status and status_map are the minimum required
    ****************/
    let res = {
      status : [],
      status_map : {
      }
    }; 
    return res; 

  },

  mounted() {
    /****************
    Allow some time for DOM rendering after Vue is loaded
    ****************/    
    setTimeout(() => {this.loadMap();}, 500);
  } ,

  methods : {
    
    loadMap : async function (){

      /*********
      Setup table map on component loaded
      This function has to be called to update the table map visualization
      *********/      
      await this.fetchData();
      this.$forceUpdate();
      this.$refs["map"].update() ;
    },

    async fetchData() {
      /*********
      Setup table map on component loaded
      *********/       
      try {
        // ******* Status Service URL: change this to the table status web service location
        // may need CoRS configuration
        let status_url = "http://l3af-mesites.llego.co/api/l3af-map/chili";
        let response = await fetch(status_url);
            let data = await response.json();
            /// status_obj = {...data}; 

            this.status = data,
            // ***** Color configuration for each status
            this.status_map = {
                "empty": "#356bcf",
                "occupied": "#eee539"
              }
      } catch (error) {
        console.error('Error fetching data:', error);
      }
    },

    clicked( e ){
      /*********
      This function is the event handler for click event on Tables
      e.id contains the identifier for the clicked table
      *********/        
      window.alert( "Selected : " + e.id );
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
