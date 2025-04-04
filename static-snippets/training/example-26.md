Change this Hyperlambda such that its [email] and [phone] arguments are optional

```hyperlambda
.arguments
   contact_id:int
   email:string
   phone:string

// Connecting to the CRM database
data.connect:[generic|crm]
   database-type:sqlite

   // Updating the contact record
   data.update
      database-type:sqlite
      table:contacts
      values
         email:x:@.arguments/*/email
         phone:x:@.arguments/*/phone
      where
         and
            contact_id:x:@.arguments/*/contact_id

   // Returning success to caller
   yield
      message:Contact updated successfully
```
---
.arguments
   contact_id:int
   email:string
   phone:string

// Connecting to the CRM database
data.connect:[generic|crm]
   database-type:sqlite

   // Adding [email] and [name], but only if they were given to the endpoint
   add:x:./*/data.update/*/values
      get-nodes:x:@.arguments/*/email
      get-nodes:x:@.arguments/*/name

   // Updating the contact record
   data.update
      database-type:sqlite
      table:contacts
      values
      where
         and
            contact_id:x:@.arguments/*/contact_id

   // Returning success to caller
   yield
      message:Contact updated successfully
