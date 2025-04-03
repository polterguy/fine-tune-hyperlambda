Wrap this code into an endpoint

```hyperlambda
data.connect:[hr|company]
   data.select:select first_name, last_name from employees
```
---
.arguments
data.connect:[hr|company]
   data.select:select first_name, last_name from employees
   yield
      employees:x:@data.select/*
