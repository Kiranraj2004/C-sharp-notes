

# 🧠 1️⃣ Why Do We Need Concurrent Collections?

Normal collections like:

```csharp
List<T>
Dictionary<TKey, TValue>
Queue<T>
```

❌ Are **NOT thread-safe**

If multiple threads modify them at the same time:

- Data corruption
    
- Race conditions
    
- Exceptions
    
- Unexpected results
    

Example problem:

```csharp
List<int> numbers = new List<int>();

Parallel.For(0, 1000, i =>
{
    numbers.Add(i);  // ⚠️ Not thread-safe
});
```

You might:

- Lose data
    
- Crash
    
- Get unpredictable behavior
    

---

# 🚀 2️⃣ Solution → Concurrent Collections

Namespace:

```csharp
System.Collections.Concurrent
```

These are thread-safe collections built for parallel scenarios.

Common ones:

|Collection|Purpose|
|---|---|
|ConcurrentBag|Unordered thread-safe collection|
|ConcurrentQueue|Thread-safe FIFO|
|ConcurrentStack|Thread-safe LIFO|
|ConcurrentDictionary<TKey,TValue>|Thread-safe dictionary|

---

# 📦 3️⃣ ConcurrentBag

Think of it as:

- Thread-safe version of List
    
- Unordered
    
- Best for “add and process later” scenarios
    

⚠️ No guaranteed order.

---

## 🧪 Example: ConcurrentBag

```csharp
using System;
using System.Collections.Concurrent;
using System.Threading.Tasks;

class Program
{
    static void Main()
    {
        ConcurrentBag<int> numbers = new ConcurrentBag<int>();

        Parallel.For(0, 10, i =>
        {
            numbers.Add(i);
        });

        foreach (var num in numbers)
        {
            Console.WriteLine(num);
        }
    }
}
```

### 🖥 Possible Output (order not guaranteed)

```
3
7
1
9
0
2
8
4
6
5
```

Notice:  
✔ All values added  
❌ Order is random

---

# 📦 4️⃣ ConcurrentQueue (Thread-Safe FIFO)

Like normal Queue, but thread-safe.

---

## 🧪 Example

```csharp
using System;
using System.Collections.Concurrent;
using System.Threading.Tasks;

class Program
{
    static void Main()
    {
        ConcurrentQueue<string> queue = new ConcurrentQueue<string>();

        queue.Enqueue("First");
        queue.Enqueue("Second");

        while (queue.TryDequeue(out string result))
        {
            Console.WriteLine(result);
        }
    }
}
```

### 🖥 Output

```
First
Second
```

Note:

Instead of `Dequeue()`, we use:

```csharp
TryDequeue(out value)
```

Because it safely handles empty cases.

---

# 📦 5️⃣ ConcurrentStack (Thread-Safe LIFO)

---

## 🧪 Example

```csharp
using System;
using System.Collections.Concurrent;

class Program
{
    static void Main()
    {
        ConcurrentStack<string> stack = new ConcurrentStack<string>();

        stack.Push("First");
        stack.Push("Second");

        while (stack.TryPop(out string item))
        {
            Console.WriteLine(item);
        }
    }
}
```

### 🖥 Output

```
Second
First
```

---

# 📦 6️⃣ ConcurrentDictionary<TKey, TValue>

Thread-safe dictionary.

Instead of:

```csharp
Dictionary<string, Person>
```

Use:

```csharp
ConcurrentDictionary<string, Person>
```

---

## 🧪 Example

```csharp
using System;
using System.Collections.Concurrent;

class Program
{
    static void Main()
    {
        ConcurrentDictionary<string, string> people =
            new ConcurrentDictionary<string, string>();

        people.TryAdd("M", "Matt");
        people.TryAdd("L", "Larry");

        if (people.TryGetValue("M", out string name))
        {
            Console.WriteLine(name);
        }
    }
}
```

### 🖥 Output

```
Matt
```

---

# 🔥 Important Concept: Why Not Just Use lock?

You could do:

```csharp
lock(myList)
{
    myList.Add(item);
}
```

But:

- Hard to manage
    
- Easy to forget
    
- Can cause deadlocks
    
- Poor performance if misused
    

Concurrent collections:  
✔ Internally optimized  
✔ Lock-free algorithms (in many cases)  
✔ Fine-grained locking  
✔ Safer design

---

# 🧠 Extra Knowledge (Very Important)

## 1️⃣ When to Use ConcurrentBag?

Best when:

- Order doesn’t matter
    
- Many threads adding items
    
- Example: Parallel file processing
    

Example scenario:

```csharp
Parallel.ForEach(files, file =>
{
    results.Add(Process(file));
});
```

---

## 2️⃣ When to Use ConcurrentDictionary?

Very common in:

- Caching
    
- Web applications
    
- In-memory lookups
    
- API rate limiting
    

Example:

```csharp
cache.TryAdd(userId, userData);
```

---

## 3️⃣ Performance Note

Concurrent collections:

- Slightly slower than normal collections
    
- But safe for multi-threading
    

So rule:

✔ Single-thread → use List, Dictionary  
✔ Multi-thread → use Concurrent collections

---

# 📊 Comparison Summary

|Scenario|Use|
|---|---|
|Normal app, single thread|List|
|Multi-thread add/remove|ConcurrentBag|
|Multi-thread FIFO|ConcurrentQueue|
|Multi-thread LIFO|ConcurrentStack|
|Multi-thread key-value|ConcurrentDictionary|

---

