Remove position

```hyperlambda
.arguments

   // Optional name column value
   name:string

   // Optional email column value
   email:string

   // Optional phone column value
   phone:string

   // Optional position column value
   position:string

// Verifying user is authorized to access endpoint.
auth.ticket.verify:root,admin

// Opening up database connection.
data.connect:[generic|crm]
   database-type:sqlite

   // Parametrising our create invocation.
   add:x:./*/data.create/*/values
      get-nodes:x:@.arguments/*

   // Creating our record.
   data.create
      database-type:sqlite
      table:contacts
      values

   // Returning the correct status code.
   response.status.set:201

   // Returning result of above invocation to caller.
   yield
      id:x:@data.create
``` 
---
.arguments

   // Optional name column value
   name:string

   // Optional email column value
   email:string

   // Optional phone column value
   phone:string

// Verifying user is authorized to access endpoint.
auth.ticket.verify:root,admin

// Opening up database connection.
data.connect:[generic|crm]
   database-type:sqlite

   // Parametrising our create invocation.
   add:x:./*/data.create/*/values
      get-nodes:x:@.arguments/*

   // Creating our record.
   data.create
      database-type:sqlite
      table:contacts
      values

   // Returning the correct status code.
   response.status.set:201

   // Returning result of above invocation to caller.
   yield
      id:x:@data.create
