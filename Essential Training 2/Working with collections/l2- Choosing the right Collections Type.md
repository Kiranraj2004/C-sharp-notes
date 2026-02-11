
# 🧠 1. Problem With Old Collections (System.Collections)

Older .NET collections (early 2000s):

- `ArrayList`
    
- `Stack`
    
- `Queue`
    
- `HashTable`
    
- `SortedList`
    
- `DictionaryBase`
    
- `NameValueCollection`
    

They store everything as:

```csharp
object
```

So when you remove items, you must cast:

```csharp
(string)stack.Pop();
```

❌ Not type-safe  
❌ Slower (boxing/unboxing)  
❌ Runtime casting errors possible

---

# 🚀 2. Modern Solution → Generic Collections

Namespace:

```csharp
System.Collections.Generic
```

Examples:

|Old Type|Generic Version|
|---|---|
|ArrayList|List|
|Stack|Stack|
|Queue|Queue|
|HashTable|Dictionary<TKey, TValue>|
|SortedList|SortedList<TKey, TValue>|
|—|SortedDictionary<TKey, TValue>|

✅ Type safe  
✅ No casting  
✅ Better performance  
✅ Cleaner code

---

# 📦 3. Queue (FIFO – First In First Out)

Think of it like a **line in a bank** 🏦

First person enters → first person leaves.

Operations:

- `Enqueue()` → Add item
    
- `Dequeue()` → Remove item
    
- `Count` → Number of items
    

---

## 🧪 Example 1: Non-Generic Queue (Old Way)

```csharp
using System;
using System.Collections;

class Program
{
    static void Main()
    {
        Queue queue = new Queue();

        queue.Enqueue("First Item");
        queue.Enqueue("Second Item");

        while (queue.Count > 0)
        {
            string item = (string)queue.Dequeue();  // Casting needed
            Console.WriteLine(item);
        }
    }
}
```

### 🖥 Output

```
First Item
Second Item
```

---

# 📦 4. Stack (LIFO – Last In First Out)

Think of it like a **stack of plates** 🍽

Last plate placed → first plate removed.

Operations:

- `Push()` → Add item
    
- `Pop()` → Remove item
    
- `Count` → Number of items
    

---

## 🧪 Example 2: Non-Generic Stack (Old Way)

```csharp
using System;
using System.Collections;

class Program
{
    static void Main()
    {
        Stack stack = new Stack();

        stack.Push("First Item");
        stack.Push("Second Item");

        while (stack.Count > 0)
        {
            string item = (string)stack.Pop();  // Casting needed
            Console.WriteLine(item);
        }
    }
}
```

### 🖥 Output

```
Second Item
First Item
```

See the difference?

Queue → FIFO  
Stack → LIFO

---

# 🔥 5. Now Let’s Use Generic Version (Recommended)

This is what you SHOULD use in modern C#.

---

## 🧪 Example 3: Generic Queue

```csharp
using System;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        Queue<string> queue = new Queue<string>();

        queue.Enqueue("First Item");
        queue.Enqueue("Second Item");

        while (queue.Count > 0)
        {
            string item = queue.Dequeue();  // No casting needed
            Console.WriteLine(item);
        }
    }
}
```

### 🖥 Output

```
First Item
Second Item
```

✔ No casting  
✔ Type safe  
✔ Cleaner

---

## 🧪 Example 4: Generic Stack

```csharp
using System;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        Stack<string> stack = new Stack<string>();

        stack.Push("First Item");
        stack.Push("Second Item");

        while (stack.Count > 0)
        {
            string item = stack.Pop();  // No casting needed
            Console.WriteLine(item);
        }
    }
}
```

### 🖥 Output

```
Second Item
First Item
```

---

# 📘 6. Dictionary (Replacement for Hashtable)

Used for key-value storage.

Example:

```csharp
Dictionary<int, string> students = new Dictionary<int, string>();

students.Add(1, "Kiran");
students.Add(2, "Rahul");

Console.WriteLine(students[1]);
```

### 🖥 Output

```
Kiran
```

---

# 🎯 7. When to Use What?

|Situation|Use|
|---|---|
|Simple dynamic list|`List<T>`|
|First in, first out|`Queue<T>`|
|Last in, first out|`Stack<T>`|
|Key-value lookup|`Dictionary<TKey, TValue>`|
|Need sorted key-value|`SortedDictionary`|

💡 In real projects:

- `List<T>` → most common
    
- `Dictionary<TKey,TValue>` → second most common
    

---

# 🧠 8. Why Generics Are Better (Very Important for Interviews)

Old collection:

```csharp
Stack stack = new Stack();
stack.Push("Hello");
stack.Push(123);   // Allowed 😬
```

Generic:

```csharp
Stack<string> stack = new Stack<string>();
stack.Push("Hello");
stack.Push(123);   // ❌ Compile-time error
```

So generics give:

- Compile-time safety
    
- Better performance
    
- No boxing/unboxing
    
- Cleaner API
    

---

