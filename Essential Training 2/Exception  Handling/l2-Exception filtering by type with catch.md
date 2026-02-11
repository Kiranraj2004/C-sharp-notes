
# 🔹 1. Why Do We Need Multiple catch Blocks?

In the previous example we used:

```csharp
catch (Exception ex)
```

That catches **everything**.

But the problem is:
- We don’t know *what kind* of error happened.
- File issue?  
- JSON issue?  
- Something else?

So instead, we catch **specific exception types**.

---

# 🔹 2. Exception Hierarchy Concept (Very Important ⚡)

Exceptions follow inheritance.

Example:

```
Exception (base class)
   |
   ---> IOException
            |
            ---> FileNotFoundException
```

So:
- `FileNotFoundException` IS-A `IOException`
- `IOException` IS-A `Exception`

Because of inheritance, order matters.

---

# 🔹 3. Order of catch Blocks (Very Important Rule 🚨)

❌ Wrong Order:

```csharp
catch (Exception ex)
catch (IOException ioex)
```

Why wrong?

Because:
- `Exception` catches EVERYTHING.
- So `IOException` will NEVER execute.

Compiler gives error (red squiggly).

---

# ✅ Correct Order

Always go:

**Most specific → Most general**

```csharp
catch (FileNotFoundException)
catch (IOException ioex)
catch (JsonException jex)
catch (Exception ex)
```

---

# 🔹 4. Example Scenario

We have two possible problems:

1. File not found → `FileNotFoundException`
2. JSON format wrong → `JsonException`

---

# 📄 Employee.cs

```csharp
public record Employee(int Id, string FirstName, string LastName);
```

---

# 📄 matt.json (Correct JSON)

```json
{
  "Id": 1,
  "FirstName": "Matt",
  "LastName": "Smith"
}
```

---

# 🔥 Full Example Code with Multiple catch Blocks

```csharp
using System;
using System.IO;
using System.Text.Json;

class Program
{
    static void Main()
    {
        string path = "matt.json"; // change to wrong.json to test

        try
        {
            using var fileStream = new FileStream(path, FileMode.Open);

            var employee = JsonSerializer.Deserialize<Employee>(fileStream);

            Console.WriteLine("Employee read successfully:");
            Console.WriteLine(employee);
        }
        catch (FileNotFoundException)
        {
            Console.WriteLine("File not found!");
        }
        catch (IOException ioex)
        {
            Console.WriteLine("IO Exception occurred:");
            Console.WriteLine(ioex.Message);
        }
        catch (JsonException jex)
        {
            Console.WriteLine("JSON Exception occurred:");
            Console.WriteLine(jex.Message);
        }
        catch (Exception ex)
        {
            Console.WriteLine("General Exception:");
            Console.WriteLine(ex.Message);
        }
    }
}
```

---

# 🔹 5. Output Cases

---

## ✅ Case 1: Correct JSON + Correct Path

```
Employee read successfully:
Employee { Id = 1, FirstName = Matt, LastName = Smith }
```

---

## ❌ Case 2: Wrong File Path

Change:

```csharp
string path = "wrong.json";
```

### Output:

```
File not found!
```

Why?

Because:
`FileNotFoundException` matches first.

---

## ❌ Case 3: Invalid JSON Format

Example invalid JSON:

```json
{
  "Id": 1,
  "FirstName": 123,
  "LastName": "Smith"
}
```

Now output:

```
JSON Exception occurred:
The JSON value could not be converted to System.String.
```

---

# 🔹 6. Catch Without Variable

If you're not using the exception object:

Instead of:

```csharp
catch (FileNotFoundException fnfex)
```

You can write:

```csharp
catch (FileNotFoundException)
{
    Console.WriteLine("File not found!");
}
```

Cleaner ✅

Use variable only if:
- You need ex.Message
- You need stack trace
- You want logging

---

# 🔹 7. Key Interview Points 🚀

### 1️⃣ Why order matters?
Because catch blocks are checked top to bottom.

---

### 2️⃣ What happens if base exception comes first?
Derived exceptions will never execute.
Compiler error.

---

### 3️⃣ Why catch specific exceptions?
- Better debugging
- Better logging
- Better user messages
- Cleaner architecture

---

### 4️⃣ Can we have multiple catch blocks?
Yes, unlimited.

---

### 5️⃣ Best Practice in Production

```csharp
catch (SpecificException)
catch (SpecificException2)
catch (Exception ex) // last fallback
```

Always keep general Exception LAST.

---

# 🔹 8. Quick Visual Summary

```
try
{
   risky code
}
catch (MostSpecificException)
{
}
catch (LessSpecificException)
{
}
catch (Exception)   // Most General
{
}
```

---

