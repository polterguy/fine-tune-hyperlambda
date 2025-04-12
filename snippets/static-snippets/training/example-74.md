Change it such that it creates a log entry after it's done inserting the record

```hyperlambda
.arguments

   // name column value
   name:string

   // email column value
   email:string

   // phone column value
   phone:string

// Verifying user is authorized to access endpoint.
auth.ticket.verify:root,admin

// Sanity checking invocation.
validators.mandatory:x:@.arguments/*/name
validators.mandatory:x:@.arguments/*/email
validators.mandatory:x:@.arguments/*/phone

// Opening up our database connection.
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
      id:x:@data.create/*

``` 
---
.arguments

   // name column value
   name:string

   // email column value
   email:string

   // phone column value
   phone:string

// Verifying user is authorized to access endpoint.
auth.ticket.verify:root,admin

// Sanity checking invocation.
validators.mandatory:x:@.arguments/*/name
validators.mandatory:x:@.arguments/*/email
validators.mandatory:x:@.arguments/*/phone

// Opening up our database connection.
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

   // Logging invocation
   log.info:Contact successfully created
      id:x:@data.create/*
      name:x:@.arguments/*/name
      email:x:@.arguments/*/email
      phone:x:@.arguments/*/phone

   // Returning the correct status code.
   response.status.set:201

   // Returning result of above invocation to caller.
   yield
      id:x:@data.create/*

