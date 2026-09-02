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




-----------------------------------------------




# LWC Data Fetching from Apex

## GET data from Apex to LWC (Imperative Call)

### When to Use
- When data retrieval is triggered by a user action (button click).
- When you need more control over when the Apex method is executed.
- Supports both cacheable and non-cacheable Apex methods.

### Apex Class

```apex
public with sharing class AccountController {
    @AuraEnabled
    public static List<Account> getAccounts() {
        return [
            SELECT Id, Name, Industry
            FROM Account
            LIMIT 10
        ];
    }
}
```

### LWC JavaScript

```javascript
import { LightningElement } from 'lwc';
import getAccounts from '@salesforce/apex/AccountController.getAccounts';

export default class AccountListImperative extends LightningElement {
    accounts;
    error;

    handleLoadData() {
        getAccounts()
            .then(result => {
                this.accounts = result;
                this.error = undefined;
            })
            .catch(error => {
                this.error = error;
                this.accounts = undefined;
            });
    }
}
```

### LWC HTML

```html
<template>
    <lightning-button
        label="Load Accounts"
        onclick={handleLoadData}>
    </lightning-button>

    <template if:true={accounts}>
        <template for:each={accounts} for:item="account">
            <p key={account.Id}>
                {account.Name}
            </p>
        </template>
    </template>
</template>
```

### Key Points

- Apex method is called manually.
- Returns a Promise (`then()` / `catch()`).
- Best for create, update, delete, and user-driven operations.
- Provides complete control over execution timing.

---

#  GET data Using @wire (Recommended for Read Operations)

## When to Use

- For read-only operations.
- Automatically retrieves data.
- Supports client-side caching.
- Reactive to parameter changes.

### Apex Class

```apex
public with sharing class AccountController {
    @AuraEnabled(cacheable=true)
    public static List<Account> getAccounts() {
        return [
            SELECT Id, Name, Industry
            FROM Account
            LIMIT 10
        ];
    }
}
```

### LWC JavaScript

```javascript
import { LightningElement, wire } from 'lwc';
import getAccounts from '@salesforce/apex/AccountController.getAccounts';

export default class AccountListWire extends LightningElement {

    @wire(getAccounts)
    accounts;
}
```

### LWC HTML

```html
<template>
    <template if:true={accounts.data}>
        <template for:each={accounts.data} for:item="account">
            <p key={account.Id}>
                {account.Name}
            </p>
        </template>
    </template>

    <template if:true={accounts.error}>
        <p>Error loading accounts.</p>
    </template>
</template>
```

### Key Points

- Automatically calls Apex.
- Requires `@AuraEnabled(cacheable=true)` for read operations.
- Supports reactive parameters.
- Provides better performance through caching.
- Recommended for displaying data on page load.

---

# Imperative vs @wire

| Feature | Imperative Call | @wire |
|----------|----------------|--------|
| Execution | Manual | Automatic |
| Use Case | User Action (Button Click) | Read-Only Data |
| Caching | Optional | Supported |
| Return Type | Promise | Property/Function |
| Supports DML | ✅ Yes | ❌ No |
| Reactive Parameters | Manual Handling | Automatic |
| Recommended For | Create, Update, Delete | Fetching Data |

## Interview Answer

**Use Imperative Apex** when you need explicit control over execution, such as button clicks, form submissions, or DML operations.

**Use @wire** for read-only operations because it automatically fetches data, supports caching, and reacts to parameter changes, resulting in better performance and simpler code.


