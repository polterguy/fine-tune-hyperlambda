Make it such that order and direction are mandatory

```hyperlambda
.arguments
   order:string
   direction:string
   offset:int
   limit:int

// Connecting to the "chinook" database and reading from the "Album" table.
data.connect:chinook

   // Adding sorting if specified.
   add:x:@data.connect/*/data.read
      get-nodes:x:@.arguments/*/order
      get-nodes:x:@.arguments/*/direction
   remove-nodes:x:@.arguments/*/order
   remove-nodes:x:@.arguments/*/direction

   // Adding paging if specified.
   add:x:@data.connect/*/data.read
      get-nodes:x:@.arguments/*/offset
      get-nodes:x:@.arguments/*/limit
   remove-nodes:x:@.arguments/*/offset
   remove-nodes:x:@.arguments/*/limit

   // Reading data from the "Album" table.
   data.read
      table:Album

   // Returning the result of the read operation to the caller.
   return-nodes:x:@data.read/*
```
---
.arguments
   order:string
   direction:string
   offset:int
   limit:int

// Making sure [order] and [direction] was supplied
validators.mandatory:x:@.arguments/*/order
validators.mandatory:x:@.arguments/*/direction

// Connecting to the "chinook" database and reading from the "Album" table.
data.connect:chinook

   // Adding sorting if specified.
   add:x:@data.connect/*/data.read
      get-nodes:x:@.arguments/*/offset
      get-nodes:x:@.arguments/*/limit
   remove-nodes:x:@.arguments/*/offset
   remove-nodes:x:@.arguments/*/limit

   // Reading data from the "Album" table.
   data.read
      table:Album
      order:x:@.arguments/*/order
      direction:x:@.arguments/*/direction

   // Returning the result of the read operation to the caller.
   return-nodes:x:@data.read/*
