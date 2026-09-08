### LWC
LWC (Lightning Web Components) is a modern Salesforce framework used to build fast and reusable user interface components. It is based on standard web technologies like HTML, JavaScript, and CSS and follows web standards, making applications more efficient and easier to develop.

**Structure**

        myComponent/
        ├── myComponent.html      ← Template (UI markup)
        ├── myComponent.js        ← JavaScript Controller (Logic)
        ├── myComponent.css       ← Styles (Scoped via Shadow DOM)
        ├── myComponent.js-meta.xml ← Metadata Configuration
        ├── myComponent.svg       ← (Optional) Custom icon
        ├── __tests__/            ← (Optional) Jest unit tests



### Why use LWC?

 - Better performance than Aura Components.
 - Reusable components.
 - Easy to develop and maintain.
 - Uses standard web technologies.
 - Supported by Salesforce Lightning Experience and Experience Cloud




<details><summary><h3><mark>LWC Lifecycle Hooks</mark></h3></summary>
Lightning Web Components (LWC) lifecycle hooks are special, pre-defined JavaScript methods that Salesforce calls automatically at specific stages of a component's existence — from creation to deletion.
<hr>

In LWC lifecycle, first constructor() is called when the component is created. Then connectedCallback() runs when it is inserted into the DOM. After the UI is displayed, renderedCallback() executes. Whenever data changes, renderedCallback() can run again. When the component is removed from the page, disconnectedCallback() is called. For handling errors from child components, we use errorCallback().

- #### 1. constructor() ::
  constructor() is the first lifecycle hook that runs when the component instance is created. It is mainly used for initialization.
  - **When?** Called first when the component is created.
  - **Use for**
    - Initialize variables.
    - Basic setup. 
  
- #### 2. connectedCallback() ::
  connectedCallback() executes when the component is added to the page. It is commonly used to load data from Apex or perform setup operations.
  
  - **When?** Called when the component is inserted into the DOM (page).
  - **Use for**
    - Call Apex methods.
    - Fetch data from APIs.
    - Initialize data.
      
- #### 3. renderedCallback() ::
  renderedCallback() runs after the component UI is rendered on the screen and is used when we need access to DOM elements.
  
  - **When?** Called after the HTML is rendered. Runs every time the component rerenders.
  - **Use for**
    - DOM manipulation.
    - Third-party library initialization.
      
- #### 4. disconnectedCallback() ::
  disconnectedCallback() executes when the component is removed from the DOM and is used for cleanup activities.
  
  - **When?** Called when the component is removed from the page.
  - **Use for**
    - Cleanup operations.
    - Remove event listeners.
    - Clear timers.
      
- #### 5. errorCallback() ::
  errorCallback() catches errors from child components and helps in implementing custom error handling.
  
  - **When?** Called when an error occurs in a child component.
  - **Use for**
    - Error handling.
    - Logging.
        
</details>

<details><summary><h3><mark>LWC annotations/decorators- @api, @wire, @track </mark></h3></summary>
        
 Decorators are SPECIAL ANNOTATIONS that modify the behavior of the property or function in a LWC.
 The 3 primary decorators have in LWC - @api, @wire, and @track.

 - #### @api :-
   Used to expose a property or method as public, allowing parent components to interact with child components.
   - **Use Cases :**
     - Parent-to-child communication.
     - Exposing configurable properties
     - Exposing methods that parents can call
   
 - #### @wire :-
   Used to connect a component to Salesforce data sources such as **1. Apex methods**, **2. Lightning Data Service adapters**, **3. UI API services**
   - **Use Cases :**
     - Retrieve Salesforce records
     - Call cacheable Apex methods
     - Automatically refresh UI when data changes
       
UI API services
   
 - #### @track :-
   Historically used to make private properties re-active. Since Spring '20, most primitive fields are re-active by default, so @track is rarely required. It is mainly used when we need to observe changes within complex objects or arrays.
   
   - **Use Cases :**
     - Deep tracking of object property changes.
     - Tracking array element modifications.
     - Legacy LWC codebases

**@api →** Makes a property or method public and accessible to parent components.
**@wire →** Retrieves Salesforce data reactively from Apex or UI APIs.
**@track →** Used for observing changes inside complex objects and arrays; mostly un-necessary for primitive fields in modern LWC.

</details>



<details><summary><h3><mark>Parent-to-Child and Child-to-Parent Communication</mark></h3></summary>

 #### 1. Parent → Child Communication :
 
  Parent-to-child communication in Lightning Web Components (LWC) is achieved by passing data down through public properties or invoking public methods exposed by the child.
  
  **Main Approaches**
   - Public Properties (@api) -

     @api decorator in the child's JavaScript file to make it public. The parent passes data by binding an attribute to the child's tag in the parent's HTML template.
     
   - Public Methods  (@api function) -

     Define a function with the @api decorator inside the child component. The parent uses this.template.querySelector('c-child-tag').methodName(data) to call it directly.
     
   - Getters and Setters -

     Use JavaScript getter and setter blocks on an @api property in the child component to intercept and process data whenever the parent updates it.
 
 #### 2. Child → Parent Communication :
 
 
  Child to parent communication in Lightning Web Components (LWC) is achieved using custom events. The child dispatches an event and the parent listens for it.
  
  **Steps for Child-to-Parent Communication**
  
  - Create the Event:

    The child component uses the CustomEvent() constructor to build an event and optionally attach data using the detail property.
  
  - Dispatch the Event:

    The child calls this.dispatchEvent(myEvent) to send the signal upward.
  
  - Listen for the Event:

    The parent component listens for this custom event in its HTML template by adding an on prefix to the event name (onEventName).
  
  - Handle the Event:

    The parent runs a handler method in its JavaScript file to process the incoming data stored in event.detail
  
        
</details>







<details><summary><h3><mark> GET data from Apex to LWC  </mark></h3></summary>
  
## LWC Data Fetching from Apex

  <details><summary><h3><mark> GET data from Apex to LWC (Imperative Call) </mark></h3></summary>
  ### When to Use
- When data retrieval is triggered by a user action (button click).
- When you need more control over when the Apex method is executed.
- Supports both cacheable and non-cacheable Apex methods.

#### Apex Class

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

#### LWC JavaScript

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

#### LWC HTML

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

#### Key Points

- Apex method is called manually.
- Returns a Promise (`then()` / `catch()`).
- Best for create, update, delete, and user-driven operations.
- Provides complete control over execution timing.

---

  
  </details>
  <details><summary><h3><mark>  GET data Using @wire (Recommended for Read Operations) </mark></h3></summary>

  #  GET data Using @wire (Recommended for Read Operations)

### When to Use

- For read-only operations.
- Automatically retrieves data.
- Supports client-side caching.
- Reactive to parameter changes.

#### Apex Class

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

#### LWC JavaScript

```javascript
import { LightningElement, wire } from 'lwc';
import getAccounts from '@salesforce/apex/AccountController.getAccounts';

export default class AccountListWire extends LightningElement {

    @wire(getAccounts)
    accounts;
}
```

#### LWC HTML

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

  

  
#### Key Points

- Automatically calls Apex.
- Requires `@AuraEnabled(cacheable=true)` for read operations.
- Supports reactive parameters.
- Provides better performance through caching.
- Recommended for displaying data on page load.

---

## Imperative vs @wire

| Feature | Imperative Call | @wire |
|----------|----------------|--------|
| Execution | Manual | Automatic |
| Use Case | User Action (Button Click) | Read-Only Data |
| Caching | Optional | Supported |
| Return Type | Promise | Property/Function |
| Supports DML | ✅ Yes | ❌ No |
| Reactive Parameters | Manual Handling | Automatic |
| Recommended For | Create, Update, Delete | Fetching Data |

### Interview Answer

**Use Imperative Apex** when you need explicit control over execution, such as button clicks, form submissions, or DML operations.

**Use @wire** for read-only operations because it automatically fetches data, supports caching, and reacts to parameter changes, resulting in better performance and simpler code.

</details>




<details><summary><h3><mark> Send data from LWC to Apex </mark></h3></summary>
## Pass Data from LWC to Apex

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
