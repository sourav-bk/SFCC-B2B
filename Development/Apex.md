## What is apex
Apex is Salesforce’s strongly typed, Oops language designed to add custom logic to system events like button clicks, record updates, and web service requests. It features a syntax similar to Java and acts much like database stored procedures.


## Main Apex Components:

 ### 1. Apex Classes -
 ### 2. Apex Triggers -
 ### 3. Apex Interfaces -


## Execution Types (Synchronous vs. Asynchronous)

  - **Synchronous ::** Runs immediately in real-time when triggered by a user action, UI click, or standard transaction, blocking the user until it completes.
  - **Asynchronous ::** Runs in the background on the server when system resources are free. It handles large data volumes or long-running tasks using tools like **Future methods**, **Queueable Apex**, **Batch Apex** or **Scheduled Apex** .

    ### 1. Future Methods (@future) :-
    A Future method allows a task to run asynchronously and provides a way to get the result once the task completes.

    <details><summary>+</summary>
     
     - **Features ::**
       - Runs asynchronously in a separate thread.
       - Must be static and return void
       - Parameters must be primitive data types only (no sObjects)
       - Defined using @future annotation
       - Using @future(callout=true) to make HTTP call
       - Cannot be called from another future or batch method.
     - **Benefits and Best Used For ::**
       - Improves user experience by moving heavy processing to the background
       - Suitable for simple one-time asynchronous tasks.
       - Helps avoid mixed DML errors.
     - **Benefits ::**
     - **Governor Limits ::**
       - Maximum 50 future calls per transaction
       - Up to 250,000 future method executions per 24 hours (or licenses × 200, whichever is greater)
       - Cannot call another future method.
       - No job chaining support
     - **Example ::**
       ```apex
       public class FutureExample {

       @future(callout=true)
       public static void sendData(String accountName) {
           HttpRequest req = new HttpRequest();
           req.setEndpoint('https://api.example.com');
           req.setMethod('POST');

           Http http = new Http();
           HttpResponse res = http.send(req);
           }
       }
       ```
    
    </details>
     
     
    
    
    ### 2. Queueable Apex :-

     <details><summary>+</summary>
     
     - **Features ::**
       - Its Runs asynchronously in a separate thread.
       - Must be static and return void
     - **Best Used For ::**
     - **Benefits ::**
     - **Governor Limits ::**
     - **Example ::**
    
    </details>
    
    
    ### 3. Batch Apex :-

     <details><summary>+</summary>
     
     - **Features ::**
     - **Best Used For ::**
     - **Benefits ::**
     - **Governor Limits ::**
     - **Example ::**
    
    </details>
    
    
    ### 4. Scheduled Apex :-

     <details><summary>+</summary>
     
     - **Features ::**
     - **Best Used For ::**
     - **Benefits ::**
     - **Governor Limits ::**
     - **Example ::**
    
    </details>
    


