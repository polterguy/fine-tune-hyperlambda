Change this code such that it can only be executed by an admin user

```hyperlambda
.arguments
log.info:Ping invoked!
yield
   result:success
```
---
.arguments
auth.ticket.verify:admin
log.info:Ping invoked!
yield
   result:success
