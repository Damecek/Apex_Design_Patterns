
# Adapter Pattern in Salesforce Apex

## Overview
The Adapter pattern allows incompatible interfaces to work together. It acts as a bridge between two incompatible interfaces by converting the interface of a class into another interface that a client expects.

## Use Case
In Salesforce, the Adapter pattern can be used to integrate external systems or legacy code with your existing Apex classes by adapting their interfaces.

## Implementation

### Step 1: Define the Target Interface
Create an interface that defines the domain-specific interface used by the client.

```apex
public interface Target {
    String request();
}
```

### Step 2: Implement the Adaptee Class
Create a class that has an existing interface but needs to be adapted.

```apex
public class Adaptee {
    public String specificRequest() {
        return 'Adaptee response';
    }
}
```

### Step 3: Implement the Adapter Class
Create a class that implements the target interface and translates the requests to the adaptee.

```apex
public class Adapter implements Target {
    private Adaptee adaptee;

    public Adapter(Adaptee adaptee) {
        this.adaptee = adaptee;
    }

    public String request() {
        return adaptee.specificRequest();
    }
}
```

### Example Usage
Use the adapter to interact with the adaptee through the target interface.

```apex
public class AdapterDemo {
    public static void demo() {
        Adaptee adaptee = new Adaptee();
        Target adapter = new Adapter(adaptee);
        System.debug(adapter.request());
    }
}
```

## Conclusion
The Adapter pattern in Salesforce Apex allows for integrating incompatible interfaces, enabling systems to work together more effectively and promoting code reuse.

[Return to Design Patterns Catalog](../README.md)
