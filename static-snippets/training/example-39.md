Change the database to sakila and the table to Actor

```hyperlambda
/*
 * This file contains an API endpoint for retrieving contacts from a CRM database.
 * 
 * It requires an 'admin' level user to access, and takes two optional query parameters:
 * - limit: the maximum number of records to return
 * - offset: the number of records to skip before starting to return results
 * 
 * The endpoint connects to a CRM database, reads contacts with the specified limit and offset,
 * and returns the resulting records to the caller.
 */
.arguments
   limit:long
   offset:long

// Ensuring user is authorized to access endpoint.
auth.ticket.verify:admin

// Connecting to CRM database.
data.connect:[generic|crm]
   database-type:sqlite

   // Reading data from database.
   data.read
      database-type:sqlite
      table:contacts
      limit:x:@.arguments/*/limit
      offset:x:@.arguments/*/offset

   // Returning result of above read invocation to caller.
   return-nodes:x:@data.read/*
```
---

/*
 * This file contains an API endpoint for retrieving Actor rows from the sakila database.
 * 
 * It requires an 'admin' level user to access, and takes two optional query parameters:
 * - limit: the maximum number of records to return
 * - offset: the number of records to skip before starting to return results
 * 
 * The endpoint connects to the sakila database, reads Actor rows with the specified limit and offset,
 * and returns the resulting records to the caller.
 */
.arguments
   limit:long
   offset:long
.type:public

// Ensuring user is authorized to access endpoint.
auth.ticket.verify:admin

// Connecting to sakila database.
data.connect:[generic|sakila]
   database-type:sqlite

   // Reading data from database.
   data.read
      database-type:sqlite
      table:Actor
      limit:x:@.arguments/*/limit
      offset:x:@.arguments/*/offset

   // Returning result of above read invocation to caller.
   return-nodes:x:@data.read/*
