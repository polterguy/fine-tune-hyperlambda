Modify this code such that it only selects name and email columns

```hyperlambda
// Empty [.arguments] implies endpoint NOT taking arguments at all
.arguments

// Connecting to database.
data.connect:crm

   // Reading data from database.
   data.read
      table:contacts

   // Returning result to caller.
   yield
      contacts:x:@data.read/*
```
---
// Empty [.arguments] implies endpoint NOT taking arguments at all
.arguments

// Connecting to database.
data.connect:crm

   // Reading data from database.
   data.read
      table:contacts
      columns
         name
         email

   // Returning result to caller.
   yield
      contacts:x:@data.read/*
