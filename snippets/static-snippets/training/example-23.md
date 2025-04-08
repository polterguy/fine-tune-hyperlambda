Use [math.decrement] instead

```hyperlambda
.count:int:0
while
   lt
      get-value:x:@.count
      .:int:10
   .lambda
      log.info:Hello World
      math.increment:x:@.count
```
---
.count:int:10
while
   mt
      get-value:x:@.count
      .:int:0
   .lambda
      log.info:Hello World
      math.decrement:x:@.count
