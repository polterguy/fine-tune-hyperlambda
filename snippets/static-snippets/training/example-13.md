Wrap this code into an endpoint

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
      message:Contact inserted successfully
