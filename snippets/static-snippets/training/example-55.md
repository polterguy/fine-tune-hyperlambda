Log the entire XML payload

```hyperlambda
.arguments
   xml:string

.type:public

// Sanity checking invocation.
validators.mandatory:x:@.arguments/*/xml
try

   /*
    * Authenticating user
    *
    * Returns JWT token tat can be used to invoke API.
    */
   .token
   execute:magic.workflows.actions.execute
      name:auth
      filename:/modules/actions-pro/workflows/actions/authenticate.hl
      arguments
   set-value:x:@.token
      get-value:x:@execute/*/token

   // Figuring out URL.
   .url
   set-value:x:@.url
      strings.concat
         config.get:"magic:resolve:url"
         .:"/resolve/rest/wiki/bot/updateModel"

   // Invoking HTTP endpoint.
   http.post:x:@.url
      query
         token:x:@.token
      headers
         Content-Type:application/xml
      payload:x:@.arguments/*/xml

   // Sanity checking invocation.
   if
      not
         and
            mte:x:@http.post
               .:int:200
            lt:x:@http.post
               .:int:300
      .lambda

         // Oops ...!!
         lambda2hyper:x:@http.post
         log.error:Could not create XML activity
            stack:x:@lambda2hyper
         strings.concat
            .:"Could not creater activity, response from server was \n\n"
            get-value:x:@lambda2hyper
         throw:x:-

   // Logging success.
   log.info:Successfully created XML activity for model.

   // Returning success to caller
   return
      result:success

.catch

   lambda2hyper:x:..
   log.error:x:@.arguments/*/message
      stack:x:@lambda2hyper
``` 
---
.arguments
   xml:string

.type:public

// XML payload given to endpoint
log.info:XML payload
   xml:x:@.arguments/*/xml

// Sanity checking invocation.
validators.mandatory:x:@.arguments/*/xml
try

   /*
    * Authenticating user
    *
    * Returns JWT token tat can be used to invoke API.
    */
   .token
   execute:magic.workflows.actions.execute
      name:auth
      filename:/modules/actions-pro/workflows/actions/authenticate.hl
      arguments
   set-value:x:@.token
      get-value:x:@execute/*/token

   // Figuring out URL.
   .url
   set-value:x:@.url
      strings.concat
         config.get:"magic:resolve:url"
         .:"/resolve/rest/wiki/bot/updateModel"

   // Invoking HTTP endpoint.
   http.post:x:@.url
      query
         token:x:@.token
      headers
         Content-Type:application/xml
      payload:x:@.arguments/*/xml

   // Sanity checking invocation.
   if
      not
         and
            mte:x:@http.post
               .:int:200
            lt:x:@http.post
               .:int:300
      .lambda

         // Oops ...!!
         lambda2hyper:x:@http.post
         log.error:Could not create XML activity
            stack:x:@lambda2hyper
         strings.concat
            .:"Could not creater activity, response from server was \n\n"
            get-value:x:@lambda2hyper
         throw:x:-

   // Logging success.
   log.info:Successfully created XML activity for model.

   // Returning success to caller
   return
      result:success

.catch

   lambda2hyper:x:..
   log.error:x:@.arguments/*/message
      stack:x:@lambda2hyper
