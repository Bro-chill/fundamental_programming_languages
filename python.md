# Python Fundamentals

## Variable

**Data Types:**
```python
# String
text = "Hello, World!"

# Integer
count = 42

# Float
price = 19.99

# Boolean
is_active = True

# None (null value)
result = None
```

**Lists:**
```python
# Creating a list
fruits = ["apple", "banana", "orange"]

# Accessing elements (zero-indexed)
first_fruit = fruits[0]  # "apple"

# Modifying lists
fruits.append("mango")  # Add to end
fruits.pop()            # Remove from end
fruits.insert(1, "grape")  # Insert at position

# List methods for CRUD operations
fruits.remove("apple")  # Remove specific item
fruits.clear()          # Remove all items
```

**Dictionaries:**
```python
# Creating a dictionary
person = {
    "name": "John",
    "age": 30,
    "city": "New York"
}

# Accessing values
print(person["name"])  # "John"

# Adding or modifying
person["email"] = "john@example.com"

# Get with default value
phone = person.get("phone", "Not available")

# Dictionary methods for CRUD
person.update({"age": 31, "phone": "123-456-7890"})  # Update multiple
del person["city"]  # Delete key
person.pop("email", None)  # Safe delete with default
```

**Conditional Statements:**
```python
# If-elif-else statement
if age < 13:
    print("Child")
elif age < 20:
    print("Teenager")
else:
    print("Adult")

# Ternary operator (conditional expression)
status = "Adult" if age >= 18 else "Minor"
```

**Loops:**
```python
# For loop with range
for i in range(5):  # 0 to 4
    print(i)

# For loop with list
for fruit in fruits:
    print(fruit)

# While loop
count = 0
while count < 5:
    print(count)
    count += 1

# Enumerate for index and value
for index, fruit in enumerate(fruits):
    print(f"{index}: {fruit}")
```

**Functions:**
```python
# Defining a function
def greet(name):
    return f"Hello, {name}!"

# Function with default parameter
def greet(name="Guest"):
    return f"Hello, {name}!"

# Function with multiple return values
def get_user_info(user_id):
    # Simulate database lookup
    return "John", 30, "john@example.com"

# Calling functions
message = greet("John")  # "Hello, John!"
name, age, email = get_user_info(1)
```

## CRUD-Features

**Handling JSON:**
```python
import json

# Converting Python dict to JSON string
user_data = {"name": "John", "age": 30, "email": "john@example.com"}
json_string = json.dumps(user_data)

# Converting JSON string to Python dict
json_data = '{"name": "John", "age": 30}'
user_dict = json.loads(json_data)

# Reading JSON from file
with open("users.json", "r") as file:
    users = json.load(file)

# Writing JSON to file
with open("users.json", "w") as file:
    json.dump(users, file, indent=2)
```

**Data Validation:**
```python
# Input validation for CRUD operations
def validate_user_data(data):
    required_fields = ["name", "email", "age"]
    
    # Check if all required fields are present
    for field in required_fields:
        if field not in data:
            raise ValueError(f"Missing required field: {field}")
    
    # Type validation
    if not isinstance(data["name"], str) or len(data["name"]) < 2:
        raise ValueError("Name must be a string with at least 2 characters")
    
    if not isinstance(data["age"], int) or data["age"] < 0:
        raise ValueError("Age must be a positive integer")
    
    # Email validation (basic)
    if "@" not in data["email"]:
        raise ValueError("Invalid email format")
    
    return True

# Usage
try:
    user_data = {"name": "John", "email": "john@example.com", "age": 30}
    validate_user_data(user_data)
    print("Data is valid")
except ValueError as e:
    print(f"Validation error: {e}")
```

**Dates and Times:**
```python
from datetime import datetime, date, timedelta
import time

# Current timestamp
now = datetime.now()
today = date.today()

# Formatting dates for database storage
iso_format = now.isoformat()  # "2023-12-01T14:30:00"
date_string = now.strftime("%Y-%m-%d %H:%M:%S")

# Parsing date strings
date_obj = datetime.strptime("2023-12-01", "%Y-%m-%d")

# Unix timestamp (common in APIs)
timestamp = int(time.time())
from_timestamp = datetime.fromtimestamp(timestamp)
```

**Environment(.env) Configuration:**
```python
import os
from dotenv import load_dotenv  # pip install python-dotenv

# Load environment variables from .env file
load_dotenv()

# Database configuration
DATABASE_URL = os.getenv("DATABASE_URL", "sqlite:///default.db")
API_KEY = os.getenv("API_KEY")
DEBUG_MODE = os.getenv("DEBUG", "False").lower() == "true"

# Configuration class
class Config:
    DATABASE_URL = os.getenv("DATABASE_URL", "sqlite:///app.db")
    SECRET_KEY = os.getenv("SECRET_KEY", "dev-secret-key")
    DEBUG = os.getenv("DEBUG", "False").lower() == "true"
```

**HTTP Status Codes and Error Handling:**
```python
# HTTP status codes for CRUD operations
HTTP_STATUS = {
    "OK": 200,
    "CREATED": 201,
    "NO_CONTENT": 204,
    "BAD_REQUEST": 400,
    "NOT_FOUND": 404,
    "INTERNAL_ERROR": 500
}

# Custom exceptions for CRUD operations
class UserNotFoundError(Exception):
    pass

class ValidationError(Exception):
    pass

class DatabaseError(Exception):
    pass

# Error handling in CRUD functions
def get_user_by_id(user_id):
    try:
        # Simulate database query
        if user_id <= 0:
            raise ValidationError("User ID must be positive")
        
        # Simulate user not found
        if user_id > 1000:
            raise UserNotFoundError(f"User with ID {user_id} not found")
        
        return {"id": user_id, "name": "John", "email": "john@example.com"}
    
    except ValidationError as e:
        print(f"Validation error: {e}")
        return None
    except UserNotFoundError as e:
        print(f"Not found: {e}")
        return None
    except Exception as e:
        print(f"Unexpected error: {e}")
        return None
```

**Data Structure:**
```python
# User model as a class
class User:
    def __init__(self, id=None, name=None, email=None, created_at=None):
        self.id = id
        self.name = name
        self.email = email
        self.created_at = created_at or datetime.now()
    
    def to_dict(self):
        """Convert user object to dictionary for JSON serialization"""
        return {
            "id": self.id,
            "name": self.name,
            "email": self.email,
            "created_at": self.created_at.isoformat()
        }
    
    @classmethod
    def from_dict(cls, data):
        """Create user object from dictionary"""
        return cls(
            id=data.get("id"),
            name=data.get("name"),
            email=data.get("email"),
            created_at=datetime.fromisoformat(data["created_at"]) if data.get("created_at") else None
        )
    
    def __repr__(self):
        return f"User(id={self.id}, name='{self.name}', email='{self.email}')"

# In-memory database simulation
class UserDatabase:
    def __init__(self):
        self.users = {}
        self.next_id = 1
    
    def create_user(self, name, email):
        """Create a new user"""
        user = User(id=self.next_id, name=name, email=email)
        self.users[self.next_id] = user
        self.next_id += 1
        return user
    
    def get_user(self, user_id):
        """Read a user by ID"""
        return self.users.get(user_id)
    
    def get_all_users(self):
        """Read all users"""
        return list(self.users.values())
    
    def update_user(self, user_id, **kwargs):
        """Update a user"""
        if user_id not in self.users:
            return None
        
        user = self.users[user_id]
        for key, value in kwargs.items():
            if hasattr(user, key):
                setattr(user, key, value)
        
        return user
    
    def delete_user(self, user_id):
        """Delete a user"""
        return self.users.pop(user_id, None)
```

**String Formatting:**
```python
# f-strings (Python 3.6+) - Best for simple formatting
name = "John"
age = 30
message = f"My name is {name} and I am {age} years old."

# For API responses
def format_api_response(status, data=None, message=None):
    return {
        "status": status,
        "data": data,
        "message": message,
        "timestamp": datetime.now().isoformat()
    }

# SQL query templates (be careful with SQL injection)
def build_select_query(table, conditions=None):
    query = f"SELECT * FROM {table}"
    if conditions:
        where_clause = " AND ".join([f"{k} = ?" for k in conditions.keys()])
        query += f" WHERE {where_clause}"
    return query
```

**Data Processing:**
```python
# Filter and transform data
users = [
    {"id": 1, "name": "John", "age": 30, "active": True},
    {"id": 2, "name": "Jane", "age": 25, "active": False},
    {"id": 3, "name": "Bob", "age": 35, "active": True}
]

# Get active users
active_users = [user for user in users if user["active"]]

# Get user names only
user_names = [user["name"] for user in users]

# Transform data structure
user_lookup = {user["id"]: user["name"] for user in users}

# Filter and transform in one step
active_user_emails = [f"{user['name'].lower()}@example.com" 
                     for user in users if user["active"]]
```

**Data Persistence:**
```python
import csv

# Reading CSV data
def read_users_from_csv(filename):
    users = []
    with open(filename, "r", newline="") as file:
        reader = csv.DictReader(file)
        for row in reader:
            users.append(row)
    return users

# Writing CSV data
def write_users_to_csv(users, filename):
    if not users:
        return
    
    with open(filename, "w", newline="") as file:
        fieldnames = users[0].keys()
        writer = csv.DictWriter(file, fieldnames=fieldnames)
        writer.writeheader()
        writer.writerows(users)

# Log file operations
def log_crud_operation(operation, user_id, details=""):
    timestamp = datetime.now().strftime("%Y-%m-%d %H:%M:%S")
    log_entry = f"[{timestamp}] {operation} - User ID: {user_id} - {details}\n"
    
    with open("crud_operations.log", "a") as log_file:
        log_file.write(log_entry)
```

**Decorators:**
```python
from functools import wraps

# Logging decorator
def log_operation(operation_type):
    def decorator(func):
        @wraps(func)
        def wrapper(*args, **kwargs):
            start_time = time.time()
            try:
                result = func(*args, **kwargs)
                end_time = time.time()
                print(f"{operation_type} completed in {end_time - start_time:.2f}s")
                return result
            except Exception as e:
                print(f"{operation_type} failed: {e}")
                raise
        return wrapper
    return decorator

# Validation decorator
def validate_input(validator_func):
    def decorator(func):
        @wraps(func)
        def wrapper(*args, **kwargs):
            # Assume first argument is data to validate
            if args:
                validator_func(args[0])
            return func(*args, **kwargs)
        return wrapper
    return decorator

# Usage
@log_operation("CREATE_USER")
@validate_input(validate_user_data)
def create_user(user_data):
    # Create user logic here
    return User(**user_data)
```

**Exception Handling:**
```python
def safe_crud_operation(operation_func, *args, **kwargs):
    """Wrapper for safe CRUD operations with proper error handling"""
    try:
        return {
            "success": True,
            "data": operation_func(*args, **kwargs),
            "error": None
        }
    except ValidationError as e:
        return {
            "success": False,
            "data": None,
            "error": {"type": "validation", "message": str(e)}
        }
    except UserNotFoundError as e:
        return {
            "success": False,
            "data": None,
            "error": {"type": "not_found", "message": str(e)}
        }
    except Exception as e:
        return {
            "success": False,
            "data": None,
            "error": {"type": "internal", "message": "An unexpected error occurred"}
        }

# Usage
result = safe_crud_operation(get_user_by_id, 123)
if result["success"]:
    print(f"User found: {result['data']}")
else:
    print(f"Error: {result['error']['message']}")
```

**APIs & HTTP Requests:**
```python
import requests  # pip install requests

# Making HTTP requests for external APIs
def fetch_user_from_api(user_id):
    try:
        response = requests.get(f"https://api.example.com/users/{user_id}")
        response.raise_for_status()  # Raises an HTTPError for bad responses
        return response.json()
    except requests.exceptions.RequestException as e:
        print(f"API request failed: {e}")
        return None

# Sending data to external APIs
def send_user_to_api(user_data):
    try:
        response = requests.post(
            "https://api.example.com/users",
            json=user_data,
            headers={"Content-Type": "application/json"}
        )
        response.raise_for_status()
        return response.json()
    except requests.exceptions.RequestException as e:
        print(f"Failed to send data: {e}")
        return None
```

## Advanced Features

**Context Management:**
```python
from contextlib import contextmanager

@contextmanager
def database_transaction():
    """Simulate database transaction context manager"""
    print("Starting transaction...")
    try:
        yield
        print("Committing transaction...")
    except Exception as e:
        print(f"Rolling back transaction due to error: {e}")
        raise
    finally:
        print("Closing database connection...")

# Usage
try:
    with database_transaction():
        # Perform multiple CRUD operations
        create_user({"name": "John", "email": "john@example.com"})
        update_user(1, name="John Doe")
except Exception as e:
    print(f"Transaction failed: {e}")
```

**Data Processing:**
```python
def process_large_dataset(filename):
    """Generator for processing large CSV files without loading everything into memory"""
    with open(filename, 'r') as file:
        reader = csv.DictReader(file)
        for row in reader:
            # Process each row individually
            yield {
                'id': int(row['id']),
                'name': row['name'].strip().title(),
                'email': row['email'].lower(),
                'created_at': datetime.strptime(row['created_at'], '%Y-%m-%d')
            }

# Usage for batch processing
def batch_import_users(filename, batch_size=100):
    batch = []
    for user_data in process_large_dataset(filename):
        batch.append(user_data)
        
        if len(batch) >= batch_size:
            # Process batch
            for user in batch:
                create_user(user['name'], user['email'])
            batch = []
            print(f"Processed batch of {batch_size} users")
    
    # Process remaining users
    if batch:
        for user in batch:
            create_user(user['name'], user['email'])
        print(f"Processed final batch of {len(batch)} users")
```

**Async/Await:**
```python
import asyncio
import aiohttp  # pip install aiohttp
import aiofiles  # pip install aiofiles

# Async CRUD operations
async def async_get_user(session, user_id):
    """Async function to fetch user from API"""
    try:
        async with session.get(f"https://api.example.com/users/{user_id}") as response:
            if response.status == 200:
                return await response.json()
            else:
                return None
    except Exception as e:
        print(f"Error fetching user {user_id}: {e}")
        return None

async def async_create_user(session, user_data):
    """Async function to create user via API"""
    try:
        async with session.post(
            "https://api.example.com/users",
            json=user_data
        ) as response:
            if response.status == 201:
                return await response.json()
            else:
                return None
    except Exception as e:
        print(f"Error creating user: {e}")
        return None

async def batch_process_users(user_ids):
    """Process multiple users concurrently"""
    async with aiohttp.ClientSession() as session:
        tasks = [async_get_user(session, user_id) for user_id in user_ids]
        results = await asyncio.gather(*tasks, return_exceptions=True)
        
        users = []
        for result in results:
            if isinstance(result, dict):
                users.append(result)
        
        return users

# Async file operations
async def async_save_users_to_file(users, filename):
    """Async function to save users to file"""
    async with aiofiles.open(filename, 'w') as file:
        await file.write(json.dumps(users, indent=2))

# Usage
async def main():
    user_ids = [1, 2, 3, 4, 5]
    users = await batch_process_users(user_ids)
    await async_save_users_to_file(users, 'users.json')
    print(f"Processed {len(users)} users")

# Run async code
# asyncio.run(main())
```

**Database Integration:**
```python
import sqlite3
from contextlib import contextmanager

class DatabaseManager:
    def __init__(self, db_path):
        self.db_path = db_path
        self.init_database()
    
    def init_database(self):
        """Initialize database with users table"""
        with self.get_connection() as conn:
            conn.execute('''
                CREATE TABLE IF NOT EXISTS users (
                    id INTEGER PRIMARY KEY AUTOINCREMENT,
                    name TEXT NOT NULL,
                    email TEXT UNIQUE NOT NULL,
                    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
                    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
                )
            ''')
            conn.commit()
    
    @contextmanager
    def get_connection(self):
        """Context manager for database connections"""
        conn = sqlite3.connect(self.db_path)
        conn.row_factory = sqlite3.Row  # Enable dict-like access
        try:
            yield conn
        finally:
            conn.close()
    
    def create_user(self, name, email):
        """Create a new user"""
        with self.get_connection() as conn:
            cursor = conn.execute(
                "INSERT INTO users (name, email) VALUES (?, ?)",
                (name, email)
            )
            conn.commit()
            return cursor.lastrowid
    
    def get_user(self, user_id):
        """Get user by ID"""
        with self.get_connection() as conn:
            cursor = conn.execute(
                "SELECT * FROM users WHERE id = ?",
                (user_id,)
            )
            row = cursor.fetchone()
            return dict(row) if row else None
    
    def get_all_users(self, limit=None, offset=0):
        """Get all users with pagination"""
        query = "SELECT * FROM users ORDER BY created_at DESC"
        params = []
        
        if limit:
            query += " LIMIT ? OFFSET ?"
            params.extend([limit, offset])
        
        with self.get_connection() as conn:
            cursor = conn.execute(query, params)
            return [dict(row) for row in cursor.fetchall()]
    
    def update_user(self, user_id, **kwargs):
        """Update user with dynamic fields"""
        if not kwargs:
            return False
        
        # Build dynamic UPDATE query
        set_clause = ", ".join([f"{key} = ?" for key in kwargs.keys()])
        query = f"UPDATE users SET {set_clause}, updated_at = CURRENT_TIMESTAMP WHERE id = ?"
        params = list(kwargs.values()) + [user_id]
        
        with self.get_connection() as conn:
            cursor = conn.execute(query, params)
            conn.commit()
            return cursor.rowcount > 0
    
    def delete_user(self, user_id):
        """Delete user by ID"""
        with self.get_connection() as conn:
            cursor = conn.execute("DELETE FROM users WHERE id = ?", (user_id,))
            conn.commit()
            return cursor.rowcount > 0
    
    def search_users(self, search_term):
        """Search users by name or email"""
        with self.get_connection() as conn:
            cursor = conn.execute(
                "SELECT * FROM users WHERE name LIKE ? OR email LIKE ?",
                (f"%{search_term}%", f"%{search_term}%")
            )
            return [dict(row) for row in cursor.fetchall()]

# Usage
db = DatabaseManager("users.db")

# Create
user_id = db.create_user("John Doe", "john@example.com")

# Read
user = db.get_user(user_id)
all_users = db.get_all_users(limit=10)

# Update
db.update_user(user_id, name="John Smith", email="johnsmith@example.com")

# Delete
db.delete_user(user_id)
```

**Caching:**
```python
from functools import lru_cache
import time

class CachedUserService:
    def __init__(self, db_manager):
        self.db = db_manager
        self._cache = {}
        self._cache_timeout = 300  # 5 minutes
    
    def _is_cache_valid(self, cache_entry):
        """Check if cache entry is still valid"""
        return time.time() - cache_entry['timestamp'] < self._cache_timeout
    
    def get_user_cached(self, user_id):
        """Get user with caching"""
        cache_key = f"user_{user_id}"
        
        # Check cache first
        if cache_key in self._cache:
            cache_entry = self._cache[cache_key]
            if self._is_cache_valid(cache_entry):
                print(f"Cache hit for user {user_id}")
                return cache_entry['data']
            else:
                # Remove expired cache entry
                del self._cache[cache_key]
        
        # Fetch from database
        print(f"Cache miss for user {user_id}, fetching from DB")
        user = self.db.get_user(user_id)
        
        # Cache the result
        if user:
            self._cache[cache_key] = {
                'data': user,
                'timestamp': time.time()
            }
        
        return user
    
    def invalidate_user_cache(self, user_id):
        """Invalidate cache for specific user"""
        cache_key = f"user_{user_id}"
        self._cache.pop(cache_key, None)
    
    def clear_cache(self):
        """Clear all cache"""
        self._cache.clear()

# Using functools.lru_cache for simple caching
@lru_cache(maxsize=128)
def expensive_user_calculation(user_id):
    """Simulate expensive calculation that should be cached"""
    time.sleep(1)  # Simulate slow operation
    return f"Processed data for user {user_id}"

# Clear cache when needed
# expensive_user_calculation.cache_clear()
```

**Pagination & Filtering:**
```python
from dataclasses import dataclass
from typing import List, Optional, Dict, Any

@dataclass
class PaginationParams:
    page: int = 1
    per_page: int = 10
    
    @property
    def offset(self):
        return (self.page - 1) * self.per_page

@dataclass
class FilterParams:
    name: Optional[str] = None
    email: Optional[str] = None
    active: Optional[bool] = None
    created_after: Optional[str] = None
    created_before: Optional[str] = None

@dataclass
class PaginatedResponse:
    data: List[Dict[str, Any]]
    total: int
    page: int
    per_page: int
    total_pages: int
    has_next: bool
    has_prev: bool

class UserService:
    def __init__(self, db_manager):
        self.db = db_manager
    
    def get_users_paginated(self, pagination: PaginationParams, filters: FilterParams = None):
        """Get users with pagination and filtering"""
        
        # Build WHERE clause based on filters
        where_conditions = []
        params = []
        
        if filters:
            if filters.name:
                where_conditions.append("name LIKE ?")
                params.append(f"%{filters.name}%")
            
            if filters.email:
                where_conditions.append("email LIKE ?")
                params.append(f"%{filters.email}%")
            
            if filters.active is not None:
                where_conditions.append("active = ?")
                params.append(filters.active)
            
            if filters.created_after:
                where_conditions.append("created_at >= ?")
                params.append(filters.created_after)
            
            if filters.created_before:
                where_conditions.append("created_at <= ?")
                params.append(filters.created_before)
        
        where_clause = " WHERE " + " AND ".join(where_conditions) if where_conditions else ""
        
        # Count total records
        count_query = f"SELECT COUNT(*) FROM users{where_clause}"
        with self.db.get_connection() as conn:
            total = conn.execute(count_query, params).fetchone()[0]
        
        # Get paginated data
        data_query = f"""
            SELECT * FROM users{where_clause} 
            ORDER BY created_at DESC 
            LIMIT ? OFFSET ?
        """
        data_params = params + [pagination.per_page, pagination.offset]
        
        with self.db.get_connection() as conn:
            cursor = conn.execute(data_query, data_params)
            users = [dict(row) for row in cursor.fetchall()]
        
        # Calculate pagination info
        total_pages = (total + pagination.per_page - 1) // pagination.per_page
        
        return PaginatedResponse(
            data=users,
            total=total,
            page=pagination.page,
            per_page=pagination.per_page,
            total_pages=total_pages,
            has_next=pagination.page < total_pages,
            has_prev=pagination.page > 1
        )

# Usage
user_service = UserService(db)

# Get paginated users
pagination = PaginationParams(page=1, per_page=5)
filters = FilterParams(name="John", active=True)
result = user_service.get_users_paginated(pagination, filters)

print(f"Found {result.total} users")
print(f"Page {result.page} of {result.total_pages}")
for user in result.data:
    print(f"- {user['name']} ({user['email']})")
```

**API Response Formatting:**
```python
from enum import Enum
from typing import Union, Dict, List

class ResponseStatus(Enum):
    SUCCESS = "success"
    ERROR = "error"
    WARNING = "warning"

class APIResponse:
    @staticmethod
    def success(data=None, message="Operation successful", meta=None):
        """Format successful API response"""
        response = {
            "status": ResponseStatus.SUCCESS.value,
            "message": message,
            "data": data,
            "timestamp": datetime.now().isoformat()
        }
        
        if meta:
            response["meta"] = meta
        
        return response
    
    @staticmethod
    def error(message="An error occurred", error_code=None, details=None):
        """Format error API response"""
        response = {
            "status": ResponseStatus.ERROR.value,
            "message": message,
            "data": None,
            "timestamp": datetime.now().isoformat()
        }
        
        if error_code:
            response["error_code"] = error_code
        
        if details:
            response["details"] = details
        
        return response
    
    @staticmethod
    def paginated(data, pagination_info):
        """Format paginated API response"""
        return APIResponse.success(
            data=data,
            message=f"Retrieved {len(data)} items",
            meta={
                "pagination": {
                    "current_page": pagination_info.page,
                    "per_page": pagination_info.per_page,
                    "total_items": pagination_info.total,
                    "total_pages": pagination_info.total_pages,
                    "has_next": pagination_info.has_next,
                    "has_previous": pagination_info.has_prev
                }
            }
        )

# Usage examples
def api_get_user(user_id):
    try:
        user = db.get_user(user_id)
        if user:
            return APIResponse.success(data=user, message="User found")
        else:
            return APIResponse.error(message="User not found", error_code="USER_NOT_FOUND")
    except Exception as e:
        return APIResponse.error(message="Internal server error", details=str(e))

def api_create_user(user_data):
    try:
        validate_user_data(user_data)
        user_id = db.create_user(user_data["name"], user_data["email"])
        new_user = db.get_user(user_id)
        return APIResponse.success(data=new_user, message="User created successfully")
    except ValidationError as e:
        return APIResponse.error(message="Validation failed", error_code="VALIDATION_ERROR", details=str(e))
    except Exception as e:
        return APIResponse.error(message="Failed to create user", details=str(e))

def api_get_users_paginated(page=1, per_page=10, **filters):
    try:
        pagination = PaginationParams(page=page, per_page=per_page)
        filter_params = FilterParams(**filters)
        result = user_service.get_users_paginated(pagination, filter_params)
        return APIResponse.paginated(result.data, result)
    except Exception as e:
        return APIResponse.error(message="Failed to retrieve users", details=str(e))
```

**Testing Operation (CRUD):**
```python
import unittest
from unittest.mock import Mock, patch
import tempfile
import os

class TestUserCRUD(unittest.TestCase):
    def setUp(self):
        """Set up test database"""
        self.test_db_fd, self.test_db_path = tempfile.mkstemp()
        self.db = DatabaseManager(self.test_db_path)
    
    def tearDown(self):
        """Clean up test database"""
        os.close(self.test_db_fd)
        os.unlink(self.test_db_path)
    
    def test_create_user(self):
        """Test user creation"""
        user_id = self.db.create_user("John Doe", "john@example.com")
        self.assertIsNotNone(user_id)
        self.assertIsInstance(user_id, int)
    
    def test_get_user(self):
        """Test user retrieval"""
        # Create a user first
        user_id = self.db.create_user("Jane Doe", "jane@example.com")
        
        # Retrieve the user
        user = self.db.get_user(user_id)
        self.assertIsNotNone(user)
        self.assertEqual(user["name"], "Jane Doe")
        self.assertEqual(user["email"], "jane@example.com")
    
    def test_get_nonexistent_user(self):
        """Test retrieving non-existent user"""
        user = self.db.get_user(999)
        self.assertIsNone(user)
    
    def test_update_user(self):
        """Test user update"""
        # Create a user
        user_id = self.db.create_user("Bob Smith", "bob@example.com")
        
        # Update the user
        success = self.db.update_user(user_id, name="Robert Smith", email="robert@example.com")
        self.assertTrue(success)
        
        # Verify the update
        updated_user = self.db.get_user(user_id)
        self.assertEqual(updated_user["name"], "Robert Smith")
        self.assertEqual(updated_user["email"], "robert@example.com")
    
    def test_delete_user(self):
        """Test user deletion"""
        # Create a user
        user_id = self.db.create_user("Alice Johnson", "alice@example.com")
        
        # Delete the user
        success = self.db.delete_user(user_id)
        self.assertTrue(success)
        
        # Verify deletion
        deleted_user = self.db.get_user(user_id)
        self.assertIsNone(deleted_user)
    
    def test_validation_error(self):
        """Test validation error handling"""
        invalid_data = {"name": "", "email": "invalid-email"}
        
        with self.assertRaises(ValidationError):
            validate_user_data(invalid_data)

class TestAPIResponses(unittest.TestCase):
    def test_success_response(self):
        """Test successful API response format"""
        response = APIResponse.success(data={"id": 1, "name": "John"}, message="User found")
        
        self.assertEqual(response["status"], "success")
        self.assertEqual(response["message"], "User found")
        self.assertIsNotNone(response["data"])
        self.assertIn("timestamp", response)
    
    def test_error_response(self):
        """Test error API response format"""
        response = APIResponse.error(message="User not found", error_code="USER_NOT_FOUND")
        
        self.assertEqual(response["status"], "error")
        self.assertEqual(response["message"], "User not found")
        self.assertEqual(response["error_code"], "USER_NOT_FOUND")
        self.assertIsNone(response["data"])

# Mock testing for external dependencies
class TestExternalAPI(unittest.TestCase):
    @patch('requests.get')
    def test_fetch_user_from_api(self, mock_get):
        """Test fetching user from external API"""
        # Mock the API response
        mock_response = Mock()
        mock_response.json.return_value = {"id": 1, "name": "John", "email": "john@example.com"}
        mock_response.raise_for_status.return_value = None
        mock_get.return_value = mock_response
        
        # Test the function
        user = fetch_user_from_api(1)
        
        self.assertIsNotNone(user)
        self.assertEqual(user["name"], "John")
        mock_get.assert_called_once_with("https://api.example.com/users/1")

# Run tests
if __name__ == "__main__":
    unittest.main()
```

**Configuration Management:**
```python
import configparser
from pathlib import Path

class AppConfig:
    def __init__(self, config_file="config.ini"):
        self.config = configparser.ConfigParser()
        self.config_file = config_file
        self.load_config()
    
    def load_config(self):
        """Load configuration from file"""
        if Path(self.config_file).exists():
            self.config.read(self.config_file)
        else:
            self.create_default_config()
    
    def create_default_config(self):
        """Create default configuration file"""
        self.config['DATABASE'] = {
            'url': 'sqlite:///app.db',
            'pool_size': '10',
            'echo': 'false'
        }
        
        self.config['API'] = {
            'host': '0.0.0.0',
            'port': '5000',
            'debug': 'false'
        }
        
        self.config['CACHE'] = {
            'timeout': '300',
            'max_size': '1000'
        }
        
        self.config['LOGGING'] = {
            'level': 'INFO',
            'file': 'app.log',
            'format': '%(asctime)s - %(name)s - %(levelname)s - %(message)s'
        }
        
        self.save_config()
    
    def save_config(self):
        """Save configuration to file"""
        with open(self.config_file, 'w') as configfile:
            self.config.write(configfile)
    
    def get(self, section, key, fallback=None):
        """Get configuration value"""
        return self.config.get(section, key, fallback=fallback)
    
    def getint(self, section, key, fallback=None):
        """Get integer configuration value"""
        return self.config.getint(section, key, fallback=fallback)
    
    def getboolean(self, section, key, fallback=None):
        """Get boolean configuration value"""
        return self.config.getboolean(section, key, fallback=fallback)

# Usage
config = AppConfig()
database_url = config.get('DATABASE', 'url')
api_port = config.getint('API', 'port')
debug_mode = config.getboolean('API', 'debug')
```

**Logging:**
```python
import logging
from logging.handlers import RotatingFileHandler
import sys

def setup_logging(config):
    """Set up application logging"""
    log_level = getattr(logging, config.get('LOGGING', 'level', fallback='INFO'))
    log_file = config.get('LOGGING', 'file', fallback='app.log')
    log_format = config.get('LOGGING', 'format', 
                           fallback='%(asctime)s - %(name)s - %(levelname)s - %(message)s')
    
    # Create formatter
    formatter = logging.Formatter(log_format)
    
    # Create file handler with rotation
    file_handler = RotatingFileHandler(
        log_file, 
        maxBytes=10*1024*1024,  # 10MB
        backupCount=5
    )
    file_handler.setFormatter(formatter)
    file_handler.setLevel(log_level)
    
    # Create console handler
    console_handler = logging.StreamHandler(sys.stdout)
    console_handler.setFormatter(formatter)
    console_handler.setLevel(log_level)
    
    # Configure root logger
    logging.basicConfig(
        level=log_level,
        handlers=[file_handler, console_handler]
    )
    
    return logging.getLogger(__name__)

# CRUD operation logging
class LoggedUserService:
    def __init__(self, db_manager):
        self.db = db_manager
        self.logger = logging.getLogger(self.__class__.__name__)
    
    def create_user(self, name, email):
        """Create user with logging"""
        self.logger.info(f"Creating user: {name} ({email})")
        try:
            user_id = self.db.create_user(name, email)
            self.logger.info(f"User created successfully with ID: {user_id}")
            return user_id
        except Exception as e:
            self.logger.error(f"Failed to create user {name}: {e}")
            raise
    
    def get_user(self, user_id):
        """Get user with logging"""
        self.logger.debug(f"Fetching user with ID: {user_id}")
        try:
            user = self.db.get_user(user_id)
            if user:
                self.logger.debug(f"User found: {user['name']}")
            else:
                self.logger.warning(f"User not found with ID: {user_id}")
            return user
        except Exception as e:
            self.logger.error(f"Error fetching user {user_id}: {e}")
            raise
    
    def update_user(self, user_id, **kwargs):
        """Update user with logging"""
        self.logger.info(f"Updating user {user_id} with data: {kwargs}")
        try:
            success = self.db.update_user(user_id, **kwargs)
            if success:
                self.logger.info(f"User {user_id} updated successfully")
            else:
                self.logger.warning(f"User {user_id} not found for update")
            return success
        except Exception as e:
            self.logger.error(f"Failed to update user {user_id}: {e}")
            raise
    
    def delete_user(self, user_id):
        """Delete user with logging"""
        self.logger.info(f"Deleting user with ID: {user_id}")
        try:
            success = self.db.delete_user(user_id)
            if success:
                self.logger.info(f"User {user_id} deleted successfully")
            else:
                self.logger.warning(f"User {user_id} not found for deletion")
            return success
        except Exception as e:
            self.logger.error(f"Failed to delete user {user_id}: {e}")
            raise
```

**Monitoring:**
```python
import time
from functools import wraps
from collections import defaultdict

class PerformanceMonitor:
    def __init__(self):
        self.metrics = defaultdict(list)
        self.call_counts = defaultdict(int)
    
    def monitor(self, operation_name=None):
        """Decorator to monitor function performance"""
        def decorator(func):
            name = operation_name or f"{func.__module__}.{func.__name__}"
            
            @wraps(func)
            def wrapper(*args, **kwargs):
                start_time = time.time()
                try:
                    result = func(*args, **kwargs)
                    success = True
                except Exception as e:
                    success = False
                    raise
                finally:
                    end_time = time.time()
                    duration = end_time - start_time
                    
                    self.metrics[name].append({
                        'duration': duration,
                        'timestamp': start_time,
                        'success': success
                    })
                    self.call_counts[name] += 1
                
                return result
            return wrapper
        return decorator
    
    def get_stats(self, operation_name):
        """Get performance statistics for an operation"""
        if operation_name not in self.metrics:
            return None
        
        durations = [m['duration'] for m in self.metrics[operation_name]]
        successes = [m['success'] for m in self.metrics[operation_name]]
        
        return {
            'operation': operation_name,
            'total_calls': len(durations),
            'success_rate': sum(successes) / len(successes) * 100,
            'avg_duration': sum(durations) / len(durations),
            'min_duration': min(durations),
            'max_duration': max(durations),
            'total_duration': sum(durations)
        }
    
    def get_all_stats(self):
        """Get statistics for all monitored operations"""
        return {name: self.get_stats(name) for name in self.metrics.keys()}

# Usage
monitor = PerformanceMonitor()

class MonitoredUserService:
    def __init__(self, db_manager):
        self.db = db_manager
    
    @monitor.monitor("user_create")
    def create_user(self, name, email):
        return self.db.create_user(name, email)
    
    @monitor.monitor("user_read")
    def get_user(self, user_id):
        return self.db.get_user(user_id)
    
    @monitor.monitor("user_update")
    def update_user(self, user_id, **kwargs):
        return self.db.update_user(user_id, **kwargs)
    
    @monitor.monitor("user_delete")
    def delete_user(self, user_id):
        return self.db.delete_user(user_id)

# Performance reporting
def generate_performance_report():
    """Generate a performance report"""
    stats = monitor.get_all_stats()
    
    print("=== Performance Report ===")
    for operation, data in stats.items():
        if data:
            print(f"\nOperation: {operation}")
            print(f"  Total Calls: {data['total_calls']}")
            print(f"  Success Rate: {data['success_rate']:.2f}%")
            print(f"  Average Duration: {data['avg_duration']:.4f}s")
            print(f"  Min Duration: {data['min_duration']:.4f}s")
            print(f"  Max Duration: {data['max_duration']:.4f}s")
```

**CRUD Example:**
```python
#!/usr/bin/env python3
"""
Complete CRUD Application Example
This demonstrates all the concepts together in a working application.
"""

import json
import sys
from datetime import datetime

class CRUDApplication:
    def __init__(self):
        self.config = AppConfig()
        self.logger = setup_logging(self.config)
        self.db = DatabaseManager(self.config.get('DATABASE', 'url'))
        self.user_service = LoggedUserService(self.db)
        self.monitor = PerformanceMonitor()
        self.logger.info("CRUD Application initialized")
    
    def run_interactive_mode(self):
        """Run the application in interactive mode"""
        print("=== CRUD Application ===")
        print("Commands: create, read, update, delete, list, search, stats, quit")
        
        while True:
            try:
                command = input("\nEnter command: ").strip().lower()
                
                if command == "quit":
                    print("Goodbye!")
                    break
                elif command == "create":
                    self.handle_create()
                elif command == "read":
                    self.handle_read()
                elif command == "update":
                    self.handle_update()
                elif command == "delete":
                    self.handle_delete()
                elif command == "list":
                    self.handle_list()
                elif command == "search":
                    self.handle_search()
                elif command == "stats":
                    self.handle_stats()
                else:
                    print("Unknown command. Available: create, read, update, delete, list, search, stats, quit")
            
            except KeyboardInterrupt:
                print("\nGoodbye!")
                break
            except Exception as e:
                self.logger.error(f"Error in interactive mode: {e}")
                print(f"Error: {e}")
    
    def handle_create(self):
        """Handle user creation"""
        try:
            name = input("Enter name: ").strip()
            email = input("Enter email: ").strip()
            
            if not name or not email:
                print("Name and email are required")
                return
            
            user_data = {"name": name, "email": email}
            validate_user_data(user_data)
            
            user_id = self.user_service.create_user(name, email)
            print(f"User created successfully with ID: {user_id}")
            
        except ValidationError as e:
            print(f"Validation error: {e}")
        except Exception as e:
            print(f"Error creating user: {e}")
    
    def handle_read(self):
        """Handle user reading"""
        try:
            user_id = int(input("Enter user ID: "))
            user = self.user_service.get_user(user_id)
            
            if user:
                print(f"User found:")
                print(f"  ID: {user['id']}")
                print(f"  Name: {user['name']}")
                print(f"  Email: {user['email']}")
                print(f"  Created: {user['created_at']}")
            else:
                print("User not found")
                
        except ValueError:
            print("Invalid user ID")
        except Exception as e:
            print(f"Error reading user: {e}")
    
    def handle_update(self):
        """Handle user updating"""
        try:
            user_id = int(input("Enter user ID: "))
            
            # Check if user exists
            existing_user = self.user_service.get_user(user_id)
            if not existing_user:
                print("User not found")
                return
            
            print(f"Current user: {existing_user['name']} ({existing_user['email']})")
            
            name = input(f"Enter new name (current: {existing_user['name']}): ").strip()
            email = input(f"Enter new email (current: {existing_user['email']}): ").strip()
            
            update_data = {}
            if name:
                update_data['name'] = name
            if email:
                update_data['email'] = email
            
            if not update_data:
                print("No changes specified")
                return
            
            # Validate update data
            validate_user_data({**existing_user, **update_data})
            
            success = self.user_service.update_user(user_id, **update_data)
            if success:
                print("User updated successfully")
            else:
                print("Failed to update user")
                
        except ValueError:
            print("Invalid user ID")
        except ValidationError as e:
            print(f"Validation error: {e}")
        except Exception as e:
            print(f"Error updating user: {e}")
    
    def handle_delete(self):
        """Handle user deletion"""
        try:
            user_id = int(input("Enter user ID: "))
            
            # Check if user exists
            existing_user = self.user_service.get_user(user_id)
            if not existing_user:
                print("User not found")
                return
            
            print(f"User to delete: {existing_user['name']} ({existing_user['email']})")
            confirm = input("Are you sure? (yes/no): ").strip().lower()
            
            if confirm == "yes":
                success = self.user_service.delete_user(user_id)
                if success:
                    print("User deleted successfully")
                else:
                    print("Failed to delete user")
            else:
                print("Deletion cancelled")
                
        except ValueError:
            print("Invalid user ID")
        except Exception as e:
            print(f"Error deleting user: {e}")
    
    def handle_list(self):
        """Handle listing users"""
        try:
            page = int(input("Enter page number (default 1): ") or "1")
            per_page = int(input("Enter items per page (default 10): ") or "10")
            
            pagination = PaginationParams(page=page, per_page=per_page)
            user_service = UserService(self.db)
            result = user_service.get_users_paginated(pagination)
            
            if result.data:
                print(f"\nUsers (Page {result.page} of {result.total_pages}):")
                print(f"Total users: {result.total}")
                print("-" * 50)
                
                for user in result.data:
                    print(f"ID: {user['id']:<5} Name: {user['name']:<20} Email: {user['email']}")
                
                print("-" * 50)
                if result.has_prev:
                    print("Previous page available")
                if result.has_next:
                    print("Next page available")
            else:
                print("No users found")
                
        except ValueError:
            print("Invalid page number or items per page")
        except Exception as e:
            print(f"Error listing users: {e}")
    
    def handle_search(self):
        """Handle searching users"""
        try:
            search_term = input("Enter search term (name or email): ").strip()
            if not search_term:
                print("Search term is required")
                return
            
            users = self.db.search_users(search_term)
            
            if users:
                print(f"\nFound {len(users)} user(s):")
                print("-" * 50)
                for user in users:
                    print(f"ID: {user['id']:<5} Name: {user['name']:<20} Email: {user['email']}")
                print("-" * 50)
            else:
                print("No users found matching the search term")
                
        except Exception as e:
            print(f"Error searching users: {e}")
    
    def handle_stats(self):
        """Handle showing performance statistics"""
        try:
            stats = self.monitor.get_all_stats()
            
            if stats:
                print("\n=== Performance Statistics ===")
                for operation, data in stats.items():
                    if data and data['total_calls'] > 0:
                        print(f"\nOperation: {operation}")
                        print(f"  Total Calls: {data['total_calls']}")
                        print(f"  Success Rate: {data['success_rate']:.2f}%")
                        print(f"  Average Duration: {data['avg_duration']:.4f}s")
                        print(f"  Min Duration: {data['min_duration']:.4f}s")
                        print(f"  Max Duration: {data['max_duration']:.4f}s")
            else:
                print("No performance statistics available")
                
        except Exception as e:
            print(f"Error showing statistics: {e}")
    
    def run_batch_mode(self, operations_file):
        """Run the application in batch mode from a JSON file"""
        try:
            with open(operations_file, 'r') as file:
                operations = json.load(file)
            
            results = []
            
            for operation in operations:
                try:
                    op_type = operation.get('type')
                    data = operation.get('data', {})
                    
                    if op_type == 'create':
                        user_id = self.user_service.create_user(data['name'], data['email'])
                        results.append({'operation': op_type, 'success': True, 'user_id': user_id})
                    
                    elif op_type == 'read':
                        user = self.user_service.get_user(data['id'])
                        results.append({'operation': op_type, 'success': user is not None, 'user': user})
                    
                    elif op_type == 'update':
                        success = self.user_service.update_user(data['id'], **data['updates'])
                        results.append({'operation': op_type, 'success': success})
                    
                    elif op_type == 'delete':
                        success = self.user_service.delete_user(data['id'])
                        results.append({'operation': op_type, 'success': success})
                    
                    else:
                        results.append({'operation': op_type, 'success': False, 'error': 'Unknown operation'})
                
                except Exception as e:
                    results.append({'operation': op_type, 'success': False, 'error': str(e)})
            
            # Save results
            results_file = f"batch_results_{datetime.now().strftime('%Y%m%d_%H%M%S')}.json"
            with open(results_file, 'w') as file:
                json.dump(results, file, indent=2, default=str)
            
            print(f"Batch operations completed. Results saved to {results_file}")
            
            # Print summary
            successful = sum(1 for r in results if r['success'])
            print(f"Summary: {successful}/{len(results)} operations successful")
            
        except FileNotFoundError:
            print(f"Operations file '{operations_file}' not found")
        except json.JSONDecodeError:
            print(f"Invalid JSON in operations file '{operations_file}'")
        except Exception as e:
            print(f"Error in batch mode: {e}")

def main():
    """Main application entry point"""
    app = CRUDApplication()
    
    if len(sys.argv) > 1:
        # Batch mode
        operations_file = sys.argv[1]
        app.run_batch_mode(operations_file)
    else:
        # Interactive mode
        app.run_interactive_mode()

if __name__ == "__main__":
    main()
```

```markdown
<!-- config.ini -->
[DATABASE]
url = sqlite:///users.db
pool_size = 10
echo = false

[API]
host = 0.0.0.0
port = 5000
debug = false

[CACHE]
timeout = 300
max_size = 1000

[LOGGING]
level = INFO
file = app.log
format = %(asctime)s - %(name)s - %(levelname)s - %(message)s
```

```json
// batch_operations.json
[
  {
    "type": "create",
    "data": {
      "name": "John Doe",
      "email": "john@example.com"
    }
  },
  {
    "type": "create",
    "data": {
      "name": "Jane Smith",
      "email": "jane@example.com"
    }
  },
  {
    "type": "read",
    "data": {
      "id": 1
    }
  },
  {
    "type": "update",
    "data": {
      "id": 1,
      "updates": {
        "name": "John Smith"
      }
    }
  },
  {
    "type": "delete",
    "data": {
      "id": 2
    }
  }
]
```

```environment
DATABASE_URL=sqlite:///production.db
SECRET_KEY=your-secret-key-here
DEBUG=False
API_KEY=your-api-key-here
```

```text
# Core dependencies for CRUD applications
requests>=2.28.0
python-dotenv>=0.19.0
aiohttp>=3.8.0
aiofiles>=0.8.0

# Database (choose one or more)
sqlite3  # Built into Python
# psycopg2-binary>=2.9.0  # PostgreSQL
# pymongo>=4.0.0  # MongoDB
# sqlalchemy>=1.4.0  # ORM

# Web frameworks (choose one)
# flask>=2.2.0
# fastapi>=0.85.0
# django>=4.1.0

# Testing
pytest>=7.0.0
pytest-asyncio>=0.20.0

# Development tools
black>=22.0.0  # Code formatting
flake8>=5.0.0  # Linting
mypy>=0.991    # Type checking
```