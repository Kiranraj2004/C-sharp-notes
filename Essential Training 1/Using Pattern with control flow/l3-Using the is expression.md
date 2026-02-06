
# 1️⃣ Problem Scenario (From Transcript)

We have:

- An interface: `IPerson`
    
- Two classes:
    
    - `ShiftWorker`
        
    - `Manager`
        
- Both implement `IPerson`
    

But inside a method, we receive only:

```csharp
IPerson p
```

Now the question becomes:

👉 How do we check what actual type it is?

---

# 2️⃣ Old Way: Using `as` Keyword

### What `as` does

- Tries to cast
    
- If successful → returns object
    
- If not → returns `null`
    
- Must check for `null`
    

---

## Example Using `as`

```csharp
using System;

interface IPerson
{
    string FirstName { get; }
    string LastName { get; }
}

class ShiftWorker : IPerson
{
    public string FirstName { get; set; }
    public string LastName { get; set; }
    public DateTime StartDate { get; set; }
}

class Manager : IPerson
{
    public string FirstName { get; set; }
    public string LastName { get; set; }
    public int DirectReports { get; set; }
}

class Program
{
    static string GetPersonDetails(IPerson p)
    {
        ShiftWorker sw = p as ShiftWorker;

        if (sw != null)
        {
            return $"{sw.FirstName} {sw.LastName}, Start Date: {sw.StartDate}";
        }

        return string.Empty;
    }

    static void Main()
    {
        IPerson sw = new ShiftWorker
        {
            FirstName = "John",
            LastName = "Doe",
            StartDate = new DateTime(2022, 1, 10)
        };

        IPerson mgr = new Manager
        {
            FirstName = "Alice",
            LastName = "Smith",
            DirectReports = 5
        };

        Console.WriteLine(GetPersonDetails(sw));
        Console.WriteLine(GetPersonDetails(mgr));
    }
}
```

---

## 🖥 Output

```
John Doe, Start Date: 10-01-2022 12:00:00 AM

```

Notice:

- ShiftWorker prints
    
- Manager prints empty string
    

Because `as` returns null if not match.

---

# 3️⃣ Modern Way: Using `is` (Pattern Matching)

C# improved this 🔥

Instead of:

```csharp
ShiftWorker sw = p as ShiftWorker;
if (sw != null)
```

We can write:

```csharp
if (p is ShiftWorker sw)
```

This does TWO things:

1. Checks type
    
2. Declares and assigns variable
    

Much cleaner.

---

# Example Using `is` Pattern Matching

```csharp
static string GetPersonDetails(IPerson p)
{
    if (p is ShiftWorker sw)
    {
        return $"{sw.FirstName} {sw.LastName}, Start Date: {sw.StartDate}";
    }
    else if (p is Manager mgr)
    {
        return $"{mgr.FirstName} {mgr.LastName}, Reports: {mgr.DirectReports}";
    }

    return string.Empty;
}
```

---

## 🖥 Output

```
John Doe, Start Date: 10-01-2022 12:00:00 AM
Alice Smith, Reports: 5
```

---

# 🔎 What Exactly is Happening?

### This:

```csharp
if (p is ShiftWorker sw)
```

Means:

- Check if `p` is of type `ShiftWorker`
    
- If TRUE:
    
    - Create variable `sw`
        
    - Assign `p` to `sw`
        
    - Enter block
        

If FALSE:

- Skip block
    

No null checks needed. Cleaner. Safer.

---

# 4️⃣ `is` vs `as` — Clear Comparison

|Feature|`as`|`is`|
|---|---|---|
|Casting|Yes|No (just checks)|
|Returns null|Yes|No|
|Needs null check|Yes|No|
|Pattern matching|❌|✅|
|Cleaner|❌|✅|

---

# 5️⃣ Even More Modern (Switch Pattern Matching)

You can combine this with switch:

```csharp
static string GetPersonDetails(IPerson p) =>
    p switch
    {
        ShiftWorker sw => $"{sw.FirstName} {sw.LastName}, Start Date: {sw.StartDate}",
        Manager mgr => $"{mgr.FirstName} {mgr.LastName}, Reports: {mgr.DirectReports}",
        _ => string.Empty
    };
```

🔥 This is very modern C#.

---

# 🎯 Why Do We Need This?

Because:

- We receive interface type (`IPerson`)
    
- But we need implementation-specific properties
    
    - ShiftWorker → StartDate
        
    - Manager → DirectReports
        

So we must check real type.

---

