

To take input:

```csharp
Console.ReadLine();
```

⚠ Important:  
`Console.ReadLine()` **always returns string**.

So if you want:

- int
    
- double
    
- float
    
- bool  
    You must convert it.
    

---

# 🟢 1️⃣ Taking String Input

```csharp
Console.WriteLine("Enter your name:");
string name = Console.ReadLine();

Console.WriteLine("Hello " + name);
```

✔ No conversion needed  
✔ Direct assignment

---

# 🔵 2️⃣ Taking Integer Input

Since input is string, convert it.

### Method 1: Using int.Parse()

```csharp
Console.WriteLine("Enter your age:");
int age = int.Parse(Console.ReadLine());

Console.WriteLine("Your age is " + age);
```

---

### Method 2: Using Convert.ToInt32()

```csharp
int age = Convert.ToInt32(Console.ReadLine());
```

Both work.  
Difference is small (Convert handles null slightly better).

---

# 🟣 3️⃣ Taking Double Input

```csharp
Console.WriteLine("Enter your salary:");
double salary = double.Parse(Console.ReadLine());

Console.WriteLine("Salary: " + salary);
```

---

# 🟡 4️⃣ Taking Float Input

```csharp
float number = float.Parse(Console.ReadLine());
```

---

# 🟠 5️⃣ Taking Boolean Input

```csharp
Console.WriteLine("Are you placed? (true/false)");
bool isPlaced = bool.Parse(Console.ReadLine());

Console.WriteLine(isPlaced);
```

User must type:

```
true
```

or

```
false
```

---

# 🔥 6️⃣ Safer Way (Recommended) – TryParse

If user types wrong value, `Parse()` throws exception.

Better way:

```csharp
Console.WriteLine("Enter age:");
string input = Console.ReadLine();

if (int.TryParse(input, out int age))
{
    Console.WriteLine("Valid age: " + age);
}
else
{
    Console.WriteLine("Invalid input!");
}
```

This prevents program crash.

Interview-level clean code uses `TryParse()`.

---

# 🧩 Full Example Program

```csharp
Console.WriteLine("Enter your name:");
string name = Console.ReadLine();

Console.WriteLine("Enter your age:");
int age = int.Parse(Console.ReadLine());

Console.WriteLine("Enter your CGPA:");
double cgpa = double.Parse(Console.ReadLine());

Console.WriteLine("Name: " + name);
Console.WriteLine("Age: " + age);
Console.WriteLine("CGPA: " + cgpa);
```

---

# ⚡ Important Tip (Very Useful)

If you're using .NET 6+ with nullable reference types enabled,  
`Console.ReadLine()` may return null.

Safer way:

```csharp
string? input = Console.ReadLine();
```

Or:

```csharp
string input = Console.ReadLine() ?? "";
```

---

# 🆚 Java Comparison (So You Connect Faster)

Java:

```java
Scanner sc = new Scanner(System.in);
int age = sc.nextInt();
```

C#:

```csharp
int age = int.Parse(Console.ReadLine());
```

C# doesn’t use Scanner.  
It uses `Console.ReadLine()`.

---

# 🎯 Quick Summary

|Data Type|How to Take Input|
|---|---|
|string|Console.ReadLine()|
|int|int.Parse(Console.ReadLine())|
|double|double.Parse(Console.ReadLine())|
|float|float.Parse(Console.ReadLine())|
|bool|bool.Parse(Console.ReadLine())|

Safe version → `TryParse()`

---