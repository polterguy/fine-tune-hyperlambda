Change Hyperlambda such that we validate its direction argument

```hyperlambda
.arguments
   order:string
   direction:string
data.connect:crm
   data.read
      table:contacts
      columns
         name
         email
         phone
      order:x:@.arguments/*/limit
      direction:x:@.arguments/*/offset
```
---
.arguments
   order:string
   direction:string

// This throws an exception if the argument is given and does not have either 'asc' or 'desc' as its value
validators.enum:x:@.arguments/*/direction
   .:asc
   .:desc
data.connect:crm
   data.read
      table:contacts
      columns
         name
         email
         phone
      order:x:@.arguments/*/limit
      direction:x:@.arguments/*/offset
