
# 1️⃣ Arithmetic Operators (Math Operations)

Used for numbers.

|Operator|Meaning|Example|
|---|---|---|
|`+`|Addition|`x + y`|
|`-`|Subtraction|`x - y`|
|`*`|Multiplication|`x * y`|
|`/`|Division|`x / y`|
|`%`|Modulus (remainder)|`x % y`|

---

## Example:

```csharp
int x = 10;
int y = 5;

Console.WriteLine(x / y * x);
```

Important:

Division of integers gives integer result.

```
10 / 5 = 2
2 * 10 = 20
```

---

# 🧵 String Addition (Concatenation)

When you use `+` with strings:

```csharp
string a = "Hello";
string b = "World";

Console.WriteLine(a + b);
```

Output:

```
HelloWorld
```

So `+` works differently for strings → it joins them.

---

# 2️⃣ Increment and Decrement

## Increment

```csharp
x++;
```

Same as:

```csharp
x = x + 1;
```

## Decrement

```csharp
y--;
```

Same as:

```csharp
y = y - 1;
```

---

# 3️⃣ Compound Assignment Operators

Shorter way of writing math operations.

|Normal Form|Short Form|
|---|---|
|`a = a + b`|`a += b`|
|`a = a - b`|`a -= b`|
|`a = a * b`|`a *= b`|
|`a = a / b`|`a /= b`|

---

## Example:

```csharp
string a = "Hello ";
string b = "World";

a += b;
Console.WriteLine(a);
```

Output:

```
Hello World
```

---

# 4️⃣ Comparison Operators

Used to compare values.

They return **true or false**.

|Operator|Meaning|
|---|---|
|`>`|Greater than|
|`<`|Less than|
|`>=`|Greater or equal|
|`<=`|Less or equal|
|`==`|Equal|
|`!=`|Not equal|

---

Example:

```csharp
x > y
```

Returns:

```
true or false
```

---

# 5️⃣ Logical Operators

Used for decision-making.

They return Boolean (true/false).

---

## 🔹 Logical AND (`&&`)

```csharp
x > y && y >= 5
```

True only if BOTH conditions are true.

---

## 🔹 Logical OR (`||`)

```csharp
x > y || y >= 5
```

True if at least ONE condition is true.

---

## 🔹 Logical NOT (`!`)

Reverses result.

```csharp
!(x > y)
```

If true → becomes false.

---

### Important Concept

`&&` needs both true  
`||` needs at least one true

---

# 6️⃣ Null Coalescing Operator (`??`)

This is very useful.

It means:

👉 “If left side is NOT null, use it.”  
👉 “If left side is null, use right side.”

---

## Example:

```csharp
string str = null;

Console.WriteLine(str ?? "Unknown");
```

Output:

```
Unknown
```

Because `str` is null.

---

If:

```csharp
string str = "Hello";
```

Then:

```
Hello
```

---

# 7️⃣ Null Coalescing Assignment (`??=`)

This assigns value only if variable is null.

---

Normal way:

```csharp
if (str == null)
{
    str = "New Value";
}
```

Short way:

```csharp
str ??= "New Value";
```

If str is null → assign  
If not null → do nothing

---

# 🔥 Important Operator Behavior (Order of Operations)

Like math:

1. `*`, `/`
    
2. `+`, `-`
    
3. Comparison
    
4. Logical operators
    

So:

```csharp
x / y * x
```

Evaluates left to right.

---

# 🧠 Real Understanding Example

If:

```csharp
int x = 10;
int y = 5;

x++;
y--;
```

Now:

```
x = 11
y = 4
```

If you check:

```csharp
x > y && y >= 5
```

11 > 4 → true  
4 >= 5 → false

true && false → false

---

If you check:

```csharp
x > y || y >= 5
```

true || false → true

---

# 🎯 Interview-Level Summary

Operators in C# are divided into:

- Arithmetic
    
- Comparison
    
- Logical
    
- Assignment
    
- Null-coalescing
    

Logical operators return Boolean values and are used in control flow statements like if and loops.

---

# 🚀 Bonus (Modern & Cleaner Way)

Instead of:

```csharp
Console.WriteLine("{0}", x);
```

Use string interpolation:

```csharp
Console.WriteLine($"Value is {x}");
```

Much cleaner and modern.

---

# 🧩 Quick Cheat Sheet

```
+   -   *   /   %
++  --
+=  -=  *=  /=
>   <   >=  <=  ==  !=
&&  ||  !
??  ??=
```

---
