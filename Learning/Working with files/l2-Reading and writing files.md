.

We’ll cover:

1. `WriteAllText`
    
2. `ReadAllText`
    
3. `AppendAllText`
    
4. `StreamWriter` with `AppendText`
    
5. Example code + Output
    

---

# 📁 File Handling in C# (Text Files)

C# provides the **`File` class** inside:

```csharp
using System.IO;
```

This class contains static methods to read and write files easily.

---

# 1️⃣ WriteAllText()

### 🔹 Purpose:

Writes text into a file.

### 🔹 Important:

- If the file does NOT exist → it creates it.
    
- If the file exists → it OVERWRITES the content.
    

### 🔹 Syntax:

```csharp
File.WriteAllText("filename.txt", "content");
```

### 🔹 Example:

```csharp
using System;
using System.IO;

class Program
{
    static void Main()
    {
        File.WriteAllText("sample.txt", "This is a text file.");
        Console.WriteLine("File written successfully.");
    }
}
```

### 🖥 Output (Console):

```
File written successfully.
```

### 📄 File Content (sample.txt):

```
This is a text file.
```

---

# 2️⃣ ReadAllText()

### 🔹 Purpose:

Reads entire file content into a string.

### 🔹 Syntax:

```csharp
string data = File.ReadAllText("filename.txt");
```

### 🔹 Example:

```csharp
using System;
using System.IO;

class Program
{
    static void Main()
    {
        File.WriteAllText("sample.txt", "This is a text file.");

        string content = File.ReadAllText("sample.txt");

        Console.WriteLine(content);
    }
}
```

### 🖥 Output:

```
This is a text file.
```

---

# 3️⃣ AppendAllText()

### 🔹 Purpose:

Adds content to the end of the file.

### 🔹 Important:

- Does NOT overwrite.
    
- Adds new text at the bottom.
    

### 🔹 Syntax:

```csharp
File.AppendAllText("filename.txt", "content");
```

### 🔹 Example:

```csharp
using System;
using System.IO;

class Program
{
    static void Main()
    {
        File.WriteAllText("sample.txt", "This is a text file.\n");

        File.AppendAllText("sample.txt", "This text gets appended to the file.\n");

        string content = File.ReadAllText("sample.txt");

        Console.WriteLine(content);
    }
}
```

### 🖥 Output:

```
This is a text file.
This text gets appended to the file.
```

---

# 4️⃣ Using StreamWriter (AppendText)

When writing multiple lines or writing gradually, `StreamWriter` is better.

### 🔹 Why use it?

- Better control
    
- Write line by line
    
- More efficient for large data
    

---

## Example Using StreamWriter

```csharp
using System;
using System.IO;

class Program
{
    static void Main()
    {
        File.WriteAllText("sample.txt", "This is a text file.\n");

        File.AppendAllText("sample.txt", "This text gets appended to the file.\n");

        using (StreamWriter writer = File.AppendText("sample.txt"))
        {
            writer.WriteLine("Line 1");
            writer.WriteLine("Line 2");
            writer.WriteLine("Line 3");
        }

        string content = File.ReadAllText("sample.txt");
        Console.WriteLine(content);
    }
}
```

---

# 🖥 Final Output:

```
This is a text file.
This text gets appended to the file.
Line 1
Line 2
Line 3
```

---


# ⚠️ Best Practice

Always use `using` when working with streams:

```csharp
using(StreamWriter writer = new StreamWriter("file.txt"))
{
    writer.WriteLine("Hello");
}
```

This ensures:

- File is closed properly
    
- Memory is released
    
- Prevents file lock issues
    

---

# 🧠 When to Use What?

|Situation|Use|
|---|---|
|Write once, simple text|WriteAllText|
|Read entire file|ReadAllText|
|Add small content|AppendAllText|
|Write multiple lines gradually|StreamWriter|

---

