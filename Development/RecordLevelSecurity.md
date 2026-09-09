## Record Level Security in Salesforce

### 1. Organization-Wide Defaults (OWD)
Organization-Wide Defaults (OWD) in Salesforce set the baseline, record-level default access for users who do not own a record.

it have 4 Core Access Levels
 
 - Private :

   Only the record owner and users above them in the role hierarchy can access the record.
   
 - Public Read-Only :
  
   All users can view the record, but only the owner and superiors can edit it.
   
 - Public Read/Write :

   All users can view, modify, and edit all records.
   
 - Controlled by Parent :

   Access to a detail record is inherited directly from the parent record in a master-detail relationship

### 2. Role and Role Hierarchy

### 3. Sharing Rules  
  
  - **Owner-Based Sharing Rules**
    
  - **Criteria-Based Sharing Rules**


### 4. Manual Sharing

