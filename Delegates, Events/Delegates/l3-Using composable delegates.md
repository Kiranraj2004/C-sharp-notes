
# ✅ 1. What Are Composable Delegates?

Composable delegates (also called **Multicast Delegates**) allow you to:

> 🔗 Chain multiple methods together into one delegate  
> 📞 Call all of them using a single function call

---

# ✅ 2. How Does It Work?

You use:

- `+` or `+=` → to add methods
    
- `-` or `-=` → to remove methods
    

Example concept:

```
F1 → Add
F2 → Multiply

All = F1 + F2
```

Calling:

```
All(10, 20);
```

Will execute:

```
Add(10,20)
Multiply(10,20)
```

---

# ✅ 3. Important Rules

When using multicast delegates:

### 🔹 Rule 1: Execution Order

Delegates are called **in the order they were added**.

---

### 🔹 Rule 2: Return Value

If delegate has a return type:

👉 Only the **last delegate’s return value** is returned.

---

### 🔹 Rule 3: Exception Handling

If one delegate throws an exception:

❌ Remaining delegates will NOT execute.

---

### 🔹 Rule 4: Passing Data Between Delegates

If you want one delegate to affect the next:

👉 Use `ref` parameters.

---

# ✅ 4. Basic Composable Delegate Example

---

## Step 1: Define Delegate

```csharp
public delegate int MyDelegate(int a, int b);
```

---

## Step 2: Create Methods

```csharp
public static int Add(int a, int b)
{
    Console.WriteLine("Add: " + (a + b));
    return a + b;
}

public static int Multiply(int a, int b)
{
    Console.WriteLine("Multiply: " + (a * b));
    return a * b;
}
```

---

## Step 3: Chain Delegates

```csharp
class Program
{
    public delegate int MyDelegate(int a, int b);

    public static int Add(int a, int b)
    {
        Console.WriteLine("Add: " + (a + b));
        return a + b;
    }

    public static int Multiply(int a, int b)
    {
        Console.WriteLine("Multiply: " + (a * b));
        return a * b;
    }

    static void Main(string[] args)
    {
        MyDelegate f1 = Add;
        MyDelegate f2 = Multiply;

        // Chain delegates
        MyDelegate all = f1 + f2;

        int result = all(10, 20);

        Console.WriteLine("Returned Value: " + result);
    }
}
```

---

# ✅ Output

```
Add: 30
Multiply: 200
Returned Value: 200
```

⚠ Notice:

- Both methods executed.
    
- Only **Multiply's return value (200)** was returned.
    

---

# ✅ 5. Removing a Delegate

You can remove like this:

```csharp
all -= f1;
all(20, 20);
```

---

### Output After Removing Add

```
Multiply: 400
Returned Value: 400
```

Only Multiply runs now ✅

---

# ✅ 6. Advanced Example Using ref Parameters

This allows one delegate to modify data for the next one.

---

## Step 1: Delegate with ref

```csharp
public delegate void MyDelegate(ref int a, ref int b);
```

---

## Step 2: Methods

```csharp
public static void Func1(ref int a, ref int b)
{
    Console.WriteLine("Before Change - Add: " + (a + b));
    b += 20;
}

public static void Func2(ref int a, ref int b)
{
    Console.WriteLine("Multiply: " + (a * b));
}
```

---

## Step 3: Chain and Execute

```csharp
class Program
{
    public delegate void MyDelegate(ref int a, ref int b);

    public static void Func1(ref int a, ref int b)
    {
        Console.WriteLine("Add: " + (a + b));
        b += 20;
    }

    public static void Func2(ref int a, ref int b)
    {
        Console.WriteLine("Multiply: " + (a * b));
    }

    static void Main(string[] args)
    {
        int A = 10;
        int B = 20;

        MyDelegate f1 = Func1;
        MyDelegate f2 = Func2;

        MyDelegate chain = f1 + f2;

        chain(ref A, ref B);
    }
}
```

---

# ✅ Output

```
Add: 30
Multiply: 400
```

### Why 400?

Step-by-step:

- A = 10, B = 20
    
- Func1 → 10 + 20 = 30
    
- Func1 increases B → B = 40
    
- Func2 → 10 × 40 = 400
    

🔥 The second delegate receives modified value.

---

# ✅ Real-World Usage

Composable delegates are used heavily in:

- Event handling
    
- Logging systems
    
- Plugin architectures
    
- Notification systems
    

Example:

```csharp
button.Click += LogClick;
button.Click += SaveToDatabase;
button.Click += ShowMessage;
```

One click → multiple operations execute.


---

# ✅ Summary Table

|Feature|Composable Delegate|
|---|---|
|Chain multiple methods|✅|
|Execution order maintained|✅|
|Last return value returned|✅|
|Remove method using -|✅|
|Can pass data via ref|✅|

---

