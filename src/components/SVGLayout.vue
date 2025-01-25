<template>
   <div class="hello">
    <svg width="200" height="200">
      <circle cx="100" cy="100" r="50" stroke="black" stroke-width="3" fill="red" />
    </svg>
  </div>
</template>

<script>
export default {
  name: 'SVGLayout',
  props: {
    location : String, // URL of the SVG table layout file
    status : Object, // table status data obtained with the Table Status Service
    table_statuses : Object, // A Dictionary with the styles for each of the possible table_status values
    order_statuses : Object // A Dictionary with the styles to be applied on every order status value 
  },

/*  Events
table-selected : Trigered when the user selects a table on the screen
*/
  methods : {
/*    updateStatus( status_object ) {},   // Updates all tables with a full status JSON object for all tables
    updateTable( table_id, table_status, order_status ) {}  // Updates the status of only one Table, given its ID */
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
