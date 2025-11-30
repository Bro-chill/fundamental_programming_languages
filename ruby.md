# Ruby Fundamentals

> Ruby is designed for programmer happiness with clean, readable syntax. Popular for web development with Ruby on Rails.

## Variables & Data Types

```ruby
# Variables (dynamically typed)
name = "John"           # String
age = 30                # Integer
price = 19.99           # Float
is_active = true        # Boolean
nothing = nil           # Nil (null)

# Constants (start with uppercase)
API_KEY = "abc123"
MAX_USERS = 100

# Symbols (immutable identifiers)
status = :active
role = :admin

# Multiple assignment
a, b, c = 1, 2, 3
x, y = y, x  # Swap values

# String interpolation
greeting = "Hello, #{name}!"

# Type checking
name.class      # String
age.is_a?(Integer)  # true
```

---

## Control Flow

```ruby
# If-else
if age >= 18
  puts "Adult"
elsif age >= 13
  puts "Teenager"
else
  puts "Child"
end

# One-liner
puts "Adult" if age >= 18
puts "Minor" unless age >= 18

# Ternary
status = age >= 18 ? "Adult" : "Minor"

# Case (switch)
case role
when :admin
  puts "Full access"
when :user
  puts "Limited access"
else
  puts "No access"
end

# Case with ranges
grade = case score
when 90..100 then "A"
when 80..89 then "B"
when 70..79 then "C"
else "F"
end
```

---

## Loops

```ruby
# Times loop
5.times { |i| puts i }

# Each loop
[1, 2, 3].each { |n| puts n }

# Each with index
["a", "b", "c"].each_with_index do |item, index|
  puts "#{index}: #{item}"
end

# For loop
for i in 0..4
  puts i
end

# While loop
count = 0
while count < 5
  puts count
  count += 1
end

# Until loop
count = 0
until count >= 5
  puts count
  count += 1
end

# Loop with break/next
loop do
  break if condition
  next if skip_condition
end
```

---

## Methods

```ruby
# Basic method
def greet(name)
  "Hello, #{name}!"
end

# Default parameters
def greet(name = "Guest")
  "Hello, #{name}!"
end

# Keyword arguments
def create_user(name:, email:, age: 18)
  { name: name, email: email, age: age }
end
create_user(name: "John", email: "john@example.com")

# Splat operator (variable args)
def sum(*numbers)
  numbers.reduce(0, :+)
end

# Double splat (keyword args)
def configure(**options)
  options.each { |k, v| puts "#{k}: #{v}" }
end

# Block methods
def with_logging
  puts "Starting..."
  result = yield
  puts "Done!"
  result
end
with_logging { perform_task }

# Lambda and Proc
double = ->(n) { n * 2 }
double.call(5)  # 10

square = Proc.new { |n| n * n }
square.call(4)  # 16
```

---

## Arrays

```ruby
# Create arrays
numbers = [1, 2, 3, 4, 5]
names = %w[john jane bob]  # ["john", "jane", "bob"]

# Access elements
numbers[0]      # 1
numbers[-1]     # 5 (last)
numbers[1..3]   # [2, 3, 4]

# Common methods
numbers.length          # 5
numbers.first           # 1
numbers.last            # 5
numbers.include?(3)     # true
numbers.push(6)         # Add to end
numbers << 7            # Add to end
numbers.pop             # Remove from end
numbers.shift           # Remove from front
numbers.unshift(0)      # Add to front

# Transformations
numbers.map { |n| n * 2 }       # [2, 4, 6, 8, 10]
numbers.select { |n| n > 2 }    # [3, 4, 5]
numbers.reject { |n| n > 2 }    # [1, 2]
numbers.reduce(0) { |sum, n| sum + n }  # 15
numbers.sort                    # Ascending
numbers.sort.reverse            # Descending
numbers.compact                 # Remove nils
numbers.uniq                    # Remove duplicates
numbers.flatten                 # Flatten nested arrays

# Find
numbers.find { |n| n > 3 }      # 4 (first match)
numbers.find_all { |n| n > 3 }  # [4, 5]
```

---

## Hashes

```ruby
# Create hash
user = {
  name: "John",
  email: "john@example.com",
  age: 30
}

# Alternative syntax
user = { "name" => "John", "age" => 30 }

# Access values
user[:name]         # "John"
user[:missing]      # nil
user.fetch(:name)   # "John"
user.fetch(:missing, "default")  # "default"

# Modify
user[:phone] = "123-456"  # Add/update
user.delete(:phone)       # Remove

# Common methods
user.keys           # [:name, :email, :age]
user.values         # ["John", "john@example.com", 30]
user.has_key?(:name)  # true
user.merge(other_hash)  # Combine hashes

# Iterate
user.each do |key, value|
  puts "#{key}: #{value}"
end

# Transform
user.transform_values { |v| v.to_s.upcase }
user.select { |k, v| v.is_a?(String) }
```

---

## Classes & OOP

```ruby
class User
  # Class variable
  @@count = 0
  
  # Attribute accessors
  attr_reader :id
  attr_accessor :name, :email
  
  # Constructor
  def initialize(name, email)
    @id = rand(1000)
    @name = name
    @email = email
    @@count += 1
  end
  
  # Instance method
  def to_s
    "User: #{@name} (#{@email})"
  end
  
  # Class method
  def self.count
    @@count
  end
  
  # Private methods
  private
  
  def secret_method
    "This is private"
  end
end

# Inheritance
class Admin < User
  attr_accessor :permissions
  
  def initialize(name, email, permissions = [])
    super(name, email)
    @permissions = permissions
  end
end

# Modules (mixins)
module Timestamps
  def created_at
    @created_at ||= Time.now
  end
end

class Post
  include Timestamps
end

# Usage
user = User.new("John", "john@example.com")
puts user.name
puts User.count
```

---

## Error Handling

```ruby
# Begin-rescue
begin
  result = risky_operation
rescue StandardError => e
  puts "Error: #{e.message}"
ensure
  puts "Cleanup"
end

# Raise exceptions
def divide(a, b)
  raise ArgumentError, "Cannot divide by zero" if b.zero?
  a / b
end

# Custom exception
class ValidationError < StandardError
  attr_reader :errors
  
  def initialize(errors)
    @errors = errors
    super("Validation failed")
  end
end

# Rescue specific exceptions
begin
  operation
rescue ValidationError => e
  puts e.errors
rescue StandardError => e
  puts e.message
end

# Retry
attempts = 0
begin
  attempts += 1
  risky_operation
rescue => e
  retry if attempts < 3
  raise e
end
```

---

## File Operations

```ruby
# Read file
content = File.read("file.txt")
lines = File.readlines("file.txt", chomp: true)

# Write file
File.write("file.txt", "Hello World")
File.open("file.txt", "a") { |f| f.puts "New line" }

# Read line by line
File.foreach("file.txt") do |line|
  puts line
end

# Check file exists
File.exist?("file.txt")
File.directory?("folder")

# File info
File.size("file.txt")
File.mtime("file.txt")

# Directory operations
Dir.entries(".")        # List files
Dir.mkdir("new_folder")
Dir.glob("*.rb")        # Pattern matching
```

---

## Strings

```ruby
str = "Hello World"

# Common methods
str.length              # 11
str.downcase            # "hello world"
str.upcase              # "HELLO WORLD"
str.capitalize          # "Hello world"
str.reverse             # "dlroW olleH"
str.strip               # Remove whitespace
str.split(" ")          # ["Hello", "World"]
str.include?("World")   # true
str.start_with?("Hello")  # true
str.gsub("World", "Ruby") # "Hello Ruby"
str.chars               # ["H", "e", "l", ...]

# String interpolation
name = "John"
"Hello, #{name}!"

# Multiline strings
text = <<~HEREDOC
  This is a
  multiline string
HEREDOC

# Format strings
"Hello %s, you are %d years old" % [name, age]
```

---

## Blocks, Procs & Lambdas

```ruby
# Block (inline)
[1, 2, 3].each { |n| puts n }

# Block (multi-line)
[1, 2, 3].each do |n|
  puts n
end

# Yield to block
def twice
  yield
  yield
end
twice { puts "Hello" }

# Block with argument
def with_value
  yield(42)
end
with_value { |n| puts n }

# Proc
my_proc = Proc.new { |n| n * 2 }
my_proc.call(5)  # 10
[1, 2, 3].map(&my_proc)  # [2, 4, 6]

# Lambda
my_lambda = ->(n) { n * 2 }
my_lambda.call(5)  # 10

# Difference: Lambda checks args, Proc doesn't
# Lambda returns to caller, Proc returns from enclosing method
```

---

## Common Patterns

```ruby
# Safe navigation (&.)
user&.name  # Returns nil if user is nil

# Double pipe assignment
@name ||= "Default"  # Assign if nil/false

# Chaining
users
  .select { |u| u.active? }
  .map { |u| u.name }
  .sort

# Struct (simple class)
Person = Struct.new(:name, :age) do
  def adult?
    age >= 18
  end
end
person = Person.new("John", 30)

# OpenStruct (dynamic attributes)
require 'ostruct'
user = OpenStruct.new(name: "John", age: 30)
user.email = "john@example.com"

# JSON handling
require 'json'
json_str = { name: "John" }.to_json
data = JSON.parse(json_str)
```

---

## Date & Time

```ruby
require 'time'

# Current time
now = Time.now
today = Date.today

# Create specific date/time
time = Time.new(2024, 1, 15, 14, 30, 0)
date = Date.new(2024, 1, 15)

# Formatting
now.strftime("%Y-%m-%d %H:%M:%S")  # "2024-01-15 14:30:00"
now.strftime("%B %d, %Y")          # "January 15, 2024"

# Parsing
Time.parse("2024-01-15 14:30:00")
Date.parse("2024-01-15")

# Arithmetic
tomorrow = Date.today + 1
next_week = Date.today + 7
one_hour_later = Time.now + 3600

# Comparison
date1 < date2
time1 > time2
```
