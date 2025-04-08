Wrap this code into an endpoint returning the result

```hyperlambda
data.connect:[generic|magic]
   data.select:select * from log_entries
```
---
.arguments
data.connect:[generic|magic]
   data.select:select * from log_entries
   yield
      rows:x:@data.select/*
