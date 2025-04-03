/*
 * Wrap this into a [while] loop that runs 4 times
 */
log.info:Running iteration
---
.count:int:0
while
   lt
      get-value:x:@.count
      .:int:4
   .lambda
      log.info:Running iteration
      math.increment:x:@.count
