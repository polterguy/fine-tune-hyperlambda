/*
 * Wrap this logic so that it only runs if [.execute] is true
 */
set-value:x:@.status
   .:complete
---
.execute:bool:true
if:x:@.execute
   set-value:x:@.status
      .:complete
