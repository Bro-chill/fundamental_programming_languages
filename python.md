# Python Fundamentals

## Variables & Data Types

```python
# Basic types
name = "John"           # String
age = 30                # Integer
price = 19.99           # Float
is_active = True        # Boolean
nothing = None          # None (null)

# Type conversion
str(42)                 # "42"
int("42")               # 42
float("3.14")           # 3.14

# f-strings (formatting)
message = f"Hello {name}, you are {age} years old"
```

---

## Collections

```python
# List - stores multiple items in order (can be changed)
fruits = ["apple", "banana", "orange"]
fruits.append("mango")      # Add to end
fruits.pop()                # Remove from end
fruits[0]                   # Access by index

# Dictionary - stores data as key:value pairs (like a phone book)
user = {
    "name": "John",
    "email": "john@example.com",
    "age": 30
}
user["name"]                # Access value
user.get("phone", "N/A")    # Get with default
user["phone"] = "123-456"   # Add/update

# Tuple - like a list but cannot be changed after creation
point = (10, 20)
point[0]                    # Access: 10

# Set - only stores unique values (no duplicates)
unique = {1, 2, 3, 3}       # Result: {1, 2, 3}
```

---

## Control Flow

```python
# If-elif-else
if age >= 18:
    print("Adult")
elif age >= 13:
    print("Teenager")
else:
    print("Child")

# Ternary
status = "Adult" if age >= 18 else "Minor"

# Match (Python 3.10+)
match status:
    case "active":
        print("Active user")
    case "pending":
        print("Pending user")
    case _:
        print("Unknown")
```

---

## Loops

```python
# For loop
for fruit in fruits:
    print(fruit)

# For with range
for i in range(5):          # 0 to 4
    print(i)

# For with enumerate
for index, fruit in enumerate(fruits):
    print(f"{index}: {fruit}")

# While loop
count = 0
while count < 5:
    print(count)
    count += 1

# List comprehension
squares = [x**2 for x in range(10)]
evens = [x for x in range(10) if x % 2 == 0]
```

---

## Functions

```python
# Basic function
def greet(name):
    return f"Hello, {name}!"

# Default parameters
def greet(name="Guest"):
    return f"Hello, {name}!"

# Multiple return values
def get_user():
    return "John", 30, "john@example.com"

name, age, email = get_user()

# *args and **kwargs
def func(*args, **kwargs):
    print(args)     # Tuple of positional args
    print(kwargs)   # Dict of keyword args

# Lambda
double = lambda x: x * 2
```

---

## Classes

```python
class User:
    def __init__(self, name, email):
        self.name = name
        self.email = email
    
    def greet(self):
        return f"Hello, {self.name}!"
    
    def __str__(self):
        return f"User({self.name})"

# Inheritance
class Admin(User):
    def __init__(self, name, email, permissions):
        super().__init__(name, email)
        self.permissions = permissions

# Usage
user = User("John", "john@example.com")
print(user.greet())
```

---

## Error Handling

```python
try:
    result = 10 / 0
except ZeroDivisionError as e:
    print(f"Error: {e}")
except Exception as e:
    print(f"Unexpected error: {e}")
finally:
    print("Cleanup")

# Raise exception
def validate_age(age):
    if age < 0:
        raise ValueError("Age cannot be negative")
```

---

## File Operations

```python
# Read file
with open("file.txt", "r") as f:
    content = f.read()
    # or lines = f.readlines()

# Write file
with open("file.txt", "w") as f:
    f.write("Hello World")

# Append to file
with open("file.txt", "a") as f:
    f.write("\nNew line")
```

---

## Working with JSON

```python
import json

# Dict to JSON string
data = {"name": "John", "age": 30}
json_str = json.dumps(data)

# JSON string to dict
parsed = json.loads(json_str)

# Read JSON file
with open("data.json", "r") as f:
    data = json.load(f)

# Write JSON file
with open("data.json", "w") as f:
    json.dump(data, f, indent=2)
```

---

## Useful Built-in Functions

```python
# Common functions
len([1, 2, 3])              # 3
max([1, 2, 3])              # 3
min([1, 2, 3])              # 1
sum([1, 2, 3])              # 6
sorted([3, 1, 2])           # [1, 2, 3]

# String methods
"hello".upper()             # "HELLO"
"HELLO".lower()             # "hello"
"  hello  ".strip()         # "hello"
"hello".replace("l", "x")   # "hexxo"
"a,b,c".split(",")          # ["a", "b", "c"]
",".join(["a", "b", "c"])   # "a,b,c"

# List methods
[1, 2, 3].index(2)          # 1
[1, 2, 3].count(2)          # 1
```

---

## Modules & Imports

```python
# Import module
import os
import json

# Import specific functions
from datetime import datetime, timedelta

# Import with alias
import numpy as np

# Common standard library
import os           # OS operations
import sys          # System operations
import json         # JSON handling
import datetime     # Date and time
import re           # Regular expressions
import random       # Random numbers
```

---

## Date & Time

```python
from datetime import datetime, date, timedelta

# Current date/time
now = datetime.now()
today = date.today()

# Formatting
now.strftime("%Y-%m-%d %H:%M:%S")  # "2024-01-15 14:30:00"

# Parsing
datetime.strptime("2024-01-15", "%Y-%m-%d")

# Arithmetic
tomorrow = today + timedelta(days=1)
next_week = today + timedelta(weeks=1)
```

---

## Virtual Environment

```bash
# Create virtual environment
python -m venv venv

# Activate (Windows)
venv\Scripts\activate

# Activate (Mac/Linux)
source venv/bin/activate

# Install packages
pip install requests

# Save dependencies
pip freeze > requirements.txt

# Install from requirements
pip install -r requirements.txt
```