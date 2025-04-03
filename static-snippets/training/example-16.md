Wrap this logic in a conditional that only executes if `.enabled` is true

```hyperlambda
set-value:x:@.result
   .:Executing block
```
---
.enabled:bool:true
if:x:@.enabled
   set-value:x:@.result
      .:Executing block
