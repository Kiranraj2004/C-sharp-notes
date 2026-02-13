
This topic solves an important problem:

> ❓ What happens if two interfaces have methods with the same name?

C# solves this using **Explicit Interface Implementation**.

Let’s understand it clearly step by step.

---

# 🔹 1️⃣ The Problem: Method Name Collision

Suppose we have two interfaces:

```csharp
interface Intf1
{
    void SomeMethod();
}

interface Intf2
{
    void SomeMethod();
}
```

Both define:

```
void SomeMethod();
```

Now we create a class:

```csharp
class InterfaceTest : Intf1, Intf2
{
}
```

Now the class must implement `SomeMethod()` for BOTH interfaces.

But how?

If we just write:

```csharp
public void SomeMethod()
{
    Console.WriteLine("Class version");
}
```

This creates only ONE version.

It does NOT separate Intf1 and Intf2.

---

# 🔥 2️⃣ The Solution: Explicit Interface Implementation

To differentiate them, we write:

```csharp
class InterfaceTest : Intf1, Intf2
{
    public void SomeMethod()
    {
        Console.WriteLine("Class version of SomeMethod");
    }

    void Intf1.SomeMethod()
    {
        Console.WriteLine("Intf1 version of SomeMethod");
    }

    void Intf2.SomeMethod()
    {
        Console.WriteLine("Intf2 version of SomeMethod");
    }
}
```

Notice:

```
void Intf1.SomeMethod()
```

We prefix method name with interface name.

This is called:

> Explicit Interface Implementation

---

# 🔹 Important Rule

Explicit interface methods:

- ❌ Cannot have access modifiers (no public/private)
    
- ❌ Cannot be called directly using class object
    
- ✅ Can only be called through interface reference
    

---

# 🔹 3️⃣ Calling the Methods

```csharp
class Program
{
    static void Main()
    {
        InterfaceTest test = new InterfaceTest();

        // Class version
        test.SomeMethod();

        // Intf1 version
        Intf1 i1 = test;
        i1.SomeMethod();

        // Intf2 version
        Intf2 i2 = test;
        i2.SomeMethod();
    }
}
```

---

# ✅ Output:

```
Class version of SomeMethod
Intf1 version of SomeMethod
Intf2 version of SomeMethod
```

---

# 🔥 Why This Works

Because:

- `test.SomeMethod()` → calls class version
    
- `i1.SomeMethod()` → calls Intf1 version
    
- `i2.SomeMethod()` → calls Intf2 version
    

The interface reference controls which implementation runs.

---

# 🔹 Why Do We Need This?

Imagine two interfaces:

- ILogger → Log()
    
- IFileWriter → Log()
    

They both define `Log()`, but behavior should be different.

Explicit implementation avoids conflict.

---

# 🔹 What Happens If You Try This?

```csharp
test.Intf1.SomeMethod();  // ❌ ERROR
```

Not allowed.

You must cast or assign to interface.

---

# 🔥 Shorter Version Using Casting

Instead of:

```csharp
Intf1 i1 = test;
//same
Intf1 il=test as Intf1;
```

You can write:

```csharp
((Intf1)test).SomeMethod();
((Intf2)test).SomeMethod();
```

---

# 🔹 Why Not Just Use One Public Method?

If you use only:

```csharp
public void SomeMethod()
```

Then both interfaces will use the same implementation.

But sometimes you need:

- Different behavior per interface
    
- Complete separation
    

That’s why explicit implementation exists.

---

# 🔥 Summary

### Normal Implementation

```csharp
public void SomeMethod()
```

- Accessible through class
    
- Same for all interfaces
    

---

### Explicit Implementation

```csharp
void Intf1.SomeMethod()
```

- Only accessible via interface reference
    
- Used to resolve name conflicts
    
- Keeps implementations separate
    

---

# 🎯 Final Concept Clarity

|Call Type|Which Method Executes|
|---|---|
|test.SomeMethod()|Class version|
|(Intf1)test.SomeMethod()|Intf1 version|
|(Intf2)test.SomeMethod()|Intf2 version|

---

