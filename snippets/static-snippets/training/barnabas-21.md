Add a condition that only performs addition if [.add-mode] is true

```hyperlambda
math.add
   get-value:int:5
   get-value:int:10
```
---
.add-mode:bool:true
if:x:@.add-mode
   math.add
      get-value:int:5
      get-value:int:10
