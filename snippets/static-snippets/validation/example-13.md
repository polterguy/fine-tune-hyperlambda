Change it such that it always logs 'Done', even if an exception is thrown

```hyperlambda
try
   throw:Some error
.catch
   log.error:Something went wrong
```
---
try
   throw:Some error
.catch
   log.error:Something went wrong
.finally
   log.info:Done
