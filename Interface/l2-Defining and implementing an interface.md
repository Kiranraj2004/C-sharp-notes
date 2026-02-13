
Now we move from theory ➝ practical implementation 👨‍💻

This example shows:

1. Creating a class (`Document`)
    
2. Creating an interface (`IStorable`)
    
3. Implementing that interface
    
4. Using it in `Main()`
    

---

# 🔹 Step 1: Basic Class (Before Interface)

First, we create a simple class.

```csharp
class Document
{
    private string name;

    public Document(string name)
    {
        this.name = name;
        Console.WriteLine("Created document with name: " + name);
    }
}
```

### 🔎 What this does:

- `name` → member variable
    
- Constructor → prints document name when object is created
    

---

### 🧪 Main Method

```csharp
class Program
{
    static void Main()
    {
        Document doc = new Document("Test Document");
    }
}
```

---

### ✅ Output:

```
Created document with name: Test Document
```

So far everything works fine.

---

# 🔹 Step 2: Create the Interface

Now we want:

- Ability to Save
    
- Ability to Load
    
- Property to check if document needs saving
    

---

## Interface Definition

```csharp
interface IStorable
{
    void Save();
    void Load();
    bool NeedsSave { get; set; }
}
```

---

## 🧠 Important Rules About Interfaces

1. No method body (no implementation)
    
2. No access modifiers (public/private not allowed)
    
3. Everything is implicitly public
    
4. No member variables
    
5. Only method signatures + properties
    

---

# 🔹 Step 3: Implement Interface (Incorrect Way First ❌)

If we write:

```csharp
class Document : IStorable
{
}
```

And try to run...

### ❌ Compile Error:

```
'Document' does not implement interface member 'IStorable.Save()'
'Document' does not implement interface member 'IStorable.Load()'
'Document' does not implement interface member 'IStorable.NeedsSave'
```

Because:

> If you implement an interface, you MUST implement all members.

---

# 🔹 Step 4: Correct Implementation ✅

```csharp
class Document : IStorable
{
    private string name;

    public Document(string name)
    {
        this.name = name;
        Console.WriteLine("Created document with name: " + name);
    }

    public void Save()
    {
        Console.WriteLine("Saving document...");
    }

    public void Load()
    {
        Console.WriteLine("Loading document...");
    }

    public bool NeedsSave { get; set; }
}
```

Now everything is properly implemented.

---

# 🔹 Step 5: Use Interface Methods in Main

```csharp
class Program
{
    static void Main()
    {
        Document doc = new Document("Test Document");

        doc.Load();
        doc.Save();
        doc.NeedsSave = false;
    }
}
```

---

### ✅ Final Output:

```
Created document with name: Test Document
Loading document...
Saving document...
```

---

# 🎯 What We Learned

### ✔ Interface Definition

```csharp
interface IStorable
{
    void Save();
    void Load();
    bool NeedsSave { get; set; }
}
```

- No implementation
    
- No access modifiers
    
- Only declarations
    

---

### ✔ Implementing Interface

```csharp
class Document : IStorable
```

- Use colon `:`
    
- Must implement ALL methods and properties
    

---

### ✔ Interface Enforces Contract

If you don't implement everything ➝ Compile error.

---

# 🔥 Extra: Using Interface as Reference Type (Polymorphism)

Instead of:

```csharp
Document doc = new Document("Test Document");
```

You can write:

```csharp
IStorable doc = new Document("Test Document");
```

This is powerful because:

- You now depend on behavior (interface)
    
- Not specific implementation (Document)
    

This is called **loose coupling**.

---

# 🧠 Important Interview Notes

1. Interface members are implicitly public.
    
2. Cannot declare fields (variables).
    
3. Cannot provide implementation (except C# 8+ default methods).
    
4. A class can implement multiple interfaces.
    
5. A class must implement ALL interface members.
    

---

# 🚀 Quick Summary (Revision)

- Interface = Contract
    
- Class implements using `:`
    
- Must implement all members
    
- No code inside interface
    
- Used for common behavior across different classes
    


# q1

1. ❓ Why do we create variables of interface type?
    
2. ❓ What is loose coupling?
    

Let’s break this clearly and simply.

---

# 🔹 1️⃣ Why Do We Create Variables of Interface Type?

Example:

```csharp
IStorable doc = new Document("Test Document");
```

Instead of:

```csharp
Document doc = new Document("Test Document");
```

Why?

---

## 🎯 The Real Reason

When you write:

```csharp
IStorable doc = new Document("Test Document");
```

You are saying:

> "I don’t care what the actual object is.  
> I only care that it can Save and Load."

You are programming based on **behavior**, not concrete class.

That is powerful.

---

# 🔹 Example to Understand This Clearly

Let’s say we have:

```csharp
interface IStorable
{
    void Save();
}
```

Two classes implement it:

```csharp
class Document : IStorable
{
    public void Save()
    {
        Console.WriteLine("Saving document...");
    }
}

class UserSettings : IStorable
{
    public void Save()
    {
        Console.WriteLine("Saving user settings...");
    }
}
```

---

## Case 1: Without Interface Variable ❌ (Tightly Coupled)

```csharp
Document doc = new Document();
doc.Save();
```

Now your code ONLY works with `Document`.

If tomorrow you want to use `UserSettings`?

You must rewrite your code.

---

## Case 2: Using Interface Variable ✅

```csharp
IStorable item;

item = new Document();
item.Save();

item = new UserSettings();
item.Save();
```

---

### ✅ Output:

```
Saving document...
Saving user settings...
```

Same variable.  
Different objects.  
Same behavior.

That is flexibility.

---

# 🔥 Now Let’s Understand Loose Coupling

---

## 🔹 What is Coupling?

Coupling = How strongly two classes depend on each other.

---

## ❌ Tight Coupling (Bad Design)

```csharp
class ReportGenerator
{
    private Document doc = new Document();

    public void Generate()
    {
        doc.Save();
    }
}
```

Problem:

- `ReportGenerator` is directly dependent on `Document`
    
- If you change Document → ReportGenerator breaks
    
- Hard to test
    
- Hard to extend
    

---

## ✅ Loose Coupling (Good Design)

```csharp
class ReportGenerator
{
    private IStorable item;

    public ReportGenerator(IStorable item)
    {
        this.item = item;
    }

    public void Generate()
    {
        item.Save();
    }
}
```

Now use it:

```csharp
ReportGenerator generator1 = new ReportGenerator(new Document());
generator1.Generate();

ReportGenerator generator2 = new ReportGenerator(new UserSettings());
generator2.Generate();
```

---

### ✅ Output:

```
Saving document...
Saving user settings...
```

---

# 🎯 Why This Is Loose Coupling

Because:

- `ReportGenerator` does NOT know what class it is using.
    
- It only knows: "Something that implements IStorable."
    

If tomorrow you create:

```csharp
class CloudStorage : IStorable
```

You don’t change ReportGenerator at all.

That is flexible architecture.

---

# 🔥 Real-World Analogy

Think about charging cable.

Your phone depends on:

> USB interface

Not on:

> Specific electricity source

You can connect:

- Power bank
    
- Laptop
    
- Wall adapter
    

Phone doesn't care.  
It just needs USB.

That is loose coupling.

---

# 🔹 Why Interface Variables Are Important

When you write:

```csharp
IStorable doc = new Document();
```

You get:

✅ Flexibility  
✅ Replaceable implementations  
✅ Easy unit testing  
✅ Scalable architecture  
✅ Follows SOLID principles (Dependency Inversion)

---

# 🔥 Interview-Level Definition

Loose Coupling means:

> Classes depend on abstractions (interfaces), not concrete implementations.

---

# 🧠 Super Important Rule

Always try to:

```
Depend on Interface
Not on Implementation
```

---

