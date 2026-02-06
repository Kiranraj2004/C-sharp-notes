

When you pass a value type (like `int`) to a function normally, C# sends a **copy** of the value.

So if the function changes its parameter, the original variable outside the function **does not change**.

### Example (Pass by Value)

using System;

  

void TestFunc1(int arg1)

{

    arg1 += 10;  // changes only the local copy

    Console.WriteLine($"Inside TestFunc1: arg1 = {arg1}");

}

  

int val1 = 10;

Console.WriteLine($"Before TestFunc1: val1 = {val1}");

  

TestFunc1(val1);

  

Console.WriteLine($"After TestFunc1: val1 = {val1}");

### ✅ Output

```
Before TestFunc1: val1 = 10
Inside TestFunc1: arg1 = 20
After TestFunc1: val1 = 10
```

📌 **Key Point:** `val1` stays `10` because the function only modified a copy.

---

## ✅ 2) `ref` Parameter: Pass **By Reference**

When you use `ref`, the function receives a **reference to the original variable**, not a copy.

✅ Any change inside the function **will reflect outside** too.

### Rules for `ref`

- The variable **must be initialized** before passing.
- Both function definition **and** function call must use `ref`.

### Example (`ref`)

using System;

  

void TestFunc2(ref int arg1)

{

    arg1 += 10;  // modifies the original variable

    Console.WriteLine($"Inside TestFunc2: arg1 = {arg1}");

}

  

int val1 = 10;

Console.WriteLine($"Before TestFunc2: val1 = {val1}");

  

TestFunc2(ref val1);

  

Console.WriteLine($"After TestFunc2: val1 = {val1}");

### ✅ Output

```
Before TestFunc2: val1 = 10
Inside TestFunc2: arg1 = 20
After TestFunc2: val1 = 20
```

📌 **Key Point:** Now `val1` becomes `20` because `ref` allowed direct modification.

---

## ✅ 3) Why the Compiler Forces `ref` in the Call?

Because C# wants the code to be **explicit and readable**.

If you write:

TestFunc2(val1); // ❌ error

C# complains:

> “Argument must be passed with the ref keyword”

So you must write:

TestFunc2(ref val1); // ✅ correct

---

## ✅ 4) `out` Parameter: Used to **Return Values**

`out` is used when a function should **produce** a value for the caller, rather than consume one.

Think of `out` like:

> “This parameter will be assigned inside the function and returned back.”

### Rules for `out`

- The variable **does NOT need to be initialized** before passing.
- The method **must assign** a value to every `out` parameter before returning.
- Both function definition **and** call must use `out`.

---

## ✅ Example: Return Multiple Values (Sum and Product)

The transcript starts building a function like `PlusTimes` that takes 2 ints and returns results through `out`.

using System;

  

void PlusTimes(int a, int b, out int sum, out int product)

{

    sum = a + b;

    product = a * b;

}

  

int x = 6, y = 4;

  

// out variables don't need prior initialization

PlusTimes(x, y, out int s, out int p);

  

Console.WriteLine($"x = {x}, y = {y}");

Console.WriteLine($"Sum = {s}");

Console.WriteLine($"Product = {p}");

### ✅ Output

```
x = 6, y = 4
Sum = 10
Product = 24
```

📌 **Key Point:** A function can only “return” one value normally, but `out` lets you return extra values.

---

## ✅ 5) Quick Difference: `ref` vs `out`

### `ref`

- Caller must provide an **existing value**
- Function may read & modify it

### `out`

- Caller provides an **empty variable**
- Function must assign it before return (used like output)

---

## ✅ 6) `TryParse` is a Real-World `out` Example

You already saw this in parsing:

bool ok = int.TryParse("123", out int result);

  

Console.WriteLine(ok);

Console.WriteLine(result);

### Output

```
True
123
```

---

