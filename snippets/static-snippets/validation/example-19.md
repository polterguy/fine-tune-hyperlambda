Change it such that subject is optional with a default value of 'Hello' unless specified by caller

```hyperlambda
.arguments
   name:string
   email:string
   subject:string
   content:string

// Making sure name, email, subject, and content arguments are mandatory
validators.mandatory:x:@.arguments/*/name
validators.mandatory:x:@.arguments/*/email
validators.mandatory:x:@.arguments/*/subject
validators.mandatory:x:@.arguments/*/content

// Sending email using provided arguments
mail.smtp.send
   message
      to
         .
            name:x:@.arguments/*/name
            email:x:@.arguments/*/email
      subject:x:@.arguments/*/subject
      entity:text/plain
         content:x:@.arguments/*/content```
---
.arguments
   name:string
   email:string
   subject:string
   content:string

// Making sure name, email, and content arguments are mandatory, but not subject
validators.mandatory:x:@.arguments/*/name
validators.mandatory:x:@.arguments/*/email
validators.mandatory:x:@.arguments/*/content

// Applying default value to subject.
validators.default:x:@.arguments
   subject:Hello

// Sending email using provided arguments
mail.smtp.send
   message
      to
         .
            name:x:@.arguments/*/name
            email:x:@.arguments/*/email
      subject:x:@.arguments/*/subject
      entity:text/plain
         content:x:@.arguments/*/content
