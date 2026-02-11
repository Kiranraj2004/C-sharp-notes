
# 🔹 1. What is Exception Handling?

An **exception** is an error that occurs during program execution.

Examples:

- File not found
    
- Divide by zero
    
- Null reference
    
- Invalid JSON format
    

Instead of crashing the program, we handle it using:

```
try
catch
finally
```

---

# 🔹 2. Basic Structure of try-catch-finally

```csharp
try
{
    // Code that may throw exception
}
catch (Exception ex)
{
    // Code to handle exception
}
finally
{
    // Code that always runs
}
```

---

# 🔹 3. Understanding Each Block

## ✅ 1. try block

- Contains risky code
    
- If something goes wrong → exception is thrown
    

Example risky operations:

- Opening file
    
- Database connection
    
- JSON deserialization
    

---

## ✅ 2. catch block

- Executes only if exception occurs
    
- You can capture the exception object
    
- `ex.Message` gives error message
    

Example:

```csharp
catch (Exception ex)
{
    Console.WriteLine("Error: " + ex.Message);
}
```

---

## ✅ 3. finally block

- Always runs
    
- Used for cleanup
    
- Closing files
    
- Closing DB connections
    

Even if:

- No exception
    
- Exception occurs
    
- Program returns early
    

finally still executes.

---

# 🔹 4. Example from Transcript – Reading JSON File

Let’s recreate a simple working example.

---

## 📁 Employee.cs

```csharp
public record Employee(int Id, string FirstName, string LastName);
```

---

## 📄 matt.json

```json
{
  "Id": 1,
  "FirstName": "Matt",
  "LastName": "Smith"
}
```

---

## 💻 Program.cs (Manual Dispose Version)

```csharp
using System;
using System.IO;
using System.Text.Json;

class Program
{
    static void Main()
    {
        string rightPath = "matt.json";
        string wrongPath = "wrong.json";

        FileStream fileStream = null;

        try
        {
            Console.WriteLine("Current Directory: " + Directory.GetCurrentDirectory());

            fileStream = new FileStream(rightPath, FileMode.Open);

            var employee = JsonSerializer.Deserialize<Employee>(fileStream);

            Console.WriteLine("Employee read from file:");
            Console.WriteLine(employee);
        }
        catch (Exception ex)
        {
            Console.WriteLine("Exception caught:");
            Console.WriteLine(ex.Message);
        }
        finally
        {
            if (fileStream != null)
            {
                fileStream.Dispose();
                Console.WriteLine("FileStream closed.");
            }
        }
    }
}
```

---

## ✅ OUTPUT (Correct Path)

```
Current Directory: C:\Project\bin\Debug\net6.0
Employee read from file:
Employee { Id = 1, FirstName = Matt, LastName = Smith }
FileStream closed.
```

---

## ❌ OUTPUT (Wrong Path)

```
Current Directory: C:\Project\bin\Debug\net6.0
Exception caught:
Could not find file 'wrong.json'
FileStream closed.
```

---

# 🔹 5. Problem With Manual Dispose

In manual method:

- You must remember to call `Dispose()`
    
- If you forget → memory leak
    
- External resource may remain open
    

FileStream implements:

```
IDisposable
```

That means it has a `Dispose()` method.

---

# 🔹 6. Better Way – Using Statement (Recommended)

Instead of manually disposing:

```csharp
using var fileStream = new FileStream(path, FileMode.Open);
```

The `using` statement automatically disposes the object when the block ends.

---

## 💻 Improved Code (Using Statement)

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
            Console.WriteLine("Current Directory: " + Directory.GetCurrentDirectory());

            using var fileStream = new FileStream(path, FileMode.Open);

            var employee = JsonSerializer.Deserialize<Employee>(fileStream);

            Console.WriteLine("Employee read from file:");
            Console.WriteLine(employee);
        }
        catch (Exception ex)
        {
            Console.WriteLine("Exception caught:");
            Console.WriteLine(ex.Message);
        }
    }
}
```

---

## 🔥 Why Using is Better?

Because:

- Automatically calls Dispose()
    
- Cleaner code
    
- Safer
    
- Prevents resource leaks
    
- Preferred in interviews
    

---

# 🔹 7. Execution Flow Summary

### 🟢 Case 1: No Exception

```
try block executes fully
↓
finally executes
```

---

### 🔴 Case 2: Exception Occurs

```
try executes until error
↓
catch executes
↓
finally executes
```

---

# 🔹 8. Important Interview Concepts

### 1️⃣ What is IDisposable?

Interface used to clean unmanaged resources (file handles, DB connections, etc.)

### 2️⃣ Why finally?

To ensure cleanup happens no matter what.

### 3️⃣ Can we have try without catch?

Yes, but must have finally.

### 4️⃣ Can we have multiple catch blocks?

Yes.

Example:

```csharp
catch (FileNotFoundException ex)
{
    Console.WriteLine("File missing");
}
catch (JsonException ex)
{
    Console.WriteLine("Invalid JSON format");
}
```

---

# 🔹 9. Best Practice (Production Level)

Instead of catching base `Exception`, catch specific ones.

❌ Not recommended:

```csharp
catch (Exception ex)
```

✅ Better:

```csharp
catch (FileNotFoundException ex)
catch (JsonException ex)
```

---

