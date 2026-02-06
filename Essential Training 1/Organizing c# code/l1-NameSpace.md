
We’ll cover:

1. ✅ What is a Namespace?
    
2. ✅ Two ways to declare namespace (Old vs C# 10 style)
    
3. ✅ What is `using`?
    
4. ✅ Fully Qualified Name
    
5. ✅ Default namespaces in .NET 6
    
6. ✅ Why namespaces are important
    
7. ✅ Example code + output
    

---

# 🔹 1. What is a Namespace?

👉 A **namespace** is a container that organizes related classes, interfaces, enums, etc.

Think of it like:

- 📁 Folder = Namespace
    
- 📄 File/Class inside folder = Type
    

It helps avoid name conflicts.

Example:  
You might have:

- `MyApp.Models.Employee`
    
- `MyApp.HR.Employee`
    

Both classes are named `Employee`, but different namespaces keep them separate.

---

# 🔹 2. Two Ways to Declare Namespace

## ✅ 1️⃣ Traditional Way (Before C# 10)

```csharp
namespace LinkedIn.Essentials
{
    public class Constants
    {
        public const string DbString = "Database Connected";
    }
}
```

Here:

- The class is wrapped inside `{ }`
    
- This was the standard way before C# 10
    

---

## ✅ 2️⃣ New Way (C# 10 and above)

```csharp
namespace LinkedIn.Essentials;

public class Constants
{
    public const string DbString = "Database Connected";
}
```

✨ Difference:

- No curly braces
    
- Just a semicolon `;`
    
- Cleaner and shorter
    
- Mostly used because usually one file = one class
    

---

# 🔹 3. What is `using`?

If you want to use a class from another namespace, you must:

Either:

### ✅ Option 1: Use `using`

```csharp
using LinkedIn.Essentials;

Console.WriteLine(Constants.DbString);
```

This brings the namespace into scope.

---

### ❌ If you remove `using`

```csharp
Console.WriteLine(Constants.DbString);
```

You get error:

```
The name 'Constants' does not exist in the current context
```

Because it is not in scope.

---

# 🔹 4. Fully Qualified Name

Instead of using `using`, you can write:

```csharp
Console.WriteLine(LinkedIn.Essentials.Constants.DbString);
```

Here:

```
LinkedIn.Essentials.Constants
```

is the **fully qualified name**

👉 Structure:

```
NamespaceName.ClassName
```

---

# 🔹 5. Example with System Namespace

`Console` belongs to:

```
System namespace
```

Normally we write:

```csharp
using System;

Console.WriteLine("Hello");
```

But without using:

```csharp
System.Console.WriteLine("Hello");
```

Both work ✅

---

# 🔹 6. Default Namespaces in .NET 6

In .NET 6 (C# 10), some namespaces are automatically included.

That’s why in new console apps, you may not see:

```csharp
using System;
```

But `Console` still works.

This is because of **Implicit Global Usings**.

---

# 🔹 7. Why Namespaces Are Important

Without namespaces:

If two libraries have:

```csharp
public class Employee { }
```

It would clash ❌

With namespaces:

```
CompanyA.Employee
CompanyB.Employee
```

No conflict ✅

---

# 🔹 8. Full Working Example (Simple Project)

---

## 📁 Constants.cs

```csharp
namespace LinkedIn.Essentials;

public class Constants
{
    public const string DbString = "Database Connected Successfully";
}
```

---

## 📁 Program.cs (Using `using`)

```csharp
using LinkedIn.Essentials;

class Program
{
    static void Main()
    {
        Console.WriteLine(Constants.DbString);
    }
}
```

---

## ✅ Output:

```
Database Connected Successfully
```

---

## 📁 Program.cs (Without using — Fully Qualified)

```csharp
class Program
{
    static void Main()
    {
        Console.WriteLine(LinkedIn.Essentials.Constants.DbString);
    }
}
```

---

## ✅ Output:

```
Database Connected Successfully
```

Same output. Just different way.

---

# 🔥 Interview Summary Notes (Quick Revision)

- Namespace = logical grouping of types
    
- Avoids naming conflicts
    
- All .NET types belong to some namespace
    
- Two styles:
    
    - Old: `{ }` wrapping
        
    - New (C# 10): `namespace Name;`
        
- To use types:
    
    - Either `using NamespaceName`
        
    - Or use fully qualified name
        
- .NET 6 includes implicit global usings
    

---

