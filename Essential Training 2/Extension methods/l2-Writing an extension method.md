
# 🔹 What Changed?

Originally we had:

```csharp
public static string Right(string input, int numChars)
```

Now we change it to:

```csharp
public static string Right(this string input, int numChars)
```

That’s it. Just adding `this` before `string`.

And boom 💥 it becomes an extension method.

---

# 🔹 What Does `this` Actually Do?

When we write:

```csharp
this string input
```

We are telling C#:

👉 “Attach this method to the string type.”

So now every string can call `.Right()`.

---

# 🔹 Very Important Concept (From Transcript)

The instructor says something very important:

> You don’t get internal access.  
> You don’t change how string works internally.  
> You just change how the method is accessed.

Meaning:

Inside the extension method, you only have access to:

- Public properties
    
- Public methods
    

You CANNOT:

- Access private fields
    
- Modify internal behavior
    
- Change how string works internally
    

You are just adding a new helper method.

---

# 🔹 Think of It Like This

Extension method is like:

You're adding a utility tool to an object,  
not opening the engine of the object.

You are NOT modifying `string`.  
You are decorating it.

---

# 🔹 Full Example (Final Version)

### StringExtensions.cs

```csharp
using System;

namespace Essentials2.Library.Extensions
{
    public static class StringExtensions
    {
        public static string Right(this string input, int numChars)
        {
            if (string.IsNullOrEmpty(input))
                return string.Empty;

            if (numChars > input.Length)
                return input;

            return input.Substring(input.Length - numChars);
        }
    }
}
```

---

# 🔹 Using It in Program.cs

```csharp
using System;
using Essentials2.Library.Extensions;

class Program
{
    static void Main()
    {
        string s = "right four";

        string result = s.Right(4);

        Console.WriteLine(result);
    }
}
```

---

# ✅ Output

```
four
```

---

# 🔹 What Actually Happens Behind the Scenes?

When you write:

```csharp
s.Right(4);
```

Compiler converts it to:

```csharp
StringExtensions.Right(s, 4);
```

So extension methods are just **syntactic sugar**.

---

# 🔹 Important Clarification From Transcript

Inside this method:

```csharp
public static string Right(this string input, int numChars)
```

You still only have normal string capabilities:

```csharp
input.Length
input.Substring()
string.IsNullOrEmpty()
```

You do NOT get:

- Internal fields
    
- Hidden properties
    
- Extra power
    

You’re working exactly like before.

Only difference?

👉 The consumer experience is better.

---

# 🔹 Why This Is Powerful

Without extension methods:

```csharp
StringExtensions.Right(s, 4);
```

With extension methods:

```csharp
s.Right(4);
```

Second one:  
✔ Cleaner  
✔ More readable  
✔ Looks natural  
✔ Feels built-in

This simplifies the programming model.

---

# 🔹 Another Simple Example

Let’s create an extension method that counts vowels.

```csharp
public static class StringExtensions
{
    public static int CountVowels(this string input)
    {
        if (string.IsNullOrEmpty(input))
            return 0;

        int count = 0;

        foreach (char c in input.ToLower())
        {
            if ("aeiou".Contains(c))
                count++;
        }

        return count;
    }
}
```

---

### Usage

```csharp
string name = "Kiran";
Console.WriteLine(name.CountVowels());
```

---

### ✅ Output

```
2
```

Feels like a real string method again 😎

---

# 🔹 Key Interview Notes

Extension Method:

• Static method  
• Inside static class  
• First parameter uses `this`  
• Does NOT modify original class  
• Does NOT give internal access  
• Improves readability and usability

---

# 🔥 One Important Thing

Extension methods are resolved at compile time.

If the original class later defines a method with the same name,  
that original method will take priority.

---

# l3


# 🔹 What Happened in the Transcript?

You created the extension method:

```csharp
public static string Right(this string input, int numChars)
```

Then you tried to use it like this:

```csharp
string s = "right four";
var result = s.Right(4);
```

But ❌ you got a **red squiggly line**.

Why?

Because the **namespace was not in scope**.

---

# 🔥 Core Concept: Namespace Must Be In Scope

Even though you created the extension method,  
C# will not recognize it unless the namespace is imported.

Remember:

Your extension class was inside:

```csharp
namespace Essentials2.Library.Extensions
```

So in your program file, you MUST add:

```csharp
using Essentials2.Library.Extensions;
```

If you don’t…

👉 The compiler doesn’t know that `Right()` exists.

---

# 🔹 Why This Happens

Extension methods are:

- Static methods
    
- Inside static classes
    
- Found via namespace resolution
    

If the namespace is not imported,  
C# cannot “attach” that method to the type.

This is why sometimes:

You copy code from documentation  
You see a method  
But it doesn’t work

Because you're missing a `using` statement.

---

# 🔹 Step-by-Step Example

## 1️⃣ Extension Method File

### StringExtensions.cs

```csharp
using System;

namespace Essentials2.Library.Extensions
{
    public static class StringExtensions
    {
        public static string Right(this string input, int numChars)
        {
            if (string.IsNullOrEmpty(input))
                return string.Empty;

            if (numChars > input.Length)
                return input;

            return input.Substring(input.Length - numChars);
        }
    }
}
```

---

## 2️⃣ Program File (Without Using)

```csharp
using System;

class Program
{
    static void Main()
    {
        string s = "right four";
        var result = s.Right(4); // ❌ Red squiggly
    }
}
```

Error:

```
'string' does not contain a definition for 'Right'
```

---

## 3️⃣ Fix: Add Using Statement

```csharp
using System;
using Essentials2.Library.Extensions;  // 🔥 This fixes it

class Program
{
    static void Main()
    {
        string s = "right four";

        var four = s.Right(4);
        var five = s.Right(5);

        Console.WriteLine(four);
        Console.WriteLine(five);
    }
}
```

---

# ✅ Output

```
four
 four
```

Notice carefully:

- `"right four"` → Right(4) → `"four"`
    
- `"right four"` → Right(5) → `" four"`
    

The space is included 😎

---

# 🔹 Why This Is Powerful (From Transcript)

Now think practically.

Before extension method, you would write this everywhere:

```csharp
if (!string.IsNullOrEmpty(s) && s.Length >= 4)
{
    var result = s.Substring(s.Length - 4);
}
```

And repeat it in:

- File 1
    
- File 2
    
- File 3
    
- File 20
    

That’s duplication.

Now with extension method:

```csharp
var result = s.Right(4);
```

All logic is centralized.

---

# 🔥 Big Advantage: Encapsulation

If tomorrow you realize:

“Oh no 😬 we need more error checking.”

You modify ONE place:

```csharp
StringExtensions.cs
```

And it fixes everywhere in your project.

No duplication.  
No maintenance headache.

---

# 🔹 Why Libraries Often Use Extension Methods

Framework example:

```csharp
numbers.Where(x => x > 5);
```

`Where()` is not part of List originally.

It is an extension method in:

```csharp
System.Linq
```

If you forget:

```csharp
using System.Linq;
```

You’ll get red squiggly again.

---

# 🔹 Key Concepts From This Transcript

1. Extension methods must be in namespace scope.
    
2. If namespace not imported → method won’t appear.
    
3. They simplify programming model.
    
4. They reduce code duplication.
    
5. They centralize logic in one place.
    
6. They are heavily used in frameworks like LINQ.
    

---


