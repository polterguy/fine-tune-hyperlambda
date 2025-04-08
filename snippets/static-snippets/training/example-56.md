Change it such that it also selects items from logistics and returns the resulting records in addition to what it's returning from before

```hyperlambda
.arguments
   str1:Hello
   str2:World
strings.concat
   get-value:x:@.arguments/*/str1
   get-value:x:@.arguments/*/str2
log.info:Concatenated result
   result:x:@strings.concat
yield
   result:x:@strings.concat
``` 
---
.arguments
   str1:Hello
   str2:World
strings.concat
   get-value:x:@.arguments/*/str1
   get-value:x:@.arguments/*/str2
log.info:Concatenated result
   result:x:@strings.concat
data.connect:logistics
   data.read
      table:items
   yield
      result:x:@strings.concat
      rows:x:@data.read/*
