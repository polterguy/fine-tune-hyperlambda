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

// Connects to our database
data.connect:CRM

   // Reads name an email columns from contacts table
   data.read
      table:contacts
      columns
         name
         email

   // Returns records as an array named 'rows' where each object contains 'name' and 'email' fields
   yield
      rows:x:@data.read/*
