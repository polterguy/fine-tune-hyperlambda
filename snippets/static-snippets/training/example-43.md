Change my code in accordance to the description in my comment

```hyperlambda
/*
 * An HTTP endpoint that sends an email to John Jensen, john@microsoft.com
 *
 * It will also CC Thomas Hansen, thomas@ainiro.io
 */
.arguments

// Sending email
mail.smtp.send
   message

      // Making sure we send the email to John Jensen / john@microsoft.com
      to
         .
            name:John Jensen
            email:john@microsoft.com

      subject:Hello from Magic Backend
      entity:text/plain
         content:This is a test email sent from a Magic backend.

return
   result:success
```
---
/*
 * An HTTP endpoint that sends an email to John Jensen, john@microsoft.com
 *
 * It will also CC Thomas Hansen, thomas@ainiro.io
 */
.arguments

// Sending email
mail.smtp.send
   message

      // Making sure we send the email to John Jensen / john@microsoft.com
      to
         .
            name:John Jensen
            email:john@microsoft.com
      cc
         .
            name:Thomas Hansen
            email:thomas@ainiro.io

      subject:Hello from Magic Backend
      entity:text/plain
         content:This is a test email sent from a Magic backend.

return
   result:success
