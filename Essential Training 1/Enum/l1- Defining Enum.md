
# 1️⃣ What is an Enum?

👉 **Enum (Enumerated Type)** = A special type that contains a fixed set of named constants.

You use it when:

- Values are limited
    
- You don’t want random numbers or strings
    
- You want readable and safe code
    

Example:

```csharp
DayOfWeek day = DayOfWeek.Monday;
```

Here `DayOfWeek` is a built-in enum.

---

# 2️⃣ Why Use Enum Instead of int or string?

Instead of:

```csharp
int day = 1;      // What is 1?
string day = "Mon";  // Risk of spelling mistakes
```

We use:

```csharp
DayOfWeek day = DayOfWeek.Monday;
```

✅ More readable  
✅ Type-safe  
✅ Auto suggestions in IDE  
✅ Prevents invalid values

---

# 3️⃣ Default Behavior of Enum

If you don’t assign values manually:

```csharp
enum Example
{
    A,  // 0
    B,  // 1
    C   // 2
}
```

By default:

- First value = 0
    
- Then increments by 1
    
- Base type = `int`
    

You can cast enum to int:

```csharp
int value = (int)Example.B;
```

---

# 4️⃣ Creating Custom Enum (Like in Transcript)

The instructor creates:

```csharp
enum ShiftDays
{
    Sunday = 1,
    Monday = 2,
    Tuesday = 4,
    Wednesday = 8,
    Thursday = 16,
    Friday = 32,
    Saturday = 64
}
```

⚠ Notice these values:  
1, 2, 4, 8, 16, 32, 64  
These are powers of 2.

Why?  
👉 To allow **combining multiple days together** (bitwise operations).

---

# 5️⃣ Simple Enum Example (Single Day)

### Code:

```csharp
using System;

enum ShiftDays
{
    Sunday = 1,
    Monday = 2,
    Tuesday = 4,
    Wednesday = 8,
    Thursday = 16,
    Friday = 32,
    Saturday = 64
}

class Program
{
    static void Main()
    {
        ShiftDays shiftDay = ShiftDays.Tuesday;

        Console.WriteLine("Shift Day: " + shiftDay);
        Console.WriteLine("Numeric Value: " + (int)shiftDay);
    }
}
```

---

### Output:

```
Shift Day: Tuesday
Numeric Value: 4
```

Why 4?  
Because we assigned `Tuesday = 4`.

---

# 6️⃣ Using Enum in a Class (Like ShiftWorker)

Now we create a class:

```csharp
class ShiftWorker
{
    public string FirstName { get; set; }
    public ShiftDays DaysAvailable { get; set; }
}
```

### Usage:

```csharp
ShiftWorker worker = new ShiftWorker();
worker.FirstName = "Kiran";
worker.DaysAvailable = ShiftDays.Wednesday;

Console.WriteLine(worker.DaysAvailable);
```

### Output:

```
Wednesday
```

Clean. Readable. Professional. 🔥

---

# 7️⃣ Why Not Just Use DayOfWeek?

Built-in `DayOfWeek` enum only allows:

```csharp
DayOfWeek.Monday
```

You cannot combine:

```csharp
DayOfWeek.Monday | DayOfWeek.Tuesday   ❌ Not designed for that
```

But in shift management:  
👉 A worker can be available on multiple days.

So we need something better.

---

# 8️⃣ Supporting Multiple Days (Very Important Concept)

To allow multiple values, we use:

```csharp
[Flags]
enum ShiftDays
{
    None = 0,
    Sunday = 1,
    Monday = 2,
    Tuesday = 4,
    Wednesday = 8,
    Thursday = 16,
    Friday = 32,
    Saturday = 64
}
```

Notice:

- `[Flags]` attribute
    
- Values are powers of 2
    

---

# 9️⃣ Assigning Multiple Days

```csharp
ShiftDays availableDays = ShiftDays.Monday | ShiftDays.Wednesday;

Console.WriteLine(availableDays);
Console.WriteLine((int)availableDays);
```

---

### Output:

```
Monday, Wednesday
10
```

Why 10?

Monday = 2  
Wednesday = 8

2 + 8 = 10

That number can be saved in a database.

---

# 🔟 Checking If a Worker Is Available on a Specific Day

```csharp
if ((availableDays & ShiftDays.Monday) == ShiftDays.Monday)
{
    Console.WriteLine("Worker is available on Monday");
}
```

This is called **bitwise AND checking**.

---

# 🔥 Full Professional Example

```csharp
using System;

[Flags]
enum ShiftDays
{
    None = 0,
    Sunday = 1,
    Monday = 2,
    Tuesday = 4,
    Wednesday = 8,
    Thursday = 16,
    Friday = 32,
    Saturday = 64
}

class ShiftWorker
{
    public string Name { get; set; }
    public ShiftDays DaysAvailable { get; set; }
}

class Program
{
    static void Main()
    {
        ShiftWorker worker = new ShiftWorker
        {
            Name = "Kiran",
            DaysAvailable = ShiftDays.Monday | ShiftDays.Wednesday | ShiftDays.Friday
        };

        Console.WriteLine("Worker: " + worker.Name);
        Console.WriteLine("Available Days: " + worker.DaysAvailable);
        Console.WriteLine("Stored Value: " + (int)worker.DaysAvailable);

        if ((worker.DaysAvailable & ShiftDays.Wednesday) == ShiftDays.Wednesday)
        {
            Console.WriteLine("Worker is available on Wednesday");
        }
    }
}
```

---

### Output:

```
Worker: Kiran
Available Days: Monday, Wednesday, Friday
Stored Value: 42
Worker is available on Wednesday
```

Why 42?

Monday = 2  
Wednesday = 8  
Friday = 32

2 + 8 + 32 = 42

---

# 🧠 Interview-Ready Notes

If interviewer asks:

### ❓ What is enum?

> Enum is a value type that represents a fixed set of named constants. It improves readability and type safety.

### ❓ What is the default base type?

> int

### ❓ Can you store multiple enum values?

> Yes, using `[Flags]` attribute and powers of 2.

### ❓ Why use powers of 2?

> To enable bitwise operations and combine multiple values.

---

# 🎯 Final Summary (Very Simple)

- Enum = fixed set of values
    
- Default base type = int
    
- You can cast enum to int
    
- Use `[Flags]` for multiple selections
    
- Use bitwise OR `|` to combine
    
- Use bitwise AND `&` to check
    

---



## q1

# 🚩 Why `[Flags]` Is Used in C#

`[Flags]` is used when you want an enum to represent **multiple values at the same time**.

Without `[Flags]` → enum holds **only one value**  
With `[Flags]` → enum can combine values like a set

---

## 🔹 Without `[Flags]`

```csharp
enum ShiftDays
{
    Sunday = 1,
    Monday = 2,
    Tuesday = 4
}

ShiftDays day = ShiftDays.Monday | ShiftDays.Tuesday;
Console.WriteLine(day);
```

### Output:

```
6
```

Why 6?  
2 (Monday) + 4 (Tuesday) = 6

But it prints just `6` 😐  
Not readable. Not clean.

---

## 🔹 With `[Flags]`

```csharp
[Flags]
enum ShiftDays
{
    None = 0,
    Sunday = 1,
    Monday = 2,
    Tuesday = 4
}

ShiftDays day = ShiftDays.Monday | ShiftDays.Tuesday;
Console.WriteLine(day);
```

### Output:

```
Monday, Tuesday
```

✨ See the difference?  
Now it prints properly and is human-readable.

---

# 💡 What `[Flags]` Actually Does

`[Flags]` tells C#:

> “Hey, this enum is meant to be treated as a **bit field**, and values may be combined.”

It improves:

- String formatting
    
- Debugging readability
    
- Logical intent of code
    

---

# 🧠 Why Powers of 2 Are Required

When using `[Flags]`, values must be:

```
1  -> 0001
2  -> 0010
4  -> 0100
8  -> 1000
```

Each value occupies a unique bit.

So combining works:

```
Monday  = 0010
Tuesday = 0100
----------------
Combined = 0110 (6)
```

Now we can later check:

```csharp
if ((day & ShiftDays.Monday) == ShiftDays.Monday)
{
    Console.WriteLine("Available on Monday");
}
```

---

# 🔥 Real World Example

Think of it like switches:

|Bit|Meaning|
|---|---|
|1|Sunday|
|2|Monday|
|4|Tuesday|
|8|Wednesday|

If value = 10

Binary of 10:

```
1010
```

That means:

- Monday (2) ✔
    
- Wednesday (8) ✔
    

Very efficient for:

- Storing permissions
    
- User roles
    
- File access rights
    
- Days of availability
    
- Feature toggles
    

---

# 🎯 So In One Line

`[Flags]` is used when you want an enum to represent **multiple values at the same time using bitwise operations**.

---

# ⚠ Important

`[Flags]` does NOT magically allow multiple values.

You can combine enums even without it.

But `[Flags]`:

- Makes output readable
    
- Makes intention clear
    
- Is best practice
    

---

# 🚀 Interview-Level Answer

If interviewer asks:

> Why do we use `[Flags]` in enum?

You say:

> The `[Flags]` attribute is used when an enum is intended to represent a combination of values. It enables bitwise operations and improves string representation when multiple enum values are combined.

Clean. Confident. Done. 😎

---
