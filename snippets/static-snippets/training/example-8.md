Modify this code such that it requires the user to be authenticated

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

log.info:Endpoint invoked!

yield
   result:x:@strings.concat
```
---
.arguments
   name:string
   age:int

auth.ticket.verify

strings.concat
   .:"Hello "
   get-value:x:@.arguments/*/name
   .:" you are "
   get-value:x:@.arguments/*/age
   .:" years old"

log.info:Endpoint invoked!

yield
   result:x:@strings.concat
