
# ✅ 1. What is an Event in C#?

👉 An **event** is a mechanism that allows a class to notify other classes when something happens.

It is built on top of **delegates**.

Think of it like:

- 📢 Publisher → broadcasts message
    
- 👂 Subscriber → listens and reacts
    

---

# ✅ 2. Why Do We Use Events?

Events allow:

✔ Communication between objects  
✔ Asynchronous behavior  
✔ Loosely coupled systems  
✔ More responsive applications

Example:

- Button clicked
    
- File downloaded
    
- Value changed
    
- User logged in
    

---

# ✅ 3. How Events Work Internally

Events are based on **delegates**.

Steps to create an event:

### Step 1: Declare Delegate (Event Handler Signature)

```csharp
public delegate void MyEventHandler(string value);
```

---

### Step 2: Declare Event in Class

```csharp
public event MyEventHandler ValueChanged;
```

Notice:  
We use the keyword **event**, not delegate.

---

### Step 3: Trigger (Raise) the Event

```csharp
ValueChanged(theValue);
```

---

### Step 4: Subscribe to Event

```csharp
obj.ValueChanged += HandlerMethod;
```

---

# ✅ 4. Full Working Example (Simple Version)

---

## 🔹 Event Publisher Class

```csharp
using System;

public delegate void MyEventHandler(string value);

class EventPublisher
{
    private string theVal;

    public event MyEventHandler ValueChanged;

    public string Val
    {
        get { return theVal; }
        set
        {
            theVal = value;

            // Trigger event
            if (ValueChanged != null)
            {
                ValueChanged(theVal);
            }
        }
    }
}
```

---

## 🔹 Main Program

```csharp
class Program
{
    static void Main(string[] args)
    {
        EventPublisher obj = new EventPublisher();

        // Subscribe to event
        obj.ValueChanged += Obj_ValueChanged;

        Console.WriteLine("Type something (type 'exit' to quit):");

        string input;

        while ((input = Console.ReadLine()) != "exit")
        {
            obj.Val = input;
        }
    }

    static void Obj_ValueChanged(string newValue)
    {
        Console.WriteLine("Value changed to: " + newValue);
    }
}
```

---

# ✅ Output

```
Type something (type 'exit' to quit):
hello
Value changed to: hello
world
Value changed to: world
exit
```

---

# ✅ 5. Using Anonymous Delegate as Event Handler

Instead of writing a named method:

```csharp
obj.ValueChanged += Obj_ValueChanged;
```

We can write:

```csharp
obj.ValueChanged += delegate(string val)
{
    Console.WriteLine("Value changed to: " + val);
};
```

---

## 🔹 Updated Main Method

```csharp
static void Main(string[] args)
{
    EventPublisher obj = new EventPublisher();

    obj.ValueChanged += delegate(string val)
    {
        Console.WriteLine("Value changed to: " + val);
    };

    Console.WriteLine("Type something:");

    string input;

    while ((input = Console.ReadLine()) != "exit")
    {
        obj.Val = input;
    }
}
```

---

# ✅ Output

```
Type something:
Kiran
Value changed to: Kiran
AI
Value changed to: AI
exit
```

Same result ✅  
Cleaner code 🔥

---

# ✅ 6. Important Concept: Safe Event Invocation

Instead of writing:

```csharp
ValueChanged(theVal);
```

Better practice:

```csharp
ValueChanged?.Invoke(theVal);
```

Why?

Prevents NullReferenceException if no subscribers exist.

---

# ✅ 7. Publisher vs Subscriber Concept

|Role|Responsibility|
|---|---|
|Publisher|Declares and triggers event|
|Subscriber|Subscribes and handles event|
|Delegate|Defines method signature|

---

# ✅ 8. Real-World Example

Think of a button click:

```csharp
button.Click += delegate(object sender, EventArgs e)
{
    Console.WriteLine("Button clicked!");
};
```

Click → event fires → handler runs

---

# ✅ 9. Why Events Are Better Than Direct Method Calls

Without events:

```
Object A must know about Object B
```

With events:

```
Object A just announces
Anyone listening can react
```

This reduces coupling.

---


---

# ✅ 11. Flow Summary

```
1. Declare delegate
2. Declare event using event keyword
3. Subscribe using +=
4. Trigger using Invoke()
```

---

# ✅ 12. Big Picture

Events are:

✔ Built on multicast delegates  
✔ Used for async communication  
✔ Core of UI frameworks  
✔ Foundation of event-driven programming

---

