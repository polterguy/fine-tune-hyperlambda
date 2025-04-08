Change the following code such that it also created a log entry

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
strings.concat
   .:"Hello "
   get-value:x:@.arguments/*/name
   .:" you are "
   get-value:x:@.arguments/*/age
   .:" years old"
log.info:Endpoint invoked!
yield
   result:x:@strings.concat
