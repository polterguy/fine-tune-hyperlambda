Add a [yield] block that returns the final value of [.count]

```hyperlambda
.count:int:0
while
   lt
      get-value:x:@.count
      .:int:2
   .lambda
      math.increment:x:@.count
```
---
.count:int:0
while
   lt
      get-value:x:@.count
      .:int:2
   .lambda
      math.increment:x:@.count
yield
   final-count:x:@.count
