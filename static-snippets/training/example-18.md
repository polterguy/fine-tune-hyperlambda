Wrap this into a [while] loop that continues until [.count] equals 3

```hyperlambda
log.info:Hello World
```
---
.count:int:0
while
   lt
      get-value:x:@.count
      .:int:3
   .lambda
      log.info:Hello World
      math.increment:x:@.count
