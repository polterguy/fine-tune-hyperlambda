Create whatever the comment says

```hyperlambda
/*
 * An HTTP endpoint that sends an email to John Jensen, john@microsoft.com
 */
```
---
/*
 * An HTTP endpoint that sends an email to John Jensen, john@microsoft.com
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