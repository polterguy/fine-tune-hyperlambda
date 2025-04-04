Convert to an HTTP endpoint and make paging optional arguments

```hyperlambda
data.connect:crm
   data.select:select name, email from contacts limit @limit offset @offset
      @limit:5
      @offset:10
```
---
.arguments
   limit:long
   offset:long
data.connect:crm
   add:x:./*/data.read
      get-nodes:x:@.arguments/*/limit
      get-nodes:x:@.arguments/*/offset
   data.read
      table:contacts