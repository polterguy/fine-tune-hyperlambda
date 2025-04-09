Remove the last 3 filtering arguments

```hyperlambda
.arguments

   // Fully qualified name of column to order by, must be in TABLE_NAME.COLUMN_NAME format
   order:string

   // What direction to order, can be 'asc' or 'desc' implying ascending and descending
   direction:string

   // Optional filtering arguments dynamically added to below [where] becoming conditions.
   contacts.contact_id.eq:long
   contacts.first_name.like:string
   contacts.first_name.eq:string
   contacts.last_name.like:string
   contacts.last_name.eq:string
   contacts.email.like:string
   contacts.email.eq:string
   contacts.phone.like:string
   contacts.phone.eq:string
   contacts.position.like:string
   contacts.position.eq:string
   contacts.company_id.eq:long

// Opening up our database connection.
data.connect:erp

   // Parametrising our read invocation with ordering arguments if specified.
   add:x:./*/data.read
      get-nodes:x:@.arguments/*/order
      get-nodes:x:@.arguments/*/direction
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
```
---
.arguments

   // Fully qualified name of column to order by, must be in TABLE_NAME.COLUMN_NAME format
   order:string

   // What direction to order, can be 'asc' or 'desc' implying ascending and descending
   direction:string

   // Optional filtering arguments dynamically added to below [where] becoming conditions.
   contacts.contact_id.eq:long
   contacts.first_name.like:string
   contacts.first_name.eq:string
   contacts.last_name.like:string
   contacts.last_name.eq:string
   contacts.email.like:string
   contacts.email.eq:string
   contacts.phone.like:string
   contacts.phone.eq:string

// Opening up our database connection.
data.connect:erp

   // Parametrising our read invocation with ordering arguments if specified.
   add:x:./*/data.read
      get-nodes:x:@.arguments/*/order
      get-nodes:x:@.arguments/*/direction
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
