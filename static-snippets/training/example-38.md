Remove ordering and create a descriptive file level comment

```hyperlambda
.arguments
   limit:long
   offset:long
   order:string
.type:public

// Connecting to CRM database.
data.connect:[generic|crm]
   database-type:sqlite

   // Reading data from database.
   add:x:./*/data.read
      get-nodes:x:@.arguments/*/limit
      get-nodes:x:@.arguments/*/offset
      get-nodes:x:@.arguments/*/order
   data.read
      database-type:sqlite
      table:contacts
   return-nodes:x:@data.read/*
```
---
/*
 * Returns records from your crm database and its contacts table
 *
 * Optionally apply paging with [limit] and [offset]
 */
.arguments
   limit:long
   offset:long
.type:public

// Connecting to CRM database.
data.connect:[generic|crm]
   database-type:sqlite

   // Reading data from database.
   add:x:./*/data.read
      get-nodes:x:@.arguments/*/limit
      get-nodes:x:@.arguments/*/offset
   data.read
      database-type:sqlite
      table:contacts
   return-nodes:x:@data.read/*
