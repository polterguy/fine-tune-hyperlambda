Make all arguments mandatory

```hyperlambda
.arguments

   // Optional name column value
   name:string

   // Optional email column value
   email:string

   // Optional phone column value
   phone:string

// Verifying user is authorized to access endpoint.
auth.ticket.verify:root

// Opening up database connection.
data.connect:crm

   // Parametrising our create invocation.
   add:x:./*/data.create/*/values
      get-nodes:x:@.arguments/*

   // Creating our record.
   data.create
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

   // Mandatory name column value
   name:string

   // Mandatory email column value
   email:string

   // Mandatory phone column value
   phone:string

// Verifying user is authorized to access endpoint.
auth.ticket.verify:root

// Making sure arguments are provided.
validators.mandatory:x:@.arguments/*/name
validators.mandatory:x:@.arguments/*/email
validators.mandatory:x:@.arguments/*/phone

// Opening up database connection.
data.connect:crm

   // Creating our record.
   data.create
      table:contacts
      values
         name:x:@.arguments/*/name
         email:x:@.arguments/*/email
         phone:x:@.arguments/*/phone

   // Returning the correct status code.
   response.status.set:201

   // Returning result of above invocation to caller.
   yield
      id:x:@data.create
