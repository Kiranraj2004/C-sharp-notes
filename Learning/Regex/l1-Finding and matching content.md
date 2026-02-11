
I’ll break this into:

1. What is Regex?
    
2. Using `IsMatch()`
    
3. Using `RegexOptions`
    
4. Using `Match()` + `NextMatch()`
    
5. Using `Matches()`
    
6. Full example code + output
    
7. Interview summary
    

All clean and simple 👌

---

# 🔎 What is Regular Expression (Regex)?

A **Regular Expression** is a pattern used to search text.

Used for:

- Email validation
    
- Password validation
    
- Extracting numbers
    
- Finding capital words
    
- Log parsing
    
- Data cleaning
    

Namespace required:

```csharp
using System.Text.RegularExpressions;
```

⚠ Regex is NOT included by default — must import namespace.

---

# 🧪 Example Strings

We’ll use two strings:

```csharp
string testStr1 = "The Quick Brown Fox jumps over the Lazy Dog";
string testStr2 = "the quick brown fox jumps over the lazy dog";
```

---

# 1️⃣ Using `IsMatch()`

## 🔹 Purpose:

Returns `true` or `false`  
Checks if pattern exists in string.

---

## 🔹 Example Pattern: Capital Words

Pattern:

```csharp
@"[A-Z]\S+"
```

### What does this mean?

| Symbol  | Meaning                               |
| ------- | ------------------------------------- |
| `[A-Z]` | Any uppercase letter                  |
| `\S+`   | One or more non-whitespace characters |
| `@`     | Literal string (so \ is not escaped)  |

So this finds:  
👉 Words starting with capital letters

---

## ✅ Example Code

```csharp
using System;
using System.Text.RegularExpressions;

class Program
{
    static void Main()
    {
        string testStr1 = "The Quick Brown Fox";
        string testStr2 = "the quick brown fox";

        Regex capWords = new Regex(@"[A-Z]\S+");

        Console.WriteLine(capWords.IsMatch(testStr1));
        Console.WriteLine(capWords.IsMatch(testStr2));
    }
}
```

---

### 🖥 Output:

```
True
False
```

✔ First string has capital words  
✖ Second string does not

---

# 2️⃣ Using `RegexOptions`

Sometimes we want to ignore case.

---

## 🔹 Example: Ignore Case

```csharp
Regex noCase = new Regex("fox", RegexOptions.IgnoreCase);

Console.WriteLine(noCase.IsMatch(testStr1));
```

Even if text contains "Fox", it matches "fox".

---

### 🖥 Output:

```
True
```

✔ Case is ignored

---

# 3️⃣ Using `Match()` (One at a Time)

`Match()` returns the first match.  
You can use `NextMatch()` to move forward.

---

## ✅ Example

```csharp
using System;
using System.Text.RegularExpressions;

class Program
{
    static void Main()
    {
        string testStr1 = "The Quick Brown Fox";

        Regex capWords = new Regex(@"[A-Z]\S+");

        Match m = capWords.Match(testStr1);

        while (m.Success)
        {
            Console.WriteLine($"'{m.Value}' found at position {m.Index}");
            m = m.NextMatch();
        }
    }
}
```

---

### 🖥 Output:

```
'The' found at position 0
'Quick' found at position 4
'Brown' found at position 10
'Fox' found at position 16
```

🔥 Now you get:

- Exact word
    
- Its position in string
    

---

# 4️⃣ Using `Matches()` (All at Once)

Instead of looping manually, get all matches at once.

---

## ✅ Example

```csharp
using System;
using System.Text.RegularExpressions;

class Program
{
    static void Main()
    {
        string testStr1 = "The Quick Brown Fox";

        Regex capWords = new Regex(@"[A-Z]\S+");

        MatchCollection mc = capWords.Matches(testStr1);

        Console.WriteLine($"Found {mc.Count} matches");

        foreach (Match match in mc)
        {
            Console.WriteLine($"'{match.Value}' found at position {match.Index}");
        }
    }
}
```

---

### 🖥 Output:

```
Found 4 matches
'The' found at position 0
'Quick' found at position 4
'Brown' found at position 10
'Fox' found at position 16
```

---

# 🆚 Match vs Matches

|Match()|Matches()|
|---|---|
|Returns one match|Returns all matches|
|Use NextMatch()|Use foreach|
|More manual control|Cleaner for most cases|

---

# 🧠 Important Regex Concepts Used

### ✅ `@` Symbol

Used for literal strings.

Without @:

```csharp
"\\S+"
```

With @:

```csharp
@"\S+"
```

Much cleaner.

---

# 🔥 Real Interview Use Cases

- Validate email:
    
    ```csharp
    @"^[^@\s]+@[^@\s]+\.[^@\s]+$"
    ```
    
- Extract numbers:
    
    ```csharp
    @"\d+"
    ```
    
- Find phone numbers
    
- Parse logs
    
- Data cleaning in backend systems
    

---

# 🎯 Summary

✔ Import `System.Text.RegularExpressions`  
✔ `IsMatch()` → true/false  
✔ `Match()` → first match  
✔ `NextMatch()` → iterate manually  
✔ `Matches()` → all matches at once  
✔ `RegexOptions.IgnoreCase` → ignore casing  
✔ `@` → literal string

---

