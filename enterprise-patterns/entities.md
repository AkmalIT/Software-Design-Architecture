# Entities

**Entities** are a fundamental concept in Domain-Driven Design (DDD). They represent objects within the domain that have a distinct identity that runs through time and different states. Unlike value objects, which are defined solely by their attributes, entities are defined by their unique identity, which persists even as their attributes change.

# Key Characteristics of Entities

1. **Identity**:

- Each entity has a unique identifier that distinguishes it from other entities. This identifier remains constant throughout the lifecycle of the entity.

2. **State and Behavior**:

- Entities have state (attributes) and behavior (methods) that define their characteristics and how they interact with other entities.

3. **Lifecycle**:

- Entities have a lifecycle that includes creation, modification, and deletion. Their state can change over time, but their identity remains the same.

4. **Equality by Identity**:

- Two entities are considered equal if they share the same identifier, regardless of their current state.

# Benefits of Entities

1. **Clear Identification**:

- Entities provide a clear way to identify and track objects within the domain, ensuring consistency and integrity.

2. **Complex Behavior**:

- Entities encapsulate complex behaviors and rules, making it easier to manage and reason about the domain logic.

3. **Consistency**:

- By maintaining a unique identity, entities help ensure data consistency and prevent duplication.

# Example of Entities in TypeScript

Consider an example where we model a simple library system with Book and LibraryMember entities.

1. **Defining the Entities**:

```typescript
class Book {
  constructor(
    public id: string,
    public title: string,
    public author: string,
    public publishedYear: number
  ) {}

  changeTitle(newTitle: string): void {
    this.title = newTitle;
  }
}

class LibraryMember {
  constructor(public id: string, public name: string, public email: string) {}

  changeEmail(newEmail: string): void {
    this.email = newEmail;
  }
}
```

2. **Example Usage**:

```typescript
const book1 = new Book("1", "1984", "George Orwell", 1949);
const book2 = new Book("2", "Brave New World", "Aldous Huxley", 1932);

const member1 = new LibraryMember("1", "Alice", "alice@example.com");
const member2 = new LibraryMember("2", "Bob", "bob@example.com");

console.log(book1.title); // Output: 1984
book1.changeTitle("Animal Farm");
console.log(book1.title); // Output: Animal Farm

console.log(member1.email); // Output: alice@example.com
member1.changeEmail("alice@newdomain.com");
console.log(member1.email); // Output: alice@newdomain.com
```

# Real-Life Analogy

**Employee in a Company**:

Consider an employee in a company. The employee has a unique identifier (e.g., employee ID) that remains the same throughout their employment. Their attributes (e.g., name, position, department) and state (e.g., active, on leave) may change over time, but their identity within the company is constant.

# Summary

Entities are vital in modeling real-world scenarios where objects have a distinct identity and lifecycle. They encapsulate both state and behavior, making it easier to manage domain logic and ensure data consistency. By maintaining a unique identifier, entities provide a clear way to track and interact with objects within the domain.
