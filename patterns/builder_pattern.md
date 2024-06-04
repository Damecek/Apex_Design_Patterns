
# Builder Pattern in Salesforce Apex

## Overview
The Builder pattern is used to construct complex objects step by step. It allows you to produce different types and representations of an object using the same construction process.

## Use Case
In Salesforce, you might need to construct complex SObjects with nested relationships, such as an Order with multiple OrderItems.

## Implementation

### Step 1: Define the Builder Interface
Create an interface that declares the methods for building parts of the complex object.

```apex
public interface OrderBuilder {
    void buildOrder(String orderName);
    void addOrderItem(String itemName, Integer quantity);
    Order getOrder();
}
```

### Step 2: Implement Concrete Builders
Create concrete builder classes that implement the builder interface.

```apex
public class StandardOrderBuilder implements OrderBuilder {
    private Order order;

    public void buildOrder(String orderName) {
        order = new Order(Name = orderName);
    }

    public void addOrderItem(String itemName, Integer quantity) {
        if (order.OrderItems == null) {
            order.OrderItems = new List<OrderItem>();
        }
        order.OrderItems.add(new OrderItem(Name = itemName, Quantity = quantity));
    }

    public Order getOrder() {
        return order;
    }
}
```

### Step 3: Use the Builder
Create a class to use the builder to construct the complex object.

```apex
public class OrderDirector {
    private OrderBuilder builder;

    public OrderDirector(OrderBuilder builder) {
        this.builder = builder;
    }

    public Order constructOrder(String orderName, List<Map<String, Object>> items) {
        builder.buildOrder(orderName);
        for (Map<String, Object> item : items) {
            builder.addOrderItem((String)item.get('Name'), (Integer)item.get('Quantity'));
        }
        return builder.getOrder();
    }
}
```

### Example Usage
Use the `OrderDirector` class to construct an Order with multiple OrderItems.

```apex
public class OrderBuilderDemo {
    public static void demo() {
        OrderBuilder builder = new StandardOrderBuilder();
        OrderDirector director = new OrderDirector(builder);
        List<Map<String, Object>> items = new List<Map<String, Object>>{
            new Map<String, Object>{'Name' => 'Item1', 'Quantity' => 2},
            new Map<String, Object>{'Name' => 'Item2', 'Quantity' => 3}
        };
        Order order = director.constructOrder('New Order', items);

        // Insert the created order into Salesforce
        insert order;
    }
}
```

## Conclusion
The Builder pattern in Salesforce Apex allows for constructing complex objects step by step, improving code readability and maintainability.

[Return to Design Patterns Catalog](../README.md)
