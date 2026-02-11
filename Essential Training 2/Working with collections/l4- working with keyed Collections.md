

This section mainly covers:

- `Dictionary<TKey, TValue>`
    
- `ContainsKey()`
    
- `TryGetValue()`
    
- `TryAdd()`
    
- Iterating over dictionary
    
- Unique key requirement
    
- `NameValueCollection` (multiple values per key)
    

Let’s break it down clean and simple 👇

---

# 🧠 1️⃣ What is a Dictionary?

A dictionary stores:

```
Key  →  Value
```

Like a real dictionary:

```
"cat" → definition
```

In C#:

```csharp
Dictionary<string, Person>
```

- Key = string
    
- Value = Person object
    

---

# 📦 2️⃣ Creating a Dictionary

```csharp
Dictionary<string, Person> people = 
    new Dictionary<string, Person>();
```

Now we can add items:

```csharp
people.Add("M", new Person("Matt", "Milner"));
people.Add("L", new Person("Larry", "Lawnmower"));
```

⚠️ Important: Keys must be unique.

---

# 🧪 Example Setup

### 🔹 Person Class

```csharp
public class Person
{
    public string FirstName { get; set; }
    public string LastName { get; set; }

    public Person(string first, string last)
    {
        FirstName = first;
        LastName = last;
    }
}
```

---

# 📌 3️⃣ Accessing by Key (Indexing)

```csharp
var person = people["M"];
Console.WriteLine(person.FirstName);
```

Output:

```
Matt
```

BUT ⚠️  
If key doesn’t exist:

```csharp
people["X"];
```

You get:

```
KeyNotFoundException
```

---

# 📌 4️⃣ Safe Way – ContainsKey()

```csharp
if (people.ContainsKey("M"))
{
    var person = people["M"];
    Console.WriteLine($"Person with key M is {person.FirstName}");
}
```

Output:

```
Person with key M is Matt
```

---

# 📌 5️⃣ Better Way – TryGetValue()

Cleaner and safer.

```csharp
if (people.TryGetValue("M", out Person foundPerson))
{
    Console.WriteLine($"Found {foundPerson.FirstName}");
}
else
{
    Console.WriteLine("Key not found");
}
```

Output:

```
Found Matt
```

It:

- Returns true/false
    
- Outputs value safely
    

---

# 📌 6️⃣ Iterating Through Dictionary

When you do:

```csharp
foreach (var item in people)
{
    Console.WriteLine(item.Key);
    Console.WriteLine(item.Value.FirstName);
}
```

Each `item` is:

```
KeyValuePair<string, Person>
```

Output:

```
M Matt
L Larry
```

---

# 🚨 7️⃣ Duplicate Key Error

If you do:

```csharp
people.Add("L", new Person("Leticia", "Lopez"));
```

You’ll get:

```
An item with the same key has already been added.
```

Because dictionary requires:

✅ Unique keys

---

# 📌 8️⃣ Safe Add – TryAdd()

Instead of crashing:

```csharp
bool added = people.TryAdd("L", new Person("Leticia", "Lopez"));

Console.WriteLine("Was added? " + added);
```

If key exists:

```
Was added? False
```

No exception. Much safer.

---

# 📚 9️⃣ NameValueCollection (Multiple Values Per Key)

Namespace:

```csharp
using System.Collections.Specialized;
```

Unlike Dictionary:

- Allows duplicate keys
    
- One key → multiple values
    

---

## 🧪 Example

```csharp
using System.Collections.Specialized;

NameValueCollection items = new NameValueCollection();

items.Add("L", "Leticia");
items.Add("L", "Larry");
items.Add("M", "Matt");

foreach (string key in items.AllKeys)
{
    Console.WriteLine($"Key: {key}");
    Console.WriteLine("Values: " + items[key]);
}
```

### 🖥 Output

```
Key: L
Values: Leticia,Larry
Key: M
Values: Matt
```

Notice:

```
L → Leticia, Larry
```

Multiple values allowed.

---

# 📊 Dictionary vs NameValueCollection

|Feature|Dictionary|NameValueCollection|
|---|---|---|
|Unique keys|Yes|No|
|Strongly typed|Yes|No (string only)|
|Performance|Fast|Slower|
|Common usage|Very common|Mostly legacy / config / HTTP|

---

# 🎯 When to Use What?

Use **Dictionary<TKey, TValue>** when:

- You need fast lookup
    
- Keys must be unique
    
- Strong typing required
    
- Most real-world scenarios
    

Use **NameValueCollection** when:

- Working with HTTP query strings
    
- Config settings
    
- Cookies
    
- Multiple values per key needed
    

---

# 💡 Real-World Example

In backend:

```csharp
Dictionary<int, User> usersById;
Dictionary<string, Product> productsBySku;
Dictionary<string, string> headers;
```

In ASP.NET:

```csharp
Request.Query
Request.Headers
```

Often use NameValueCollection internally.

---

