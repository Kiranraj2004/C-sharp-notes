
## 1) C# is Object-Oriented

- C# is an **object-oriented programming (OOP)** language.
- A **class** is a **blueprint/template** used to create **objects** (instances).
- Objects combine:
    - **data** (fields/properties)
    - **behavior** (methods)

---

## 2) How to Define a Class

To define a class in C#:

public class Book

{

    // fields + constructor + methods

}

``

### Keywords used:

- `class` → defines a class
- `public` → makes the class accessible from other parts of the program
- Class name → usually **PascalCase** (e.g., `Book`)

---

## 3) Fields (Member Variables)

Inside a class, you can declare fields to store data.

Example fields in transcript:

- `_name` → string
- `_author` → string
- `_pageCount` → int

> The transcript uses `_` prefix to indicate “internal/private field name”.

Example:

string _name;

string _author;

int _pageCount;

``

📌 **Important:** If you don’t specify access, C# fields inside a class are **private by default**, meaning: ✅ accessible inside the class\ ❌ not accessible from outside the class

---

## 4) Constructor

A **constructor** is a special method used to create and initialize an object.

Rules:

- Same name as the class (`Book`)
- No return type (not even `void`)
- Runs automatically when you use `new Book(...)`

Example:

public Book(string name, string author, int pages)

{

    _name = name;

    _author = author;

    _pageCount = pages;

}

---

## 5) Methods (Behavior)

A class can contain methods that operate on its data.

Example: `GetDescription()` returns a string using interpolation:

public string GetDescription()

{

    return $"{_name__} by {_author}";

}

---

## 6) Creating Objects (Instances)

To create an object, you use the `new` keyword:

Book b1 = new Book("War and Peace", "Leo Tolstoy", 800);

Book b2 = new Book("The Grapes of Wrath", "John Steinbeck", 464);

``

---

## 7) Calling Methods

You call methods using the dot operator (`.`):

Console.WriteLine(b1.GetDescription());

Console.WriteLine(b2.GetDescription());

---

## 8) Why You Got This Error:

> `Book._name is inaccessible due to its protection level`

Because `_name` is a **field** that is **private** (default), so it cannot be accessed directly from outside:

❌ This fails:

b1._name = "Something";

✅ You must change it using:

- a **public property**, or
- a **public method** (setter method)

This is part of **encapsulation** in OOP: protect internal data and expose controlled access.

---

# ✅ Full Example Code (Like Transcript)

## 📌 `Book.cs`

public class Book

{

    // Fields (private by default)

    string _name;

    string _author;

    int _pageCount;

  

    // Constructor

    public Book(string name, string author, int pages)

    {

        _name = name;

        _author = author;

        _pageCount = pages;

    }

  

    // Method

    public string GetDescription()

    {

        return $"{_name__} by {_author}";

    }

}

## 📌 `Program.cs`

using System;

  

Book b1 = new Book("War and Peace", "Leo Tolstoy", 800);

Book b2 = new Book("The Grapes of Wrath", "John Steinbeck", 464);

  

Console.WriteLine(b1.GetDescription());

Console.WriteLine(b2.GetDescription());

### 🖥 Output

```
War and Peace by Leo Tolstoy
The Grapes of Wrath by John Steinbeck
```

---

# ❌ Example Showing the Error (Transcript’s last part)

If you try:

b1._name = "Aldous Huxley";

### You get error:

```
'Book._name' is inaccessible due to its protection level
```

This happens because `_name` is private and cannot be accessed directly from outside the class.

---

# ✅ Fix: Use a Public Property (Recommended)

## Updated `Book.cs`

public class Book

{

    private string _name;

    private string _author;

    private int _pageCount;

  

    public Book(string name, string author, int pages)

    {

        _name = name;

        _author = author;

        _pageCount = pages;

    }

  

    // Public property to allow safe access

    public string Name

    {

        get { return _name; }

        set { _name = value; }

    }

  

    public string GetDescription()

    {

        return $"{_name__} by {_author}";

    }

}

## Updated `Program.cs`

using System;

  

Book b1 = new Book("War and Peace", "Leo Tolstoy", 800);

  

Console.WriteLine(b1.GetDescription());

  

b1.Name = "Brave New World"; // ✅ works through property

Console.WriteLine(b1.GetDescription());

``

### 🖥 Output

```
War and Peace by Leo Tolstoy
Brave New World by Leo Tolstoy
```

---

