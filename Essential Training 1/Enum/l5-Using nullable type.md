
# 🔹 1️⃣ What Is a Nullable Type Internally?

When you write:

```csharp
int? age;
```

It actually becomes:

```csharp
Nullable<int> age;
```

And `Nullable<T>` has:

- ✅ `HasValue` → returns `true` or `false`
    
- ✅ `Value` → gives the actual stored value
    
- ✅ Conversion operators (implicit & explicit)
    

---

# 🔹 2️⃣ The Two Important Properties

## ✅ 1. HasValue

This tells you whether the nullable variable contains a value.

```csharp
int? age = null;

Console.WriteLine(age.HasValue);
```

### ✔ Output:

```
False
```

If:

```csharp
int? age = 25;
```

Output:

```
True
```

---

## ✅ 2. Value

This returns the actual underlying value.

```csharp
int? age = 25;

Console.WriteLine(age.Value);
```

### ✔ Output:

```
25
```

⚠ BUT if age is null:

```csharp
int? age = null;
Console.WriteLine(age.Value);   // ❌ Exception
```

### ❌ Runtime Error:

```
InvalidOperationException: Nullable object must have a value.
```

That’s why you must check `HasValue` first.

---

# 🔹 3️⃣ Safe Way to Use Value

```csharp
int? age = null;

if (age.HasValue)
{
    Console.WriteLine("Age is: " + age.Value);
}
else
{
    Console.WriteLine("Age has no value.");
}
```

### ✔ Output:

```
Age has no value.
```

---

# 🔹 4️⃣ Implicit Conversion (Very Important)

The instructor mentioned something powerful.

You can assign:

```csharp
int? age = 17;
```

Even though `age` is nullable, you can directly assign an `int`.

Why?

Because `Nullable<T>` defines **implicit conversion operators**.

You don’t need:

```csharp
age.Value = 17;  ❌ NOT ALLOWED
```

That would fail because:

- `Value` is read-only.
    
- You must assign to `age` directly.
    

---

# 🔹 5️⃣ Comparing Nullable with Normal Values

You can do this:

```csharp
int? age = 17;

if (age == 17)
{
    Console.WriteLine("Age is 17");
}
```

This works because of implicit conversion.

C# automatically converts:

```
int?  ↔  int
```

---

# 🔹 6️⃣ Full Working Example

```csharp
using System;

class Program
{
    static void Main()
    {
        int? age = null;

        Console.WriteLine("HasValue: " + age.HasValue);

        if (age.HasValue)
        {
            Console.WriteLine("Age: " + age.Value);
        }
        else
        {
            Console.WriteLine("Age is not set.");
        }

        // Assigning value using implicit conversion
        age = 17;

        Console.WriteLine("\nAfter assigning 17:");

        Console.WriteLine("HasValue: " + age.HasValue);
        Console.WriteLine("Age: " + age.Value);

        if (age == 17)
        {
            Console.WriteLine("Age equals 17");
        }
    }
}
```

---

### ✔ Output:

```
HasValue: False
Age is not set.

After assigning 17:
HasValue: True
Age: 17
Age equals 17
```

---

# 🔹 7️⃣ What Happens Behind the Scenes?

Think of `Nullable<int>` like this simplified structure:

```csharp
struct Nullable<T>
{
    private bool hasValue;
    private T value;

    public bool HasValue { get; }
    public T Value { get; }
}
```

So when you write:

```csharp
int? age = null;
```

It sets:

```
hasValue = false
```

When you write:

```csharp
int? age = 25;
```

It sets:

```
hasValue = true
value = 25
```

---

# 🔹 8️⃣ Important Concept from Transcript

The instructor said:

> Nullable types behave like reference types.

That means:

- You can assign null
    
- You can check for null
    
- You can compare with constants
    
- You can assign normal values directly
    

But internally, they are still value types (struct).

That’s why they need `HasValue` and `Value`.

---

