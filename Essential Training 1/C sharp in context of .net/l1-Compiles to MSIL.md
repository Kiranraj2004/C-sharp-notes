
## 1️⃣ What happens when you write C#?

When you write C# code:

```
C# Source Code (.cs)
        ↓
C# Compiler (csc)
        ↓
MSIL (Microsoft Intermediate Language)
        ↓
CLR (Common Language Runtime)
        ↓
Machine Code (via JIT)
        ↓
Program Runs
```

So C# does **NOT** directly compile to machine code.

It compiles to **MSIL (also called IL or CIL)**.

---

# 📘 What is MSIL?

**MSIL (Microsoft Intermediate Language)** is:

- A CPU-independent intermediate language
    
- Used by all .NET languages
    
- Executed by the .NET runtime (CLR)
    
- Converted to machine code using **JIT (Just-In-Time compiler)**
    

Think of it like:

> MSIL is the “middle language” between C# and the actual computer hardware.

---

# 🌍 Multiple Languages → Same Runtime

These languages all compile to MSIL:

- C#
    
- F#
    
- Visual Basic .NET
    

That means:

✅ They all run on the same runtime (CLR)  
✅ They can use each other’s libraries  
✅ They share the same memory management  
✅ Same garbage collector

This is a HUGE advantage of .NET.

---

# 🔥 Why Is This Powerful?

Because:

### 1️⃣ Language evolves independently

C# can change without changing the runtime.

For example:

- C# 5
    
- C# 6
    
- C# 7
    
- C# 10
    
- C# 12
    

All can target the same runtime.

---

### 2️⃣ Portability

Since MSIL is CPU independent, the CLR can generate machine code for:

- Windows
    
- Linux
    
- macOS
    

---

# 🛠 ILDASM (IL Disassembler)

When you compile a C# program into:

```
.exe
or
.dll
```

You can open it in:

> ILDASM (Intermediate Language Disassembler)

It shows you:

- The MSIL instructions
    
- Methods
    
- Fields
    
- Properties
    
- Backing fields
    

---

# 🧩 Example 1: Simple Hello World

### 📝 C# Code

```csharp
using System;

class Program
{
    static void Main()
    {
        Console.WriteLine("Hello World");
    }
}
```

---

### 🖥 Output

```
Hello World
```

---

### 🔍 Conceptual MSIL (Simplified)

```il
.method private hidebysig static void Main() cil managed
{
    ldstr "Hello World"
    call void [System.Console]::WriteLine(string)
    ret
}
```

### What those IL instructions mean:

|IL Instruction|Meaning|
|---|---|
|`ldstr`|Load string onto stack|
|`call`|Call a method|
|`ret`|Return from method|

---

# 🧩 Example 2: Property and Backing Field

### 📝 C# Code

```csharp
using System;

class Person
{
    public string LastName { get; set; }
}
```

You wrote this very simple property.

But the compiler actually generates:

```csharp
private string <LastName>k__BackingField;

public string get_LastName()
{
    return <LastName>k__BackingField;
}

public void set_LastName(string value)
{
    <LastName>k__BackingField = value;
}
```

You didn’t write that — the compiler created it.

---

### 🔍 Conceptual MSIL for Getter

```il
ldarg.0            // load 'this'
ldfld string Person::<LastName>k__BackingField
ret
```

Meaning:

- `ldarg.0` → load current object
    
- `ldfld` → load field
    
- `ret` → return value
    

---

### 🔍 Conceptual MSIL for Setter

```il
ldarg.0
ldarg.1
stfld string Person::<LastName>k__BackingField
ret
```

Meaning:

- `ldarg.1` → load parameter (value)
    
- `stfld` → store into field
    

---

# 🧩 Example 3: Full Example

### 📝 C# Code

```csharp
using System;

class Person
{
    public string FirstName { get; set; }
}

class Program
{
    static void Main()
    {
        Person p = new Person();
        p.FirstName = "Kiran";

        Console.WriteLine("Hello " + p.FirstName);
    }
}
```

---

### 🖥 Output

```
Hello Kiran
```

---

### 🔍 What Happens Internally (Conceptually)

MSIL will:

1. Create new Person object
    
2. Call set_FirstName()
    
3. Load string "Hello "
    
4. Call get_FirstName()
    
5. Concatenate strings
    
6. Call Console.WriteLine()
    

---

# 🧠 Important Concepts for Interviews

If an interviewer asks:

### ❓ Does C# compile to machine code?

You say:

> No. C# compiles to MSIL (Intermediate Language), which is then converted into native machine code at runtime by the CLR using JIT compilation.

---

### ❓ What is CLR?

Common Language Runtime:

- Executes MSIL
    
- Handles memory
    
- Garbage collection
    
- Exception handling
    
- Security
    
- JIT compilation
    

---

# 💡 Very Simple Analogy

Think of it like this:

C# → English  
MSIL → Common Translator Language  
CLR → Real-time interpreter  
Machine Code → What the CPU understands

---
