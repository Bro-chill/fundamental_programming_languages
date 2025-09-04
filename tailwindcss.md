# TailwindCSS Fundamentals

## Container

```html
<!-- Main container for your app -->
<div class="container mx-auto max-w-7xl px-4 sm:px-6 lg:px-8">
  <!-- Responsive container with proper max-width and padding -->
  <div class="min-h-screen bg-gray-50">
    <!-- Full height layout with background -->
  </div>
</div>

<!-- Grid layouts for data display -->
<div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
  <!-- Responsive grid for cards/items -->
</div>
```

## Box Model & Spacing

```html
<!-- Consistent spacing system -->
<div class="p-4 m-4">         <!-- 1rem padding/margin -->
<div class="p-6 m-6">         <!-- 1.5rem padding/margin -->
<div class="px-4 py-2">       <!-- Horizontal 1rem, vertical 0.5rem -->
<div class="space-y-4">       <!-- Vertical spacing between children -->
<div class="space-x-4">       <!-- Horizontal spacing between children -->

<!-- Box sizing for forms -->
<input class="box-border w-full p-3 border">
```

## Display & Positioning

```html
<!-- Common display patterns -->
<div class="block">           <!-- Block element -->
<div class="inline-block">    <!-- Inline-block for buttons -->
<div class="hidden">          <!-- Hide element -->
<div class="sr-only">         <!-- Screen reader only -->

<!-- Positioning for modals/dropdowns -->
<div class="relative">        <!-- Relative positioning -->
<div class="absolute top-0 right-0">  <!-- Absolute positioning -->
<div class="fixed inset-0">   <!-- Fixed overlay -->
<div class="sticky top-0">    <!-- Sticky header -->
```

## Flexbox

```html
<!-- Header with actions -->
<div class="flex justify-between items-center mb-6">
  <h1 class="text-2xl font-bold">Users</h1>
  <button class="bg-blue-500 text-white px-4 py-2 rounded">Add User</button>
</div>

<!-- Form layouts -->
<div class="flex flex-col space-y-4">
  <input class="border rounded p-2">
  <input class="border rounded p-2">
  <div class="flex justify-end space-x-2">
    <button class="bg-gray-500 text-white px-4 py-2 rounded">Cancel</button>
    <button class="bg-blue-500 text-white px-4 py-2 rounded">Save</button>
  </div>
</div>

<!-- Responsive flex -->
<div class="flex flex-col md:flex-row gap-4">
  <!-- Stacks vertically on mobile, horizontally on desktop -->
</div>
```

## Grid

```html
<!-- Dashboard layout -->
<div class="grid grid-cols-12 gap-6">
  <div class="col-span-12 lg:col-span-8">Main content</div>
  <div class="col-span-12 lg:col-span-4">Sidebar</div>
</div>

<!-- Data table alternative -->
<div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4 gap-4">
  <!-- Responsive card grid -->
</div>
```

## Typography

```html
<!-- Page headings -->
<h1 class="text-3xl font-bold text-gray-900 mb-6">Dashboard</h1>
<h2 class="text-xl font-semibold text-gray-800 mb-4">User Management</h2>

<!-- Form labels -->
<label class="block text-sm font-medium text-gray-700 mb-1">Email</label>

<!-- Body text -->
<p class="text-gray-600 text-sm">Last updated 2 hours ago</p>

<!-- Status text -->
<span class="text-green-600 font-medium">Active</span>
<span class="text-red-600 font-medium">Inactive</span>

<!-- Truncated text for tables -->
<div class="truncate max-w-xs">Very long text that gets cut off...</div>
```

## Form

```html
<!-- Input fields -->
<input type="text" 
       class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500 focus:border-transparent"
       placeholder="Enter email">

<!-- Select dropdown -->
<select class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500">
  <option>Choose option</option>
</select>

<!-- Textarea -->
<textarea class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500 resize-none" 
          rows="4"></textarea>

<!-- Checkbox -->
<input type="checkbox" class="h-4 w-4 text-blue-600 focus:ring-blue-500 border-gray-300 rounded">
```

## Buttons

```html
<!-- Primary button -->
<button class="bg-blue-600 hover:bg-blue-700 text-white font-medium py-2 px-4 rounded-md transition duration-200">
  Save
</button>

<!-- Secondary button -->
<button class="bg-gray-200 hover:bg-gray-300 text-gray-800 font-medium py-2 px-4 rounded-md transition duration-200">
  Cancel
</button>

<!-- Danger button -->
<button class="bg-red-600 hover:bg-red-700 text-white font-medium py-2 px-4 rounded-md transition duration-200">
  Delete
</button>

<!-- Icon button -->
<button class="p-2 text-gray-400 hover:text-gray-600 transition duration-200">
  <svg class="h-5 w-5">...</svg>
</button>
```

## Cards

```html
<!-- Data card -->
<div class="bg-white rounded-lg shadow-md p-6 border border-gray-200">
  <div class="flex justify-between items-start mb-4">
    <h3 class="text-lg font-semibold text-gray-900">John Doe</h3>
    <span class="bg-green-100 text-green-800 text-xs font-medium px-2.5 py-0.5 rounded-full">
      Active
    </span>
  </div>
  <p class="text-gray-600 text-sm mb-4">john@example.com</p>
  <div class="flex justify-end space-x-2">
    <button class="text-blue-600 hover:text-blue-800 text-sm font-medium">Edit</button>
    <button class="text-red-600 hover:text-red-800 text-sm font-medium">Delete</button>
  </div>
</div>
```

## Tables

```html
<!-- Responsive table -->
<div class="overflow-x-auto">
  <table class="min-w-full bg-white border border-gray-200">
    <thead class="bg-gray-50">
      <tr>
        <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">
          Name
        </th>
        <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">
          Email
        </th>
        <th class="px-6 py-3 text-right text-xs font-medium text-gray-500 uppercase tracking-wider">
          Actions
        </th>
      </tr>
    </thead>
    <tbody class="divide-y divide-gray-200">
      <tr class="hover:bg-gray-50">
        <td class="px-6 py-4 whitespace-nowrap text-sm font-medium text-gray-900">
          John Doe
        </td>
        <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">
          john@example.com
        </td>
        <td class="px-6 py-4 whitespace-nowrap text-right text-sm font-medium">
          <button class="text-blue-600 hover:text-blue-900 mr-3">Edit</button>
          <button class="text-red-600 hover:text-red-900">Delete</button>
        </td>
      </tr>
    </tbody>
  </table>
</div>
```

## Status

```html
<!-- Status badges -->
<span class="inline-flex items-center px-2.5 py-0.5 rounded-full text-xs font-medium bg-green-100 text-green-800">
  Active
</span>
<span class="inline-flex items-center px-2.5 py-0.5 rounded-full text-xs font-medium bg-red-100 text-red-800">
  Inactive
</span>

<!-- Alert messages -->
<div class="bg-green-50 border border-green-200 text-green-700 px-4 py-3 rounded-md mb-4">
  <p class="text-sm">User created successfully!</p>
</div>

<div class="bg-red-50 border border-red-200 text-red-700 px-4 py-3 rounded-md mb-4">
  <p class="text-sm">Error: Please fill in all required fields.</p>
</div>
```

## Modal Overlay

```html
<!-- Modal overlay -->
<div class="fixed inset-0 bg-gray-600 bg-opacity-50 flex items-center justify-center p-4">
  <!-- Modal content -->
  <div class="bg-white rounded-lg shadow-xl max-w-md w-full p-6">
    <div class="flex justify-between items-center mb-4">
      <h3 class="text-lg font-semibold text-gray-900">Confirm Delete</h3>
      <button class="text-gray-400 hover:text-gray-600">
        <svg class="h-6 w-6">...</svg>
      </button>
    </div>
    <p class="text-gray-600 mb-6">Are you sure you want to delete this user?</p>
    <div class="flex justify-end space-x-3">
      <button class="bg-gray-200 hover:bg-gray-300 text-gray-800 px-4 py-2 rounded-md">
        Cancel
      </button>
      <button class="bg-red-600 hover:bg-red-700 text-white px-4 py-2 rounded-md">
        Delete
      </button>
    </div>
  </div>
</div>
```

## Responsive Design

```html
<!-- Responsive utilities -->
<div class="block md:hidden">Mobile only</div>
<div class="hidden md:block">Desktop only</div>

<!-- Responsive text -->
<h1 class="text-xl md:text-2xl lg:text-3xl">Responsive heading</h1>

<!-- Responsive spacing -->
<div class="p-4 md:p-6 lg:p-8">Responsive padding</div>

<!-- Responsive grid -->
<div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4 gap-4">
  <!-- Responsive columns -->
</div>
```

## Animate Loading

```html
<!-- Loading spinner -->
<div class="flex justify-center items-center py-12">
  <div class="animate-spin rounded-full h-8 w-8 border-b-2 border-blue-600"></div>
</div>
```

## Empty States

```html
<!-- Empty state -->
<div class="text-center py-12">
  <svg class="mx-auto h-12 w-12 text-gray-400">...</svg>
  <h3 class="mt-2 text-sm font-medium text-gray-900">No users found</h3>
  <p class="mt-1 text-sm text-gray-500">Get started by creating a new user.</p>
  <div class="mt-6">
    <button class="bg-blue-600 text-white px-4 py-2 rounded-md">Add User</button>
  </div>
</div>
```

## Common Patterns (CRUD)

```html
<!-- List view with actions -->
<div class="space-y-4">
  <div class="flex justify-between items-center">
    <h2 class="text-xl font-semibold">Users</h2>
    <button class="bg-blue-600 text-white px-4 py-2 rounded-md">Add New</button>
  </div>
  
  <!-- Search/Filter -->
  <div class="flex space-x-4">
    <input type="search" placeholder="Search users..." 
           class="flex-1 px-3 py-2 border border-gray-300 rounded-md">
    <select class="px-3 py-2 border border-gray-300 rounded-md">
      <option>All Status</option>
      <option>Active</option>
      <option>Inactive</option>
    </select>
  </div>
</div>
```