Change the loop so it logs every even number between 0 and 6

```hyperlambda
.count:int:0
while
   lt
      get-value:x:@.count
      .:int:6
   .lambda
      log.info:Logging
      math.increment:x:@.count
```
---
.count:int:0
while
   lt
      get-value:x:@.count
      .:int:6
   .lambda
      if
         eq
            math.modulo
               get-value:x:@.count
               .:int:2
            .:int:0
         .lambda
            log.info:x:@.count
      math.increment:x:@.count
