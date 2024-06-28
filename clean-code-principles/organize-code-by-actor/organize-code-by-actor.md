# Organize Code by Actor

"Organize Code by Actor" is a principle that suggests structuring code based on the primary entities (or "actors") that perform actions within a system. An "actor" can be a user, a system component, or any entity that interacts with the system. This approach focuses on grouping related functionalities and responsibilities around these actors, leading to a more modular and comprehensible codebase.

# Guidelines for Organizing Code by Actor:

1. **Identify Key Actors**: Determine the main entities that interact with the system.
2. **Group Related Functionality**: Organize code into modules or packages where each module contains all the functionalities related to a specific actor.
3. **Encapsulate Actor Responsibilities**: Ensure that each module encapsulates all the actions and responsibilities of its actor.
4. **Maintain Clear Boundaries**: Keep the boundaries between different actors clear to avoid tight coupling.
5. **Consistent Naming**: Use consistent and meaningful names for modules and functions to reflect their association with specific actors.
6. **DRY Principle**: Follow the DRY (Don't Repeat Yourself) principle to avoid code duplication across different actor modules.
7. **Facilitate Collaboration**: Organize code in a way that makes it easy for team members to collaborate, focusing on specific actors without affecting other parts of the system.

# Benefits of Organizing Code by Actor:

1. **Modularity**: Enhances modularity by encapsulating related functionalities within actor-specific modules.
2. **Readability**: Improves code readability by providing a clear structure that aligns with the system's real-world interactions.
3. **Maintainability**: Simplifies maintenance as changes related to a specific actor are confined to a single module.
4. **Scalability**: Makes it easier to scale the system by adding new actors or extending existing ones.
5. **Testing**: Facilitates more straightforward unit and integration testing by isolating functionalities within actor-specific modules.

# Example 1: Organizing by User Actor

Suppose we are building an e-commerce platform. Key actors might include customers and administrators.

```javascript
// src/users/customer.js
class Customer {
  viewProducts() {
    // logic for viewing products
  }

  placeOrder(orderDetails) {
    // logic for placing an order
  }

  viewOrderHistory() {
    // logic for viewing order history
  }
}

module.exports = Customer;

// src/users/admin.js
class Admin {
  addProduct(productDetails) {
    // logic for adding a product
  }

  removeProduct(productId) {
    // logic for removing a product
  }

  viewAllOrders() {
    // logic for viewing all orders
  }
}

module.exports = Admin;
```

# Example 2: Organizing by System Actor

In a microservices architecture, each service can be considered an actor. For example, in a social media platform, you might have services for user management, post management, and notification management.

```javascript
// src/services/userService.js
class UserService {
  createUser(userData) {
    // logic to create a new user
  }

  getUser(userId) {
    // logic to get user details
  }

  updateUser(userId, userData) {
    // logic to update user details
  }
}

module.exports = UserService;

// src/services/postService.js
class PostService {
  createPost(postData) {
    // logic to create a new post
  }

  getPost(postId) {
    // logic to get post details
  }

  deletePost(postId) {
    // logic to delete a post
  }
}

module.exports = PostService;

// src/services/notificationService.js
class NotificationService {
  sendNotification(notificationData) {
    // logic to send a notification
  }

  getNotifications(userId) {
    // logic to get notifications for a user
  }
}

module.exports = NotificationService;
```

Example 3: Organizing by API Actor
In a RESTful API, endpoints can be grouped by the primary resources (actors) they deal with.

```javascript
// src/routes/userRoutes.js
const express = require("express");
const UserService = require("../services/userService");
const router = express.Router();
const userService = new UserService();

router.post("/users", (req, res) => {
  const userData = req.body;
  userService.createUser(userData);
  res.status(201).send("User created");
});

router.get("/users/:id", (req, res) => {
  const userId = req.params.id;
  const user = userService.getUser(userId);
  res.status(200).json(user);
});

module.exports = router;

// src/routes/postRoutes.js
const express = require("express");
const PostService = require("../services/postService");
const router = express.Router();
const postService = new PostService();

router.post("/posts", (req, res) => {
  const postData = req.body;
  postService.createPost(postData);
  res.status(201).send("Post created");
});

router.get("/posts/:id", (req, res) => {
  const postId = req.params.id;
  const post = postService.getPost(postId);
  res.status(200).json(post);
});

module.exports = router;
```
