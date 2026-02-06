
# 🔹 Why Do We Need Properties?

Earlier, we used **public methods** like:

```csharp
public string GetName() { return _name; }
public void SetName(string name) { _name = name; }
```

But that’s:

- Verbose
    
- Repetitive
    
- Not elegant
    

👉 Instead, C# gives us **Properties** — a clean way to control access to private fields.

---

# 🔹 What is a Property?

A **Property** is a special member that:

- Looks like a variable
    
- Works like a method (because it has logic inside)
    
- Controls access to private data (Encapsulation)
    

It combines:

- A **backing field** (private variable)
    
- A **getter**
    
- A **setter**
    

---

# 🔹 1️⃣ Basic Property Syntax

```csharp
private string _name;   // Backing field

public string Name
{
    get { return _name; }
    set { _name = value; }
}
```

### ✅ Important Points

- `get` → returns value
    
- `set` → assigns value
    
- `value` → special keyword (automatically provided)
    
- `_name` → backing field
    

---

# 🔹 2️⃣ Expression-Bodied Property (Shorter Version)

Instead of writing full `{ }` blocks:

```csharp
public string Author
{
    get => _author;
    set => _author = value;
}
```

Cleaner. Modern. Interview-friendly.

---

# 🔹 3️⃣ Read-Only Property

Remove `set`

```csharp
public int PageCount
{
    get => _pageCount;
}
```

Now:

```csharp
book.PageCount = 200; ❌ ERROR
```

Only readable, not writable.

---

# 🔹 4️⃣ Computed Property (Very Important)

Property whose value depends on other properties.

```csharp
public string Description
{
    get => $"{Name} by {Author} has {PageCount} pages";
}
```

✔ No backing field  
✔ Read-only  
✔ Calculated dynamically

Every time you call `Description`, it recomputes.

---

# 🔹 5️⃣ Auto-Implemented Properties

No backing field needed.

```csharp
public string ISBN { get; set; }
public decimal Price { get; set; }
```

C# internally creates hidden backing fields.

Used when:

- No validation logic needed
    
- Just storing data
    

---

# 🧠 Complete Example Code

## 🔹 Book.cs

```csharp
using System;

public class Book
{
    // Private fields
    private string _name;
    private string _author;
    private int _pageCount;

    // Property with full syntax
    public string Name
    {
        get { return _name; }
        set { _name = value; }
    }

    // Expression-bodied property
    public string Author
    {
        get => _author;
        set => _author = value;
    }

    public int PageCount
    {
        get => _pageCount;
        set => _pageCount = value;
    }

    // Computed property
    public string Description
    {
        get => $"{Name} by {Author} has {PageCount} pages";
    }

    // Auto-implemented properties
    public string ISBN { get; set; }
    public decimal Price { get; set; }
}
```

---

## 🔹 Program.cs

```csharp
using System;

class Program
{
    static void Main()
    {
        Book book = new Book();

        book.Name = "Atomic Habits";
        book.Author = "James Clear";
        book.PageCount = 320;

        Console.WriteLine("Name: " + book.Name);
        Console.WriteLine("Description: " + book.Description);

        book.ISBN = "123-456789";
        book.Price = 499.99m;

        Console.WriteLine("ISBN: " + book.ISBN);
        Console.WriteLine("Price: " + book.Price);

        // Modify values
        book.Name = "Deep Work";
        book.PageCount = 280;

        Console.WriteLine("\nAfter Updating:");
        Console.WriteLine("Description: " + book.Description);
        Console.WriteLine("Name: " + book.Name);
        Console.WriteLine("Page Count: " + book.PageCount);
    }
}
```

---

# 🖥 Output

```
Name: Atomic Habits
Description: Atomic Habits by James Clear has 320 pages
ISBN: 123-456789
Price: 499.99

After Updating:
Description: Deep Work by James Clear has 280 pages
Name: Deep Work
Page Count: 280
```

---

# 🔥 Interview Summary (Very Important)

If interviewer asks:

### ❓ What is a property in C#?

You say:

> A property in C# is a class member that provides controlled access to private fields using getter and setter methods. It supports encapsulation and can include validation or computed logic.

---

### ❓ What is backing field?

Private variable that stores the actual data controlled by a property.

---

### ❓ What is auto-implemented property?

Property where C# automatically creates the backing field.

---

### ❓ What is computed property?

A property that calculates its value dynamically from other properties.

---

# 🚀 Why Properties Are Powerful

✔ Encapsulation  
✔ Cleaner syntax  
✔ Supports validation  
✔ Supports read-only / write-only  
✔ Supports computed values

---

If you want, next I can:

- 🔥 Add validation example (like preventing negative page count)
    
- 🔥 Explain difference between field vs property (very common interview trap)
    
- 🔥 Give you 3 tricky interview questions on properties
    

What do you want to practice next, Kiran?