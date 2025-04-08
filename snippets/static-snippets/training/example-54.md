Wrap this into an endpoint returning the result

```hyperlambda
/*
 * From the `ecommerce` database, join `orders` with `products` to fetch order-product pairs.
 * Retrieve 20 records, starting from the 41st — typical for page 3 with page size 20.
 */
data.connect:ecommerce
   data.read
      table:orders
         join:products
            type:inner
            on
               and
                  orders.product_id:products.id
      columns
         orders.id
         products.name
      limit:int:20
      offset:int:40
``` 
---
/*
 * From the `ecommerce` database, join `orders` with `products` to fetch order-product pairs.
 * Retrieve 20 records, starting from the 41st — typical for page 3 with page size 20.
 */
.arguments
data.connect:ecommerce
   data.read
      table:orders
         join:products
            type:inner
            on
               and
                  orders.product_id:products.id
      columns
         orders.id
         products.name
      limit:int:20
      offset:int:40
   yield
      records:x:@data.read/*