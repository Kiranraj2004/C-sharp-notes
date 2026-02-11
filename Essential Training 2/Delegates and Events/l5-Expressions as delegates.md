

Earlier we did this:

```csharp
PassMeWork(WriteHello);
```

That means:

- Pass a pointer to a method
    
- Method matches `Action<string>`
    

But instead of passing a method name…

We can pass the logic directly:

```csharp
PassMeWork(s => Console.WriteLine("Hello Expression " + s));
```

No separate method needed.

That lambda **is the delegate**.

---

# 🟢 2️⃣ Example – Action with Lambda

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
        DelegateSamples.PassMeWork(
            s => Console.WriteLine("Hello Expression " + s)
        );
    }
}
```

---

### 🔥 Output

```
Hello Expression Delegates
```

---

### 🧠 Why No Type Mentioned?

Because `PassMeWork` already says:

```csharp
Action<string>
```

So C# already knows:

- Parameter type is string
    
- No return value
    

That’s called **type inference**.

---

# 🔵 3️⃣ Func with Lambda (Returning Value)

Earlier we had:

```csharp
PassMeLogic(CalculateLength);
```

Instead of defining:

```csharp
static int CalculateLength(string s)
{
    return s.Length;
}
```

We can do:

```csharp
PassMeLogic(s => s.Length);
```

---

## 🧪 Example

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
        DelegateSamples.PassMeLogic(
            s => s.Length
        );
    }
}
```

---

### 🔥 Output

```
Function returned: 11
```

---

# 🟡 4️⃣ Statement-Based Lambda (Multiple Lines)

If you need multiple statements:

```csharp
DelegateSamples.PassMeLogic(
    s =>
    {
        Console.WriteLine("Input was: " + s);
        return s.Length;
    }
);
```

---

### 🔥 Output

```
Input was: Hello World
Function returned: 11
```

---

# 🧠 5️⃣ Important Rule: Signature Must Match

If method expects:

```csharp
Func<string, int>
```

Your lambda must:

- Take 1 string
    
- Return int
    

❌ Wrong:

```csharp
(s, x) => s.Length
```

Because that takes 2 parameters.

✔ Correct:

```csharp
s => s.Length
```

Always match the delegate signature.

---

# 🧠 6️⃣ Real Framework Example (Very Important)

The instructor mentioned this:

```csharp
AggregateException.Handle(...)
```

Signature of `Handle`:

```csharp
Func<Exception, bool>
```

So it expects:

- One Exception
    
- Returns bool
    

Example:

```csharp
catch (AggregateException ex)
{
    ex.Handle(inner => inner is JsonException);
}
```

This means:

- For each exception
    
- Return true if handled
    
- Return false if not handled
    

---

### Equivalent Long Version

Instead of lambda:

```csharp
bool HandleException(Exception inner)
{
    return inner is JsonException;
}

ex.Handle(HandleException);
```

Lambda avoids creating a full method.

Much cleaner.

---

# 🧠 7️⃣ Expression vs Statement Version

### Expression Lambda

```csharp
inner => inner is JsonException
```

No return keyword needed.

---

### Statement Lambda

```csharp
inner =>
{
    Console.WriteLine(inner.Message);
    return inner is JsonException;
}
```

Now return is required.

---

# 🧠 8️⃣ Why This Is Powerful

Because:

- You don’t pollute class with small one-time methods
    
- Logic stays close to where it's used
    
- Cleaner code
    
- Less boilerplate
    

This is heavily used in:

- LINQ
    
- ASP.NET middleware
    
- Tasks
    
- Exception handling
    
- Event handling
    

---

# 🧠 9️⃣ Mental Model

Old way:

```
Write method
Give it a name
Pass method
```

Modern way:

```
Just pass the logic directly
```

---

# 🚀 Final Clean Summary Notes

✔ Lambda = anonymous method  
✔ Can be passed directly as delegate  
✔ Works with Action & Func  
✔ No need to define separate method  
✔ Must match delegate signature  
✔ Expression lambda → no return keyword  
✔ Statement lambda → use return

---

# 🧠 Big Picture Flow

```
Delegate defines shape
Action / Func simplify delegate declaration
Lambda simplifies method creation
```

So now you can:

- Define delegate type automatically
    
- Skip method declaration
    
- Inject logic inline
    

That’s modern C#.

---

If you want next, I can explain:

🔥 Closures (VERY important interview topic)  
🔥 How lambdas capture variables  
🔥 Common lambda mistakes  
🔥 How this works internally (compiler magic)

You're now understanding real-world C# patterns, not just syntax 👌