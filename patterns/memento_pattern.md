
# Memento Pattern in Salesforce Apex

## Overview
The Memento pattern provides the ability to restore an object to its previous state. It is useful for implementing undo operations.

## Use Case
In Salesforce, the Memento pattern can be used to snapshot object states for undo operations, such as reverting changes made to records.

## Implementation

### Step 1: Define the Memento Class
Create a class that stores the state of an object.

```apex
public class AccountMemento {
    public String name;
    public String industry;

    public AccountMemento(String name, String industry) {
        this.name = name;
        this.industry = industry;
    }
}
```

### Step 2: Implement the Originator Class
Create a class that creates and restores memento objects.

```apex
public class AccountOriginator {
    private Account account;

    public AccountOriginator(Account account) {
        this.account = account;
    }

    public AccountMemento save() {
        return new AccountMemento(account.Name, account.Industry);
    }

    public void restore(AccountMemento memento) {
        account.Name = memento.name;
        account.Industry = memento.industry;
    }
}
```

### Example Usage
Use the Memento pattern to save and restore an account's state.

```apex
public class MementoDemo {
    public static void demo() {
        Account account = new Account(Name = 'Original Account', Industry = 'Technology');
        AccountOriginator originator = new AccountOriginator(account);

        // Save the state to a memento
        AccountMemento memento = originator.save();

        // Change the account state
        account.Name = 'Updated Account';
        account.Industry = 'Finance';

        // Restore the state from the memento
        originator.restore(memento);
        System.debug('Restored Account Name: ' + account.Name);
        System.debug('Restored Account Industry: ' + account.Industry);
    }
}
```

## Conclusion
The Memento pattern in Salesforce Apex provides a way to restore an object to a previous state, useful for implementing undo operations.

[Return to Design Patterns Catalog](../README.md)
