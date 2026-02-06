
Parsing = **converting a string into another C# data type** (int, float, bool, etc.).

Example:\ `"123"` → `123` (int)\ `"1.23"` → `1.23f` (float)

---

# ✅ **1. Basic Parsing Using `Parse()`**

Every numeric type (int, float, double, bool) has a **Parse()** method.

### Example: convert string → int

int number = int.Parse("1");

Console.WriteLine(number); // 1

✔ Works if the string is valid\ ❌ Throws an exception if invalid → so we use **try/catch**

---

# ⚠️ **Why use try/catch?**

Because invalid input like `"abc"` causes:

```
FormatException: Input string was not in a correct format
```

Example:

try

{

    int n = int.Parse("1");

}

catch (Exception ex)

{

    Console.WriteLine(ex.Message);

}

---

# ✅ **2. Parsing Different Number Formats — `NumberStyles`**

Located in **System.Globalization** namespace.

Used when strings include:

- decimals → `"2.0"`
- thousands separators → `"3,000"`
- both → `"3,000.45"`

---

## **Parse floating‑point string into int**

int n = int.Parse("2.0", NumberStyles.Float);

✔ Works only if decimal part is `.0`\ ❌ `"2.5"` would fail

---

## **Allow thousands separators**

int n = int.Parse("3,000", NumberStyles.AllowThousands);

---

## **Allow multiple styles (use `|` for OR)**

int n = int.Parse("3,000.45",

    NumberStyles.Float | NumberStyles.AllowThousands);

This tells C#:

> “Expect a decimal and also expect commas.”

---

# ✅ **3. Parsing Other Types**

### Parse boolean

bool b = bool.Parse("True");

Console.WriteLine(b); // True

### Parse float

float f = float.Parse("1.235");

Console.WriteLine($"{f:F2}"); // 1.24 (rounded)

`:F2` → formats to 2 decimal places

---

# ⭐ **4. The Safer Method: `TryParse()`**

`TryParse` does NOT throw exceptions.

Instead:

- returns **true/false** (success/failure)
- gives the converted value through an **out parameter**

Example:

bool succeeded = int.TryParse("1", out int value);

  

Console.WriteLine(succeeded); // True

Console.WriteLine(value);     // 1

### Why use TryParse?

✔ No try/catch required\ ✔ Recommended for user input\ ✔ Cleaner, shorter code

Comparison:

|Method|Throws Exception?|Returns Value?|
|---|---|---|
|`Parse()`|Yes|As return value|
|`TryParse()`|No|Through `out` parameter|

---

# 🔍 **What is an `out` parameter?**

Function gives back value **through the parameter**, not the return value.

Example:

int.TryParse("123", out int result);

- `TryParse(...)` → returns `true` or `false`
- `result` → contains parsed integer

---

