/*
 * Change the log message to 'Looping started'
 */
```hyperlambda
.count:int:0
while
   lt
      get-value:x:@.count
      .:int:3
   .lambda
      log.info:Init loop
      math.increment:x:@.count
```
---
.count:int:0
while
   lt
      get-value:x:@.count
      .:int:3
   .lambda
      log.info:Looping started
      math.increment:x:@.count
