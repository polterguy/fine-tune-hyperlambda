I have the following code:

```hyperlambda
strings.concat
   .:"Hello "
   get-value:x:@.arguments/*/name
   .:" you are "
   get-value:x:@.arguments/*/age
   .:" years old"
```

Wrap the above code into an endpoint and return the result. Do NOT add any comments or explanation
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
yield
   result:x:@strings.concat
