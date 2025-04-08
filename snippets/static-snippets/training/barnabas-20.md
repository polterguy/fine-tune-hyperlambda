Wrap the logic in a [try] block and add [.catch] that logs 'Something went wrong'

```hyperlambda
throw:Oops
```
---
try
   throw:Oops
.catch
   log.info:Something went wrong
