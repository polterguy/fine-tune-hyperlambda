/*
 * Log an info message after the loop completes
 */
.count:int:0
while
   lt
      get-value:x:@.count
      .:int:2
   .lambda
      math.increment:x:@.count
---
.count:int:0
while
   lt
      get-value:x:@.count
      .:int:2
   .lambda
      math.increment:x:@.count
log.info:Loop completed
