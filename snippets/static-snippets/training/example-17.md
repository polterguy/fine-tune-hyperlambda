Add an [else] clause to handle the case where `.active` is false

```hyperlambda
.active:bool:true
.message
if:x:@.active
   set-value:x:@.message
      .:User is active
```
---
.active:bool:true
.message
if:x:@.active
   set-value:x:@.message
      .:User is active
else
   set-value:x:@.message
      .:User is inactive
