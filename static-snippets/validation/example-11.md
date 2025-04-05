Generate Hyperlambda code that does what the comment says

```hyperlambda
/*
 * An HTTP endpoint that connects to our CRM database and returns name and email from contacts
 */
```
---
/*
 * An HTTP endpoint that connects to our CRM database and returns name and email from contacts
 */
.arguments

data.connect:CRM
   data.read
      table:contacts
      columns
         name
         email
   yield
      rows:x:@data.read/*
