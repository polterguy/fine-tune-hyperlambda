/*
 * Add an [else] clause that handles when .is-admin is false
 */
```hyperlambda
.is-admin:bool:true
.response
if:x:@.is-admin
   set-value:x:@.response
      .:Access granted
```
---
.is-admin:bool:true
.response
if:x:@.is-admin
   set-value:x:@.response
      .:Access granted
else
   set-value:x:@.response
      .:Access denied
