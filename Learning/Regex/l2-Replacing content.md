
We’ll cover:

1. Basic `Replace()`
    
2. Replace with fixed text
    
3. Replace using custom logic (MatchEvaluator)
    
4. Example code + output
    
5. Interview takeaways
    

---

# 🔁 Regex Replace in C#

Namespace required:

```csharp
using System.Text.RegularExpressions;
```

---

# 🧪 Example String

```csharp
string testStr1 = "The Quick Brown Fox jumps over the Lazy Dog";
```

Regex pattern used:

```csharp
Regex capWords = new Regex(@"[A-Z]\S+");
```

### What does this match?

- Words starting with capital letter
    
- Followed by non-whitespace characters
    

Matches:

```
The
Quick
Brown
Fox
Lazy
Dog
```

---

# 1️⃣ Basic Replace (Fixed Replacement)

### Replace all capital words with `***`

---

## ✅ Code Example

```csharp
using System;
using System.Text.RegularExpressions;

class Program
{
    static void Main()
    {
        string testStr1 = "The Quick Brown Fox jumps over the Lazy Dog";

        Regex capWords = new Regex(@"[A-Z]\S+");

        string result = capWords.Replace(testStr1, "***");

        Console.WriteLine("Original: " + testStr1);
        Console.WriteLine("Replaced: " + result);
    }
}
```

---

### 🖥 Output

```
Original: The Quick Brown Fox jumps over the Lazy Dog
Replaced: *** *** *** *** jumps over the *** ***
```

✔ Every capital word replaced with `***`.

Simple and clean.

---

# 2️⃣ Replace Using Custom Logic (MatchEvaluator)

Now it gets interesting 🔥

Instead of replacing with fixed text, we can:

- Examine each match
    
- Apply logic
    
- Return dynamic replacement
    

---

## 🔹 Step 1: Create a Function

Function must:

- Take `Match` as parameter
    
- Return `string`
    

Example: Convert matched word to uppercase

---

## ✅ Code Example

```csharp
using System;
using System.Text.RegularExpressions;

class Program
{
    static string MakeUpper(Match m)
    {
        string s = m.ToString();

        if (m.Index == 0)   // If match is at beginning
            return s;       // Don't change it

        return s.ToUpper(); // Otherwise uppercase it
    }

    static void Main()
    {
        string testStr1 = "The Quick Brown Fox jumps over the Lazy Dog";

        Regex capWords = new Regex(@"[A-Z]\S+");

        string upperStr = capWords.Replace(testStr1, new MatchEvaluator(MakeUpper));

        Console.WriteLine("Original: " + testStr1);
        Console.WriteLine("Modified: " + upperStr);
    }
}
```

---

### 🖥 Output

```
Original: The Quick Brown Fox jumps over the Lazy Dog
Modified: The QUICK BROWN FOX jumps over the LAZY DOG
```

✔ First word ("The") remains same  
✔ Other capital words converted to ALL CAPS

---

# 🧠 What Happened Here?

`Replace()` has two versions:

### Version 1: Replace with string

```csharp
regex.Replace(text, "replacement");
```

### Version 2: Replace with function

```csharp
regex.Replace(text, MatchEvaluatorFunction);
```

In Version 2:

- Regex finds match
    
- Calls your function
    
- Your function decides replacement
    

This allows:

- Conditional replacements
    
- Smart formatting
    
- Data masking
    
- Custom transformations
    

---

# 🔥 Why This Is Powerful

You can do things like:

- Mask credit card numbers
    
- Replace numbers with doubled values
    
- Format phone numbers
    
- Capitalize specific words
    
- Modify based on position
    

---

# 💡 Bonus Example: Double All Numbers

```csharp
Regex numbers = new Regex(@"\d+");

string result = numbers.Replace("Total is 25 and tax is 5", m =>
{
    int value = int.Parse(m.Value);
    return (value * 2).ToString();
});

Console.WriteLine(result);
```

### 🖥 Output

```
Total is 50 and tax is 10
```

🔥 That’s real-world level usage.

---

# 🆚 Replace vs Match vs Matches

|Method|Purpose|
|---|---|
|`IsMatch()`|True/False|
|`Match()`|First match|
|`Matches()`|All matches|
|`Replace()`|Modify string|
