
# Visitor Pattern in Salesforce Apex

## Overview
The Visitor pattern allows you to add further operations to objects without having to modify them. It separates an algorithm from the object structure it operates on.

## Use Case
In Salesforce, the Visitor pattern can be used to perform operations on a complex object structure, such as processing different types of records in a polymorphic way.

## Implementation

### Step 1: Define the Visitor Interface
Create an interface that declares methods for visiting different elements.

```apex
public interface Visitor {
    void visitAccount(Account account);
    void visitContact(Contact contact);
}
```

### Step 2: Implement Concrete Visitors
Create concrete classes that implement the visitor interface and define specific operations.

```apex
public class RecordVisitor implements Visitor {
    public void visitAccount(Account account) {
        System.debug('Visited Account: ' + account.Name);
    }

    public void visitContact(Contact contact) {
        System.debug('Visited Contact: ' + contact.Name);
    }
}
```

### Step 3: Define the Element Interface
Create an interface for elements that can accept a visitor.

```apex
public interface Element {
    void accept(Visitor visitor);
}
```

### Step 4: Implement Concrete Elements
Create concrete classes that implement the element interface and accept visitors.

```apex
public class VisitableAccount extends Account implements Element {
    public void accept(Visitor visitor) {
        visitor.visitAccount(this);
    }
}

public class VisitableContact extends Contact implements Element {
    public void accept(Visitor visitor) {
        visitor.visitContact(this);
    }
}
```

### Example Usage
Use the visitor to perform operations on elements.

```apex
public class VisitorDemo {
    public static void demo() {
        List<Element> elements = new List<Element>{
            new VisitableAccount(Name = 'Account 1'),
            new VisitableContact(FirstName = 'Contact', LastName = '1')
        };
        
        Visitor visitor = new RecordVisitor();
        for (Element element : elements) {
            element.accept(visitor);
        }
    }
}
```

## Conclusion
The Visitor pattern in Salesforce Apex allows for adding operations to objects without modifying them, promoting flexibility and separation of concerns.

[Return to Design Patterns Catalog](../README.md)
