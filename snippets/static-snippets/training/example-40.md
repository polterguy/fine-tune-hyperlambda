Implement what the comment says

```hyperlambda
/*
 * An HTTP endpoint that consumes the Cat fact API and returns a random cat fact
 */
```
---
/*
 * An HTTP endpoint that consumes the Cat fact API and returns a random cat fact
 */
.arguments

// Invoking Cat fact API.
http.get:"https://catfact.ninja/fact"
   convert:true

// Returning result of above HTTP GET invocation to caller.
return:x:@http.get/*/content/*/fact
