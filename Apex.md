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

# Future vs Queueable vs Batch vs Scheduled Apex

| Feature | Future Method | Queueable Apex | Batch Apex | Scheduled Apex |
|----------|-------------|---------------|------------|---------------|
| Purpose | Simple asynchronous processing | Complex asynchronous processing | Process large volumes of records | Run jobs at a specified time |
| Declaration | `@future` | `implements Queueable` | `implements Database.Batchable` | `implements Schedulable` |
| Supports sObjects | ❌ No | ✅ Yes | ✅ Yes | ✅ Yes |
| Supports Primitive Types | ✅ Yes | ✅ Yes | ✅ Yes | ✅ Yes |
| Supports Complex Types | ❌ No | ✅ Yes | ✅ Yes | ✅ Yes |
| Callouts | ✅ Yes (`@future(callout=true)`) | ✅ Yes (`Database.AllowsCallouts`) | ✅ Yes (`Database.AllowsCallouts`) | ✅ Indirectly |
| Job Monitoring | ❌ No | ✅ Yes | ✅ Yes | ✅ Yes |
| Job Chaining | ❌ No | ✅ Yes | ✅ Via `finish()` | ✅ Can schedule other jobs |
| Governor Limits | Shared Async Limits | Shared Async Limits | New Limits for Each Batch | Shared Async Limits |
| Execution Order Guaranteed | ❌ No | ❌ No | Batch Order Managed | ✅ Scheduled Time |
| Maximum Records | Small Volume | Small to Medium Volume | Millions of Records | Depends on Job Logic |
| Best Use Case | Sending emails, simple updates | Integrations, complex async logic | Mass data processing | Automated recurring jobs |
| Salesforce Recommendation | Legacy option | Preferred over Future Methods | Best for large datasets | Best for recurring executions |

# Quick Decision Guide

| Scenario | Recommended Apex Type |
|-----------|----------------------|
| Send email asynchronously | Future Apex |
| Make external API call and track status | Queueable Apex |
| Process 500,000 records | Batch Apex |
| Run job every night at 1 AM | Scheduled Apex |
| Chain multiple async jobs | Queueable Apex |
| Data cleanup for millions of records | Batch Apex |
| Daily product synchronization | Scheduled + Batch Apex |
| Order processing in B2B Commerce | Queueable Apex |

# Memory Trick

- **Future Apex** → Do it later
- **Queueable Apex** → Do it later with tracking and chaining
- **Batch Apex** → Do it later for huge data volumes
- **Scheduled Apex** → Do it later at a specific time
``



