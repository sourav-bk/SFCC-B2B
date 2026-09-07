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
     
     - **Governor Limits ::**
       - Maximum 50 future calls per transaction
       - Up to 250,000 future method executions per 24 hours (or licenses × 200, whichever is greater)
       - Cannot call another future method.
       - No job chaining support.
       - SOQL queries limit -> 200
       - DML statements limit -> 150
       - Max future calls per 24 hours -> 2,50,000 or (number of licenses × 200) , whichever is greater.
         
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
    Queueable Apex is an asynchronous Apex feature that allows we to run jobs in the background and process complex operations without affecting the user experience.

     <details><summary>+</summary>
     
     - **Features ::**
       - Implements Queueable interface and execute(QueueableContext context) method
       - Supports complex data types (SObjects, custom objects)
       - Returns a Job ID via System.enqueueJob() for monitoring
       - Supports job chaining
         
     - **Benefits and Best Used For ::**
       - More flexible than future methods
       - Complex asynchronous processing
       - Chaining multiple async jobs sequentially.
       - Easier debugging and monitoring using Job ID.
         
     - **Governor Limits ::**
       - Up to 50 Queueable jobs can be added per transaction.
       - Only 1 child Queueable job can be chained from a running Queueable.
       - SOQL queries limit -> 200
       - DML statements limit -> 150
       - Max future calls per 24 hours -> 2,50,000 or (number of licenses × 200) , whichever is greater.
       
     - **Example ::**
       ```
       public class QueueableExample implements Queueable, Database.AllowsCallouts {
    
              private List<Account> accounts;

              public QueueableExample(List<Account> accounts) {
                   this.accounts = accounts;
              }

              public void execute(QueueableContext context) {
                   List<Account> toUpdate = new List<Account>();

                   for (Account acc : accounts) {
                       acc.Description = 'Processed by Queueable Job';
                       toUpdate.add(acc);
                   }

              update toUpdate;

              // Chaining: Enqueue next job
              if (!Test.isRunningTest()) {
                   System.enqueueJob(new AnotherQueueableJob());
                }
             }
        }

        // How to call:
        // Id jobId = System.enqueueJob(new QueueableExample(accountList));
        // System.debug('Job ID: ' + jobId);

       ```
    
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
    


