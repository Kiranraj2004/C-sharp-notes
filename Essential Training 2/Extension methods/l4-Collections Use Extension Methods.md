

Take this collection:

```csharp
List<string> names = new List<string>
{
    "Kiran",
    "Xi",
    "Alexander",
    "Raj",
    "Sam"
};
```

When you type:

```csharp
names.
```

You suddenly see:

- `Where()`
    
- `Select()`
    
- `OrderBy()`
    
- `Distinct()`
    
- `MinBy()`
    
- `Average()`
    
- `ElementAt()`
    
- `Cast()`
    
- `AsQueryable()`
    

Here’s the important thing:

👉 These are NOT methods inside `List<T>`.

They are extension methods from:

```csharp
using System.Linq;
```

LINQ = Language Integrated Query.

---

# 🔥 Example 1: MinBy (C# 10+)

### Goal:

Find the shortest name.

### Code:

```csharp
using System;
using System.Collections.Generic;
using System.Linq;

class Program
{
    static void Main()
    {
        List<string> names = new List<string>
        {
            "Kiran",
            "Xi",
            "Alexander",
            "Raj",
            "Sam"
        };

        var shortest = names.MinBy(s => s.Length);

        Console.WriteLine(shortest);
    }
}
```

---

### 🔎 What Is Happening?

```csharp
names.MinBy(s => s.Length);
```

We are saying:

- Give me each string `s`
    
- Return its `Length`
    
- Find the minimum based on that value
    

---

### ✅ Output:

```
Xi
```

Because `"Xi"` has length 2 (shortest).

---

# 🔥 Example 2: OrderBy

Now let’s sort names by length.

### Code:

```csharp
var orderedNames = names.OrderBy(s => s.Length);

foreach (var name in orderedNames)
{
    Console.WriteLine(name);
}
```

---

### 🔎 What Happens?

`OrderBy()`:

- Takes each string
    
- Evaluates `s.Length`
    
- Sorts based on that value
    
- Returns a new collection
    

Important:  
It does NOT modify original list.

---

### ✅ Output:

```
Xi
Raj
Sam
Kiran
Alexander
```

Shortest → Longest

---

# 🔥 Important Understanding

These methods:

- MinBy()
    
- OrderBy()
    
- Where()
    
- Select()
    

Are NOT part of:

```csharp
List<T>
```

They are extension methods from:

```csharp
System.Linq
```

If you remove:

```csharp
using System.Linq;
```

They disappear.

Red squiggly again 😅

---

# 🔹 Why This Is So Powerful

Without extension methods, sorting would look like:

```csharp
names.Sort((a, b) => a.Length.CompareTo(b.Length));
```

But LINQ makes it:

```csharp
names.OrderBy(s => s.Length);
```

Much more readable.

Much more declarative.

---

# 🔥 More Common Collection Extension Methods

### 1️⃣ Where (Filtering)

```csharp
var shortNames = names.Where(s => s.Length <= 3);

foreach (var name in shortNames)
{
    Console.WriteLine(name);
}
```

### ✅ Output:

```
Xi
Raj
Sam
```

---

### 2️⃣ Select (Projection)

```csharp
var nameLengths = names.Select(s => s.Length);

foreach (var length in nameLengths)
{
    Console.WriteLine(length);
}
```

### ✅ Output:

```
5
2
9
3
3
```

---

### 3️⃣ Distinct

```csharp
List<string> duplicateNames = new List<string>
{
    "Kiran", "Xi", "Kiran", "Raj"
};

var unique = duplicateNames.Distinct();

foreach (var name in unique)
{
    Console.WriteLine(name);
}
```

### ✅ Output:

```
Kiran
Xi
Raj
```

---

# 🔥 Big Concept From Transcript

Extension methods allow us to:

✔ Query collections  
✔ Transform collections  
✔ Filter collections  
✔ Sort collections  
✔ Aggregate data

All in a clean, readable way.

---

# 🔹 Behind The Scenes

When you write:

```csharp
names.OrderBy(...)
```

Compiler converts it to:

```csharp
Enumerable.OrderBy(names, ...)
```

These methods live in:

```csharp
System.Linq.Enumerable
```

They are static extension methods.

---

# 🔥 Interview-Level Explanation

If interviewer asks:

**Why are LINQ methods extension methods?**

You can say:

> LINQ methods are implemented as extension methods so they can extend any type that implements IEnumerable without modifying those types directly.

That’s a strong answer.

---

# 🧠 Final Summary Notes

• Most common extension methods are used on collections  
• They come from `System.Linq`  
• They extend `IEnumerable<T>`  
• They do not modify the original collection  
• They return new sequences  
• They make code readable and expressive

---

Now here’s a small question for you 😏

If I write:

```csharp
var result = names.OrderBy(s => s.Length);
```

Will the original `names` list be sorted permanently?

Think about it.  
Answer me.