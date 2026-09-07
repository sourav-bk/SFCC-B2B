## What is apex
Apex is Salesforce’s strongly typed, Oops language designed to add custom logic to system events like button clicks, record updates, and web service requests. It features a syntax similar to Java and acts much like database stored procedures.


## Main Apex Components:

 ### 1. Apex Classes -
 ### 2. Apex Triggers -
  Apex Trigger is a piece of Apex code that executes automatically before or after events occur on Salesforce records, such as insert, update, delete, or undelete.
  
  **Key Points:**
  
  - Runs automatically when record data changes.
  - Can execute before or after DML events.
  - Used for validation, automation, and business logic.
  - Supports events: before insert, before update, after insert, after update, before delete, after delete, and after undelete.
  
  **Types of Triggers::**
   
   - Before Triggers: Used to update or validate record values before they save to the database.
   - After Triggers: Used to access system-set field values and affect changes on related or other records.

  **Governor Limits ::**
   - 100 SOQL queries per synchronous transaction.
   - 150 DML statements per transaction.
   - 50,000 records retrieved by SOQL
  
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
       - Max queueable jobs per 24 hours -> 2,50,000 or (number of licenses × 200).
       
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
    Batch Apex is a Salesforce feature used to process large volumes of records asynchronously in smaller batches, helping to avoid governor limit issues

     <details><summary>+</summary>
     
     - **Features ::**
       - Implements Database.Batchable<sObject> interface.
         - it have 3 mandatory methods:
           - start() – collects records (returns Database.QueryLocator or Iterable<sObject>)
           - execute() – processes each batch/chunk
           - finish() – post-processing (send emails, chain jobs)
       - Records are processed in chunks (batches)
       - Returns a Job ID for monitoring.
       - Separate governor limits for each batch execution.
         
     - **Benefits and Best Used For ::**
       - Can process huge datasets up to 50 million records using Database.QueryLocator
       - Governor limits reset per batch chunk.
       - Ideal for scheduled data maintenance jobs.
     - **Governor Limits ::**
       - Max records returned by Database.QueryLocator 50 million
       - Max records returned by Iterable 50,000
       - Max batch size 2,000
       - SOQL queries limit -> 200
       - Max batch executions per 24 hours -> 2,50,000 
     - **Example ::**
    
    </details>
    
    
    ### 4. Scheduled Apex :-
    Scheduled Apex allows we to execute Apex classes automatically at a specified time or recurring interval without manual intervention. link corn job.

     <details><summary>+</summary>
     
     - **Features ::**
       - Must Implements the Schedulable interface and execute method.
       - Uses CRON expressions to define schedule.
       - Can be scheduled via Apex code or Salesforce UI (Setup → Apex Classes → Schedule Apex)
       - Returns a Job ID (CronTrigger ID)
         
     - **Benefits and Best Used For ::**
       - Recurring jobs that need to run at specific times (daily, weekly, monthly) to Eliminates manual intervention.
       - Can be monitored via CronTrigger and CronJobDetail objects.
       - Supports complex schedules via CRON expressions
      
     - **Governor Limits ::**
       - Maximum 100 scheduled jobs per org
       - SOQL queries limit -> 200
       - DML statements limit -> 150
      
     - **Example ::**
    
    </details>
    


