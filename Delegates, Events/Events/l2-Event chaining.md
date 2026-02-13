
# ✅ PART 1 — Chaining Multiple Event Handlers

Events are based on **multicast delegates**, so:

> One event → Multiple handlers → All execute in order

---

## 🔹 Example: Simple Chained Event Handlers

---

### Step 1: Declare Delegate

```csharp
public delegate void MyEventHandler(string value);
```

---

### Step 2: Event Publisher Class

```csharp
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
            ValueChanged?.Invoke(theVal);
        }
    }
}
```

---

### Step 3: Add Multiple Handlers in Main

```csharp
class Program
{
    static void Main(string[] args)
    {
        EventPublisher obj = new EventPublisher();

        // Handler 1
        obj.ValueChanged += ChangeListener1;

        // Handler 2
        obj.ValueChanged += ChangeListener2;

        // Anonymous handler
        obj.ValueChanged += delegate (string val)
        {
            Console.WriteLine("Anonymous handler received: " + val);
        };

        Console.WriteLine("Enter text (type 'exit' to quit):");

        string input;

        while ((input = Console.ReadLine()) != "exit")
        {
            obj.Val = input;
        }
    }

    static void ChangeListener1(string val)
    {
        Console.WriteLine("Listener1: Value changed to " + val);
    }

    static void ChangeListener2(string val)
    {
        Console.WriteLine("Listener2: I also received " + val);
    }
}
```

---

# ✅ Output

```
Enter text:
hello
Listener1: Value changed to hello
Listener2: I also received hello
Anonymous handler received: hello
```

👉 Notice:

- All handlers executed
    
- In the order added
    
- This is event chaining
    

---

# ✅ PART 2 — Standard .NET Event Pattern

Now we move to the professional .NET way.

In .NET Framework:

Events follow this pattern:

```
void Handler(object sender, EventArgs e)
```

Why?

- `sender` → Who raised the event
    
- `e` → Data about the event
    

---

# ✅ Why Use EventArgs?

Instead of passing a string directly:

```csharp
public event MyEventHandler ValueChanged;
```

We use:

```csharp
public event EventHandler<MyCustomEventArgs> ObjChanged;
```

This matches .NET standards.

---

# ✅ Step-by-Step Example (Standard Pattern)

---

## 🔹 Step 1: Create Custom EventArgs Class

```csharp
using System;

public class ObjChangeEventArgs : EventArgs
{
    public string PropChanged { get; set; }
}
```

This class holds event data.

---

## 🔹 Step 2: Define Event Using EventHandler

```csharp
class EventPublisher
{
    private string theVal;

    public event EventHandler<ObjChangeEventArgs> ObjChanged;

    public string Val
    {
        get { return theVal; }
        set
        {
            theVal = value;

            // Trigger event
            ObjChanged?.Invoke(this,
                new ObjChangeEventArgs
                {
                    PropChanged = theVal
                });
        }
    }
}
```

Important:

- `this` → sender
    
- `new ObjChangeEventArgs` → event data
    

---

## 🔹 Step 3: Subscribe in Main

```csharp
class Program
{
    static void Main(string[] args)
    {
        EventPublisher obj = new EventPublisher();

        obj.ObjChanged += delegate (object sender, ObjChangeEventArgs e)
        {
            Console.WriteLine(
                sender.GetType().Name +
                " changed property to: " +
                e.PropChanged
            );
        };

        Console.WriteLine("Enter text (type exit to quit):");

        string input;

        while ((input = Console.ReadLine()) != "exit")
        {
            obj.Val = input;
        }
    }
}
```

---

# ✅ Output

```
Enter text:
Hello
EventPublisher changed property to: Hello
World
EventPublisher changed property to: World
```

---

# ✅ What Is Happening Internally?

When:

```
obj.Val = "Hello";
```

1. Setter runs
    
2. Event is triggered
    
3. All subscribers are notified
    
4. Each handler receives:
    
    - sender (object that raised event)
        
    - event data
        

---

# ✅ Why This Pattern Is Important

This matches how .NET Framework works.

Example:

```
button.Click += Button_Click;
```

Signature:

```csharp
void Button_Click(object sender, EventArgs e)
```

All .NET UI events follow this pattern.

---

# ✅ Named Handler Version

Instead of anonymous delegate:

```csharp
obj.ObjChanged += Obj_ObjChanged;

static void Obj_ObjChanged(object sender, ObjChangeEventArgs e)
{
    Console.WriteLine("Property changed to: " + e.PropChanged);
}
```

---

# ✅ Interview Important Points 🔥

If asked:

### ❓ What is the standard .NET event pattern?

Answer:

"The standard .NET event pattern uses EventHandler, where T derives from EventArgs. The handler takes two parameters: object sender and EventArgs-derived object containing event data."

---

### ❓ Why use EventArgs?

- Encapsulates event data
    
- Extensible
    
- Follows .NET conventions
    

---

### ❓ Difference Between Delegate and Event?

|Delegate|Event|
|---|---|
|Can be invoked anywhere|Only inside class|
|Can overwrite|Only += or -= outside|
|Less secure|More secure|

---

# ✅ Big Picture

You now understand:

✔ Multicast events  
✔ Anonymous event handlers  
✔ Named event handlers  
✔ .NET standard event pattern  
✔ EventArgs custom class  
✔ Sender concept

---

