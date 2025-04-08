Change the comparison from 'less than' to 'greater than or equal'

```hyperlambda
.value:int:10
if
   lt
      get-value:x:@.value
      .:int:20
   .lambda
      log.info:Low value
```
---
.value:int:10
if
   gte
      get-value:x:@.value
      .:int:20
   .lambda
      log.info:High enough
