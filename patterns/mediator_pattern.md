
# Mediator Pattern in Salesforce Apex

## Overview
The Mediator pattern defines an object that encapsulates how a set of objects interact. It promotes loose coupling by preventing objects from referring to each other explicitly.

## Use Case
In Salesforce, the Mediator pattern can be used to manage communication between different parts of a complex process, such as coordinating actions between multiple triggers or batch jobs.

## Implementation

### Step 1: Define the Mediator Interface
Create an interface that declares methods for communicating with colleague objects.

```apex
public interface Mediator {
    void notify(SObject sender, String event);
}
```

### Step 2: Implement Concrete Mediators
Create concrete classes that implement the mediator interface and coordinate interactions.

```apex
public class AccountMediator implements Mediator {
    private AccountTriggerHandler handler;

    public AccountMediator(AccountTriggerHandler handler) {
        this.handler = handler;
    }

    public void notify(SObject sender, String event) {
        if (event == 'beforeInsert') {
            handler.handleBeforeInsert((Account)sender);
        } else if (event == 'afterInsert') {
            handler.handleAfterInsert((Account)sender);
        }
    }
}
```

### Step 3: Implement Colleague Classes
Create classes that interact with the mediator to coordinate actions.

```apex
public class AccountTriggerHandler {
    private Mediator mediator;

    public AccountTriggerHandler(Mediator mediator) {
        this.mediator = mediator;
    }

    public void handleBeforeInsert(Account account) {
        System.debug('Handling before insert for: ' + account.Name);
    }

    public void handleAfterInsert(Account account) {
        System.debug('Handling after insert for: ' + account.Name);
    }
}
```

### Example Usage
Use the mediator to coordinate actions in a trigger.

```apex
trigger AccountTrigger on Account (before insert, after insert) {
    AccountTriggerHandler handler = new AccountTriggerHandler(new AccountMediator(handler));
    if (Trigger.isBefore && Trigger.isInsert) {
        for (Account account : Trigger.new) {
            handler.mediator.notify(account, 'beforeInsert');
        }
    }
    if (Trigger.isAfter && Trigger.isInsert) {
        for (Account account : Trigger.new) {
            handler.mediator.notify(account, 'afterInsert');
        }
    }
}
```

## Conclusion
The Mediator pattern in Salesforce Apex manages communication between different parts of a complex process, promoting loose coupling and improving code maintainability.

[Return to Design Patterns Catalog](../README.md)
