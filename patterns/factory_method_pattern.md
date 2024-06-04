
# Factory Method Pattern in Salesforce Apex

## Overview
The Factory Method pattern is used to create objects without specifying the exact class of object that will be created. In Salesforce, this pattern can dynamically create different SObject types based on user input or other runtime conditions.

## Use Case
In a Salesforce application, you might need to create various SObjects (like `Account`, `Contact`, etc.) based on user selections from a dropdown menu in a Lightning component. Using the Factory Method pattern helps decouple the object creation logic from the client code.

## Implementation

### Step 1: Define the Factory Interface
Create an interface that declares the method for creating SObjects.

```apex
public interface SObjectFactory {
    SObject createSObject();
}
```

### Step 2: Implement Concrete Factories
Create concrete factory classes for each type of SObject.

```apex
public class AccountFactory implements SObjectFactory {
    public SObject createSObject() {
        return new Account(Name = 'New Account');
    }
}

public class ContactFactory implements SObjectFactory {
    public SObject createSObject() {
        return new Contact(LastName = 'New Contact');
    }
}
```

### Step 3: Use the Factory Method
Create a class to use the factory method to instantiate SObjects dynamically.

```apex
public class SObjectFactoryCreator {
    public static SObject createSObject(String sObjectType) {
        SObjectFactory factory;
        switch on sObjectType {
            when 'Account' {
                factory = new AccountFactory();
            }
            when 'Contact' {
                factory = new ContactFactory();
            }
            when else {
                throw new IllegalArgumentException('Unsupported SObject type');
            }
        }
        return factory.createSObject();
    }
}
```

### Example Usage
Use the `SObjectFactoryCreator` class to create different SObjects based on input.

```apex
public class SObjectFactoryDemo {
    public static void demo() {
        SObject account = SObjectFactoryCreator.createSObject('Account');
        SObject contact = SObjectFactoryCreator.createSObject('Contact');
        
        // Insert the created records into Salesforce
        insert account;
        insert contact;
    }
}
```

## Conclusion
The Factory Method pattern in Salesforce Apex allows for dynamic creation of different SObjects, improving code modularity and maintainability. This approach is particularly useful when the type of object to be created is determined at runtime.

[Return to Design Patterns Catalog](../README.md)
