
# Abstract Factory Pattern in Salesforce Apex

## Overview
The Abstract Factory pattern provides a way to encapsulate a group of individual factories with a common goal. It helps to create families of related objects without specifying their concrete classes.

## Use Case
In Salesforce, you might need to create families of related objects, such as Accounts and their associated Contacts, in a consistent manner.

## Implementation

### Step 1: Define the Abstract Factory Interface
Create an interface that declares methods for creating related objects.

```apex
public interface SObjectAbstractFactory {
    Account createAccount();
    Contact createContact();
}
```

### Step 2: Implement Concrete Factories
Create concrete factory classes for each family of related objects.

```apex
public class StandardSObjectFactory implements SObjectAbstractFactory {
    public Account createAccount() {
        return new Account(Name = 'Standard Account');
    }

    public Contact createContact() {
        return new Contact(LastName = 'Standard Contact');
    }
}

public class PremiumSObjectFactory implements SObjectAbstractFactory {
    public Account createAccount() {
        return new Account(Name = 'Premium Account');
    }

    public Contact createContact() {
        return new Contact(LastName = 'Premium Contact');
    }
}
```

### Step 3: Use the Abstract Factory
Create a class to use the abstract factory to instantiate families of related objects.

```apex
public class SObjectAbstractFactoryCreator {
    public static void createSObjects(String accountType) {
        SObjectAbstractFactory factory;
        if (accountType == 'Standard') {
            factory = new StandardSObjectFactory();
        } else if (accountType == 'Premium') {
            factory = new PremiumSObjectFactory();
        } else {
            throw new IllegalArgumentException('Unsupported Account type');
        }
        Account account = factory.createAccount();
        Contact contact = factory.createContact();
        
        // Insert the created records into Salesforce
        insert account;
        insert contact;
    }
}
```

### Example Usage
Use the `SObjectAbstractFactoryCreator` class to create families of related objects based on input.

```apex
public class SObjectAbstractFactoryDemo {
    public static void demo() {
        SObjectAbstractFactoryCreator.createSObjects('Standard');
        SObjectAbstractFactoryCreator.createSObjects('Premium');
    }
}
```

## Conclusion
The Abstract Factory pattern in Salesforce Apex allows for creating families of related objects in a consistent manner, improving code modularity and maintainability.

[Return to Design Patterns Catalog](../README.md)
