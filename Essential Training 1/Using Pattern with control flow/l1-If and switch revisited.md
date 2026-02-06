
---

# 🔹 1️⃣ if Statement – Simple Notes

### ✅ What is `if`?

`if` is used to check **conditions (boolean expressions)**.

It works when:

- You need comparisons (`==`, `!=`, `<`, `>`)
    
- You need logical operations (`&&`, `||`)
    
- You need complex expressions
    

---

### ✅ Basic Structure

```csharp
if (condition)
{
    // execute if true
}
else if (anotherCondition)
{
    // execute if true
}
else
{
    // execute if none are true
}
```

---

### ✅ Important Notes from Transcript

✔ Always use curly braces `{ }` for clean scoping  
✔ You can use complex conditions with `&&`  
✔ Good for validation checks  
✔ Can throw exceptions if condition fails

---

# 🔹 Example 1 – if-else (Pad and Trim Logic)

Let’s write a simplified version.

```csharp
using System;

class Program
{
    static string PadInput(string input, int length)
    {
        if (input == null)
        {
            return "Input is null";
        }
        else if (input.Length <= length)
        {
            return input.PadRight(length, '*');
        }
        else
        {
            throw new ArgumentException("Input is longer than requested length");
        }
    }

    static void Main()
    {
        string result = PadInput("Hello", 10);
        Console.WriteLine(result);
    }
}
```

---

### 🖥 Output

```
Hello*****
```

---

### 🧠 Explanation

- `"Hello"` length = 5
    
- Requested length = 10
    
- 5 <= 10 → true
    
- So we pad with `*`
    
- Result becomes `"Hello*****"`
    

---

### ❗ What if input is longer?

```csharp
PadInput("HelloWorld123", 5);
```

Output:

```
Unhandled Exception:
System.ArgumentException: Input is longer than requested length
```

---

# 🔹 2️⃣ switch Statement – Simple Notes

### ✅ What is `switch`?

`switch` is used when:

- You compare a value against multiple constant options
    
- Cleaner than many `else if` statements
    
- Good for fixed known cases
    

---

### 🧱 Basic Structure

```csharp
switch (variable)
{
    case value1:
        // code
        break;

    case value2:
        // code
        break;

    default:
        // code
        break;
}
```

---

### ✅ Important Points from Transcript

✔ Works with simple types (char, int, string)  
✔ Each case must end with:

- `break`
    
- `return`
    
- `throw`
    

✔ You can stack cases (fall-through behavior)

```csharp
case '0':
case '9':
    // same logic
    break;
```

That means:  
👉 If it's '0' OR '9', run this block.

---

# 🔹 Example 2 – Switch with Pad Character

```csharp
using System;

class Program
{
    static string PadInput(string input, int length, char padChar)
    {
        switch (padChar)
        {
            case ' ':
            case '|':
                return input.PadLeft(length, padChar);

            case '0':
            case '9':
                return input.PadRight(length, padChar);

            default:
                throw new ArgumentException("No match found for pad character");
        }
    }

    static void Main()
    {
        string result = PadInput("Data", 10, '0');
        Console.WriteLine(result);
    }
}
```

---

### 🖥 Output

```
Data000000
```

---

### 🧠 Why?

- `"Data"` length = 4
    
- Target = 10
    
- padChar = `'0'`
    
- Case `'0'` → PadRight
    
- Adds 6 zeros
    

---

# 🔹 Example 3 – Multiple Case Fall-through

```csharp
char ch = '9';

switch (ch)
{
    case '0':
    case '9':
        Console.WriteLine("Pad Right Character");
        break;

    default:
        Console.WriteLine("Other Character");
        break;
}
```

### 🖥 Output

```
Pad Right Character
```

Because `'9'` falls into same block as `'0'`.

---

# 🔹 if vs switch (Interview Comparison)

|Feature|if|switch|
|---|---|---|
|Complex conditions|✅ Yes|❌ No (traditional switch)|
|Logical operators|✅ Yes|❌ No|
|Multiple constant values|😐 Messy|✅ Clean|
|Readability for many cases|😐 Hard|✅ Better|

---

# 🔹 When to Use What?

### ✔ Use `if` when:

- Checking ranges (`age > 18`)
    
- Using `&&` or `||`
    
- Validating input
    
- Complex logic
    

### ✔ Use `switch` when:

- Comparing one variable to multiple constant values
    
- Cleaner decision branching
    
- Enum-based logic
    

---

# 🔥 Bonus (Important for You – Interview Point)

In **modern C# (C# 7+)**, switch is more powerful:

- Pattern matching
    
- Switch expressions
    
- More dynamic logic
    

Example:

```csharp
string result = padChar switch
{
    '0' or '9' => input.PadRight(length, padChar),
    ' ' or '|' => input.PadLeft(length, padChar),
    _ => throw new ArgumentException("Invalid character")
};
```

Much cleaner 👌

---

