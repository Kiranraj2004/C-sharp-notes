
Loops repeat a block of code multiple times.\ While `for` loops are used when you know **how many times** to repeat,\ **while loops** run as long as a _condition stays true_.

---

# 🔹 **1. The `while` Loop**

A **while loop** keeps running **as long as its condition is true**.

### ✔ Basic structure:

while (condition)

{

    // code to execute repeatedly

}

### ✔ How it works:

1. The condition is checked **before** each loop cycle.
2. If `true` → loop runs.
3. If `false` → loop stops immediately.

---

# 🧪 **Example from the transcript**

string inputStr = "";

  

while (inputStr != "exit")

{

    inputStr = Console.ReadLine();

    Console.WriteLine($"You entered {inputStr}");

}

### ✔ What this does:

- Loop keeps running **until** the user types `"exit"`.
- Each time:
    - It reads user input
    - It prints what the user typed
- When `inputStr` becomes `"exit"`, the condition becomes `false` → loop ends.

### Example run:

```
John
You entered John
hello
You entered hello
stop
You entered stop
exit
```

Loop stops after `"exit"`.

---

# 🔍 **Key Points About `while`**

- Condition is checked **at the top**.
- If the condition is **false at the beginning**, the loop may **never run**.

Example:

string inputStr = "exit";

  

while (inputStr != "exit")

{

    // this will NEVER run

}

---

# 🔹 **2. The `do-while` Loop**

A **do‑while loop** is similar to a while loop, but:

### ✔ It **always runs at least once**.

### Structure:

do

{

    // code to run

}

while (condition);

### ✔ Main difference:

- Code block runs **first**
- Condition is checked **after** the loop body

---

# 🧪 **Example from the transcript**

string inputStr = "";

  

do

{

    inputStr = Console.ReadLine();

    Console.WriteLine($"You entered {inputStr}");

}

while (inputStr != "exit");

### ✔ What this does:

- Runs the code once (even if `inputStr` is already `"exit"`).
- After running once, condition is checked.
- If `inputStr != "exit"` → loop continues.
- Otherwise → loop stops.

---

# 🔍 **Why this matters**

### Example:

string inputStr = "exit";

- **while loop** → will NOT run even once.
- **do-while loop** → WILL run once (because condition is checked after).

---

# 📌 **3. Choosing the right loop**

|Loop Type|When to Use|
|---|---|
|**while loop**|When you want to run only if a condition is true **before** starting.|
|**do-while loop**|When you need the loop to run **at least once** no matter what.|

---

# 📘 **Summary**

### 🟦 **While Loop**

- Checks condition **before** running.
- Might not run at all.
- Good when you want to avoid running the loop unnecessarily.

### 🟩 **Do‑While Loop**

- Runs code **at least once**.
- Checks condition **after** the first run.
- Good for:
    - Menus
    - Input prompts
    - Repeating tasks until the user stops
