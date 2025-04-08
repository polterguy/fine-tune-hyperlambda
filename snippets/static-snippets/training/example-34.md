Change it such that order is not mandatory but is using a default value of 'Title'

```hyperlambda
.arguments
   order:string
   direction:string
   offset:int
   limit:int

// Sanity checking invocation, making sure 'order' was specified.
validators.mandatory:x:@.arguments/*/order

// Adding default [direction] if not specified.
validators.default:x:@.arguments
   direction:asc

// Connecting to the "chinook" database and reading from the "Album" table.
data.connect:chinook

   // Adding sorting.
   add:x:@data.connect/*/data.read
      get-nodes:x:@.arguments/*/order
      get-nodes:x:@.arguments/*/direction
      get-nodes:x:@.arguments/*/offset
      get-nodes:x:@.arguments/*/limit
   remove-nodes:x:@.arguments/*/order
   remove-nodes:x:@.arguments/*/direction
   remove-nodes:x:@.arguments/*/offset
   remove-nodes:x:@.arguments/*/limit

   // Reading data from the "Album" table.
   data.read
      table:Album
      columns
         Title
         ReleaseDate

   // Returning the result of the read operation to the caller.
   return-nodes:x:@data.read/*
```
---
.arguments
   order:string
   direction:string
   offset:int
   limit:int

// Adding default [direction] and [order] if not specified.
validators.default:x:@.arguments
   direction:asc
   order:Title

// Connecting to the "chinook" database and reading from the "Album" table.
data.connect:chinook

   // Adding sorting.
   add:x:@data.connect/*/data.read
      get-nodes:x:@.arguments/*/order
      get-nodes:x:@.arguments/*/direction
      get-nodes:x:@.arguments/*/offset
      get-nodes:x:@.arguments/*/limit
   remove-nodes:x:@.arguments/*/order
   remove-nodes:x:@.arguments/*/direction
   remove-nodes:x:@.arguments/*/offset
   remove-nodes:x:@.arguments/*/limit

   // Reading data from the "Album" table.
   data.read
      table:Album
      columns
         Title
         ReleaseDate

   // Returning the result of the read operation to the caller.
   return-nodes:x:@data.read/*
