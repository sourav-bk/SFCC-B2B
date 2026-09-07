## Salesforce Governor Limits?

Salesforce Governor Limits are restrictions enforced by Salesforce to ensure that no single user or process consumes excessive shared resources in the multi-tenant environment. These limits help maintain system performance and stability for all customers.

## Why are Governor Limits Important?
Since Salesforce is a multi-tenant platform, multiple organizations share the same infrastructure. Governor Limits prevent one organization's code from affecting others.

## Common Governor Limits in Apex?
  
  - **OQL Queries:** Maximum 100 synchronous queries per transaction.
  - **DML Statements:** Maximum 150 DML operations per transaction.
  - **Records Retrieved by SOQL:** Up to 50,000 records.
  - **CPU Time Limit:** Limited execution time per transaction.
  - **Heap Size:** Limited memory usage for Apex code.
  - **Callouts:** Maximum 100 HTTP/Web Service callouts per transaction.
