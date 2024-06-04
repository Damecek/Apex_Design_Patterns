
# Decorator Pattern in Salesforce Apex

## Overview
The Decorator pattern allows behavior to be added to an individual object, dynamically, without affecting the behavior of other objects from the same class.

## Use Case
In Salesforce, the Decorator pattern can be used to extend the behavior of objects, such as adding additional functionality to a standard object like an Account or Contact.

## Implementation

### Step 1: Define the Component Interface
Create an interface that declares the operations to be implemented.

```apex
public interface AccountComponent {
    void display();
}
```

### Step 2: Implement Concrete Components
Create concrete classes that implement the component interface.

```apex
public class StandardAccount implements AccountComponent {
    public void display() {
        System.debug('Standard Account');
    }
}
```

### Step 3: Implement the Decorator Class
Create a class that implements the component interface and has a reference to a component object.

```apex
public abstract class AccountDecorator implements AccountComponent {
    protected AccountComponent decoratedAccount;

    public AccountDecorator(AccountComponent decoratedAccount) {
        this.decoratedAccount = decoratedAccount;
    }

    public void display() {
        decoratedAccount.display();
    }
}
```

### Step 4: Implement Concrete Decorators
Create concrete classes that extend the decorator class and add functionality.

```apex
public class PremiumAccountDecorator extends AccountDecorator {
    public PremiumAccountDecorator(AccountComponent decoratedAccount) : super(decoratedAccount) {}

    public void display() {
        decoratedAccount.display();
        setPremiumFeatures();
    }

    private void setPremiumFeatures() {
        System.debug('Premium Account Features');
    }
}
```

### Example Usage
Use the decorator to add functionality to an account object.

```apex
public class DecoratorDemo {
    public static void demo() {
        AccountComponent standardAccount = new StandardAccount();
        AccountComponent premiumAccount = new PremiumAccountDecorator(standardAccount);

        System.debug('Standard Account:');
        standardAccount.display();

        System.debug('Premium Account:');
        premiumAccount.display();
    }
}
```

## Conclusion
The Decorator pattern in Salesforce Apex allows for adding behavior to individual objects dynamically, promoting code flexibility and reuse.

[Return to Design Patterns Catalog](../README.md)
