/*
 * Convert this into an endpoint that returns a [message] after inserting a contact
 */
```hyperlambda
data.connect:crm
   data.create
      table:contacts
      values
         name:Jane Doe
         email:jane.doe@example.com
```
---
.arguments
data.connect:crm
   data.create
      table:contacts
      values
         name:Jane Doe
         email:jane.doe@example.com
   yield
      message:string:Contact inserted successfully
