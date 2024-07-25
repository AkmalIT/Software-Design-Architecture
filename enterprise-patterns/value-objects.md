# Value Objects

**Value Objects** are a fundamental concept in Domain-Driven Design (DDD). They represent descriptive aspects of the domain with no conceptual identity. Unlike entities, which have a distinct identity and life cycle, value objects are immutable and are compared based on their attributes.

# Key Characteristics of Value Objects

1. **Immutability**:

- Value objects are immutable; once created, their state cannot be changed. Any modification results in a new instance.

2. **Equality**:

- Two value objects are considered equal if all their attributes are the same. Equality is based on the values they hold rather than their identity.

3. **Self-Validation**:

- Value objects validate their own state, ensuring that they are always in a valid state.

4. **No Identity**:

- Value objects do not have a distinct identity. They are defined solely by their attributes.

# Benefits of Value Objects

1. **Simplicity**:

- They encapsulate simple concepts and make the model easier to understand and work with.

2. **Immutability**:

- Being immutable, they simplify reasoning about the code and reduce bugs related to state changes.

3. **Reusability**:

- Value objects can be reused across different parts of the application without concern for side effects.

4. **Maintainability**:

- Promote cleaner, more maintainable code by encapsulating value-specific logic and validation.

# Example of Value Objects in TypeScript

Consider an example where we model a Money value object to represent monetary values.

1. **Defining the Money Value Object**:

```typescript
class Money {
  private readonly amount: number;
  private readonly currency: string;

  constructor(amount: number, currency: string) {
    if (amount < 0) {
      throw new Error("Amount cannot be negative");
    }
    if (!currency) {
      throw new Error("Currency cannot be empty");
    }
    this.amount = amount;
    this.currency = currency;
  }

  getAmount(): number {
    return this.amount;
  }

  getCurrency(): string {
    return this.currency;
  }

  equals(other: Money): boolean {
    return this.amount === other.amount && this.currency === other.currency;
  }

  add(other: Money): Money {
    if (this.currency !== other.currency) {
      throw new Error("Currencies must match to add");
    }
    return new Money(this.amount + other.amount, this.currency);
  }
}
```

2. **Usage Example**:

```typescript
const money1 = new Money(100, "USD");
const money2 = new Money(200, "USD");
const money3 = money1.add(money2);

console.log(money3.getAmount()); // Output: 300
console.log(money3.getCurrency()); // Output: USD

console.log(money1.equals(new Money(100, "USD"))); // Output: true
console.log(money1.equals(new Money(100, "EUR"))); // Output: false
```

# Real-Life Analogy

**Coordinate Points**:

Consider a point on a Cartesian plane represented by its x and y coordinates. The point itself has no identity; it is defined solely by its coordinates (x, y). If you change either coordinate, you get a different point. Similarly, value objects are defined by their values and have no inherent identity.

# Summary

Value Objects are essential in modeling complex domains where attributes rather than identity define objects. They provide immutability, equality based on attributes, and self-validation, making the code more understandable, maintainable, and free from side effects related to state changes. By encapsulating specific value logic, they promote clean and robust domain models.
