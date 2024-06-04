
# Chain of Responsibility Pattern in Salesforce Apex

## Overview
The Chain of Responsibility pattern passes a request along a chain of handlers. Upon receiving a request, each handler decides either to process the request or to pass it to the next handler in the chain.

## Use Case
In Salesforce, the Chain of Responsibility pattern can be used to implement approval processes where multiple handlers process a request, such as handling different stages of an approval workflow.

## Implementation

### Step 1: Define the Handler Interface
Create an interface that declares the method for handling requests.

```apex
public interface Approver {
    void setNext(Approver nextApprover);
    void approveRequest(Integer amount);
}
```

### Step 2: Implement Concrete Handlers
Create concrete classes that implement the handler interface and handle requests.

```apex
public class Manager implements Approver {
    private Approver nextApprover;

    public void setNext(Approver nextApprover) {
        this.nextApprover = nextApprover;
    }

    public void approveRequest(Integer amount) {
        if (amount <= 1000) {
            System.debug('Manager approved the request');
        } else if (nextApprover != null) {
            nextApprover.approveRequest(amount);
        }
    }
}

public class Director implements Approver {
    private Approver nextApprover;

    public void setNext(Approver nextApprover) {
        this.nextApprover = nextApprover;
    }

    public void approveRequest(Integer amount) {
        if (amount <= 5000) {
            System.debug('Director approved the request');
        } else if (nextApprover != null) {
            nextApprover.approveRequest(amount);
        }
    }
}
```

### Example Usage
Use the chain of handlers to process a request.

```apex
public class ChainOfResponsibilityDemo {
    public static void demo() {
        Approver manager = new Manager();
        Approver director = new Director();
        manager.setNext(director);

        manager.approveRequest(500);
        manager.approveRequest(2000);
        manager.approveRequest(6000);
    }
}
```

## Conclusion
The Chain of Responsibility pattern in Salesforce Apex allows for creating a chain of handlers to process requests, improving flexibility and handling complex workflows.

[Return to Design Patterns Catalog](../README.md)
