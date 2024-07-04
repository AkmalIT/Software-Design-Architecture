# Hollywood Principle

**Hollywood Principle** is a software design principle that states "Don't call us, we'll call you." It promotes a design where lower-level components do not call higher-level components directly but are instead called by higher-level components when needed. This principle is often used in frameworks and libraries to maintain control over the flow of the application.

# Why is the Hollywood Principle Important?

1. **Decoupling**: It helps in decoupling the higher-level logic from the lower-level details, leading to more modular and maintainable code.
2. **Inversion of Control**: It enforces Inversion of Control (IoC), where the control flow of a program is inverted compared to traditional procedural programming.
3. **Flexibility**: Provides flexibility in extending and modifying the system since the control logic resides in one place.
4. **Simplified Code Management**: Higher-level components manage the interaction between lower-level components, simplifying the overall code management.

# Real-Life Analogy

**Movie Casting**: Imagine a movie director (higher-level component) managing actors (lower-level components). Actors do not decide when to perform; instead, the director calls them when their performance is needed.

# Example of the Hollywood Principle in Code

Let's consider a plugin system where the application framework controls when plugins are invoked.

**Without the Hollywood Principle**

```typescript
class Plugin {
  doTask() {
    console.log("Plugin task executed");
  }
}

class Application {
  plugin: Plugin;

  constructor(plugin: Plugin) {
    this.plugin = plugin;
  }

  run() {
    // Directly calling the plugin method
    this.plugin.doTask();
  }
}

const plugin = new Plugin();
const app = new Application(plugin);
app.run();
```

In this example, the application directly calls the plugin's doTask method, leading to tighter coupling.

**With the Hollywood Principle**

```typescript
class Plugin {
  doTask() {
    console.log("Plugin task executed");
  }
}

class Application {
  plugin: Plugin;

  constructor(plugin: Plugin) {
    this.plugin = plugin;
  }

  run() {
    // Application framework decides when to call the plugin method
    this.invokePlugin();
  }

  invokePlugin() {
    this.plugin.doTask();
  }
}

const plugin = new Plugin();
const app = new Application(plugin);
app.run();
```

In this example, the application controls when the plugin's method is called, following the Hollywood Principle and promoting decoupling.

# Benefits of Using the Hollywood Principle

1. **Modularity**: Enhances modularity by decoupling the components.
2. **Ease of Maintenance**: Easier to maintain and extend the code since higher-level components manage the control flow.
3. **Testability**: Improves testability by isolating components and controlling their interaction.
4. **Scalability**: Facilitates scalability by allowing easy addition or replacement of lower-level components without affecting higher-level logic.

# Guidelines for Implementing the Hollywood Principle

1. **Use Interfaces and Abstract Classes**: Define interfaces or abstract classes for lower-level components to implement.
2. **Control Flow Management**: Ensure that the higher-level components manage the control flow and interactions.
3. **Event-Driven Design**: Adopt an event-driven design where lower-level components register themselves with higher-level components.
4. **Frameworks and Inversion of Control**: Use frameworks that enforce IoC to adhere to the Hollywood Principle.
