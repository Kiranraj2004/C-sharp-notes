

Loops allow a program to repeat actions multiple times. They are very useful when you need to process lists, arrays, strings, or perform repeated tasks.

This lesson explains two important loop types in C#:

✔ **for loop**\ ✔ **foreach loop**

---

# 🔹 **1. What is a _for loop_?**

A **for loop** is used when you know **exactly how many times** you want to repeat a block of code.

---

# 📌 **2. Structure of a for loop**

for (initialization; condition; increment)

{

    // code to run repeatedly

}

### 🔍 Explanation of parts:

1. **initialization**
    
    - Sets the starting value of the loop counter
    - Example: `int i = 0`
2. **condition**
    
    - The loop runs **as long as** this condition is `true`
    - Example: `i < myVal`
3. **increment**
    
    - Changes the loop counter every cycle
    - Example: `i++` (increases by 1)

---

# 🧪 **3. Example from transcript**

int myVal = 15;

  

for (int i = 0; i < myVal; i++)

{

    Console.WriteLine($"i is currently {i}");

}

### ✔ What happens?

- Loop starts at **i = 0**
- Runs while **i < 15**
- Stops when **i reaches 15**
- Prints values from **0 to 14**

So it runs **15 times**.

---

# 🔹 **4. What is a _foreach loop_?**

A **foreach loop** is used to go through **each item** in a collection like:

- Arrays
- Lists
- Strings (each character)

It is simpler than a `for` loop when working with collections.

---

# 📌 **5. Structure of a foreach loop**

foreach (type variable in collection)

{

    // code using variable

}

### ✔ Meaning:

- `variable` holds each element from the collection one by one
- You cannot change the collection’s size inside a foreach loop

---

# 🧪 **6. Example: Loop through an integer array**

int[] nums = { 3, 14, 15, 92, 6 };

  

foreach (int i in nums)

{

    Console.WriteLine($"i is currently {i}");

}

### Output:

```
3
14
15
92
6
```

The loop processes **each number in order**.

---

# 🔹 **7. foreach with Strings**

Strings are sequences of characters.\ So you can loop over each **character**.

---

# 🧪 **Example: Count how many 'O' characters are in a string**

string str = "This is a sample string for counting O's";

int count = 0;

  

foreach (char c in str)

{

    if (c == 'o' || c == 'O')

    {

        count++;

    }

}

  

Console.WriteLine($"Counted {count} O characters");

### ✔ What happens?

- Loop reads **every character**
- If character is `'O'` (or `'o'`), count increases
- Finally prints how many O’s were found

---

# 🎯 **8. When to use which loop?**

|Loop Type|Best Used When|
|---|---|
|**for loop**|You know the number of iterations (e.g., run 10 times)|
|**foreach loop**|You want to process each element in a collection (array, list, string)|
|**while / do-while**|When you want to loop until a condition becomes true|

---

# 📘 **Summary**

### 🟦 **For Loop**

- Good for repeating a fixed number of times.
- Has **initialization**, **condition**, **increment**.

### 🟩 **Foreach Loop**

- Best for looping through items in collections.
- Works with arrays, strings, lists, etc.
- Automatically moves through each element.

### 🟧 **Useful for**

- Counting characters
- Processing lists
- Running tasks many times
- Reading data row-by-row
