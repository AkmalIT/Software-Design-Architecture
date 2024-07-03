# Inheritance

**Inheritance** is one of the core principles of Object-Oriented Programming (OOP). It allows one class (called a subclass or child class) to inherit properties and methods from another class (called a superclass or parent class). This promotes code reuse and the creation of class hierarchies.

# Why is inheritance needed?

1. **Code reuse**: Child classes can use the code of parent classes without duplicating it.
2. **Hierarchy creation**: Helps organize classes into logical hierarchies, making the code more understandable and structured.
3. **Polymorphism**: Allows objects of child classes to be used in the context of the parent class, simplifying object management and making the code more flexible.

# Real-life example

Imagine a company's organizational structure. The company has common positions such as "Employee," "Manager," and "Director."

- **Employee** might have common attributes like name and salary, and methods like work.
- **Manager** is also an employee, but they have additional attributes like department and methods like manage a team.
- **Director** is also an employee, but they have even more responsibilities, such as managing the entire company.

# Example of inheritance in JavaScript

```javascript
// Parent class
class Employee {
  constructor(name, salary) {
    this.name = name;
    this.salary = salary;
  }

  work() {
    console.log(`${this.name} is working.`);
  }
}

// Child class inheriting from Employee
class Manager extends Employee {
  constructor(name, salary, department) {
    super(name, salary);
    this.department = department;
  }

  manage() {
    console.log(`${this.name} is managing the ${this.department} department.`);
  }
}

// Another child class inheriting from Employee
class Director extends Employee {
  constructor(name, salary) {
    super(name, salary);
  }

  oversee() {
    console.log(`${this.name} is overseeing the company.`);
  }
}

// Creating objects
const emp = new Employee("John Doe", 50000);
const mgr = new Manager("Jane Smith", 70000, "Marketing");
const dir = new Director("Alice Johnson", 100000);

// Using objects
emp.work(); // John Doe is working.
mgr.work(); // Jane Smith is working.
mgr.manage(); // Jane Smith is managing the Marketing department.
dir.work(); // Alice Johnson is working.
dir.oversee(); // Alice Johnson is overseeing the company.
```

# Advantages of inheritance

1. **Simplifies code reuse**: Core logic can be defined in parent classes and used in child classes.
2. **Creates logical hierarchies**: Organizing classes in hierarchies makes the code more readable and manageable.
3. **Enables polymorphism**: Allows objects of different classes to be used through the same interface.

# Disadvantages of inheritance

1. **Can lead to tight coupling**: If changes in the parent class require changes in the child classes.
2. **Complexities with deep hierarchies**: Multi-level inheritance can make the code difficult to understand and maintain.
3. **Issues with multiple inheritance**: Some programming languages do not support multiple inheritance due to complexity and potential conflicts.
