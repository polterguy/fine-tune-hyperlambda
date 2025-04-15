Wrap this logic so that it only runs if [.execute] is true

```hyperlambda
set-value:x:@.status
   .:complete
```
---
if:x:@.execute
   set-value:x:@.status
      .:complete
