
# 🔹 1. What is Exception Filtering with `when`?

Normally we do:

```csharp
catch (JsonException ex)
{
    // handle JSON error
}
```

But what if:

- There are **many reasons** for a JsonException?
    
    - Type conversion error
        
    - Missing comma
        
    - Invalid syntax
        
    - Unexpected token
        
    - Null value
        

We might want to handle them differently.

That’s where `when` comes in.

---

# 🔹 2. Syntax of `when`

```csharp
catch (ExceptionType ex) when (condition)
{
    // executes only if condition is true
}
```

So:

- First → exception type must match
    
- Then → condition must return true
    
- Only then → catch block executes
    

If condition is false → it skips this catch and checks next one.

---

# 🔥 3. Real Example from Transcript

We have this invalid JSON:

```json
{
  "Id": 1,
  "FirstName": 809,
  "LastName": "Smith"
}
```

Problem:

- FirstName should be string
    
- But we gave number
    

Error message contains:

```
"The JSON value could not be converted..."
```

So we filter like this:

```csharp
catch (JsonException jsoex)
    when (jsoex.Message.Contains("converted", StringComparison.OrdinalIgnoreCase))
{
    Console.WriteLine("JSON Conversion Error:");
    Console.WriteLine(jsoex.Message);
}
```

This will ONLY catch JSON exceptions where message contains "converted".

---

# 🔹 4. Full Working Example

---

## 📄 Employee.cs

```csharp
public record Employee(int Id, string FirstName, string LastName);
```

---

## 💻 Program.cs

```csharp
using System;
using System.IO;
using System.Text.Json;

class Program
{
    static void Main()
    {
        string path = "matt.json";

        try
        {
            using var fileStream = new FileStream(path, FileMode.Open);

            var employee = JsonSerializer.Deserialize<Employee>(fileStream);

            Console.WriteLine("Employee read successfully:");
            Console.WriteLine(employee);
        }

        // Filter 1 → Conversion problem
        catch (JsonException jsoex)
            when (jsoex.Message.Contains("converted",
                   StringComparison.OrdinalIgnoreCase))
        {
            Console.WriteLine("JSON Conversion Error:");
            Console.WriteLine(jsoex.Message);
        }

        // Filter 2 → Syntax problem (missing comma etc.)
        catch (JsonException jsoex)
            when (jsoex.Message.Contains("invalid",
                   StringComparison.OrdinalIgnoreCase))
        {
            Console.WriteLine("JSON Syntax Error:");
            Console.WriteLine(jsoex.Message);
        }

        // General JSON fallback
        catch (JsonException jsoex)
        {
            Console.WriteLine("Other JSON Error:");
            Console.WriteLine(jsoex.Message);
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

# 🔹 5. Output Scenarios

---

## ✅ Case 1: Type Conversion Error

JSON:

```json
{
  "Id": 1,
  "FirstName": 809,
  "LastName": "Smith"
}
```

### Output:

```
JSON Conversion Error:
The JSON value could not be converted to System.String.
```

Because:  
✔ Exception type = JsonException  
✔ Message contains "converted"

---

## ❌ Case 2: Missing Comma (Syntax Error)

JSON:

```json
{
  "Id": 1
  "FirstName": "Matt",
  "LastName": "Smith"
}
```

### Output:

```
JSON Syntax Error:
'"' is invalid after a value.
```

Because:  
✔ JsonException  
✔ Message contains "invalid"

---

## 🔁 Case 3: Some Other JSON Error

If it doesn’t match any `when` filter:

```
Other JSON Error:
<actual message>
```

---

# 🔹 6. Important Concept: How `when` Works Internally

Flow:

1. Exception thrown
    
2. Check first catch type
    
3. If type matches → evaluate `when`
    
4. If `when` true → execute
    
5. If false → skip to next catch
    

It DOES NOT throw another exception.  
It just continues searching.

---

# 🔹 7. Why Use `when`?

Without `when`, you'd write:

```csharp
catch (JsonException ex)
{
    if (ex.Message.Contains("converted"))
    {
        ...
    }
}
```

But with `when`:

- Cleaner
    
- More readable
    
- Better structured
    
- Compiler-level filtering
    
- More efficient
    

---

