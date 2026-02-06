

## 1️⃣ Big Picture Architecture

Here’s the flow of how a C# program runs:

```
C# Source Code (.cs)
        ↓
C# Compiler (csc)
        ↓
IL Code (Intermediate Language)
        ↓
CLR (Common Language Runtime)
        ↓
JIT Compiler
        ↓
Machine Code
        ↓
Execution on OS
```

Now let’s break this properly.

---

## 🔹 1. C# Source Code

You write code like this:

```csharp
using System;

class Program
{
    static void Main(string[] args)
    {
        Console.WriteLine("Hello Kiran!");
    }
}
```

File extension: `.cs`

---

## 🔹 2. C# Compiler (csc)

- The C# compiler compiles `.cs` files.
    
- It does NOT convert directly to machine code.
    
- It converts code into **IL (Intermediate Language)**.
    

Output:

- `.exe` or `.dll` file
    
- Contains IL code + metadata
    

---

## 🔹 3. IL (Intermediate Language)

Also called:

- MSIL (Microsoft Intermediate Language)
    
- CIL (Common Intermediate Language)
    

This is **platform-independent code**.

👉 Same idea as:  
Java → Bytecode

So:

- C# → IL
    
- Java → Bytecode
    

Very similar concept.

---

## 🔹 4. CLR (Common Language Runtime)

This is the **heart of .NET**.

Think of it like:  
JVM in Java.

CLR is responsible for:

✔ Memory management (Garbage Collection)  
✔ Exception handling  
✔ Thread management  
✔ Security  
✔ Type safety  
✔ JIT compilation

Without CLR → C# program cannot run.

---

## 🔹 5. JIT (Just-In-Time Compiler)

When you run the program:

- CLR takes IL code
    
- Converts it into machine code
    
- Executes it
    

This happens at runtime.

So:

IL → JIT → Native Machine Code

---

# 📦 What is .NET?

C# runs inside the **.NET platform**.

.NET contains:

- CLR
    
- Base Class Library (BCL)
    
- Runtime libraries
    
- APIs
    

---

# 📚 Base Class Library (BCL)

This gives ready-made classes:

- `System`
    
- `System.IO`
    
- `System.Collections`
    
- `System.Net`
    
- `System.Threading`
    

Example:

```csharp
using System;
```

That’s importing classes from BCL.

---

# 🧠 Full Execution Flow (Step by Step)

Let’s simulate what happens when you press “Run”.

1. You write `.cs` file
    
2. Compiler converts it into IL
    
3. IL stored in assembly (.exe/.dll)
    
4. CLR loads assembly
    
5. CLR verifies type safety
    
6. JIT converts IL to machine code
    
7. OS executes machine code
    
8. Garbage Collector manages memory automatically
    

---

# 🏛️ C# Program Structure

Now let’s understand structure clearly.

---

## 🔹 Basic Structure

```csharp
using System;        // Namespace import

namespace MyApp      // Namespace
{
    class Program    // Class
    {
        static void Main(string[] args)  // Entry point
        {
            Console.WriteLine("Hello");
        }
    }
}
```

Let’s break this down:

---

## 1️⃣ Using Directive

```csharp
using System;
```

Imports namespace so we can use:

- Console
    
- Math
    
- DateTime
    

Without using:  
You must write:

```csharp
System.Console.WriteLine("Hello");
```

---

## 2️⃣ Namespace

```csharp
namespace MyApp
```

- Used to organize code
    
- Prevent naming conflicts
    
- Like packages in Java
    

Java equivalent:

```java
package com.example;
```

---

## 3️⃣ Class

```csharp
class Program
```

Everything in C# must be inside a class.

C# is fully object-oriented.

---

## 4️⃣ Main Method (Entry Point)

```csharp
static void Main(string[] args)
```

This is where execution starts.

Important parts:

- `static` → belongs to class
    
- `void` → no return value
    
- `string[] args` → command-line arguments
    

Without `Main()` → program cannot start.

---

# ⚙️ Memory Architecture

C# uses:

## 🟢 Stack

Stores:

- Local variables
    
- Method calls
    

## 🔵 Heap

Stores:

- Objects
    
- Reference types
    

Garbage Collector:

- Automatically removes unused objects from heap
    
- You don’t manually free memory
    

---

# 🔥 Managed vs Unmanaged Code

C# is **managed code**.

Meaning:

- Runs under CLR control
    
- Memory handled automatically
    

Unmanaged:

- C, C++
    
- Manual memory management
    

---

# 🆚 Java vs C# Architecture (Quick Compare)

|Java|C#|
|---|---|
|Java Code|C# Code|
|Bytecode|IL|
|JVM|CLR|
|JIT|JIT|
|GC|GC|

Very similar structure.





## q1

# 📦 What is an Assembly in C#?

In simple words:

> An **assembly** is the compiled output of a C# program.

When you compile your `.cs` file, you don’t directly get machine code.

You get an **assembly file**.

Usually:

- `.exe` → Executable assembly
    
- `.dll` → Library assembly
    

---

# 🔄 Where Does Assembly Fit in Architecture?

Flow again:

```
C# Code (.cs)
      ↓
C# Compiler
      ↓
Assembly (.exe / .dll)
      ↓
CLR
      ↓
JIT
      ↓
Machine Code
```

So assembly sits **between compilation and execution**.

---

# 🧠 What Does an Assembly Contain?

An assembly contains:

### 1️⃣ IL Code (Intermediate Language)

This is the actual compiled code.

### 2️⃣ Metadata

Information about:

- Classes
    
- Methods
    
- Variables
    
- References
    
- Version
    

This is powerful because:  
CLR reads metadata to understand your program structure.

### 3️⃣ Manifest

The manifest contains:

- Assembly name
    
- Version
    
- Culture
    
- Security info
    
- Referenced assemblies
    

Think of manifest like a “table of contents”.

---

# 🏗️ Types of Assemblies

## 🔹 1. EXE Assembly

- Entry point present (Main method)
    
- Can run directly
    

Example:

```
MyApp.exe
```

---

## 🔹 2. DLL Assembly

- No entry point
    
- Used as reusable library
    
- Imported into other projects
    

Example:

```
Utilities.dll
```

---

# 📁 Example

Suppose you write:

```csharp
class Program
{
    static void Main()
    {
        Console.WriteLine("Hello");
    }
}
```

After compilation:

You get:

```
Program.exe
```

This file is the **assembly**.

It contains:

- IL code
    
- Metadata
    
- Manifest
    

---

# 🆚 Java Comparison (So You Connect Faster)

|Java|C#|
|---|---|
|.class file|Assembly (.exe/.dll)|
|Bytecode|IL|
|JAR file|Assembly|
|JVM|CLR|

Assembly is similar to:

- `.jar` in Java
    
- `.class` file (but richer because it includes metadata)
    

---

# 🔥 What Makes Assembly Powerful?

Because of metadata inside assembly:

- CLR knows everything about your types
    
- Supports reflection
    
- Supports versioning
    
- Supports side-by-side execution
    

This is why .NET is very structured.

---

# 🧪 What is Single File vs Multiple File Assembly?

### Single-file assembly

Most common.  
Everything in one `.exe` or `.dll`.

### Multi-file assembly

Rarely used.  
One manifest file + multiple modules.

---

# 🧩 What is Strong Name Assembly?

An assembly can be digitally signed.

Strong name includes:

- Public key
    
- Version
    
- Culture
    

Used in:

- Enterprise apps
    
- Shared libraries
    

---

