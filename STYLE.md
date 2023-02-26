Tutoruu - Coding Style Guide
============================

At Tutoruu, we believe that following a consistent coding style is essential for writing clean, maintainable, and easy-to-read code. This guide outlines our coding style standards and best practices for JavaScript, React, Node.js, and other technologies used in our platform.

General Guidelines
------------------

-   Write clear, concise, and readable code that follows the DRY (Don't Repeat Yourself) principle
-   Use meaningful and descriptive variable and function names
-   Comment your code when necessary to explain the purpose of the code and its logic
-   Avoid using magic numbers or hard-coded values. Use constants or configuration files instead
-   Follow the [JavaScript Standard Style](https://standardjs.com/) for code formatting
-   Use best practices for security, performance, and scalability
-   Write tests to ensure that your code is working as expected

JavaScript
----------

### Variables

-   Use `const` for variables that do not change, and `let` for variables that can change
-   Declare each variable on a new line
-   Use descriptive names for variables that explain their purpose
-   Avoid abbreviations or acronyms in variable names

```javascript
// Bad example
const x = 1, y = 2, z = x + y;

// Good example
const num1 = 1;
const num2 = 2;
const sum = num1 + num2;
```

### Functions

-   Use descriptive names for functions that explain their purpose
-   Use camelCase for function names
-   Use arrow functions for short, simple functions
-   Write one function to perform one task

```javascript
// Bad example
function doSomething() {
  //...
}

// Good example
function calculateSum(num1, num2) {
  return num1 + num2;
}

const multiply = (num1, num2) => num1 * num2;```
```

### Control Structures

-   Use curly braces `{}` for all control structures, even if they contain only one statement
-   Use indentation to show the hierarchy of control structures

```javascript

// Bad example
if (x === 1)
  doSomething();

// Good example
if (x === 1) {
  doSomething();
}
```

### Error Handling

-   Use `try...catch` blocks to handle errors
-   Throw meaningful error messages that explain the problem
-   Use `console.error` to log errors to the console

```javascript

`// Bad example
function divide(num1, num2) {
  return num1 / num2;
}

// Good example
function divide(num1, num2) {
  if (num2 === 0) {
    throw new Error("Division by zero");
  }
  return num1 / num2;
}
```

React
-----

### Components

-   Use PascalCase for component names
-   Use functional components instead of class components whenever possible
-   Use `props` to pass data and callbacks to child components
-   Use `state` to manage component-level data
-   Use destructuring to extract data from `props` and `state`

```jsx

// Bad example
class MyComponent extends React.Component {
  render() {
    return <div>{this.props.text}</div>;
  }
}

// Good example
const MyComponent = ({ text }) => {
  return <div>{text}</div>;
};
```

### Hooks

-   Use `useState` to manage component-level state
-   Use `useEffect` to perform side effects, such as fetching data from an API
-   Use custom hooks to reuse logic across multiple components

```jsx
// example
const MyComponent = () => {
  const [text, setText] = useState("");
  useEffect(() => {
    fetch("<https://api.example.com/text>")
      .then((response) => response.text()) 
      .then((data) => setText(data)); 
  }, []);

  return <div>{text}</div>; 
};
```

### JSX

- Use indentation to show the hierarchy of JSX elements
- Use self-closing tags for empty elements
- Use double quotes `"` for attribute values

```jsx
// Bad example
const MyComponent = () => {
  return (
    <div><span className='text'>Hello</span></div>
  );
};

// Good example
const MyComponent = () => {
  return (
    <div>
      <span className="text">Hello</span>
    </div>
  );
};
```
TypeScript
----------

### General

-   Use TypeScript for all new projects and components
-   Use strong and descriptive types
-   Use interfaces to define the structure of complex objects

### Variable Declarations

-   Use `const` for variables that will not be reassigned
-   Use `let` for variables that may be reassigned
-   Avoid using `var`

```typescript

// Bad example
var name = "John";

// Good example
const name = "John";
let age = 30;
```

### Function Declarations

-   Use arrow functions for simple functions
-   Use function declarations for complex functions
-   Use typed parameters and return types

```typescript

// Bad example
function add(a, b) {
  return a + b;
}

// Good example
const add = (a: number, b: number): number => {
  return a + b;
};

function getUser(id: number): User {
  //...
}
```

### Classes

-   Use classes to define object-oriented functionality
-   Use access modifiers to control access to class properties and methods
-   Use typed class properties

```typescript

// Bad example
class User {
  id;
  name;

  constructor(id, name) {
    this.id = id;
    this.name = name;
  }

  getName() {
    return this.name;
  }
}

// Good example
class User {
  private id: number;
  public name: string;

  constructor(id: number, name: string) {
    this.id = id;
    this.name = name;
  }

  public getName(): string {
    return this.name;
  }
}
```

Node.js
-------

### Modules

-   Use CommonJS modules for server-side code
-   Use ES modules for client-side code
-   Use `module.exports` to export a single function or object from a module
-   Use `exports` to export multiple functions or objects from a module

```javascript

// Bad example
export function doSomething() {
  //...
}

// Good example
module.exports = {
  doSomething,
};
```

### Error Handling

-   Use `try...catch` blocks to handle errors
-   Throw meaningful error messages that explain the problem
-   Use `console.error` to log errors to the console

```javascript

// Bad example
function readJsonFile(filename) {
  return JSON.parse(fs.readFileSync(filename));
}

// Good example
function readJsonFile(filename) {
  try {
    return JSON.parse(fs.readFileSync(filename));
  } catch (error) {
    throw new Error(`Could not read JSON file ${filename}: ${error.message}`);
  }
}
```


Laravel
-------

### General

-   Use Laravel for server-side code
-   Use Laravel's conventions and best practices
-   Use the latest version of Laravel

### Routing

-   Use the `Route` facade to define routes
-   Use named routes for easy linking
-   Use route parameters for dynamic routes

```php

// Bad example
Route::get("/users", function () {
  //...
});

// Good example
Route::get("/users", [UserController::class, "index"])->name("users.index");

Route::get("/users/{id}", [UserController::class, "show"])->name("users.show");
```

### Controllers

-   Use controllers to handle route logic
-   Use resource controllers for CRUD operations
-   Use dependency injection to manage dependencies

```php

// Bad example
Route::get("/users", function () {
  $users = DB::table("users")->get();

  return view("users.index", ["users" => $users]);
});

// Good example
class UserController extends Controller {
  public function index(UserRepository $repository) {
    $users = $repository->getAll();

    return view("users.index", ["users" => $users]);
  }

  public function store(UserRequest $request, UserRepository $repository) {
    $user = $repository->create($request->validated());

    return redirect()->route("users.show", $user->id);
  }

  //...
}
```

### Models

-   Use models to represent database tables
-   Use model events to add behavior to models
-   Use relationships to define database relationships

```php

// Bad example
class User extends Model {
  protected $table = "users";
}

// Good example
class User extends Model {
  protected $table = "users";

  public function posts() {
    return $this->hasMany(Post::class);
  }

  public static function boot() {
    parent::boot();

    static::creating(function ($model) {
      $model->slug = Str::slug($model->name);
    });
  }
}
```

Tools and Libraries
-------------------

### ESLint

-   Use ESLint to enforce coding style and best practices
-   Configure ESLint to match the coding style guidelines of Tutoruu
-   Use ESLint plugins to catch common errors and security issues

### Prettier

-   Use Prettier to automatically format code
-   Configure Prettier to match the coding style guidelines of Tutoruu

### Jest

-   Use Jest to write and run tests
-   Write tests for each function or component
-   Use descriptive test names that explain the purpose of the test
-   Use `expect` to test the output of functions and components
-   Use mocking to test API calls and other dependencies

Conclusion
----------

Following these coding style guidelines will help us maintain a consistent and high-quality codebase. Please keep these guidelines in mind when writing code for Tutoruu. If you have any questions or suggestions for improving this guide, please let us know!
