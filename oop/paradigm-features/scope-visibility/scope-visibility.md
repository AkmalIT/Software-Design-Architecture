# Scope Visibility

In TypeScript, you can use access modifiers directly within class definitions to control the visibility and accessibility of class members. Here’s how you can use public, private, and protected in TypeScript.

# Public Members

Public members are accessible from anywhere. This is the default visibility in TypeScript if no access modifier is specified.

```typescript
class Person {
  public name: string; // public by default
  public age: number; // public by default

  constructor(name: string, age: number) {
    this.name = name;
    this.age = age;
  }

  public greet(): void {
    console.log(
      `Hello, my name is ${this.name} and I am ${this.age} years old.`
    );
  }
}

const person = new Person("Alice", 30);
person.greet(); // Accessible, Output: Hello, my name is Alice and I am 30 years old.
console.log(person.name); // Accessible
console.log(person.age); // Accessible
```

# Private Members

Private members are only accessible within the class they are declared in.

```typescript
class Person {
  private name: string;
  private age: number;

  constructor(name: string, age: number) {
    this.name = name;
    this.age = age;
  }

  public greet(): void {
    console.log(
      `Hello, my name is ${this.name} and I am ${this.age} years old.`
    );
  }
}

const person = new Person("Bob", 40);
person.greet(); // Accessible, Output: Hello, my name is Bob and I am 40 years old.
// console.log(person.name); // Error: Property 'name' is private and only accessible within class 'Person'.
// console.log(person.age); // Error: Property 'age' is private and only accessible within class 'Person'.
```

# Protected Members

Protected members are accessible within the class they are declared in and in subclasses.

```typescript
class Person {
  protected name: string;
  protected age: number;

  constructor(name: string, age: number) {
    this.name = name;
    this.age = age;
  }

  public greet(): void {
    console.log(
      `Hello, my name is ${this.name} and I am ${this.age} years old.`
    );
  }
}

class Employee extends Person {
  private jobTitle: string;

  constructor(name: string, age: number, jobTitle: string) {
    super(name, age);
    this.jobTitle = jobTitle;
  }

  public introduce(): void {
    console.log(
      `Hello, my name is ${this.name}, I am ${this.age} years old, and I work as a ${this.jobTitle}.`
    );
  }
}

const employee = new Employee("Charlie", 35, "Developer");
employee.greet(); // Accessible, Output: Hello, my name is Charlie and I am 35 years old.
employee.introduce(); // Accessible, Output: Hello, my name is Charlie, I am 35 years old, and I work as a Developer.
// console.log(employee.name); // Error: Property 'name' is protected and only accessible within class 'Person' and its subclasses.
// console.log(employee.age); // Error: Property 'age' is protected and only accessible within class 'Person' and its subclasses.
```

# Summary

- **Public** members can be accessed from anywhere.
- **Private** members can only be accessed within the class they are declared in.
- **Protected** members can be accessed within the class they are declared in and in subclasses.

# Benefits of Using Access Modifiers

1. **Encapsulation**: Helps in encapsulating data, protecting the internal state of an object.
2. **Security**: Enhances security by restricting access to sensitive data and methods.
3. **Maintainability**: Improves code maintainability by defining clear interfaces for interacting with objects.
4. **Modularity**: Supports modularity by clearly defining the boundaries of each class.

# Guidelines for Using Access Modifiers

1. **Use Public for APIs**: Use public for methods and properties that need to be accessed from outside the class.
2. **Use Private for Internal Logic**: Use private for methods and properties that should not be exposed outside the class.
3. **Use Protected for Inheritance**: Use protected for methods and properties that should be accessible in subclasses but not from outside.
