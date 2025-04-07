Remove sorting

```hyperlambda
.arguments

   // Number of records to return, defaults to 25 if not specified. Pass in -1 to return all records
   limit:long

   // Offset into the dataset of where to start retrieving records
   offset:long

   // Fully qualified name of column to order by, must be in TABLE_NAME.COLUMN_NAME format
   order:string

   // What direction to order, can be 'asc' or 'desc' implying ascending and descending
   direction:string

// Verifying user is authorized to access endpoint.
auth.ticket.verify:guest

// Opening up our database connection.
data.connect:[generic|erp]
   database-type:sqlite

   // Parametrising our read invocation with ordering arguments if specified.
   add:x:./*/data.read
      get-nodes:x:@.arguments/*/order
      get-nodes:x:@.arguments/*/direction
   remove-nodes:x:@.arguments/*/order
   remove-nodes:x:@.arguments/*/direction

   // Parametrising our read invocation with paging arguments if specified.
   add:x:./*/data.read
      get-nodes:x:@.arguments/*/limit
      get-nodes:x:@.arguments/*/offset
   remove-nodes:x:@.arguments/*/limit
   remove-nodes:x:@.arguments/*/offset

   // Reading data from database.
   data.read
      database-type:sqlite
      table:contacts

   // Returning result of above read invocation to caller.
   return-nodes:x:@data.read/*
```
---
.arguments

   // Number of records to return, defaults to 25 if not specified. Pass in -1 to return all records
   limit:long

   // Offset into the dataset of where to start retrieving records
   offset:long

// Verifying user is authorized to access endpoint.
auth.ticket.verify:guest

// Opening up our database connection.
data.connect:[generic|erp]
   database-type:sqlite

   // Parametrising our read invocation with paging arguments if specified.
   add:x:./*/data.read
      get-nodes:x:@.arguments/*/limit
      get-nodes:x:@.arguments/*/offset
   remove-nodes:x:@.arguments/*/limit
   remove-nodes:x:@.arguments/*/offset

   // Reading data from database.
   data.read
      database-type:sqlite
      table:contacts

   // Returning result of above read invocation to caller.
   return-nodes:x:@data.read/*
