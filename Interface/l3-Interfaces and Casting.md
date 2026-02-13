
This topic explains:

1. ❌ Why we cannot create an interface object directly
    
2. ✅ How to check if an object implements an interface
    
3. 🔄 How to cast objects using `is` and `as`
    
4. 🎯 Why this is useful in real programs
    

---

# 🔹 1️⃣ You Cannot Instantiate an Interface

Interfaces are NOT classes.

So this is ❌ illegal:

```csharp
IStorable obj = new IStorable();  // ❌ ERROR
```

Why?

Because:

- Interface has no implementation
    
- It is just a contract
    
- There is no actual object to create
    

You must create a class that implements it.

---

# 🔹 2️⃣ The `is` Operator (Type Checking)

The `is` operator checks:

> "Is this object of this type (or derived type)?"

It returns **true or false**.

---

## Example with Classes

```csharp
class A { }
class B : A { }
class C : B { }

B obj = new B();

Console.WriteLine(obj is B); // true
Console.WriteLine(obj is A); // true
Console.WriteLine(obj is C); // false
```

---

### ✅ Output:

```
True
True
False
```

Why?

- `obj is B` → true (exact type)
    
- `obj is A` → true (B inherits from A)
    
- `obj is C` → false (B is not derived from C)
    

---

# 🔹 3️⃣ The `as` Operator (Safe Casting)

The `as` operator:

- Tries to cast object
    
- If success → returns object
    
- If fail → returns `null`
    
- Does NOT throw exception
    

---

Example:

```csharp
A a = obj as A;  // works
C c = obj as C;  // returns null
```

---

# 🔹 4️⃣ Using `is` and `as` with Interfaces

Now let’s use interface example.

---

## Step 1: Define Interface

```csharp
interface IStorable
{
    void Save();
    void Load();
}
```

---

## Step 2: Implement in Class

```csharp
class Document : IStorable
{
    public void Save()
    {
        Console.WriteLine("Saving document...");
    }

    public void Load()
    {
        Console.WriteLine("Loading document...");
    }
}
```

---

# 🔹 5️⃣ Using `is` Operator with Interface

```csharp
class Program
{
    static void Main()
    {
        Document d = new Document();

        if (d is IStorable)
        {
            d.Save();
        }
    }
}
```

---

### ✅ Output:

```
Saving document...
```

Explanation:

- `d` implements `IStorable`
    
- So condition is true
    
- Save() is called
    

---

# 🔹 6️⃣ Using `as` Operator with Interface

```csharp
class Program
{
    static void Main()
    {
        Document d = new Document();

        IStorable istor = d as IStorable;

        if (istor != null)
        {
            istor.Load();
        }
    }
}
```

---

### ✅ Output:

```
Loading document...
```

Explanation:

- `as` tries to cast `d` to `IStorable`
    
- It succeeds
    
- So `istor` is not null
    
- Load() is called
    

---

# 🔥 What If Cast Fails?

Let’s create another class:

```csharp
class Person
{
}
```

Now:

```csharp
Person p = new Person();

IStorable istor = p as IStorable;

if (istor == null)
{
    Console.WriteLine("Cast failed");
}
```

---

### ✅ Output:

```
Cast failed
```

Because:

- Person does NOT implement IStorable
    
- So `as` returns null
    

---

# 🔹 Difference Between `is` and `as`

|Operator|Purpose|Returns|
|---|---|---|
|`is`|Type check|true / false|
|`as`|Safe cast|Object or null|

---

# 🔥 Why Is This Useful?

Imagine you have a collection of mixed objects.

---

## Example: Collection with Mixed Types

```csharp
using System;
using System.Collections.Generic;

interface IStorable
{
    void Save();
}

class Document : IStorable
{
    public void Save()
    {
        Console.WriteLine("Saving document...");
    }
}

class Person
{
}

class Program
{
    static void Main()
    {
        List<object> items = new List<object>();

        items.Add(new Document());
        items.Add(new Person());

        foreach (object obj in items)
        {
            if (obj is IStorable storable)
            {
                storable.Save();
            }
        }
    }
}
```

---

### ✅ Output:

```
Saving document...
```

Explanation:

- Loop checks each object
    
- Only calls Save() if object implements IStorable
    
- Person is ignored
    

This is very powerful in real-world systems.

---

# 🔥 Modern C# (Pattern Matching)

Instead of:

```csharp
if (obj is IStorable)
```

You can write:

```csharp
if (obj is IStorable storable)
{
    storable.Save();
}
```

Cleaner and safer.

---

# 🧠 Key Takeaways

1. ❌ Cannot create interface instance directly.
    
2. ✅ `is` checks type.
    
3. ✅ `as` safely casts.
    
4. `as` returns null if cast fails.
    
5. Useful for collections and loose coupling.
    
6. Works with both classes and interfaces.
    

---

# 🚀 Final Summary (Interview Ready)

- Interfaces cannot be instantiated.
    
- Use `is` to test type.
    
- Use `as` to safely cast.
    
- Extremely useful in polymorphic systems.
    
- Helps write flexible, dynamic code.
    

---

