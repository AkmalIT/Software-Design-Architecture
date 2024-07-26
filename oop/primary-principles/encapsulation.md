# Encapsulation

**Encapsulation** is a fundamental principle of Object-Oriented Programming (OOP) that involves bundling the data (attributes) and the methods (functions) that operate on the data into a single unit, known as a class. It also restricts direct access to some of an object's components, which is a means of preventing unintended interference and misuse of the data.

# Why is Encapsulation Important?

1. **Data Hiding**: Protects the internal state of an object from unintended or harmful interference.
2. **Modularity**: Helps in organizing code into discrete, logical units, making it more manageable.
3. **Control**: Provides control over the way data is accessed and modified.
4. **Maintenance**: Simplifies code maintenance by keeping related data and methods together, making the system easier to understand and modify.

# Real-Life Analogy

**ATM Machine**: Think of an ATM machine. You interact with it through a simple interface (buttons and screen), but you don't need to know the complex internals of how it processes transactions or communicates with the bank's server. This internal complexity is encapsulated within the ATM.

# Example of Encapsulation in JavaScript

In JavaScript, encapsulation can be achieved using classes and the concept of private and public members. Private members can be created using closures or the new # syntax for private fields.

**Using Closures**

```javascript
function createPerson(name, age) {
  let _name = name; // private variable
  let _age = age; // private variable

  return {
    getName: function () {
      return _name;
    },
    getAge: function () {
      return _age;
    },
    setName: function (newName) {
      _name = newName;
    },
    setAge: function (newAge) {
      if (newAge > 0) {
        _age = newAge;
      }
    },
  };
}

const person = createPerson("Alice", 25);
console.log(person.getName()); // Alice
person.setName("Bob");
console.log(person.getName()); // Bob
console.log(person._name); // undefined (can't access private variable)
```

**Using Classes with Private Fields**

```javascript
class Person {
  #name; // private field
  #age; // private field

  constructor(name, age) {
    this.#name = name;
    this.#age = age;
  }

  getName() {
    return this.#name;
  }

  getAge() {
    return this.#age;
  }

  setName(newName) {
    this.#name = newName;
  }

  setAge(newAge) {
    if (newAge > 0) {
      this.#age = newAge;
    }
  }
}

const person = new Person("Alice", 25);
console.log(person.getName()); // Alice
person.setName("Bob");
console.log(person.getName()); // Bob
console.log(person.#name); // SyntaxError: Private field '#name' must be declared in an enclosing class
```

# Benefits of Encapsulation

1. **Improves Data Integrity**: Prevents the accidental modification of data by restricting direct access.
2. **Enhances Security**: Sensitive data can be kept hidden from the outside world.
3. **Increases Flexibility**: Changes to encapsulated code are less likely to affect other parts of the program.
4. **Promotes Code Reusability**: Well-defined classes can be reused across different parts of a program or in different projects.

# Guidelines for Using Encapsulation

1. **Keep Data Private**: Use private fields and methods to hide the internal state of objects.
2. **Provide Public Accessors**: Use getter and setter methods to control access to private data.
3. **Encapsulate Related Data and Methods**: Group related data and methods together within classes.
4. **Limit Public Exposure**: Only expose methods and properties that are necessary for the object's operation from the outside.
