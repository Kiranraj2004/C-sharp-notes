

In C#, you don’t always need to create your own interfaces.  
The .NET framework already provides many useful interfaces that solve common problems.

Before creating your own interface, always check:

> “Does .NET already provide something for this?”

---

# 🔹 Common Built-in .NET Interfaces

Here are some important ones:

---

## 1️⃣ `IComparable`

Used for sorting objects.

- Defines: `CompareTo()`
    
- Helps collections like `List<T>` sort objects.
    

---

## 2️⃣ `IComparer`

Also used for sorting, but allows custom comparison logic.

---

## 3️⃣ `IDisposable`

Used when your class manages unmanaged resources:

- File handles
    
- Database connections
    
- Network streams
    

Defines:

```csharp
void Dispose();
```

Used with:

```csharp
using (...)
{
}
```

---

## 4️⃣ `IEquatable<T>`

Used for comparing objects for equality.

Defines:

```csharp
bool Equals(T other);
```

---

## 5️⃣ `INotifyPropertyChanged` ⭐ (Today’s Focus)

Used to notify other objects when a property changes.

Very common in:

- WPF
    
- MVVM
    
- Data Binding
    
- UI applications
    

Namespace:

```csharp
using System.ComponentModel;
```

---

# 🎯 What Does `INotifyPropertyChanged` Provide?

It contains only ONE member:

```csharp
event PropertyChangedEventHandler PropertyChanged;
```

When a property changes,  
you raise this event to notify listeners.

---

# 🧩 Step-By-Step Example

We will modify our `Document` class.

---

## Step 1: Add Namespace

```csharp
using System;
using System.ComponentModel;
```

---

## Step 2: Implement Interface

```csharp
class Document : INotifyPropertyChanged
{
    private string docName;
    private bool needsSave;

    public event PropertyChangedEventHandler PropertyChanged;

    private void NotifyPropChanged(string propName)
    {
        PropertyChanged?.Invoke(this, 
            new PropertyChangedEventArgs(propName));
    }
```

---

## Step 3: Create Properties That Trigger Event

```csharp
    public string DocName
    {
        get { return docName; }
        set
        {
            docName = value;
            NotifyPropChanged(nameof(DocName));
        }
    }

    public bool NeedsSave
    {
        get { return needsSave; }
        set
        {
            needsSave = value;
            NotifyPropChanged(nameof(NeedsSave));
        }
    }
}
```

---

# 🔹 Explanation

Whenever a property changes:

```
DocName = "New Name";
```

It calls:

```
NotifyPropChanged("DocName");
```

Which triggers:

```
PropertyChanged event
```

---

# 🧩 Step 4: Listen for the Event

In `Main()`:

```csharp
class Program
{
    static void Main()
    {
        Document doc = new Document();

        doc.PropertyChanged += (sender, e) =>
        {
            Console.WriteLine("Document property changed: " + e.PropertyName);
        };

        doc.DocName = "My File";
        doc.NeedsSave = true;
    }
}
```

---

# ✅ Output:

```
Document property changed: DocName
Document property changed: NeedsSave
```

---

# 🔥 What Just Happened?

1. Property value changed.
    
2. Event was fired.
    
3. Listener caught event.
    
4. Printed property name.
    

---

# 🔹 Why Is This Useful?

Imagine:

- UI text box bound to DocName
    
- When DocName changes → UI updates automatically
    

That’s how data binding works internally.

---

# 🔥 Key Concepts

### ✔ Event

An event allows objects to subscribe and listen for changes.

### ✔ PropertyChangedEventArgs

Contains the name of the property that changed.

### ✔ PropertyChanged?.Invoke

Safely triggers the event.

---

# 🔹 Modern Shortcut

Instead of:

```csharp
NotifyPropChanged("DocName");
```

Use:

```csharp
NotifyPropChanged(nameof(DocName));
```

Safer (avoids typo errors).

---

# 🎯 Important Interview Points

- `INotifyPropertyChanged` is widely used in MVVM.
    
- It helps maintain loose coupling.
    
- It enables reactive UI updates.
    
- It uses events to notify changes.
    

---

# 🚀 Summary

|Concept|Meaning|
|---|---|
|Built-in Interfaces|Provided by .NET|
|INotifyPropertyChanged|Notifies when property changes|
|PropertyChanged Event|Triggered on property change|
|Event Subscription|Listeners respond to changes|
