
## 1) What are **Default Parameters**?

A **default parameter** is a parameter that already has a value assigned in the **function definition**.\ So when you call the function, you can **skip that argument**, and C# will use the default value automatically.

### ✅ Why it’s useful

- Makes calls **cleaner**
- Avoids passing “dummy values” like `""` or `0`
- Makes optional arguments easy

### Syntax

void MyFunc(string msg, string prefix = "")

{

    // …

}

### Key Rule (very important)

✅ **Parameters with defaults must be at the end** of the parameter list.

✅ Allowed:

void F(int a, int b = 10, int c = 20) { }

❌ Not allowed:

void F(int a = 10, int b) { } // ERROR

---

## 2) What are **Named Parameters**?

Named parameters mean you call a function by explicitly writing the **parameter name** with the value.

### ✅ Why it’s useful

- Improves readability
- Great when a function has many parameters (especially optional/default ones)
- Allows passing arguments **out of order**

### Syntax

PrintWithPrefix(prefix: "[INFO]", theStr: "Hello");

---

# 🧠 Transcript Idea (Explained Simply)

The transcript’s function originally takes:

- the string to print
- the prefix to print in front

If you don’t want a prefix, you might pass an empty string `""`, but that’s not readable.

✅ Better approach: set a **default value** for `prefix`, like `""`\ Then you can skip it when calling.

Then, to make calls more readable, you can use **named arguments**, even out of order.

---

# ✅ Example Code (with Default + Named Parameters)

using System;

  

void PrintWithPrefix(string theStr, string prefix = "")

{

    Console.WriteLine($"{prefix} {theStr}".Trim());

}

  

// 1) Call without prefix (uses default "")

PrintWithPrefix("Hello there");

  

// 2) Call with prefix (override default)

PrintWithPrefix("Hello there", ">>>");

  

// 3) Named arguments (in normal order)

PrintWithPrefix(theStr: "Named args in order", prefix: "[INFO]");

  

// 4) Named arguments (out of order - still works)

PrintWithPrefix(prefix: "[WARN]", theStr: "Named args out of order");

### 🔍 Why `.Trim()`?

If prefix is empty, it avoids printing a leading space.

---

# 🖥 Output

```
Hello there
>>> Hello there
[INFO] Named args in order
[WARN] Named args out of order
```

---

# ✅ Extra Notes (Interview / Exam Friendly)

## Default parameter evaluation

Default values are decided at **compile-time**, not runtime.

So avoid using things like:

void Foo(DateTime t = DateTime.Now) // Not allowed as default

Instead:

void Foo(DateTime? t = null)

{

    t ??= DateTime.Now;

}

---

# ✅ Quick Summary

### Default Parameters

- Defined in the function signature
- Let you skip optional arguments
- Must be at the end

### Named Parameters

- Use `paramName: value`
- Improves readability
- Allows out-of-order arguments