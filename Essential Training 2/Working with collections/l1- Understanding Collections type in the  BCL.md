

# 🧠 1. Why Do We Need Collections?

When we create multiple objects of the same type:

```csharp
string[] names = { "Matt", "Milner" };
```

Arrays:

- ✅ Store multiple items
    
- ❌ Fixed size
    
- ❌ Cannot grow automatically
    
- ✅ Zero-based indexing
    

If you try:

```csharp
names[2] = "John";  // ❌ Error
```

You’ll get an **IndexOutOfRangeException**.

---

# 📦 2. What is BCL?

**BCL (Base Class Library)** is part of the .NET Framework that provides:

- Collections
    
- File handling
    
- Networking
    
- Data structures
    
- LINQ
    
- and more...
    

Collections are available inside:

```
System.Collections
System.Collections.Generic   ← (Better version)
```

---

# 🧰 3. ArrayList (Non-Generic Collection)

📍 Namespace: `System.Collections`

```csharp
ArrayList al = new ArrayList();
```

## Important Things About ArrayList

- Stores **object**
    
- Can store **any data type**
    
- Automatically resizes
    
- Implements important interfaces
    

---

# 🧩 4. Important Interfaces

ArrayList implements:

### 1️⃣ IEnumerable

- Used for `foreach`
    
- Has `GetEnumerator()`
    
- Allows iteration
    

### 2️⃣ ICollection

- Has `Count`
    
- Can copy items
    
- Inherits IEnumerable
    

### 3️⃣ IList

- Has `Add()`
    
- `Insert()`
    
- `Remove()`
    
- `Contains()`
    
- Indexing support `[index]`
    

---

# 🧪 5. Example Code (Like in Transcript)

```csharp
using System;
using System.Collections;

class Program
{
    static void Main()
    {
        // Array example
        string[] names = { "Matt", "Milner" };
        Console.WriteLine("Hello " + names[0] + " " + names[1]);

        // ArrayList example
        ArrayList al = new ArrayList(2);

        al.Add("First");

        al.AddRange(new string[] { "Second", "Third", "Fourth" });

        Console.WriteLine("Collection size is {0}", al.Count);

        Console.WriteLine("Indexed item from collection: {0}", al[2]);

        Console.WriteLine("All items in the list:");

        foreach (var item in al)
        {
            Console.WriteLine(item);
        }
    }
}
```

---

# 🖥️ Output

```
Hello Matt Milner
Collection size is 4
Indexed item from collection: Third
All items in the list:
First
Second
Third
Fourth
```

---

# 🚨 6. Important Problem With ArrayList

Notice this method:

```csharp
al.Add("First");
```

The `Add()` method takes:

```csharp
public virtual int Add(object value)
```

⚠️ That means everything is stored as **object**.

So you could accidentally do:

```csharp
al.Add(100);
al.Add(true);
```

Now your list contains:

- string
    
- int
    
- bool
    

This causes:

- Runtime errors
    
- Boxing & unboxing
    
- No type safety
    

Example:

```csharp
string s = (string)al[1]; // ❌ might crash at runtime
```

---

# 💡 7. Why Generics Are Better

Instead of:

```csharp
ArrayList al = new ArrayList();
```

Use:

```csharp
List<string> list = new List<string>();
```

From:

```
System.Collections.Generic
```

Now:

```csharp
list.Add("First");
// list.Add(100); ❌ Compile-time error
```

✅ Type safe  
✅ No casting  
✅ Better performance  
✅ No boxing/unboxing

---

# 📊 Array vs ArrayList vs List

|Feature|Array|ArrayList|List|
|---|---|---|---|
|Fixed size|Yes|No|No|
|Type safe|Yes|No|Yes|
|Auto resizing|No|Yes|Yes|
|Casting needed|No|Yes|No|
|Recommended|Sometimes|❌ No|✅ Yes|

---

