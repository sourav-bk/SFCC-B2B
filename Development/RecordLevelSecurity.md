## Record Level Security in Salesforce

### 1. Organization-Wide Defaults (OWD)
Organization-Wide Defaults (OWD) in Salesforce is the baseline security setting that defines the default level of access users have to records they do not own. It is the first step in the Salesforce record-level security model.

OWD helps control whether users can view, edit, or access records owned by other users. Based on business requirements,

**OWD can be configured **
 
 - **Private -** Users can access only records they own.
 - **Public Read Only -** Users can view all records but can edit only their own records.
 - **Public Read/Write -** Users can view and edit all records.
 - **Controlled by Parent -** Child record access is inherited from the parent recor


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

