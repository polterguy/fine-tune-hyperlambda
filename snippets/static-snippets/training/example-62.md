Change it such that I can use wild cards on name column

```hyperlambda
.arguments
   name.eq:string
   email.eq:string
   phone.eq:string

// Connect to the employees database.
data.connect:employees
   database-type:sqlite

   // Add filtering arguments to [data.read] dynamically.
   add:x:./*/data.read/*/where/*
      get-nodes:x:@.arguments/*

   // Read data from the employees table.
   data.read
      database-type:sqlite
      table:employees
      where
         and

   // Return the result of the read operation to the caller.
   return-nodes:x:@data.read/*
```
---
.arguments
   name.like:string
   email.eq:string
   phone.eq:string

// Connect to the employees database.
data.connect:employees
   database-type:sqlite

   // Add filtering arguments to [data.read] dynamically.
   add:x:./*/data.read/*/where/*
      get-nodes:x:@.arguments/*

   // Read data from the employees table.
   data.read
      database-type:sqlite
      table:employees
      where
         and

   // Return the result of the read operation to the caller.
   return-nodes:x:@data.read/*
