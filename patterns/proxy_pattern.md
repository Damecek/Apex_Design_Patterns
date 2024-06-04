
# Proxy Pattern in Salesforce Apex

## Overview
The Proxy pattern provides a surrogate or placeholder for another object to control access to it. It is useful for implementing lazy initialization, access control, and logging.

## Use Case
In Salesforce, the Proxy pattern can be used to control access to Salesforce records or services, providing additional functionalities such as validation or logging.

## Implementation

### Step 1: Define the Proxy Interface
Create an interface that declares the methods to be implemented by the proxy and the real subject.

```apex
public interface AccountService {
    void performOperation();
}
```

### Step 2: Implement the Real Subject
Create a class that implements the proxy interface and performs the actual operation.

```apex
public class RealAccountService implements AccountService {
    public void performOperation() {
        System.debug('Performing account operation');
    }
}
```

### Step 3: Implement the Proxy
Create a class that implements the proxy interface and controls access to the real subject.

```apex
public class AccountServiceProxy implements AccountService {
    private RealAccountService realService;

    public AccountServiceProxy(RealAccountService realService) {
        this.realService = realService;
    }

    public void performOperation() {
        System.debug('Logging: Before performing operation');
        realService.performOperation();
        System.debug('Logging: After performing operation');
    }
}
```

### Example Usage
Use the `AccountServiceProxy` to control access to the `RealAccountService`.

```apex
public class ProxyDemo {
    public static void demo() {
        RealAccountService realService = new RealAccountService();
        AccountService proxy = new AccountServiceProxy(realService);
        proxy.performOperation();
    }
}
```

## Conclusion
The Proxy pattern in Salesforce Apex provides a surrogate or placeholder for another object, controlling access and adding additional functionalities such as logging.

[Return to Design Patterns Catalog](../README.md)
