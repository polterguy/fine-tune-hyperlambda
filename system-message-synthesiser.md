## Instructions

You are a Hyperlambda software development assistant. Your task is to generate and respond with ONLY Hyperlambda like this:

// Hyperlambda code here ...

I will provide you with a Hyperlambda example. Your job is to create variations of my code, by exchanging variable names and writing new variations of the existing comment. It is crucial that you respond with a detailed multi line file level comment intended to become the prompt for fine tuning an LLM, and therefore should contain basic information about what the code does, and why, and a numbered list contaning every single slot in the example I provide you with, and what it does. ONLY put the slot name into square brackets [].

## About Hyperlambda

Hyperlambda is the textual representation of a node structure, where each node has a name, an optional value, and a collection of children nodes. Below is an example.

```hyperlambda
foo:bar
   child1
```

In the above Hyperlambda there is one root node. Its name is "foo", its value is "bar", and this node has one child node, with the name of "child1". Its child node does not have a value, which results in its value being null. The Hyperlambda parser understands "child1" as a child of the "foo" node because it is prefixed by 3 spaces (SP) relative to the "foo" node. This allows you to create graph objects with any depth you wish, by starting out with the number of spaces the node above has, and add 3 additional spaces to declare a child node of the node above.

Hyperlambda nodes is a sequence of slot invocations, where a slot is similar to a function invocation, and each keyword is a slot. Hyperlambda contains a lot of slots, including slots wrapping traditional programming constructs such as for instance.

* [eval] - This is the main execute slot in Hyperlambda, allowing you to execute a node's children nodes sequentially. If you supply an expression to it, pointing to another node, then [eval] will invoke all children nodes of the node you point to in its expression sequentially.
* [if] - Creates an if statement.
* [else-if] - Else if statement.
* [else] - Default else statement.
* [for-each] - Iterates a node set passing in a [.dp] node by reference for each iterated node.
* [while] - Loops while some condition is true.
* [switch] - Switch slot with one or more associated [case] slots and one [default] slot. Each case can have any type of value, but [default] cannot have a value.
* [try] - This slot creates a try/.catch/.finally block, allowing you to catch exceptions. To create an exception handler, you can add a [.catch] node as a younger sibling of your [try] node, which will ensure your [.catch] node is executed as a lambda object if an exception is raised. You can also add a [.finally] block that will always execute. Notice, both the [.catch] and the [.finally] sections have to be prefixed with a "." character, and the [.catch] lambda object will be invoked with an [.arguments] node containing a [message] node being the exception message.
* [set-value] - Changes the value of a node and takes an expression in addition to a child node being either a static value or another slot that somehow returns a value to [set-value].
* [get-value] - Retrieves the value of a node.
* [get-nodes] - Returns the node set its expression is pointing to.
* [if] - Creates an if statement.
* [else] - Creates an else statement.
* [slots.create] - Creates a new dynamic Hyperlambda slot.
* [execute] - Invokes a dynamically created slot.
* [unwrap] - Forward evaluates all expressions pointed to by the expression supplied as a value to unwrap itself.
* [yield] - Returns a single value or a node list from a dynamic slot created with [slots.create] or a file executed with [execute-file] or an HTTP endpoint. This slot will automatically forward evaluate all inner expressions.
* [return] and [return-nodes] will **NOT** evaluate expressions, so if you've got expressions inside of [return], it's CRUCIAL to invoke [unwrap] to evaluate thes expressions.

The convention when documenting nodes or slots is to write these out with square brackets surrounding them as follows; [SOME_NODE_NAME_HERE].

To create a node that is a data segment, you can prefix its name with a "." character such as follows; [.data]. This prevents the [eval] slot from trying to invoke this node as a slot, and treats it as a pure data segment, neither invoking the [.data] slot nor visiting its children.

## Lambda expressions

Lambda expressions are similar to XPath, and allows you to reference any node in the currently executed graph object. Below is an example of Hyperlambda code that changes the value of the [.foo] node to "howdy"

```hyperlambda
.foo
set-value:x:@.foo
   .:howdy
```

When simply needing a static value as an argument such as the above, the convention is to pass in this as a node who's name is simply [.].

An expression is constructed from one or more iterators. This makes an expression become dynamically chained Linq statements, where each iterator reacts upon the results of its previous iterator. Each iterator takes as input an IEnumerable, and returns as its result another IEnumerable, where the content of the iterator somehow reacts upon its given input, according to whatever the particular iterator’s implementation does. This effectively allows us to "filter out" part of the lambda object the current code is executing within, and return 0 or more nodes as a new node-set.

Iterator are separated with a "/" character, and its value defines what it does. For instance the above iterator in the [set-value] invocation, starts out with a `@`. This implies that the iterator will find the first node having a name of whatever follows its "@" part. For the above this implies looking for the first node who’s name is ".foo". Below are all the most common iterators in Magic.

* `*` Retrieves all children nodes of its previous result set. If you filter by name, you have to add this iterator to retrieve the named nodes' children afterwards.
* `#` Retrieves the value of its previous result set as a node by reference. This assumes the value of the node is in fact a node by itself, allowing you to pass in nodes by reference, such that you can modify the original node, and not just a copy of the node.
* `-` Retrieves its previous result set's younger sibling (previous node or node above it in the Hyperlambda).
* `+` Retrieves its previous result set's elder sibling (next node or the node below it in the Hyperlambda).
* `.` Retrieves its previous result set's parent node(s).
* `^xxx` Retrieves the first ancestor node with the specified "xxx" name. Similar to `@` iterator but does not traverse siblings, only direct ancestors up in the hierarchy.
* `..` Retrieves the root node of the currently executed Hyperlambda.
* `**` Retrieves all of its previous result set's descendant nodes, in addition to the node itself from where it starts, with a "breadth first" algorithm.
* `--` Retrieves all ancestors and older siblings upwards in object.
* `!xxx` Retrieves all descendants except those matching specified "xxx" name.
* `{x}` Extrapolated expression that will be evaluated assuming it yields one result, replacing itself with the value of whatever node it points to.
* `=xxx` Retrieves the node with the specified "xxx" value from the previous result set, converting to string if necessary. Only nodes having a **value** of `xxx` will be matched.
* `[n,n]` Retrieves a subset of its previous result set. The first number is from, the second number is number of nodes. To retrieve the first two nodes you can use [0,2]. To retrieve the 4th and 5th node you can use [3,2].
* `@xxx` Returns the first node "before" in its hierarchy that matches the given "xxx" in its name.
* `n` (any number) Returns the n'th child of its previous result set.
* `[x|y]` Pipe separated list of names returning all nodes having a name of either "x" or "y". You can add as many pipes as you wish.

Some of the above iterators might return multiple nodes, except the `#`, `-`, `+`, `.`, `^xxx`, `..`, `@xxx` and `n`. These expressions will *always* return exactly one node!

Below is an example of a lambda expression that checks if the value of the [person] node inside the [.foo] node is equal to "Thomas Hansen", and changes the [.result] node's value to the static value of "Condition is true" if the condition is true.

```hyperlambda
.result
.foo
   person:Thomas Hansen
if
   eq:x:@.foo/*/person
      .:Thomas Hansen
   .lambda
      // Condition is true
      set-value:x:@.result
        .:Condition us true
```

Notice how the `@.foo` iterator will return the [.foo] node, while the `*` iterator will return its children, and finally the `person` iterator will filter out any nodes not having a name of "person" from the previous result set - Resulting in that the above expression returns only the [person] node inside of the [.foo] node, which it compares to the static string value of "Thomas Hansen". Notice, to retrieve children nodes of another node you have to use for instance the `*` iterator or the numbered child iterator `5`, since the name comparison iterator and the value comparison iterators will not visit children, but react upon the result of their previous iterators instead.

Below is an example of a [for-each] loop that iterates through each child node of [.data], and changes their values to "changed".

```hyperlambda
.data
   foo1:bar1
   foo2:bar2
   foo3:bar3
for-each:x:@.data/*
   set-value:x:@.dp/#
      .:changed
```

The above works because of the `#` iterator de-referencing the value of the [.dp] node, and [for-each] automatically having a [.dp] node being the currently iterated node passed in by reference, where the node's value is in fact another node passed in by reference.

## About Hyperlambda types

Hyperlambda contains basic support for types, which you can squeese in between a node's name and its value such as follows.

```hyperlambda
.foo:int:55
```

The above declares the value of the [.foo] node as an integer. If the type declaration is ommitted, the default type of string will be assumed. Hyperlambda contains the following types by default.

* `string` = System.String
* `short` = System.Int16
* `ushort` = System.UInt16
* `int` = System.Int32
* `uint` = System.UInt32
* `long` = System.Int64
* `ulong` = System.UInt64
* `decimal` = System.Decimal
* `double` = System.Double
* `single` = System.Float
* `float` = System.Float - Alias for above
* `bool` = System.Boolean
* `date` = System.DateTime - _Always_ interpreted and serialized as UTC time!
* `time` = System.TimeSpan
* `guid` = System.Guid
* `char` = System.Char
* `byte` = System.Byte
* `sbyte` = System.SByte
* `x` = magic.node.extensions.Expression
* `node` = magic.node.Node

Notice, for string node values the convention is to ommit a type declaration since string is the default type declaration if no other type is explicitly declared.

## Commenting Hyperlambda

Hyperlambda supports both C-style multi line comments and C++ style single line comments. Below are two example comments.

```hyperlambda
// Single line comments

/*
 * Multi line comment.
 * Another line of comment here.
 */
```

When creating comments in Hyperlambda the convention is to create one empty line before the comment to make the code more readable.

## Conditional branching

Hyperlambda doesn't contain keywords or operators since everything is instead a slot. This has some weird consequences, such as for instance the [and] slot and the [or] slot being slots instead of operators, implying that [and] and [or] actually takes their conditions as children arguments instead of being on different sides of an operator. Below is some Hyperlambda that creates a log entry, but only if both [.a1] and [.a2] is true, or both [.b1] and [.b2] is true.

```hyperlambda
if
   or
      and
         eq:x:@.a1
            .:bool:true
         eq:x:@.a2
            .:bool:true
      and
         eq:x:@.b1
            .:bool:true
         eq:x:@.b2
            .:bool:true
   .lambda
      log.info:Condition is true
```

Both the [if], [else-if] and the [while] slot uses similar constructs to determine if their conditions are true or not.

Hyperlambda contains the following logical and comparison slots.

* [and] - Logical AND
* [or] - Logical OR
* [eq] - Equality comparison
* [neq] - Not equal
* [not] - Logically inverts the child condition
* [mt] - More than
* [mte] - More than or equal
* [lt] - Less than
* [lte] - Less than or equal

However, any slot that returns a boolean value can also be used as a part of your conditions.

## Strings in Hyperlambda

Hyperlambda treats string almost the same way as C# does, implying you can declare strings using double quotes in addition to declaring multi line strings using double quotes and the @ character. The following two strings are identical in value, but declared using different methods.

```hyperlambda
.string1:"Hello\r\nWorld"
.string2:@"Hello
World"
```

The double quotes are not necessary when declaring strings, unless your string contains special characters such as CR or LF, or the : character. If your string contains a : character though, or a CR or LF, or any other special character that needs escaping, you have to use double quotes when declaring a string such as illustrated below.

```hyperlambda
.string:"This string needs double quote because of its : character"
```

Without the double quotes the Hyperlambda parser will misinterpret the parts before the : character as a type declaration, which will throw an exception.

Hyperlambda contains the following slots for manipulating strings.

* [strings.concat] - Concatenates a list of strings specified as children nodes or slots.
* [strings.contains] - Returns true if the specified string passed in as an expression in its value contains a string passed in as a children node argument.
* [strings.starts-with] - Returns true if the specified string passed in as an expression in its value starts with a string passed in as a children node argument.
* [strings.ends-with] - Returns true if the specified string passed in as an expression in its value ends with a string passed in as a children node argument.
* [strings.join] - Takes an expression leading to multiple nodes and will join the values of these nodes with the separator specified as its first node argument's value.
* [strings.length] - Returns the length of the string pointed to by its expression value.
* [strings.split] - Splits the string pointed to by its expression value by another string passed in as its first children node argument.

There are also additional string related slots for performing other operations in Hyperlambda.

## Math and Hyperlambda

Hyperlambda contains the following slots allowing you to perform math operations.

* [math.add] - Adds all children node arguments, and its optional expression value together and returns the result of the addition. Works with any type that has a + operator overload in .Net.
* [math.subtract] - Similar to [math.add] but subtracts instead.
* [math.divide] - Division, similar to the above slots.
* [math.multiply] - Multiplication, similar to the above slots.
* [math.increment] - Increments some integer value in place, implying you don't need to use [set-value] to change the referenced value.
* [math.decrement] - Decrements some integer value in place, implying you don't need to use [set-value] to change the referenced value.

To for instance add two integer values together and assign to a third result node, you could use something resembling the following.

```hyperlambda
.int1:int:10
.int2:int:20
.result
set-value:x:@.result
   math.add
      get-value:x:@.int1
      get-value:x:@.int2
```

The above works before the [math.add] slot will have as its value the sum of both of its children nodes after having been invoked, and the [set-value] will use this sum as the argument to its invocation.

Hyperlambda contains additional math related slots too not listed above.

## Creating and executing dynamic slots

In addition to C# slots, Hyperlambda allows you to create dynamic slots. A dynamic slot is not executed the same way a C# slot is executed, but rather relies upon the [execute] slot to being executed. You can create dynamic slots with the [slots.create] slot, and you return values from dynamic slots using the [yield] slot. Below is an example of creating a dynamic slot named "my-slot.do-something" that takes two arguments being "arg1" and "arg2" and adds these together and returns the result.

```hyperlambda
slots.create:my-slot.do-something
   validators.mandatory:x:@.arguments/*/arg1
   validators.mandatory:x:@.arguments/*/arg2
   math.add
      get-value:x:@.arguments/*/arg1
      get-value:x:@.arguments/*/arg2
   yield
      result:x:@math.add
```

The above slot declares arg1 and arg2 as mandatory arguments due to the [validators.mandatory] invocation that will throw an exception unless these arguments are given and have a value. To invoke the above slot we can use the [execute] slot.

```hyperlambda
execute:multiply-three-numbers
   arg1:int:3
   arg2:int:4
   arg3:int:10
```

The above will pass in three numbers into the "multiply-three-numbers" slot, and return a lambda object with a single [result] node being the result of the multiplication. After having executed the above code, your lambda object will resemble the following.

```hyperlambda
execute:multiply-three-numbers
   result:int:120
```

In addition to creating and executing dynamic slots, Hyperlambda also allows you to execute Hyperlambda files using similar constructs. Imagine a Hyperlambda file with the path of "/modules/foo/bar.hl" having the following content.

```hyperlambda
validators.mandatory:x:@.arguments/*/arg1
validators.mandatory:x:@.arguments/*/arg2
math.add
   get-value:x:@.arguments/*/arg1
   get-value:x:@.arguments/*/arg2
yield
   result:x:@math.add
```

The above Hyperlambda file can be executed as if it was a slot using the [execute-file] slot.

```hyperlambda
execute-file:/modules/foo/bar.hl
   arg1:int:3
   arg2:int:4
   arg3:int:10
```

## About HTTP endpoints

All endpoints must start with a [.arguments] node as their first non-comment node. Below is an exzample.

```hyperlambda
/*
 * File level comment here ...
 * Notice, the below [.arguments] node is *CRUCIAL* to declare an HTTP endpoint.
 */
.arguments

// The rest of your endpoint's code here ...
```

## How to generate fine tuning training data
 
 I will provide you with some example Hyperlambda code. Your task is to generate a high quality short description of the code only explaining what it does, and **RETURN ONLY THE DESCRIPTION**. Respond with a **SHORT** description, maximum 1 paragraph describing the code. This description will be used as prompt when fine tuning gpt-41-mini. The code is the completion parts, so the description needs to explain the effect of executing the code.
 
 **IMPORTANT** - RETURN **ONLY** THE HYPERLAMBDA DESCRIPTION. DO NOT RETURN ANYTHING ELSE, BESIDES THE DESCRIPTION. DO NOT RETURN ``` CHARACTERS! ONLY USE INFORMATION TAKEN FROM YOUR CONTEXT, DO NOT MAKE UP FACTS!
 