
---

# 🔷 1️⃣ Three Types of Point

We’ll define:

### ✅ Class Point (Reference Type)

```csharp
public class CPoint
{
    public int X { get; set; }
    public int Y { get; set; }
}
```

---

### ✅ Struct Point (Value Type)

```csharp
public struct SPoint
{
    public int X { get; set; }
    public int Y { get; set; }
}
```

---

### ✅ Record Point (C# 9+)

```csharp
public record RPoint(int X, int Y);
```

This automatically:

- Creates properties
    
- Creates constructor
    
- Implements value-based equality
    

Very powerful.

---

# 🔷 2️⃣ Equality with Class

### Example:

```csharp
CPoint p1 = new CPoint { X = 1, Y = 2 };
CPoint p2 = p1;
CPoint p3 = new CPoint { X = 1, Y = 2 };

Console.WriteLine(p1 == p2);
Console.WriteLine(p1 == p3);
```

---

### ✅ Output:

```
True
False
```

---

### Why?

- `p1 == p2` → same reference → TRUE
    
- `p1 == p3` → different objects → FALSE
    

Even though values are same.

👉 Classes compare references by default.

---

# 🔷 3️⃣ Equality with Struct

### Example:

```csharp
SPoint s1 = new SPoint { X = 1, Y = 2 };
SPoint s2 = s1;
SPoint s3 = new SPoint { X = 1, Y = 2 };

Console.WriteLine(s1.Equals(s2));
Console.WriteLine(s1.Equals(s3));
```

---

### ✅ Output:

```
True
True
```

---

### Why?

Struct compares values.

BUT ⚠️

If you try:

```csharp
Console.WriteLine(s1 == s2);
```

❌ Error:

Operator == not defined for struct (unless overloaded)

---

# 🔷 4️⃣ Operator Overloading for Struct

To enable `==`:

```csharp
public struct SPoint
{
    public int X { get; set; }
    public int Y { get; set; }

    public static bool operator ==(SPoint p1, SPoint p2)
    {
        return p1.X == p2.X && p1.Y == p2.Y;
    }

    public static bool operator !=(SPoint p1, SPoint p2)
    {
        return !(p1 == p2);
    }

    public override bool Equals(object obj)
    {
        if (obj is SPoint p)
            return this == p;
        return false;
    }

    public override int GetHashCode()
    {
        return HashCode.Combine(X, Y);
    }
}
```

Now this works:

```csharp
Console.WriteLine(s1 == s3);
```

---

### ✅ Output:

```
True
```

---

# 🔷 5️⃣ Equality with Record

### Example:

```csharp
RPoint r1 = new RPoint(1, 2);
RPoint r2 = r1;
RPoint r3 = new RPoint(1, 2);

Console.WriteLine(r1 == r2);
Console.WriteLine(r1 == r3);
```

---

### ✅ Output:

```
True
True
```

---

### Why?

Records compare values automatically.

Even though they are reference types.

This is the BIG difference 🔥

---

# 🔷 6️⃣ Summary Table

|Type|Default `==` Behavior|Equality Type|
|---|---|---|
|Class|Reference comparison|Memory address|
|Struct|Value comparison (Equals)|Field values|
|Record|Value comparison|Property values|

---

# 🔷 7️⃣ Visual Understanding

## Class

```
p1 ----\
         --> Object A (1,2)
p2 ----/

p3 ------> Object B (1,2)
```

p1 == p3 → FALSE (different objects)

---

## Record

Even if different objects:

```
r1 ---> Object A (1,2)
r3 ---> Object B (1,2)
```

r1 == r3 → TRUE  
Because values match.

---

# 🔷 8️⃣ Interview-Level Explanation

If interviewer asks:

### 🔹 How does equality differ between class and record?

You say:

> Classes compare references by default, meaning two objects are equal only if they reference the same memory location. Records compare values by default, meaning two objects are equal if their properties have equal values.

That answer is strong 💪

---

# 🔷 9️⃣ Very Important Concept

Why records are useful?

Because for DTOs and data models, we usually care about:

> “Do they have same data?”

Not:

> “Are they the same object in memory?”

---

# 🧠 Let Me Test You (Interview Style)

If I write:

```csharp
CPoint p1 = new CPoint { X = 5, Y = 10 };
CPoint p2 = new CPoint { X = 5, Y = 10 };

Console.WriteLine(p1.Equals(p2));
```
