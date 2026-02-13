
# 🔹 1️⃣ The Problem: Single Inheritance Limitation

In C#:

```csharp
class A { }
class B { }

// ❌ Not allowed
class C : A, B { }
```

A class can inherit from **only one base class**.

This is called **Single Inheritance**.

---

# 🔹 2️⃣ The Solution: Multiple Interfaces ✅

While C# does NOT support multiple class inheritance,  
it DOES support:

> Multiple Interface Implementation

---

# 🔹 Why Is This Useful?

Sometimes a class needs:

- Storage behavior
    
- Encryption behavior
    
- Logging behavior
    
- Printing behavior
    

These are separate features.

Instead of putting everything into one big class,  
we separate them into interfaces.

---

# 🔹 Example Scenario

We want a `Document` to:

1. Be stored (Save/Load)
    
2. Be encrypted (Encrypt/Decrypt)
    

These are unrelated features.

So we create:

- `IStorable`
    
- `IEncryptable`
    

---

# 🧩 Step 1: Define First Interface

```csharp
interface IStorable
{
    void Save();
    void Load();
}
```

---

# 🧩 Step 2: Define Second Interface

```csharp
interface IEncryptable
{
    void Encrypt();
    void Decrypt();
}
```

---

# 🧩 Step 3: Implement Multiple Interfaces

Notice the comma `,`

```csharp
class Document : IStorable, IEncryptable
{
    public void Save()
    {
        Console.WriteLine("Saving document...");
    }

    public void Load()
    {
        Console.WriteLine("Loading document...");
    }

    public void Encrypt()
    {
        Console.WriteLine("Encrypting document...");
    }

    public void Decrypt()
    {
        Console.WriteLine("Decrypting document...");
    }
}
```

---

# 🧩 Step 4: Use in Main Method

```csharp
class Program
{
    static void Main()
    {
        Document doc = new Document();

        doc.Load();
        doc.Encrypt();
        doc.Save();
        doc.Decrypt();
    }
}
```

---

# ✅ Output:

```
Loading document...
Encrypting document...
Saving document...
Decrypting document...
```

---

# 🔥 What Just Happened?

The `Document` class now has:

✔ Storage capability  
✔ Encryption capability

Without inheriting from multiple base classes.

---

# 🔹 Important Syntax Rule

To implement multiple interfaces:

```csharp
class ClassName : Interface1, Interface2, Interface3
```

Separated by commas.

---

# 🔹 Why This Is Powerful

Interfaces allow:

- Separation of concerns
    
- Clean architecture
    
- Feature-based design
    
- Flexibility
    

Each interface represents a clear behavior.

---

# 🔥 Real-World Analogy

Think of a smartphone.

It can:

- Call (ICallable)
    
- Take photos (ICamera)
    
- Connect to WiFi (IConnectable)
    
- Play music (IMediaPlayer)
    

It doesn't inherit from 4 parent devices.

It just supports multiple capabilities.

---

# 🔹 Interface Polymorphism Example

You can use interface references:

```csharp
IStorable s = new Document();
s.Save();

IEncryptable e = new Document();
e.Encrypt();
```

Same object.  
Different interface view.

---

# 🔥 Output:

```
Saving document...
Encrypting document...
```

---

# 🧠 Key Concepts to Remember

1. C# supports single class inheritance.
    
2. C# supports multiple interface implementation.
    
3. Interfaces separate behavior cleanly.
    
4. Use comma to implement multiple interfaces.
    
5. Class must implement ALL members of all interfaces.
    

---



# 🔎 What About Method Name Collisions?

What if both interfaces have:

```csharp
void Save();
```

How does C# handle that?

That requires something called:

> Explicit Interface Implementation

That’s the advanced concept mentioned at the end of your transcript.

---

# q1

# 🔹 Suppose We Have

```csharp
interface IStorable
{
    void Save();
    void Load();
}

interface IEncryptable
{
    void Encrypt();
    void Decrypt();
}

class Document : IStorable, IEncryptable
{
    public void Save()
    {
        Console.WriteLine("Saving document...");
    }

    public void Load()
    {
        Console.WriteLine("Loading document...");
    }

    public void Encrypt()
    {
        Console.WriteLine("Encrypting document...");
    }

    public void Decrypt()
    {
        Console.WriteLine("Decrypting document...");
    }
}
```

---

# 🔹 Now Your Question

If we write:

```csharp
IStorable obj = new Document();
```

What methods can we call?

Can we call `Encrypt()`?

---

# 🎯 Answer

👉 You can ONLY call methods defined inside `IStorable`.

So this is allowed:

```csharp
obj.Save();
obj.Load();
```

But this is ❌ NOT allowed:

```csharp
obj.Encrypt();   // ❌ Compile-time error
```

---

# 🔥 Why?

Because the **reference type controls what is accessible**, not the object type.

Important rule:

> The variable type decides what methods you can access.

Even though the object is `Document`,  
the reference type is `IStorable`.

So the compiler only sees:

```csharp
void Save();
void Load();
```

---

# 🧠 Think of It Like This

Imagine:

```
Document object = Big Machine
IStorable reference = Small Window
```

Through that window, you can only see:

- Save
    
- Load
    

Even though the machine has Encrypt and Decrypt,  
the window does not show them.

---

# 🔹 Demonstration Code

```csharp
class Program
{
    static void Main()
    {
        IStorable obj = new Document();

        obj.Save();   // ✅ works
        obj.Load();   // ✅ works

        // obj.Encrypt();  ❌ compile error
    }
}
```

---

# 🔹 Output

```
Saving document...
Loading document...
```

---

# 🔹 How To Access Encrypt Then?

You must cast it.

---

## Option 1: Use `as`

```csharp
IEncryptable enc = obj as IEncryptable;

if (enc != null)
{
    enc.Encrypt();
}
```

---

## Option 2: Use Pattern Matching (Modern C#)

```csharp
if (obj is IEncryptable encryptable)
{
    encryptable.Encrypt();
}
```

---

### ✅ Output:

```
Encrypting document...
```

---

# 🔥 Very Important Concept

There are TWO TYPES involved:

```
Reference Type → IStorable
Object Type → Document
```

### Compile-time checks → use Reference Type

### Runtime object → is Document

---

# 🔹 Another Example

```csharp
Document doc = new Document();
```

Now you can call:

```
doc.Save();
doc.Load();
doc.Encrypt();
doc.Decrypt();
```

Because reference type is `Document`.

---

# 🔥 Rule Summary

|Reference Type|What You Can Call|
|---|---|
|Document|All methods|
|IStorable|Only Save, Load|
|IEncryptable|Only Encrypt, Decrypt|

---

# 🎯 Why This Is Useful?

Because it enforces abstraction.

If a method accepts:

```csharp
void Process(IStorable item)
```

You are guaranteed:

- It can Save
    
- It can Load
    

But you don't care if it can Encrypt.

That is clean design.

---

