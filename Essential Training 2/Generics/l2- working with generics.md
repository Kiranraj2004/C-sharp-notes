
In C#, generics are used in two main places:

1. **Generic Methods**
    
2. **Generic Types (Classes, Structs, Records, etc.)**
    

---

# 1️⃣ Generic Methods

A generic method allows you to specify a type when calling the method.

### 📌 Real Example: JSON Deserialization

C# has:

```csharp
JsonSerializer.Deserialize<T>()
```

Notice the `<T>` — this is a **generic method**.

---

## 🔹 Why is this useful?

When deserializing JSON:

- You KNOW what type you expect (like `Person`)
    
- So instead of getting `object`, you tell the method:
    

> “Deserialize this JSON into a Person”

---

## 🧩 Example: Person Class

```csharp
public class Person
{
    public int Id { get; set; }
    public string FirstName { get; set; }
    public string LastName { get; set; }
    public int Age { get; set; }
}
```

---

## 🧩 Example: Using Generic Method

```csharp
using System;
using System.Text.Json;

class Program
{
    static void Main()
    {
        string json = """
        {
            "Id": 1,
            "FirstName": "Matt",
            "LastName": "Smith",
            "Age": 50
        }
        """;

        Person? pj = JsonSerializer.Deserialize<Person>(json);

        Console.WriteLine($"JSON Person: {pj?.FirstName} is {pj?.Age}");
    }
}
```

---

### ✅ Output:

```
JSON Person: Matt is 50
```

---

## 🧠 What’s Happening?

When we write:

```csharp
JsonSerializer.Deserialize<Person>(json);
```

The compiler replaces:

```
T → Person
```

So internally it behaves like:

```csharp
Person Deserialize(string json)
```

✔ Type-safe  
✔ No casting required  
✔ Compile-time checking

---

# 2️⃣ Generic Types

Now let’s talk about generic classes.

Example:

```csharp
Nullable<T>
```

You usually see it as:

```csharp
int? x;
```

But internally it is:

```csharp
Nullable<int> x;
```

---

# 🔷 Example 1: Nullable

```csharp
int? x = 5;

Console.WriteLine(x.Value);
Console.WriteLine(x.GetValueOrDefault());
```

### ✅ Output:

```
5
5
```

---

If null:

```csharp
int? x = null;

Console.WriteLine(x.GetValueOrDefault());
```

### ✅ Output:

```
0
```

Why 0?

Because:

- Default value of `int` = 0
    

---

# 🔷 Example 2: Nullable

```csharp
DateTime? maybeDate = null;

Console.WriteLine(maybeDate.GetValueOrDefault());
```

### ✅ Output:

```
01-01-0001 00:00:00
```

That’s:

> Default(DateTime)

---

## 🧠 What’s Happening?

When you write:

```csharp
DateTime? maybeDate;
```

Compiler converts it to:

```csharp
Nullable<DateTime> maybeDate;
```

So inside the class:

- `Value` property → returns `DateTime`
    
- `GetValueOrDefault()` → returns `DateTime`
    
- Type depends on `<T>`
    

---

# 🔥 Key Understanding

When using generics:

The type parameter `<T>` influences:

- Method parameters
    
- Return types
    
- Properties
    
- Internal fields
    

---

# 📦 Another Simple Generic Class Example

Let’s create our own generic class:

```csharp
class Box<T>
{
    public T Value { get; set; }

    public void Display()
    {
        Console.WriteLine($"Stored value: {Value}");
    }
}
```

---

## Using It:

```csharp
Box<int> intBox = new Box<int>();
intBox.Value = 10;
intBox.Display();

Box<string> stringBox = new Box<string>();
stringBox.Value = "Hello";
stringBox.Display();
```

---

### ✅ Output:

```
Stored value: 10
Stored value: Hello
```

---

# 🎯 Important Concept

When you write:

```csharp
Box<int>
```

Compiler creates a type-safe version of:

```csharp
class Box
{
    public int Value { get; set; }
}
```

No casting needed.  
No runtime confusion.

---

# 🧠 Difference Between Generic Method & Generic Type

|Feature|Generic Method|Generic Class|
|---|---|---|
|Scope|Only that method|Whole class|
|Syntax|`void Method<T>()`|`class MyClass<T>`|
|Example|`Deserialize<T>()`|`Nullable<T>`|

---

# 🔥 Interview-Level Understanding

### ❓ Why use generics in Deserialize?

Without generics:

```csharp
object obj = JsonSerializer.Deserialize(json);
Person p = (Person)obj;   // Casting required
```

Problems:

- Runtime casting errors possible
    
- Not type-safe
    
- Ugly code
    

With generics:

```csharp
Person p = JsonSerializer.Deserialize<Person>(json);
```

✔ Safe  
✔ Clean  
✔ No casting

---

