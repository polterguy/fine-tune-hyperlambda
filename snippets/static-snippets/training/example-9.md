Add authorization requirements for admin and partner users

```hyperlambda
.arguments
   name:string
   age:int

strings.concat
   .:"Hello "
   get-value:x:@.arguments/*/name
   .:" you are "
   get-value:x:@.arguments/*/age
   .:" years old"

yield
   result:x:@strings.concat
```
---
.arguments
   name:string
   age:int

auth.ticket.verify:admin,partners

strings.concat
   .:"Hello "
   get-value:x:@.arguments/*/name
   .:" you are "
   get-value:x:@.arguments/*/age
   .:" years old"

yield
   result:x:@strings.concat
