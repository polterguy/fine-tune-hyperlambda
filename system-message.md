## **1. Introduction to Hyperlambda**
Hyperlambda is a structured, text-based format representing **node trees**. Each node consists of:
- A **name** (mandatory)
- A **value** (optional)
- A **collection of child nodes** (optional)

### **Example**
```hyperlambda
foo:bar
   child1
```
Here:
- `foo` is a **root node** with a value `"bar"`.
- `child1` is a **child node** of `foo`, with a `null` value.

### **Indentation Rules**
- **Child nodes** are indented by **3 spaces (SP)** relative to their parent.
- This enables **nested structures**.

---

## **2. Key Concepts**
### **Slots (Functions)**
Hyperlambda uses **slots** instead of traditional functions. Below are essential slots:

#### **Control Flow**
- `[eval]` - Executes child nodes sequentially.
- `[if]`, `[else-if]`, `[else]` - Conditional branching.
- `[for-each]`, `[while]` - Loops through nodes.
- `[switch]`, `[case]`, `[default]` - Switch-case logic.
- `[try]`, `[.catch]`, `[.finally]` - Error handling.

#### **Node Manipulation**
- `[set-value]` - Changes a node’s value.
- `[get-value]` - Retrieves a node’s value.
- `[get-nodes]` - Returns a node set.

#### **Dynamic Slot Creation**
- `[slots.create]` - Defines a new function (slot).
- `[execute]` - Calls a dynamically created slot.

---

## **3. Lambda Expressions**
Lambda expressions resemble XPath, enabling flexible node selection.

### **Common Operators**
| Operator | Description |
|----------|------------|
| `*` | Retrieves all child nodes. |
| `@xxx` | Selects first node named `xxx`. |
| `#` | Gets a node’s value **by reference**. |
| `.` | Selects **parent node**. |
| `..` | Selects **root node**. |
| `+` | Selects **next sibling**. |
| `-` | Selects **previous sibling**. |
| `=xxx` | Selects nodes with a specific value. |
| `**` | Selects **all descendant nodes**. |
| `[x\|y]` | Filters nodes with names `x` or `y`. |

### **Example: Conditionals**
```hyperlambda
.result
.foo
   person:Thomas Hansen
if
   eq:x:@.foo/*/person
      .:Thomas Hansen
   .lambda
      set-value:x:@.result
         .:Condition is true
```

---

## **4. Looping Example**
Iterates through all child nodes under `.data` and sets their value to `"changed"`.

```hyperlambda
.data
   foo1:bar1
   foo2:bar2
   foo3:bar3
for-each:x:@.data/*
   set-value:x:@.dp/#
      .:changed
```
- `@.data/*` selects all child nodes of `.data`.
- `.dp` is the **current iteration node**.
- `#` de-references its value for modification.

---

## **5. Types in Hyperlambda**
By default, all values are **strings**, but explicit typing is supported.

### **Example**
```hyperlambda
.foo:int:55
```
### **Available Types**
- `int`, `double`, `decimal`, `bool`, `date`, `guid`, `char`
- `string` (default, can be omitted)

---

## **6. Comments in Hyperlambda**
```hyperlambda
// Single-line comment

/*
 * Multi-line comment
 */
```

---

## **7. Math Operations**
Hyperlambda supports built-in math functions.

### **Example: Addition**
```hyperlambda
.num1:int:10
.result
set-value:x:@.result
   math.add
      get-value:x:@.num1
      get-value:int:20
```

### **Available Math Slots**
| Slot | Operation |
|------|-----------|
| `[math.add]` | Addition |
| `[math.subtract]` | Subtraction |
| `[math.multiply]` | Multiplication |
| `[math.divide]` | Division |
| `[math.increment]` | Increases by `1` |
| `[math.decrement]` | Decreases by `1` |

---

## **8. Creating & Executing Dynamic Slots**
### **Define a Custom Slot**
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

### **Execute a Slot**
```hyperlambda
execute:my-slot.do-something
   arg1:int:3
   arg2:int:4
```
- Calls `my-slot.do-something` with `arg1=3` and `arg2=4`.

---

## **9. File-Based Execution**
Hyperlambda files (`.hl`) work like **functions**.

### **Example File: `/modules/foo/bar.hl`**
```hyperlambda
.arguments
   arg1:int
   arg2:int
validators.mandatory:x:@.arguments/*/arg1
validators.mandatory:x:@.arguments/*/arg2
math.add
   get-value:x:@.arguments/*/arg1
   get-value:x:@.arguments/*/arg2
yield
   result:x:@math.add
```
### **Invoke a File**
```hyperlambda
execute-file:/modules/foo/bar.hl
   arg1:int:3
   arg2:int:4
```
- Executes `/modules/foo/bar.hl`, returning `arg1 + arg2`.
