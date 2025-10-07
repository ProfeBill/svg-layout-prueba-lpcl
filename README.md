Estamos haciendo pruebas en clase de Código Limpio


# svg-layout

## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```

### Lints and fixes files
```
npm run lint
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).




# Requisites:

The following funcionality is needed on l3af backend in order to build the Table Layout feature:

## Table Status Service

L3af must provide a web service that retuns all the tables in restaurant for the current logged in user.

The returned JSON must have this structure:
```
[
    {
        "id": "ID for the table",
        "capacity": "Number of seats on the table",
        "customer_count": "Number of patrons currently using the table ",
        "table_status" : "Table status (see list of posible values below)",
        "order_status": "Current order status (see list below)"
    },
    .....
]

}
```

The possible values for `table_status` could be (but are not limited to) this list:
- empty: Table is empty and available for new customers.
- occupied: Table is occupied and asigned to other user.
- checkout: Occupants at the table are in the process of paying the bill. This occurs when the user presses the pre-checkout button on the checkout screen.
- assigned: Table is under the direct care of the user logged into the system, highlighting their specific responsibilities.
- not_available: The table cannot be used

The possible values for `order_status` field could be (but are not limited to) this list:
- no_order : No order taken for this table yet
- submitted : The order has been submited and waiting for BKS confirmation
- cooking : The order has been received by the BKS and preparation started
- ready : The order preparation is complete at BKS and ready to be served
- delivered : The order has been served to the table

## Table layout file storage

The table layout is an SVG file designed for the restaurant and needs to be stored on the L3AF server 
in order to be used. So the funcionality for the configuration of Table Layout must allow the 
administrative user, to upload the SVG file and store it on the server.

A web service must be available to access the SVG file to be displayed on Table Layout feature. 

# Functionality

The Table Layout functionality is a custom Vue.js widget that displays the SVG table layout file, 
and then applies the status information on the Table Status JSON service, to reflect it visually.

The Vue.js widget has the following properties, methods and events:

## Properties

- location : URL of the SVG table layout file
- status : table status data obtained with the Table Status Service
- table-statuses : A Dictionary with the styles for each of the possible table_status values
- order-statuses : A Dictionary with the styles to be applied on every order status value

## Events
- table-selected : Trigered when the user selects a table on the screen

## Methods
- updateStatus( status_object )  : Updates all tables with a full status JSON object for all tables
- updateTable( table_id, table_status, order_status ) : Updates the status of only one Table, given its ID
