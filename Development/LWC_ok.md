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

- #### constructor() ::
- #### connectedCallback() ::
- #### renderedCallback() ::
- #### disconnectedCallback() ::
- #### errorCallback() :: 
        
</details>
