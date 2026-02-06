
# 🔥 Switch Statement vs Switch Expression (C# 8+)

---

# 1️⃣ Switch Statement (Traditional)

### ✅ What it is

- Introduced long ago
    
- Uses `switch` keyword
    
- Contains `case` blocks
    
- Each case executes statements
    
- Must use `break`, `return`, or `throw`
    

---

### 🧱 Structure

```csharp
switch (variable)
{
    case value1:
        // multiple lines of logic
        break;

    case value2:
        // multiple lines
        break;

    default:
        // fallback
        break;
}
```

---

### ✅ Key Characteristics

✔ Used for branching logic  
✔ Can contain multiple statements  
✔ Requires explicit exit (`break`)  
✔ More verbose

---

# Example – Switch Statement

```csharp
using System;

class Program
{
    static string GetShiftDay(DayOfWeek day)
    {
        switch (day)
        {
            case DayOfWeek.Monday:
                return "Monday Shift";

            case DayOfWeek.Tuesday:
                return "Tuesday Shift";

            case DayOfWeek.Wednesday:
                return "Wednesday Shift";

            default:
                throw new ArgumentException("Invalid day");
        }
    }

    static void Main()
    {
        var shift = GetShiftDay(DateTime.Now.DayOfWeek);
        Console.WriteLine(shift);
    }
}
```

---

### 🖥 Sample Output (if today is Tuesday)

```
Tuesday Shift
```

---

# 2️⃣ Switch Expression (C# 8+)

Now comes the modern version 🚀

### ✅ What it is

- Introduced in C# 8
    
- Returns a value directly
    
- More compact
    
- Expression-based (no `break`)
    
- Uses `=>`
    

---

### 🧱 Structure

```csharp
variable switch
{
    pattern1 => result1,
    pattern2 => result2,
    _ => defaultResult
};
```

⚠ `_` is the default case (like `default` in switch statement)

---

# Example – Switch Expression

```csharp
using System;

class Program
{
    static string GetShiftDay(DayOfWeek day) =>
        day switch
        {
            DayOfWeek.Monday => "Monday Shift",
            DayOfWeek.Tuesday => "Tuesday Shift",
            DayOfWeek.Wednesday => "Wednesday Shift",
            DayOfWeek.Thursday => "Thursday Shift",
            DayOfWeek.Friday => "Friday Shift",
            DayOfWeek.Saturday => "Weekend Shift",
            DayOfWeek.Sunday => "Weekend Shift",
            _ => throw new ArgumentException("Invalid day supplied")
        };

    static void Main()
    {
        var shift = GetShiftDay(DateTime.Now.DayOfWeek);
        Console.WriteLine(shift);
    }
}
```

---

### 🖥 Output (If today is Tuesday)

```
Tuesday Shift
```

---

# 🧠 Important Differences

|Feature|Switch Statement|Switch Expression|
|---|---|---|
|Introduced|Early C#|C# 8|
|Style|Statement-based|Expression-based|
|Returns value directly|❌ No|✅ Yes|
|Needs break|✅ Yes|❌ No|
|Cleaner syntax|❌|✅|
|Best for simple mapping|😐|✅ Perfect|

---

# 🔥 What Happened in the Transcript?

The instructor did this:

```csharp
day switch
{
    DayOfWeek.Monday => ShiftDay.Monday,
    ...
}
```

Each line:

- Left side → condition/pattern
    
- Right side → returned value
    
- Separated by commas
    
- Entire thing returns a value
    

---

# ⚠ Important: Why Warning Happened?

`DayOfWeek` is an enum (internally int).

So this is possible:

```csharp
GetShiftDay((DayOfWeek)17);
```

17 is not a valid day.

If no `_` case is present → runtime exception:

```
SwitchExpressionException
```

So we add:

```csharp
_ => throw new ArgumentException("Invalid day supplied")
```

Now we control the error safely.

---

# 🧪 Example: Invalid Enum

```csharp
var shift = GetShiftDay((DayOfWeek)17);
Console.WriteLine(shift);
```

### 🖥 Output

```
Unhandled Exception:
System.ArgumentException: Invalid day supplied
```

---

# 🎯 Simplified Real-World Example (Interview Friendly)

### Traditional Way

```csharp
string GetGrade(int marks)
{
    switch (marks)
    {
        case 90:
            return "A";
        case 80:
            return "B";
        default:
            return "C";
    }
}
```

---

### Modern Way (Switch Expression)

```csharp
string GetGrade(int marks) =>
    marks switch
    {
        90 => "A",
        80 => "B",
        _ => "C"
    };
```

Much cleaner 👌

---

# 🚀 When Should You Use Switch Expression?

Use it when:

✔ You're mapping input → output  
✔ Logic is simple  
✔ You want cleaner code  
✔ Returning a value

---

# ❌ When NOT to Use It

Avoid if:

- You need multiple statements
    
- You need complex logic blocks
    
- You need loops inside case
    

Then use traditional switch.

---

