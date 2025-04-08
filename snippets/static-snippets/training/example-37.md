Remove arguments

```hyperlambda
.arguments
   department.eq:string
   location.eq:string
data.connect:erp
   add:x:./*/data.read/*/where/*/and
      get-nodes:x:@.arguments/*
   data.read
      table:contacts
      where
         and
```
---
.arguments
data.connect:erp
   data.read
      table:contacts
