
# 🔷 1️⃣ Reference Type Copy (Class)

### Important Rule:

When you assign a class variable to another variable…

You are copying the **reference**, NOT the object.

Both variables point to the same memory.

---

## 🔥 Example 1 — Copying a Class

```csharp
public class Employee
{
    public string FirstName { get; set; }
    public int Age { get; set; }
}

class Program
{
    static void Main()
    {
        Employee me = new Employee
        {
            FirstName = "Matt",
            Age = 50
        };

        Employee other = me;   // Copy reference

        other.FirstName = "Bizarro Matt";
        other.Age = 39;

        Console.WriteLine($"{me.FirstName} is {me.Age}");
        Console.WriteLine($"{other.FirstName} is {other.Age}");
    }
}
```

---

### ✅ Output:

```
Bizarro Matt is 39
Bizarro Matt is 39
```

---

### Why?

Because:

```
me  ----\
          --->  SAME OBJECT in heap
other ----/
```

Both point to same object.

---

# 🔷 2️⃣ Passing Reference Type to Method

By default, class objects are passed **by value of the reference**.

Important subtle concept ⚠️

That means:

- Method gets a copy of the reference
    
- But both references still point to same object
    

---

## 🔥 Example 2 — Modifying Inside Method

```csharp
static void ChangeName(Employee person)
{
    person.FirstName = "Changed Inside Method";
}

static void Main()
{
    Employee me = new Employee
    {
        FirstName = "Matt",
        Age = 50
    };

    ChangeName(me);

    Console.WriteLine(me.FirstName);
}
```

---

### ✅ Output:

```
Changed Inside Method
```

---

### Why?

Because method modified the object itself.

---

# 🔷 3️⃣ Changing the Reference Inside Method

Now this is the tricky part 👀

```csharp
static void ChangeName(Employee person)
{
    person = new Employee
    {
        FirstName = "New Person",
        Age = 25
    };

    Console.WriteLine("Inside Method: " + person.FirstName);
}
```

Main:

```csharp
Employee me = new Employee
{
    FirstName = "Matt",
    Age = 50
};

ChangeName(me);

Console.WriteLine("Outside Method: " + me.FirstName);
```

---

### ✅ Output:

```
Inside Method: New Person
Outside Method: Matt
```

---

### Why?

Because:

- Method changed what `person` points to
    
- But only local copy of reference changed
    
- Original variable `me` still points to old object
    

---

# 🔷 4️⃣ Key Difference

Inside method:

```csharp
person.LastName = "Unknown";  // Changes object
```

✅ Affects outside

But:

```csharp
person = new Employee();  // Changes reference
```

❌ Does NOT affect outside

---

# 🔷 5️⃣ Struct (Value Type) Behavior

Now compare with struct.

---

## 🔥 Example 3 — Struct Copy

```csharp
public struct Age
{
    public int Years;
}

class Program
{
    static void Main()
    {
        Age a1 = new Age { Years = 50 };
        Age a2 = a1;

        a2.Years = 39;

        Console.WriteLine(a1.Years);
        Console.WriteLine(a2.Years);
    }
}
```

---

### ✅ Output:

```
50
39
```

---

### Why?

Struct copies the actual value.

Different memory locations.

---

# 🔷 6️⃣ Passing Struct to Method

```csharp
static void ChangeAge(Age age)
{
    age.Years = 20;
}

static void Main()
{
    Age a = new Age { Years = 50 };

    ChangeAge(a);

    Console.WriteLine(a.Years);
}
```

---

### ✅ Output:

```
50
```

---

### Why?

Struct is copied when passed to method.

---

# 🔷 7️⃣ Summary Table (Very Important)

|Behavior|Class|Struct|
|---|---|---|
|Assignment|Copies reference|Copies value|
|Modify property|Affects original|Does not affect original|
|Passed to method|Reference copied|Value copied|
|Changing reference inside method|No effect outside|N/A|

---

# 🔷 8️⃣ Interview-Level Explanation

If interviewer asks:

### 🔹 What happens when you assign one class object to another?

> The reference is copied, not the object. Both variables point to the same object in heap.

---

### 🔹 What happens when passing class object to method?

> The reference is passed by value. The method can modify the object, but cannot change the caller’s reference unless passed with `ref`.

🔥 That answer shows deep understanding.

---

