## Record Level Security in Salesforce

### 1. Organization-Wide Defaults (OWD)

Organization-Wide Defaults (OWD) in Salesforce is the baseline security setting that defines the default level of access users have to records they do not own. It is the first step in the Salesforce record-level security model.

OWD helps control whether users can view, edit, or access records owned by other users. Based on business requirements,

**OWD can be configured**
 
 - **Private -** Users can access only records they own.
 - **Public Read Only -** Users can view all records but can edit only their own records.
 - **Public Read/Write -** Users can view and edit all records.
 - **Controlled by Parent -** Child record access is inherited from the parent records.


### 2. Role and Role Hierarchy

 - **Role :**

   A Role in Salesforce controls record-level access based on an organization's hierarchy. Roles determine who can see whose records, regardless of object permissions.

   Roles control record visibility, while Profiles and Permission Sets control object-level and field-level permissions.

 - **Role Hierarchy :**

   Role Hierarchy is a mechanism that grants users higher in the hierarchy access to records owned by users below them.

   It mirrors an organization's reporting structure. A role hierarchy automatically grants users at higher roles access to records owned by users in lower roles.

### 3. Sharing Rules  
  
  - **Owner-Based Sharing Rules**
    
  - **Criteria-Based Sharing Rules**


### 4. Manual Sharing

