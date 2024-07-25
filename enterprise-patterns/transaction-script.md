# Transaction Script

**Transaction Script** is a design pattern that organizes business logic by procedures where each procedure handles a single request from the presentation. It's often used in applications where business logic is simple or straightforward, and it's an alternative to more complex patterns like Domain Model or Service Layer.

# Key Characteristics of Transaction Script

1. **Procedural**:

- Business logic is implemented as a series of scripts or procedures, each corresponding to a transaction or a use case.

2. **Simple Organization**:

- Each script handles a specific transaction, making it easy to understand and implement.

3. **Straightforward**:

- Ideal for applications with simple business logic, reducing the need for complex object-oriented structures.

4. **Stateless**:

- Scripts typically do not maintain state between calls, which can simplify the logic but may also result in repeated code.

# Benefits of Transaction Script

1. **Simplicity**:

- Easy to implement and understand, making it suitable for small projects or applications with straightforward business logic.

2. **Performance**:

- Can be more performant in simple scenarios due to the lack of overhead associated with more complex patterns.

3. **Clear Structure**:

- Each script is focused on a specific transaction, making the codebase more modular and easier to navigate.

# Challenges of Transaction Script

1. **Scalability**:

- Can become difficult to manage as the application grows and business logic becomes more complex.

2. **Code Duplication**:

- Tends to result in code duplication since common logic may be repeated across multiple scripts.

3. **Maintenance**:

- Maintenance can become challenging as changes in business logic need to be reflected across multiple scripts.

# Example of Transaction Script in TypeScript

Consider an example where we manage transactions for a banking system.

1. **Defining the Account Model**:

```typescript
class Account {
  constructor(public id: string, public balance: number) {}
}
```

2. **Implementing Transaction Scripts**:

```typescript
class AccountService {
  private accounts: Map<string, Account> = new Map();

  constructor() {
    // Initializing with some accounts for demonstration
    this.accounts.set("1", new Account("1", 1000));
    this.accounts.set("2", new Account("2", 2000));
  }

  deposit(accountId: string, amount: number): void {
    const account = this.accounts.get(accountId);
    if (account) {
      account.balance += amount;
      console.log(
        `Deposited ${amount} to account ${accountId}. New balance: ${account.balance}`
      );
    } else {
      console.log(`Account ${accountId} not found.`);
    }
  }

  withdraw(accountId: string, amount: number): void {
    const account = this.accounts.get(accountId);
    if (account) {
      if (account.balance >= amount) {
        account.balance -= amount;
        console.log(
          `Withdrew ${amount} from account ${accountId}. New balance: ${account.balance}`
        );
      } else {
        console.log(`Insufficient balance in account ${accountId}.`);
      }
    } else {
      console.log(`Account ${accountId} not found.`);
    }
  }

  transfer(fromAccountId: string, toAccountId: string, amount: number): void {
    const fromAccount = this.accounts.get(fromAccountId);
    const toAccount = this.accounts.get(toAccountId);
    if (fromAccount && toAccount) {
      if (fromAccount.balance >= amount) {
        fromAccount.balance -= amount;
        toAccount.balance += amount;
        console.log(
          `Transferred ${amount} from account ${fromAccountId} to account ${toAccountId}.`
        );
      } else {
        console.log(`Insufficient balance in account ${fromAccountId}.`);
      }
    } else {
      console.log(`Account not found.`);
    }
  }
}
```

3. **Usage Example**:

```typescript
const accountService = new AccountService();

accountService.deposit("1", 500);
// Output: Deposited 500 to account 1. New balance: 1500

accountService.withdraw("1", 300);
// Output: Withdrew 300 from account 1. New balance: 1200

accountService.transfer("1", "2", 200);
// Output: Transferred 200 from account 1 to account 2.
```

# Real-Life Analogy

**Cashier's Transactions**:

Imagine a cashier in a store. Each transaction (like a purchase, return, or transfer) is handled as a separate script. The cashier doesn't need to know the details of other transactions; they just follow the procedure for the specific transaction at hand.

# Summary

Transaction Script is a straightforward and procedural approach to organizing business logic in applications. It is suitable for small or simple applications where the business logic is not overly complex. While it offers simplicity and performance benefits, it can lead to scalability and maintenance challenges as the application grows. Understanding when and how to use Transaction Script can help developers keep their codebases clean and manageable, especially in the early stages of development or in smaller projects.
