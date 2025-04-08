Convert this into an endpoint that returns a [message] after inserting a contact

```hyperlambda
data.connect:crm
   data.create
      table:contacts
      values
         name:Jane Doe
         email:jane.doe@example.com
```
---
/*
 * HTTP endpoint returning contacts from crm database
 */
.arguments
data.connect:crm
   data.create
      table:contacts
      values
         name:Jane Doe
         email:jane.doe@example.com
   yield
      message:string:Contact inserted successfully
