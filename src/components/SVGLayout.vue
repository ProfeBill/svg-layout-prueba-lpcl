<template>
    <div ref="svgobject" >
    <object alt="Layout" :data="location" type="image/svg+xml">
			Browser not compatible
		</object>    
  </div>
</template>

<script>
export default {
  name: 'SVGLayout',
  model: {
    event: 'select'
  },  
  props: {
    location : String, // URL of the SVG table layout file,
    status : Object,
    status_map : Object
  },

  data(){
    return   {   
    }
  },
  
  beforeMount : function() {
      // this.loadMap();
    },

  methods : {
/*    updateStatus( status_object ) {},   // Updates all tables with a full status JSON object for all tables
    updateTable( table_id, table_status, order_status ) {}  // Updates the status of only one Table, given its ID */

    update : function (){
      this.buildMap( this.$refs["svgobject"]  );
    },

// get the embedded document, if possible
    getContentDocument : function (embeddingElement) {
      if (embeddingElement.contentDocument !== null) {
        return embeddingElement.contentDocument;
      }
      try {
        var svg = embeddingElement.getSVGDocument();
      return svg;
      } catch (e) {
      console.log(e);
      }
      return null;
    },

    // eslint-disable-next-line
    select : function ( e, o ){
      // console.log( "Selecting" );
      // console.log(e);
      let selection = e.target;

      // Find the parent with clickable class
      while( !selection.classList.contains("clickable") && selection.parentNode !== null )
        selection = selection.parentNode;

      if ( selection.id == "" || selection.id == "."  || selection.parentNode == null) 
        // Invalid selection
        return;

      this.$emit( "select", selection )
    },

    // main logic
    buildMap : function (m) {
      let children = m.children;
      let d = this.getContentDocument(children[0]),
      p = d.querySelectorAll('g.clickable');

      for(var i = 0; i < p.length; i++){
        let path = p[i];
        path.addEventListener('click', this.select );

        console.log("Event listening " + path.id);

        // Find status for ID
        let status = this.status[ path.id ];
        // Get style used for that status
        let style = (status) ? this.status_map[ status.table_status ] : null;
        
        if( style  ){
          // console.log("setting style to " + style)
          path.style.fill = style;
        } 
      }
    }


  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
