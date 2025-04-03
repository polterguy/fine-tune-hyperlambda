Change the the log entry to 'Thomas Hansen was here!'

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
.count:int:0
while
   lt
      get-value:x:@.count
      .:int:10
   .lambda
      log.info:Thomas Hansen was here!
      math.increment:x:@.count
