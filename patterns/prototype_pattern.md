
# Prototype Pattern in Salesforce Apex

## Overview
The Prototype pattern is used to create new objects by copying existing objects, known as prototypes. It is useful for creating objects that are similar to existing ones.

## Use Case
In Salesforce, you might need to clone records to create new ones with the same attributes, such as cloning an Opportunity with its related OpportunityLineItems.

## Implementation

### Step 1: Define the Prototype Interface
Create an interface that declares the method for cloning the object.

```apex
public interface SObjectPrototype {
    SObject cloneSObject();
}
```

### Step 2: Implement Concrete Prototypes
Create concrete prototype classes that implement the prototype interface.

```apex
public class OpportunityPrototype implements SObjectPrototype {
    private Opportunity opportunity;

    public OpportunityPrototype(Opportunity opportunity) {
        this.opportunity = opportunity;
    }

    public SObject cloneSObject() {
        Opportunity clone = opportunity.clone(false, false, false, false);
        return clone;
    }
}
```

### Step 3: Use the Prototype
Create a class to use the prototype to clone objects.

```apex
public class SObjectPrototypeCreator {
    public static SObject cloneSObject(SObjectPrototype prototype) {
        return prototype.cloneSObject();
    }
}
```

### Example Usage
Use the `SObjectPrototypeCreator` class to clone an Opportunity.

```apex
public class SObjectPrototypeDemo {
    public static void demo() {
        Opportunity original = [SELECT Id, Name, CloseDate FROM Opportunity LIMIT 1];
        OpportunityPrototype prototype = new OpportunityPrototype(original);
        Opportunity clone = (Opportunity)SObjectPrototypeCreator.cloneSObject(prototype);
        
        // Insert the cloned opportunity into Salesforce
        insert clone;
    }
}
```

## Conclusion
The Prototype pattern in Salesforce Apex allows for creating new objects by copying existing ones, improving code efficiency and consistency.

[Return to Design Patterns Catalog](../README.md)
