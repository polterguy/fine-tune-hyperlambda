Create code that does what my comment says the file does

```hyperlambda
/*
 * Reads artists from chinook database and returns results to caller
 * 
 * Optionally apply filtering on name
 */
.arguments
   name.eq:string
   name.like:string
.type:public
``` 
---
/*
 * Reads artists from chinook database and returns results to caller
 * 
 * Optionally apply filtering on name
 */
.arguments
   name.eq:string
   name.like:string
.type:public
data.connect:chinook

   add:x:+/*/where/*/and
      get-nodes:x:@.arguments/*/name.eq
      get-nodes:x:@.arguments/*/name.like
   data.read
      table:Artist
      where
         and
   return-nodes:x:@data.read/*
