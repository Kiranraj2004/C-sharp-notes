
# 🔥 Introduction to Patterns (C# 7+)

## ✅ What Are Patterns?

Patterns allow us to:
- Check a type
- Extract a value
- Match conditions
- Use them inside:
  - `is` statement
  - `switch` statement
  - `switch` expression

They make type checking + casting much cleaner.

---

# 1️⃣ Type Pattern

This is the simplest one.

### Example:

```csharp
if (p is ShiftWorker)
```

✔ Checks if `p` is of type `ShiftWorker`  
✔ Returns true or false  
❌ Does NOT create a variable  

This is called a **Type Pattern**.

---

# 2️⃣ Declaration Pattern (Most Common)

This is more powerful.

```csharp
if (p is ShiftWorker sw)
```

This does TWO things:

1. Checks if `p` is `ShiftWorker`
2. Declares a variable `sw` of type `ShiftWorker`

This replaces:

```csharp
ShiftWorker sw = p as ShiftWorker;
if (sw != null)
```

Much cleaner.

---

# 3️⃣ Using Patterns Inside `switch` Expression

Earlier, switch was limited to constant values:

```csharp
case 1:
case 2:
```

But now we can match TYPES.

Instead of:

```csharp
if (p is ShiftWorker sw)
{
    return "...";
}
else if (p is Manager mgr)
{
    return "...";
}
```

We can use:

```csharp
var result = p switch
{
    ShiftWorker sw => $"{sw.FirstName} {sw.LastName}, Start: {sw.StartDate}",
    Manager mgr => $"{mgr.FirstName} {mgr.LastName}, Reports: {mgr.DirectReports}",
    _ => string.Empty
};

return result;
```

🔥 This is pattern matching inside switch expression.

---

# 4️⃣ What Is Happening Here?

When we write:

```csharp
ShiftWorker sw =>
```

This means:

- If `p` is `ShiftWorker`
- Declare `sw`
- Execute expression on right side
- Return that value

No need for:
- `as`
- null checks
- break
- return inside each case

Cleaner + safer.

---

# 5️⃣ Patterns Work In 3 Places

| Location | Example |
|----------|----------|
| `is` statement | `if (p is ShiftWorker sw)` |
| `switch` statement | `case ShiftWorker sw:` |
| `switch` expression | `ShiftWorker sw => ...` |

Same concept, different syntax context.

---

# 6️⃣ Why Patterns Are Powerful

Before C# 7:

Switch only worked with:
- int
- char
- string
- enum
- constant values

After patterns:

Switch can now:
- Match types
- Extract variables
- Use conditions
- Become much more expressive

---

# 7️⃣ Core Idea Behind Patterns

Instead of:

> Compare value to constant

We now do:

> Match structure or type and optionally extract data

That’s a big conceptual upgrade.

---

# 8️⃣ Real Interview-Level Explanation

If interviewer asks:

> What are patterns in C#?

You can say:

> Patterns in C# allow us to match an object against a specific type or condition and optionally extract a strongly typed variable. They are commonly used with the `is` operator, switch statements, and switch expressions, and were introduced in C# 7 to make code more expressive and type-safe.

That answer sounds solid.

---

# 9️⃣ Why Instructor Says Patterns Keep Improving

Each C# version added new pattern types:

- C# 7 → Type & Declaration patterns
- C# 8 → Switch expressions
- C# 9 → Relational & logical patterns
- C# 10+ → More refinements

So patterns are evolving.

---

# 🔟 Big Conceptual Upgrade

Old switch:
```
Value → Constant comparison
```

Modern switch:
```
Object → Pattern match → Extract → Return
```

That’s much more flexible.

---

# 🧠 Quick Revision Summary

✔ Patterns were introduced in C# 7  
✔ Used with `is`, `switch`, `switch expression`  
✔ Type pattern → only checks type  
✔ Declaration pattern → checks + declares variable  
✔ Makes switch more powerful  
✔ Removes need for manual casting  

---

# l5-Constant, relational, and logical patterns


- ✅ Constant patterns
    
- ✅ Relational patterns
    
- ✅ Logical patterns (`and`, `or`, `not`)
    
- ✅ How they combine
    

Let’s break this cleanly and simply.

---

# 🔥 1️⃣ Constant Pattern

This is the traditional switch behavior.

### Definition:

Matches against a fixed constant value.

### Example:

```csharp
case 'A':
case 'Z':
```

Here:

- `'A'` and `'Z'` are constants.
    
- We are checking equality.
    

---

### Switch Expression Example

```csharp
padChar switch
{
    '0' => "Digit Zero",
    '1' => "Digit One",
    _ => "Other"
};
```

✔ Simple  
✔ Exact match  
✔ Old-style behavior

---

# 🔥 2️⃣ Relational Pattern (C# 9+)

Now we can use:

- `>`
    
- `<`
    
- `>=`
    
- `<=`
    

inside switch.

---

### Example: Check lowercase letters

```csharp
case >= 'a' and <= 'z':
```

This means:

> If padChar is between 'a' and 'z'

Very powerful 🔥

---

# 🔥 3️⃣ Logical Patterns

We can combine patterns using:

- `and`
    
- `or`
    
- `not`
    

⚠ Important:  
Use `and` instead of `&&`  
Use `or` instead of `||`

Because this is pattern syntax, not normal boolean syntax.

---

# 💡 Example – Combining Relational + Logical

```csharp
case >= 'a' and <= 'z':
case >= 'A' and <= 'Z':
```

This means:

> If padChar is any letter (lowercase or uppercase)

---

# 🔥 Full Example (Pad Logic)

Let’s write a full switch statement using these patterns.

```csharp
using System;

class Program
{
    static string PadInput(string input, int length, char padChar)
    {
        return padChar switch
        {
            >= 'a' and <= 'z' => input.PadLeft(length, padChar),
            >= 'A' and <= 'Z' => input.PadLeft(length, padChar),

            >= '0' and <= '9' => input.PadRight(length, padChar),

            _ => input
        };
    }

    static void Main()
    {
        Console.WriteLine(PadInput("Hello", 10, '0'));
        Console.WriteLine(PadInput("Hello", 10, 'Z'));
    }
}
```

---

# 🖥 Output

```
Hello00000
ZZZZZHello
```

---

### Explanation:

1️⃣ `'0'` → digit → PadRight  
2️⃣ `'Z'` → uppercase letter → PadLeft

---

# 🔥 Combining Everything in ONE Line

You can combine uppercase and lowercase like this:

```csharp
case (>= 'a' and <= 'z') or (>= 'A' and <= 'Z'):
```

This means:

> If lowercase OR uppercase letter

Very expressive.

---

# 🧠 Pattern Types Summary

|Pattern Type|Example|Meaning|
|---|---|---|
|Constant|`'A'`|Exact match|
|Relational|`>= 'a'`|Compare values|
|Logical|`and`, `or`, `not`|Combine patterns|

---

# 🔥 Why This Is Powerful

Old switch:

```
Only constant equality
```

Modern switch:

```
Ranges
Combined conditions
Type checks
Value extraction
```

Switch is no longer limited to constant comparison.

---

# 🔍 Important Difference

Normal boolean logic:

```csharp
if (x >= 'a' && x <= 'z')
```

Pattern matching logic:

```csharp
case >= 'a' and <= 'z':
```

Different syntax.  
Different concept.  
Cleaner inside switch.

---

