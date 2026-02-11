
# 🔹 1. What is Throwing an Exception?

When your code detects a problem, you can manually raise an exception using:

```csharp
throw new ExceptionType("message");
```

This immediately:
- Stops execution
- Sends exception up the call stack
- Must be caught somewhere

---

# 🔹 2. Example Method That Throws Exceptions

```csharp
public static void ThrowExceptions(bool? shouldThrow)
{
    if (!shouldThrow.HasValue)
    {
        throw new ArgumentNullException(nameof(shouldThrow));
    }

    if (shouldThrow.Value)
    {
        throw new Exception("I was told to throw this!");
    }

    Console.WriteLine("No exceptions being thrown here.");
}
```

---

# 🔹 3. Understanding the Logic

### Case 1: `shouldThrow == null`
→ Throw `ArgumentNullException`

Why use this?
Because it is **more specific** than ArgumentException.

---

### Case 2: `shouldThrow == true`
→ Throw generic Exception (not recommended in real projects)

---

### Case 3: `shouldThrow == false`
→ Normal execution

---

# 🔹 4. Calling Method with try-catch

```csharp
try
{
    ThrowExceptions(null);
}
catch (Exception ex)
{
    Console.WriteLine("Caught Exception:");
    Console.WriteLine(ex);
}
```

---

# 🔥 OUTPUT 1: Passing null

```
Caught Exception:
System.ArgumentNullException: Value cannot be null. (Parameter 'shouldThrow')
   at ExceptionSamples.ThrowExceptions(Boolean? shouldThrow) in ExceptionSamples.cs:line 10
   at Program.Main() in Program.cs:line 6
```

Notice:
- Shows where exception started
- Shows where it was caught

That is called:

# 🔹 Stack Trace

Stack trace shows:
- Where exception originated
- How it propagated
- Where it was handled

---

# 🔥 OUTPUT 2: Passing true

```csharp
ThrowExceptions(true);
```

Output:

```
Caught Exception:
System.Exception: I was told to throw this!
   at ExceptionSamples.ThrowExceptions(Boolean? shouldThrow) in ExceptionSamples.cs:line 15
   at Program.Main() in Program.cs:line 6
```

---

# 🔹 5. What is Rethrowing?

Sometimes you catch an exception, but you don’t want to fully handle it.

You want:
- Maybe log it
- Then pass it upward

There are TWO ways.

This is VERY important.

---

# 🔹 6. Correct Way to Rethrow

```csharp
catch (Exception ex)
{
    Console.WriteLine("Logging exception...");
    throw;
}
```

Notice:
```
throw;
```
NO variable.

This preserves:
- Original stack trace
- Original location

---

## 🔥 Output (Unhandled Exception)

```
Unhandled exception. System.Exception: I was told to throw this!
   at ExceptionSamples.ThrowExceptions(Boolean? shouldThrow) in ExceptionSamples.cs:line 15
   at Program.Main() in Program.cs:line 6
```

Stack trace is intact ✅

---

# 🔹 7. WRONG Way to Rethrow

```csharp
catch (Exception ex)
{
    throw ex;
}
```

This resets stack trace ❌

---

## 🔥 Output

```
Unhandled exception. System.Exception: I was told to throw this!
   at Program.Main() in Program.cs:line 12
```

Notice:
- Original source line lost
- Looks like exception started here
- Debugging becomes harder

---

# 🔥 Interview Gold Concept

### Difference Between:

```
throw;
```

and

```
throw ex;
```

| throw; | throw ex; |
|---------|-----------|
| Preserves original stack trace | Resets stack trace |
| Recommended | Not recommended |
| Keeps debugging info | Loses origin |

---

# 🔹 8. What is Exception Propagation?

If you don’t catch an exception:
- It moves upward
- If no one catches it → application crashes

That’s called:
```
Unhandled Exception
```

---

# 🔹 9. Realistic Example (Full Code)

```csharp
class Program
{
    static void Main()
    {
        try
        {
            ThrowExceptions(true);
        }
        catch (Exception ex)
        {
            Console.WriteLine("Logging exception...");
            throw; // try changing to throw ex;
        }
    }

    static void ThrowExceptions(bool? shouldThrow)
    {
        if (!shouldThrow.HasValue)
            throw new ArgumentNullException(nameof(shouldThrow));

        if (shouldThrow.Value)
            throw new Exception("I was told to throw this!");

        Console.WriteLine("No exception.");
    }
}
```

---

# 🔹 11. Visual Flow

```
ThrowExceptions()
    ↓
Exception occurs
    ↓
Caught in Main
    ↓
Rethrow
    ↓
Application crashes (if not handled above)
```

