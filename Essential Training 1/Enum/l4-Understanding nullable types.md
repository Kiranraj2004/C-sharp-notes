
# 🔹 1️⃣ Reference Types vs Value Types

## ✅ Reference Types

Examples:

- `string`
    
- `class`
    
- `object`
    
- `array`
    

They can naturally be `null`.

```csharp
string input = null;
```

This is valid because a string is a reference type.  
It can point to:

- An actual string
    
- Or nothing (`null`)
    

---

## ❌ Value Types

Examples:

- `int`
    
- `double`
    
- `bool`
    
- `struct`
    

They **cannot be null by default**.

```csharp
int number = null;   // ❌ ERROR
```

Why?

Because value types always store actual data in memory.  
They are not references — they directly hold the value.

---

# 🔹 2️⃣ Why Nullable Types Are Needed

Imagine this:

```csharp
int age = 0;
```

Now question:

Is the person's age really 0?  
Or did they just not enter their age?

You can’t tell.

That’s where `null` becomes meaningful.

- `0` → actual value
    
- `null` → no value provided
    

---

# 🔹 3️⃣ Making a Value Type Nullable

You add `?` after the type.

```csharp
int? age = null;
```

Now age can store:

- Any integer
    
- OR null
    

---

# 🔹 4️⃣ Another Way to Write It

```csharp
Nullable<int> age2 = null;
```

This is exactly the same as:

```csharp
int? age2 = null;
```

👉 `int?` is just shorthand for `Nullable<int>`.

---

# 🔹 5️⃣ Checking for Null

```csharp
int? age = null;

if (age != null)
{
    Console.WriteLine("Age is: " + age);
}
else
{
    Console.WriteLine("Age was not provided.");
}
```

### ✔ Output:

```
Age was not provided.
```

---

# 🔹 6️⃣ Full Working Example

```csharp
using System;

class Program
{
    static void Main()
    {
        string input = null;

        if (input != null)
        {
            Console.WriteLine("String is: " + input);
        }
        else
        {
            Console.WriteLine("String is null");
        }

        int definiteInt = 5;

        // This would cause warning:
        // if (definiteInt != null) ❌ Not allowed

        int? age = null;

        if (age != null)
        {
            Console.WriteLine("Age is: " + age);
        }
        else
        {
            Console.WriteLine("Age is null");
        }

        age = 25;

        if (age != null)
        {
            Console.WriteLine("Age is now: " + age);
        }
    }
}
```

---

### ✔ Output:

```
String is null
Age is null
Age is now: 25
```

---

# 🔹 7️⃣ Important Nullable Properties

Nullable types have special properties.

```csharp
int? age = 30;

Console.WriteLine(age.HasValue);
Console.WriteLine(age.Value);
```

### ✔ Output:

```
True
30
```

If:

```csharp
int? age = null;
```

Then:

```
age.HasValue → False
age.Value → ❌ Exception
```

⚠ Always check `HasValue` before accessing `.Value`.

---

# 🔹 8️⃣ Null-Coalescing Operator (Very Important)

Super useful shortcut:

```csharp
int? age = null;

int finalAge = age ?? 18;

Console.WriteLine(finalAge);
```

### ✔ Output:

```
18
```

Meaning:

- If age is null → use 18
    
- Otherwise use age
    

This is used a LOT in real applications.

---

# 🔹 9️⃣ Quick Summary Notes (For Revision)

### 🔸 Reference Types

- Can be null by default
    
- Example: `string`
    

### 🔸 Value Types

- Cannot be null by default
    
- Example: `int`, `bool`
    

### 🔸 Make Value Type Nullable

```
int? age;
```

OR

```
Nullable<int> age;
```

### 🔸 Check for Value

```
age != null
age.HasValue
```

### 🔸 Safe Default Value

```
age ?? 0
```

---

# 🔹 🔥 Real World Example

In forms:

- Age field optional
    
- Salary optional
    
- Discount optional
    
- Date of birth optional
    

Without nullable types, you can't differentiate:

- “User entered 0”
    
- “User entered nothing”
    

---

