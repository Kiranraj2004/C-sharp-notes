
# 🧠 1️⃣ Why Do We Need Action & Func?

Earlier we wrote:

```csharp
public delegate void MyDelegate(string input);
```

But think about it…

Every time we need:

- A method that takes 1 string
    
- Or 2 ints
    
- Or 3 parameters
    
- Or returns something
    

We would have to create a new delegate type.

That’s repetitive and unnecessary.

So C# gives us **generic delegates**:

✔ `Action`  
✔ `Func`

They save us from writing custom delegate types.

---

# 🟢 2️⃣ Action

### 👉 Used when:

- Method returns **void**
    
- Has 0–16 parameters
    

---

## 🔹 Syntax

```csharp
Action<T1, T2, ...>
```

Example:

```csharp
Action<string>
```

Means:

- Takes a string
    
- Returns void
    

---

## 🧪 Example – Action

### DelegateSamples.cs

```csharp
using System;

public static class DelegateSamples
{
    public static void PassMeWork(Action<string> work)
    {
        work("Delegates");
    }
}
```

---

### Program.cs

```csharp
using System;

class Program
{
    static void Main()
    {
        DelegateSamples.PassMeWork(WriteHello);
    }

    static void WriteHello(string message)
    {
        Console.WriteLine("Action says: " + message);
    }
}
```

---

## 🔥 Output

```
Action says: Delegates
```

---

### 🧠 What Happened?

Instead of:

```csharp
public delegate void MyDelegate(string input);
```

We simply used:

```csharp
Action<string>
```

Much cleaner.

---

# 🟢 3️⃣ Action with Multiple Parameters

```csharp
Action<string, int>
```

Means:

- Takes string
    
- Takes int
    
- Returns void
    

---

### Example

```csharp
public static void PassInfo(Action<string, int> worker)
{
    worker("Kiran", 21);
}
```

Usage:

```csharp
PassInfo(PrintDetails);

static void PrintDetails(string name, int age)
{
    Console.WriteLine($"Name: {name}, Age: {age}");
}
```

---

### 🔥 Output

```
Name: Kiran, Age: 21
```

---

# 🔵 4️⃣ Func – When You Want Return Value

### 👉 Used when:

- Method RETURNS something
    

---

## 🔹 Syntax

```csharp
Func<T1, T2, ..., TResult>
```

Very Important Rule:

👉 The **last type parameter is the return type**

Example:

```csharp
Func<string, int>
```

Means:

- Takes string
    
- Returns int
    

---

# 🧪 Example – Func

### DelegateSamples.cs

```csharp
using System;

public static class DelegateSamples
{
    public static void PassMeLogic(Func<string, int> worker)
    {
        int count = worker("Hello World");

        Console.WriteLine("Function returned: " + count);
    }
}
```

---

### Program.cs

```csharp
using System;

class Program
{
    static void Main()
    {
        DelegateSamples.PassMeLogic(CalculateLength);
    }

    static int CalculateLength(string input)
    {
        return input.Length;
    }
}
```

---

## 🔥 Output

```
Function returned: 11
```

Because `"Hello World"` has 11 characters.

---

# 🧠 What’s Happening?

`PassMeLogic` doesn’t know:

- What logic is being used
    
- How count is calculated
    
- What the function does
    

It just knows:

👉 “I will pass you a string, you give me an int.”

That’s abstraction and loose coupling.

---

# 🧠 5️⃣ Action vs Func Quick Comparison

|Feature|Action|Func|
|---|---|---|
|Returns value?|❌ No|✅ Yes|
|Parameters allowed|0–16|0–16|
|Last type parameter|N/A|Return type|

---

# 🧠 6️⃣ Modern Style (With Lambda 😎)

Instead of writing:

```csharp
DelegateSamples.PassMeLogic(CalculateLength);
```

You could write:

```csharp
DelegateSamples.PassMeLogic(s => s.Length);
```

Even shorter.

---

## Example

```csharp
DelegateSamples.PassMeLogic(s => s.Length * 2);
```

Now output:

```
Function returned: 22
```

Because:  
11 * 2 = 22

🔥 This is where LINQ magic comes from.

---

# 🧠 7️⃣ Real-Life Usage

Action & Func are used everywhere:

- LINQ
    
- ASP.NET middleware
    
- Task.Run()
    
- Event handling
    
- Sorting custom logic
    
- Dependency injection
    
- Callbacks
    

Example in LINQ:

```csharp
numbers.Where(n => n > 5);
```

That lambda is a `Func<int, bool>`.

---

# 🧠 Final Clean Summary Notes (Save This)

✔ `Action<T>` → void return  
✔ `Func<T, TResult>` → returns value  
✔ Last generic type in Func = return type  
✔ Can accept up to 16 parameters  
✔ Replaces need to define custom delegates  
✔ Makes code shorter & reusable

---

# 🚀 Mental Model

Think of it like this:

```
Action = "Do something"
Func   = "Do something and give me result"
```

---

