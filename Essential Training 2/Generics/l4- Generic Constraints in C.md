
---

# 1️⃣ What Is a Generic Constraint?

When we define:

```csharp
class Sorter<T>
```

The compiler does NOT know:

- Is `T` a number?
    
- Is it a string?
    
- Can it be compared?
    
- Does it have a constructor?
    

So if we try:

```csharp
if (items[i] > items[i - 1])
```

❌ Compiler error.

Why?

Because:

> “I don’t know what T is. I don’t know if it supports comparison.”

---

# 2️⃣ The Solution: `where` Constraint

We add rules using:

```csharp
where T : some_rule
```

Example:

```csharp
class Sorter<T> where T : IComparable<T>
```

Now we are telling the compiler:

> Whatever T is, it MUST implement IComparable.

That means:

- It must have `CompareTo()` method
    
- Now we can safely compare objects
    

---

# 3️⃣ Example: Generic Sorter Class

### 🔹 Step 1: Define Sorter with Constraint

```csharp
using System;

public class Sorter<T> where T : IComparable<T>
{
    public void Sort(T[] items)
    {
        for (int i = 1; i < items.Length; i++)
        {
            if (items[i].CompareTo(items[i - 1]) < 0)
            {
                Swap(items, i, i - 1);
            }
        }
    }

    private void Swap(T[] items, int index1, int index2)
    {
        T temp = items[index1];
        items[index1] = items[index2];
        items[index2] = temp;
    }
}
```

---

## 🧠 Why This Works

Because:

```csharp
where T : IComparable<T>
```

guarantees:

```csharp
items[i].CompareTo(...)
```

is valid.

Compiler is happy ✅

---

# 4️⃣ Now Create a Class That Supports Comparison

## 🔹 Customer Class

```csharp
public class Customer : IComparable<Customer>
{
    public int Id { get; set; }
    public string FirstName { get; set; }

    public int CompareTo(Customer other)
    {
        if (this.Id == other.Id)
            return 0;
        else if (this.Id < other.Id)
            return -1;
        else
            return 1;
    }
}
```

---

## 🧠 What CompareTo Means

|Return Value|Meaning|
|---|---|
|0|Equal|
|Negative|Less than|
|Positive|Greater than|

We are comparing customers based on **Id**.

---

# 5️⃣ Using the Sorter

```csharp
class Program
{
    static void Main()
    {
        Customer c1 = new Customer { Id = 7, FirstName = "Alice" };
        Customer c2 = new Customer { Id = 3, FirstName = "Bob" };

        Customer[] customers = { c1, c2 };

        Sorter<Customer> sorter = new Sorter<Customer>();
        sorter.Sort(customers);

        foreach (var c in customers)
        {
            Console.WriteLine($"Id: {c.Id}, Name: {c.FirstName}");
        }
    }
}
```

---

# ✅ Output

```
Id: 3, Name: Bob
Id: 7, Name: Alice
```

Sorted by ID 🎯

---

# 🔥 What If We Remove Constraint?

If we remove:

```csharp
where T : IComparable<T>
```

Then this line:

```csharp
items[i].CompareTo(...)
```

💥 Compile-time error:

> T does not contain definition for CompareTo

---

# 6️⃣ Types of Generic Constraints

C# supports several constraints:

---

## 🔹 1. Must Be Class

```csharp
where T : class
```

Only reference types allowed.

---

## 🔹 2. Must Be Struct

```csharp
where T : struct
```

Only value types allowed.

---

## 🔹 3. Must Inherit From Specific Class

```csharp
where T : Animal
```

---

## 🔹 4. Must Implement Interface

```csharp
where T : IComparable<T>
```

---

## 🔹 5. Must Have Empty Constructor

```csharp
where T : new()
```

Allows:

```csharp
T obj = new T();
```

---

## 🔹 Combine Constraints

```csharp
where T : class, IComparable<T>, new()
```

---

# 🧠 Why Constraints Are Powerful

They allow:

- Compile-time safety
    
- Enforcing design rules
    
- Avoiding runtime errors
    
- Cleaner architecture
    

Without constraints → generics are blind.  
With constraints → generics are smart.

---

