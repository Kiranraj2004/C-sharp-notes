
Loops normally run until their ending condition is met.\ But sometimes, you want to:

✔ Stop the loop early\ ✔ Skip certain iterations

For this, C# provides two special statements:

- **`break`**
- **`continue`**

---

# 🔹 **1. The `break` Statement**

### ✔ What it does:

`break` **immediately stops** the loop—no further iterations happen.

### ✔ When to use:

- When you’ve found what you're looking for.
- When continuing the loop is unnecessary.
- When you want to exit early for efficiency.

---

## 🧪 Example from transcript:

You have a list of integers, and you want to find the **first value ≥ 40**:

foreach (int val in values)

{

    if (val >= 40)

        break;

  

    Console.WriteLine(val);

}

### ✔ What happens:

- Loop prints values until it encounters something ≥ 40.
- When `41` appears → `break` runs → **loop stops immediately**.
- No more values are processed after that.

---

# 🔍 Summary of `break`:

|Behavior|Meaning|
|---|---|
|Stops loop|Yes|
|Executes remaining loop code?|No|
|Goes to next iteration?|No — loop ends completely|

---

# 🔹 **2. The `continue` Statement**

### ✔ What it does:

`continue` **skips the remaining code in the current iteration**\ and jumps directly to the **next iteration** of the loop.

### ✔ When to use:

- When you want to _ignore_ certain values.
- When some iterations should be skipped based on a condition.

---

## 🧪 Example from the transcript:

Skip all values between 20 and 29:

foreach (int val in values)

{

    if (val >= 20 && val <= 29)

        continue;

  

    Console.WriteLine(val);

}

### ✔ What happens:

- If the value is between **20 and 29**, the loop skips the `WriteLine` and moves to the next number.
- Values like 23 or 28 are ignored.
- All other values are printed normally.

---

# 🔍 Summary of `continue`:

|Behavior|Meaning|
|---|---|
|Skips current iteration|Yes|
|Checks next iteration?|Yes|
|Exits loop completely?|No|

---

# 📝 Quick Comparison

|Feature|`break`|`continue`|
|---|---|---|
|Stops the entire loop|✔ Yes|✖ No|
|Skips only current iteration|✖ No|✔ Yes|
|Useful for "stop when found"|✔|✖|
|Useful for "skip unwanted items"|✖|✔|

---

# 📌 **Practical Uses**

### ✔ Use `break` when:

- Searching for an element
- Avoiding unnecessary extra work
- Loop must stop early

### ✔ Use `continue` when:

- Filtering values
- Skipping certain items
- Ignoring cases like zeros, negatives, empty strings, etc.

---

# 📘 Final Summary

- **`break`** → stops loop completely
- **`continue`** → skips current iteration only
- Both are used to **control loop flow more precisely**
- They help simplify logic and avoid unnecessary processing
