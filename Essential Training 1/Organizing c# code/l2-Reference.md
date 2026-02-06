
# 🔹 Big Picture

Earlier:

- Everything was inside **one project**
    
- Namespace was enough
    

Now:

- We created a **separate Class Library (DLL)**
    
- And tried to use its types in another project
    

💥 Suddenly namespace alone was NOT enough.

Why?

Because:

> Namespace organizes types  
> Assembly (DLL) contains compiled code

You must reference the assembly, not just the namespace.

---

# 🔹 Important Concepts

## 1️⃣ What is an Assembly?

An **Assembly** is a compiled output:

- `.dll` (Class Library)
    
- `.exe` (Console App)
    

When you create:

```bash
dotnet new classlib
```

It produces a `.dll`.

That DLL contains:

- Compiled code
    
- Metadata
    
- Type definitions
    

---

## 2️⃣ Namespace vs Assembly (Very Important)

|Namespace|Assembly|
|---|---|
|Logical grouping|Physical compiled file|
|Helps avoid naming conflicts|Contains compiled code|
|Exists in source code|Exists after compilation|

⚠️ Namespace alone is NOT enough.  
You must reference the assembly that contains it.

---

# 🔹 Scenario Explained

You had:

### Console App Project

```
LinkedIn.Essentials (Console App)
```

Then added:

### Class Library Project

```
LinkedIn.Essentials.Types (Class Library)
```

Moved:

- `Employee`
    
- `Manager`
    
- `Constants`
    

into the library project.

Now Console App tries:

```csharp
using LinkedIn.Essentials.Types;
```

💥 Error appears.

Why?

Because the console app does not know about that DLL.

---

# 🔹 Solution: Add Project Reference

In Visual Studio:

```
Right click Project
→ Add
→ Project Reference
→ Select LinkedIn.Essentials.Types
```

Now:

✔ Assembly is referenced  
✔ Namespace becomes usable  
✔ Types are available

---

# 🔹 Example Structure

---

## 📁 LinkedIn.Essentials.Types (Class Library)

### Employee.cs

```csharp
namespace LinkedIn.Essentials.Types;

public class Employee
{
    public string FirstName { get; set; }
}
```

---

### Manager.cs

```csharp
namespace LinkedIn.Essentials.Types;

public class Manager : Employee
{
}
```

---

### Constants.cs

```csharp
namespace LinkedIn.Essentials.Types;

public class Constants
{
    public const string Company = "LinkedIn";
}
```

---

## 📁 Console App Project

After adding project reference 👇

---

### Program.cs

```csharp
using LinkedIn.Essentials.Types;

class Program
{
    static void Main()
    {
        Employee e = new Manager();
        e.FirstName = "Hello";

        Console.WriteLine(e.FirstName);
        Console.WriteLine(Constants.Company);
    }
}
```

---

## ✅ Output

```
Hello
LinkedIn
```

Boom 💥  
Types are coming from another assembly (DLL).

---

# 🔹 How Compiler Thinks

When you compile:

```
Compile this project
BUT
Also look inside this referenced DLL for missing types
```

Without reference → compiler cannot find those types.

---

# 🔹 Another Way to Add Reference: NuGet

Now this is what happens in real-world projects.

Instead of referencing your own DLL,  
you download packages from:

👉 [https://nuget.org](https://nuget.org/)

Example:  
`Newtonsoft.Json`

---

## Install via NuGet

Visual Studio:

```
Manage NuGet Packages
→ Browse
→ Newtonsoft.Json
→ Install
```

Now it:

✔ Downloads DLL  
✔ Adds reference automatically  
✔ Adds entry in project file

---

# 🔹 Example Using Newtonsoft.Json

After installing:

```csharp
using Newtonsoft.Json;
using LinkedIn.Essentials.Types;

class Program
{
    static void Main()
    {
        Employee e = new Employee();
        e.FirstName = "Kiran";

        string json = JsonConvert.SerializeObject(e);

        Console.WriteLine(json);
    }
}
```

---

## ✅ Output

```
{"FirstName":"Kiran"}
```

Now you're using:

- Your own assembly (project reference)
    
- External assembly (NuGet package)
    

Same concept 🔥

---

# 🔹 Alternative: Fully Qualified Name

Instead of:

```csharp
using LinkedIn.Essentials.Types;
```

You could write:

```csharp
LinkedIn.Essentials.Types.Employee e =
    new LinkedIn.Essentials.Types.Employee();
```

But that becomes ugly fast 😅

---

# 🔹 Three Ways to Add References

### 1️⃣ Project Reference

- Reference another project in solution
    

### 2️⃣ DLL Reference

- Browse and add external DLL manually
    

### 3️⃣ NuGet Package

- Download from nuget.org
    
- Automatically managed
    

---

# 🔹 Real Interview Understanding

If interviewer asks:

👉 "What is the difference between namespace and assembly?"

You say:

> Namespace is a logical grouping of types in code.  
> Assembly is the compiled output (DLL/EXE) that contains those types.  
> To use types from another project, we must reference the assembly.

Clean. Strong. Mature answer. 💪

---

# 🔹 What Happened in Transcript (Step-by-Step)

1. Created class library
    
2. Moved types there
    
3. Console app broke
    
4. Added project reference
    
5. Types became available
    
6. Installed NuGet package
    
7. Used JsonSerializer
    
8. Program printed JSON output
    

---

