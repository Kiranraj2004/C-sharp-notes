
# 🔷 What is Inheritance?

👉 Inheritance allows one class to reuse properties and methods from another class.

It helps:

- Avoid code duplication
    
- Create logical hierarchy
    
- Improve maintainability
    
- Support polymorphism
    

---

# 🔷 The Problem (Without Inheritance)

Suppose we have:

### Book class

- Name
    
- PageCount
    
- Price
    
- Author
    

### Magazine class

- Name
    
- PageCount
    
- Price
    
- Publisher
    

🚨 Problem:  
Both classes repeat:

- Name
    
- PageCount
    
- Price
    

If we change logic for Price later, we must modify in both places → error-prone.

---

# 🔷 The Solution: Create a Parent Class

We create a base class:

```
Publication
```

It will contain common properties:

- Name
    
- PageCount
    
- Price
    

Then:

```
Book : Publication
Magazine : Publication
```

---

# 🔷 Basic Inheritance Syntax

```csharp
class ChildClass : ParentClass
```

Example:

```csharp
class Book : Publication
```

---

# 🔷 Step 1 — Create Parent Class

## Publication.cs

```csharp
using System;

public class Publication
{
    private string _name;

    public string Name
    {
        get => _name;
        set
        {
            if (string.IsNullOrWhiteSpace(value))
                throw new ArgumentException("Name cannot be blank");

            _name = value;
        }
    }

    public int PageCount { get; set; }
    public decimal Price { get; set; }

    // Virtual method (can be overridden)
    public virtual string GetDescription()
    {
        return $"{Name} has {PageCount} pages.";
    }

    // Constructor
    public Publication(string name, int pageCount, decimal price)
    {
        Name = name;
        PageCount = pageCount;
        Price = price;
    }
}
```

---

# 🔷 Important Concepts Here

### ✅ 1. Validation inside property

We prevent Name from being empty.

```csharp
if (string.IsNullOrWhiteSpace(value))
    throw new ArgumentException("Name cannot be blank");
```

This is a good use of properties.

---

### ✅ 2. Virtual Method

```csharp
public virtual string GetDescription()
```

- `virtual` means child classes can override this method.
    

---

# 🔷 Step 2 — Create Book Class

## Book.cs

```csharp
public class Book : Publication
{
    public string Author { get; set; }

    public Book(string name, int pageCount, decimal price, string author)
        : base(name, pageCount, price)
    {
        Author = author;
    }

    public override string GetDescription()
    {
        return $"{Name} by {Author} has {PageCount} pages. Price: {Price}";
    }
}
```

---

# 🔷 Important Concepts

### ✅ 1. Colon `: base(...)`

```csharp
: base(name, pageCount, price)
```

This calls the constructor of the parent class.

Parent constructor runs first.

---

### ✅ 2. Override

```csharp
public override string GetDescription()
```

- Parent method must be `virtual`
    
- Child method must use `override`
    

---

# 🔷 Step 3 — Create Magazine Class

## Magazine.cs

```csharp
public class Magazine : Publication
{
    public string Publisher { get; set; }

    public Magazine(string name, int pageCount, decimal price, string publisher)
        : base(name, pageCount, price)
    {
        Publisher = publisher;
    }

    // Not overriding GetDescription
}
```

Here:

- It inherits the default version from Publication.
    

---

# 🔷 Step 4 — Program.cs

```csharp
using System;

class Program
{
    static void Main()
    {
        Book book = new Book("Atomic Habits", 320, 499.99m, "James Clear");
        Magazine magazine = new Magazine("Tech Today", 50, 199.99m, "TechWorld");

        Console.WriteLine("Book Info:");
        Console.WriteLine(book.GetDescription());

        Console.WriteLine("\nMagazine Info:");
        Console.WriteLine(magazine.GetDescription());

        // Uncomment to test exception
        // book.Name = "";
    }
}
```

---

# 🖥 Output

```
Book Info:
Atomic Habits by James Clear has 320 pages. Price: 499.99

Magazine Info:
Tech Today has 50 pages.
```

---

# 🔥 What Happens If We Do This?

```csharp
book.Name = "";
```

Output:

```
Unhandled Exception: System.ArgumentException: Name cannot be blank
```

Because validation is inside the property.

---

# 🔷 Key OOP Concepts Covered

### 1️⃣ Inheritance

Child class inherits from parent.

### 2️⃣ Constructor Chaining

Using `: base(...)`

### 3️⃣ Method Overriding

Using `virtual` + `override`

### 4️⃣ Code Reusability

Common properties defined once.

### 5️⃣ Encapsulation

Validation inside property setter.

---

# 🔷 Why This Is Powerful

Without inheritance:

- Code duplication
    
- Hard to maintain
    
- Bug-prone
    

With inheritance:

- Clean structure
    
- Centralized logic
    
- Easy customization
    

---

# 🔥 Interview-Ready Answers

### ❓ What is inheritance in C#?

> Inheritance allows a class to derive from another class and reuse its properties and methods. It helps reduce duplication and supports polymorphism.

---

### ❓ What is the purpose of `base` keyword?

> It is used to call the constructor or methods of the parent class.

---

### ❓ What is the difference between virtual and override?

- `virtual` → defined in parent
    
- `override` → redefined in child
    

---

# 🚀 Next Level (Very Important for Placements)

If you want, next we can cover:

- 🔥 Polymorphism using base class reference
    
- 🔥 Sealed classes
    
- 🔥 Abstract classes
    
- 🔥 Method hiding vs overriding (very tricky question)
    
- 🔥 Real interview tricky scenario
    

Tell me what you want to master next 😎