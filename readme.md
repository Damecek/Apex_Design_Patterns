# Design Patterns in Salesforce Apex

## Creational Patterns
- **[Factory Method](patterns/factory_method_pattern.md):** Create different types of records (e.g., Account, Contact) dynamically based on user input.
- **[Abstract Factory](patterns/abstract_factory_pattern.md):** Generate related objects like accounts and their associated contacts.
- **[Builder](patterns/builder_pattern.md):** Construct complex Salesforce objects with nested details, such as Orders with multiple OrderItems.
- **[Prototype](patterns/prototype_pattern.md):** Clone existing Salesforce records to create new ones.
- **[Singleton](patterns/singleton_pattern.md):** Ensure a single instance of a configuration or utility class across a transaction.

## Structural Patterns
- **[Adapter](patterns/adapter_pattern.md):** Integrate Salesforce with external services by adapting external API responses.
- **[Bridge](patterns/bridge_pattern.md):** Separate complex logic from object creation for reusable components.
- **[Composite](patterns/composite_pattern.md):** Manage hierarchies of records, such as Opportunity and related OpportunityLineItems.
- **[Decorator](patterns/decorator_pattern.md):** Add functionalities to Salesforce objects dynamically without altering their structure.
- **[Facade](patterns/facade_pattern.md):** Simplify complex interfaces with a unified class, e.g., a service class to handle all DML operations.
- **[Flyweight](patterns/flyweight_pattern.md):** Reuse shared Salesforce objects to save memory, like frequently accessed records.
- **[Proxy](patterns/proxy_pattern.md):** Control access to Salesforce records or services, providing validation or logging.

## Behavioral Patterns
- **[Chain of Responsibility](patterns/chain_of_responsibility_pattern.md):** Implement approval processes where multiple handlers process a request.
- **[Command](patterns/command_pattern.md):** Encapsulate Apex methods as command objects to be executed later.
- **[Iterator](patterns/iterator_pattern.md):** Traverse complex collections of records, like custom objects with child relationships.
- **[Mediator](patterns/mediator_pattern.md):** Manage communication between different parts of a complex Salesforce process.
- **[Memento](patterns/memento_pattern.md):** Snapshot object states for undo operations in record updates.
- **[Observer](patterns/observer_pattern.md):** Implement trigger frameworks where multiple observers react to changes in Salesforce records.
- **[State](patterns/state_pattern.md):** Manage the state of a Salesforce record and change behavior accordingly.
- **[Strategy](patterns/strategy_pattern.md):** Swap out different algorithms within Salesforce for processing data.
- **[Template Method](patterns/template_method_pattern.md):** Define a skeleton of an operation, deferring some steps to subclasses.
- **[Visitor](patterns/visitor_pattern.md):** Perform operations across a collection of different objects, such as different SObject types.
