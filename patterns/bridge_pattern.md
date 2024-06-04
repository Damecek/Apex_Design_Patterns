
# Bridge Pattern in Salesforce Apex

## Overview
The Bridge pattern decouples an abstraction from its implementation so that the two can vary independently. This pattern is useful for enabling flexibility and extensibility in systems.

## Use Case
In Salesforce, the Bridge pattern can be used to separate the logic of different objects from their implementation, such as varying notification methods independently of the notification logic.

## Implementation

### Step 1: Define the Abstraction Interface
Create an interface that declares the methods for the abstraction.

```apex
public abstract class Notification {
    protected NotificationSender sender;

    public Notification(NotificationSender sender) {
        this.sender = sender;
    }

    public abstract void send(String message);
}
```

### Step 2: Implement the Implementation Interface
Create an interface that declares the methods for the implementation.

```apex
public interface NotificationSender {
    void sendNotification(String message);
}
```

### Step 3: Implement Concrete Implementations
Create concrete classes that implement the implementation interface.

```apex
public class EmailSender implements NotificationSender {
    public void sendNotification(String message) {
        System.debug('Sending Email: ' + message);
    }
}

public class SmsSender implements NotificationSender {
    public void sendNotification(String message) {
        System.debug('Sending SMS: ' + message);
    }
}
```

### Step 4: Implement Refined Abstractions
Create concrete classes that extend the abstraction and use the implementations.

```apex
public class UrgentNotification extends Notification {
    public UrgentNotification(NotificationSender sender) {
        super(sender);
    }

    public void send(String message) {
        sender.sendNotification('Urgent: ' + message);
    }
}

public class RegularNotification extends Notification {
    public RegularNotification(NotificationSender sender) {
        super(sender);
    }

    public void send(String message) {
        sender.sendNotification('Regular: ' + message);
    }
}
```

### Example Usage
Use the bridge to send different types of notifications.

```apex
public class BridgeDemo {
    public static void demo() {
        NotificationSender emailSender = new EmailSender();
        NotificationSender smsSender = new SmsSender();

        Notification urgentEmail = new UrgentNotification(emailSender);
        urgentEmail.send('This is an urgent message.');

        Notification regularSms = new RegularNotification(smsSender);
        regularSms.send('This is a regular message.');
    }
}
```

## Conclusion
The Bridge pattern in Salesforce Apex decouples an abstraction from its implementation, allowing the two to vary independently and promoting flexibility and extensibility.

[Return to Design Patterns Catalog](../README.md)
