
# 🧠 What Does “Compiling C#” Mean?

When you write:

```
person.cs
```

It’s just **source code**.

To run or reuse it, you must compile it into:

- An **Executable (.exe)** → runnable program  
    OR
    
- A **Library (.dll)** → reusable code
    

---

# 🏗 Two Types of Compilation Targets

The C# compiler (`csc`) can create:

## 1️⃣ Executable (.exe)

- Has `Main()` method
    
- Can run directly
    
- Entry point exists
    
- Example: Console App
    

---

## 2️⃣ Library (.dll)

- No entry point required
    
- Cannot run directly
    
- Used by other programs
    
- Contains reusable classes
    

---

# 🛠 Using the C# Compiler (csc)

From command prompt:

```
csc person.cs
```

By default → creates an executable.

But if you want a library:

```
csc person.cs /target:library /out:personlibrary.dll
```

---

## 🔎 What These Parameters Mean

|Parameter|Meaning|
|---|---|
|`csc`|C# compiler|
|`person.cs`|Input source file|
|`/target:library`|Build DLL instead of EXE|
|`/out:personlibrary.dll`|Output file name|

---

# 📦 Example 1: Compiling a Library

## 📝 person.cs

```csharp
public class Person
{
    public string Name { get; set; }

    public void Greet()
    {
        System.Console.WriteLine("Hello " + Name);
    }
}
```

---

## 🔧 Compile as Library

```
csc person.cs /target:library /out:personlibrary.dll
```

Now you get:

```
personlibrary.dll
```

✔ Contains MSIL  
✔ Contains Person class  
✔ Not directly runnable

---

# 🔍 Viewing DLL in ILDASM

If you open `personlibrary.dll` in ILDASM:

You will see:

- Person class
    
- Backing fields
    
- get_Name()
    
- set_Name()
    
- Greet()
    

All converted into MSIL.

Even DLLs contain MSIL — same as EXEs.

---

# 🧠 Important Concept

DLL and EXE both:

✔ Contain MSIL  
✔ Run using CLR  
✔ Use BCL  
✔ Are assemblies

The only difference:

EXE → Has entry point  
DLL → Does not

---

# 🏗 Example 2: Using That Library

Now suppose you have:

## 📝 program.cs

```csharp
class Program
{
    static void Main()
    {
        Person p = new Person();
        p.Name = "Kiran";
        p.Greet();
    }
}
```

---

To compile this and link the DLL:

```
csc program.cs /reference:personlibrary.dll
```

This tells compiler:

> “Use this external library.”

---

## 🖥 Output When Run

```
Hello Kiran
```

---

# 🧩 What Happened Internally?

Step-by-step:

1️⃣ person.cs → compiled into personlibrary.dll  
2️⃣ program.cs → compiled referencing DLL  
3️⃣ Both contain MSIL  
4️⃣ CLR executes them  
5️⃣ JIT converts to machine code

---

# 📚 What Is an Assembly?

Both `.dll` and `.exe` are called:

> Assemblies in .NET

An assembly contains:

- MSIL
    
- Metadata
    
- Manifest
    
- Version info
    
- Type definitions
    

---

# 🎯 Why Compile as DLL?

Because in real projects:

You don’t write everything in one file.

You separate:

- Business logic
    
- Data access
    
- Utilities
    
- Services
    

Example:

```
MyApp.exe
MyBusinessLogic.dll
MyDataAccess.dll
```

Each compiled separately.

That’s modular design.

---

# 🧠 Interview-Level Understanding

If interviewer asks:

### ❓ Difference between EXE and DLL in .NET?

You say:

> Both are assemblies containing MSIL. An EXE contains an entry point (Main method) and can run independently. A DLL is a reusable library that must be referenced by another assembly.

---

### ❓ What happens when you compile C#?

You say:

> The C# compiler converts source code into MSIL and packages it into an assembly, either a DLL or EXE, which is then executed by the CLR.

---

# 🔥 Real-World Development Note

Today we rarely use `csc` manually.

Instead we use:

```
dotnet build
dotnet run
```

But internally:  
It still uses the same compiler.

---

# 🧠 Big Picture Architecture

```
C# Source Code
      ↓
csc Compiler
      ↓
Assembly (.dll or .exe)
      ↓
CLR Runtime
      ↓
JIT Compiler
      ↓
Machine Code
      ↓
Execution
```

---

## q1

You’re thinking:

> “Instead of creating an object of Person, what if Program just inherits from Person? Then I can access its properties and methods directly.”

Something like this:

```csharp
class Program : Person
{
    static void Main()
    {
        Program p = new Program();
        p.Name = "Kiran";
        p.Greet();
    }
}
```

Yes — this works **IF Person is visible to the compiler**.

But that’s the key point.

---

# 🚨 The Real Issue Is NOT Object vs Inheritance

The real issue is:

👉 **Does the compiler know what Person is?**

If `Person` is:

- In the same file → ✅ works
    
- In the same compilation → ✅ works
    
- In another DLL without reference → ❌ compiler error
    

Inheritance does NOT magically import code.

---

# 🔍 Why It Still Needs a Reference

Let’s say:

1. You compiled `Person` into `personlibrary.dll`
    
2. Now you write:
    

```csharp
class Program : Person
{
}
```

If you compile:

```
csc program.cs
```

You’ll get:

```
error CS0246: The type or namespace name 'Person' could not be found
```

Because the compiler has no idea where Person lives.

So you must do:

```
csc program.cs /reference:personlibrary.dll
```

Only then it works.

---

# 🧠 Important Concept

Inheritance is a **language feature**.

Referencing a DLL is a **compiler requirement**.

These are two different levels.

---

# 🏗 Think of It Like This

Inheritance =  
“Program is a Person.”

Reference =  
“Hey compiler, Person is defined in this assembly.”

Without reference, inheritance can’t even begin.

---

# 🎯 Why Object Creation vs Inheritance Doesn't Matter

Whether you do:

```csharp
Person p = new Person();
```

OR

```csharp
class Program : Person
```

Both require the compiler to:

- Know Person’s definition
    
- Know its metadata
    
- Know its methods
    
- Know its properties
    

And that metadata lives in the DLL.

So the DLL must be referenced.

---

# 🔥 Simple Rule to Remember

If code is compiled separately into another assembly:

👉 You MUST reference that assembly  
No matter if you:

- Create object
    
- Inherit
    
- Use static method
    
- Use extension method
    

Always required.

---

# 🧠 Big Mental Model

Compilation works like this:

Compiler only sees:

- Files being compiled
    
- Referenced assemblies
    

It does NOT:

- Search your folders automatically
    
- Guess your types
    
- Merge code magically
    

---

