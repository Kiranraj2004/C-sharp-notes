
### 🔹 1. What is a Class?

- A **class** defines an **object template**.
    
- It contains:
    
    - **Data (fields)**
        
    - **Methods (behavior + logic)**
        
- Used to create multiple objects with different data.
    

```csharp
class Document
{
    public string Title;
}
```

👉 Here, `Document` defines what a document object looks like.

---

### 🔹 2. What is an Interface?

- An **interface defines behavior only**.
    
- It does NOT contain implementation (logic).
    
- It only declares:
    
    - Method signatures
        
    - Properties
        
    - Events (advanced)
        

💡 Think of an interface as a **contract**:

> “If you implement me, you must provide these methods.”

---

### 🔹 3. Key Differences: Class vs Interface

|Feature|Class|Interface|
|---|---|---|
|Defines object?|✅ Yes|❌ No|
|Contains implementation?|✅ Yes|❌ No (only method declarations)|
|Can inherit multiple?|❌ No (single inheritance)|✅ Yes (multiple interfaces allowed)|
|Purpose|Create objects|Define capabilities|

---

### 🔹 4. Why Use Interfaces?

Let’s say:

- Documents can be saved
    
- User preferences can also be saved
    

But:

- Preferences are NOT documents
    
- So they shouldn't inherit from a `Document` class
    

✅ Solution → Create an interface like `IStorable`

Now:

- `Document` can implement it
    
- `UserPreferences` can implement it
    
- Both get "save/load" behavior
    
- No unnecessary inheritance
    

---

## 🧠 Naming Convention

In C#, interfaces usually start with **I**

Examples:

- `IStorable`
    
- `IComparable`
    
- `IDisposable`
    

---

# 🧩 Example 1: Basic Interface Implementation

### Step 1: Define Interface

```csharp
interface IStorable
{
    void Save();
    void Load();
}
```

---

### Step 2: Implement Interface in a Class

```csharp
class Document : IStorable
{
    public string Title;

    public void Save()
    {
        Console.WriteLine("Document saved.");
    }

    public void Load()
    {
        Console.WriteLine("Document loaded.");
    }
}
```

---

### Step 3: Use in Main Method

```csharp
class Program
{
    static void Main()
    {
        Document doc = new Document();
        doc.Save();
        doc.Load();
    }
}
```

---

### ✅ Output:

```
Document saved.
Document loaded.
```

---

# 🧩 Example 2: Multiple Classes Using Same Interface

### Interface

```csharp
interface IStorable
{
    void Save();
    void Load();
}
```

---

### Class 1: Document

```csharp
class Document : IStorable
{
    public void Save()
    {
        Console.WriteLine("Document saved.");
    }

    public void Load()
    {
        Console.WriteLine("Document loaded.");
    }
}
```

---

### Class 2: UserPreferences

```csharp
class UserPreferences : IStorable
{
    public void Save()
    {
        Console.WriteLine("Preferences saved.");
    }

    public void Load()
    {
        Console.WriteLine("Preferences loaded.");
    }
}
```

---

### Main Method

```csharp
class Program
{
    static void Main()
    {
        IStorable doc = new Document();
        IStorable prefs = new UserPreferences();

        doc.Save();
        prefs.Save();
    }
}
```

---

### ✅ Output:

```
Document saved.
Preferences saved.
```

---

## 🔥 Important Concept: Polymorphism with Interfaces

Notice this:

```csharp
IStorable doc = new Document();
```

We are using the **interface type as reference**.

This allows:

- Writing flexible code
    
- Handling different object types in same way
    

Example:

```csharp
List<IStorable> items = new List<IStorable>();

items.Add(new Document());
items.Add(new UserPreferences());

foreach (var item in items)
{
    item.Save();
}
```

### ✅ Output:

```
Document saved.
Preferences saved.
```

---

# 🎯 Why Not Just Use a Base Class?

Suppose:

```csharp
class BaseDocument
{
    public void Save() { }
}
```

Problem:

- What if `UserPreferences` is NOT a document?
    
- C# allows only **single inheritance**
    
- So it can't inherit from two base classes
    

But it **can implement multiple interfaces**:

```csharp
class MyClass : IStorable, IPrintable, ILoggable
```

This makes interfaces very powerful.

---

# 📌 When Should You Use Interfaces?

Use interfaces when:

- Multiple unrelated classes share behavior
    
- You want loose coupling
    
- You want better testability
    
- You need polymorphism
    
- You want to follow SOLID principles
    

---

# 🧠 Simple Real-World Analogy

Interface = **Ability**

Examples:

- `IFlyable`
    
- `ISwimmable`
    
- `IDrivable`
    

A:

- Bird → IFlyable
    
- Airplane → IFlyable
    
- Fish → ISwimmable
    
- Car → IDrivable
    

They are not same type of object  
But they share same **capability**

---

# q1

## ❓ Situation

Suppose your interface has **2 methods**, but your class implements **only 1 method**.

What happens?

---

## ✅ Answer

👉 **You will get a compile-time error.**  
C# will not allow your class to compile.

Because:

> When a class implements an interface, it MUST implement ALL members of that interface.

It’s a strict contract.

---

## 🔎 Example

### Step 1: Define Interface

```csharp
interface IStorable
{
    void Save();
    void Load();
}
```

---

### Step 2: Implement Only One Method (Wrong Way ❌)

```csharp
class Document : IStorable
{
    public void Save()
    {
        Console.WriteLine("Saved");
    }
}
```

---

### ❌ What Happens?

You will get a compile-time error like:

```
'Document' does not implement interface member 'IStorable.Load()'
```

The program will NOT compile.

---

## 🎯 Why Does This Happen?

Because interface is a **contract**.

If you say:

```csharp
class Document : IStorable
```

You are telling C#:

> "I promise to provide both Save() and Load() methods."

If you break that promise → compiler error.

---

## ✅ Correct Way

```csharp
class Document : IStorable
{
    public void Save()
    {
        Console.WriteLine("Saved");
    }

    public void Load()
    {
        Console.WriteLine("Loaded");
    }
}
```

Now it works perfectly.

---

## 🔥 Important Interview Point

Interfaces are:

- Enforced at **compile time**
    
- Strict contracts
    
- Cannot partially implement methods
    

---

## 🧠 Special Case (Advanced)

If your class is declared as **abstract**, then it can skip implementing methods.

Example:

```csharp
abstract class Document : IStorable
{
    public void Save()
    {
        Console.WriteLine("Saved");
    }
}
```

This is allowed because:

- Abstract class does NOT need to fully implement interface
    
- But any non-abstract child class must implement remaining methods
    

---
