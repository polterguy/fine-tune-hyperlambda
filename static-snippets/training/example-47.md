 Change it such that limit and offset have default values being 10 and 0

```hyperlambda
/*
 * Reads artists from chinook database and returns results to caller
 */
.arguments
   limit:long
   offset:long
.type:public
data.connect:chinook
   data.read
      table:Artist
      limit:x:@.arguments/*/limit
      offset:x:@.arguments/*/offset
   return-nodes:x:@data.read/*
``` 
---
/*
 * Reads artists from chinook database and returns results to caller
 *
 * Limit defaults to 10 unless specified and offset defaults to 0
 */
.arguments
   limit:long
   offset:long
.type:public
validators.default:x:@.arguments
   limit:long:10
   offset:long:0
data.connect:chinook
   data.read
      table:Artist
      limit:x:@.arguments/*/limit
      offset:x:@.arguments/*/offset
   return-nodes:x:@data.read/*
