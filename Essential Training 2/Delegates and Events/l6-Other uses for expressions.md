
# 🧠 1️⃣ What is an Expression-Bodied Member?

Normally we write methods like this:

```csharp
public string GetName()
{
    return fName;
}
```

With expression-bodied syntax:

```csharp
public string GetName() => fName;
```

That’s it.

If the method has **only one expression**, you can use `=>`.

---

# 🟢 2️⃣ Expression-Bodied Method

### Example

```csharp
using System;

class Person
{
    private string fName;

    public Person(string name)
    {
        fName = name;
    }

    public string GetName() => fName;
}

class Program
{
    static void Main()
    {
        Person p = new Person("Kiran");
        Console.WriteLine(p.GetName());
    }
}
```

---

### 🔥 Output

```
Kiran
```

---

# 🟢 3️⃣ Expression-Bodied Property (Getter)

Normally:

```csharp
public string FirstName
{
    get
    {
        return fName;
    }
}
```

Short version:

```csharp
public string FirstName => fName;
```

Cleaner.

---

## Example

```csharp
using System;

class Person
{
    private string fName;

    public Person(string name)
    {
        fName = name;
    }

    public string FirstName => fName;
}

class Program
{
    static void Main()
    {
        Person p = new Person("Kiran");
        Console.WriteLine(p.FirstName);
    }
}
```

---

### 🔥 Output

```
Kiran
```

---

# 🟡 4️⃣ Expression-Bodied Setter

Normally:

```csharp
public string FirstName
{
    get { return fName; }
    set { fName = value; }
}
```

Using expression body:

```csharp
public string FirstName
{
    get => fName;
    set => fName = value;
}
```

Or using `init` (for immutable properties):

```csharp
public string FirstName
{
    get => fName;
    init => fName = value;
}
```

`value` is a special keyword inside setters.

---

## Example

```csharp
using System;

class Person
{
    private string fName;

    public string FirstName
    {
        get => fName;
        set => fName = value;
    }
}

class Program
{
    static void Main()
    {
        Person p = new Person();
        p.FirstName = "Kiran";

        Console.WriteLine(p.FirstName);
    }
}
```

---

### 🔥 Output

```
Kiran
```

---

# 🟠 5️⃣ Expression-Bodied Constructor

You can use `=>` for constructors too.

⚠ Important:

- Only works cleanly when doing ONE statement.
    

---

## Example

```csharp
using System;

class Person
{
    private string fName;

    public Person(string name) => fName = name;

    public string FirstName => fName;
}

class Program
{
    static void Main()
    {
        Person p = new Person("Kiran");
        Console.WriteLine(p.FirstName);
    }
}
```

---

### 🔥 Output

```
Kiran
```

---

# 🟣 6️⃣ Expression-Bodied Methods with Calculation

Example:

```csharp
class Calculator
{
    public int Square(int x) => x * x;
}
```

Usage:

```csharp
Calculator c = new Calculator();
Console.WriteLine(c.Square(5));
```

---

### 🔥 Output

```
25
```

---

# 🧠 7️⃣ When Should You Use It?

Use expression-bodied members when:

✔ Only one expression  
✔ Simple return  
✔ Clean and readable

Avoid when:

❌ Multiple statements  
❌ Complex logic  
❌ Reduces readability

---

# 🧠 8️⃣ Big Picture Connection

Earlier:

```
Delegate → Lambda → Inline logic
```

Now:

```
Method → Expression-bodied method
Property → Expression-bodied property
Constructor → Expression-bodied constructor
```

All use:

```
=> 
```

But meaning depends on context.

---

# 🧠 Final Quick Notes (Interview Ready)

✔ `=>` used for expression-bodied members  
✔ Works with methods, properties, constructors  
✔ Must contain single expression  
✔ Setter uses special keyword `value`  
✔ Cleaner alternative to `{ return ... }`

---

# 🚀 Mental Model

If the body is just:

```
return something;
```

Replace it with:

```
=> something;
```

---

