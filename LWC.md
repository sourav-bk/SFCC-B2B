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

