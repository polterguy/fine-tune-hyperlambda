Remove sockets logic

```hyperlambda
.arguments

   // Optional client_id column value
   client_id:long

   // Optional name column value
   name:string

   // Optional email column value
   email:string

   // Optional phone column value
   phone:string

   // Optional address column value
   address:string

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
      return-id:bool:true
      values

   // Returning the correct status code.
   response.status.set:201

   // Publishing socket message.
   add:x:./*/sockets.signal/*/args
      get-nodes:x:@.arguments/*
   add:x:./*/sockets.signal
      get-nodes:x:@auth.ticket.verify
   set-name:x:./*/sockets.signal/*/auth.ticket.verify
      .:roles
   sockets.signal:crm.contacts.post
      args

   // Returning result of above invocation to caller.
   unwrap:x:+/*
   return
      id:x:@data.create
```
---
.arguments

   // Optional client_id column value
   client_id:long

   // Optional name column value
   name:string

   // Optional email column value
   email:string

   // Optional phone column value
   phone:string

   // Optional address column value
   address:string

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
      return-id:bool:true
      values

   // Returning the correct status code.
   response.status.set:201

   // Returning result of above invocation to caller.
   unwrap:x:+/*
   return
      id:x:@data.create
