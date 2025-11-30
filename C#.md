# C# Fundamentals

## Variables & Data Types

```csharp
// Value types
int age = 30;
long population = 7800000000L;
double price = 19.99;
float rate = 3.14f;
bool isActive = true;
char grade = 'A';

// Reference types
string name = "John";
object obj = new object();

// Nullable types - allows value types to be null
int? nullableAge = null;    // '?' makes int accept null

// Constants
const double TaxRate = 0.08;

// Type inference
var message = "Hello";
var numbers = new List<int>();
```

---

## Control Flow

```csharp
// If-else
if (age >= 18)
{
    Console.WriteLine("Adult");
}
else if (age >= 13)
{
    Console.WriteLine("Teenager");
}
else
{
    Console.WriteLine("Child");
}

// Ternary
string status = age >= 18 ? "Adult" : "Minor";

// Switch
switch (day)
{
    case 1:
        Console.WriteLine("Monday");
        break;
    case 2:
        Console.WriteLine("Tuesday");
        break;
    default:
        Console.WriteLine("Other day");
        break;
}

// Switch expression (C# 8+)
string dayName = day switch
{
    1 => "Monday",
    2 => "Tuesday",
    _ => "Other"
};

// Null coalescing
string name = user?.Name ?? "Guest";
```

---

## Loops

```csharp
// For loop
for (int i = 0; i < 5; i++)
{
    Console.WriteLine(i);
}

// Foreach
string[] names = { "John", "Jane", "Bob" };
foreach (string name in names)
{
    Console.WriteLine(name);
}

// While loop
int count = 0;
while (count < 5)
{
    Console.WriteLine(count);
    count++;
}
```

---

## Arrays & Collections

```csharp
// Arrays
int[] numbers = { 1, 2, 3, 4, 5 };
string[] names = new string[3];
numbers[0] = 10;

// List
List<string> list = new List<string>();
list.Add("John");
list[0];
list.Remove("John");
list.Count;

// Dictionary
Dictionary<string, int> dict = new Dictionary<string, int>();
dict["John"] = 30;
dict.TryGetValue("John", out int age);
dict.ContainsKey("John");

// HashSet
HashSet<string> set = new HashSet<string>();
set.Add("John");
set.Contains("John");
```

---

## Methods

```csharp
// Basic method
public string Greet(string name)
{
    return $"Hello, {name}!";
}

// Default parameters
public string Greet(string name = "Guest")
{
    return $"Hello, {name}!";
}

// Out parameters
public bool TryParse(string input, out int result)
{
    return int.TryParse(input, out result);
}

// Ref parameters
public void Swap(ref int a, ref int b)
{
    (a, b) = (b, a);
}

// Expression body
public string Greet(string name) => $"Hello, {name}!";
```

---

## Classes & OOP

```csharp
public class User
{
    // Properties
    public long Id { get; private set; }
    public string Name { get; set; }
    public string Email { get; set; }

    // Constructor
    public User(string name, string email)
    {
        Id = DateTime.Now.Ticks;
        Name = name;
        Email = email;
    }

    // Method
    public string Greet()
    {
        return $"Hello, {Name}!";
    }

    public override string ToString()
    {
        return $"User{{Name='{Name}'}}";
    }
}

// Inheritance
public class Admin : User
{
    public List<string> Permissions { get; set; }

    public Admin(string name, string email, List<string> permissions)
        : base(name, email)
    {
        Permissions = permissions;
    }
}
```

---

## Interfaces & Abstract Classes

```csharp
// Interface
public interface IRepository<T>
{
    T FindById(int id);
    IEnumerable<T> FindAll();
    T Save(T entity);
    void Delete(int id);
}

// Abstract class
public abstract class Shape
{
    public abstract double GetArea();
}

// Implementation
public class UserRepository : IRepository<User>
{
    public User FindById(int id) { /* ... */ }
    // ... other methods
}
```

---

## Exception Handling

```csharp
// Try-catch-finally
try
{
    int result = 10 / 0;
}
catch (DivideByZeroException ex)
{
    Console.Error.WriteLine($"Error: {ex.Message}");
}
finally
{
    Console.WriteLine("Cleanup");
}

// Using statement
using (var reader = new StreamReader("file.txt"))
{
    string content = reader.ReadToEnd();
}

// Using declaration (C# 8+)
using var reader = new StreamReader("file.txt");

// Throwing exceptions
public void ValidateAge(int age)
{
    if (age < 0)
        throw new ArgumentException("Age cannot be negative");
}
```

---

## LINQ

> LINQ (Language Integrated Query) - query collections like a database

```csharp
List<User> users = GetUsers();

// Where - filter items (like SQL WHERE)
var activeUsers = users.Where(u => u.IsActive);

// Select (map)
var names = users.Select(u => u.Name);

// First/FirstOrDefault
var admin = users.FirstOrDefault(u => u.Role == "admin");

// OrderBy
var sorted = users.OrderBy(u => u.Name);

// GroupBy
var byRole = users.GroupBy(u => u.Role);

// Any/All
bool hasAdmin = users.Any(u => u.Role == "admin");
bool allActive = users.All(u => u.IsActive);

// Query syntax
var query = from u in users
            where u.IsActive
            orderby u.Name
            select u.Name;
```

---

## Async/Await

```csharp
// Async method
public async Task<User> GetUserAsync(int id)
{
    var response = await httpClient.GetAsync($"/api/users/{id}");
    return await response.Content.ReadFromJsonAsync<User>();
}

// Async with error handling
public async Task<User?> GetUserSafeAsync(int id)
{
    try
    {
        return await GetUserAsync(id);
    }
    catch (Exception ex)
    {
        Console.Error.WriteLine(ex.Message);
        return null;
    }
}

// Parallel tasks
var tasks = new[] { GetUserAsync(1), GetUserAsync(2) };
var users = await Task.WhenAll(tasks);
```

---

## Records (C# 9+)

```csharp
// Simple record
public record User(long Id, string Name, string Email);

// Usage
var user = new User(1, "John", "john@example.com");
var updated = user with { Name = "Jane" };
```

---

## File I/O

```csharp
// Read file
string content = File.ReadAllText("file.txt");
string[] lines = File.ReadAllLines("file.txt");

// Write file
File.WriteAllText("file.txt", "Hello World");
File.WriteAllLines("file.txt", lines);

// Async
string content = await File.ReadAllTextAsync("file.txt");
await File.WriteAllTextAsync("file.txt", "Hello World");
```

---

## String Operations

```csharp
// String interpolation
string message = $"Hello, {name}!";

// Common methods
str.ToUpper();
str.ToLower();
str.Trim();
str.Split(',');
string.Join(",", array);
str.Contains("text");
str.Replace("old", "new");

// StringBuilder
var sb = new StringBuilder();
sb.Append("Hello");
sb.Append(" World");
string result = sb.ToString();
```

---

## Useful Types

```csharp
// DateTime
DateTime now = DateTime.Now;
DateTime today = DateTime.Today;
DateTime parsed = DateTime.Parse("2024-01-15");
string formatted = now.ToString("yyyy-MM-dd HH:mm:ss");

// TimeSpan
TimeSpan duration = TimeSpan.FromHours(2);
DateTime future = now.Add(duration);

// Guid
Guid id = Guid.NewGuid();
string idString = id.ToString();
```