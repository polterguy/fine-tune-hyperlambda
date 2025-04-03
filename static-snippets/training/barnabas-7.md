/*
 * Replace hardcoded [true] condition with [.should-run] variable
 */
```hyperlambda
.result
if
   .:bool:true
   .lambda
      set-value:x:@.result
         .:Running
```
---
.should-run:bool:true
.result
if:x:@.should-run
   set-value:x:@.result
      .:Running
