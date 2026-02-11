
We’ll cover:

1. Using `File` class methods
    
2. Setting file attributes
    
3. Using `FileInfo` class
    
4. Changing file timestamps
    
5. Example code + output
    

---

# 📁 Inspecting File Information in C#

Namespace required:

```csharp
using System.IO;
```

---

# 1️⃣ Getting File Information Using `File` Class

The `File` class provides static methods to retrieve file metadata.

## 🔹 Common Methods

|Method|Purpose|
|---|---|
|`GetCreationTime()`|Returns when file was created|
|`GetLastWriteTime()`|Returns last modified time|
|`GetLastAccessTime()`|Returns last accessed time|
|`GetAttributes()`|Returns file attributes|

---

## ✅ Example: Getting File Time Information

```csharp
using System;
using System.IO;

class Program
{
    static void Main()
    {
        string fileName = "sample.txt";

        // Create file if not exists
        File.WriteAllText(fileName, "Hello File!");

        Console.WriteLine("Creation Time: " + File.GetCreationTime(fileName));
        Console.WriteLine("Last Write Time: " + File.GetLastWriteTime(fileName));
        Console.WriteLine("Last Access Time: " + File.GetLastAccessTime(fileName));
    }
}
```

### 🖥 Example Output:

```
Creation Time: 11-02-2026 10:15:30
Last Write Time: 11-02-2026 10:15:30
Last Access Time: 11-02-2026 10:15:30
```

⚠ Since file was just created, all times are nearly identical.

---

# 2️⃣ Setting File Attributes

We can make a file:

- ReadOnly
    
- Hidden
    
- Archive
    
- etc.
    

## 🔹 Setting File as ReadOnly

```csharp
File.SetAttributes(fileName, FileAttributes.ReadOnly);
```

## 🔹 Checking Attributes

```csharp
Console.WriteLine("Attributes: " + File.GetAttributes(fileName));
```

---

## ✅ Example:

```csharp
using System;
using System.IO;

class Program
{
    static void Main()
    {
        string fileName = "sample.txt";

        File.WriteAllText(fileName, "Testing attributes");

        // Set file to ReadOnly
        File.SetAttributes(fileName, FileAttributes.ReadOnly);

        Console.WriteLine("File Attributes: " + File.GetAttributes(fileName));
    }
}
```

### 🖥 Output:

```
File Attributes: ReadOnly
```

---

# 3️⃣ Using `FileInfo` Class (Object-Oriented Way)

Instead of static methods, we can use `FileInfo`.

🔹 Advantage:

- Access multiple properties at once
    
- More readable
    
- Better for complex operations
    

---

## 🔹 Common Properties of FileInfo

|Property|Meaning|
|---|---|
|`fi.Length`|File size in bytes|
|`fi.DirectoryName`|Folder path|
|`fi.IsReadOnly`|True/False|
|`fi.CreationTime`|Created time|
|`fi.LastWriteTime`|Modified time|

---

## ✅ Example with Try-Catch

```csharp
using System;
using System.IO;

class Program
{
    static void Main()
    {
        string fileName = "sample.txt";

        File.WriteAllText(fileName, "Hello World!");

        try
        {
            FileInfo fi = new FileInfo(fileName);

            Console.WriteLine("File Size: " + fi.Length + " bytes");
            Console.WriteLine("Directory: " + fi.DirectoryName);
            Console.WriteLine("Is ReadOnly: " + fi.IsReadOnly);
        }
        catch (Exception ex)
        {
            Console.WriteLine("Error occurred: " + ex.Message);
        }
    }
}
```

### 🖥 Example Output:

```
File Size: 12 bytes
Directory: C:\Users\User\Documents
Is ReadOnly: False
```

---

# 4️⃣ Changing File Creation Time

Yes — your program can modify file timestamps.

## 🔹 Example: Set Creation Time to Past Date

```csharp
using System;
using System.IO;

class Program
{
    static void Main()
    {
        string fileName = "sample.txt";

        File.WriteAllText(fileName, "Changing time!");

        DateTime oldDate = new DateTime(2020, 7, 1);

        File.SetCreationTime(fileName, oldDate);

        Console.WriteLine("New Creation Time: " + File.GetCreationTime(fileName));
    }
}
```

### 🖥 Output:

```
New Creation Time: 01-07-2020 12:00:00 AM
```

Even though file was created now, we changed its creation time.

---

# ⚠ Important Note

If file is `ReadOnly`, some operations (like changing attributes or writing) may throw exceptions.

That’s why using:

```csharp
try { }
catch(Exception ex) { }
```

is recommended.

---

