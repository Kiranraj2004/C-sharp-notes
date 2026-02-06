	
# 🔷 1️⃣ What is a Static Class?

A static class:

- ❌ Cannot create object (no instance)
    
- ❌ Cannot have instance members
    
- ✅ Only static members allowed
    
- ✅ Used for utility/helper logic
    
- ✅ Used for constants/config values
    

Example:

```csharp
public static class Constants
{
}
```

---

# 🔷 2️⃣ Why Use Static Class?

Because sometimes:

- You don’t need object state
    
- You just need helper methods
    
- Or shared configuration
    
- Or constant values
    

Example in real projects:

- Math helpers
    
- Configuration keys
    
- Logging utilities
    
- Extension methods
    

---

# 🔷 3️⃣ Static Class Cannot Be Instantiated

This is ❌ illegal:

```csharp
Constants c = new Constants();  // ERROR
```

Compiler error:

> Cannot create an instance of static class

---

# 🔷 4️⃣ Static Constructor

A static class can have a static constructor.

```csharp
public static class Constants
{
    public static string ConnectionString;

    static Constants()
    {
        ConnectionString = "Server=localhost;Database=TestDB;";
        Console.WriteLine("Static constructor executed");
    }
}
```

### Important:

- No access modifier (no public/private)
    
- Runs only once
    
- Runs when class is first accessed
    

---

# 🔥 Example Usage

```csharp
class Program
{
    static void Main()
    {
        Console.WriteLine(Constants.ConnectionString);
    }
}
```

---

### ✅ Output:

```
Static constructor executed
Server=localhost;Database=TestDB;
```

Notice:  
Constructor runs only once.

---

# 🔷 5️⃣ Static Fields

```csharp
public static class ConfigKeys
{
    public static string ServerName = "TargetServer";
}
```

Use like this:

```csharp
Console.WriteLine(ConfigKeys.ServerName);
```

No object needed.

---

# 🔷 6️⃣ readonly vs const (VERY Important)

### ✅ const

```csharp
public const string DatabaseName = "MyDatabase";
```

- Must be compile-time constant
    
- Replaced by compiler
    
- Cannot change ever
    
- Faster
    
- Dangerous if used in shared libraries (value gets embedded)
    

---

### ✅ static readonly

```csharp
public static readonly string ServerName = "ProdServer";
```

- Assigned at runtime
    
- Can be set in static constructor
    
- Safer for config-like values
    

---

### Interview Difference

|const|static readonly|
|---|---|
|Compile-time constant|Runtime constant|
|Cannot change ever|Can change via constructor|
|Inlined by compiler|Not inlined|

---

# 🔷 7️⃣ Static Methods

Static classes are perfect for helper methods.

Example:

```csharp
public static class DateHelper
{
    public static DateTime GetDateTimeFromDateOnly(DateOnly input)
    {
        return input.ToDateTime(TimeOnly.MinValue);
    }
}
```

---

### Usage:

```csharp
DateOnly date = new DateOnly(2025, 6, 1);
DateTime result = DateHelper.GetDateTimeFromDateOnly(date);

Console.WriteLine(result);
```

---

### ✅ Output:

```
01-06-2025 00:00:00
```

---

# 🔷 8️⃣ Static Members in Normal Class

You can also use static inside normal class.

```csharp
public class Employee
{
    public static int EmployeeCount = 0;

    public Employee()
    {
        EmployeeCount++;
    }
}
```

Usage:

```csharp
Employee e1 = new Employee();
Employee e2 = new Employee();

Console.WriteLine(Employee.EmployeeCount);
```

---

### ✅ Output:

```
2
```

Shared across all objects.

---

# 🔷 9️⃣ When to Use Static Class?

Use static class when:

- No instance state required
    
- Pure helper functions
    
- Shared configuration values
    
- Constants
    
- Extension methods
    

---

# 🔷 🔟 Interview-Ready Answer

If interviewer asks:

### 🔹 What is a static class?

You say:

> A static class cannot be instantiated and can only contain static members. It is typically used for utility methods, constants, or shared configuration data.

Clean. Simple. Confident.

---

# 🔷 1️⃣1️⃣ Important Design Insight

Static classes:

- Are not good for dependency injection
    
- Harder to test
    
- Should be used carefully in enterprise apps
    

In big systems, we prefer services over static classes.

---

# 🧠 Interview Test For You

If I write:

```csharp
public static class Test
{
    public static int Value;

    static Test()
    {
        Value = 10;
        Console.WriteLine("Static constructor");
    }
}
```

And in Main:

```csharp
Console.WriteLine(Test.Value);
Console.WriteLine(Test.Value);
```

