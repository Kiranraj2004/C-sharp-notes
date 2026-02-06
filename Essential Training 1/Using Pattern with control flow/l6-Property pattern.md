
# 🔥 What is a Property Pattern?

A **property pattern** lets you match an object **based on its property values** inside a `switch` expression or `is` expression.

Instead of checking values like this:

```csharp
if (date.Hour >= 15 && 
   (date.DayOfWeek == DayOfWeek.Friday || 
    date.DayOfWeek == DayOfWeek.Saturday))
```

We can write it more cleanly using pattern matching.

---

# ✅ Basic Idea

Inside a `switch`, you can inspect properties like this:

```csharp
shiftDate switch
{
    { Hour: >= 15, DayOfWeek: DayOfWeek.Friday } => true,
    _ => false
};
```

Here:

- `{ Hour: >= 15 }` → relational pattern
    
- `{ DayOfWeek: DayOfWeek.Friday }` → constant pattern
    
- `_` → default case
    

---

# 🎯 Example: Weekend Night Shift

### Rule:

- Friday or Saturday
    
- Time >= 3:00 PM (15:00)
    

---

## Full Example Code

```csharp
using System;

class Program
{
    static bool IsWeekendNightShift(DateTime shiftDate) =>
        shiftDate switch
        {
            { Hour: >= 15, DayOfWeek: DayOfWeek.Friday } => true,
            { Hour: >= 15, DayOfWeek: DayOfWeek.Saturday } => true,
            _ => false
        };

    static void Main()
    {
        DateTime shift = new DateTime(2022, 1, 1, 16, 0, 0); // Jan 1, 2022 - 4 PM
        Console.WriteLine(IsWeekendNightShift(shift)
            ? "Shift is a weekend night"
            : "Shift is not a weekend night");
    }
}
```

---

## 🖥 Output (4 PM Saturday)

```
Shift is a weekend night
```

---

## 🖥 If Changed to 7 AM

```csharp
DateTime shift = new DateTime(2022, 1, 1, 7, 0, 0);
```

Output:

```
Shift is not a weekend night
```

Because:

- Day is correct ✅
    
- Hour < 15 ❌
    

---

# 🔥 Cleaner Version Using Logical Pattern

Instead of writing two separate lines:

```csharp
static bool IsWeekendNightShift(DateTime shiftDate) =>
    shiftDate switch
    {
        { Hour: >= 15, DayOfWeek: DayOfWeek.Friday or DayOfWeek.Saturday } => true,
        _ => false
    };
```

🔥 Much cleaner.

Now we’re using:

- Property pattern
    
- Relational pattern
    
- Logical pattern (`or`)
    

All combined.

---

# 🧠 Important Concept from Transcript

When using property patterns inside switch:

The properties available depend on the **target of the switch**.

Example:

```csharp
p switch
{
    ShiftWorker sw => ...
}
```

Here:

- Target of switch = `p`
    
- Type of `p` = `IPerson`
    

So when writing property patterns:

```csharp
{ FirstName: "John" }
```

You only see properties defined in `IPerson`.

Even though:

```csharp
ShiftWorker sw
```

has extra properties like `StartDate`.

Because property pattern inspects the **switch target type**, not the extracted variable.

That’s a subtle but important detail.

---

# 🔍 What Makes Property Patterns Powerful?

Old style:

```csharp
if (date.Hour >= 15 && 
   (date.DayOfWeek == Friday || date.DayOfWeek == Saturday))
```

Modern style:

```csharp
shiftDate switch
{
    { Hour: >= 15, DayOfWeek: Friday or Saturday } => true,
    _ => false
};
```

Cleaner.  
More readable.  
Very expressive.

---

# 🎯 Pattern Types Used Here

|Pattern|Example|
|---|---|
|Property pattern|`{ Hour: >= 15 }`|
|Relational pattern|`>= 15`|
|Logical pattern|`Friday or Saturday`|
|Discard pattern|`_`|

---

# l7-guard conditions

---

# 🔥 What Are Guard Conditions?

A **guard condition** adds an extra condition to a pattern match.

It uses the keyword:

```
when
```

It means:

> Match this pattern ONLY IF this extra condition is true.

---

# 🧠 Basic Syntax

Inside a switch expression or switch statement:

```csharp
Type variable when condition => result
```

OR

```csharp
case Type variable when condition:
```

So now matching is not just about type —
it also checks an additional rule.

---

# 🎯 Example 1 – Shift Worker Based on Start Year

Let’s say:

- If ShiftWorker
- AND StartDate.Year > 2020 → return normal details
- AND StartDate.Year <= 2020 → return "older employee"

---

## Code Example

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

class Program
{
    static string GetPersonDetails(IPerson p) =>
        p switch
        {
            ShiftWorker sw when sw.StartDate.Year > 2020
                => $"Shift Worker: {sw.StartDate.ToShortDateString()}",

            ShiftWorker sw when sw.StartDate.Year <= 2020
                => "Older Employee",

            _ => "Not a shift worker"
        };

    static void Main()
    {
        IPerson worker = new ShiftWorker
        {
            FirstName = "John",
            LastName = "Doe",
            StartDate = new DateTime(2020, 7, 15)
        };

        Console.WriteLine(GetPersonDetails(worker));
    }
}
```

---

## 🖥 Output (StartDate = 2020)

```
Older Employee
```

---

## 🖥 If Changed to 2022

```
Shift Worker: 7/15/2022
```

---

# 🔍 What Happened?

Both branches match `ShiftWorker`.

But the guard (`when`) decides which one runs.

Without `when`, both would conflict.

---

# 🔥 Example 2 – Guard Condition with Characters

Let’s improve our pad logic.

Rule:
- If letter (A–Z or a–z)
- BUT NOT lowercase 'x'
- Then pad left normally
- If lowercase 'x' → pad with underscores

---

## Code Example

```csharp
using System;

class Program
{
    static string PadInput(string input, int length, char padChar) =>
        padChar switch
        {
            >= 'a' and <= 'z' or >= 'A' and <= 'Z'
                when padChar != 'x'
                => input.PadLeft(length, padChar),

            'x'
                => input.PadLeft(length, '_'),

            _ => input
        };

    static void Main()
    {
        Console.WriteLine(PadInput("Hello", 15, 'z'));
        Console.WriteLine(PadInput("Hello", 15, 'x'));
    }
}
```

---

## 🖥 Output

```
zzzzzzzzzzHello
__________Hello
```

---

# 🧠 Why Guards Are Powerful

Without guards:

You’d need nested if statements inside each case.

With guards:

You keep logic clean and declarative.

---

# 🔥 Where Guards Can Be Used

✔ Switch statement  
✔ Switch expression  
✔ Pattern matching cases  

---

# 🧠 Pattern Matching Flow

Matching happens in this order:

1. Pattern match (type/value/range)
2. Guard condition check
3. If both pass → execute branch

If guard fails → next pattern is tested.

---

# 🧩 Visual Example

```csharp
ShiftWorker sw when sw.StartDate.Year > 2020
```

Means:

Step 1 → Is it ShiftWorker?  
Step 2 → Is year > 2020?  
Step 3 → If yes → execute  

---

