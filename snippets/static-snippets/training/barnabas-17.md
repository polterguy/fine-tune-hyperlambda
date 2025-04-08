Convert this into a reusable slot named 'math.double' taking a number argument it doubles

```hyperlambda
math.multiply
   .:int:4
   .:int:2
```
---
slots.create:math.double
   math.multiply
      get-value:x:@.arguments/*/value
      .:int:2
   yield
      result:x:@math.multiply
