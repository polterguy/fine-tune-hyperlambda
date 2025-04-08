Convert date argument from string to date and assign to temp variable

```hyperlambda
.arguments
   date:string
.temp
```
---
.arguments
   date:string
.temp
set-value:x:@.temp
   convert:x:@.arguments/*/date
      type:date
