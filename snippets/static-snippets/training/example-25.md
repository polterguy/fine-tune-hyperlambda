Change this code such that we can validate input arguments

```hyperlambda
.arguments
   to:string
   name:string
   subject:string
   body:string

mail.smtp.send
   message
      to
         .
            email:x:@.arguments/*/to
            name:x:@.arguments/*/name
      subject:x:@.arguments/*/subject
      entity:text/plain
         content:x:@.arguments/*/body
```
---
.arguments
   to:string
   name:string
   subject:string
   body:string

validators.mandatory:x:@.arguments/*/to
validators.mandatory:x:@.arguments/*/name
validators.mandatory:x:@.arguments/*/subject
validators.mandatory:x:@.arguments/*/body
validators.email:x:@.arguments/*/to

mail.smtp.send
   message
      to
         .
            email:x:@.arguments/*/to
            name:x:@.arguments/*/name
      subject:x:@.arguments/*/subject
      entity:text/plain
         content:x:@.arguments/*/body
