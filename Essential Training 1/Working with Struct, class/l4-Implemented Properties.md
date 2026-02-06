
# 🔷 1️⃣ Auto-Implemented Properties (Basic Form)

Most common pattern:

```csharp
public string FirstName { get; set; }
```

This means:

- `get` → anyone can read
    
- `set` → anyone can modify
    

Fully mutable 🔓

---

# 🔷 2️⃣ `init` Only Properties (C# 9+)

```csharp
public byte CustomerLevel { get; init; }
```

👉 `init` means:

- Can be set **only during object initialization**
    
- After object is created → cannot modify
    

This helps create **immutable objects**

---

# 🔥 Example 1 — Using `init`

```csharp
public record PremiereCustomer
{
    public string FirstName { get; set; }
    public byte CustomerLevel { get; init; }
}
```

---

### ✅ Correct Usage (During Initialization)

```csharp
PremiereCustomer pc = new PremiereCustomer
{
    FirstName = "New Customer",
    CustomerLevel = 2
};

Console.WriteLine($"{pc.FirstName} has level {pc.CustomerLevel}");
```

### ✅ Output:

```
New Customer has level 2
```

---

### ❌ Wrong Usage (After Initialization)

```csharp
pc.CustomerLevel = 3;   // Compiler error
```

Error:

> Init-only property can only be assigned in object initializer or constructor

---

# 🔷 3️⃣ Alternative: Setting `init` via Constructor

You can also set `init` inside constructor.

```csharp
public record PremiereCustomer
{
    public string FirstName { get; set; }
    public byte CustomerLevel { get; init; }

    public PremiereCustomer(byte level)
    {
        CustomerLevel = level;
    }
}
```

Usage:

```csharp
PremiereCustomer pc = new PremiereCustomer(2)
{
    FirstName = "New Customer"
};
```

✔ Works perfectly.

---

# 🔷 4️⃣ Why `init` is Useful?

It helps enforce:

- Immutable state
    
- Safer objects
    
- Better for multi-threading
    
- Better for DTOs
    

Very common in microservices architecture.

---

# 🔷 5️⃣ `private set` (Controlled Mutation)

Another option:

```csharp
public int NumberOfDirectReports { get; private set; }
```

This means:

- Anyone can read
    
- Only class itself can modify
    

---

# 🔥 Example 2 — Private Set

```csharp
public class Manager
{
    public string FirstName { get; set; }
    public int NumberOfDirectReports { get; private set; }

    public Manager(string name)
    {
        FirstName = name;
    }

    public void SetReports(int number)
    {
        NumberOfDirectReports = number;
    }
}
```

---

### Usage:

```csharp
Manager m = new Manager("Boss");

// ❌ Not allowed
// m.NumberOfDirectReports = 7;

m.SetReports(7);

Console.WriteLine($"{m.FirstName} manages {m.NumberOfDirectReports} people");
```

---

### ✅ Output:

```
Boss manages 7 people
```

---

# 🔷 6️⃣ Difference Between `set`, `private set`, and `init`

|Type|Can modify outside class?|When allowed?|
|---|---|---|
|`set`|✅ Yes|Anytime|
|`private set`|❌ No|Only inside class|
|`init`|❌ After creation|Only during initialization|

---

# 🔷 7️⃣ Important Concept: Order of Initialization

When using object initializer:

```csharp
var obj = new MyClass { Prop = value };
```

Execution order:

1️⃣ Default constructor runs  
2️⃣ Properties assigned

So constructor happens first.

---

# 🔷 8️⃣ Real Interview-Level Summary

If interviewer asks:

### 🔹 What is `init`?

You say:

> `init` allows a property to be set only during object initialization or inside a constructor. After the object is created, the property becomes read-only.

---

### 🔹 Difference between private set and init?

You say:

> `private set` allows modification only inside the class at any time, while `init` allows modification only during initialization.

🔥 That’s a strong answer.

---

# 🧠 Let’s Test Your Understanding

If I write:

```csharp
public class Test
{
    public int Value { get; init; }
}
```

And in Main:

```csharp
Test t = new Test();
t.Value = 5;
```

