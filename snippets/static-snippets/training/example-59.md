Convert age argument to an integer and assign to temporary variable

```hyperlambda
.arguments
   age:string
```
---
.arguments
   age:string
.temp
set-value:x:@.temp
   convert:x:@.arguments/*/age
      type:int
