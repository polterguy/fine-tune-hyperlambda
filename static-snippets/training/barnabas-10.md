/*
 * Convert this into an endpoint that returns a product count
 */
data.connect:[generic|inventory]
   data.scalar:select count(*) from products
---
.arguments
data.connect:[generic|inventory]
   data.scalar:select count(*) from products
   yield
      product-count:x:@data.scalar
