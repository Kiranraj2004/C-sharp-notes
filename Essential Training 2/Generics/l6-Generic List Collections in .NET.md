	
## 1️⃣ What is `List<T>`?

`List<T>` is a **generic collection class** available in:

```csharp
using System.Collections.Generic;
```

It is the **generic version of ArrayList**.

### ✔ Benefits:

- Type-safe
    
- Faster (no boxing/unboxing)
    
- Rich methods & properties
    
- Dynamic size
    

---

# 2️⃣ Creating a Generic List

### Syntax:

```csharp
List<DataType> listName = new List<DataType>();
```

Example:

```csharp
List<int> numbers = new List<int>();
```

---

# 3️⃣ Using List with Custom Class (Employee Example)

Let’s create an Employee class and store employees inside a List.

---

## 🔹 Full Example Code

```csharp
using System;
using System.Collections.Generic;

class Employee
{
    public string mName;
    public int mSalary;

    public Employee(string name, int salary)
    {
        mName = name;
        mSalary = salary;
    }
}

class Program
{
    static int total = 0;

    static void Main()
    {
        // Create list with initial capacity 10
        List<Employee> empList = new List<Employee>(10);

        // Add employees
        empList.Add(new Employee("John Doe", 50000));
        empList.Add(new Employee("Jane Smith", 60000));
        empList.Add(new Employee("Nick Slick", 55000));
        empList.Add(new Employee("Mildred Mintz", 70000));

        // Check Capacity and Count
        Console.WriteLine("Capacity: " + empList.Capacity);
        Console.WriteLine("Count: " + empList.Count);

        // Check if highly paid employee exists
        if (empList.Exists(HighPay))
        {
            Console.WriteLine("Highly paid employee found.");
        }

        // Find first employee whose name starts with J
        Employee e = empList.Find(x => x.mName.StartsWith("J"));

        if (e != null)
        {
            Console.WriteLine("Found employee whose name starts with J: " + e.mName);
        }

        // Calculate total payroll
        empList.ForEach(TotalSalaries);
        Console.WriteLine("Total payroll is: " + total);
    }

    // Delegate method for Exists()
    static bool HighPay(Employee emp)
    {
        return emp.mSalary > 65000;
    }

    // Delegate method for ForEach()
    static void TotalSalaries(Employee emp)
    {
        total += emp.mSalary;
    }
}
```

---

# ✅ Output

```
Capacity: 10
Count: 4
Highly paid employee found.
Found employee whose name starts with J: John Doe
Total payroll is: 235000
```

---

# 4️⃣ Important List Properties

|Property|Meaning|
|---|---|
|`Count`|Number of actual items|
|`Capacity`|Internal allocated memory size|

---

### Example:

```csharp
List<int> nums = new List<int>(5);
nums.Add(1);
nums.Add(2);

Console.WriteLine(nums.Count);     // 2
Console.WriteLine(nums.Capacity);  // 5
```

---

# 5️⃣ Important List Methods

---

## 🔹 1. Add()

Adds item to list.

```csharp
empList.Add(new Employee("Alex", 45000));
```

---

## 🔹 2. Exists()

Returns **true/false**

```csharp
bool found = empList.Exists(e => e.mSalary > 65000);
```

---

## 🔹 3. Find()

Returns the first matching item.

```csharp
Employee emp = empList.Find(e => e.mName.StartsWith("J"));
```

If not found → returns `null`.

---

## 🔹 4. ForEach()

Executes action on every item.

```csharp
empList.ForEach(e => Console.WriteLine(e.mName));
```

---

## 🔹 5. Remove()

```csharp
empList.Remove(emp);
```

---

## 🔹 6. Clear()

```csharp
empList.Clear();
```

---

# 6️⃣ Capacity vs Count (Important Concept)

|Concept|Meaning|
|---|---|
|Count|How many elements currently|
|Capacity|How many elements can fit before resizing|

### Why set capacity?

If you know number of items beforehand:

```csharp
List<Employee> empList = new List<Employee>(1000);
```

✔ Better performance  
✔ Less memory reallocation

---

# 7️⃣ Lambda Expression Used in Find()

### Syntax:

```csharp
parameter => condition
```

Example:

```csharp
e => e.mName.StartsWith("J")
```

Meaning:

> For each employee, check if name starts with J.

---

# 8️⃣ Execution Flow Explanation

### Exists(HighPay)

- Calls `HighPay()` for each employee
    
- Stops when one returns true
    

---

### Find(x => x.mName.StartsWith("J"))

- Checks each employee
    
- Returns first match
    

---

### ForEach(TotalSalaries)

- Calls `TotalSalaries()` for every employee
    
- Adds salaries together
    
