Create code that does what my comment says the file does

```hyperlambda
/*
 * Reads artists from db database and people table and returns results to caller
 */
.arguments
.type:public
``` 
---
/*
 * Reads artists from db database and people table and returns results to caller
 */
.arguments
.type:public
data.connect:db
   data.read
      table:people
      where
         and
   return-nodes:x:@data.read/*
