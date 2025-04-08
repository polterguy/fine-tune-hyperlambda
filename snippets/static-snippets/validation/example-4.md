How do I change this code such that it can only be executed by an admin user?

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
auth.ticket.verify:admin
strings.concat
   .:"Hello "
   get-value:x:@.arguments/*/name
   .:" you are "
   get-value:x:@.arguments/*/age
   .:" years old"
yield
   result:x:@strings.concat
