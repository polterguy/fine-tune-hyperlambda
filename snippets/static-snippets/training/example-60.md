Convert age argument to an integer and assign to temporary variable

```hyperlambda
.arguments
   name:string
   email:string
   phone:string
   address:string

// Opening up our database connection.
data.connect:crm

   // Parametrising our create invocation.
   add:x:./*/data.create/*/values
      get-nodes:x:@.arguments/*

   // Creating our record.
   data.create
      table:contacts
      values

   // Returning result of above invocation to caller.
   unwrap:x:+/*
   return
      id:x:@data.create
```
---
.arguments
   name:string
   email:string
   phone:string
   address:string

// Opening up our database connection.
data.connect:crm

   // Parametrising our create invocation.
   add:x:./*/data.create/*/values
      get-nodes:x:@.arguments/*

   // Creating our record.
   data.create
      table:contacts
      values

   // Returning result of above invocation to caller.
   yield
      id:x:@data.create
