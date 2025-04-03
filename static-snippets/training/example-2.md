Change the following code such that only partners users can execute it:

.arguments
   to:string
   subject:string
   body:string

// Sanity checking invocation.
validators.mandatory:x:@.arguments/*/to
validators.mandatory:x:@.arguments/*/subject
validators.mandatory:x:@.arguments/*/body

// Invokes [mail.smtp.send] with default configuration.
unwrap:x:+/*
mail.smtp.send
   message
      to
         .
            email:x:@.arguments/*/to
      subject:x:@.arguments/*/subject
      entity:text/plain
         content:x:@.arguments/*/body
---
.arguments
   to:string
   subject:string
   body:string

// Sanity checking invocation.
validators.mandatory:x:@.arguments/*/to
validators.mandatory:x:@.arguments/*/subject
validators.mandatory:x:@.arguments/*/body

// Making sure only partners users can execute the function
auth.ticket.verify:partners

// Invokes [mail.smtp.send] with default configuration.
unwrap:x:+/*
mail.smtp.send
   message
      to
         .
            email:x:@.arguments/*/to
      subject:x:@.arguments/*/subject
      entity:text/plain
         content:x:@.arguments/*/body
