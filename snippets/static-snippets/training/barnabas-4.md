Rename the [.count] variable to [.total]

```hyperlambda
.count:int:0
while
   lt
      get-value:x:@.count
      .:int:3
   .lambda
      log.info:Tick
      math.increment:x:@.count
```
---
.total:int:0
while
   lt
      get-value:x:@.total
      .:int:3
   .lambda
      log.info:Tick
      math.increment:x:@.total
