
# 🔹 1️⃣ Problem: Assigning Nullable to Non-Nullable

```csharp
int definiteInt;
int? age = null;

definiteInt = age;   // ❌ ERROR
```

Why error?

Because:

- `age` can be `null`
    
- `definiteInt` cannot be `null`
    

C# won’t automatically convert null → 0.

So we must handle null safely.

---

# 🔹 2️⃣ Null-Coalescing Operator (`??`)

## 🔥 Syntax

```csharp
variable = nullableValue ?? fallbackValue;
```

### How it works:

- If left side is NOT null → use it
    
- If left side IS null → use right side
    

---

## ✅ Example 1: Age is null

```csharp
int? age = null;
int definiteInt;

definiteInt = age ?? 17;

Console.WriteLine(definiteInt);
```

### ✔ Output:

```
17
```

Explanation:

- age is null
    
- So 17 is used
    

---

## ✅ Example 2: Age has value

```csharp
int? age = 12;
int definiteInt;

definiteInt = age ?? 17;

Console.WriteLine(definiteInt);
```

### ✔ Output:

```
12
```

Because:

- age is NOT null
    
- So it uses 12
    

---

# 🔹 3️⃣ Null-Coalescing Assignment (`??=`)

This is even cooler.

## 🔥 Syntax

```csharp
variable ??= value;
```

Meaning:

> If variable is null, assign it this value.

---

## ✅ Example 3: Age is null

```csharp
int? age = null;

age ??= 12;

Console.WriteLine(age);
```

### ✔ Output:

```
12
```

Because:

- age was null
    
- So it gets assigned 12
    

---

## ✅ Example 4: Age already has value

```csharp
int? age = 5;

age ??= 12;

Console.WriteLine(age);
```

### ✔ Output:

```
5
```

Because:

- age is NOT null
    
- So it keeps 5
    

---

# 🔹 4️⃣ Combining Everything Together

```csharp
using System;

class Program
{
    static void Main()
    {
        int? age = null;

        // If age is null, assign 12
        age ??= 12;

        int definiteInt = age ?? 17;

        Console.WriteLine("Age: " + age);
        Console.WriteLine("Definite Int: " + definiteInt);
    }
}
```

---

### ✔ Output:

```
Age: 12
Definite Int: 12
```

---

# 🔹 5️⃣ What If Age Starts as 5?

Change:

```csharp
int? age = 5;
```

### ✔ Output:

```
Age: 5
Definite Int: 5
```

Because:

- `age ??= 12` → does nothing
    
- `age ?? 17` → returns 5
    

---

# 🔹 6️⃣ Equivalent Longer Version (Ternary Operator)

Instead of:

```csharp
definiteInt = age ?? 17;
```

You could write:

```csharp
definiteInt = age != null ? age.Value : 17;
```

This means:

```
condition ? value_if_true : value_if_false
```

It works, but it’s longer and less clean.

That’s why `??` is preferred.

---

# 🔹 7️⃣ Visual Comparison

### 🔸 Short Version (Recommended)

```csharp
definiteInt = age ?? 17;
```

### 🔸 Long Version

```csharp
if (age != null)
{
    definiteInt = age.Value;
}
else
{
    definiteInt = 17;
}
```

Same logic.  
Cleaner code with `??`.

---

# 🔹 8️⃣ When You’ll Use This in Real Projects

- Default age if user doesn’t enter one
    
- Default discount percentage
    
- Default configuration values
    
- Default database query results
    
- API fallback values
    

Example:

```csharp
string username = inputName ?? "Guest";
```

---

# 🔹 9️⃣ Quick Revision Notes

## ✅ `??`

Returns fallback value if left side is null.

```
x = y ?? defaultValue;
```

## ✅ `??=`

Assigns value only if variable is null.

```
y ??= defaultValue;
```

## ✅ Ternary equivalent

```
x = y != null ? y.Value : defaultValue;
```

---

