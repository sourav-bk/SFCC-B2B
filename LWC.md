##  LWC :

Lightning Web Components (LWC) is Salesforce's modern, lightweight UI framework used to build fast, reusable, and scalable custom web components using standard HTML, modern JavaScript (ES6+), and CSS.

- ***Core Anatomy***
  
- HTML : Defines the user interface and structural template.
```html
<template>
    <lightning-card title="Hello World Component">
        <div class="slds-m-around_medium">
            <p>Hello, {greeting}!</p>
            <lightning-input label="Enter Name" value={greeting} onchange={handleChange}></lightning-input>
        </div>
    </lightning-card>
</template>
```

- JavaScript : Manages business logic, user interactions, and event handling.
```js
  import { LightningElement, track } from 'lwc';

export default class HelloWorld extends LightningElement {
    greeting = 'Salesforce Developer';
    handleChange(event) {
        this.greeting = event.target.value;
    }
}
```

- Configuration XML : Sets metadata properties and deployment targets (like record pages or homepages).
```xml
<?xml version="1.0" encoding="UTF-8"?>
<LightningComponentBundle xmlns="http://sforce.com">
    <apiVersion>60.0</apiVersion>
    <isExposed>true</isExposed>
    <targets>
        <target>lightning__RecordPage</target>
        <target>lightning__AppPage</target>
        <target>lightning__HomePage</target>
    </targets>
</LightningComponentBundle>
```

- Style Sheet (css): Contains custom styling.





## LWC Lifecycle Hooks ::

Lifecycle hooks are special JavaScript methods that execute at specific stages of a Lightning Web Component's lifecycle, from creation to removal from the DOM.

# LWC Lifecycle Hooks

| Lifecycle Hook | When It Executes | Purpose | Runs How Many Times? |
|----------------|------------------|----------|----------------------|
| **constructor()** | When the component instance is created | Initialize component state and set default values | Once |
| **connectedCallback()** | When component is inserted into the DOM | Fetch data, subscribe to events, perform initialization | Multiple times (if reinserted) |
| **render()** | Before every render | Conditionally select a template for rendering | Multiple times |
| **renderedCallback()** | After component is rendered in the DOM | Access DOM elements and perform post-render operations | Multiple times |
| **disconnectedCallback()** | When component is removed from the DOM | Cleanup tasks, unsubscribe from events, clear timers | Multiple times |
| **errorCallback(error, stack)** | When a child component throws an error | Handle and log errors gracefully | Whenever an error occurs |





<details><summary><h3><mark> GET data from Apex to LWC  </mark></h3></summary>
  
# LWC Data Fetching from Apex

  <details><summary><h3><mark> GET data from Apex to LWC (Imperative Call) </mark></h3></summary>
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

  
  </details>
  <details><summary><h3><mark>  GET data Using @wire (Recommended for Read Operations) </mark></h3></summary>

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

  </details>

  

  
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

</details>




<details><summary><h3><mark> Send data from LWC to Apex </mark></h3></summary>
  # Pass Data from LWC to Apex

## Overview
This example demonstrates how to pass data from a Lightning Web Component (LWC) to an Apex method.

### Apex Class

```java
public with sharing class AccountController {

    @AuraEnabled
    public static String createAccount(String accName) {

        Account acc = new Account(
            Name = accName
        );

        insert acc;

        return 'Account Created Successfully';
    }
}
```

### LWC JavaScript

```javascript
import { LightningElement } from 'lwc';
import createAccount from '@salesforce/apex/AccountController.createAccount';

export default class AccountDemo extends LightningElement {

    accountName = '';

    handleChange(event) {
        this.accountName = event.target.value;
    }

    handleSave() {
        createAccount({ accName: this.accountName })
            .then(result => {
                console.log(result);
            })
            .catch(error => {
                console.error(error);
            });
    }
}
```

### LWC HTML

```html
<template>
    <lightning-input
        label="Account Name"
        onchange={handleChange}>
    </lightning-input>

    <lightning-button
        label="Save"
        onclick={handleSave}>
    </lightning-button>
</template>
```

## Data Flow

```text
User Input
    ↓
LWC JS
    ↓
Apex Method
    ↓
Database
```

## Key Points

- Use `@AuraEnabled` on Apex methods.
- Import Apex methods using `@salesforce/apex/ClassName.methodName`.
- Pass parameters as a JavaScript object.
- Handle responses with `.then()` and errors with `.catch()`.

</details>
