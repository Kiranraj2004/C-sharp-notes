
# 🧠 1️⃣ What is a Lambda Expression?

A **lambda expression** is a short way to write a method inline.

Instead of writing:

```csharp
static int GetLength(string s)
{
    return s.Length;
}
```

You can write:

```csharp
s => s.Length
```

That’s it.

---

# 🧠 2️⃣ Basic Lambda Syntax

```
(parameters) => expression
```

OR

```
(parameters) => { multiple statements }
```

The `=>` is called the **lambda operator**.

Think of it as:

```
input  =>  output
```

---

# 🟢 3️⃣ Simple Expression Lambda (One Expression)

If there’s only ONE expression:

- No `{ }`
    
- No `return`
    
- The value is automatically returned
    

---

## 🧪 Example 1 – No Return (Action)

```csharp
using System;

class Program
{
    static void Main()
    {
        Action<string> t = s => Console.WriteLine(s);

        t("Hello World");
    }
}
```

---

### 🔥 Output

```
Hello World
```

Explanation:

- `s` is parameter
    
- `Console.WriteLine(s)` is the expression
    
- No return value → so we use `Action`
    

---

# 🔵 4️⃣ Expression That Returns Value (Func)

If the expression evaluates to something, it returns it automatically.

---

## 🧪 Example 2 – Returning Value

```csharp
using System;

class Program
{
    static void Main()
    {
        Func<string, int> t2 = s => s.Length;

        int result = t2("Hello World");

        Console.WriteLine("Length: " + result);
    }
}
```

---

### 🔥 Output

```
Length: 11
```

Important:  
No `return` keyword needed.  
Because it's a single expression.

---

# 🟡 5️⃣ Statement Lambda (Multiple Lines)

If you need multiple statements:

- Use `{ }`
    
- Must use `return` if returning something
    

---

## 🧪 Example 3 – Multi-Line Lambda

```csharp
using System;

class Program
{
    static void Main()
    {
        Func<string, int> t3 = s =>
        {
            Console.WriteLine("Calculating length...");
            return s.Length;
        };

        int result = t3("Lambda");

        Console.WriteLine("Length: " + result);
    }
}
```

---

### 🔥 Output

```
Calculating length...
Length: 6
```

---

# 🧠 Key Differences

|Type|Syntax|Return Needed?|
|---|---|---|
|Expression Lambda|`s => s.Length`|❌ No|
|Statement Lambda|`s => { return s.Length; }`|✅ Yes|

---

# 🧠 6️⃣ Multiple Parameters

If more than one parameter, use parentheses:

---

## 🧪 Example 4

```csharp
using System;

class Program
{
    static void Main()
    {
        Func<int, int, int> add = (a, b) => a + b;

        Console.WriteLine(add(5, 3));
    }
}
```

---

### 🔥 Output

```
8
```

---

# 🧠 7️⃣ Even Shorter (Type Inference)

C# can infer types:

Instead of:

```csharp
Func<string, int> t = (string s) => s.Length;
```

You can write:

```csharp
Func<string, int> t = s => s.Length;
```

Cleaner and modern.

---

# 🧠 8️⃣ How This Connects to Delegates

This:

```csharp
Func<string, int> t = s => s.Length;
```

Is equivalent to:

```csharp
Func<string, int> t = delegate(string s)
{
    return s.Length;
};
```

Lambda is just shorter syntax.

---

# 🧠 9️⃣ Real-World Example (LINQ)

```csharp
int[] numbers = { 1, 2, 3, 4, 5 };

var result = numbers.Where(n => n > 3);
```

`n => n > 3` is a lambda.

It’s actually a:

```csharp
Func<int, bool>
```

---

# 🧠 10️⃣ Mental Model

Think of lambda like this:

Instead of writing:

```
Define method
Give it a name
Call it
```

You directly say:

```
Here is the logic → use it
```

Inline behavior injection.

---

# 🧠 Interview-Level Summary

✔ Lambda = anonymous method  
✔ Uses `=>` operator  
✔ Can be expression-based or statement-based  
✔ Works with delegates (`Action`, `Func`)  
✔ Automatically returns value in expression lambdas  
✔ Strongly used in LINQ & async programming

---

# 🚀 Final Big Picture

Evolution in C#:

```
Method → Delegate → Action/Func → Lambda
```

Each step makes code:

- Shorter
    
- Cleaner
    
- More powerful
    
- More flexible
    

---

