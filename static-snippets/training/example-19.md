Change this code such that it continues until [.count] equals 5

```hyperlambda
.count:int:0
while
   lt
      get-value:x:@.count
      .:int:3
   .lambda
      log.info:Hello World
      math.increment:x:@.count
```
---
.count:int:0
while
   lt
      get-value:x:@.count
      .:int:5
   .lambda
      log.info:Hello World
      math.increment:x:@.count
