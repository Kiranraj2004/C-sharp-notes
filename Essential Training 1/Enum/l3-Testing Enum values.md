
# 🔹 1. What is a Flags Enum?

When you use `[Flags]` with an enum, it allows you to combine multiple values using **bitwise operations**.

### Example Enum

```csharp
[Flags]
public enum ShiftDays : short
{
    None = 0,
    Monday = 1,
    Tuesday = 2,
    Wednesday = 4,
    Thursday = 8,
    Friday = 16,
    Saturday = 32,
    Sunday = 64,

    Weekdays = Monday | Tuesday | Wednesday | Thursday | Friday,
    Weekend = Saturday | Sunday
}
```

### 💡 Why powers of 2?

Because each value must have a unique bit:

```
1   -> 00000001
2   -> 00000010
4   -> 00000100
8   -> 00001000
```

This allows combining values safely using bitwise OR (`|`).

---

# 🔹 2. Combining Enum Values

```csharp
ShiftDays daysAvailable = ShiftDays.Weekdays;
```

This means:

```
Monday + Tuesday + Wednesday + Thursday + Friday
```

---

# 🔹 3. Testing Enum Values

## ✅ Method 1: Using `HasFlag()`

```csharp
bool availableMonday = daysAvailable.HasFlag(ShiftDays.Monday);
Console.WriteLine("Available Monday: " + availableMonday);
```

### ✔ Output:

```
Available Monday: True
```

---

## ✅ Method 2: Using Bitwise AND (&)

```csharp
bool availableSaturday = 
    (daysAvailable & ShiftDays.Saturday) == ShiftDays.Saturday;

Console.WriteLine("Available Saturday: " + availableSaturday);
```

### ✔ Output:

```
Available Saturday: False
```

### 🔎 How this works:

If Saturday is not included, then:

```
daysAvailable & Saturday → 0
```

So it won’t equal `ShiftDays.Saturday`.

---

# 🔹 4. If We Change to Weekend

```csharp
ShiftDays daysAvailable = ShiftDays.Weekend;
```

### Output:

```
Available Monday: False
Available Saturday: True
```

It flip-flops because now only Saturday and Sunday are included.

---

# 🔹 5. Getting All Enum Names

You can get all enum names using:

```csharp
string[] shiftNames = Enum.GetNames(typeof(ShiftDays));

Console.WriteLine(string.Join(", ", shiftNames));
```

### ✔ Output:

```
None, Monday, Tuesday, Wednesday, Thursday, Friday, Saturday, Sunday, Weekdays, Weekend
```

Useful for:

- Dropdown menus
    
- Displaying available options
    
- UI selection lists
    

---

# 🔹 6. Getting All Enum Values

```csharp
short[] shiftValues = 
    (short[])Enum.GetValues(typeof(ShiftDays));

Console.WriteLine(string.Join(", ", shiftValues));
```

### ✔ Output:

```
0, 1, 2, 4, 8, 16, 32, 64, 31, 96
```

### 🔎 Explanation of special values:

- `31` = Weekdays (1+2+4+8+16)
    
- `96` = Weekend (32+64)
    

---

# 🔹 7. Full Working Example

```csharp
using System;

class Program
{
    [Flags]
    public enum ShiftDays : short
    {
        None = 0,
        Monday = 1,
        Tuesday = 2,
        Wednesday = 4,
        Thursday = 8,
        Friday = 16,
        Saturday = 32,
        Sunday = 64,
        Weekdays = Monday | Tuesday | Wednesday | Thursday | Friday,
        Weekend = Saturday | Sunday
    }

    static void Main()
    {
        ShiftDays daysAvailable = ShiftDays.Weekdays;

        bool availableMonday = daysAvailable.HasFlag(ShiftDays.Monday);
        bool availableSaturday =
            (daysAvailable & ShiftDays.Saturday) == ShiftDays.Saturday;

        Console.WriteLine("Available Monday: " + availableMonday);
        Console.WriteLine("Available Saturday: " + availableSaturday);

        string[] shiftNames = Enum.GetNames(typeof(ShiftDays));
        Console.WriteLine("Shift Names: " + string.Join(", ", shiftNames));

        short[] shiftValues =
            (short[])Enum.GetValues(typeof(ShiftDays));
        Console.WriteLine("Shift Values: " + string.Join(", ", shiftValues));
    }
}
```

---

# 🎯 Final Simple Notes (Quick Revision)

### ✔ `[Flags]`

- Allows combining enum values.
    
- Must use powers of 2.
    

### ✔ Combine values

```csharp
ShiftDays days = ShiftDays.Monday | ShiftDays.Wednesday;
```

### ✔ Check value

```csharp
days.HasFlag(ShiftDays.Monday);
```

OR

```csharp
(days & ShiftDays.Monday) == ShiftDays.Monday;
```

### ✔ Get all names

```csharp
Enum.GetNames(typeof(ShiftDays));
```

### ✔ Get all values

```csharp
Enum.GetValues(typeof(ShiftDays));
```

---

