
# ✅ 1. Lambdas as Delegates – Core Idea

A **lambda expression** is just a shorter way to write an anonymous delegate.

Since events are based on delegates:

👉 You can use lambdas directly as event handlers.

Instead of:

```csharp
obj.ValueChanged += SomeMethod;
```

or

```csharp
obj.ValueChanged += delegate(string val) { ... };
```

You write:

```csharp
obj.ValueChanged += val => { ... };
```

Much cleaner ✅

---

# ✅ 2. Basic Example – Event with Lambda

---

## Step 1: Declare Delegate

```csharp
public delegate void MyEventHandler(string value);
```

---

## Step 2: Create Publisher Class

```csharp
using System;

class MyClass
{
    private string theVal;

    public event MyEventHandler ValueChanged;

    public string Val
    {
        get { return theVal; }
        set
        {
            theVal = value;

            // Trigger event
            ValueChanged?.Invoke(theVal);
        }
    }
}
```

---

## Step 3: Use Lambda as Event Handler

```csharp
class Program
{
    static void Main(string[] args)
    {
        MyClass obj = new MyClass();

        // Lambda used as event handler
        obj.ValueChanged += val =>
        {
            Console.WriteLine("Value changed to: " + val);
        };

        Console.WriteLine("Type something (type exit to quit):");

        string input;

        while ((input = Console.ReadLine()) != "exit")
        {
            obj.Val = input;
        }
    }
}
```

---

# ✅ Output

```
Type something:
hello
Value changed to: hello
world
Value changed to: world
exit
```

---

# ✅ What Just Happened?

When this runs:

```csharp
obj.Val = "hello";
```

1. Property setter runs
    
2. Event is triggered
    
3. Lambda function executes
    
4. Output printed
    

Lambda replaced named function completely 🔥

---

# ✅ Expression Lambda Version (Shorter)

If single statement:

```csharp
obj.ValueChanged += val => 
    Console.WriteLine("Value changed to: " + val);
```

Even cleaner ✅

---

# ✅ 3. Why Lambdas Are Preferred for Events

✔ Short  
✔ Readable  
✔ No extra method creation  
✔ Used heavily in UI frameworks

Example (Real World):

```csharp
button.Click += (sender, e) =>
{
    Console.WriteLine("Button clicked!");
};
```

---

# ✅ 4. Example Using Standard .NET Event Pattern

If using `EventHandler<T>`:

```csharp
obj.ObjChanged += (sender, e) =>
{
    Console.WriteLine(
        sender.GetType().Name +
        " changed property to: " +
        e.PropChanged
    );
};
```

This matches professional .NET style.

---

# ✅ 5. Now Let’s Talk About Func

`Func<>` is a built-in delegate type.

Instead of writing:

```csharp
public delegate int MyDelegate(int x);
```

We use:

```csharp
Func<int, int>
```

Format:

```
Func<input1, input2, ..., returnType>
```

Last type = return type

---

# ✅ 6. Simple Func Example

---

## Example 1 — Square Number

```csharp
using System;

class Program
{
    static void Main(string[] args)
    {
        Func<int, int> square = x => x * x;

        Console.WriteLine("Square of 5: " + square(5));
    }
}
```

---

### ✅ Output

```
Square of 5: 25
```

---

## Example 2 — Two Inputs

```csharp
Func<int, int, int> multiply = (a, b) => a * b;

Console.WriteLine("10 * 20 = " + multiply(10, 20));
```

---

### ✅ Output

```
10 * 20 = 200
```

---

## Example 3 — Boolean Return

```csharp
Func<int, bool> isGreaterThan10 = x => x > 10;

Console.WriteLine(isGreaterThan10(5));
Console.WriteLine(isGreaterThan10(15));
```

---

### ✅ Output

```
False
True
```

---

# ✅ 7. Passing Func as Parameter

```csharp
static void Calculate(int a, int b, Func<int, int, int> operation)
{
    Console.WriteLine("Result: " + operation(a, b));
}

static void Main()
{
    Calculate(5, 3, (x, y) => x + y);
    Calculate(5, 3, (x, y) => x * y);
}
```

---

### ✅ Output

```
Result: 8
Result: 15
```

This is very common in real-world applications.

---

# ✅ 8. Quick Comparison

|Type|Returns Value?|Example|
|---|---|---|
|Action|❌ No|Action|
|Func|✅ Yes|Func<int,int>|
|Predicate|✅ bool only|Predicate|

---

# q1


# ✅ Short Answer

❌ **No**, `Func<>` cannot have a `void` return type.

Because:

> In `Func<T1, T2, ..., TResult>`  
> 👉 The **last type parameter is always the return type**  
> 👉 `Func` must return something

---

# ✅ Why?

The definition of `Func<>` looks like this conceptually:

```csharp
Func<TInput, TResult>
```

OR

```csharp
Func<T1, T2, TResult>
```

The last generic parameter is **always the return type**.

So this is valid:

```csharp
Func<int, int> square = x => x * x;
```

But this is NOT valid:

```csharp
Func<int, void> something = x => Console.WriteLine(x); ❌
```

Because `void` cannot be used as a generic type argument.

---

# ✅ So What Do We Use Instead?

👉 We use **Action<>**

---

# ✅ Action = Takes Parameters, Returns Void

If you want:

- One parameter
    
- No return value
    

Use:

```csharp
Action<int>
```

---

# ✅ Example

```csharp
using System;

class Program
{
    static void Main()
    {
        Action<int> printNumber = x => Console.WriteLine("Number: " + x);

        printNumber(10);
    }
}
```

---

### ✅ Output

```
Number: 10
```

---

# ✅ Comparison Table (Very Important)

|Delegate Type|Parameters|Return Type|
|---|---|---|
|Func<T1, TResult>|Yes|Yes|
|Action|Yes|❌ void|
|Predicate|Yes|bool|

---

# ✅ More Examples

### 🔹 Func Example

```csharp
Func<int, int> square = x => x * x;
Console.WriteLine(square(5));
```

Output:

```
25
```

---

### 🔹 Action Example

```csharp
Action<string> greet = name =>
    Console.WriteLine("Hello " + name);

greet("Kiran");
```

Output:

```
Hello Kiran
```

---

### 🔹 Predicate Example

```csharp
Predicate<int> isEven = x => x % 2 == 0;

Console.WriteLine(isEven(4));
Console.WriteLine(isEven(5));
```

Output:

```
True
False
```

---

# ✅ Interview-Level Explanation

If interviewer asks:

> Can Func return void?

Answer:

"No. Func must always return a value because its last generic type argument represents the return type. If we need a delegate that returns void, we use Action."

---

# ✅ Quick Memory Trick

- **Func → Function → Returns value**
    
- **Action → Performs action → Returns nothing**
    
- **Predicate → Returns bool**
    

---
