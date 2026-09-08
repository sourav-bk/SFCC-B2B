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

In LWC lifecycle, first constructor() is called when the component is created. Then connectedCallback() runs when it is inserted into the DOM. After the UI is displayed, renderedCallback() executes. Whenever data changes, renderedCallback() can run again. When the component is removed from the page, disconnectedCallback() is called. For handling errors from child components, we use errorCallback()

- #### 1. constructor() ::
  constructor() is the first lifecycle hook that runs when the component instance is created. It is mainly used for initialization.
  - **When?** Called first when the component is created.
  - **Use for**
    - Initialize variables.
    - Basic setup. 
  
- #### 2. connectedCallback() ::
- #### 3. renderedCallback() ::
- #### 4. disconnectedCallback() ::
- #### 5. errorCallback() :: 
        
</details>
