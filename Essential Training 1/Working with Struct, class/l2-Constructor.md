
# 🔷 1️⃣ What is a Constructor?

A **constructor** is a special method:

- Same name as class
    
- No return type
    
- Runs automatically when object is created
    
- Used to initialize object state
    

---

# 🔷 2️⃣ Basic Constructor Example

```csharp
public class Employee
{
    public string FirstName { get; set; }
    public string LastName { get; set; }

    public Employee(string firstName, string lastName)
    {
        FirstName = firstName;
        LastName = lastName;
    }
}
```

### 🔥 Using it:

```csharp
Employee e = new Employee("Kiran", "Raj");
Console.WriteLine(e.FirstName);
```

### ✅ Output:

```
Kiran
```

---

# 🔷 3️⃣ Important Rule: Default Constructor

⚠️ Very Important:

If you define **any custom constructor**, C# does NOT automatically create a default constructor.

So this will ❌ fail:

```csharp
Employee e = new Employee();   // Error!
```

Because we created:

```csharp
public Employee(string firstName, string lastName)
```

👉 Now there is NO empty constructor.

---

# 🔷 4️⃣ Fixing Default Constructor

If you want both:

```csharp
public Employee()   // Default constructor
{
}

public Employee(string firstName, string lastName)
{
    FirstName = firstName;
    LastName = lastName;
}
```

Now both work.

---

# 🔷 5️⃣ Constructor + Inheritance Problem

Now suppose:

```csharp
public class Manager : Employee
{
}
```

If Employee only has:

```csharp
public Employee(string firstName, string lastName)
```

Then this will give ❌ error.

Why?

Because when creating a Manager, C# must first create the base Employee part.

But Employee needs parameters.

---

# 🔷 6️⃣ Solution: Use base() Constructor

```csharp
public class Manager : Employee
{
    public Manager(string firstName, string lastName)
        : base(firstName, lastName)
    {
    }
}
```

👉 `base()` calls parent constructor.

---

# 🔥 Full Working Example

```csharp
using System;

public class Employee
{
    public string FirstName { get; set; }
    public string LastName { get; set; }

    public Employee(string firstName, string lastName)
    {
        FirstName = firstName;
        LastName = lastName;
    }
}

public class Manager : Employee
{
    public Manager(string firstName, string lastName)
        : base(firstName, lastName)
    {
    }
}

class Program
{
    static void Main()
    {
        Employee e = new Manager("Kiran", "Raj");
        Console.WriteLine(e.FirstName + " " + e.LastName);
    }
}
```

### ✅ Output:

```
Kiran Raj
```

---

# 🔷 7️⃣ Polymorphism Behavior

Notice this:

```csharp
Employee e = new Manager("Kiran", "Raj");
```

Variable type = Employee  
Object type = Manager

So you can access only Employee properties.

---

# 🔷 8️⃣ Initializing Extra Values in Constructor

Inside constructor you can also set other values.

```csharp
public int Id { get; set; }

public Employee(string firstName, string lastName)
{
    FirstName = firstName;
    LastName = lastName;

    Random rand = new Random();
    Id = rand.Next(1, 10);
}
```

---

# 🔷 9️⃣ Optional Parameters in Constructor

You can give default value:

```csharp
public Employee(string firstName, string lastName, int id = 0)
{
    FirstName = firstName;
    LastName = lastName;
    Id = id;
}
```

Now both work:

```csharp
Employee e1 = new Employee("Kiran", "Raj");
Employee e2 = new Employee("Kiran", "Raj", 5);
```

---

# 🔥 Output Example

```csharp
class Program
{
    static void Main()
    {
        Employee e1 = new Employee("Kiran", "Raj");
        Employee e2 = new Employee("John", "Doe", 7);

        Console.WriteLine(e1.Id);
        Console.WriteLine(e2.Id);
    }
}
```

### ✅ Output:

```
0
7
```

---

# 🔷 1️⃣0️⃣ Important Rule About Optional Parameters

This is ❌ NOT allowed:

```csharp
public Employee(string firstName, string lastName, int id = new Random().Next(1,10))
```

### Why?

Default parameter must be a **compile-time constant**.

✔ Allowed:

```
int id = 0
int id = 5
string name = "Test"
```

❌ Not allowed:

```
new Random()
DateTime.Now
Method calls
```

---

# 🔷 1️⃣1️⃣ Clean Interview Notes (Short Version)

If interviewer asks:

### 🔹 What happens if you define a constructor?

> If we define any custom constructor, the compiler will not generate the default constructor automatically.

---

### 🔹 How do you call base class constructor?

> By using the `base()` keyword inside the derived class constructor.

---

### 🔹 What are optional parameters?

> Optional parameters allow us to assign default values to constructor parameters, but the default value must be a compile-time constant.

---

# 🔷 1️⃣2️⃣ Real Understanding Question For You 😎

If I write:

```csharp
public Manager() : base("Default", "Manager")
{
}
```

What happens when I create:

```csharp
Manager m = new Manager();
```

