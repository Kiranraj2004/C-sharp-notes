
## 1️⃣ What Are Generics?

Generics were introduced in **.NET 2.0**.

They allow you to create **type-safe data structures** like:

- `List<T>`
    
- `Stack<T>`
    
- `Queue<T>`
    
- `Dictionary<TKey, TValue>`
    

Instead of using old non-generic collections like:

- `ArrayList`
    
- `Hashtable`
    

---

# 2️⃣ Problem with Non-Generic Collections (ArrayList)

### ❌ What is ArrayList?

`ArrayList` stores elements as **object type**.

That means:

- It can store **any data type**
    
- No type safety
    
- Errors happen at **runtime**
    

---

## 🔎 Example Using ArrayList (Non-Generic)

```csharp
using System;
using System.Collections;

class Program
{
    static void Main()
    {
        ArrayList arrList = new ArrayList();

        arrList.Add(1);
        arrList.Add(2);
        arrList.Add(3);

        int total = 0;

        foreach (int num in arrList)
        {
            total += num;
        }

        Console.WriteLine("Total: " + total);
    }
}
```

### ✅ Output:

```
Total: 6
```

---

## ⚠️ Now Add a Wrong Data Type

```csharp
arrList.Add("4");   // String instead of int
```

### ❌ Runtime Error:

```
Unhandled Exception:
System.InvalidCastException:
Unable to cast object of type 'System.String' to type 'System.Int32'
```

### 💡 Why?

Because:

- `ArrayList` stores everything as `object`
    
- `"4"` is a string
    
- While reading, it tries to convert string → int
    
- That fails at runtime
    

---

# 3️⃣ What Is Type Safety?

Type safety means:

✔ Only specific data type allowed  
✔ Errors caught at compile time  
✔ Safer code

---

# 4️⃣ Using Generics – List

Instead of `ArrayList`, use:

```csharp
List<int>
```

Here:

- `T` means Type
    
- We specify the type inside `< >`
    

---

## 🔎 Example Using Generic List

```csharp
using System;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        List<int> arrList = new List<int>();

        arrList.Add(1);
        arrList.Add(2);
        arrList.Add(3);

        int total = 0;

        foreach (int num in arrList)
        {
            total += num;
        }

        Console.WriteLine("Total: " + total);
    }
}
```

### ✅ Output:

```
Total: 6
```

---

## ❌ Try Adding Wrong Type

```csharp
arrList.Add("4");  // Compile-time error
```

### 🔴 Compile-Time Error:

```
Cannot convert from 'string' to 'int'
```

✔ Error caught during compilation  
✔ Program does not run  
✔ Safer code

---

# 5️⃣ Performance Benefit – Boxing & Unboxing

## 📦 What is Boxing?

When a value type (int, double, etc.) is converted into object type.

Example:

```csharp
int num = 10;
object obj = num;  // Boxing
```

## 📤 What is Unboxing?

Converting object back to value type.

```csharp
int num2 = (int)obj;  // Unboxing
```

---

## ⚠️ Why Is This Bad?

- Extra memory usage
    
- Extra CPU work
    
- Slower performance
    

---

## ❌ ArrayList Causes Boxing

Because ArrayList stores elements as `object`.

So when adding int:

```
int → object (Boxing)
object → int (Unboxing)
```

This reduces performance.

---

## ✅ Generics Avoid Boxing

When you use:

```csharp
List<int>
```

The list stores **int directly**, not object.

✔ No boxing  
✔ No unboxing  
✔ Faster performance

---

# 6️⃣ Summary Comparison

|Feature|ArrayList|List|
|---|---|---|
|Type Safe|❌ No|✅ Yes|
|Compile-time checking|❌ No|✅ Yes|
|Runtime errors|Possible|Prevented|
|Boxing/Unboxing|Yes|No|
|Performance|Slower|Faster|
|Recommended?|❌ Old|✅ Modern|

---

# 7️⃣ Generics With Custom Class

Generics are not limited to built-in types.

### Example:

```csharp
using System;
using System.Collections.Generic;

class Student
{
    public string Name;
    public int Age;
}

class Program
{
    static void Main()
    {
        List<Student> students = new List<Student>();

        students.Add(new Student { Name = "Kiran", Age = 21 });
        students.Add(new Student { Name = "Raj", Age = 22 });

        foreach (Student s in students)
        {
            Console.WriteLine(s.Name + " - " + s.Age);
        }
    }
}
```

### ✅ Output:

```
Kiran - 21
Raj - 22
```

---

# 8️⃣ Key Interview Points 🔥

If asked in interview:

### 💬 What are Generics?

Generics allow us to define classes and collections that work with a specific data type while ensuring type safety and better performance.

---

### 💬 Why are Generics better than ArrayList?

1. Type-safe
    
2. Compile-time error detection
    
3. Avoid boxing & unboxing
    
4. Better performance
    
5. Cleaner and maintainable code
    

---

# 9️⃣ Final Quick Notes (Exam Ready)

- Introduced in **.NET 2.0**
    
- Use angle brackets `<T>`
    
- Provide **type safety**
    
- Avoid **boxing/unboxing**
    
- Improve **performance**
    
- Replace old collections like `ArrayList`
    

---
