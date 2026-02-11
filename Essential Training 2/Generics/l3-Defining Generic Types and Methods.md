
---

# 1️⃣ Defining a Generic Interface

Generic types are defined using angle brackets `< >`.

### Basic Syntax

```csharp
public interface IMapper<S, T>
{
    T Map(S source);
}
```

---

## 🧠 What does this mean?

- `S` = Source type
    
- `T` = Target type
    
- `Map` method:
    
    - Takes `S`
        
    - Returns `T`
        

So this interface says:

> "Give me two types. I will map from S → T."

This makes the interface reusable for ANY types.

---

# 2️⃣ Create Concrete Classes

## 🔹 Customer Class

```csharp
public class Customer
{
    public int Id { get; set; }
    public string FirstName { get; set; }
    public string LastName { get; set; }
    public DateTime CreateDate { get; set; }
}
```

---

## 🔹 Person Class

```csharp
public class Person
{
    public int Id { get; set; }
    public string FirstName { get; set; }
    public string LastName { get; set; }
    public int Age { get; set; }
}
```

---

# 3️⃣ Implementing the Generic Interface

Now we create a class that maps:

```
Customer → Person
```

### Implementation:

```csharp
public class CustomerToPersonMapper : IMapper<Customer, Person>
{
    public Person Map(Customer source)
    {
        return new Person
        {
            Id = source.Id,
            FirstName = source.FirstName,
            LastName = source.LastName,
            Age = 0   // No age in Customer, so default
        };
    }
}
```

---

## 🧠 What Just Happened?

When we wrote:

```csharp
IMapper<Customer, Person>
```

Compiler replaced:

```
S → Customer
T → Person
```

So the interface method:

```csharp
T Map(S source);
```

Becomes:

```csharp
Person Map(Customer source);
```

Fully type-safe.  
No casting.  
No confusion.

---

# 4️⃣ Using It in Program

```csharp
using System;

class Program
{
    static void Main()
    {
        Customer customer = new Customer
        {
            Id = 7,
            FirstName = "Customer",
            LastName = "First",
            CreateDate = new DateTime(2022, 1, 17)
        };

        CustomerToPersonMapper mapper = new CustomerToPersonMapper();

        Person p = mapper.Map(customer);

        Console.WriteLine($"Mapped Person: {p.FirstName} {p.LastName}");
        Console.WriteLine($"Person Age: {p.Age}");
    }
}
```

---

# ✅ Output

```
Mapped Person: Customer First
Person Age: 0
```

---

# 🔥 Important Observation

In `Main()`, you don’t see `<S, T>` anymore.

Why?

Because the generic types were already fixed here:

```csharp
CustomerToPersonMapper : IMapper<Customer, Person>
```

So now it's a normal strongly-typed class.

---

# 🎯 Why This Is Powerful

Without generics, you would need:

```csharp
interface ICustomerMapper
interface IOrderMapper
interface IEmployeeMapper
```

That’s messy.

With generics:

```csharp
IMapper<S, T>
```

Reusable for ANY type combination.

---

# 5️⃣ Naming Convention for Generic Types

Common naming patterns:

|Generic Name|Meaning|
|---|---|
|T|General Type|
|TKey|Key Type|
|TValue|Value Type|
|S|Source|
|T|Target|
|TSource|Source|
|TResult|Result|

---

# 6️⃣ Generic Type vs Generic Method

## Generic Type

```csharp
public interface IMapper<S, T>
```

Whole interface is generic.

---

## Generic Method

```csharp
public T Map<T>(object source)
```

Only the method is generic.

---

# 🧠 Interview-Level Understanding

If interviewer asks:

### ❓ Why use generic interface here?

Answer:

It allows creating a reusable mapping abstraction for any source and target types while maintaining compile-time type safety and avoiding casting.

---

### ❓ Why not use object instead?

Because:

- Loses type safety
    
- Requires casting
    
- Risk of runtime errors
    
- Harder to maintain
    

---

# 🔥 Real-World Usage

This pattern is commonly used in:

- DTO mapping
    
- AutoMapper libraries
    
- Repository pattern
    
- Service layers
    
- Clean Architecture
    

Example:

```csharp
IMapper<Order, OrderDTO>
IMapper<UserEntity, UserDTO>
IMapper<Product, ProductViewModel>
```

Same interface.  
Different types.  
Clean design.

---

