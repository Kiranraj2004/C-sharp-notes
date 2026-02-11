
# 🚨 Why Regex Can Be Dangerous

Some regex patterns cause **catastrophic backtracking**.

That means:

- The regex engine keeps retrying combinations
    
- CPU usage spikes
    
- App freezes
    
- Possible Denial of Service (DoS)
    

Especially dangerous if:

- Input comes from users
    
- Input comes from APIs
    
- Input is very large
    

---

# 🔥 Example of a Bad Regex

Pattern from your transcript:

```
^(A+)+B
```

What this means:

|Part|Meaning|
|---|---|
|`A+`|One or more A’s|
|`(A+)+`|That group repeated|
|`B`|Ends with B|

Now imagine a string like:

```
AAAAAAAAAAAAAAAAAAAAAAAAAAAAA
```

There is NO `B`.

The regex engine tries every possible grouping of A’s before giving up.

That’s called **catastrophic backtracking**.

---

# 🧪 Without Timeout (Dangerous)

### Example Code

```csharp
using System;
using System.Text.RegularExpressions;
using System.Diagnostics;

class Program
{
    static void Main()
    {
        string input = new string('A', 10000);

        Regex badRegex = new Regex(@"^(A+)+B");

        Stopwatch sw = Stopwatch.StartNew();

        MatchCollection matches = badRegex.Matches(input);

        sw.Stop();

        Console.WriteLine($"Found {matches.Count} matches in {sw.Elapsed}");
    }
}
```

### 🖥 Output (example):

```
Found 0 matches in 00:00:05.342
```

⚠ For larger input, it could take MUCH longer.

---

# ✅ Solution: Use Regex Timeout

.NET allows you to set a timeout.

If regex runs longer than specified time →  
It throws `RegexMatchTimeoutException`.

---

# 🛡 How to Add Timeout

### Step 1: Define timeout

```csharp
int maxRegexTime = 1000; // 1000 ms = 1 second
TimeSpan timeout = TimeSpan.FromMilliseconds(maxRegexTime);
```

---

### Step 2: Pass timeout into Regex constructor

```csharp
Regex badRegex = new Regex(
    @"^(A+)+B",
    RegexOptions.None,
    timeout
);
```

---

### Step 3: Catch Exception

```csharp
catch (RegexMatchTimeoutException ex)
{
    Console.WriteLine("Regex took too long to execute.");
    Console.WriteLine($"Timeout value: {ex.MatchTimeout}");
}
```

---

# ✅ Full Safe Example

```csharp
using System;
using System.Text.RegularExpressions;

class Program
{
    static void Main()
    {
        string input = new string('A', 10000);

        int maxRegexTime = 1000;
        TimeSpan timeout = TimeSpan.FromMilliseconds(maxRegexTime);

        try
        {
            Regex badRegex = new Regex(
                @"^(A+)+B",
                RegexOptions.None,
                timeout
            );

            MatchCollection matches = badRegex.Matches(input);

            Console.WriteLine($"Found {matches.Count} matches.");
        }
        catch (RegexMatchTimeoutException ex)
        {
            Console.WriteLine("Regex took too long to execute.");
            Console.WriteLine($"Timeout was set to: {ex.MatchTimeout.TotalMilliseconds} ms");
        }
    }
}
```

---

# 🖥 Output (When Timeout Happens)

```
Regex took too long to execute.
Timeout was set to: 1000 ms
```

✔ Your program does NOT freeze  
✔ Instead, you safely handle the problem

---

# 🧠 What Is Backtracking?

Regex engine tries:

```
(A+)+
```

It:

- Groups A’s
    
- Tries different combinations
    
- Re-checks possibilities
    

For long input → exponential explosion.

That’s the danger.

---

# 🎯 When Should You Use Regex Timeouts?

✅ When processing:

- User input
    
- Uploaded files
    
- External API text
    
- Large log files
    

🚫 Maybe not necessary for:

- Small internal strings
    
- Controlled input
    

But honestly?  
In production apps → always safer to use it.

---

