Implementing my comment

```hyperlambda
/*
 * Reads artists from chinook database and returns results to caller
 * 
 * Optionally apply sorting
 */
.arguments
   order:string
   direction:string
.type:public
``` 
---
/*
 * Reads artists from chinook database and returns results to caller
 * 
 * Optionally apply sorting
 */
.arguments
   order:string
   direction:string
.type:public
data.connect:chinook

   add:x:+
      get-nodes:x:@.arguments/*/order
      get-nodes:x:@.arguments/*/direction
   data.read
      table:Artist
   return-nodes:x:@data.read/*
