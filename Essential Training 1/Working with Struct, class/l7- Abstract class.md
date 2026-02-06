
# 🔷 1️⃣ What is an Abstract Class?

An abstract class:

- ❌ Cannot be instantiated
    
- ✅ Can contain implementation
    
- ✅ Can contain abstract members (no implementation)
    
- ✅ Used as base class
    
- Forces derived classes to implement certain behavior
    

---

# 🔷 2️⃣ Example: Interface

```csharp
public interface IPerson
{
    string FirstName { get; set; }
    string LastName { get; set; }
}
```

---

# 🔷 3️⃣ Abstract Base Class

```csharp
public abstract class Employee : IPerson
{
    public string FirstName { get; set; }
    public string LastName { get; set; }

    public DateTime StartDate { get; set; }

    // Abstract Property
    public abstract int EmployeeId { get; }

    // Abstract Method
    public abstract void ProcessPayroll();

    // Virtual Method (has default implementation)
    public virtual void Terminate()
    {
        Console.WriteLine("Employee terminated.");
    }

    // Normal Method
    public bool IsActive()
    {
        return true;
    }
}
```

---

# 🔷 4️⃣ Key Concepts

### ✅ Abstract Member

- No implementation
    
- MUST be implemented in derived class
    
- Uses `abstract` keyword
    

### ✅ Virtual Member

- Has default implementation
    
- Derived class MAY override it
    
- Uses `virtual` keyword
    

### ✅ Normal Member

- Has implementation
    
- Cannot override (unless marked virtual)
    
- Can hide using `new`
    

---

# 🔷 5️⃣ Derived Class Example

```csharp
public class ShiftWorker : Employee
{
    public TimeSpan ShiftStartTime { get; set; }

    // Must override abstract property
    public override int EmployeeId
    {
        get { return 1; }
    }

    // Must override abstract method
    public override void ProcessPayroll()
    {
        Console.WriteLine("Processing payroll for shift worker.");
    }

    // Optional override of virtual method (not overriding here)

    // Hiding normal method
    public new bool IsActive()
    {
        return false;
    }
}
```

---

# 🔷 6️⃣ Using It in Program

```csharp
class Program
{
    static void Main()
    {
        Employee emp = new ShiftWorker
        {
            FirstName = "John",
            LastName = "Doe",
            StartDate = DateTime.Now,
            ShiftStartTime = new TimeSpan(9, 0, 0)
        };

        emp.ProcessPayroll();
        emp.Terminate();
        Console.WriteLine("Is Active: " + emp.IsActive());
    }
}
```

---

# 🔷 7️⃣ Expected Output

```
Processing payroll for shift worker.
Employee terminated.
Is Active: True
```

---

# 🔷 8️⃣ Why IsActive Returned True?

Important concept 🔥

Notice:

```csharp
Employee emp = new ShiftWorker();
```

Variable type = Employee  
Object type = ShiftWorker

Since `IsActive()` was not virtual in base class,  
and derived used `new` instead of `override`,

The method called depends on variable type.

Because variable type is Employee → base version is called.

If we change:

```csharp
ShiftWorker emp = new ShiftWorker();
```

Now output becomes:

```
Is Active: False
```

🔥 That’s polymorphism behavior.

---

# 🔷 9️⃣ Summary Table

|Keyword|Must Implement?|Can Override?|Has Default Code?|
|---|---|---|---|
|abstract|YES|YES (must)|❌ No|
|virtual|NO|YES (optional)|✅ Yes|
|normal|NO|❌ No|✅ Yes|
|new|No|Hides base version|✅ Yes|

---

# 🔷 🔟 Why Use Abstract Class?

Use abstract class when:

- You want shared logic
    
- You want to force certain behavior
    
- You want partial implementation
    

---

# 🔷 1️⃣1️⃣ Interview-Level Explanation

If interviewer asks:

### 🔹 Difference between interface and abstract class?

You say:

> An abstract class can contain both implemented and abstract members and supports constructors and fields. An interface only defines a contract and cannot contain implementation (before C# 8 default methods).

That’s a strong answer.

---

# 🔷 1️⃣2️⃣ Important Polymorphism Rule

Method resolution depends on:

- If method is virtual → runtime binding
    
- If method is new → compile-time binding
    

---

# 🧠 Let Me Test You (Interview Mode)

If I change `IsActive()` in base class to:

```csharp
public virtual bool IsActive()
{
    return true;
}
```

And in derived:

```csharp
public override bool IsActive()
{
    return false;
}
```

Now if I write:

```csharp
Employee emp = new ShiftWorker();
Console.WriteLine(emp.IsActive());
```
