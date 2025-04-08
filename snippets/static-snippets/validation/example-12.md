Add error handling and log the exception message

```hyperlambda
data.connect:bar
   data.scalar:select * from foo
```
---
try
   data.connect:bar
      data.scalar:select * from foo
.catch
   log.error:x:@.arguments/*/message
