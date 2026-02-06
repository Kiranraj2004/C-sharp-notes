
# 📘 **C# — Exceptions (Simple Notes)**

In programming, things can go wrong—just like in real life.\ To prevent the program from crashing and showing ugly error messages to the user, C# uses a system called **exception handling**.

---

# 🔹 **1. What is an Exception?**

An **exception** is an object representing an error or unexpected situation in a program.

Examples:

- Dividing by zero
- File not found
- Network not available
- Invalid input
- Out of range values

If not handled, exceptions crash the program and show long error messages.

---

# 🔹 **2. What is Exception Handling?**

Exception handling is a way to catch and manage errors so that:

✔ The program doesn’t crash\ ✔ The user sees a friendly message\ ✔ Your code remains clean and readable

---

# 🔹 **3. The `try` and `catch` Blocks**

### ✔ Basic structure

try

{

    // Code that might cause an error

}

catch

{

    // Code that runs if an error happens

}

---

# 🧪 **Example: Dividing by Zero**

Without exception handling:

int x = 10;

int y = 0;

  

int result = x / y; // 💥 crashes the program

This gives an error:

```
Unhandled exception: Attempted to divide by zero.
```

---

# ✔ Fixing it with try-catch

try

{

    int result = x / y;

}

catch

{

    Console.WriteLine("Whoops!");

}

Now instead of crashing, it prints:

```
Whoops!
```

---

# 🔹 **4. Catching Specific Exceptions**

Different errors have different exception types.\ You can catch _exactly_ the type you want.

Example:

catch (DivideByZeroException e)

{

    Console.WriteLine("Whoops!");

    Console.WriteLine(e.Message);

}

### Output:

```
Whoops!
Attempted to divide by zero.
```

✔ `e.Message` gives a useful error description\ ✔ Exceptions are objects, so they have properties like `Message`

---

# 🔹 **5. Throwing Your Own Exceptions**

You can manually create an exception when something is wrong in your logic.

Example:

if (x > 1000)

{

    throw new ArgumentOutOfRangeException("x", "X has to be 1000 or less");

}

This stops execution and creates an error for the catch block to handle.

---

# 🧪 **Handling this custom exception**

catch (ArgumentOutOfRangeException e)

{

    Console.WriteLine("Sorry, 1000 is the limit.");

    Console.WriteLine(e.Message);

}

### Output:

```
Sorry, 1000 is the limit.
X has to be 1000 or less
Parameter name: x
```

---

# 🔹 **6. The `finally` Block**

### ✔ Purpose:

Code inside `finally` **always runs**, no matter what.

✔ If no error happens → runs\ ✔ If an error happens → runs\ ✔ If a catch block runs → still runs

Used for cleanup, like:

- Closing files
- Releasing resources
- Closing database connections

### Structure:

try

{

    // risky code

}

catch (Exception e)

{

    // handle error

}

finally

{

    // always runs

    Console.WriteLine("This code always runs");

}

---

# 📘 **Exception Handling Flow**

```
1. Program enters try block
2. If no error → catch is skipped
3. If error occurs → jump to matching catch block
4. finally block runs in either case
```

---

# 📌 **7. Summary**

### ✔ **try**

Contains code that might cause an error.

### ✔ **catch**

Executes if an error occurs.\ You can have:

- A generic catch
- Multiple specific catch blocks
- Access to exception details (`e.Message`)

### ✔ **throw**

Used to manually create an exception.

### ✔ **finally**

Runs always — use it for cleanup tasks.

---

