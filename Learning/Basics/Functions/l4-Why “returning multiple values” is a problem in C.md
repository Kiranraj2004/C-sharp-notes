

Normally, a function can return only **one value** using the `return` statement:

int Add(int a, int b) => a + b;

But sometimes you need to return **more than one result**, like:

- sum and product
- min and max
- success flag + computed value

---

## ✅ Option 1 (Older style): Using `out` parameters

C# provides the `out` keyword to return extra values through parameters.

### Example: sum and product with `out`

using System;

  

static void PlusTimes_Out(int a, int b, out int sum, out int product)_

_{_

    _sum = a + b;_

    _product = a * b;_

_}_

_  

int x = 6, y = 12;

  
_

_PlusTimes_Out(x, y, out int s, out int p);

  

Console.WriteLine($"Sum = {s}");

Console.WriteLine($"Product = {p}");

### Output

```
Sum = 18
Product = 72
```

### ✅ Pros / ❌ Cons of `out`

✅ Works in all modern C# versions\ ✅ Useful when one “main” return isn’t enough\ ❌ Can be **hard to read** when there are many outputs\ ❌ Parameters usually mean “inputs”, but with `out` they become outputs → less intuitive

---

## ✅ Option 2 (Modern, clean): Tuples (C# 7+)

### What is a tuple?

A **tuple** is a lightweight structure that groups multiple values into one return value.

You write tuples using parentheses:

(int a, int b) tup = (5, 10);

---

# ✅ Tuple basics from transcript

## 1) Tuple with **named elements**

(int a, int b) tup1 = (5, 10);

  

// Access by name

tup1.b = 20;

  

Console.WriteLine($"tup1.a = {tup1.a}, tup1.b = {tup1.b}");

### Output

```
tup1.a = 5, tup1.b = 20
```

---

## 2) Tuple with `var` (auto names: `Item1`, `Item2`, …)

var tup2 = ("Hello", 3.14f);

  

// Access using Item1/Item2

tup2.Item1 = "New String";

  

Console.WriteLine($"tup2.Item1 = {tup2.Item1}, tup2.Item2 = {tup2.Item2}");

### Output

```
tup2.Item1 = New String, tup2.Item2 = 3.14
```

> If you don’t name tuple fields yourself, C# uses default names: `Item1`, `Item2`, etc.

---

# ✅ Returning multiple values from a function using tuples

Instead of `out`, return a tuple.

## Example: `PlusTimes` returning `(sum, product)`

using System;

  

static (int sum, int product) PlusTimes(int a, int b)

{

    return (a + b, a * b);

}

  

var result = PlusTimes(6, 12);

  

Console.WriteLine($"Sum = {result.sum}");

Console.WriteLine($"Product = {result.product}");

### Output

```
Sum = 18
Product = 72
```

✅ Notice how readable this is:

- The function clearly returns `(sum, product)`
- You access results as `result.sum` and `result.product`

---

# ⭐ Even nicer: Tuple deconstruction (optional but common)

Instead of storing in `result`, you can unpack directly:

using System;

  

static (int sum, int product) PlusTimes(int a, int b)

    => (a + b, a * b);

  

var (sum, product) = PlusTimes(6, 12);

  

Console.WriteLine($"Sum = {sum}");

Console.WriteLine($"Product = {product}");

### Output

```
Sum = 18
Product = 72
```

---

# ✅ Quick Summary (Revision-Friendly)

### Ways to return multiple values in C\

## ✅ `out` parameters

- Function returns values via parameters
- Works but can reduce readability

## ✅ Tuples (C# 7+)

- Return multiple values cleanly
- Lightweight and easy to read
- Can name fields (`sum`, `product`) or use default (`Item1`, `Item2`)

---

## 🎯 When to use what?

- Use **tuples** for simple grouped returns (sum/product, min/max, etc.)
- Use a **custom class/record** if the return has many fields or needs strong domain meaning (e.g., `UserProfile`, `InvoiceSummary`)
