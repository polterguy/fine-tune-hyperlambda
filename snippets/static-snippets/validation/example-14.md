Convert age argument to an integer and assign to temp variable

```hyperlambda
.arguments
   age:string
.temp
```
---
.arguments
   age:string
.temp
set-value:x:@.temp
   convert:x:@.arguments/*/age
      type:int
