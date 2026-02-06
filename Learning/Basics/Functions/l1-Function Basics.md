

Functions (also called _methods_) let you:

- group reusable code
- avoid repetition
- pass inputs (parameters)
- return outputs (return values)

---

# ✅ **1. Structure of a Function**

A function in C# has:

1. **Return Type**
    
    - `int`, `float`, `string`, `bool`, etc.
    - or `void` (if nothing is returned)
2. **Function Name**
    
3. **Parameters (optional)**\ Passed inside parentheses\ Each parameter has a type + name
    
4. **Function Body**\ Code written inside `{ }`
    

### General Format

returnType FunctionName(parameterList)

{

    // code

    return value;    // only if returnType is NOT void

}

---

# ✅ **2. Example 1 — Function With Return Value**

### ✔ Converts Miles → Kilometers

float MilesToKm(float miles)

{

    float result = miles * 1.6f;

    return result;

}

### How to call it:

Console.WriteLine($"The result is {MilesToKm(8.0f)}");

Console.WriteLine($"The result is {MilesToKm(52.0f)}");

---

# ✅ **3. Example 2 — Function With No Return Value (`void`)**

### ✔ Prints text with a custom prefix

void PrintWithPrefix(string theStr)

{

    Console.WriteLine($"::> {theStr}");

}

### Calling it:

PrintWithPrefix("Test String");

PrintWithPrefix("Another Test String");

---

# 🧪 **Complete Program Example (Top‑Level Statements)**

using System;

  

float MilesToKm(float miles)

{

    float result = miles * 1.6f;

    return result;

}

  

void PrintWithPrefix(string theStr)

{

    Console.WriteLine($"::> {theStr}");

}

  

// Function calls

Console.WriteLine($"The result is {MilesToKm(8.0f)}");

Console.WriteLine($"The result is {MilesToKm(52.

---

# 🖥 **OUTPUT**

```
The result is 12.8
The result is 83.2
::> Test String
::> Another Test String
```

---

# 📌 **Key Points to Remember**

### ✔ Functions can return a value

Use `returnType FunctionName(...)`

### ✔ Or they can return nothing

Use `void FunctionName(...)`

### ✔ Parameters let you pass input values

Inside the parentheses

### ✔ Functions are reusable

Call them anytime you need them

### ✔ C# top-level statements allow defining functions below your main code

---
