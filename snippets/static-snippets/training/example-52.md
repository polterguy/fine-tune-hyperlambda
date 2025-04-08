Make my filter arguments optional

```hyperlambda
/*
 * Reads artists from chinook database and returns results to caller
 */
.arguments
   name:string
   email:string
.type:public
data.connect:some_db

   data.read
      table:some_table
      where
         and
            name.like:x:@.arguments/*/name
            email.like:x:@.arguments/*/email
   return-nodes:x:@data.read/*
``` 
---
/*
 * Reads artists from chinook database and returns results to caller
 * 
 * Optionally apply filtering on name and email
 */
.arguments
   name.like:string
   email.like:string
.type:public
data.connect:some_db

   add:x:+/*/where/*/and
      get-nodes:x:@.arguments/*/name.like
      get-nodes:x:@.arguments/*/email.like
   data.read
      table:some_table
      where
         and
   return-nodes:x:@data.read/*
