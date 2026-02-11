
# 🔹 1. Why Create Custom Exceptions?

Instead of this:

```csharp
throw new Exception("Something went wrong");
```

We create:

```csharp
throw new InvalidOptionException("Invalid menu option selected");
```

Why?

Because:

- More descriptive
    
- Easier to catch specifically
    
- Cleaner logging
    
- Better API design
    
- More readable stack traces
    

---

# 🔹 2. Creating a Basic Custom Exception

## Step 1: Create a Class

```csharp
using System;

public class InvalidOptionException : Exception
{
    public InvalidOptionException(string message)
        : base(message)
    {
    }
}
```

What’s happening?

- We inherit from `Exception`
    
- We pass message to base class
    

---

# 🔹 3. Using Custom Exception

Replace:

```csharp
throw new Exception("I was told to throw this!");
```

With:

```csharp
throw new InvalidOptionException("I was told to throw this!");
```

---

# 🔥 Example Program

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
            Console.WriteLine("Caught Exception:");
            Console.WriteLine(ex);
        }
    }

    static void ThrowExceptions(bool? shouldThrow)
    {
        if (!shouldThrow.HasValue)
            throw new ArgumentNullException(nameof(shouldThrow));

        if (shouldThrow.Value)
            throw new InvalidOptionException("I was told to throw this!");

        Console.WriteLine("No exceptions thrown.");
    }
}
```

---

# 🔥 OUTPUT

```
Caught Exception:
InvalidOptionException: I was told to throw this!
   at Program.ThrowExceptions(Boolean? shouldThrow) line 15
   at Program.Main() line 6
```

Now the exception type is clear:  
✔ InvalidOptionException  
Instead of generic Exception.

---

# 🔹 4. Best Practice Version (Full Professional Setup)

When creating custom exceptions, follow Microsoft guidelines.

You should add:

1️⃣ Default constructor  
2️⃣ Constructor with message  
3️⃣ Constructor with message + inner exception  
4️⃣ Serialization constructor  
5️⃣ [Serializable] attribute

---

# 🔥 Full Proper Custom Exception

```csharp
using System;
using System.Runtime.Serialization;

[Serializable]
public class InvalidOptionException : Exception
{
    public InvalidOptionException()
    {
    }

    public InvalidOptionException(string message)
        : base(message)
    {
    }

    public InvalidOptionException(string message, Exception innerException)
        : base(message, innerException)
    {
    }

    protected InvalidOptionException(SerializationInfo info,
                                     StreamingContext context)
        : base(info, context)
    {
    }
}
```

---

# 🔹 5. Why These Constructors?

### 1️⃣ Default Constructor

Used when no message needed.

---

### 2️⃣ Message Constructor

Most common usage.

---

### 3️⃣ Message + Inner Exception

Used when wrapping another exception.

Example:

```csharp
catch (Exception ex)
{
    throw new InvalidOptionException(
        "Error while processing option.",
        ex);
}
```

This preserves:

- Original exception
    
- Stack trace
    
- Context
    

---

### 4️⃣ Serialization Constructor

Needed when:

- Sending exception over network
    
- Logging frameworks
    
- Distributed systems
    
- Remoting scenarios
    

---

# 🔹 6. Wrapping Exceptions (Very Important Concept)

Instead of:

```csharp
catch (Exception ex)
{
    throw ex;   // ❌ loses stack trace
}
```

Better:

```csharp
catch (Exception ex)
{
    throw new ApplicationException("App level failure", ex);
}
```

This:

- Creates new exception
    
- Keeps original inside InnerException
    
- Adds context
    

---

# 🔥 Example of Wrapping

```csharp
try
{
    ThrowExceptions(true);
}
catch (InvalidOptionException ex)
{
    throw new ApplicationException("App exception occurred.", ex);
}
```

---

# 🔥 OUTPUT

```
Unhandled exception. System.ApplicationException: App exception occurred.
 ---> InvalidOptionException: I was told to throw this!
     at Program.ThrowExceptions(Boolean? shouldThrow) line 15
     at Program.Main() line 6
```

Notice:

- Outer exception: ApplicationException
    
- Inner exception: InvalidOptionException
    
- Stack trace preserved
    

---

# 🔹 7. Inner Exception Concept

Exception structure becomes:

```
ApplicationException
   |
   ---> InnerException = InvalidOptionException
           |
           ---> Original message + stack trace
```

So you don’t lose original problem.

---

# 🔹 8. Why Serialization Attribute?

```csharp
[Serializable]
```

This allows:

- .NET runtime to serialize the exception
    
- Sending over network
    
- Writing to file
    
- Remoting scenarios
    

Without it → may cause runtime issues in distributed apps.

---

