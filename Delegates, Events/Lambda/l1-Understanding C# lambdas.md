
# ✅ 1. What is a Lambda Expression?

A **Lambda expression** is a shorter way of writing an anonymous function.

👉 Lambdas are based on **delegates**  
👉 They can be used anywhere a delegate is used

Think of it like:

Anonymous delegate:

```csharp
delegate(int x) { return x * x; }
```

Lambda:

```csharp
x => x * x
```

Cleaner ✅  
Shorter ✅  
Modern C# style ✅

---

# ✅ 2. Lambda Syntax

Basic form:

```csharp
(parameters) => expression
```

OR

```csharp
(parameters) => 
{
    // multiple statements
}
```

The `=>` is called the **lambda operator**.

---

# ✅ 3. Expression Lambda vs Statement Lambda

### 🔹 Expression Lambda

Single expression  
No curly braces  
Automatically returns value

Example:

```csharp
x => x * x
```

---

### 🔹 Statement Lambda

Multiple statements  
Uses `{ }`  
Must use `return` if returning value

Example:

```csharp
(x, y) =>
{
    int result = x + y;
    return result;
}
```

---

# ✅ 4. Full Working Examples

---

## 🔹 Example 1 — Single Argument Lambda

### Delegate Definition

```csharp
public delegate int MyDelegate(int x);
```

### Code

```csharp
using System;

class Program
{
    public delegate int MyDelegate(int x);

    static void Main(string[] args)
    {
        MyDelegate d1 = x => x * x;

        Console.WriteLine("Square of 5: " + d1(5));

        // Change delegate at runtime
        d1 = x => x * 10;

        Console.WriteLine("5 times 10: " + d1(5));
    }
}
```

---

### ✅ Output

```
Square of 5: 25
5 times 10: 50
```

Notice:  
We changed the delegate dynamically 🔥

---

## 🔹 Example 2 — Two Argument Statement Lambda

### Delegate Definition

```csharp
public delegate void MyDelegate2(int x, string y);
```

### Code

```csharp
public delegate void MyDelegate2(int x, string y);

class Program
{
    static void Main(string[] args)
    {
        MyDelegate2 d2 = (x, y) =>
        {
            Console.WriteLine("Two-arg Lambda:");
            Console.WriteLine("Number * 10: " + (x * 10));
            Console.WriteLine("String: " + y);
        };

        d2(25, "Hello Lambda");
    }
}
```

---

### ✅ Output

```
Two-arg Lambda:
Number * 10: 250
String: Hello Lambda
```

This is a **statement lambda** because it has multiple statements.

---

## 🔹 Example 3 — Boolean Expression Lambda

### Delegate Definition

```csharp
public delegate bool MyDelegate3(int x);
```

### Code

```csharp
public delegate bool MyDelegate3(int x);

class Program
{
    static void Main(string[] args)
    {
        MyDelegate3 d3 = x => x > 10;

        Console.WriteLine("Is 5 > 10? " + d3(5));
        Console.WriteLine("Is 15 > 10? " + d3(15));
    }
}
```

---

### ✅ Output

```
Is 5 > 10? False
Is 15 > 10? True
```

---

# ✅ 5. Lambda With No Arguments

If no parameters:

```csharp
Action d = () => Console.WriteLine("Hello");
d();
```

---

# ✅ 6. Parentheses Rules

|Case|Parentheses Required?|
|---|---|
|One parameter|Optional|
|Multiple parameters|Required|
|No parameters|Required|

Example:

```csharp
x => x * x          // OK
(x) => x * x        // Also OK
(x, y) => x + y     // Required
() => Console.WriteLine("Hi") // Required
```

---

# ✅ 7. Why Lambdas Are Important

They are used in:

✔ LINQ  
✔ Event handlers  
✔ Threading  
✔ Sorting  
✔ Filtering collections

Example:

```csharp
button.Click += (sender, e) => 
{
    Console.WriteLine("Button clicked");
};
```

---

# ✅ 8. Modern Shortcut Using Func

Instead of custom delegate:

```csharp
public delegate int MyDelegate(int x);
```

We use:

```csharp
Func<int, int> d1 = x => x * x;
```

`Func<input, returnType>`

---

# ✅ 9. Comparison

|Feature|Anonymous Delegate|Lambda|
|---|---|---|
|Shorter|❌|✅|
|Cleaner|❌|✅|
|Modern C#|❌|✅|
|Preferred today|❌|✅|

---

