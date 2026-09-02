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
