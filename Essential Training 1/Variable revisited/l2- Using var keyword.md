
# ✅ 1️⃣ What is `var`?

`var` means:

> “Compiler, YOU decide the type based on the value I assign.”

This is called **implicit typing**.

The type is still decided at **compile time**, not runtime.

---

# ✅ 2️⃣ Basic Examples

### Example 1

```csharp
var x = 10;
```

Compiler sees `10` → that’s an `int`.

So internally this becomes:

```csharp
int x = 10;
```

---

### Example 2

```csharp
var x = 10.0;
```

Now compiler sees `10.0` → that’s a `double`.

So internally this becomes:

```csharp
double x = 10.0;
```

---

### Example 3

```csharp
var y = "Hello";
```

Compiler sees string literal → `string`.

Internally:

```csharp
string y = "Hello";
```

---

# ✅ 3️⃣ Important Rule

You **must initialize** a `var` variable at declaration.

❌ This is illegal:

```csharp
var x;   // ERROR
```

Because compiler doesn’t know the type.

---

# ✅ 4️⃣ `var` with Objects

Instead of writing:

```csharp
ShiftWorker e = new ShiftWorker();
```

You can write:

```csharp
var e = new ShiftWorker();
```

Compiler understands:

> “Oh, you're creating a ShiftWorker? Cool. `e` is a ShiftWorker.”

So this:

```csharp
var e = new ShiftWorker();
```

Is EXACTLY the same as:

```csharp
ShiftWorker e = new ShiftWorker();
```

No magic. Just shorter.

---

# ✅ 5️⃣ Full Example with Output

Let’s use your ShiftWorker example.

```csharp
using System;

public class ShiftWorker
{
    public string FirstName { get; set; }
    public TimeOnly ShiftStartTime { get; set; }
}

class Program
{
    static void Main()
    {
        var x = 10;
        var y = 10.0;
        var z = "Hello";

        Console.WriteLine(x.GetType());
        Console.WriteLine(y.GetType());
        Console.WriteLine(z.GetType());

        var e = new ShiftWorker();
        e.FirstName = "Kiran";
        e.ShiftStartTime = new TimeOnly(8, 30);

        Console.WriteLine($"Name: {e.FirstName}");
        Console.WriteLine($"Shift: {e.ShiftStartTime}");
    }
}
```

---

# ✅ Output

```
System.Int32
System.Double
System.String
Name: Kiran
Shift: 08:30
```

---

# ✅ 6️⃣ Very Important Clarification

`var` does NOT mean dynamic.

This is wrong thinking ❌:

> "var means type can change later."

Nope.

This will fail:

```csharp
var x = 10;
x = "Hello";   // ERROR
```

Because `x` is permanently an `int`.

---

# ✅ 7️⃣ When `var` is Required (Very Important)

Instructor mentioned:

> Sometimes we don’t even have a type name.

This happens with:

### 🔹 Anonymous Types

```csharp
var person = new
{
    FirstName = "Kiran",
    Age = 21
};
```

There is NO class name here.

You cannot write:

```csharp
SomeType person = new { ... }; // impossible
```

So `var` is required.

---

### 🔹 LINQ Queries (Very Common in Interviews)

```csharp
var numbers = new List<int> { 1, 2, 3, 4, 5 };

var evenNumbers = numbers.Where(n => n % 2 == 0);
```

The type of `evenNumbers` is:

```
IEnumerable<int>
```

But it's long and messy.

So we use `var`.

---

# ✅ 8️⃣ When Should You Use `var`?

✔ When type is obvious:

```csharp
var e = new ShiftWorker();
```

❌ When type is unclear:

```csharp
var result = GetSomething();  // Bad if unclear
```

Better:

```csharp
Employee result = GetSomething();
```

---

# 🎯 Interview-Level Understanding

`var`:

- Is strongly typed
    
- Is resolved at compile time
    
- Improves readability
    
- Reduces repetition
    
- Required for anonymous types
    
- Required for complex LINQ types
    

---

# 🔥 Golden Rule

> `var` removes the need to write the type — but it does NOT remove the type.

---

