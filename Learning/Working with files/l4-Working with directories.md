

We’ll cover:

1. What is a Directory?
    
2. Creating & Deleting Directories
    
3. Getting Current Directory
    
4. DirectoryInfo class
    
5. Enumerating (listing) contents
    
6. Example code + outputs
    

---

# 📂 What is a Directory?

- A directory (folder) organizes files and other directories.
    
- It does NOT directly store data like files.
    
- It helps structure your project.
    

Namespace required:

```csharp
using System;
using System.IO;
using System.Collections.Generic;
```

---

# 1️⃣ Creating and Deleting Directories

Just like `File`, C# provides a `Directory` class.

---

## 🔹 Create Directory

```csharp
Directory.CreateDirectory("TestFolder");
```

If it already exists → nothing happens.

---

## 🔹 Delete Directory

```csharp
Directory.Delete("TestFolder");
```

⚠ Directory must be empty or it throws exception.

---

## ✅ Example: Create if not exists, else delete

```csharp
using System;
using System.IO;

class Program
{
    static void Main()
    {
        string dirName = "TestFolder";

        if (!Directory.Exists(dirName))
        {
            Directory.CreateDirectory(dirName);
            Console.WriteLine("Directory Created.");
        }
        else
        {
            Directory.Delete(dirName);
            Console.WriteLine("Directory Deleted.");
        }
    }
}
```

### 🖥 Output (First Run):

```
Directory Created.
```

### 🖥 Output (Second Run):

```
Directory Deleted.
```

---

# 2️⃣ Get Current Working Directory

The current working directory is usually the folder where your app runs.

```csharp
string curPath = Directory.GetCurrentDirectory();
Console.WriteLine("Current Directory: " + curPath);
```

---

### 🖥 Example Output:

```
Current Directory: C:\Users\User\source\repos\MyApp
```

---

# 3️⃣ DirectoryInfo Class (Object-Oriented Way)

Like `FileInfo`, we have `DirectoryInfo`.

Used to get properties of a directory.

---

## 🔹 Common Properties

|Property|Meaning|
|---|---|
|`Name`|Directory name|
|`Parent`|Parent directory|
|`CreationTime`|When folder was created|
|`FullName`|Full path|

---

## ✅ Example:

```csharp
using System;
using System.IO;

class Program
{
    static void Main()
    {
        string curPath = Directory.GetCurrentDirectory();

        DirectoryInfo di = new DirectoryInfo(curPath);

        Console.WriteLine("Directory Name: " + di.Name);
        Console.WriteLine("Parent Directory: " + di.Parent);
        Console.WriteLine("Creation Time: " + di.CreationTime);
    }
}
```

---

### 🖥 Output:

```
Directory Name: MyApp
Parent Directory: C:\Users\User\source\repos
Creation Time: 11-02-2026 09:50:00
```

---

# 4️⃣ Enumerating Directory Contents

This is VERY important 🔥  
Used in real-world apps like file explorers.

---

## 🔹 Enumerate Directories Only

```csharp
Directory.EnumerateDirectories(path);
```

Returns only folders.

---

## 🔹 Enumerate Files Only

```csharp
Directory.EnumerateFiles(path);
```

Returns only files.

---

## 🔹 Enumerate Everything

```csharp
Directory.EnumerateFileSystemEntries(path);
```

Returns both files and folders.

---

# ✅ Full Example: List Everything

```csharp
using System;
using System.IO;

class Program
{
    static void Main()
    {
        string path = Directory.GetCurrentDirectory();

        Console.WriteLine("=== Directories ===");
        foreach (string dir in Directory.EnumerateDirectories(path))
        {
            Console.WriteLine(dir);
        }

        Console.WriteLine("\n=== Files ===");
        foreach (string file in Directory.EnumerateFiles(path))
        {
            Console.WriteLine(file);
        }

        Console.WriteLine("\n=== All Entries ===");
        foreach (string entry in Directory.EnumerateFileSystemEntries(path))
        {
            Console.WriteLine(entry);
        }
    }
}
```

---

# 🖥 Example Output:

```
=== Directories ===
C:\MyApp\bin
C:\MyApp\obj

=== Files ===
C:\MyApp\Program.cs
C:\MyApp\MyApp.csproj

=== All Entries ===
C:\MyApp\bin
C:\MyApp\obj
C:\MyApp\Program.cs
C:\MyApp\MyApp.csproj
```

---

# 🔥 Important Interview Concepts

### ✅ Difference Between Enumerate and Get Methods

There are also:

```csharp
Directory.GetFiles()
Directory.GetDirectories()
```

🔹 Difference:

|Get|Enumerate|
|---|---|
|Returns full array immediately|Returns items one-by-one|
|Loads everything into memory|More memory efficient|
|Slower for large folders|Better for large folders|

👉 Prefer `Enumerate` for large directories.

---

# ⚠️ Common Mistakes

❌ Redeclaring list variables  
❌ Trying to delete non-empty directory  
❌ Forgetting `Directory.Exists()` check

---

# 🧠 Real-World Uses

- File explorer app
    
- Upload systems
    
- Log file scanning
    
- Backup systems
    
- Sorting files by type
    

---

# 📌 Summary

✔ `Directory.Exists()` → Check folder  
✔ `CreateDirectory()` → Create folder  
✔ `Delete()` → Delete folder  
✔ `GetCurrentDirectory()` → Current path  
✔ `DirectoryInfo` → Get folder properties  
✔ `EnumerateDirectories()` → List folders  
✔ `EnumerateFiles()` → List files  
✔ `EnumerateFileSystemEntries()` → List everything

---

