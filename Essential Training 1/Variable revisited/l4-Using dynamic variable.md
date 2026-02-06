
# ✅ `dynamic` in C#

This is VERY different from `var`.  
Let’s go slow and make it crystal clear.

---

# ✅ 1️⃣ What is `dynamic`?

When you write:

```csharp
dynamic d = new ShiftWorker();
```

You are telling the compiler:

> “Don’t check anything about this variable at compile time.  
> We’ll figure it out at runtime.”

So unlike normal C#, **type checking is delayed until runtime**.

---

# ✅ 2️⃣ `var` vs `dynamic` (Very Important Difference)

|Feature|`var`|`dynamic`|
|---|---|---|
|Type decided when?|Compile time|Runtime|
|Type checking?|Yes|No|
|Strongly typed?|Yes|No|
|Can call invalid property?|❌ Compile error|✅ Compiles, may crash at runtime|

---

# ✅ 3️⃣ Example Setup

Let’s use this class:

```csharp
public class ShiftWorker
{
    public string FirstName { get; set; }
    public string LastName { get; set; }
}
```

---

# ✅ 4️⃣ Using `dynamic`

```csharp
using System;

class Program
{
    static void Main()
    {
        dynamic d = new ShiftWorker();

        d.FirstName = "Dynamic";
        d.LastName = "Worker";

        Console.WriteLine(d.FirstName);
    }
}
```

### ✅ Output

```
Dynamic
```

Why does this work?

Because `ShiftWorker` has `FirstName`.

---

# ✅ 5️⃣ Calling a Property That Doesn't Exist

Now watch this 👇

```csharp
using System;

class Program
{
    static void Main()
    {
        dynamic d = new ShiftWorker();

        d.FirstName = "Dynamic";
        Console.WriteLine(d.Kids);  // ⚠ No compile error
    }
}
```

### What happens?

✔ Compiles successfully  
❌ Crashes at runtime

### ❌ Runtime Error:

```
Microsoft.CSharp.RuntimeBinder.RuntimeBinderException:
'ShiftWorker' does not contain a definition for 'Kids'
```

Why?

Because compiler didn’t check it.  
Runtime checked it — and failed.

---

# ✅ 6️⃣ Compare With Normal Strong Typing

```csharp
ShiftWorker d = new ShiftWorker();

Console.WriteLine(d.Kids);  // ❌ Compile-time error
```

Here compiler immediately stops you.

That’s the big difference.

---

# ✅ 7️⃣ Real-World Use Cases of `dynamic`

`dynamic` is useful when:

### 🔹 1. Working with JSON (unknown structure)

### 🔹 2. Reflection

### 🔹 3. COM objects

### 🔹 4. Loading types from config

### 🔹 5. Interoperability with scripting languages

Example with unknown type:

```csharp
dynamic value = 10;
Console.WriteLine(value);  // 10

value = "Hello";
Console.WriteLine(value);  // Hello

value = true;
Console.WriteLine(value);  // True
```

### ✅ Output

```
10
Hello
True
```

`dynamic` can change type at runtime.

`var` CANNOT do this.

---

# ✅ 8️⃣ `dynamic` vs Interface

With interface:

```csharp
IPerson p = new ShiftWorker();
```

Compiler knows:

✔ It must follow IPerson structure.

With `dynamic`:

```csharp
dynamic p = new ShiftWorker();
```

Compiler says:

> “I’m not checking anything. You handle it.”

---

# ✅ 9️⃣ Why C# Even Allows This?

C# is strongly typed.

But sometimes:

- Types are loaded at runtime
    
- You don’t know structure at compile time
    
- You trust the data source
    

In those rare cases, `dynamic` is helpful.

But it removes safety.

---

# 🎯 Interview-Level Summary

`dynamic`:

- Bypasses compile-time type checking
    
- Resolved at runtime
    
- Can cause runtime exceptions
    
- Should be used carefully
    
- Different from `var`
    

---

# 🔥 Final Comparison (Super Important)

```csharp
var x = new ShiftWorker();     // Strongly typed
dynamic y = new ShiftWorker(); // Runtime typed
```

With `var`:

- Compiler enforces safety
    

With `dynamic`:

- You are responsible
    

---

# 🧠 Golden Rule

> `var` is strongly typed and safe.  
> `dynamic` disables compile-time checking and shifts responsibility to runtime.

---
