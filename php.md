# PHP Fundamentals

> PHP is a server-side scripting language mainly used for web development. Code runs on the server, not in the browser.

## Variables & Data Types

```php
<?php
// Variables (loosely typed)
$name = "John";           // String
$age = 30;                // Integer
$price = 19.99;           // Float
$isActive = true;         // Boolean
$nothing = null;          // Null

// Arrays
$fruits = ["apple", "banana", "orange"];
$user = [
    "name" => "John",
    "email" => "john@example.com",
    "age" => 30
];

// Constants
define("API_KEY", "abc123");
const MAX_USERS = 100;

// Type casting
$num = (int) "42";
$str = (string) 123;
?>
```

---

## Control Flow

```php
<?php
// If-else
if ($age >= 18) {
    echo "Adult";
} elseif ($age >= 13) {
    echo "Teenager";
} else {
    echo "Child";
}

// Ternary
$status = $isActive ? "Active" : "Inactive";

// Null coalescing
$username = $_GET['user'] ?? "Guest";

// Switch
switch ($role) {
    case "admin":
        echo "Full access";
        break;
    case "user":
        echo "Limited access";
        break;
    default:
        echo "No access";
}

// Match (PHP 8+)
$result = match($status) {
    "active" => "User is active",
    "pending" => "User is pending",
    default => "Unknown status"
};
?>
```

---

## Loops

```php
<?php
// For loop
for ($i = 0; $i < 5; $i++) {
    echo $i;
}

// Foreach
$users = ["John", "Jane", "Bob"];
foreach ($users as $user) {
    echo $user;
}

// Foreach with key
foreach ($user as $key => $value) {
    echo "$key: $value";
}

// While
$count = 0;
while ($count < 5) {
    echo $count;
    $count++;
}
?>
```

---

## Functions

```php
<?php
// Basic function
function greet($name) {
    return "Hello, $name!";
}

// Default parameters
function greet($name = "Guest") {
    return "Hello, $name!";
}

// Type hints (PHP 7+)
function add(int $a, int $b): int {
    return $a + $b;
}

// Nullable types
function findUser(?int $id): ?array {
    return $id ? ["id" => $id, "name" => "John"] : null;
}

// Arrow functions (PHP 7.4+)
$double = fn($n) => $n * 2;

// Variadic functions
function sum(...$numbers): int {
    return array_sum($numbers);
}
?>
```

---

## Arrays

```php
<?php
// Indexed array
$colors = ["red", "green", "blue"];

// Associative array
$person = [
    "name" => "John",
    "age" => 30
];

// Common array functions
$count = count($colors);
$merged = array_merge($arr1, $arr2);
$filtered = array_filter($numbers, fn($n) => $n > 10);
$mapped = array_map(fn($n) => $n * 2, $numbers);
$found = in_array("red", $colors);
$keys = array_keys($person);
$values = array_values($person);

// Array destructuring
[$first, $second] = $colors;
["name" => $name, "age" => $age] = $person;

// Spread operator
$all = [...$arr1, ...$arr2];
?>
```

---

## Classes & OOP

```php
<?php
class User {
    // Properties
    private int $id;
    public string $name;
    protected string $email;
    
    // Constructor
    public function __construct(string $name, string $email) {
        $this->id = rand();
        $this->name = $name;
        $this->email = $email;
    }
    
    // Method
    public function getEmail(): string {
        return $this->email;
    }
    
    // Static method
    public static function create(array $data): self {
        return new self($data['name'], $data['email']);
    }
}

// Constructor promotion (PHP 8+)
class Product {
    public function __construct(
        public string $name,
        public float $price,
        private int $stock = 0
    ) {}
}

// Inheritance
class Admin extends User {
    public function __construct(string $name, string $email, public array $permissions = []) {
        parent::__construct($name, $email);
    }
}

// Interface
interface Repository {
    public function find(int $id): ?array;
    public function save(array $data): bool;
}

// Trait
trait Timestamps {
    public DateTime $createdAt;
    public DateTime $updatedAt;
}
?>
```

---

## Error Handling

```php
<?php
// Try-catch
try {
    $result = riskyOperation();
} catch (Exception $e) {
    echo "Error: " . $e->getMessage();
} finally {
    echo "Cleanup";
}

// Custom exception
class ValidationException extends Exception {
    public function __construct(public array $errors) {
        parent::__construct("Validation failed");
    }
}

// Throwing exceptions
function divide(int $a, int $b): float {
    if ($b === 0) {
        throw new InvalidArgumentException("Cannot divide by zero");
    }
    return $a / $b;
}
?>
```

---

## Working with Forms

```php
<?php
// GET parameters
$search = $_GET['q'] ?? '';

// POST data
$name = $_POST['name'] ?? '';
$email = $_POST['email'] ?? '';

// Sanitize input
$name = htmlspecialchars(trim($_POST['name']));
$email = filter_var($_POST['email'], FILTER_SANITIZE_EMAIL);

// Validate
if (!filter_var($email, FILTER_VALIDATE_EMAIL)) {
    $errors[] = "Invalid email";
}

// File upload
if (isset($_FILES['avatar'])) {
    $file = $_FILES['avatar'];
    move_uploaded_file($file['tmp_name'], "uploads/" . $file['name']);
}
?>
```

---

## Database (PDO)

```php
<?php
// Connection
$pdo = new PDO(
    "mysql:host=localhost;dbname=myapp",
    "username",
    "password",
    [PDO::ATTR_ERRMODE => PDO::ERRMODE_EXCEPTION]
);

// Select with prepared statement
$stmt = $pdo->prepare("SELECT * FROM users WHERE id = ?");
$stmt->execute([$id]);
$user = $stmt->fetch(PDO::FETCH_ASSOC);

// Select all
$stmt = $pdo->query("SELECT * FROM users");
$users = $stmt->fetchAll(PDO::FETCH_ASSOC);

// Insert
$stmt = $pdo->prepare("INSERT INTO users (name, email) VALUES (?, ?)");
$stmt->execute([$name, $email]);
$newId = $pdo->lastInsertId();

// Update
$stmt = $pdo->prepare("UPDATE users SET name = ? WHERE id = ?");
$stmt->execute([$name, $id]);

// Delete
$stmt = $pdo->prepare("DELETE FROM users WHERE id = ?");
$stmt->execute([$id]);

// Named parameters
$stmt = $pdo->prepare("SELECT * FROM users WHERE email = :email");
$stmt->execute(['email' => $email]);
?>
```

---

## JSON & APIs

```php
<?php
// Encode to JSON
$data = ["name" => "John", "age" => 30];
$json = json_encode($data);

// Decode JSON
$decoded = json_decode($json, true); // true for associative array

// API response
header('Content-Type: application/json');
echo json_encode([
    "success" => true,
    "data" => $users
]);

// Read JSON input
$input = json_decode(file_get_contents('php://input'), true);

// HTTP request with cURL
$ch = curl_init("https://api.example.com/users");
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
$response = curl_exec($ch);
curl_close($ch);
?>
```

---

## Sessions & Cookies

```php
<?php
// Start session
session_start();

// Set session data
$_SESSION['user_id'] = 123;
$_SESSION['username'] = "john";

// Get session data
$userId = $_SESSION['user_id'] ?? null;

// Destroy session
session_destroy();

// Set cookie (expires in 7 days)
setcookie("remember_token", $token, time() + (7 * 24 * 60 * 60), "/");

// Get cookie
$token = $_COOKIE['remember_token'] ?? null;

// Delete cookie
setcookie("remember_token", "", time() - 3600, "/");
?>
```

---

## File Operations

```php
<?php
// Read file
$content = file_get_contents("file.txt");
$lines = file("file.txt", FILE_IGNORE_NEW_LINES);

// Write file
file_put_contents("file.txt", "Hello World");
file_put_contents("file.txt", "New line\n", FILE_APPEND);

// Check file exists
if (file_exists("file.txt")) {
    // File exists
}

// File info
$size = filesize("file.txt");
$modified = filemtime("file.txt");

// Directory operations
$files = scandir("./uploads");
mkdir("new_folder", 0755);
rmdir("empty_folder");
?>
```

---

## Useful String Functions

```php
<?php
$str = "Hello World";

strlen($str);                    // 11
strtolower($str);               // "hello world"
strtoupper($str);               // "HELLO WORLD"
trim("  hello  ");              // "hello"
str_replace("World", "PHP", $str); // "Hello PHP"
substr($str, 0, 5);             // "Hello"
strpos($str, "World");          // 6
explode(" ", $str);             // ["Hello", "World"]
implode(", ", $arr);            // "a, b, c"
sprintf("Hello %s", $name);     // Formatted string
?>
```

---

## Date & Time

```php
<?php
// Current date/time
$now = date("Y-m-d H:i:s");     // "2024-01-15 14:30:00"
$timestamp = time();            // Unix timestamp

// DateTime object
$date = new DateTime();
$date = new DateTime("2024-01-15");
$date->format("Y-m-d");         // "2024-01-15"

// Modify date
$date->modify("+1 week");
$date->add(new DateInterval("P1M")); // Add 1 month

// Compare dates
$date1 = new DateTime("2024-01-01");
$date2 = new DateTime("2024-12-31");
$diff = $date1->diff($date2);   // DateInterval object
echo $diff->days;               // Days between dates
?>
```
