# TypeScript Fundamentals

> TypeScript = JavaScript + Types. It helps catch errors before running your code.

## Basic Types

```typescript
// Add ': type' after variable name to specify its type
let name: string = "John";    // Can only hold text
let age: number = 30;          // Can only hold numbers
let isActive: boolean = true;  // Can only hold true/false

// Arrays
let numbers: number[] = [1, 2, 3];
let names: Array<string> = ["John", "Jane"];

// Tuple
let user: [string, number] = ["John", 30];

// Any - disables type checking (avoid when possible)
let flexible: any = "anything";  // Can be anything - no safety

// Unknown - must check type before using (safer than any)
let uncertain: unknown = 4;       // Need to verify type before use
```

---

## Type Inference

```typescript
// TypeScript infers types automatically
let message = "Hello";       // string
let count = 42;              // number
let items = [1, 2, 3];       // number[]

// Type assertion
let value = someValue as string;
```

---

## Functions

```typescript
// Typed function
function greet(name: string): string {
  return `Hello, ${name}!`;
}

// Arrow function
const add = (a: number, b: number): number => a + b;

// Optional parameters
function greet(name: string, greeting?: string): string {
  return `${greeting || "Hello"}, ${name}!`;
}

// Default parameters
function greet(name: string, greeting: string = "Hello"): string {
  return `${greeting}, ${name}!`;
}

// Function type
type MathFunc = (a: number, b: number) => number;
const multiply: MathFunc = (a, b) => a * b;
```

---

## Interfaces

```typescript
// Object interface
interface User {
  id: number;
  name: string;
  email: string;
  age?: number;              // Optional
  readonly createdAt: Date;  // Cannot modify
}

// Extending interfaces
interface Admin extends User {
  permissions: string[];
}

// Usage
const user: User = {
  id: 1,
  name: "John",
  email: "john@example.com",
  createdAt: new Date()
};
```

---

## Type Aliases

```typescript
// Basic type alias
type ID = string | number;
type Status = "pending" | "active" | "inactive";

// Object type
type Point = {
  x: number;
  y: number;
};

// Union type
type Result = string | number;

// Intersection type
type Employee = User & { department: string };
```

---

## Generics

```typescript
// Generic function
function identity<T>(arg: T): T {
  return arg;
}
identity<string>("hello");
identity(42);  // Type inferred

// Generic interface
interface Repository<T> {
  find(id: number): T;
  save(item: T): T;
}

// Generic class
class Box<T> {
  private content: T;
  
  set(value: T): void {
    this.content = value;
  }
  
  get(): T {
    return this.content;
  }
}
```

---

## Enums

```typescript
// Numeric enum
enum Direction {
  Up,      // 0
  Down,    // 1
  Left,    // 2
  Right    // 3
}

// String enum
enum Status {
  Pending = "PENDING",
  Active = "ACTIVE",
  Inactive = "INACTIVE"
}

// Usage
let dir: Direction = Direction.Up;
let status: Status = Status.Active;
```

---

## Classes

```typescript
class User {
  private id: number;
  public name: string;
  protected email: string;

  constructor(name: string, email: string) {
    this.id = Date.now();
    this.name = name;
    this.email = email;
  }

  greet(): string {
    return `Hello, ${this.name}!`;
  }

  static create(data: { name: string; email: string }): User {
    return new User(data.name, data.email);
  }
}

// Inheritance
class Admin extends User {
  constructor(name: string, email: string, public permissions: string[]) {
    super(name, email);
  }
}
```

---

## Utility Types

```typescript
interface User {
  id: number;
  name: string;
  email: string;
}

// Partial - all properties optional
type PartialUser = Partial<User>;

// Required - all properties required
type RequiredUser = Required<User>;

// Readonly - all properties readonly
type ReadonlyUser = Readonly<User>;

// Pick - select specific properties
type UserName = Pick<User, "name" | "email">;

// Omit - exclude specific properties
type PublicUser = Omit<User, "id">;

// Record - create object type
type UserRoles = Record<string, "admin" | "user">;
```

---

## Type Guards

```typescript
// typeof guard
function process(value: string | number) {
  if (typeof value === "string") {
    return value.toUpperCase();
  }
  return value.toFixed(2);
}

// instanceof guard
if (error instanceof ValidationError) {
  console.log(error.errors);
}

// in operator
if ("email" in user) {
  console.log(user.email);
}
```

---

## Async/Await

```typescript
// Async function with types
async function fetchUser(id: number): Promise<User> {
  const response = await fetch(`/api/users/${id}`);
  return response.json();
}

// Error handling
async function getData(): Promise<Data | null> {
  try {
    const response = await fetch("/api/data");
    return await response.json();
  } catch (error) {
    console.error(error);
    return null;
  }
}
```

---

## Modules

```typescript
// Export
export interface User { }
export type ID = string | number;
export default class UserService { }

// Import
import UserService, { User, ID } from "./userService";
import type { User } from "./types";  // Type-only import
```

---

## tsconfig.json Basics

```json
{
  "compilerOptions": {
    "target": "ES2020",
    "module": "ESNext",
    "strict": true,
    "esModuleInterop": true,
    "skipLibCheck": true,
    "outDir": "./dist",
    "rootDir": "./src"
  },
  "include": ["src/**/*"],
  "exclude": ["node_modules"]
}
```