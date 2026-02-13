
# ✅ What is a Delegate in C#?

👉 A **delegate** is a type that represents a reference to a method.

Think of it like:

- 🔹 A function pointer (like in C/C++)
    
- 🔹 A callback (like in JavaScript)
    
- 🔹 A variable that can store a method
    

---

# ✅ Why Do We Need Delegates?

Delegates allow us to:

- Pass methods as parameters
    
- Change method behavior at runtime
    
- Implement callback functionality
    
- Build event-driven programming
    

---

# ✅ Syntax of a Delegate

```csharp
public delegate ReturnType DelegateName(ParameterList);
```

Example:

```csharp
public delegate string MyDelegate(int arg1, int arg2);
```

This means:

- Delegate returns a **string**
    
- Takes **two integers**
    
- Can reference any method with this exact signature
    

---

# ✅ Important Rule (Type Safety)

The method assigned to a delegate must:

✔ Have the same return type  
✔ Have same number of parameters  
✔ Have same parameter types

Otherwise, compiler error ❌

---

# ✅ Step-by-Step Example (Static Methods)

### Step 1: Define Delegate

```csharp
public delegate string MyDelegate(int arg1, int arg2);
```

---

### Step 2: Create Matching Methods

```csharp
public static string Add(int a, int b)
{
    return (a + b).ToString();
}

public static string Multiply(int a, int b)
{
    return (a * b).ToString();
}
```

---

### Step 3: Use Delegate in Main()

```csharp
class Program
{
    public delegate string MyDelegate(int arg1, int arg2);

    public static string Add(int a, int b)
    {
        return (a + b).ToString();
    }

    public static string Multiply(int a, int b)
    {
        return (a * b).ToString();
    }

    static void Main(string[] args)
    {
        MyDelegate f;

        // Assign Add method
        f = Add;
        Console.WriteLine("Result from Add: " + f(10, 20));

        // Reassign Multiply method
        f = Multiply;
        Console.WriteLine("Result from Multiply: " + f(10, 20));
    }
}
```

---

# ✅ Output

```
Result from Add: 30
Result from Multiply: 200
```

---

# 🎯 Key Understanding

Even though we call:

```csharp
f(10, 20);
```

The actual method executed depends on what `f` currently refers to.

So delegate allows **switching behavior at runtime** 🔥

---

# ✅ Using Delegate with Instance Methods

Delegates can also point to non-static (instance) methods.

---

### Example with Instance Method

```csharp
class MyClass
{
    public string Subtract(int a, int b)
    {
        return (a - b).ToString();
    }
}

class Program
{
    public delegate string MyDelegate(int arg1, int arg2);

    static void Main(string[] args)
    {
        MyClass obj = new MyClass();

        MyDelegate f;

        // Assign instance method
        f = obj.Subtract;

        Console.WriteLine("Result from Subtract: " + f(20, 10));
    }
}
```

---

# ✅ Output

```
Result from Subtract: 10
```

---

# 🧠 What’s Happening Internally?

When we do:

```csharp
f = Add;
```

We are storing the **reference of the method** inside `f`.

Then:

```csharp
f(10, 20);
```

Actually calls:

```csharp
Add(10, 20);
```

---

# ✅ Real-World Use Case

Delegates are heavily used in:

- Events
    
- Button click handlers
    
- Sorting logic
    
- LINQ
    
- Asynchronous programming
    
- Callbacks
    

Example: Passing method as parameter

```csharp
static void Calculate(int a, int b, MyDelegate operation)
{
    Console.WriteLine("Result: " + operation(a, b));
}
```

Call it like:

```csharp
Calculate(5, 3, Add);
Calculate(5, 3, Multiply);
```

---


# 🔥 Bonus: Modern Shortcut (Using Func)

Instead of creating custom delegate:

```csharp
Func<int, int, string> f = Add;
```

`Func<parameters, returnType>`

---

# 🚀 Quick Summary

|Feature|Delegate|
|---|---|
|Stores method reference|✅|
|Type safe|✅|
|Can change method at runtime|✅|
|Works with static methods|✅|
|Works with instance methods|✅|

---

