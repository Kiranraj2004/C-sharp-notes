

- ✅ Class
    
- ✅ Struct
    
- ✅ Record
    
- ✅ Record Struct
    
- ✅ Inheritance rules
    
- ✅ Reference vs Value type behavior
    
- ✅ Example code + Output
    

---

# 🔷 1️⃣ Interface (IPerson)

An **interface** defines a contract.

```csharp
public interface IPerson
{
    string FirstName { get; set; }
    string LastName { get; set; }
    int Id { get; set; }
    int Age { get; set; }
}
```

👉 Any class/struct/record implementing this **must define these properties**.

---

# 🔷 2️⃣ Class (Reference Type)

### ✅ What is a Class?

- Reference type
    
- Stored in **Heap**
    
- Supports inheritance
    
- Can implement multiple interfaces
    
- Most commonly used type in C#
    

---

### Example:

```csharp
public class Employee : IPerson
{
    public string FirstName { get; set; }
    public string LastName { get; set; }
    public int Id { get; set; }
    public int Age { get; set; }

    public string Department { get; set; }
}
```

### Inheritance Example:

```csharp
public class Manager : Employee
{
    public int TeamSize { get; set; }
}
```

✔ Can inherit from **one base class**  
✔ Can implement **multiple interfaces**

---

### 🔥 Reference Type Behavior Example

```csharp
Employee emp1 = new Employee();
emp1.FirstName = "Kiran";

Employee emp2 = emp1;
emp2.FirstName = "Raj";

Console.WriteLine(emp1.FirstName);
```

### ✅ Output:

```
Raj
```

👉 Why?

Because `emp1` and `emp2` point to the **same object in memory**.

---

# 🔷 3️⃣ Struct (Value Type)

### ✅ What is Struct?

- Value type
    
- Stored in **Stack**
    
- Cannot inherit from another struct
    
- Can implement interfaces
    
- Copies value when assigned
    

---

### Example:

```csharp
public struct Age
{
    public int YearsOld { get; set; }
}
```

---

### 🔥 Value Type Behavior Example

```csharp
Age age1 = new Age();
age1.YearsOld = 20;

Age age2 = age1;
age2.YearsOld = 25;

Console.WriteLine(age1.YearsOld);
```

### ✅ Output:

```
20
```

👉 Why?

Because struct copies the value.  
`age1` and `age2` are separate copies.

---

# 🔷 4️⃣ Record (C# 9+) – Reference Type

### ✅ What is Record?

- Reference type (by default)
    
- Mainly used for **immutable data**
    
- Best for DTOs / data transfer between layers
    
- Has built-in value equality
    

---

### Example:

```csharp
public record Customer(string FirstName, string LastName, int Id);
```

### Usage:

```csharp
var c1 = new Customer("Kiran", "Raj", 1);
var c2 = new Customer("Kiran", "Raj", 1);

Console.WriteLine(c1 == c2);
```

### ✅ Output:

```
True
```

👉 Why?

Because records compare **values**, not memory addresses.

---

### 🔥 Compare with Class

```csharp
public class Person
{
    public string Name { get; set; }
}

Person p1 = new Person { Name = "Kiran" };
Person p2 = new Person { Name = "Kiran" };

Console.WriteLine(p1 == p2);
```

### ✅ Output:

```
False
```

👉 Class checks reference equality by default.

---

# 🔷 5️⃣ Record Struct (C# 10+)

### ✅ What is Record Struct?

- Value type
    
- Has record features
    
- Combines struct + record benefits
    

---

### Example:

```csharp
public record struct Order(int OrderId, DateTime OrderDate);
```

---

### Value Behavior Example:

```csharp
var o1 = new Order(1, DateTime.Now);
var o2 = o1;

o2.OrderId = 2;

Console.WriteLine(o1.OrderId);
```

### ✅ Output:

```
1
```

👉 Because it's a value type.

---

# 🔷 6️⃣ Important Inheritance Rules

|Type|Can Inherit Class?|Can Implement Interface?|Type|
|---|---|---|---|
|Class|✅ Yes (1 base class)|✅ Yes|Reference|
|Struct|❌ No|✅ Yes|Value|
|Record|✅ Yes|✅ Yes|Reference|
|Record Struct|❌ No|✅ Yes|Value|

---

# 🔷 7️⃣ Nullable Warning (C# 8+ Feature)

In .NET 6, if you write:

```csharp
public string FirstName { get; set; }
```

You may get warning:

> Non-nullable property must contain a non-null value

Because C# now enforces **nullable reference types**.

You can disable in `.csproj`:

```xml
<Nullable>disable</Nullable>
```

But better practice is:

```csharp
public string FirstName { get; set; } = string.Empty;
```

---

# 🔷 8️⃣ When To Use What?

### 🔹 Use Class When:

- You need inheritance
    
- Complex behavior
    
- Mutable object
    
- Most general cases
    

### 🔹 Use Struct When:

- Small data structure
    
- Lightweight
    
- Performance critical
    
- Like `Point`, `Date`, `Coordinates`
    

### 🔹 Use Record When:

- Immutable data
    
- DTOs
    
- Microservices
    
- Comparing values
    

### 🔹 Use Record Struct When:

- Small immutable data
    
- Want value-type behavior
    
- High-performance scenarios
    

---

