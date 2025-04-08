Change the folder to /system/

```hyperlambda
/*
 * This script counts the number of Hyperlambda files, in addition to the combined
 * number of nodes, within the '/' folder.
 */
.folder:/
.loc:int:0
.files:int:0
unwrap:x:+/*
signal:magic.io.file.load-recursively
   .:x:@.folder
for-each:x:@signal/*
   if
      strings.ends-with:x:@.dp/#
         .:.hl
      .lambda
         hyper2lambda:x:@.dp/#/0
         math.increment:x:@.loc
            get-count:x:@hyper2lambda/**
         math.increment:x:@.files
remove-nodes:x:@signal/*
```
---
/*
 * This script counts the number of Hyperlambda files, in addition to the combined
 * number of nodes, within the '/system/' folder.
 */
.folder:/system/
.loc:int:0
.files:int:0
unwrap:x:+/*
signal:magic.io.file.load-recursively
   .:x:@.folder
for-each:x:@signal/*
   if
      strings.ends-with:x:@.dp/#
         .:.hl
      .lambda
         hyper2lambda:x:@.dp/#/0
         math.increment:x:@.loc
            get-count:x:@hyper2lambda/**
         math.increment:x:@.files
remove-nodes:x:@signal/*
