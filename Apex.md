## what is apex
Apex is Salesforce’s strongly typed, Oops language designed to add custom logic to system events like button clicks, record updates, and web service requests. It features a syntax similar to Java and acts much like database stored procedures.

- **Hosted on the Server:** Apex runs entirely on the Salesforce Lightning Platform.
- **Database Integrated:** It provides direct access to Salesforce records using built-in query languages like SOQL and SOSL
- **Multitenant Aware:** Because resources are shared, Apex enforces strict governor limits to prevent runaway code from monopolizing the system.

Core Features and Data Types:

- **Primitives:** Integers, Doubles, Strings, Booleans, and Dates.
- **sObjects:** Special data types representing specific database records
- **Collections:** Lists, Sets, and Maps to handle multiple records efficiently.

### Apex Class:
A template or blueprint used to create objects and encapsulate reusable methods, variables, and programming logic . its holds Core business logic of our application and unit tests here.
- **Execution-** we can run using triggers, flows, Lightning Web Components, or anonymous blocks.

### Apex Trigger:
Block of code that runs automatically before or after DML events (insert, update, delete, undelete) on Salesforce records.

```apex
trigger SimpleTrigger on Account(after insert) {
  for (Account a : Trigger.new) {
    // Iterate over each sObject
  }

  // This single query finds every contact that is associated with any of the
  // triggering accounts. Note that although Trigger.new is a collection of
  // records, when used as a bind variable in a SOQL query, Apex automatically
  // transforms the list of records into a list of corresponding Ids.
  Contact[] cons = [
    SELECT LastName
    FROM Contact
    WHERE AccountId IN :Trigger.new
    WITH USER_MODE
  ];
}
```

