# Command Query Separation

Command Query Separation (CQS) is a design principle that divides methods into two distinct categories: commands and queries. Commands perform an action and may change the state of the system, but do not return a value. Queries retrieve data and return a result but do not modify the system's state. This separation helps improve the clarity and maintainability of the code.

# Guidelines for Command Query Separation:

1. **Commands**:

- **Perform an action or change the state.**
- **Do not return any data.**
- **Examples include methods like saveUser(), updateOrder(), or deletePost().**

2. **Queries**:

- **Retrieve and return data.**
- **Do not cause any side effects or change the state.**
- **Examples include methods like getUserById(), fetchOrders(), or listPosts().**

3. **Naming Conventions**:

- **Use verbs for command methods to indicate actions (e.g., create, update, delete).**
- **Use nouns or noun phrases for query methods to indicate data retrieval (e.g., getUser, listOrders).**

4. **Clear Separation**:

- **Ensure commands and queries are clearly separated in your codebase to avoid mixing responsibilities.**
- **Avoid methods that do both querying and modifying the state.**

# Benefits of Command Query Separation:

1. **Clarity**: Code is easier to read and understand when commands and queries are clearly separated.
2. **Maintainability**: Separation helps in maintaining the codebase by clearly defining what each method is responsible for.
3. **Testing**: Testing becomes more straightforward as it is easier to test queries and commands independently.
4. **Decoupling**: Reduces coupling between different parts of the system, making the code more modular.

# Example 1: Command and Query Methods

Using a UserService class to demonstrate CQS:

```javascript
class UserService {
  constructor(userRepository) {
    this.userRepository = userRepository;
  }

  // Command: creates a new user
  createUser(userData) {
    // logic to create a user
    this.userRepository.save(userData);
  }

  // Command: updates an existing user
  updateUser(userId, userData) {
    // logic to update a user
    const user = this.userRepository.findById(userId);
    if (user) {
      user.update(userData);
      this.userRepository.save(user);
    }
  }

  // Query: retrieves a user by ID
  getUserById(userId) {
    // logic to get a user by ID
    return this.userRepository.findById(userId);
  }

  // Query: lists all users
  listUsers() {
    // logic to list all users
    return this.userRepository.findAll();
  }
}
```

# Example 2: Benefits of CQS in Practice

Consider an e-commerce system with a ProductService class:

```javascript
class ProductService {
  constructor(productRepository) {
    this.productRepository = productRepository;
  }

  // Command: adds a new product
  addProduct(productData) {
    this.productRepository.save(productData);
  }

  // Command: updates an existing product
  updateProduct(productId, productData) {
    const product = this.productRepository.findById(productId);
    if (product) {
      product.update(productData);
      this.productRepository.save(product);
    }
  }

  // Query: retrieves a product by ID
  getProductById(productId) {
    return this.productRepository.findById(productId);
  }

  // Query: lists all products
  listProducts() {
    return this.productRepository.findAll();
  }
}
```

# Example 3: Violation of CQS

A method that violates CQS by combining command and query:

```javascript
class OrderService {
  constructor(orderRepository) {
    this.orderRepository = orderRepository;
  }

  // Violates CQS: modifies state and returns data
  placeOrderAndReturnDetails(orderData) {
    const order = this.orderRepository.save(orderData);
    return order;
  }
}
```

Refactoring to adhere to CQS:

```javascript
class OrderService {
  constructor(orderRepository) {
    this.orderRepository = orderRepository;
  }

  // Command: places a new order
  placeOrder(orderData) {
    this.orderRepository.save(orderData);
  }

  // Query: retrieves order details by ID
  getOrderDetails(orderId) {
    return this.orderRepository.findById(orderId);
  }
}
```
