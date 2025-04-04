/*
 * Create a loop that multiplies a value by 2 on each iteration, starting from 1 and looping 4 times
 */
.result:int:1
---
.count:int:0
.result:int:1
while
   lt
      get-value:x:@.count
      .:int:4
   .lambda
      math.multiply
         get-value:x:@.result
         .:int:2
      set-value:x:@.result
         x:@math.multiply
      math.increment:x:@.count
