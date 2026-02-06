
Comments are used to:

- Explain code
    
- Improve readability
    
- Help future you
    
- Help teammates
    
- Generate documentation (advanced use)
    

Comments are ignored by the compiler.

---

# 1️⃣ Single-Line Comments

## Syntax:

```csharp
// This is a single line comment
```

Use two forward slashes `//`

---

## Example:

```csharp
// This variable stores user age
int age = 21;
```

---

## When to Use?

✔ Small explanations  
✔ Temporary notes  
✔ Debugging  
✔ Short clarifications

Usually 1–3 lines max.

---

# 2️⃣ Multi-Line Comments

## Syntax:

```csharp
/*
   This is a multi-line comment
   It can span multiple lines
*/
```

Starts with:

```
/*
```

Ends with:

```
*/
```

---

## Example:

```csharp
/*
 This function calculates total marks
 and returns final score
*/
```

---

## When to Use?

✔ Large explanation  
✔ Temporary code blocking  
✔ Detailed notes

---

# 3️⃣ XML Documentation Comments (Very Important)

This is advanced and professional.

Starts with:

```csharp
///
```

Three forward slashes.

These allow automatic documentation generation.

---

## Example:

```csharp
/// <summary>
/// This is the main application function.
/// </summary>
/// <param name="args">
/// Array of command-line arguments.
/// </param>
/// <returns>
/// No return value.
/// </returns>
static void Main(string[] args)
{
}
```

---

# 🔎 Common XML Tags

|Tag|Purpose|
|---|---|
|`<summary>`|Describes method/class|
|`<param>`|Describes parameters|
|`<returns>`|Describes return value|
|`<remarks>`|Extra notes|
|`<example>`|Usage example|
|`<exception>`|Describes thrown exception|

There are ~20+ standard tags.

---

# ⚙️ How Documentation Gets Generated

By default, XML comments do nothing.

You must enable documentation generation in `.csproj`.

---

## Step 1: Open `.csproj` file

Add:

```xml
<GenerateDocumentationFile>true</GenerateDocumentationFile>
<DocumentationFile>Comments.xml</DocumentationFile>
```

Inside the `<PropertyGroup>` section.

---

## Step 2: Build Project

Run:

```
dotnet build
```

This generates:

```
Comments.xml
```

This file contains:

- Extracted summary
    
- Param details
    
- Return info
    

---

# 🧠 Why XML Documentation is Powerful

In large enterprise apps:

✔ API documentation auto-generated  
✔ Used by tools like Swagger  
✔ Used in libraries  
✔ Helps IntelliSense show method description

If you hover over a method in Visual Studio,  
the summary shows automatically.

Very professional feature.

---

# 🔥 Difference Between Comment Types

|Type|Purpose|Used For|
|---|---|---|
|`//`|Small notes|Simple explanation|
|`/* */`|Multi-line|Large explanation|
|`///`|Documentation|Professional API docs|

---

# 🧩 Best Practices (Very Important)

❌ Don’t write obvious comments

Bad:

```csharp
// Increment x by 1
x++;
```

Waste of comment.

---

✔ Write meaningful comments

Good:

```csharp
// Increment retry counter after failed login attempt
retryCount++;
```

Explain WHY, not WHAT.

---

✔ Use XML docs for:

- Public methods
    
- APIs
    
- Libraries
    
- Shared code
    

---

# 🎯 Interview-Level Understanding

If interviewer asks:

**What types of comments are available in C#?**

You say:

> C# supports single-line comments using //, multi-line comments using /* */, and XML documentation comments using ///, which can be used to generate documentation automatically.

Clean. Clear. Structured.

---

# 🚀 Pro Developer Tip

In real companies:

- Use comments to explain business logic
    
- Don’t over-comment
    
- Keep comments updated
    
- Use XML docs for public APIs
    

---

# ⚡ Bonus: Keyboard Shortcut

In VS Code:

Select lines →  
`Ctrl + /` → toggle comment

Very useful.

---
