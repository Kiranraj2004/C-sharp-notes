

String interpolation is a modern and cleaner way to build strings in C#.\ Instead of using **index-based formatting** like `{0}`, `{1}`, etc., you embed variable names or expressions **directly inside the string**.

---

# ✅ 1. What is String Interpolation?

String interpolation allows you to write:

$"The car is a {year} {make} {model}"

instead of:

string.Format("The car is a {0} {1} {2}", year, make, model);

It is:

✔ Easier to read\ ✔ Easier to write\ ✔ Less error‑prone (no indexing mistakes)

---

# 🔹 2. Syntax of Interpolated Strings

Add a **$** before the opening quote:

$"Text {variable} more text"

- Variables go inside `{ }`
- You can still use formatting options like `:C`, `:F2`, etc.

---

# 🔧 **Example from transcript**

Old formatting:

Console.WriteLine("The {0} {1} {2} costs ${3}", year, make, model, price);

String interpolation (cleaner):

Console.WriteLine($"The {year} {make} {model} costs {price:C2}");

The output is the same — but the code is MUCH easier to understand.

---

# 🔹 3. Using Format Specifiers (Still Works!)

You can still use the format options from the earlier lesson:

$"{price:C2}"     // currency, 2 decimals

$"{miles:F1}"     // fixed point, 1 decimal

$"{percent:P0}"   // percentage, no decimals

Example:

Console.WriteLine($"Price: {price:C2}");

---

# 🔹 4. Using Expressions Inside Interpolation

You can put **entire expressions** inside `{ }`.

Example from transcript:

$"Kilometers: {miles * 1.6:F2}"

- `miles * 1.6` is calculated
- `F2` formats it to 2 decimal places

This is very powerful and commonly used.

---

# 🔹 5. Escaping Curly Braces `{}`

Since `{ }` is used for interpolated expressions,\ to print a literal brace → use **double braces**:

$"The value is {{ {miles} }} "

Output:

```
The value is { 12000 }
```

Where:

- `{{` prints a literal `{`
- `}}` prints a literal `}`

---

# 🔹 6. Why Use String Interpolation?

### ✔ More readable

You see variable names directly in the string.

### ✔ No index math

You don’t need to do mental mapping like `{2} = model`.

### ✔ Supports formatting

All format functionality remains available.

### ✔ Can embed expressions

Allows inline calculations.

---

# 📘 Summary Table

|Feature|Example|Purpose|
|---|---|---|
|Basic interpolation|`$"Car: {make}"`|Insert variable|
|Formatting|`$"{price:C2}"`|Currency|
|Expression|`$"{miles * 1.6:F1}"`|Calculate while printing|
|Literal braces|`"{{ }}"`|Print real `{}`|
|No indexes needed|`{year}` vs `{0}`|Easy to read|

---
