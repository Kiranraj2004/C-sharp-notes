
# 🧠 1️⃣ C# is Strongly Typed

In C#, you must declare the **type** of a variable.

Unlike Python/JavaScript:

```python
x = 10
```

In C#:

```csharp
int x = 10;
```

Why?

✔ Prevents type errors  
✔ Improves performance  
✔ Better compile-time safety

---

# 🔢 2️⃣ Basic Data Types in C#

## 🔹 Integer Types (Whole Numbers)

```csharp
int i = 10;
long l = 1000000L;
short s = 5;
byte b = 255;
```

- `int` → 32-bit
    
- `long` → 64-bit (bigger range)
    

---

## 🔹 Floating Point Types

```csharp
float f = 2.5f;   // must add 'f'
double d = 3.14;  // default floating type
decimal m = 10.5m; // must add 'm'
```

Important:

- `float` → less precision
    
- `double` → more precision
    
- `decimal` → high precision (used in banking)
    

---

## 🔹 Boolean

```csharp
bool isPlaced = true;
```

Only:

- true
    
- false
    

---

## 🔹 Character

```csharp
char c = 'A';
```

Single quotes.

---

## 🔹 String

```csharp
string str = "Hello";
```

Double quotes.

---

# 🧩 3️⃣ var Keyword (Type Inference)

You can write:

```csharp
var x = 10;
var name = "Kiran";
```

Compiler automatically decides:

- x → int
    
- name → string
    

Important:

After assigning:

```csharp
var x = 10;
x = "hello"; ❌ ERROR
```

Type is fixed after initialization.

So var ≠ dynamic.

---

# 📦 4️⃣ Arrays

## Integer Array

```csharp
int[] vals = new int[5];
```

Or directly assign values:

```csharp
int[] vals = { 1, 2, 3, 4, 5 };
```

---

## String Array

```csharp
string[] strs = { "one", "two", "three" };
```

Arrays use square brackets `[]`.

---

# 📝 5️⃣ Format Strings (Placeholders)

```csharp
Console.WriteLine("{0}, {1}", i, str);
```

- `{0}` → first variable
    
- `{1}` → second variable
    

Modern and cleaner way:

```csharp
Console.WriteLine($"Value is {i}");
```

This is called **string interpolation**.

Much cleaner.

---

# ⚫ 6️⃣ Null Values

Null means:

> Variable has no value.

Example:

```csharp
object obj = null;
```

If you print it:

Nothing appears.

Important:

Value types (int, float) cannot be null unless nullable:

```csharp
int? x = null;
```

That `?` makes it nullable.

---

# 🔄 7️⃣ Type Conversion (Very Important)

There are two types:

---

## ✅ Implicit Conversion (Safe Conversion)

Smaller → Bigger type

```csharp
int i = 10;
long l = i;   // OK
```

Why?

Because long can store bigger values than int.

No data loss.

---

## ❌ Explicit Conversion (Casting Required)

Bigger → Smaller type

Example:

```csharp
long l = 100;
int i = (int)l;
```

You must cast.

Why?

Because smaller type may not hold large value.

---

# 🚨 Your Important Question:

## What happens if I assign long value to int?

Example:

```csharp
long l = 100;
int i = l;   // ❌ ERROR
```

You will get:

```
Cannot implicitly convert type 'long' to 'int'
```

Because:

- long → 64-bit
    
- int → 32-bit
    
- Possible data loss
    

---

## If You Force It:

```csharp
long l = 5000000000;
int i = (int)l;
Console.WriteLine(i);
```

This causes:

⚠ Overflow

The number will change to garbage value.

Because 5000000000 is too large for int.

---

# 🎯 Safe Example

```csharp
long l = 100;
int i = (int)l;
```

This works because 100 fits inside int range.

---

# 📊 Range Difference

|Type|Range|
|---|---|
|int|-2,147,483,648 to 2,147,483,647|
|long|Much larger range|

So always remember:

Small → Big = safe  
Big → Small = cast required

---

# 🔥 Float to Int Example

```csharp
float f = 2.9f;
int i = (int)f;
```

Output:

```
2
```

Decimal part removed (not rounded).

---

