
# Singleton Pattern in Salesforce Apex

## Overview
The Singleton pattern ensures that a class has only one instance and provides a global point of access to it. This is useful when exactly one object is needed to coordinate actions across the system.

## Use Case
In Salesforce, you might need a single instance of a configuration or utility class to manage settings or perform common operations across multiple classes.

## Implementation

### Step 1: Define the Singleton Class
Create a class with a private constructor and a static method to provide access to the single instance.

```apex
public class SingletonExample {
    private static SingletonExample instance;
    
    private SingletonExample() {
        // Private constructor
    }

    public static SingletonExample getInstance() {
        if (instance == null) {
            instance = new SingletonExample();
        }
        return instance;
    }

    public void performOperation() {
        // Perform some operation
    }
}
```

### Example Usage
Use the `SingletonExample` class to ensure a single instance is used.

```apex
public class SingletonDemo {
    public static void demo() {
        SingletonExample singleton = SingletonExample.getInstance();
        singleton.performOperation();
    }
}
```

## Conclusion
The Singleton pattern in Salesforce Apex ensures a class has only one instance and provides a global point of access to it, improving resource management and coordination.

[Return to Design Patterns Catalog](../README.md)
