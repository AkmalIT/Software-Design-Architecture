# Avoid Passing Nulls Booleans

Avoiding the passing of nulls and booleans as parameters in functions or methods is a principle aimed at improving code clarity and robustness. Nulls and booleans can introduce ambiguity and potential errors, making the code harder to understand, maintain, and debug.

# Guidelines for Avoiding Nulls:

1. **Use Optional Parameters**: Instead of passing null, use optional parameters or default values.
2. **Use Null Objects**: Create special null objects that provide default behaviors.
3. **Use Exceptions**: Throw exceptions instead of returning null to indicate an error condition
4. **Validate Inputs**: Always validate inputs to ensure null values are not passed into the function.

# Guidelines for Avoiding Booleans:

1. **Use Enum Types**: Instead of passing a boolean, use an enum to represent different states or options.
2. **Split Methods**: Create separate methods for different behaviors instead of using a boolean flag to switch between them.
3. **Descriptive Methods**: Use descriptive method names that clearly state their purpose without needing a boolean flag.
4. **Avoid Overloading with Booleans**: Avoid method overloading where boolean flags are used to differentiate behavior.

# Benefits of Avoiding Nulls and Booleans:

1. **Improved Readability**: Code is easier to read and understand without ambiguous nulls and booleans.
2. **Reduced Errors**: Eliminating nulls and booleans reduces the chance of null pointer exceptions and logical errors.
3. **Enhanced Maintainability**: Code is easier to maintain and modify, as the intent is clearer.
4. **Better Design**: Encourages better design practices, such as using more descriptive parameters and separating concerns.

# Example 1: Avoiding Nulls

Using a null object:

```javascript
class NullUser {
  getName() {
    return "Guest";
  }
}

function greetUser(user) {
  if (user === null) {
    user = new NullUser();
  }
  console.log(`Hello, ${user.getName()}!`);
}

const user = null;
greetUser(user); // "Hello, Guest!"
```

Using optional parameters:

```javascript
function greetUser(user = "Guest") {
  console.log(`Hello, ${user}!`);
}

greetUser(); // "Hello, Guest!"
greetUser("Alice"); // "Hello, Alice!"
```

# Example 2: Avoiding Booleans

Using enum types:

```javascript
const UserRole = {
  ADMIN: "admin",
  USER: "user",
};

function getPermissions(role) {
  switch (role) {
    case UserRole.ADMIN:
      return "Full access";
    case UserRole.USER:
      return "Limited access";
    default:
      return "No access";
  }
}

console.log(getPermissions(UserRole.ADMIN)); // "Full access"
console.log(getPermissions(UserRole.USER)); // "Limited access"
```

Splitting methods:

```javascript
function sendEmailToAdmin() {
  // logic to send email to admin
  console.log("Email sent to admin");
}

function sendEmailToUser() {
  // logic to send email to user
  console.log("Email sent to user");
}

// Instead of
function sendEmail(isAdmin) {
  if (isAdmin) {
    sendEmailToAdmin();
  } else {
    sendEmailToUser();
  }
}

sendEmailToAdmin(); // "Email sent to admin"
sendEmailToUser(); // "Email sent to user"
```

Using descriptive methods:

```javascript
function createUser() {
  // logic to create a new user
  console.log("User created");
}

function updateUser() {
  // logic to update an existing user
  console.log("User updated");
}

// Instead of
function saveUser(isNew) {
  if (isNew) {
    createUser();
  } else {
    updateUser();
  }
}

createUser(); // "User created"
updateUser(); // "User updated"
```
