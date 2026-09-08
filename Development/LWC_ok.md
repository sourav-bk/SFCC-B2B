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
