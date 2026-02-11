
# 🧠 1️⃣ What is an Event?

An **event** is built on top of a delegate.

Think of it like this:

> Delegate = method pointer  
> Event = controlled multicast delegate

It allows:

- Multiple methods to subscribe
    
- One method call to notify many listeners
    
- Callback mechanism
    

This is called a **multicast delegate**.

---

# 🧠 2️⃣ Basic Event Structure

### Step 1: Declare a Delegate

```csharp
public delegate void MyDelegate(string message);
```

---

### Step 2: Declare an Event

```csharp
public static event MyDelegate SomethingHappened;
```

Notice:

- `event` keyword
    
- Uses delegate type
    
- Has a name
    

---

### Step 3: Raise (Invoke) the Event

```csharp
public static void DoSomething()
{
    Console.WriteLine("I am about to do something");

    if (SomethingHappened != null)
    {
        SomethingHappened("I did something");
    }
}
```

Important:  
We check for null because:

- If no one subscribed, it will be null
    
- Calling null → runtime error
    

---

# 🧠 3️⃣ Complete Example

### 📌 DelegateSamples.cs

```csharp
using System;

public static class DelegateSamples
{
    public delegate void MyDelegate(string message);

    public static event MyDelegate SomethingHappened;

    public static void DoSomething()
    {
        Console.WriteLine("I am about to do something");

        if (SomethingHappened != null)
        {
            SomethingHappened("I did something");
        }
    }
}
```

---

### 📌 Program.cs

```csharp
using System;

class Program
{
    static void Main()
    {
        DelegateSamples.SomethingHappened += WriteHello;
        DelegateSamples.SomethingHappened += WriteUpper;

        DelegateSamples.DoSomething();

        // Remove one listener
        DelegateSamples.SomethingHappened -= WriteHello;

        Console.WriteLine("\nAfter removing WriteHello:\n");

        DelegateSamples.DoSomething();
    }

    static void WriteHello(string msg)
    {
        Console.WriteLine("Hello: " + msg);
    }

    static void WriteUpper(string msg)
    {
        Console.WriteLine(msg.ToUpper());
    }
}
```

---

# 🔥 Output

```
I am about to do something
Hello: I did something
I DID SOMETHING

After removing WriteHello:

I am about to do something
I DID SOMETHING
```

---

# 🧠 What Just Happened?

1. Two methods subscribed:
    
    - WriteHello
        
    - WriteUpper
        
2. Event raised once.
    
3. Both methods executed.
    
4. After removing one, only remaining method executed.
    

That’s multicast behavior.

---

# 🧠 4️⃣ Standard Event Pattern (Very Important)

In real applications, events usually follow this pattern:

```csharp
void Handler(object sender, EventArgs args)
```

Why?

Because:

- `sender` → who raised event
    
- `args` → extra data about event
    

---

# 🧠 5️⃣ Example: Console Cancel Event

This is built-in:

```csharp
Console.CancelKeyPress += OnCancel;
```

The delegate type is:

```csharp
ConsoleCancelEventHandler
```

Signature:

```csharp
void Handler(object sender, ConsoleCancelEventArgs args)
```

---

# 🧪 Example

```csharp
using System;

class Program
{
    static void Main()
    {
        Console.CancelKeyPress += OnCancel;

        Console.WriteLine("Press Ctrl + C to cancel...");

        for (int i = 0; i < 10000; i++)
        {
            Console.WriteLine(i);
        }
    }

    static void OnCancel(object sender, ConsoleCancelEventArgs args)
    {
        Console.WriteLine("\nCancel event triggered!");

        // Prevent program from closing
        args.Cancel = true;
    }
}
```

---

# 🔥 What Happens?

1. Press Ctrl + C
    
2. Event fires
    
3. OnCancel runs
    
4. If `args.Cancel = true`  
    → Program continues
    
5. If `args.Cancel = false`  
    → Program exits
    

---

# 🧠 Why Use Events?

Events are used for:

- Button clicks (UI)
    
- File download completed
    
- Payment completed
    
- User logged in
    
- Background task finished
    
- Error occurred
    

It allows **loose coupling**.

Publisher does not know who is listening.

---

# 🧠 6️⃣ Important: Cleaning Up Events

Very important for memory management.

If you subscribe:

```csharp
DelegateSamples.SomethingHappened += WriteHello;
```

You should unsubscribe when done:

```csharp
DelegateSamples.SomethingHappened -= WriteHello;
```

Why?

Because:

- Event keeps reference to method
    
- Can cause memory leaks
    
- Object may not get garbage collected
    

Interviewers LOVE this point.

---

# 🧠 Interview Notes Summary

✔ Event is a multicast delegate  
✔ Allows multiple subscribers  
✔ Uses += to subscribe  
✔ Uses -= to unsubscribe  
✔ Always check null before invoking  
✔ Standard pattern:

```
(object sender, EventArgs args)
```

✔ Used for callbacks and notifications

---

# 🧠 Final Mental Model

Think like this:

```
Event = Announcement system
Delegate = Phone number
Subscribers = People who gave their number
Raise event = Make one call → everyone gets notified
```

---
