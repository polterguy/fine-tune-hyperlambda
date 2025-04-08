Convert this into an endpoint that returns a product count

```hyperlambda
data.connect:[generic|inventory]
   data.scalar:select count(*) from products
```
---
/*
 * Returns count of products from inventory database using the generic connection string
 */
.arguments
data.connect:[generic|inventory]
   data.scalar:select count(*) from products
   yield
      product-count:x:@data.scalar
