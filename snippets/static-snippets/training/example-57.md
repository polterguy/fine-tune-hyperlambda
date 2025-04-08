Include all Album records for each artist by selecting albums for each artist

```hyperlambda
.arguments

   // Optional filtering arguments
   Artist.ArtistId.eq:long
   Artist.Name.like:string
   Artist.Name.eq:string

// Opening up our database connection.
data.connect:[generic|chinook]
   database-type:sqlite

   // Parametrising our read invocation.
   add:x:./*/data.read/*/where/*/and
      get-nodes:x:@.arguments/*

   // Reading data from database.
   data.read
      database-type:sqlite
      table:Artist
      columns
         Artist.ArtistId
         Artist.Name
      where
         and

    // Includes all albums for all artists returned above.
    include:x:@data.read/*
       data.read
          table:Albums
          where
             and
                ArtistId.eq:x:@.dp/#/*/ArtistId
        yield
           albums:x:@data.read/*

   // Returning result of above read invocation to caller.
   return-nodes:x:@data.read/*
```
---
.arguments

   // Optional filtering arguments
   Artist.ArtistId.eq:long
   Artist.Name.like:string
   Artist.Name.eq:string

// Opening up our database connection.
data.connect:[generic|chinook]
   database-type:sqlite

   // Parametrising our read invocation.
   add:x:./*/data.read/*/where/*/and
      get-nodes:x:@.arguments/*

   // Reading data from database.
   data.read
      database-type:sqlite
      table:Artist
      columns
         Artist.ArtistId
         Artist.Name
      where
         and

   // Includes all albums for all artists returned above.
   include:x:@data.read/*
      data.read
         table:Album
         where
            and
               ArtistId.eq:x:@.dp/#/*/ArtistId
      yield
         albums:x:@data.read/*

   // Returning result of above read invocation to caller.
   return-nodes:x:@data.read/*
