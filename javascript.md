# JavaScript Fundamentals

## Variable Declaration

```javascript
// Using let (block-scoped, can be reassigned)
let name = "John";
name = "Jane"; // ✅ Valid

// Using const (block-scoped, cannot be reassigned)
const age = 30;
// age = 31; // ❌ Error

// Using var (function-scoped, avoid in modern JS)
var isActive = true;
```

## Functions

```javascript
// Regular function declaration (hoisted)
function greet(name) {
  return "Hello, " + name + "!";
}

// Function expression (not hoisted)
const greet = function(name) {
  return "Hello, " + name + "!";
};

// Arrow function (not hoisted, no 'this' binding)
const greet = (name) => {
  return "Hello, " + name + "!";
};

// Simplified arrow function (implicit return)
const greet = name => `Hello, ${name}!`;
```

## Data Types & Type Checking

```javascript
// Primitive types
const str = "Hello";           // string
const num = 42;               // number
const bool = true;            // boolean
const nothing = null;         // null
const notDefined = undefined; // undefined

// Check types (important for CRUD validation)
console.log(typeof str);      // "string"
console.log(Array.isArray([])); // true
console.log(num === parseInt(num)); // Check if integer
```

## Template Literals

```javascript
const name = "John";
const age = 30;

// String interpolation
const greeting = `Hello, ${name}! You are ${age} years old.`;

// Multi-line strings (useful for SQL queries, HTML templates)
const query = `
  SELECT * FROM users 
  WHERE age > ${age} 
  AND name = '${name}'
`;
```

## Data Handling

```javascript
// Object declaration
const user = {
  id: 1,
  name: "John",
  email: "john@example.com",
  age: 30,
  isActive: true,
  createdAt: new Date()
};

// Accessing properties
console.log(user.name);        // "John"
console.log(user["email"]);    // "john@example.com"

// Adding/updating properties
user.phone = "123-456-7890";   // Add new property
user.age = 31;                 // Update existing

// Deleting properties
delete user.phone;

// Object methods (useful for data manipulation)
const keys = Object.keys(user);       // Get all keys
const values = Object.values(user);   // Get all values
const entries = Object.entries(user); // Get key-value pairs
```

## Arrays

```javascript
const users = [
  { id: 1, name: "John", email: "john@example.com" },
  { id: 2, name: "Jane", email: "jane@example.com" }
];

// CRUD-related array methods
users.push(newUser);              // CREATE: Add to end
users.unshift(newUser);           // CREATE: Add to beginning
const user = users.find(u => u.id === 1);  // READ: Find by condition
const userIndex = users.findIndex(u => u.id === 1); // Find index
users[userIndex] = updatedUser;   // UPDATE: Replace item
users.splice(userIndex, 1);       // DELETE: Remove item
const filtered = users.filter(u => u.isActive); // Filter data
```

## Destructuring

```javascript
// Object destructuring (extract data from API responses)
const { id, name, email } = user;
const { data, status, message } = apiResponse;

// Array destructuring
const [first, second, ...rest] = users;

// Destructuring in function parameters
function createUser({ name, email, age = 18 }) {
  return { id: Date.now(), name, email, age };
}
```

## Spread Operator

```javascript
// Clone objects (important for state management)
const updatedUser = { ...user, name: "Updated Name" };

// Merge objects
const userWithProfile = { ...user, ...profile };

// Clone arrays
const newUsers = [...users];

// Add items to arrays
const usersWithNew = [...users, newUser];
```

## Array Data Processing

```javascript
const users = [
  { id: 1, name: "John", age: 30, salary: 50000 },
  { id: 2, name: "Jane", age: 25, salary: 60000 },
  { id: 3, name: "Bob", age: 35, salary: 55000 }
];

// Map: Transform data
const userNames = users.map(user => user.name);
const usersWithBonus = users.map(user => ({
  ...user,
  bonus: user.salary * 0.1
}));

// Filter: Find matching records
const youngUsers = users.filter(user => user.age < 30);
const highEarners = users.filter(user => user.salary > 55000);

// Find: Get single record
const john = users.find(user => user.name === "John");
const userById = users.find(user => user.id === 2);

// Reduce: Aggregate data
const totalSalary = users.reduce((sum, user) => sum + user.salary, 0);
const usersByAge = users.reduce((acc, user) => {
  acc[user.age] = user;
  return acc;
}, {});

// Some/Every: Check conditions
const hasYoungUsers = users.some(user => user.age < 30);
const allHighEarners = users.every(user => user.salary > 40000);
```

## Conditionals

```javascript
// If statement
if (user.age >= 18) {
  console.log("Adult");
} else if (user.age >= 13) {
  console.log("Teenager");
} else {
  console.log("Child");
}

// Ternary operator (great for conditional rendering)
const status = user.isActive ? "Active" : "Inactive";
const displayName = user.name || "Anonymous";

// Nullish coalescing (handle null/undefined)
const username = user.name ?? "Guest";
const userAge = user.age ?? 0;
```

## Loops

```javascript
// For loop
for (let i = 0; i < users.length; i++) {
  console.log(users[i]);
}

// For...of loop (iterate over arrays)
for (const user of users) {
  console.log(user.name);
}

// For...in loop (iterate over object properties)
for (const key in user) {
  console.log(`${key}: ${user[key]}`);
}

// forEach (functional approach)
users.forEach((user, index) => {
  console.log(`${index}: ${user.name}`);
});
```

## Error Handling

```javascript
// Try/catch for synchronous operations
function validateUser(user) {
  try {
    if (!user.name) throw new Error("Name is required");
    if (!user.email) throw new Error("Email is required");
    return { valid: true };
  } catch (error) {
    return { valid: false, error: error.message };
  }
}

// Try/catch with async operations
async function createUser(userData) {
  try {
    const response = await fetch('/api/users', {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify(userData)
    });
    
    if (!response.ok) {
      throw new Error(`HTTP error! status: ${response.status}`);
    }
    
    const user = await response.json();
    return { success: true, data: user };
  } catch (error) {
    console.error('Error creating user:', error);
    return { success: false, error: error.message };
  }
}
```

## Promises

```javascript
// Creating promises
const fetchUser = (id) => {
  return new Promise((resolve, reject) => {
    // Simulate API call
    setTimeout(() => {
      if (id > 0) {
        resolve({ id, name: "John", email: "john@example.com" });
      } else {
        reject(new Error("Invalid user ID"));
      }
    }, 1000);
  });
};

// Using promises
fetchUser(1)
  .then(user => console.log("User:", user))
  .catch(error => console.error("Error:", error))
  .finally(() => console.log("Request completed"));

// Promise.all for multiple operations
Promise.all([fetchUser(1), fetchUser(2), fetchUser(3)])
  .then(users => console.log("All users:", users))
  .catch(error => console.error("One or more requests failed:", error));
```

## Async/Await

```javascript
// CRUD operations with async/await
class UserService {
  static async createUser(userData) {
    try {
      const response = await fetch('/api/users', {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify(userData)
      });
      return await response.json();
    } catch (error) {
      throw new Error(`Failed to create user: ${error.message}`);
    }
  }

  static async getUser(id) {
    try {
      const response = await fetch(`/api/users/${id}`);
      if (!response.ok) throw new Error('User not found');
      return await response.json();
    } catch (error) {
      throw new Error(`Failed to get user: ${error.message}`);
    }
  }

  static async updateUser(id, userData) {
    try {
      const response = await fetch(`/api/users/${id}`, {
        method: 'PUT',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify(userData)
      });
      return await response.json();
    } catch (error) {
      throw new Error(`Failed to update user: ${error.message}`);
    }
  }

  static async deleteUser(id) {
    try {
      const response = await fetch(`/api/users/${id}`, {
        method: 'DELETE'
      });
      return response.ok;
    } catch (error) {
      throw new Error(`Failed to delete user: ${error.message}`);
    }
  }
}
```

## Classes

```javascript
class User {
  constructor(name, email, age) {
    this.id = Date.now(); // Simple ID generation
    this.name = name;
    this.email = email;
    this.age = age;
    this.createdAt = new Date();
  }

  // Instance methods
  validate() {
    const errors = [];
    if (!this.name) errors.push("Name is required");
    if (!this.email) errors.push("Email is required");
    if (this.age < 0) errors.push("Age must be positive");
    return errors;
  }

  toJSON() {
    return {
      id: this.id,
      name: this.name,
      email: this.email,
      age: this.age,
      createdAt: this.createdAt
    };
  }

  // Static methods (class-level operations)
  static fromJSON(data) {
    const user = new User(data.name, data.email, data.age);
    user.id = data.id;
    user.createdAt = new Date(data.createdAt);
    return user;
  }
}
```

## Modules

```javascript
// userService.js - Export functions
export const createUser = async (userData) => {
  // Implementation
};

export const getUsers = async () => {
  // Implementation
};

export const updateUser = async (id, userData) => {
  // Implementation
};

export const deleteUser = async (id) => {
  // Implementation
};

// Default export
export default class UserService {
  // Class implementation
}

// main.js - Import functions
import { createUser, getUsers } from './userService.js';
import UserService from './userService.js';
```

## JSON Handling

```javascript
// Convert object to JSON string
const user = { id: 1, name: "John", email: "john@example.com" };
const jsonString = JSON.stringify(user);

// Convert JSON string to object
const userData = '{"id":1,"name":"John","email":"john@example.com"}';
const userObject = JSON.parse(userData);

// Handle JSON parsing errors
function safeJsonParse(jsonString) {
  try {
    return { success: true, data: JSON.parse(jsonString) };
  } catch (error) {
    return { success: false, error: error.message };
  }
}
```

## Local Storage

```javascript
// Store data
const user = { id: 1, name: "John" };
localStorage.setItem('user', JSON.stringify(user));

// Retrieve data
const storedUser = JSON.parse(localStorage.getItem('user'));

// Remove data
localStorage.removeItem('user');

// Clear all data
localStorage.clear();

// Utility functions for localStorage
const storage = {
  set(key, value) {
    localStorage.setItem(key, JSON.stringify(value));
  },
  
  get(key) {
    const item = localStorage.getItem(key);
    return item ? JSON.parse(item) : null;
  },
  
  remove(key) {
    localStorage.removeItem(key);
  }
};
```

## Form Handling

```javascript
// Get form data
function getFormData(formElement) {
  const formData = new FormData(formElement);
  const data = {};
  
  for (let [key, value] of formData.entries()) {
    data[key] = value;
  }
  
  return data;
}

// Validate form data
function validateFormData(data) {
  const errors = {};
  
  if (!data.name || data.name.trim() === '') {
    errors.name = 'Name is required';
  }
  
  if (!data.email || !data.email.includes('@')) {
    errors.email = 'Valid email is required';
  }
  
  return {
    isValid: Object.keys(errors).length === 0,
    errors
  };
}
```

## Event Handling

```javascript
// Add event listeners
document.getElementById('createBtn').addEventListener('click', handleCreate);
document.getElementById('userForm').addEventListener('submit', handleSubmit);

// Event handler functions
function handleCreate(event) {
  event.preventDefault();
  // Create logic
}

function handleSubmit(event) {
  event.preventDefault();
  const formData = getFormData(event.target);
  // Process form data
}

// Event delegation (useful for dynamic content)
document.addEventListener('click', function(event) {
  if (event.target.classList.contains('delete-btn')) {
    const userId = event.target.dataset.userId;
    handleDelete(userId);
  }
});
```