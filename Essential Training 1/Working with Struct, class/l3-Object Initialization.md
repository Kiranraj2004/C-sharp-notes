
---

# 🔷 1️⃣ Why Object Initialization?

Problem:
If a class has many properties:

- FirstName
- LastName
- EmployeeId
- Age
- StartDate
- ShiftStartTime

Creating 10–15 constructors becomes messy 😵‍💫

Instead of:

```csharp
new Employee("Matt", "Milner", 75, 30, someDate, someTime)
```

We can use **Object Initializer Syntax**.

---

# 🔷 2️⃣ What is Object Initialization?

It allows you to:

- Create object
- Set properties
- In one block
- Using `{ }` instead of constructor parameters

---

# 🔷 3️⃣ Basic Example (Class)

### Employee class

```csharp
public class Employee
{
    public string FirstName { get; set; }
    public string LastName { get; set; }
    public int EmployeeId { get; set; }
    public int Age { get; set; }

    public Employee()
    {
        EmployeeId = 5; // default value
    }
}
```

---

### 🔥 Using Object Initializer

```csharp
Employee e = new Employee
{
    FirstName = "Matt",
    LastName = "Milner",
    Age = 30
};

Console.WriteLine($"{e.FirstName} ID {e.EmployeeId}");
```

---

### ✅ Output:

```
Matt ID 5
```

---

# 🔎 What Happened Internally?

When you write:

```csharp
new Employee { FirstName = "Matt" }
```

C# does:

1️⃣ Calls default constructor  
2️⃣ Then sets properties one by one  

Equivalent to:

```csharp
Employee e = new Employee();
e.FirstName = "Matt";
e.LastName = "Milner";
e.Age = 30;
```

Just cleaner syntax ✨

---

# 🔷 4️⃣ Important Rule

Object initializer **requires default constructor**.

If you only have:

```csharp
public Employee(string firstName)
```

Then this will ❌ fail:

```csharp
new Employee { FirstName = "Matt" }
```

Because default constructor does not exist.

---

# 🔷 5️⃣ Mixing Constructor + Object Initialization

You can combine both.

```csharp
public Employee(string firstName, string lastName, int id)
{
    FirstName = firstName;
    LastName = lastName;
    EmployeeId = id;
}
```

Now:

```csharp
Employee e = new Employee("Matt", "Milner", 75)
{
    Age = 30
};

Console.WriteLine($"{e.FirstName} {e.EmployeeId} {e.Age}");
```

---

### ✅ Output:

```
Matt 75 30
```

✔ Constructor sets required values  
✔ Object initializer sets optional values  

Very clean pattern 💯

---

# 🔷 6️⃣ Struct + Object Initialization (Value Type)

Now this is important 👇

Struct is value type.

If you define custom constructor in struct:

```csharp
public struct Age
{
    public DateTime BirthDate { get; set; }
    public int YearsOld { get; set; }

    public Age(DateTime dob, int years)
    {
        BirthDate = dob;
        YearsOld = years;
    }
}
```

You must initialize all fields.

---

### 🔥 Using Struct

```csharp
Age a = new Age(new DateTime(2000, 1, 1), 25);

Console.WriteLine(a.YearsOld);
```

### ✅ Output:
```
25
```

---

# 🔷 7️⃣ Object Initialization with Struct

```csharp
Age a = new Age
{
    BirthDate = new DateTime(2000, 1, 1),
    YearsOld = 25
};

Console.WriteLine(a.YearsOld);
```

### ✅ Output:
```
25
```

---

# 🔷 8️⃣ Record + Object Initialization

Records also support object initialization.

```csharp
public record Customer
{
    public string FirstName { get; set; }
    public string LastName { get; set; }

    public Customer()
    {
        FirstName = "Default";
    }
}
```

---

### Usage:

```csharp
Customer c = new Customer
{
    LastName = "Raj"
};

Console.WriteLine($"{c.FirstName} {c.LastName}");
```

### ✅ Output:
```
Default Raj
```

---

# 🔷 9️⃣ Important Rule for Derived Classes

If you remove default constructor from base class:

```csharp
public record Customer(string FirstName);
```

And create:

```csharp
public record PremiumCustomer : Customer
{
}
```

❌ Error!

Because derived class needs base default constructor.

So you must define constructor in derived class:

```csharp
public record PremiumCustomer(string FirstName)
    : Customer(FirstName);
```

---

# 🔷 🔟 Clean Interview Summary

If interviewer asks:

### 🔹 What is Object Initialization?

You say:

> Object initialization allows us to create an object and set its properties in a single expression using curly braces. It requires a parameterless constructor and internally calls the default constructor before assigning properties.

---

### 🔹 Can we mix constructor and object initializer?

> Yes. Constructor initializes required properties, and object initializer sets optional properties.

---

# 🔷 🔥 Real Interview Example

Question:

Why prefer object initializer over large constructor?

Answer:

> It improves readability and avoids creating multiple overloaded constructors. It also makes object creation cleaner when there are many optional properties.

---

# 🧠 Let Me Test Your Understanding

If I write:

```csharp
Employee e = new Employee
{
    FirstName = "Kiran"
};
```

And default constructor sets:

```csharp
EmployeeId = 100;
FirstName = "Default";
```

