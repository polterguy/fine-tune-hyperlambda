Retrieve the HubSpot token from configuration with the key being 'magic:hubspot:key'

```hyperlambda
.arguments
   email:string
   name:string
   company:string
validators.mandatory:x:@.arguments/*/email
validators.mandatory:x:@.arguments/*/name
validators.mandatory:x:@.arguments/*/company
http.post:"https://api.hubapi.com/crm/v3/objects/contacts"
   convert:true
   headers
      Authorization:Bearer [YOUR_HUBSPOT_API_KEY]
      Content-Type:application/json
   payload
      properties
         email:x:@.arguments/*/email
         firstname:x:@.arguments/*/name
         company:x:@.arguments/*/company
yield
   result:x:@http.post/*/content
```
---
.arguments
   email:string
   name:string
   company:string
validators.mandatory:x:@.arguments/*/email
validators.mandatory:x:@.arguments/*/name
validators.mandatory:x:@.arguments/*/company
strings.concat
   .:"Bearer "
   config.get:"magic:hubspot:key"
http.post:"https://api.hubapi.com/crm/v3/objects/contacts"
   convert:true
   headers
      Authorization:x:@strings.concat
      Content-Type:application/json
   payload
      properties
         email:x:@.arguments/*/email
         firstname:x:@.arguments/*/name
         company:x:@.arguments/*/company
yield
   result:x:@http.post/*/content
