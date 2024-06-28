# Keep Framework Code Distant

"Keep Framework Code Distant" is a principle aimed at maintaining a clear separation between the core business logic of an application and the framework-specific code. This ensures that the application's architecture remains flexible, maintainable, and testable.

# Guidelines for Keeping Framework Code Distant:

1. **Abstract Framework Code**: Use abstractions to encapsulate framework-specific details, making the core logic independent of the framework.
2. **Dependency Injection**: Use dependency injection to decouple the business logic from the framework code.
3. **Service Layer**: Introduce a service layer to act as an intermediary between the framework and the business logic.
4. **Interfaces and Adapters**: Define interfaces for core functionalities and implement adapters to handle framework-specific interactions.
5. **Modular Design**: Organize code in a modular fashion, separating business logic modules from framework modules.

# Benefits of Keeping Framework Code Distant:

1. **Flexibility**: Makes it easier to switch frameworks or upgrade to newer versions without significant refactoring.
2. **Testability**: Improves testability by isolating business logic from framework dependencies, allowing for easier mocking and unit testing.
3. **Maintainability**: Simplifies maintenance by reducing the complexity and interdependence between the core logic and framework code.
4. **Reusability**: Enhances reusability of the business logic across different projects or contexts that may use different frameworks.

# Example 1: Abstracting Framework Code

Without abstraction:

```javascript
// Business logic directly tied to a specific framework (e.g., Express.js)
const express = require("express");
const app = express();

app.get("/users", (req, res) => {
  // Business logic directly within the route handler
  const users = getUsersFromDatabase();
  res.json(users);
});

function getUsersFromDatabase() {
  // Simulated database call
  return [
    { id: 1, name: "Alice" },
    { id: 2, name: "Bob" },
  ];
}

app.listen(3000, () => {
  console.log("Server running on port 3000");
});
```

With abstraction:

```javascript
// Business logic separated from framework-specific code
class UserService {
  getUsers() {
    return this.getUsersFromDatabase();
  }

  getUsersFromDatabase() {
    // Simulated database call
    return [
      { id: 1, name: "Alice" },
      { id: 2, name: "Bob" },
    ];
  }
}

// Framework-specific code in a separate module
const express = require("express");
const app = express();
const userService = new UserService();

app.get("/users", (req, res) => {
  const users = userService.getUsers();
  res.json(users);
});

app.listen(3000, () => {
  console.log("Server running on port 3000");
});
```

# Example 2: Using Dependency Injection

Without dependency injection:

```javascript
// Business logic tightly coupled with framework-specific code
class UserController {
  constructor() {
    this.userService = new UserService();
  }

  getUsers(req, res) {
    const users = this.userService.getUsers();
    res.json(users);
  }
}

const express = require("express");
const app = express();
const userController = new UserController();

app.get("/users", (req, res) => userController.getUsers(req, res));

app.listen(3000, () => {
  console.log("Server running on port 3000");
});
```

With dependency injection:

```javascript
// Business logic decoupled from framework-specific code using dependency injection
class UserController {
  constructor(userService) {
    this.userService = userService;
  }

  getUsers(req, res) {
    const users = this.userService.getUsers();
    res.json(users);
  }
}

const express = require("express");
const app = express();
const userService = new UserService();
const userController = new UserController(userService);

app.get("/users", (req, res) => userController.getUsers(req, res));

app.listen(3000, () => {
  console.log("Server running on port 3000");
});
```

# Example 3: Using Interfaces and Adapters

```typescript
// Define an interface for user service
interface IUserService {
  getUsers(): Array<{ id: number; name: string }>;
}

// Implement the interface in the business logic
class UserService implements IUserService {
  getUsers(): Array<{ id: number; name: string }> {
    return this.getUsersFromDatabase();
  }

  private getUsersFromDatabase(): Array<{ id: number; name: string }> {
    return [
      { id: 1, name: "Alice" },
      { id: 2, name: "Bob" },
    ];
  }
}

// Framework-specific adapter
class ExpressUserAdapter {
  constructor(private userService: IUserService) {}

  getUsers(req: any, res: any) {
    const users = this.userService.getUsers();
    res.json(users);
  }
}

const express = require("express");
const app = express();
const userService = new UserService();
const expressUserAdapter = new ExpressUserAdapter(userService);

app.get("/users", (req, res) => expressUserAdapter.getUsers(req, res));

app.listen(3000, () => {
  console.log("Server running on port 3000");
});
```
