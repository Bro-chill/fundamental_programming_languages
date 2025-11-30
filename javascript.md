# JavaScript Fundamentals

## Variables

```javascript
// Use 'let' when you need to change the value later
let name = "John";
name = "Jane";          // OK - can reassign

// Use 'const' when the value should never change
const age = 30;
// age = 31;             // ERROR - cannot reassign

// Avoid 'var' in modern JavaScript - use let/const instead
var isActive = true;
```

---

## Data Types

```javascript
// Primitives
const str = "Hello";          // String
const num = 42;               // Number
const bool = true;            // Boolean
const nothing = null;         // Null
const notDefined = undefined; // Undefined

// Objects
const obj = { name: "John", age: 30 };
const arr = [1, 2, 3];

// Type checking
typeof str;                   // "string"
Array.isArray(arr);           // true
```

---

## Strings

```javascript
const name = "John";
const age = 30;

// Template literals
const message = `Hello ${name}, you are ${age}`;

// Common methods
str.length;                   // Length
str.toUpperCase();            // "HELLO"
str.toLowerCase();            // "hello"
str.includes("llo");          // true
str.split(" ");               // ["Hello", "World"]
str.trim();                   // Remove whitespace
str.replace("old", "new");    // Replace text
```

---

## Arrays

```javascript
const fruits = ["apple", "banana", "orange"];

// Access
fruits[0];                    // "apple"
fruits.length;                // 3

// Add/Remove
fruits.push("mango");         // Add to end
fruits.pop();                 // Remove from end
fruits.unshift("grape");      // Add to start
fruits.shift();               // Remove from start

// Find
fruits.includes("apple");     // true
fruits.indexOf("banana");     // 1
fruits.find(f => f === "apple");

// Transform
fruits.map(f => f.toUpperCase());
fruits.filter(f => f.length > 5);
fruits.reduce((sum, f) => sum + 1, 0);

// Sort
fruits.sort();
numbers.sort((a, b) => a - b);
```

---

## Objects

```javascript
const user = {
  name: "John",
  age: 30,
  email: "john@example.com"
};

// Access
user.name;                    // "John"
user["name"];                 // "John"

// Modify
user.phone = "123-456";       // Add property
delete user.phone;            // Remove property

// Destructuring - extract values into variables
const { name, age } = user;   // name = "John", age = 30

// Spread operator - copy and merge objects
const updated = { ...user, age: 31 };  // Copy user, change age

// Methods
Object.keys(user);            // ["name", "age", "email"]
Object.values(user);          // ["John", 30, "john@..."]
```

---

## Functions

```javascript
// Function declaration
function greet(name) {
  return `Hello, ${name}!`;
}

// Arrow function
const greet = (name) => `Hello, ${name}!`;

// Default parameters
const greet = (name = "Guest") => `Hello, ${name}!`;

// Rest parameters
const sum = (...numbers) => numbers.reduce((a, b) => a + b, 0);
```

---

## Control Flow

```javascript
// If-else
if (age >= 18) {
  console.log("Adult");
} else if (age >= 13) {
  console.log("Teenager");
} else {
  console.log("Child");
}

// Ternary
const status = age >= 18 ? "Adult" : "Minor";

// Switch
switch (role) {
  case "admin":
    console.log("Full access");
    break;
  case "user":
    console.log("Limited access");
    break;
  default:
    console.log("No access");
}

// Nullish coalescing
const name = user.name ?? "Guest";

// Optional chaining
const city = user?.address?.city;
```

---

## Loops

```javascript
// For loop
for (let i = 0; i < 5; i++) {
  console.log(i);
}

// For...of (arrays)
for (const fruit of fruits) {
  console.log(fruit);
}

// For...in (objects)
for (const key in user) {
  console.log(`${key}: ${user[key]}`);
}

// forEach
fruits.forEach((fruit, index) => {
  console.log(`${index}: ${fruit}`);
});

// While
let count = 0;
while (count < 5) {
  console.log(count);
  count++;
}
```

---

## Classes

```javascript
class User {
  constructor(name, email) {
    this.name = name;
    this.email = email;
  }

  greet() {
    return `Hello, ${this.name}!`;
  }

  static create(data) {
    return new User(data.name, data.email);
  }
}

// Inheritance
class Admin extends User {
  constructor(name, email, permissions) {
    super(name, email);
    this.permissions = permissions;
  }
}

// Usage
const user = new User("John", "john@example.com");
console.log(user.greet());
```

---

## Promises & Async/Await

```javascript
// Promise
const fetchData = () => {
  return new Promise((resolve, reject) => {
    setTimeout(() => resolve("Data"), 1000);
  });
};

fetchData()
  .then(data => console.log(data))
  .catch(error => console.error(error));

// Async/Await
async function getData() {
  try {
    const response = await fetch("/api/data");
    const data = await response.json();
    return data;
  } catch (error) {
    console.error(error);
  }
}

// Parallel execution
const [users, posts] = await Promise.all([
  fetch("/api/users"),
  fetch("/api/posts")
]);
```

---

## Error Handling

```javascript
try {
  throw new Error("Something went wrong");
} catch (error) {
  console.error(error.message);
} finally {
  console.log("Cleanup");
}
```

---

## DOM Manipulation

```javascript
// Select elements
document.getElementById("myId");
document.querySelector(".myClass");
document.querySelectorAll("div");

// Modify elements
element.textContent = "New text";
element.innerHTML = "<b>Bold</b>";
element.classList.add("active");
element.style.color = "red";

// Events
element.addEventListener("click", (e) => {
  console.log("Clicked!", e.target);
});

// Create elements
const div = document.createElement("div");
div.textContent = "Hello";
document.body.appendChild(div);
```

---

## Local Storage

```javascript
// Store data
localStorage.setItem("user", JSON.stringify({ name: "John" }));

// Retrieve data
const user = JSON.parse(localStorage.getItem("user"));

// Remove data
localStorage.removeItem("user");
localStorage.clear();
```

---

## Modules

```javascript
// Export
export const add = (a, b) => a + b;
export default class User { }

// Import
import User, { add } from "./module.js";
import * as utils from "./utils.js";
```

---

## Useful Methods

```javascript
// JSON
JSON.stringify(obj);          // Object to JSON string
JSON.parse(jsonStr);          // JSON string to object

// Numbers
parseInt("42");               // 42
parseFloat("3.14");           // 3.14
Math.round(4.5);              // 5
Math.floor(4.9);              // 4
Math.ceil(4.1);               // 5
Math.random();                // 0-1
```