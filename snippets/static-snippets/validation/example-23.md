Change the email argument to become a more than / greater than comparison

```hyperlambda
.arguments
   name.eq:string
   email.eq:string
   phone.eq:string
data.connect:employees
   add:x:@data.connect/*/data.read/*/where/*/and
      get-nodes:x:@.arguments/*/name.eq
      get-nodes:x:@.arguments/*/email.eq
      get-nodes:x:@.arguments/*/phone.eq
   data.read
      table:users
      where
         and
   return-nodes:x:@data.read/*
```
---
.arguments
   name.eq:string
   email.mt:string
   phone.eq:string
data.connect:employees
   add:x:@data.connect/*/data.read/*/where/*/and
      get-nodes:x:@.arguments/*/name.eq
      get-nodes:x:@.arguments/*/email.mt
      get-nodes:x:@.arguments/*/phone.eq
   data.read
      table:users
      where
         and
   return-nodes:x:@data.read/*

