Remove the operator argument

```hyperlambda
.arguments

   // Number of records to return, defaults to 25 if not specified. Pass in -1 to return all records.
   limit:long

   // Offset into the dataset of where to start retrieving records
   offset:long

   // Fully qualified name of column to order by, must be in TABLE_NAME.COLUMN_NAME format
   order:string

   // What direction to order, can be 'asc' or 'desc' implying ascending and descending
   direction:string

   // Optional logical operator for filtering arguments, can be either 'or' or 'and'. Defaults to and.
   operator:string

   /*
    * Optional filtering arguments.
    * 
    * Since these are added to [where] condition using [add], these arguments are optional
    */
   contacts.contact_id.mt:long
   contacts.contact_id.lt:long
   contacts.contact_id.mteq:long
   contacts.contact_id.lteq:long
   contacts.contact_id.neq:long
   contacts.contact_id.eq:long
   contacts.first_name.like:string
   contacts.first_name.mt:string
   contacts.first_name.lt:string
   contacts.first_name.mteq:string
   contacts.first_name.lteq:string

// Sanity checking invocation.
validators.enum:x:@.arguments/*/operator
   .:or
   .:and

/*
 * Checking if user supplied an [operator] argument, and if so
 * changing the boolean operator for comparison operations.
 */
if
   exists:x:@.arguments/*/operator
   .lambda

      // User provided a boolean comparison [operator] argument.
      set-name:x:../*/data.connect/*/data.read/*/where/0
         get-value:x:@.arguments/*/operator
      remove-nodes:x:@.arguments/*/operator

// Opening up our database connection.
data.connect:[generic|crm]
   database-type:sqlite

   // Parametrising our read invocation with ordering arguments if specified.
   add:x:./*/data.read
      get-nodes:x:@.arguments/*/order
      get-nodes:x:@.arguments/*/direction
   remove-nodes:x:@.arguments/*/order
   remove-nodes:x:@.arguments/*/direction

   // Parametrising our read invocation with paging arguments if specified.
   add:x:./*/data.read
      get-nodes:x:@.arguments/*/limit
      get-nodes:x:@.arguments/*/offset
   remove-nodes:x:@.arguments/*/limit
   remove-nodes:x:@.arguments/*/offset

   // Parametrising our read invocation with filtering arguments.
   add:x:./*/data.read/*/where/*
      get-nodes:x:@.arguments/*

   // Reading data from database.
   data.read
      database-type:sqlite
      table:contacts
      columns
         contacts.contact_id
         contacts.first_name
         contacts.last_name
         contacts.email
         contacts.phone
         contacts.address
      where
         and

   // Returning result of above read invocation to caller.
   return-nodes:x:@data.read/*
```
---
.arguments

   // Number of records to return, defaults to 25 if not specified. Pass in -1 to return all records.
   limit:long

   // Offset into the dataset of where to start retrieving records
   offset:long

   // Fully qualified name of column to order by, must be in TABLE_NAME.COLUMN_NAME format
   order:string

   // What direction to order, can be 'asc' or 'desc' implying ascending and descending
   direction:string

   /*
    * Optional filtering arguments.
    * 
    * Since these are added to [where] condition using [add], these arguments are optional
    */
   contacts.contact_id.mt:long
   contacts.contact_id.lt:long
   contacts.contact_id.mteq:long
   contacts.contact_id.lteq:long
   contacts.contact_id.neq:long
   contacts.contact_id.eq:long
   contacts.first_name.like:string
   contacts.first_name.mt:string
   contacts.first_name.lt:string
   contacts.first_name.mteq:string
   contacts.first_name.lteq:string

// Opening up our database connection.
data.connect:[generic|crm]
   database-type:sqlite

   // Parametrising our read invocation with ordering arguments if specified.
   add:x:./*/data.read
      get-nodes:x:@.arguments/*/order
      get-nodes:x:@.arguments/*/direction
   remove-nodes:x:@.arguments/*/order
   remove-nodes:x:@.arguments/*/direction

   // Parametrising our read invocation with paging arguments if specified.
   add:x:./*/data.read
      get-nodes:x:@.arguments/*/limit
      get-nodes:x:@.arguments/*/offset
   remove-nodes:x:@.arguments/*/limit
   remove-nodes:x:@.arguments/*/offset

   // Parametrising our read invocation with filtering arguments.
   add:x:./*/data.read/*/where/*
      get-nodes:x:@.arguments/*

   // Reading data from database.
   data.read
      database-type:sqlite
      table:contacts
      columns
         contacts.contact_id
         contacts.first_name
         contacts.last_name
         contacts.email
         contacts.phone
         contacts.address
      where
         and

   // Returning result of above read invocation to caller.
   return-nodes:x:@data.read/*
