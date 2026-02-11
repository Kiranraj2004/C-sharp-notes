
# 🧠 1. What is a Delegate?

### 👉 Simple Definition

A **delegate** is a **type that holds a reference (pointer) to a method**.

It allows you to:

- Pass methods as parameters
    
- Store methods in variables
    
- Call methods indirectly
    
- Create callbacks
    

---

# 🔹 2. Basic Concept – Method Pointer

Suppose we have a method:

```csharp
static void WriteHello(string name)
{
    Console.WriteLine($"Hello {name}");
}
```

Instead of calling it directly:

```csharp
WriteHello("Kiran");
```

We can point to it using a delegate.

---

# 🔹 3. Using Built-in Delegate Type (`Delegate`)

### Step 1: Assign method to delegate variable

```csharp
Delegate del = (Action<string>)WriteHello;
```

⚠ Important:

- No parentheses → we are pointing to method
    
- If you write `WriteHello("Kiran")`, you are calling it
    
- If you write `WriteHello`, you are referencing it
    

---

### Step 2: Invoke it dynamically

```csharp
del.DynamicInvoke("Kiran");
```

### 🔥 Output:

```
Hello Kiran
```

---

# 🔹 4. Creating Your Own Delegate Type

Now let’s create a custom delegate type.

### In a separate class:

```csharp
public static class DelegateSamples
{
    // Delegate declaration
    public delegate void Del(string input);

    public static void PassMeWork(Del work)
    {
        // Invoke the delegate
        work("Delegates");
    }
}
```

---

# 🔹 5. Using It in Program.cs

```csharp
class Program
{
    static void Main(string[] args)
    {
        WriteHello("Kiran");

        DelegateSamples.PassMeWork(WriteHello);
    }

    static void WriteHello(string name)
    {
        Console.WriteLine($"Hello {name}");
    }
}
```

---

# 🔥 Final Output

```
Hello Kiran
Hello Delegates
```

---

# 🧠 What Actually Happened?

Let’s understand clearly:

### Step-by-step Flow:

1. `WriteHello("Kiran")`  
    → Direct method call
    
2. `DelegateSamples.PassMeWork(WriteHello)`  
    → We pass method as parameter
    
3. Inside `PassMeWork`  
    → `work("Delegates")`  
    → That calls `WriteHello("Delegates")`
    

---

# 🧠 Why Is This Powerful?

Because now your method can accept ANY function that matches the signature.

Example:

```csharp
static void WriteGoodbye(string name)
{
    Console.WriteLine($"Goodbye {name}");
}
```

Now this works too:

```csharp
DelegateSamples.PassMeWork(WriteGoodbye);
```

### 🔥 Output:

```
Goodbye Delegates
```

Same function.  
Different behavior.  
That’s flexibility.

---

# 📌 Important Concepts

### 1️⃣ Delegate Declaration Syntax

```csharp
public delegate ReturnType DelegateName(ParameterType param);
```

Example:

```csharp
public delegate void Del(string input);
```

---

### 2️⃣ Signature Must Match

If delegate is:

```csharp
public delegate void Del(string input);
```

Then method must:

- Return void
    
- Accept one string parameter
    

Otherwise ❌ compiler error.

---

# 🎯 Real-Life Use Case

Imagine:

- You are writing a payment system.
    
- After payment completes, you want to:
    
    - Send email
        
    - Log transaction
        
    - Show success message
        

Instead of hardcoding, you accept a delegate:

```csharp
ProcessPayment(Action<string> onComplete)
```

Now caller decides what happens after payment.

That’s clean design.

---

# 🔥 Cleaner Modern Way (Recommended)

Instead of creating custom delegate types, C# provides built-in ones:

### `Action<T>`

For methods that return void.

```csharp
public static void PassMeWork(Action<string> work)
{
    work("Delegates");
}
```

Now no need for:

```csharp
public delegate void Del(string input);
```

---

# 🎯 Final Clean Version (Modern Style)

```csharp
using System;

class Program
{
    static void Main()
    {
        WriteHello("Kiran");

        PassMeWork(WriteHello);
        PassMeWork(WriteGoodbye);
    }

    static void WriteHello(string name)
    {
        Console.WriteLine($"Hello {name}");
    }

    static void WriteGoodbye(string name)
    {
        Console.WriteLine($"Goodbye {name}");
    }

    static void PassMeWork(Action<string> work)
    {
        work("Delegates");
    }
}
```

---

# 🔥 Output

```
Hello Kiran
Hello Delegates
Goodbye Delegates
```

---


# q1

# 🧠 1️⃣ Custom Delegate with Multiple Parameters

Suppose we have this method:

```csharp
static void PrintDetails(string name, int age)
{
    Console.WriteLine($"Name: {name}, Age: {age}");
}
```

Now we create a delegate that matches this signature:

```csharp
public delegate void MyDelegate(string name, int age);
```

Notice:

- Two parameters
    
- `string`
    
- `int`
    
- Returns `void`
    

---

## 🔹 Using It

```csharp
class Program
{
    public delegate void MyDelegate(string name, int age);

    static void Main()
    {
        MyDelegate del = PrintDetails;

        del("Kiran", 21);
    }

    static void PrintDetails(string name, int age)
    {
        Console.WriteLine($"Name: {name}, Age: {age}");
    }
}
```

---

### 🔥 Output

```
Name: Kiran, Age: 21
```

---

# 🧠 2️⃣ Passing Delegate with Multiple Params to Another Method

Let’s make it more realistic.

```csharp
class Program
{
    public delegate void MyDelegate(string name, int age);

    static void Main()
    {
        PassWork(PrintDetails);
    }

    static void PassWork(MyDelegate work)
    {
        work("Kiran", 21);
    }

    static void PrintDetails(string name, int age)
    {
        Console.WriteLine($"Name: {name}, Age: {age}");
    }
}
```

---

### 🔥 Output

```
Name: Kiran, Age: 21
```

Flow:

- `PassWork` receives a method reference
    
- It invokes it with 2 parameters
    

---

# 🧠 3️⃣ Modern Way (Using Action)

Instead of declaring:

```csharp
public delegate void MyDelegate(string name, int age);
```

You can use:

```csharp
Action<string, int>
```

Because:

- `Action` = returns void
    
- `<string, int>` = parameter types
    

---

### Clean Modern Version

```csharp
class Program
{
    static void Main()
    {
        PassWork(PrintDetails);
    }

    static void PassWork(Action<string, int> work)
    {
        work("Kiran", 21);
    }

    static void PrintDetails(string name, int age)
    {
        Console.WriteLine($"Name: {name}, Age: {age}");
    }
}
```

Same output. Cleaner code.

---

# 🧠 4️⃣ What If It Returns Something?

If method returns something, use `Func`.

Example:

```csharp
static int Add(int a, int b)
{
    return a + b;
}
```

Delegate:

```csharp
Func<int, int, int>
```

Format of Func:

```
Func<param1, param2, ..., returnType>
```

---

### Example

```csharp
class Program
{
    static void Main()
    {
        int result = Calculate(Add);
        Console.WriteLine(result);
    }

    static int Calculate(Func<int, int, int> operation)
    {
        return operation(5, 3);
    }

    static int Add(int a, int b)
    {
        return a + b;
    }
}
```

---

### 🔥 Output

```
8
```

---

# 🧠 Important Rule (Very Important for Interviews)

Delegate signature must exactly match:

✔ Same number of parameters  
✔ Same parameter types  
✔ Same return type

Otherwise → ❌ compile-time error

---

# 🚀 Quick Summary

|Situation|Use|
|---|---|
|Returns void|`Action<T1, T2>`|
|Returns value|`Func<T1, T2, TResult>`|
|No parameters|`Action` or `Func<TResult>`|

---

