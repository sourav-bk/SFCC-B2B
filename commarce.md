## B2B Commerce :
Salesforce B2B Commerce is an eCommerce solution built on Salesforce for businesses selling products to other businesses. It supports catalogs, pricing, buyer groups, checkout, orders, and account-based purchasing.

<img width="801" height="601" alt="image" src="https://github.com/user-attachments/assets/e95af64a-a94d-416d-8c51-2f4624d9a583" />

<img width="572" height="756" alt="image" src="https://github.com/user-attachments/assets/dedf226d-ff8d-440f-b775-926d1e3d6f04" />
<img width="562" height="332" alt="image" src="https://github.com/user-attachments/assets/dbbb2413-8105-464f-8376-152991098f36" />



### 1. Initial System Configuration ::
   
- **Enable Digital Experiences-** Navigate to Setup, search for Digital Experiences, and enable it.
- **Enable Commerce-** Search for Commerce in the Setup menu and enable the feature to gain access to necessary objects and workspaces.

### 2. Storefront Creation::

- **Create a Site-** In Digital Experiences, select New and choose the B2B Commerce LWR template to create your store.
- **Activate the Site-** Go to the Administration settings of your newly created site and click Activate, then Publish the site to make changes live.

### 3. Security and User Access ::

- **Sharing Settings-** Update organization-wide defaults (OWD) for objects like Buyer Groups, Catalogs, and Entitlement Policies to ensure proper external access 

- **Profile Setup-** Clone a profile (e.g., Customer Community Plus Login User) and grant necessary permissions for objects like Carts, Categories, and Wishlists.

- **Assign Members-** Add your created profile to the site's members list in the Experience Builder .

### 4. Buyer Setup ::

- **Account Configuration-** Enable your Account as a Buyer by updating the page layout to include necessary buttons and related lists.

- **User Enabling-** Create a Contact for the account, then enable them as a Customer User. Ensure the account owner has a Role assigned in the system, or user creation will fail.

- **Permissions-** Assign the Buyer permission set to your user and link the account to a Buyer Group .

### 5. Store Data Setup :: 

- **Manage Content-** Use the CMS Workspace to import and publish images/banners .

- **Product Import-** Use the Product Workspace to import your products via CSV . Ensure you create and link necessary Price Books.

- **Finalize-** Manually activate products and price book entries using code or the UI and Rebuild the Search Index to ensure all products appear on the storefront.
