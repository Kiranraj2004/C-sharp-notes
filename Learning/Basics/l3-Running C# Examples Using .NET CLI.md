

## 📌 1️⃣ Prerequisite

Before running any C# program, you must install:

👉 **.NET SDK**

SDK = Software Development Kit  
It includes:

- C# Compiler
    
- .NET CLI (`dotnet` command)
    
- Runtime
    
- Build tools
    

To check if installed:

```
dotnet --version
```

If it prints a version → you're ready.

---

# 📂 2️⃣ Understanding Project Structure

Inside the exercise folder, you’ll see:

```
ExerciseFiles/
 ├── Finished/
 │    ├── Overview/
 │    │     ├── HelloWorld/
 │    │          ├── HelloWorld.csproj
 │    │          ├── Program.cs
 ├── Start/
```

---

## 🔹 What is `.csproj`?

Example:

```
HelloWorld.csproj
```

This is the **project file**.

It contains:

- Project configuration
    
- Target framework
    
- Dependencies
    
- Build settings
    

Think of it like:

- `pom.xml` in Maven
    
- `package.json` in Node
    
- `build.gradle` in Gradle
    

Very important file.

---

## 🔹 What is `Program.cs`?

This contains your actual C# code.

Example:

```csharp
Console.WriteLine("Hello World");
```

---

# ▶️ 3️⃣ Running from Command Prompt / Terminal

### Step 1

Open:

- Windows → Command Prompt
    
- Mac/Linux → Terminal
    

### Step 2

Navigate to project folder

Example:

```
cd Desktop/ExerciseFiles/Finished/Overview/HelloWorld
```

### Step 3

Run:

```
dotnet run
```

---

# ⚙️ What Happens When You Type `dotnet run`?

Internally:

1. CLI reads `.csproj`
    
2. Builds project
    
3. Compiles `.cs` files into IL
    
4. Creates assembly (.dll)
    
5. CLR loads assembly
    
6. JIT compiles IL to machine code
    
7. Program runs
    

So `dotnet run` = build + execute.

---

# 💬 Example Output

```
Hello world, what is your name?
Joe
Hello Joe
```

---

# 💻 4️⃣ Running in Visual Studio Code

VS Code has:

👉 Integrated Terminal

Instead of manually navigating folders:

Right click folder →  
**Open in Integrated Terminal**

Then just run:

```
dotnet run
```

Much faster workflow.

---

# 🔥 Important CLI Commands (Extra Knowledge)

These are very useful for interviews and real development.

### Create new console app:

```
dotnet new console -n MyApp
```

Creates:

```
MyApp/
 ├── MyApp.csproj
 ├── Program.cs
```

---

### Build project:

```
dotnet build
```

Compiles project but does NOT run.

---

### Run project:

```
dotnet run
```

Builds + runs.

---

### Restore dependencies:

```
dotnet restore
```

Downloads required packages.

---

# 🧠 What Actually Gets Created?

After running:

Inside project folder:

```
bin/
 ├── Debug/
      ├── net8.0/
           ├── HelloWorld.dll
```

That `.dll` file is your **assembly**.

That is what CLR executes.

---

# 🏗️ Modern C# Console Program (Important Update)

Old style (before C# 9):

```csharp
using System;

class Program
{
    static void Main(string[] args)
    {
        Console.WriteLine("Hello");
    }
}
```

Modern style (.NET 6+):

```csharp
Console.WriteLine("Hello");
```

No explicit `Main()` needed.

Why?

Because .NET now supports **top-level statements**.

Cleaner. Shorter. Modern.

---

# 🧩 Why Console Apps?

The instructor uses console apps because:

✔ Simple  
✔ No GUI complexity  
✔ Focus on language basics  
✔ Easy to run from terminal

Console apps are best for:

- Learning syntax
    
- Practicing logic
    
- DSA
    
- Interview preparation
    

---

# 🆚 VS Code vs Command Prompt

|VS Code Terminal|Command Prompt|
|---|---|
|Built-in|Separate app|
|Faster navigation|Manual cd|
|Better for development|Simple & clean|

Both do the same thing.

---


## q1

# 🎯 First Important Rule

When you run:

```
dotnet run
```

👉 It does **NOT randomly pick a .cs file**.

It runs the project based on the **.csproj file**, not based on individual `.cs` files.

---

# 🧠 How Does .NET Decide What to Run?

Inside a project folder:

```
MyApp/
 ├── MyApp.csproj   👈 important
 ├── Program.cs
 ├── File1.cs
 ├── File2.cs
```

When you type:

```
dotnet run
```

What happens:

1. It reads `MyApp.csproj`
    
2. It compiles **ALL .cs files in that project**
    
3. It looks for the **entry point**
    
4. It runs the method:
    

```
static void Main()
```

OR (modern C#)  
Top-level statements

---

# 🚀 So Which File Runs?

The file that contains:

```
Main()
```

OR top-level statements.

That is the **entry point**.

Even if you have 20 `.cs` files,  
only one `Main()` can exist.

---

# 🧩 Example

### Program.cs

```csharp
class Program
{
    static void Main()
    {
        Console.WriteLine("I am main");
    }
}
```

### File1.cs

```csharp
class Test
{
    public void SayHello()
    {
        Console.WriteLine("Hello");
    }
}
```

When you run:

```
dotnet run
```

Only `Main()` runs.

File1.cs is compiled but NOT executed automatically.

---

# 🔥 What If Multiple Files Have Main()?

You’ll get a compilation error:

```
Program has more than one entry point defined
```

Because .NET doesn’t know which one to start.

---

# 💡 How to Run Individual .cs Files?

Now comes your main doubt 👇

If you have:

```
File1.cs
File2.cs
File3.cs
```

And you want to run them separately.

There are 3 methods.

---

# ✅ Method 1: Create Separate Projects (Best Practice)

Each example should have its own folder:

```
Example1/
 ├── Example1.csproj
 ├── Program.cs

Example2/
 ├── Example2.csproj
 ├── Program.cs
```

Then:

```
cd Example1
dotnet run
```

This is the correct and professional way.

That’s why your course has separate folders for each example.

---

# ✅ Method 2: Comment / Uncomment Main

If inside same project you have:

File1.cs:

```csharp
static void Main() { ... }
```

File2.cs:

```csharp
static void Main() { ... }
```

You must comment one of them.

Only one Main allowed.

---

# ✅ Method 3: Compile Single File Manually (Advanced Way)

If you don’t want project structure:

You can use:

```
csc File1.cs
```

This directly compiles a single file.

It creates:

```
File1.exe
```

Then run:

```
File1.exe
```

But this method is not recommended for modern .NET development.

---

# 🆕 Modern .NET (Top-Level Statements Case)

Example:

File1.cs

```csharp
Console.WriteLine("Hello from File1");
```

File2.cs

```csharp
Console.WriteLine("Hello from File2");
```

If both have top-level statements → ERROR.

Only one file can contain top-level code.

---

# 🧠 Important Concept: Entry Point

Entry point is:

```
static void Main(string[] args)
```

or top-level code.

CLR starts execution from here.

Everything else is just supporting code.

---

# 📌 Real-World Practice

In real projects:

You never run individual `.cs` files.

You run:

- The entire project
    
- Or specific startup project
    

Because C# is project-based, not file-based like scripting languages.

Unlike:

- Python → run single .py
    
- Node → run single .js
    

C# is compiled project-based.


## q2

# ☕ Java Way

In Java you do:

```
javac FileName.java
```

This creates:

```
FileName.class
```

Then you run:

```
java FileName
```

So:

```
Source → Bytecode → JVM → Run
```

Two-step process:

1. Compile
    
2. Execute
    

---

# 🔷 C# Modern Way (.NET CLI)

In C# with .NET SDK:

You usually just run:

```
dotnet run
```

Behind the scenes it does BOTH:

- Compile
    
- Run
    

So it’s like:

```
Compile + Execute (together)
```

---

# 🔥 If You Want Java-Like Behavior in C#

You can separate it.

### Step 1: Build (like javac)

```
dotnet build
```

This compiles your code and creates:

```
bin/Debug/net8.0/MyApp.dll
```

That `.dll` is your compiled assembly (like `.class` in Java).

---

### Step 2: Run (like java command)

```
dotnet bin/Debug/net8.0/MyApp.dll
```

So this:

```
dotnet MyApp.dll
```

Is similar to:

```
java FileName
```

Now it looks very similar, right? 😄

---

# 🧠 What About `csc`?

There is also a lower-level compiler command:

```
csc FileName.cs
```

That directly creates:

```
FileName.exe
```

Then run:

```
FileName.exe
```

That’s VERY similar to:

```
javac
java
```

But modern .NET development prefers:

```
dotnet build
dotnet run
```

Because it handles:

- Dependencies
    
- Framework targeting
    
- Versioning
    
- Project configuration
    

---

# 🆚 Clean Comparison Table

|Java|C# (.NET CLI)|
|---|---|
|javac File.java|dotnet build|
|java File|dotnet MyApp.dll|
|.class|.dll|
|JVM|CLR|

---

# ⚡ Important Difference

Java runs `.class` files directly on JVM.

C# runs:

- Assembly (.dll or .exe)
    
- Through CLR
    
- Then JIT converts to machine code
    

Architecture is very similar.

---

# 🧩 One Big Mindset Shift

Java = file-based execution  
C# = project-based execution

That’s why `.csproj` exists.

You don’t usually run single `.cs` files in professional C# development.

---
