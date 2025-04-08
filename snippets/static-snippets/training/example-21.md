Change the name of the count variable such that it's named iterations

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
.iterations:int:0
while
   lt
      get-value:x:@.iterations
      .:int:10
   .lambda
      log.info:Hello World
      math.increment:x:@.iterations
