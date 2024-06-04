
# Facade Pattern in Salesforce Apex

## Overview
The Facade pattern provides a simplified interface to a complex subsystem. It hides the complexities of the subsystem by providing a unified interface.

## Use Case
In Salesforce, the Facade pattern can be used to simplify interactions with complex systems, such as integrating multiple external APIs or simplifying complex business logic.

## Implementation

### Step 1: Define the Facade Class
Create a class that provides a simplified interface to the complex subsystem.

```apex
public class AccountServiceFacade {
    public void createAccountWithContact(String accountName, String contactLastName) {
        Account account = new Account(Name = accountName);
        insert account;

        Contact contact = new Contact(LastName = contactLastName, AccountId = account.Id);
        insert contact;
    }
}
```

### Example Usage
Use the `AccountServiceFacade` to create an Account with an associated Contact.

```apex
public class FacadeDemo {
    public static void demo() {
        AccountServiceFacade facade = new AccountServiceFacade();
        facade.createAccountWithContact('Acme Corporation', 'Doe');
    }
}
```

## Conclusion
The Facade pattern in Salesforce Apex simplifies complex interactions by providing a unified interface, improving code readability and maintainability.

[Return to Design Patterns Catalog](../README.md)
