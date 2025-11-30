# HTML Fundamentals

> HTML (HyperText Markup Language) is the standard language for creating web pages. It defines the structure and content of a webpage.

## Basic HTML Document Structure

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
  <link rel="stylesheet" href="styles.css">
</head>
<body>
  <!-- Content goes here -->
  <script src="script.js"></script>
</body>
</html>
```

## Text Elements

```html
<!-- Headings (h1 is largest, h6 is smallest) -->
<h1>Main Title</h1>
<h2>Section Title</h2>
<h3>Subsection Title</h3>

<!-- Text content -->
<p>Paragraph text</p>
<strong>Bold/Important text</strong>
<em>Italic/Emphasized text</em>
<small>Small text</small>
<mark>Highlighted text</mark>

<!-- Line breaks and separators -->
<br>  <!-- Line break -->
<hr>  <!-- Horizontal rule -->
```

## Links and Navigation

```html
<!-- External link -->
<a href="https://example.com" target="_blank">Visit Example</a>

<!-- Internal link -->
<a href="#section1">Go to Section 1</a>

<!-- Email link -->
<a href="mailto:user@example.com">Send Email</a>

<!-- Phone link -->
<a href="tel:+1234567890">Call Us</a>
```

## Media

```html
<!-- Image with responsive attributes -->
<img src="image.jpg" alt="Descriptive text" width="200" height="100" loading="lazy">

<!-- Figure with caption -->
<figure>
  <img src="chart.jpg" alt="Sales chart">
  <figcaption>Monthly sales data</figcaption>
</figure>

<!-- Video -->
<video width="320" height="240" controls>
  <source src="movie.mp4" type="video/mp4">
  <source src="movie.webm" type="video/webm">
  Your browser does not support the video tag.
</video>

<!-- Audio -->
<audio controls>
  <source src="audio.mp3" type="audio/mpeg">
  <source src="audio.ogg" type="audio/ogg">
  Your browser does not support the audio tag.
</audio>
```

## Lists

```html
<!-- Unordered list -->
<ul>
  <li>Item 1</li>
  <li>Item 2</li>
  <li>Item 3</li>
</ul>

<!-- Ordered list -->
<ol>
  <li>First step</li>
  <li>Second step</li>
  <li>Third step</li>
</ol>

<!-- Description list -->
<dl>
  <dt>Term</dt>
  <dd>Definition</dd>
  <dt>Another term</dt>
  <dd>Another definition</dd>
</dl>
```

## Tables

```html
<table>
  <caption>User Data</caption>
  <thead>
    <tr>
      <th>ID</th>
      <th>Name</th>
      <th>Email</th>
      <th>Actions</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>1</td>
      <td>John Doe</td>
      <td>john@example.com</td>
      <td>
        <button>Edit</button>
        <button>Delete</button>
      </td>
    </tr>
  </tbody>
</table>
```

## Forms

```html
<form action="/submit" method="POST" id="userForm">
  <!-- Text inputs -->
  <label for="username">Username:</label>
  <input type="text" id="username" name="username" required>
  
  <label for="email">Email:</label>
  <input type="email" id="email" name="email" required>
  
  <label for="password">Password:</label>
  <input type="password" id="password" name="password" required>
  
  <!-- Number input -->
  <label for="age">Age:</label>
  <input type="number" id="age" name="age" min="1" max="120">
  
  <!-- Date input -->
  <label for="birthdate">Birth Date:</label>
  <input type="date" id="birthdate" name="birthdate">
  
  <!-- Select dropdown -->
  <label for="country">Country:</label>
  <select id="country" name="country">
    <option value="">Select a country</option>
    <option value="us">United States</option>
    <option value="ca">Canada</option>
    <option value="uk">United Kingdom</option>
  </select>
  
  <!-- Radio buttons -->
  <fieldset>
    <legend>Gender:</legend>
    <input type="radio" id="male" name="gender" value="male">
    <label for="male">Male</label>
    
    <input type="radio" id="female" name="gender" value="female">
    <label for="female">Female</label>
  </fieldset>
  
  <!-- Checkboxes -->
  <input type="checkbox" id="newsletter" name="newsletter" value="yes">
  <label for="newsletter">Subscribe to newsletter</label>
  
  <!-- Textarea -->
  <label for="bio">Bio:</label>
  <textarea id="bio" name="bio" rows="4" cols="50"></textarea>
  
  <!-- Hidden input (useful for IDs in CRUD) -->
  <input type="hidden" name="userId" value="123">
  
  <!-- Submit buttons -->
  <input type="submit" value="Create User">
  <button type="button" onclick="updateUser()">Update User</button>
  <button type="reset">Reset Form</button>
</form>
```

## Semantic HTML

```html
<!-- Page structure -->
<header>
  <nav>
    <ul>
      <li><a href="#home">Home</a></li>
      <li><a href="#users">Users</a></li>
      <li><a href="#products">Products</a></li>
    </ul>
  </nav>
</header>

<main>
  <section id="users">
    <h2>User Management</h2>
    <article>
      <!-- User CRUD interface -->
    </article>
  </section>
</main>

<aside>
  <!-- Sidebar content -->
</aside>

<footer>
  <p>&copy; 2024 My CRUD App</p>
</footer>
```

## Container Elements

```html
<!-- Block-level container -->
<div class="user-card">
  <h3>User Information</h3>
  <p>User details here...</p>
</div>

<!-- Inline container -->
<p>This is <span class="highlight">highlighted text</span> in a paragraph.</p>

<!-- Generic containers with semantic meaning -->
<section><!-- Thematic grouping --></section>
<article><!-- Standalone content --></article>
<aside><!-- Sidebar content --></aside>
```

## Attributes

```html
<!-- IDs for JavaScript targeting -->
<div id="user-123" class="user-item">

<!-- Data attributes for storing information -->
<button data-user-id="123" data-action="delete">Delete User</button>

<!-- Classes for CSS styling -->
<div class="form-group error">

<!-- ARIA attributes for accessibility -->
<button aria-label="Delete user John Doe">🗑️</button>
```

## Meta Tags

```html
<head>
  <!-- Character encoding -->
  <meta charset="UTF-8">
  
  <!-- Responsive design -->
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  
  <!-- SEO -->
  <meta name="description" content="User management system">
  <meta name="keywords" content="CRUD, users, management">
  
  <!-- External CSS -->
  <link rel="stylesheet" href="styles.css">
  
  <!-- External JavaScript -->
  <script src="script.js" defer></script>
  
  <!-- Favicon -->
  <link rel="icon" href="favicon.ico" type="image/x-icon">
</head>
```

## Common Interface Pattern (CRUD)

```html
<!-- Typical CRUD interface structure -->
<div class="crud-container">
  <!-- Create Form -->
  <section class="create-section">
    <h2>Add New User</h2>
    <form id="createForm">
      <!-- Form fields here -->
    </form>
  </section>
  
  <!-- Read/Display Section -->
  <section class="display-section">
    <h2>Users List</h2>
    <table id="usersTable">
      <!-- Table content here -->
    </table>
  </section>
  
  <!-- Update Modal (hidden by default) -->
  <div id="updateModal" class="modal" style="display: none;">
    <form id="updateForm">
      <!-- Update form fields -->
    </form>
  </div>
</div>
```