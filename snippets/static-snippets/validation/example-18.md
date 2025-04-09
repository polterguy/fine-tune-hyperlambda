Add an optional filter argument for contact_id

```hyperlambda
.arguments

   // Fully qualified name of column to order by, must be in TABLE_NAME.COLUMN_NAME format
   order:string

   // What direction to order, can be 'asc' or 'desc' implying ascending and descending
   direction:string

// Opening up our database connection.
data.connect:erp

   // Parametrising our read invocation with ordering arguments if specified.
   add:x:./*/data.read
      get-nodes:x:@.arguments/*/order
      get-nodes:x:@.arguments/*/direction

   // Reading data from database.
   data.read
      database-type:sqlite
      table:contacts

   // Returning result of above read invocation to caller.
   return-nodes:x:@data.read/*
```
---
.arguments

   // Fully qualified name of column to order by, must be in TABLE_NAME.COLUMN_NAME format
   order:string

   // What direction to order, can be 'asc' or 'desc' implying ascending and descending
   direction:string

   // Optional filtering arguments dynamically added to below [where] becoming conditions.
   contacts.contact_id.eq:long

// Opening up our database connection.
data.connect:erp

   // Parametrising our read invocation with ordering arguments if specified.
   add:x:./*/data.read
      get-nodes:x:@.arguments/*/order
      get-nodes:x:@.arguments/*/direction

   // Now we have to rmove these from the arguments collection, since we're going to add all remaining arguments to [where]
   remove-nodes:x:@.arguments/*/order
   remove-nodes:x:@.arguments/*/direction

   // Parametrising our read invocation with filtering arguments.
   add:x:./*/data.read/*/where/*
      get-nodes:x:@.arguments/*

   // Reading data from database.
   data.read
      database-type:sqlite
      table:contacts
      where
         and

   // Returning result of above read invocation to caller.
   return-nodes:x:@data.read/*
