/*
 * Add a dynamic calculation where the result is base^exponent
 */
.base:int:2
.exponent:int:3
---
.base:int:2
.exponent:int:3
math.power
   get-value:x:@.base
   get-value:x:@.exponent
