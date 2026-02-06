
# ✅ 1️⃣ Core Concept: Variable Type vs Object Type

In C# (and most OOP languages):

```csharp
Employee e = new ShiftWorker();
```

- **Object type** → `ShiftWorker`
    
- **Variable type (reference type)** → `Employee`
    

👉 The compiler only allows access to members defined in the **variable type**.

Even if the object is actually a `ShiftWorker`, the compiler only checks what `Employee` contains.

---

# ✅ 2️⃣ Example Class Structure

Let’s assume this structure:

```csharp
public interface IPerson
{
    string FirstName { get; set; }
    string LastName { get; set; }
}

public class Employee : IPerson
{
    public string FirstName { get; set; }
    public string LastName { get; set; }
    public DateTime StartDate { get; set; }
    public DateTime EndDate { get; set; }
}

public class ShiftWorker : Employee
{
    public TimeOnly ShiftStartTime { get; set; }
}
```

---

# ✅ 3️⃣ Case 1 — Variable Type = Employee

```csharp
Employee e = new ShiftWorker();

e.FirstName = "Kiran";
e.StartDate = DateTime.Now;

// ❌ ERROR
e.ShiftStartTime = new TimeOnly(8, 30);
```

### ❓ Why Error?

Because `ShiftStartTime` exists in `ShiftWorker`,  
but `e` is declared as `Employee`.

Compiler thinks:

> "I only know this is an Employee. Employee doesn't have ShiftStartTime."

---

# ✅ 4️⃣ Case 2 — Variable Type = ShiftWorker

```csharp
ShiftWorker e = new ShiftWorker();

e.FirstName = "Kiran";
e.ShiftStartTime = new TimeOnly(8, 30);
```

✔ Now everything works  
because the variable type includes that property.

---

# ✅ 5️⃣ Case 3 — Variable Type = Interface (IPerson)

```csharp
IPerson e = new ShiftWorker();

e.FirstName = "Kiran";

// ❌ ERROR
e.ShiftStartTime = new TimeOnly(8, 30);
```

Why?

Because `IPerson` only defines:

```csharp
FirstName
LastName
```

So compiler says:

> "I only know this is a person. I don't know anything about shifts."

---

# ✅ 6️⃣ Accessing Child Properties Using Casting

If you're 100% sure the object is actually a `ShiftWorker`, you can cast it.

```csharp
IPerson e = new ShiftWorker();

((ShiftWorker)e).ShiftStartTime = new TimeOnly(8, 30);
```

Now it works because you're telling the compiler:

> "Trust me, this object is a ShiftWorker."

---

# ✅ 7️⃣ Safer Casting (Recommended)

Instead of direct casting, use:

```csharp
IPerson e = new ShiftWorker();

if (e is ShiftWorker sw)
{
    sw.ShiftStartTime = new TimeOnly(8, 30);
}
```

✔ This avoids runtime errors.

---

# ✅ 8️⃣ Full Working Example with Output

```csharp
using System;

public interface IPerson
{
    string FirstName { get; set; }
    string LastName { get; set; }
}

public class Employee : IPerson
{
    public string FirstName { get; set; }
    public string LastName { get; set; }
    public DateTime StartDate { get; set; }
}

public class ShiftWorker : Employee
{
    public TimeOnly ShiftStartTime { get; set; }
}

class Program
{
    static void Main()
    {
        Employee e = new ShiftWorker();

        e.FirstName = "Kiran";
        e.StartDate = DateTime.Today;

        Console.WriteLine($"Name: {e.FirstName}");

        // Cast to access ShiftStartTime
        ShiftWorker sw = (ShiftWorker)e;
        sw.ShiftStartTime = new TimeOnly(8, 30);

        Console.WriteLine($"Shift starts at: {sw.ShiftStartTime}");
    }
}
```

---

# ✅ Output

```
Name: Kiran
Shift starts at: 08:30
```

---

# 🎯 Key Takeaways (Very Important for Interviews)

1. The **type of the variable** determines what members are accessible.
    
2. The **actual object type** determines what exists in memory.
    
3. Compiler checks based on variable type.
    
4. Casting allows access to derived members.
    
5. Interfaces restrict accessible members to only what's defined in them.
    
6. This concept is called **Polymorphism**.
    

---

# 🔥 One-Line Golden Rule

> The compiler only sees the declared type of the variable, not the actual object type.

---

