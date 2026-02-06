
# 🔹 1️⃣ The Problem: NullReferenceException

Example method:

```csharp
static string PadAndTrim(string input, int finalLength, char padChar)
{
    return input.Trim().PadLeft(finalLength, padChar);
}
```

Now suppose:

```csharp
string input = null;

Console.WriteLine(PadAndTrim(input, 15, '0'));
```

### ❌ Runtime Error:

```
System.NullReferenceException
```

Why?

Because:

```csharp
input.Trim()
```

If `input` is null → you are calling `.Trim()` on nothing.

Boom 💥 exception.

---

# 🔹 2️⃣ Old Behavior (Before Nullable Reference Types)

Before C# 8:

- All reference types (like `string`) were automatically nullable.
    
- Compiler did NOT warn you.
    
- Errors happened only at runtime.
    

So this compiled fine:

```csharp
string input = null;
```

But crashed later.

---

# 🔹 3️⃣ Enabling Nullable Reference Types

In your `.csproj` file:

```xml
<Nullable>enable</Nullable>
```

Now C# changes behavior:

- Reference types are NON-nullable by default
    
- You must explicitly say if they can be null
    

---

# 🔹 4️⃣ With Nullable Reference Types Enabled

Now:

```csharp
string input = null;   // ⚠ Compiler warning
```

Compiler says:

> “This string should not be null.”

Because:

```csharp
string
```

means:

> This variable should NOT contain null.

If you want to allow null, you must write:

```csharp
string? input = null;
```

That `?` now means:

> This reference type may be null.

Just like we did with `int?`.

---

# 🔹 5️⃣ Null-Conditional Operator (`?.`)

This operator prevents null reference exceptions.

### Syntax:

```csharp
object?.Method()
```

Meaning:

> Call method ONLY if object is not null.

---

## 🔥 Fixing PadAndTrim

Instead of:

```csharp
return input.Trim().PadLeft(finalLength, padChar);
```

We write:

```csharp
return input?.Trim()?.PadLeft(finalLength, padChar);
```

Now:

- If `input` is null → entire expression returns null
    
- No crash
    

---

# 🔹 6️⃣ Example Without NRT (Old Style)

```csharp
static string PadAndTrim(string input, int finalLength, char padChar)
{
    if (input != null)
        return input.Trim().PadLeft(finalLength, padChar);
    else
        return "";
}
```

Works, but verbose.

---

# 🔹 7️⃣ Example With Nullable Reference Types Enabled

```csharp
#nullable enable
using System;

class Program
{
    static string? PadAndTrim(string? input, int finalLength, char padChar)
    {
        return input?.Trim()?.PadLeft(finalLength, padChar);
    }

    static void Main()
    {
        string? input = null;

        string? result = PadAndTrim(input, 15, '0');

        Console.WriteLine(result);
    }
}
```

---

### ✔ Output:

```
(blank line)
```

No exception.  
Just returns null safely.

---

# 🔹 8️⃣ Better Version (Avoid Returning Null)

Usually we combine with `??`:

```csharp
static string PadAndTrim(string? input, int finalLength, char padChar)
{
    return input?.Trim()?.PadLeft(finalLength, padChar)
           ?? new string(padChar, finalLength);
}
```

Now:

If input is null → return 15 padded characters.

---

### ✔ Example Run

```csharp
string? input = null;

Console.WriteLine(PadAndTrim(input, 10, '0'));
```

### ✔ Output:

```
0000000000
```

---

# 🔹 9️⃣ What Nullable Reference Types Actually Do

Important:

👉 They DO NOT change runtime behavior.

They only:

- Add compiler warnings
    
- Use static code analysis
    
- Help prevent NullReferenceException
    

They help you catch errors at compile time instead of runtime.

---

# 🔹 🔟 Compiler Warnings Example

If NRT is enabled:

```csharp
static string PadAndTrim(string input, int length, char padChar)
{
    return input.Trim();   // ⚠ Warning if input might be null
}
```

Compiler says:

> “input may be null.”

That’s static analysis.

---

# 🔹 1️⃣1️⃣ Quick Comparison

|Feature|Value Types|Reference Types (Old)|Reference Types (NRT)|
|---|---|---|---|
|Default null allowed?|❌|✅|❌|
|Use `?` to allow null?|✅|❌|✅|
|Compiler warnings?|Limited|❌|✅|

---


---

# 🔹 1️⃣2️⃣ Most Important Operators Summary

|Operator|Meaning|
|---|---|
|`?.`|Null-conditional (safe access)|
|`??`|Null-coalescing|
|`??=`|Null-coalescing assignment|
|`?`|Marks type as nullable|

---

# Working with nullable reference types



# 🔹 1️⃣ Big Idea: After Enabling Nullable Reference Types

When you enable this in your project:

```xml
<Nullable>enable</Nullable>
```

Now:

```csharp
string name;
```

Means:

> This string is NOT allowed to be null.

If you try:

```csharp
string name = null;   // ⚠ Warning
```

You’ll get a compiler warning.

---

# 🔹 2️⃣ Making a Reference Type Nullable

Just like value types:

```csharp
string? name = null;
```

The `?` now means:

> This string may contain null.

This is called a **nullable reference type**.

It doesn’t change runtime behavior.  
It just enables better compiler checking.

---

# 🔹 3️⃣ Compiler Static Analysis

Once nullable reference types are enabled:

The compiler checks:

- Could this parameter be null?
    
- Could this method return null?
    
- Did you initialize non-nullable properties?
    

Example warning:

```csharp
static string PadAndTrim(string input)
{
    return input.Trim();  // ⚠ input might be null
}
```

Even if it compiles, the compiler warns you:

> “input might be null here.”

This is static analysis.

---

# 🔹 4️⃣ Fixing Parameter Nullability

Option 1: Make parameter nullable

```csharp
static string PadAndTrim(string? input)
```

Now the compiler knows:

> This parameter might be null.

---

# 🔹 5️⃣ Fixing Return Value Issue

If your method returns:

```csharp
return input?.Trim()?.PadLeft(length, padChar);
```

That might return null.

If method signature is:

```csharp
static string PadAndTrim(...)
```

Compiler warns:

> “Possible null return.”

Fix it by guaranteeing non-null return:

```csharp
static string PadAndTrim(string? input, int length, char padChar)
{
    if (input == null)
        return new string(padChar, length);

    return input.Trim().PadLeft(length, padChar);
}
```

Now compiler is happy.

---

# 🔹 6️⃣ Example: Full Working Version

```csharp
#nullable enable
using System;

class Program
{
    static string PadAndTrim(string? input, int length, char padChar)
    {
        if (input == null)
        {
            return new string(padChar, length);
        }

        return input.Trim().PadLeft(length, padChar);
    }

    static void Main()
    {
        string? input = null;

        Console.WriteLine(PadAndTrim(input, 10, '0'));
    }
}
```

---

### ✔ Output:

```
0000000000
```

If you change:

```csharp
string? input = "abc";
```

### ✔ Output:

```
0000000abc
```

---

# 🔹 7️⃣ Using Attributes (Advanced Control)

The instructor used:

```csharp
[AllowNull]
```

This tells the compiler:

> I know this might be null. I will handle it.

You must include:

```csharp
using System.Diagnostics.CodeAnalysis;
```

Example:

```csharp
static string PadAndTrim([AllowNull] string input)
```

This suppresses certain warnings.

There are other attributes too:

|Attribute|Meaning|
|---|---|
|`[AllowNull]`|Parameter can be null|
|`[NotNull]`|Value will never be null|
|`[MaybeNull]`|Might return null|
|`[DisallowNull]`|Must not be null|

These help the compiler understand your intent.

---

# 🔹 8️⃣ Properties and Constructors Warning

When nullable reference types are enabled:

```csharp
class Person
{
    public string Name { get; set; }  // ⚠ Warning
}
```

Compiler says:

> Name must be initialized.

Why?

Because `string` is now non-nullable.

You must either:

### Option 1: Make it nullable

```csharp
public string? Name { get; set; }
```

### Option 2: Initialize it

```csharp
public string Name { get; set; } = "";
```

### Option 3: Initialize in constructor

```csharp
public Person(string name)
{
    Name = name;
}
```

This forces safer design.

---

# 🔹 9️⃣ Key Concept

Nullable Reference Types:

- DO NOT prevent null at runtime
    
- DO NOT change CLR behavior
    
- ONLY give compile-time warnings
    
- Use static analysis to detect possible null problems
    

They help prevent:

```
NullReferenceException
```

before your program runs.

---

# 🔹 🔟 Quick Summary Notes

### 🔹 After enabling:

- `string` → non-nullable
    
- `string?` → nullable
    

### 🔹 Fix warnings by:

- Adding `?`
    
- Adding null checks
    
- Returning default values
    
- Initializing properties
    
- Using attributes
    

### 🔹 Purpose:

Catch null bugs at compile time instead of runtime.

---

# 🔥 Interview-Ready Answer

If asked:

**“What are nullable reference types?”**

You say:

- Introduced in C# 8.
    
- Reference types are non-nullable by default.
    
- `?` marks them as nullable.
    
- Uses static analysis to warn about possible null usage.
    
- Helps reduce NullReferenceException.
    
- Does not change runtime behavior.
    

Clean. Confident. Done. 💪

---

If you want, next we can go:

- 🔥 Real-world ASP.NET model example
    
- 🔥 Deep comparison: nullable value vs reference types
    
- 🔥 Common nullable mistakes in interviews
    
- 🔥 Advanced attributes deep dive
    

Where do you want to go next?