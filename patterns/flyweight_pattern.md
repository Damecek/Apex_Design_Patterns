
# Flyweight Pattern in Salesforce Apex

## Overview
The Flyweight pattern reduces the memory footprint by sharing as much data as possible with similar objects. It is useful when dealing with a large number of similar objects.

## Use Case
In Salesforce, the Flyweight pattern can be used to manage frequently accessed records, such as caching frequently queried records to minimize SOQL queries.

## Implementation

### Step 1: Define the Flyweight Interface
Create an interface that declares the methods for sharing data.

```apex
public interface SObjectFlyweight {
    SObject getSharedInstance(String key);
}
```

### Step 2: Implement the Flyweight
Create a class that implements the flyweight interface and shares data.

```apex
public class AccountFlyweight implements SObjectFlyweight {
    private Map<String, Account> accountCache = new Map<String, Account>();

    public Account getSharedInstance(String key) {
        if (!accountCache.containsKey(key)) {
            accountCache.put(key, [SELECT Id, Name FROM Account WHERE Id = :key LIMIT 1]);
        }
        return accountCache.get(key);
    }
}
```

### Example Usage
Use the `AccountFlyweight` to get shared instances of Account records.

```apex
public class FlyweightDemo {
    public static void demo() {
        AccountFlyweight flyweight = new AccountFlyweight();
        Account account1 = flyweight.getSharedInstance('001...');
        Account account2 = flyweight.getSharedInstance('001...'); // Same instance as account1

        System.debug(account1 == account2); // Outputs: true
    }
}
```

## Conclusion
The Flyweight pattern in Salesforce Apex reduces memory usage by sharing data between similar objects, improving performance and resource utilization.

[Return to Design Patterns Catalog](../README.md)
