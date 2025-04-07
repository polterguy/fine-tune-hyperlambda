 Generate code implementing my comment

```hyperlambda
/*
 * Reads artists from chinook database and returns results to caller
 * 
 * Optionally apply paging arguments
 */
.arguments
   limit:long
   offset:long
.type:public
``` 
---
/*
 * Reads artists from chinook database and returns results to caller
 * 
 * Optionally apply paging arguments
 */
.arguments
   limit:long
   offset:long
.type:public
data.connect:chinook

   add:x:+
      get-nodes:x:@.arguments/*/limit
      get-nodes:x:@.arguments/*/offset
   data.read
      table:Artist
   return-nodes:x:@data.read/*
