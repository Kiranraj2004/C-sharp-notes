
This section is mainly about:

- Working with `List<T>`
    
- Indexing
    
- `Contains()`
    
- `Find()` with predicate
    
- `Reverse()`
    
- `Sort()` with `IComparable`
    
- Iteration (Enumerator vs foreach)
    
- Reference type vs value type behavior
    

Let’s break it clean and simple 👇

---

# 🧠 1. Setup – Creating a List of Customers

We create:

```csharp
static List<Customer> customers;
```

In static constructor:

- Create new list
    
- Add 10–11 customers
    
- ID = 1 to 10
    
- FirstName = i
    
- LastName = "Customer"
    
- Date = October 2021
    

So now we have a collection of objects.

---

# 📌 2. Indexing in List

Just like arrays:

```csharp
var customer = customers[2];
```

✔ Zero-based indexing  
✔ Direct access  
✔ Returns actual object (no casting)

---

# 📌 3. Contains()

```csharp
customers.Contains(customerThree);
```

Important concept 🔥

### If Customer is a class (reference type)

`Contains()` checks:

- Are they the same object reference?
    

If you create a new object with same values:

```csharp
new Customer(3, "3", "Customer", date)
```

👉 It will return FALSE  
Because it's a different memory reference.

---

# 📌 4. Find() with Predicate

```csharp
customers.Find(CustomerIsMatch);
```

A **predicate** = method that returns `bool`

Example:

```csharp
static bool CustomerIsMatch(Customer c)
{
    return c.Id == 7;
}
```

`Find()`:

- Loops through list
    
- Calls predicate
    
- Returns first match
    
- Stops when true is found
    

---

# 📌 5. Reverse()

```csharp
customers.Reverse();
```

Reverses order of list.

Not sorting.  
Just flips order.

Example:

Before:

```
1 2 3 4 5
```

After:

```
5 4 3 2 1
```

---

# 📌 6. Iteration – Two Ways

### 🔹 Method 1: Manual Enumerator

```csharp
var enumerator = customers.GetEnumerator();

while (enumerator.MoveNext())
{
    var current = enumerator.Current;
    Console.WriteLine(current.Id);
}
```

More control.  
Low-level.

---

### 🔹 Method 2: foreach (Recommended)

```csharp
foreach (var customer in customers)
{
    Console.WriteLine(customer.Id);
}
```

Simpler.  
Cleaner.  
Same logic internally.

---

# 📌 7. Sorting with IComparable

If Customer implements:

```csharp
IComparable<Customer>
```

Then you can:

```csharp
customers.Sort();
```

Sort uses:

```csharp
CompareTo()
```

Example:

```csharp
public int CompareTo(Customer other)
{
    return this.Id.CompareTo(other.Id);
}
```

Sorts by ID.

---

# 🧪 FULL WORKING EXAMPLE

### 🔹 Customer Class

```csharp
using System;

public class Customer : IComparable<Customer>
{
    public int Id { get; set; }
    public string FirstName { get; set; }
    public string LastName { get; set; }
    public DateTime CreatedDate { get; set; }

    public Customer(int id, string firstName, string lastName, DateTime date)
    {
        Id = id;
        FirstName = firstName;
        LastName = lastName;
        CreatedDate = date;
    }

    public int CompareTo(Customer other)
    {
        return this.Id.CompareTo(other.Id);
    }

    public override string ToString()
    {
        return $"Customer {Id}";
    }
}
```

---

### 🔹 CollectionSamples Example

```csharp
using System;
using System.Collections.Generic;

class Program
{
    static List<Customer> customers;

    static Program()
    {
        customers = new List<Customer>();

        for (int i = 1; i <= 10; i++)
        {
            customers.Add(new Customer(
                i,
                i.ToString(),
                "Customer",
                new DateTime(2021, 10, i)
            ));
        }
    }

    static void Main()
    {
        // INDEXING
        var customerThree = customers[2];
        Console.WriteLine($"Found {customerThree} at index 2");

        // CONTAINS
        Console.WriteLine("Contains customerThree? " + customers.Contains(customerThree));

        // FIND (Predicate)
        var customerSeven = customers.Find(CustomerIsMatch);
        Console.WriteLine($"Found {customerSeven}");

        // REVERSE
        customers.Reverse();
        Console.WriteLine("After Reverse:");
        foreach (var c in customers)
        {
            Console.Write(c.Id + " ");
        }

        Console.WriteLine();

        // SORT
        customers.Sort();
        Console.WriteLine("After Sort:");
        foreach (var c in customers)
        {
            Console.Write(c.Id + " ");
        }
    }

    static bool CustomerIsMatch(Customer c)
    {
        return c.Id == 7;
    }
}
```

---

# 🖥 OUTPUT

```
Found Customer 3 at index 2
Contains customerThree? True
Found Customer 7
After Reverse:
10 9 8 7 6 5 4 3 2 1
After Sort:
1 2 3 4 5 6 7 8 9 10
```

---

# 🔥 Important Concept – Reference Type Behavior

If you do this:

```csharp
var newCustomer = new Customer(3, "3", "Customer", new DateTime(2021,10,3));
Console.WriteLine(customers.Contains(newCustomer));
```

Output:

```
False
```

Because:

- Same values
    
- Different object reference
    

Unless you override `Equals()` and `GetHashCode()`.

---

