# Event Sourcing

**Event Sourcing** is a design pattern in which changes to the application's state are captured as a sequence of immutable events. Instead of storing the current state of an entity, the system stores a series of events that represent the changes made to the entity. The current state can be derived by replaying these events in order.

# Key Concepts of Event Sourcing

1. **Events**:

- Events are immutable records of something that has happened in the system. Each event captures a state change.

2. **Event Store**:

- The event store is a storage mechanism for events. It serves as the source of truth for the system's state.

3. **Event Handlers**:

- Event handlers process events to update the state of the application or to trigger other actions.

4. **Rebuilding State**:

- The current state of an entity is rebuilt by replaying the events associated with that entity.

# Benefits of Event Sourcing

1. **Auditability**:

- Every change to the state is recorded as an event, providing a complete audit trail.

2. **Debugging**:

- The sequence of events can be replayed to understand how the system reached its current state, aiding in debugging.

3. **Temporal Queries**:

- It's possible to reconstruct the state of the system at any point in time.

4. **Scalability**:

- Event sourcing can scale well because it separates the concerns of event generation and state reconstruction.

# Challenges of Event Sourcing

1. **Complexity**:

- Implementing event sourcing can add complexity to the system, especially in terms of handling event versions and schema changes.

2. **Storage**:

- Storing events can require more storage compared to storing only the current state.

3. **Eventual Consistency**:

- Systems using event sourcing often rely on eventual consistency, which can complicate the development of real-time applications.

# Example of Event Sourcing

Consider a simplified banking application in TypeScript where account transactions are stored as events.

1. **Event Definition**:

```typescript
interface Event {
  type: string;
  data: any;
  timestamp: Date;
}

class DepositEvent implements Event {
  type = "Deposit";
  data: { amount: number };
  timestamp = new Date();

  constructor(amount: number) {
    this.data = { amount };
  }
}

class WithdrawEvent implements Event {
  type = "Withdraw";
  data: { amount: number };
  timestamp = new Date();

  constructor(amount: number) {
    this.data = { amount };
  }
}
```

2. **Event Store**:

```typescript
class EventStore {
  private events: Event[] = [];

  append(event: Event): void {
    this.events.push(event);
  }

  getEvents(): Event[] {
    return this.events;
  }
}
```

3. **Event Handlers and State Reconstruction**:

```typescript
class Account {
  private balance: number = 0;

  constructor(private eventStore: EventStore) {}

  deposit(amount: number): void {
    const event = new DepositEvent(amount);
    this.eventStore.append(event);
    this.apply(event);
  }

  withdraw(amount: number): void {
    const event = new WithdrawEvent(amount);
    this.eventStore.append(event);
    this.apply(event);
  }

  getBalance(): number {
    return this.balance;
  }

  private apply(event: Event): void {
    if (event.type === "Deposit") {
      this.balance += event.data.amount;
    } else if (event.type === "Withdraw") {
      this.balance -= event.data.amount;
    }
  }

  rebuildState(): void {
    this.balance = 0;
    const events = this.eventStore.getEvents();
    for (const event of events) {
      this.apply(event);
    }
  }
}
```

4. **Usage**:

```typescript
const eventStore = new EventStore();
const account = new Account(eventStore);

account.deposit(100);
account.withdraw(30);

console.log(account.getBalance()); // Output: 70

// Rebuild state from events
const newAccount = new Account(eventStore);
newAccount.rebuildState();
console.log(newAccount.getBalance()); // Output: 70
```

# Real-Life Analogy

**Financial Transactions**:

Think of a bank account. Instead of just storing the current balance, the bank records each transaction (deposit, withdrawal) as an event. To determine the current balance, the bank processes all the transactions from the beginning. This provides a complete history of all changes made to the account.

# Summary

Event Sourcing is a powerful pattern for capturing the complete history of changes in a system through immutable events. It provides benefits in terms of auditability, debugging, and the ability to reconstruct past states. However, it introduces complexity and requires careful handling of storage and consistency. Event sourcing is particularly useful in domains where a complete history of changes is crucial, such as financial systems, auditing, and distributed systems.
