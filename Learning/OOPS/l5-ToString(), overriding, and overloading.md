

If you understand **ToString(), overriding, and overloading**, you automatically revise:

- Inheritance
    
- Polymorphism
    
- Method overriding
    
- Method overloading
    

Let’s break it cleanly 👇

---

# 🔷 1️⃣ Every Class Inherits from `object`

In C#:

```csharp
class Book { }
```

Actually means:

```csharp
class Book : object { }
```

✔ Every class implicitly inherits from **object**  
✔ `object` class provides basic methods like:

- `ToString()`
    
- `Equals()`
    
- `GetHashCode()`
    

---

# 🔷 2️⃣ What is `ToString()`?

`ToString()` returns a string representation of an object.

Purpose:  
👉 Convert object data into readable text.

---

# 🔷 3️⃣ Default Behavior of `ToString()`

If you do NOT override it:

It returns:

```
Namespace.ClassName
```

---

## Example

```csharp
using System;

class Program
{
    static void Main()
    {
        object obj = new object();
        Console.WriteLine(obj.ToString());
    }
}
```

### ✅ Output

```
System.Object
```

Because default version just prints type name.

---

# 🔷 4️⃣ Built-in Types Override It

Example:

```csharp
int x = 1000;
Console.WriteLine(x.ToString());
```

### ✅ Output

```
1000
```

Because `int` already overrides `ToString()`.

---

# 🔷 5️⃣ Why Should We Override It?

If you create your own class:

```csharp
Book b = new Book();
Console.WriteLine(b);
```

Without overriding:

```
YourNamespace.Book
```

Which is useless for users.

So we override it to make it meaningful.

---

# 🔷 6️⃣ Overriding `ToString()` in Our Class

## Book.cs

```csharp
using System;

public class Book
{
    public string Name { get; set; }
    public string Author { get; set; }
    public int PageCount { get; set; }

    public Book(string name, string author, int pageCount)
    {
        Name = name;
        Author = author;
        PageCount = pageCount;
    }

    // Overriding base object method
    public override string ToString()
    {
        return $"Book: {Name} by {Author}";
    }
}
```

---

# 🔷 7️⃣ Using It in Program

```csharp
using System;

class Program
{
    static void Main()
    {
        Book b1 = new Book("Atomic Habits", "James Clear", 320);

        Console.WriteLine(b1.ToString());  // Explicit call
        Console.WriteLine(b1);             // Implicit call
    }
}
```

---

# 🖥 Output

```
Book: Atomic Habits by James Clear
Book: Atomic Habits by James Clear
```

---

# 🔥 Important Concept

Even if you write:

```csharp
Console.WriteLine(b1);
```

It automatically calls:

```csharp
b1.ToString()
```

That’s called **implicit conversion to string**.

---

# 🔷 8️⃣ Overriding vs Overloading

Very important difference 👇

|Overriding|Overloading|
|---|---|
|Same method signature|Different parameters|
|Uses `override` keyword|No override keyword|
|Parent method must be `virtual`|No parent version needed|

---

# 🔷 9️⃣ Overloading `ToString()`

Now we create another version with formatting.

### Book.cs (Extended Version)

```csharp
public override string ToString()
{
    return $"Book: {Name} by {Author}";
}

// Overloaded method (not overriding)
public string ToString(char format)
{
    if (format == 'B')
    {
        return $"Book -> {Name} : {Author}";
    }
    else if (format == 'F')
    {
        return $"{Name} by {Author} has {PageCount} pages.";
    }
    else
    {
        return ToString(); // call default version
    }
}
```

Notice:

- No `override` keyword
    
- Different parameter → this is overloading
    

---

# 🔷 10️⃣ Using Overloaded Version

```csharp
class Program
{
    static void Main()
    {
        Book b1 = new Book("Atomic Habits", "James Clear", 320);

        Console.WriteLine(b1);                // Default
        Console.WriteLine(b1.ToString('B')); // Short format
        Console.WriteLine(b1.ToString('F')); // Full format
    }
}
```

---

# 🖥 Output

```
Book: Atomic Habits by James Clear
Book -> Atomic Habits : James Clear
Atomic Habits by James Clear has 320 pages.
```

---

# 🔷 11️⃣ Why Not Use Override Keyword in Overloaded Version?

Because:

Base class `object` has:

```csharp
public virtual string ToString()
```

But it does NOT have:

```csharp
public string ToString(char format)
```

So we are not replacing anything — we are adding a new method.

That’s overloading.

---

# 🔥 Interview-Ready Summary

### ❓ Why override ToString()?

> To provide a meaningful string representation of an object suitable for display.

---

### ❓ What happens if we don't override it?

> It returns the fully qualified class name (namespace + class).

---

### ❓ Difference between overriding and overloading?

Overriding:

- Same method signature
    
- Uses `override`
    
- Supports runtime polymorphism
    

Overloading:

- Same method name
    
- Different parameters
    
- Compile-time polymorphism
    

---

# 🔥 Very Common Interview Trap

If interviewer asks:

```csharp
Console.WriteLine(book);
```

Which method gets called?

Correct answer:

> The overridden ToString() method.

---

# 🚀 Real-World Use Case

ToString() is used in:

- Logging
    
- Debugging
    
- Console apps
    
- API responses
    
- Printing object data
    

---
