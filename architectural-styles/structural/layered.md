# Layered

**Layered Architecture** is a design pattern that organizes an application into a set of layers, each with a specific responsibility. This separation of concerns allows for better modularity, maintainability, and scalability of the application. Each layer in a layered architecture performs a specific role and communicates with the layers directly above or below it.

# Key Characteristics of Layered Architecture

1. **Separation of Concerns**: Different layers handle different aspects of the application, such as presentation, business logic, and data access.

2. **Modularity**: Each layer is self-contained, making the system easier to understand, develop, and maintain.

3. **Inter-Layer Communication**: Layers interact with each other through well-defined interfaces, promoting loose coupling.

4. **Reusability**: Layers can be reused across different parts of the application or in different projects.

5. **Maintainability**: Changes in one layer typically do not affect other layers, making the system easier to maintain and evolve.

# Common Layers in a Layered Architecture

1. **Presentation Layer**: This layer handles the user interface and user interaction. It displays data to the user and sends user commands to the business logic layer.

2. **Business Logic Layer**: This layer contains the core functionality and business rules of the application. It processes user commands, makes decisions, and performs calculations.

3. **Data Access Layer**: This layer manages the data storage and retrieval. It interacts with databases or other data sources to fetch and persist data.

4. **Database Layer**: This layer contains the database management system and the actual data storage.

# Benefits of Layered Architecture

1. **Maintainability**: Changes to one layer usually do not affect other layers, making the application easier to maintain.

2. **Testability**: Each layer can be tested independently, improving the reliability of the system.

3. **Scalability**: Layers can be scaled independently based on the load and performance requirements.

4. **Reusability**: Layers can be reused across different applications or parts of the application.

# Example in TypeScript

To illustrate Layered Architecture in TypeScript, let's consider a simple web application using Express.js. We'll separate the application into presentation, business logic, and data access layers.

**Presentation Layer**

```typescript
// presentationLayer.ts
import express from "express";
import bodyParser from "body-parser";
import { getUserController, createUserController } from "./businessLayer";

const app = express();
app.use(bodyParser.json());

app.get("/users", getUserController);
app.post("/users", createUserController);

app.listen(3000, () => {
  console.log("Server is running on port 3000");
});
```

**Business Logic Layer**

```typescript
// businessLayer.ts
import { Request, Response } from "express";
import { getAllUsers, addUser } from "./dataAccessLayer";

export const getUserController = (req: Request, res: Response) => {
  const users = getAllUsers();
  res.json(users);
};

export const createUserController = (req: Request, res: Response) => {
  const newUser = req.body;
  const createdUser = addUser(newUser);
  res.status(201).json(createdUser);
};
```

**Data Access Layer**

```typescript
// dataAccessLayer.ts
type User = {
  id: number;
  name: string;
};

let users: User[] = [{ id: 1, name: "John Doe" }];

export const getAllUsers = (): User[] => {
  return users;
};

export const addUser = (user: { name: string }): User => {
  const newUser = { id: users.length + 1, name: user.name };
  users.push(newUser);
  return newUser;
};
```

In this example, the application is divided into three layers:

1. **Presentation Layer**: Handles HTTP requests and responses using Express.js.
2. **Business Logic Layer**: Contains the application’s core logic and coordinates between the presentation and data access layers.
3. **Data Access Layer**: Manages data retrieval and storage.

# Real-Life Analogy

**Restaurant**: Think of a restaurant as a layered system. The waitstaff (presentation layer) interact with customers, taking orders and serving food. The kitchen staff (business logic layer) prepare the food based on the orders. The suppliers (data access layer) provide the raw ingredients. Each group performs its role independently but interacts with the other groups through well-defined processes.

# Summary

Layered Architecture is a widely used design pattern that promotes modularity, maintainability, and scalability by separating an application into distinct layers with specific responsibilities. Each layer interacts with adjacent layers through well-defined interfaces, enabling developers to manage complexity, improve reusability, and facilitate independent development and testing. This architecture is particularly useful for large and complex systems where different aspects of the application can be developed and maintained separately.
