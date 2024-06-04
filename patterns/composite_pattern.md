
# Composite Pattern in Salesforce Apex

## Overview
The Composite pattern allows you to compose objects into tree structures to represent part-whole hierarchies. This pattern lets clients treat individual objects and compositions of objects uniformly.

## Use Case
In Salesforce, the Composite pattern can be used to manage complex hierarchical data structures, such as organizational structures or product categories.

## Implementation

### Step 1: Define the Component Interface
Create an interface that declares the operations common to both simple and complex objects.

```apex
public interface Component {
    void operation();
}
```

### Step 2: Implement Leaf Class
Create a class that represents leaf objects in the composition.

```apex
public class Leaf implements Component {
    public void operation() {
        System.debug('Leaf operation');
    }
}
```

### Step 3: Implement Composite Class
Create a class that represents composite objects and stores child components.

```apex
public class Composite implements Component {
    private List<Component> children = new List<Component>();

    public void add(Component component) {
        children.add(component);
    }

    public void remove(Component component) {
        children.remove(component);
    }

    public void operation() {
        for (Component child : children) {
            child.operation();
        }
    }
}
```

### Example Usage
Use the composite and leaf objects to form a tree structure and perform operations.

```apex
public class CompositeDemo {
    public static void demo() {
        Leaf leaf1 = new Leaf();
        Leaf leaf2 = new Leaf();

        Composite composite = new Composite();
        composite.add(leaf1);
        composite.add(leaf2);

        composite.operation();
    }
}
```

## Conclusion
The Composite pattern in Salesforce Apex allows for creating hierarchical structures, enabling clients to interact with individual objects and compositions of objects uniformly.

[Return to Design Patterns Catalog](../README.md)
