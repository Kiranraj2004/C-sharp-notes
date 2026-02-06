 
# ✅ 1) What is String Formatting?

String formatting is a way to **insert variable values inside a string** and control **how they appear** (like decimals, currency symbols, column spacing, percentages, etc.).

You’ve already seen the basic placeholder style:

Console.WriteLine("Value is {0}", val);

But C# lets you **add formatting options** inside the placeholder.

---

# ✅ 2) General Placeholder Pattern

The general format used in the transcript is:

{index[,alignment][:formatSpecifier]}

### 🔹 Parts explained:

### ✅ **Index**

- Which argument to insert.
- `{0}` inserts the first argument, `{1}` inserts the second, etc.

### ✅ **Alignment (optional)**

- Controls spacing (useful for printing tables).
- Example: `{0,12}` makes a column width of **12 characters**.

### ✅ **Format Specifier (optional)**

- Controls how numbers look (currency, decimals, percent, etc.)
- Comes after a colon: `{0:C}`

---

# ✅ 3) Common Format Specifiers (mentioned in transcript)

Here are the ones used:

## 🔢 Number / General

### ✅ `D` — Decimal (integers)

- Mostly used with integers
- Can add leading zeros with precision

Console.WriteLine("{0:D4}", 12);   // 0012

### ✅ `N` — Number format (commas + decimals)

Console.WriteLine("{0:N}", 12345);   // 12,345.00 (depends on culture)

### ✅ `F` — Fixed-point (fixed decimals)

Console.WriteLine("{0:F2}", 12.3456);  // 12.35

### ✅ `G` — General

- Default “best” representation
- For integers, often looks like normal integer output.
- For decimals, keeps meaningful decimals.

Console.WriteLine("{0:G}", 12.3400); // 12.34

## 🔬 Scientific

### ✅ `E` — Exponential (scientific notation)

Console.WriteLine("{0:E}", 1234.5); // 1.234500E+003

## 💰 Currency

### ✅ `C` — Currency

Console.WriteLine("{0:C}", 2500);   // ₹2,500.00 (symbol depends on culture settings)

## 📊 Percent

### ✅ `P` — Percentage

- Multiplies by 100 and adds %

Console.WriteLine("{0:P}", 0.25);   // 25.00 %

---

# ✅ 4) Formatting Integers vs Decimals (as in transcript)

### Example (integer `val1`)

Console.WriteLine("{0:D4}", val1);

Console.WriteLine("{0:N}", val1);

Console.WriteLine("{0:F}", val1);

Console.WriteLine("{0:G}", val1);

### Example (decimal `val2`)

Console.WriteLine("{0:E}", val2);

Console.WriteLine("{0:N}", val2);

Console.WriteLine("{0:F}", val2);

Console.WriteLine("{0:G}", val2);

📌 **Important idea:** Some format specifiers behave differently depending on whether the value is an `int` or a `decimal/double`.

---

# ✅ 5) Precision Specifier (Very Important)

You can add a number after the format code to control **precision**.

### Examples from transcript:

- `D6` → total width 6 digits (leading zeros)
- `N2` → 2 decimal places
- `F1` → 1 decimal place
- `G3` → 3 digits (may switch to scientific form)

Console.WriteLine("{0:D6}", 123);  // 000123

Console.WriteLine("{0:N2}", 1234.567); // 1,234.57

Console.WriteLine("{0:F1}", 12.34); // 12.3

Console.WriteLine("{0:G3}", 12345); // 1.23E+04 (can happen)

---

# ✅ 6) Alignment Specifier (Formatting in Columns)

Alignment helps make output look like a **table**.

### Format:

{index, width}

Example: width 12:

Console.WriteLine("{0,12}{1,12}{2,12}{3,12}", q1, q2, q3, q4);

This makes each column exactly **12 characters wide**, giving clean alignment.

📌 If the content is smaller than the width, spaces are added.

---

# ✅ 7) Transcript’s Table Example (Quarters + Sales + Percentages)

The transcript prints:

1. Quarter headings aligned in columns
2. Sales formatted as currency
3. International mix formatted as percentage with varying precision

### Quarter Headings (aligned)

Console.WriteLine("{0,12}{1,12}{2,12}{3,12}", quarters[0], quarters[1], quarters[2], quarters[3]);

### Sales row as Currency (C0 = currency with 0 decimals)

Console.WriteLine("{0,12:C0}{1,12:C0}{2,12:C0}{3,12:C0}", sales[0], sales[1], sales[2], sales[3]);

### Percent row as Percent (P0, P1, P2)

Console.WriteLine("{0,12:P0}{1,12:P0}{2,12:P1}{3,12:P2}", mix[0], mix[1], mix[2], mix[3]);

📌 **P0** = 0 decimals\ 📌 **P1** = 1 decimal\ 📌 **P2** = 2 decimals

---

# ✅ 8) Key Takeaways (Easy Revision)

### ⭐ What you learned:

- Format placeholders can include **alignment and formatting**
- Numeric formatting codes control how numbers appear:
    - `D` integer digits
    - `N` thousands separators
    - `F` fixed decimals
    - `G` general
    - `E` scientific notation
    - `C` currency
    - `P` percentage
- Precision changes digits / decimals
- Alignment makes console output look like tables
- C# has rich formatting support, and docs list many more specifiers

---
