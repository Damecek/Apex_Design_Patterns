
# Iterator Pattern in Salesforce Apex

## Overview
The Iterator pattern provides a way to access elements of a collection sequentially without exposing its underlying representation.

## Use Case
In Salesforce, the Iterator pattern can be used to traverse complex collections of records, such as custom objects with child relationships, in a standardized manner.

## Implementation

### Step 1: Define the Iterator Interface
Create an interface that declares methods for iterating over a collection.

```apex
public interface Iterator {
    Boolean hasNext();
    SObject next();
}
```

### Step 2: Implement Concrete Iterators
Create concrete classes that implement the iterator interface and traverse collections.

```apex
public class AccountIterator implements Iterator {
    private List<Account> accounts;
    private Integer position = 0;

    public AccountIterator(List<Account> accounts) {
        this.accounts = accounts;
    }

    public Boolean hasNext() {
        return position < accounts.size();
    }

    public SObject next() {
        if (!hasNext()) {
            throw new NoSuchElementException();
        }
        return accounts[position++];
    }
}
```

### Example Usage
Use the `AccountIterator` to traverse a list of accounts.

```apex
public class IteratorDemo {
    public static void demo() {
        List<Account> accounts = [SELECT Id, Name FROM Account];
        Iterator iterator = new AccountIterator(accounts);

        while (iterator.hasNext()) {
            Account account = (Account) iterator.next();
            System.debug('Account Name: ' + account.Name);
        }
    }
}
```

## Conclusion
The Iterator pattern in Salesforce Apex provides a standardized way to access elements of a collection sequentially, improving code readability and maintainability.

[Return to Design Patterns Catalog](../README.md)
