
# Template Method Pattern in Salesforce Apex

## Overview
The Template Method pattern defines the skeleton of an algorithm in a method, deferring some steps to subclasses. It allows subclasses to redefine certain steps of an algorithm without changing its structure.

## Use Case
In Salesforce, the Template Method pattern can be used to define a common workflow for processing records while allowing specific steps to be customized by subclasses.

## Implementation

### Step 1: Define the Abstract Class
Create an abstract class that defines the template method and abstract methods for the steps.

```apex
public abstract class RecordProcessor {
    public void process() {
        fetchRecords();
        processRecords();
        saveRecords();
    }

    protected abstract void fetchRecords();
    protected abstract void processRecords();
    protected abstract void saveRecords();
}
```

### Step 2: Implement Concrete Classes
Create concrete classes that implement the abstract methods.

```apex
public class AccountProcessor extends RecordProcessor {
    private List<Account> accounts;

    protected void fetchRecords() {
        accounts = [SELECT Id, Name FROM Account];
    }

    protected void processRecords() {
        for (Account account : accounts) {
            account.Name = account.Name + ' Processed';
        }
    }

    protected void saveRecords() {
        update accounts;
    }
}
```

### Example Usage
Use the concrete class to process records.

```apex
public class TemplateMethodDemo {
    public static void demo() {
        RecordProcessor processor = new AccountProcessor();
        processor.process();
    }
}
```

## Conclusion
The Template Method pattern in Salesforce Apex defines the skeleton of an algorithm, allowing specific steps to be customized by subclasses, promoting code reuse and consistency.

[Return to Design Patterns Catalog](../README.md)
