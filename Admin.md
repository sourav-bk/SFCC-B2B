### Salesforce Data Security::

Salesforce Data Security is a multi-layered framework that controls who can see what data and what they can do with it within a Salesforce organization.

<img width="857" height="668" alt="image" src="https://github.com/user-attachments/assets/07162b86-2244-46b5-b55b-5edfdc919345" />

---

### LAYER 1: ORGANIZATION-LEVEL SECURITY  | 
<img width="365" height="612" alt="image" src="https://github.com/user-attachments/assets/0eab0bd2-cebb-4568-a53b-18380e499caf" />


### LAYER 2: OBJECT-LEVEL SECURITY  |- Profiles | - Permission Sets |  Permission Set Groups
- **Profiles::** 

A Profile defines the baseline permissions and settings for a user, and every user must have exactly one profile. 

- **Permission**

A Permission Set is used to grant additional permissions without modifying the profile, and a user can have multiple permission sets assigned. Salesforce recommends using profiles for minimum access and permission sets for extra access.

-  **Permission Set Groups**

Bundles of Permission Sets managed as a single unit.

<img width="546" height="490" alt="image" src="https://github.com/user-attachments/assets/89c37054-0a21-4fb4-8ada-3db083b8d0f3" />



### LAYER 3: FIELD-LEVEL SECURITY  
<img width="465" height="257" alt="image" src="https://github.com/user-attachments/assets/2e9b90a1-8c89-417b-b4b3-a19abaf67b0e" />





### LAYER 4: RECORD-LEVEL SECURITY
<img width="446" height="347" alt="image" src="https://github.com/user-attachments/assets/6f8e5a0f-d996-412d-8ea0-4b8ca42a4af4" />




Licence -> profile -> user 

permission set ().

Roles, Sharing Rules, and access management scenarios.



# User Management ::
User <- Roles <- Profiles <- permission sets

Licence
- Licence lype 

# Object level Security ::

- profile
- permission set | permission set groups  | public groups


# Field-Level Security (FLS)

# Record level Security ::

- OWD/ Sharing settings
- Role and Role Hierarchy
- Sharing rules / data access | - criteria based - Owner Based sharing rules - Manual Sharing.


# Difference between Queue and Public Group in Salesforce.

# Data_loader
