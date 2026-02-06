

Programs need to **make decisions** based on data.

Examples:

- Bank balance check
    
- Login validation
    
- Age verification
    
- Range checks
    

C# provides multiple ways to control program flow.  
The **first and most common** is the `if` statement.

---

## 1️⃣ Basic `if` Statement

### Syntax:

```csharp
if (condition)
{
    // code runs if condition is true
}
```

---

### Example:

```csharp
int theVal = 50;

if (theVal == 50)
{
    Console.WriteLine("theVal is 50");
}
```

⚠ Important:

- `==` is used for **comparison**
    
- `=` is used for **assignment**
    

---

## 2️⃣ `if – else` Statement

Used when you want an alternative path.

### Syntax:

```csharp
if (condition)
{
    // true block
}
else
{
    // false block
}
```

---

### Example:

```csharp
int theVal = 51;

if (theVal == 50)
{
    Console.WriteLine("theVal is 50");
}
else
{
    Console.WriteLine("theVal is something else");
}
```

Only **one block** executes.

---

## 3️⃣ Multiple Conditions – `else if`

Used to check multiple logical cases.

### Syntax:

```csharp
if (condition1)
{
}
else if (condition2)
{
}
else
{
}
```

---

### Example:

```csharp
int theVal = 55;

if (theVal == 50)
{
    Console.WriteLine("theVal is 50");
}
else if (theVal >= 51 && theVal <= 60)
{
    Console.WriteLine("theVal is between 51 and 60");
}
else
{
    Console.WriteLine("theVal is something else");
}
```

---

### Important Notes:

- Conditions are checked **top to bottom**
    
- First true condition executes
    
- Remaining blocks are skipped
    
- No practical limit, but:
    
    - More than 4–5 `else if` → code becomes messy
        
    - Better to use `switch`
        

---

## 4️⃣ Logical Operators Used in `if`

|Operator|Meaning|
|---|---|
|`==`|Equal|
|`!=`|Not equal|
|`>`|Greater than|
|`<`|Less than|
|`>=`|Greater or equal|
|`<=`|Less or equal|
|`&&`|AND|
|`||

---

### Example:

```csharp
if (theVal >= 51 && theVal <= 60)
{
    Console.WriteLine("In range");
}
```

Both conditions must be true.

---

## 5️⃣ Ternary Operator (`?:`)

Used to **shorten simple if–else statements**.

---

### Normal `if–else`:

```csharp
if (theVal < 50)
{
    Console.WriteLine("theVal is small");
}
else
{
    Console.WriteLine("theVal is large");
}
```

---

### Ternary Version:

```csharp
Console.WriteLine(
    theVal < 50 ? "theVal is small" : "theVal is large"
);
```

---

### Syntax:

```csharp
condition ? value_if_true : value_if_false
```

---

### How It Works:

- Condition checked first
    
- If true → left value chosen
    
- If false → right value chosen
    
- Result is passed to `WriteLine`
    

---

## 6️⃣ When to Use Ternary

✔ Simple conditions  
✔ One-line decisions  
✔ Cleaner code

❌ Avoid for complex logic  
❌ Avoid nested ternary (hard to read)

---

## 7️⃣ Key Differences (Very Important)

|Feature|`if-else`|Ternary|
|---|---|---|
|Readability|High|Medium|
|Complexity|Handles complex logic|Best for simple checks|
|Lines of code|More|Less|

---

## 🎯 Interview-Level Explanation

If asked:

**How do conditionals work in C#?**

Answer:

> C# uses `if`, `else if`, and `else` statements to make decisions based on Boolean expressions. For simple conditions, the ternary operator can be used to shorten an `if-else` into a single expression.

Clean. Professional.

---

## 🧩 Common Beginner Mistakes

❌ Using `=` instead of `==`

```csharp
if (x = 10)  // ❌ ERROR
```

✔ Correct:

```csharp
if (x == 10)
```

---

❌ Too many `else if` blocks

✔ Use `switch` when values are discrete.

---

## 🚀 Quick Summary

- `if` checks a condition
    
- `else` runs if condition is false
    
- `else if` handles multiple cases
    
- Logical operators combine conditions
    
- Ternary operator shortens simple decisions
    

