# C++ Fundamentals

## Variables & Data Types

```cpp
#include <iostream>
#include <string>
using namespace std;

// Primitive types
int age = 30;
long population = 7800000000L;
double price = 19.99;
float rate = 3.14f;
bool isActive = true;
char grade = 'A';

// String
string name = "John";

// Constants
const double TAX_RATE = 0.08;
constexpr int MAX_SIZE = 100;

// Auto type inference (C++11)
auto message = "Hello";
auto count = 42;
```

---

## Control Flow

```cpp
// If-else
if (age >= 18) {
    cout << "Adult" << endl;
} else if (age >= 13) {
    cout << "Teenager" << endl;
} else {
    cout << "Child" << endl;
}

// Ternary
string status = (age >= 18) ? "Adult" : "Minor";

// Switch
switch (day) {
    case 1:
        cout << "Monday" << endl;
        break;
    case 2:
        cout << "Tuesday" << endl;
        break;
    default:
        cout << "Other day" << endl;
}
```

---

## Loops

```cpp
// For loop
for (int i = 0; i < 5; i++) {
    cout << i << endl;
}

// Range-based for (C++11)
int numbers[] = {1, 2, 3, 4, 5};
for (int num : numbers) {
    cout << num << endl;
}

// While loop
int count = 0;
while (count < 5) {
    cout << count << endl;
    count++;
}

// Do-while
do {
    cout << "Runs at least once" << endl;
} while (false);
```

---

## Arrays & Vectors

```cpp
#include <vector>
#include <array>

// C-style arrays
int numbers[5] = {1, 2, 3, 4, 5};
numbers[0] = 10;

// std::array (C++11) - fixed size
array<int, 5> arr = {1, 2, 3, 4, 5};
arr.size();

// std::vector - dynamic array
vector<int> vec = {1, 2, 3};
vec.push_back(4);     // Add to end
vec.pop_back();       // Remove from end
vec[0];               // Access
vec.size();           // Size
vec.empty();          // Is empty?

// Iterate vector
for (const auto& item : vec) {
    cout << item << endl;
}
```

---

## Functions

```cpp
// Basic function
string greet(string name) {
    return "Hello, " + name + "!";
}

// Default parameters
string greet(string name = "Guest") {
    return "Hello, " + name + "!";
}

// Pass by reference
void swap(int& a, int& b) {
    int temp = a;
    a = b;
    b = temp;
}

// Pass by const reference (for efficiency)
void printName(const string& name) {
    cout << name << endl;
}

// Function overloading
int add(int a, int b) { return a + b; }
double add(double a, double b) { return a + b; }

// Lambda (C++11)
auto multiply = [](int a, int b) { return a * b; };
```

---

## Classes & OOP

```cpp
class User {
private:
    long id;
    string name;
    string email;

public:
    // Constructor
    User(string name, string email) 
        : name(name), email(email), id(time(nullptr)) {}

    // Getters
    string getName() const { return name; }
    string getEmail() const { return email; }

    // Setters
    void setName(const string& newName) { name = newName; }

    // Method
    string greet() const {
        return "Hello, " + name + "!";
    }

    // Destructor
    ~User() {}
};

// Inheritance
class Admin : public User {
private:
    vector<string> permissions;

public:
    Admin(string name, string email, vector<string> perms)
        : User(name, email), permissions(perms) {}
};

// Usage
User user("John", "john@example.com");
cout << user.greet() << endl;
```

---

## Pointers & References

```cpp
// Pointers
int value = 42;
int* ptr = &value;      // Pointer to value
cout << *ptr << endl;   // Dereference: 42

// Dynamic allocation
int* arr = new int[5];
delete[] arr;           // Free memory

// Smart pointers (C++11) - automatically free memory when done
#include <memory>
// unique_ptr - only one owner, deleted when owner goes out of scope
unique_ptr<User> user1 = make_unique<User>("John", "john@email.com");
// shared_ptr - multiple owners, deleted when last owner is gone
shared_ptr<User> user2 = make_shared<User>("Jane", "jane@email.com");

// References
int& ref = value;       // Reference to value
ref = 100;              // value is now 100
```

---

## Maps & Sets

```cpp
#include <map>
#include <unordered_map>
#include <set>

// Map (ordered)
map<string, int> ages;
ages["John"] = 30;
ages["Jane"] = 25;
ages.find("John");      // Iterator
ages.count("John");     // 0 or 1

// Unordered map (hash map)
unordered_map<string, int> fastMap;
fastMap["key"] = 100;

// Set (unique values)
set<int> uniqueNums = {3, 1, 4, 1, 5};  // {1, 3, 4, 5}
uniqueNums.insert(2);
uniqueNums.count(3);    // 1 if exists

// Iterate
for (const auto& [key, value] : ages) {
    cout << key << ": " << value << endl;
}
```

---

## String Operations

```cpp
#include <string>
#include <sstream>

string str = "Hello World";

// Common operations
str.length();           // Size
str.substr(0, 5);       // "Hello"
str.find("World");      // Position or npos
str.replace(0, 5, "Hi"); // Replace
str.append("!");        // Append
str += "!";             // Concatenate

// Convert to/from numbers
int num = stoi("42");
double d = stod("3.14");
string s = to_string(42);

// String stream
stringstream ss;
ss << "Value: " << 42;
string result = ss.str();
```

---

## File I/O

```cpp
#include <fstream>

// Write to file
ofstream outFile("file.txt");
if (outFile.is_open()) {
    outFile << "Hello World" << endl;
    outFile.close();
}

// Read from file
ifstream inFile("file.txt");
string line;
while (getline(inFile, line)) {
    cout << line << endl;
}
inFile.close();

// Read entire file
ifstream file("file.txt");
string content((istreambuf_iterator<char>(file)),
                istreambuf_iterator<char>());
```

---

## Exception Handling

```cpp
#include <stdexcept>

try {
    if (age < 0) {
        throw invalid_argument("Age cannot be negative");
    }
    // risky operation
} catch (const invalid_argument& e) {
    cerr << "Error: " << e.what() << endl;
} catch (const exception& e) {
    cerr << "Unexpected: " << e.what() << endl;
} catch (...) {
    cerr << "Unknown error" << endl;
}
```

---

## Templates

```cpp
// Function template
template <typename T>
T maximum(T a, T b) {
    return (a > b) ? a : b;
}

// Usage
maximum(10, 20);        // int
maximum(3.14, 2.71);    // double

// Class template
template <typename T>
class Box {
private:
    T content;
public:
    void set(T value) { content = value; }
    T get() const { return content; }
};

// Usage
Box<int> intBox;
intBox.set(42);
```

---

## Basic Standard Library Algorithms

```cpp
#include <algorithm>
#include <vector>

vector<int> nums = {3, 1, 4, 1, 5, 9};

// Sort
sort(nums.begin(), nums.end());

// Find
auto it = find(nums.begin(), nums.end(), 4);
if (it != nums.end()) {
    cout << "Found: " << *it << endl;
}

// Count
int count = count_if(nums.begin(), nums.end(), 
    [](int n) { return n > 3; });

// Transform
transform(nums.begin(), nums.end(), nums.begin(),
    [](int n) { return n * 2; });

// For each
for_each(nums.begin(), nums.end(), 
    [](int n) { cout << n << " "; });
```

---

## Compilation

```bash
# Compile single file
g++ -o program main.cpp

# With C++17 standard
g++ -std=c++17 -o program main.cpp

# With optimizations
g++ -O2 -std=c++17 -o program main.cpp

# Run
./program
```