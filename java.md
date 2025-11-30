# Java Fundamentals

## Variables & Data Types

```java
// Primitive types
int age = 30;
long population = 7800000000L;
double price = 19.99;
float rate = 3.14f;
boolean isActive = true;
char grade = 'A';

// Reference types
String name = "John";
Integer wrappedAge = 30;

// Constants
final double TAX_RATE = 0.08;

// Type inference (Java 10+) - compiler figures out the type
var message = "Hello";               // Inferred as String
var numbers = new ArrayList<Integer>(); // Inferred as ArrayList<Integer>
```

---

## Control Flow

```java
// If-else
if (age >= 18) {
    System.out.println("Adult");
} else if (age >= 13) {
    System.out.println("Teenager");
} else {
    System.out.println("Child");
}

// Ternary
String status = age >= 18 ? "Adult" : "Minor";

// Switch
switch (day) {
    case 1:
        System.out.println("Monday");
        break;
    case 2:
        System.out.println("Tuesday");
        break;
    default:
        System.out.println("Other day");
}

// Switch expression (Java 14+)
String dayName = switch (day) {
    case 1 -> "Monday";
    case 2 -> "Tuesday";
    default -> "Other";
};
```

---

## Loops

```java
// For loop
for (int i = 0; i < 5; i++) {
    System.out.println(i);
}

// Enhanced for loop
String[] names = {"John", "Jane", "Bob"};
for (String name : names) {
    System.out.println(name);
}

// While loop
int count = 0;
while (count < 5) {
    System.out.println(count);
    count++;
}
```

---

## Arrays & Collections

```java
// Arrays
int[] numbers = {1, 2, 3, 4, 5};
String[] names = new String[3];
numbers[0] = 10;

// ArrayList
List<String> list = new ArrayList<>();
list.add("John");
list.get(0);
list.remove(0);
list.size();

// HashMap
Map<String, Integer> map = new HashMap<>();
map.put("John", 30);
map.get("John");
map.containsKey("John");

// HashSet
Set<String> set = new HashSet<>();
set.add("John");
set.contains("John");
```

---

## Methods

```java
// Basic method
public String greet(String name) {
    return "Hello, " + name + "!";
}

// Method overloading
public int add(int a, int b) {
    return a + b;
}

public double add(double a, double b) {
    return a + b;
}

// Varargs
public int sum(int... numbers) {
    int total = 0;
    for (int n : numbers) {
        total += n;
    }
    return total;
}

// Static method
public static void main(String[] args) {
    System.out.println("Hello World");
}
```

---

## Classes & OOP

```java
public class User {
    // Fields
    private long id;
    private String name;
    private String email;

    // Constructor
    public User(String name, String email) {
        this.id = System.currentTimeMillis();
        this.name = name;
        this.email = email;
    }

    // Getters and Setters
    public String getName() { return name; }
    public void setName(String name) { this.name = name; }

    // Method
    public String greet() {
        return "Hello, " + name + "!";
    }

    @Override
    public String toString() {
        return "User{name='" + name + "'}";
    }
}

// Inheritance
public class Admin extends User {
    private List<String> permissions;

    public Admin(String name, String email, List<String> permissions) {
        super(name, email);
        this.permissions = permissions;
    }
}
```

---

## Interfaces & Abstract Classes

```java
// Interface - defines a contract that classes must follow
// Any class implementing this must have these methods
public interface Repository<T> {
    T findById(int id);
    List<T> findAll();
    T save(T entity);
    void delete(int id);
}

// Abstract class
public abstract class Shape {
    public abstract double getArea();
}

// Implementation
public class UserRepository implements Repository<User> {
    @Override
    public User findById(int id) { /* ... */ }
    // ... other methods
}
```

---

## Exception Handling

```java
// Try-catch-finally
try {
    int result = 10 / 0;
} catch (ArithmeticException e) {
    System.err.println("Error: " + e.getMessage());
} finally {
    System.out.println("Cleanup");
}

// Try-with-resources
try (BufferedReader reader = new BufferedReader(new FileReader("file.txt"))) {
    String line = reader.readLine();
} catch (IOException e) {
    e.printStackTrace();
}

// Throwing exceptions
public void validateAge(int age) {
    if (age < 0) {
        throw new IllegalArgumentException("Age cannot be negative");
    }
}
```

---

## Streams & Lambdas

```java
List<User> users = getUsers();

// Filter
List<User> activeUsers = users.stream()
    .filter(u -> u.isActive())
    .collect(Collectors.toList());

// Map
List<String> names = users.stream()
    .map(User::getName)
    .collect(Collectors.toList());

// Find
Optional<User> admin = users.stream()
    .filter(u -> u.getRole().equals("admin"))
    .findFirst();

// Sum
int totalAge = users.stream()
    .mapToInt(User::getAge)
    .sum();

// Sort
List<User> sorted = users.stream()
    .sorted(Comparator.comparing(User::getName))
    .collect(Collectors.toList());
```

---

## Optional

```java
// Create Optional
Optional<String> opt = Optional.of("value");
Optional<String> nullable = Optional.ofNullable(getValue());
Optional<String> empty = Optional.empty();

// Usage
String value = opt.orElse("default");
String value2 = opt.orElseThrow(() -> new RuntimeException("Not found"));

// Chaining
opt.filter(s -> s.length() > 5)
   .map(String::toUpperCase)
   .ifPresent(System.out::println);
```

---

## Records (Java 16+)

```java
// Simple record
public record User(Long id, String name, String email) {}

// Usage
User user = new User(1L, "John", "john@example.com");
System.out.println(user.name());  // "John"
```

---

## File I/O

```java
// Read file
String content = Files.readString(Path.of("file.txt"));
List<String> lines = Files.readAllLines(Path.of("file.txt"));

// Write file
Files.writeString(Path.of("file.txt"), "Hello World");
Files.write(Path.of("file.txt"), lines);
```

---

## Useful Classes

```java
// StringBuilder
StringBuilder sb = new StringBuilder();
sb.append("Hello").append(" ").append("World");
String result = sb.toString();

// Date/Time (Java 8+)
LocalDate today = LocalDate.now();
LocalDateTime now = LocalDateTime.now();
String formatted = now.format(DateTimeFormatter.ofPattern("yyyy-MM-dd"));

// Math
Math.max(a, b);
Math.min(a, b);
Math.abs(n);
Math.round(3.7);
Math.random();
```