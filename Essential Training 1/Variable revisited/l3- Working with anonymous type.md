
# ✅ 1️⃣ What Is an Anonymous Type?

An anonymous type is:

> An object created without explicitly defining a class.

Example:

```csharp
var e = new
{
    FirstName = "Matt",
    LastName = "Milner"
};
```

Notice something?

❗ There is **no class name**.

We didn’t write:

```csharp
class Person { ... }
```

But still, C# creates a type behind the scenes.

That hidden type contains:

```
string FirstName
string LastName
```

---

# ✅ 2️⃣ Why `var` Is Required

This will NOT work:

```csharp
Person e = new { FirstName = "Matt" }; // ❌ ERROR
```

Because:

👉 The type has no name.

So we must write:

```csharp
var e = new { FirstName = "Matt" };
```

`var` allows compiler to generate the hidden type.

---

# ✅ 3️⃣ Anonymous Type Properties Are Read-Only

This will fail:

```csharp
var e = new
{
    FirstName = "Matt"
};

e.FirstName = "John";   // ❌ ERROR
```

Anonymous type properties are:

✔ Public  
✔ Read-only  
❌ Cannot modify after creation

---

# ✅ 4️⃣ Accessing Properties

You can access them normally:

```csharp
var e = new
{
    FirstName = "Matt",
    LastName = "Milner"
};

Console.WriteLine(e.FirstName);
Console.WriteLine(e.LastName);
```

### ✅ Output

```
Matt
Milner
```

---

# ✅ 5️⃣ Anonymous Types Cannot Be Cast

If you previously had:

```csharp
ShiftWorker e = new ShiftWorker();
```

You cannot do:

```csharp
ShiftWorker sw = (ShiftWorker)e; // ❌ ERROR
```

Because:

👉 Anonymous type is NOT ShiftWorker.  
👉 It’s a completely separate hidden type.

---

# ✅ 6️⃣ Adding Arrays Inside Anonymous Types

You can make them more complex.

```csharp
var person = new
{
    FirstName = "Matt",
    LastName = "Milner",
    Kids = new string[] { "Anna", "Ben" }
};

Console.WriteLine(person.Kids[0]);
Console.WriteLine(person.Kids[1]);
```

### ✅ Output

```
Anna
Ben
```

So yes — they can contain arrays.

---

# ✅ 7️⃣ Nested Anonymous Types (Hierarchy)

You can even nest objects inside.

```csharp
var person = new
{
    FirstName = "Matt",
    LastName = "Milner",
    Address = new
    {
        City = "London",
        Country = "UK"
    }
};

Console.WriteLine(person.Address.City);
```

### ✅ Output

```
London
```

So anonymous types can form full hierarchies.

---

# ✅ 8️⃣ Real-World Usage (Very Important)

Anonymous types are heavily used in:

### 🔹 LINQ Projections

Example:

```csharp
var numbers = new List<int> { 1, 2, 3, 4 };

var result = numbers.Select(n => new
{
    Number = n,
    Square = n * n
});

foreach (var item in result)
{
    Console.WriteLine($"{item.Number} -> {item.Square}");
}
```

### ✅ Output

```
1 -> 1
2 -> 4
3 -> 9
4 -> 16
```

Here we created a **new object type on the fly**.

No class needed.

---

# ✅ 9️⃣ Important Rules Summary

|Feature|Anonymous Type|
|---|---|
|Has class name?|❌ No|
|Requires `var`?|✅ Yes|
|Properties editable?|❌ No (read-only)|
|Can contain arrays?|✅ Yes|
|Can contain nested objects?|✅ Yes|
|Used in LINQ?|✅ Very common|

---

# 🎯 Interview-Level Explanation

Anonymous types:

- Created using `new { }` syntax
    
- Compiler generates a hidden sealed class
    
- Properties are read-only
    
- Scope-limited (usually method-level)
    
- Mainly used for projections in LINQ
    

---

# 🔥 Golden Rule

> Anonymous types are temporary, read-only objects created without defining a class.

---

If you want next, I can:

- Compare Anonymous Type vs Class
    
- Or Anonymous Type vs Tuple
    
- Or Explain how memory works behind the scenes
    
- Or Give you interview trap questions 😈
    

What level are we going next?