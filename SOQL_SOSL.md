SOQL (Salesforce Object Query Language) and SOSL (Salesforce Object Search Language) are the two languages used to retrieve data from the Salesforce database

<details><summary><h3><mark> SOQL (Salesforce Object Query Language) </mark></h3></summary>
  SOQL is like a standard SQL SELECT statement. we use it to query one object or related objects at a time when we know exactly where the data lives.
  
  - **Best for :** Targeted, structured data retrieval.
  - **Key Features :**
  - **Governor Limits :**  Up to 100 synchronous queries per transaction; returns a maximum of 50,000 rows.
  - **Example :**
    ```sql
      SELECT Id, Name FROM Account WHERE Industry = 'Banking'
    ```

  Targeted, structured data retrieval.
</details>

<details><summary><h3><mark> SOSL (Salesforce Object Search Language) </mark></h3></summary>
  SOSL is a text-based search language. we use it to search for a specific term or keyword across multiple objects and fields at the same time.
  
   - **Best for :** Quick keyword searches when we do not know which object or field contains the data.
     
   - **Key Features :**
   - **Governor Limits :** Up to 20 queries per transaction; returns up to 2,000 records per object.
   - **Example :**
     ```sql
       FIND 'Sales*' RETURNING Account(Id, Name), Contact(Id, Name)
     ```
</details>
