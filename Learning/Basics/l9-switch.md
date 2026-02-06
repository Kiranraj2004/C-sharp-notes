

# 📘 **C# — Conditionals with `switch` (Simple Notes)**

## ✅ **1. What is a `switch` statement?**

A `switch` statement is another way to make decisions in your code—similar to `if-else`, but cleaner and easier when you have **many conditions**.

Use `switch` when:

- There are many values to compare.
- Using multiple `if-else-if` conditions becomes messy and hard to read.

---

# 📌 **2. Basic Structure of a `switch`**

switch (expression)

{

    case value1:

        // code

        break;

  

    case value2:

        // code

        break;

  

    default:

        // code when no case matches

        break;

}

### **Explanation**

- **expression** → the value you want to test (e.g., an integer, string, char, enum, etc.)
- **case value:** → code that runs if `expression` matches `value`
- **break;** → stops the switch, and prevents running the next case (mandatory in most cases)
- **default:** → runs if _none_ of the cases match (similar to `else`)

---

# 🧪 **3. Example from the transcript**

int theVal = 50;

  

switch (theVal)

{

    case 50:

        Console.WriteLine("theVal is 50");

        break;

  

   .WriteLine("theVal is something else");

        break;

}

---

# 🔍 **4. How it works**

### ✔ If `theVal = 50`

→ It prints: **"theVal is 50"**

### ✔ If `theVal = 53`

→ It matches the group of cases **52, 53, 54**\ → It prints: **"theVal is between 52 and 54"**

### ✔ If `theVal = 60`

→ No cases match\ → Executes **default**\ → Prints: **"theVal is something else"**

---

# 🎯 **5. Group```csharp

case 52: case 53: case 54: Console.WriteLine("theVal is between 52 and 54"); break;

````
This avoids writing the same code again and again.

---

# 🤔 **6. Why do we need `break`?**
- Without `break`, the program would continue to the next case (known as “fall-through”).
- `break` stops the switch execution immediately.

---

# 🎁 **7. What can a `switch` test?**
Originally, only integer types were allowed.  
But **from C# 7 onward**, the expression can be:

- `int`
- `string`
- `char`
- `bool`
- `enum`
- Any non-null value

So this is valid now:

```csharp
switch (day)
{
    case "Monday":
        ...
}
````

---

# 📌 **8. When to use `if-else` vs `switch`?**

### ✔ Use **if-else** when:

- You have a few conditions (2–4)
- Conditions use relational operators (`>`, `<`, `>=`, comparisons between variables)

### ✔ Use **switch** when:

- You compare the **same value** against many **constant values**
- E.g., many menu options, status codes, categories

---

# 📝 **Summary**

|Concept|Meaning|
|---|---|
|`switch`|Used for multiple comparisons with a single value|
|`case`|A possible value that matches the switch expression|
|`break`|Stops the switch block|
|`default`|Executes if no case matches|
|Grouping cases|Multiple cases can share the same code|
|Can test many types|int, string, char, enum, bool (C# 7+)|
