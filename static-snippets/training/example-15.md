Replace the hardcoded `true` value in the `[if]` with a variable reference

```hyperlambda
.result
if
   .:bool:true
   .lambda
      set-value:x:@.result
         .:Condition is true
```
---
.condition:bool:true
.result
if:x:@.condition
   set-value:x:@.result
      .:Condition is true
