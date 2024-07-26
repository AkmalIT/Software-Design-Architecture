# ORMs

**Object-Relational Mappers (ORMs)** are tools that help bridge the gap between object-oriented programming languages and relational databases. They provide a way to map objects in your code to rows in a database, allowing developers to interact with the database using higher-level abstractions rather than raw SQL queries.

# Key Characteristics of ORMs

1. **Object-Relational Mapping**:

- Maps classes in the programming language to tables in the database, and instances of those classes to rows in the tables.

2. **CRUD Operations**:

- Simplifies the implementation of Create, Read, Update, and Delete (CRUD) operations through high-level API methods.

3. **Abstraction**:

- Abstracts the database interactions, allowing developers to work with objects instead of dealing with SQL directly.

4. **Automatic SQL Generation**:

- Automatically generates SQL queries based on the operations performed on the objects.

5. **Relationships**:

- Manages relationships between different entities, such as one-to-many, many-to-one, and many-to-many relationships.

# Benefits of ORMs

1. **Productivity**:

- Increases developer productivity by reducing the amount of boilerplate code and SQL queries needed.

2. **Maintainability**:

- Makes the codebase more maintainable by keeping database-related code within the ORM layer.

3. **Database Abstraction**:

- Allows for easier switching between different database systems by abstracting database-specific details.

4. **Type Safety**:

- Provides type safety and better integration with the programming language’s features, such as autocompletion and refactoring tools.

# Example of ORM in TypeScript (Using TypeORM)

1. **Setting Up the Entity**:

```typescript
import {
  Entity,
  PrimaryGeneratedColumn,
  Column,
  ManyToOne,
  OneToMany,
} from "typeorm";

@Entity()
class User {
  @PrimaryGeneratedColumn()
  id: number;

  @Column()
  name: string;

  @Column()
  email: string;

  @OneToMany(() => Post, (post) => post.user)
  posts: Post[];
}

@Entity()
class Post {
  @PrimaryGeneratedColumn()
  id: number;

  @Column()
  title: string;

  @Column()
  content: string;

  @ManyToOne(() => User, (user) => user.posts)
  user: User;
}
```

2.  **Using the Repository Pattern**:

```typescript
import { getRepository } from "typeorm";

async function createUser() {
  const userRepository = getRepository(User);
  const user = new User();
  user.name = "John Doe";
  user.email = "john@example.com";
  await userRepository.save(user);
  console.log("User has been saved");
}

async function findUser(userId: number) {
  const userRepository = getRepository(User);
  const user = await userRepository.findOne(userId, { relations: ["posts"] });
  console.log(user);
}

async function createPost(userId: number) {
  const postRepository = getRepository(Post);
  const userRepository = getRepository(User);
  const user = await userRepository.findOne(userId);
  if (user) {
    const post = new Post();
    post.title = "My First Post";
    post.content = "This is the content of the post";
    post.user = user;
    await postRepository.save(post);
    console.log("Post has been saved");
  }
}
```

3. **Example Usage**:

```typescript
createUser().then(() => {
  findUser(1).then((user) => {
    console.log("User found:", user);
  });
});

createPost(1).then(() => {
  findUser(1).then((user) => {
    console.log("User with post:", user);
  });
});
```

# Real-Life Analogy
**Online Shopping System**:

Think of an online shopping system where users can place orders for products. An ORM would allow you to model the User, Order, and Product entities and handle their interactions and relationships without having to write complex SQL queries for every operation. Instead, you interact with these entities directly through your programming language, simplifying development and maintenance.
# Summary
ORMs provide a powerful and convenient way to manage database interactions within an object-oriented programming environment. By abstracting the underlying SQL and providing high-level methods for CRUD operations, ORMs increase productivity, maintainability, and type safety. They enable developers to focus more on the business logic rather than the intricacies of database management, promoting a cleaner and more efficient codebase.