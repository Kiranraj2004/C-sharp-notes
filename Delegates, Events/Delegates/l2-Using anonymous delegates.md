
# ✅ What is an Anonymous Delegate?

An **anonymous delegate** is a delegate **without a method name**.

Instead of:

```csharp
f = Add;
```

We directly write the method implementation inline.

Think of it like:

- Writing a function without naming it
    
- Creating the method at the same place where it is used
    
- A quick one-time function
    

---

# ✅ Why Use Anonymous Delegates?

Use them when:

✔ The method is small  
✔ The method is used only once  
✔ You don’t want to clutter code with extra method names  
✔ You want better readability

---

# ✅ Normal Delegate vs Anonymous Delegate

### 🔹 Normal Way (Two Steps)

```csharp
public static string Add(int a, int b)
{
    return (a + b).ToString();
}

MyDelegate f = Add;
```

---

### 🔹 Anonymous Way (One Step)

```csharp
MyDelegate f = delegate(int a, int b)
{
    return (a + b).ToString();
};
```

Same functionality ✅  
Less code 🔥

---

# ✅ Basic Syntax

```csharp
DelegateType variableName = delegate(parameters)
{
    // method body
};
```

---

# ✅ Full Example (From Transcript Style)

### Step 1: Declare Delegate Type

```csharp
public delegate string MyDelegate(int arg1, int arg2);
```

---

### Step 2: Use Anonymous Delegate in Main()

```csharp
using System;

class Program
{
    public delegate string MyDelegate(int arg1, int arg2);

    static void Main(string[] args)
    {
        MyDelegate f = delegate(int arg1, int arg2)
        {
            return (arg1 + arg2).ToString();
        };

        Console.WriteLine("Result: " + f(10, 20));
    }
}
```

---

# ✅ Output

```
Result: 30
```

---

# ✅ More Examples

---

## 🔹 Example 1: Multiply Using Anonymous Delegate

```csharp
MyDelegate multiply = delegate(int a, int b)
{
    return (a * b).ToString();
};

Console.WriteLine("Multiply Result: " + multiply(10, 5));
```

### Output

```
Multiply Result: 50
```

---

## 🔹 Example 2: Passing Anonymous Delegate as Parameter

```csharp
static void Calculate(int a, int b, MyDelegate operation)
{
    Console.WriteLine("Result: " + operation(a, b));
}

static void Main()
{
    Calculate(5, 3, delegate(int x, int y)
    {
        return (x - y).ToString();
    });
}
```

### Output

```
Result: 2
```

🔥 Notice: We didn’t even create a variable.  
We directly passed the anonymous delegate.

---

# ✅ How It Works Internally

When you write:

```csharp
MyDelegate f = delegate(int a, int b) { return ... };
```

Compiler:

1. Creates a hidden method
    
2. Stores its reference in `f`
    
3. Allows calling it like normal function
    

---

# ✅ Where You’ll See This in Real Projects

Anonymous delegates are often used in:

- Button click events
    
- Timers
    
- Threading
    
- Sorting
    
- Callbacks
    

Example (event-style usage):

```csharp
button.Click += delegate(object sender, EventArgs e)
{
    Console.WriteLine("Button clicked!");
};
```

(You’ll see this more when learning Events.)

---

# ✅ Important: Anonymous Delegate vs Lambda Expression

Anonymous delegate:

```csharp
delegate(int a, int b) { return a + b; }
```

Lambda expression (modern way):

```csharp
(a, b) => (a + b).ToString();
```

Lambda is shorter and preferred today ✅


---

# ✅ Quick Comparison Table

|Feature|Normal Delegate|Anonymous Delegate|
|---|---|---|
|Has method name|✅|❌|
|Defined separately|✅|❌|
|Written inline|❌|✅|
|Good for small logic|❌|✅|

---

