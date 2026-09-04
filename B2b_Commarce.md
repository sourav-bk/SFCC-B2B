## <mark>SF B2B Commerce ::</mark>
Salesforce B2B Commerce is an eCommerce solution built on Salesforce for businesses selling products to other businesses. It supports catalogs, pricing, buyer groups, checkout, orders, and account-based purchasing.
<img width="650" alt="image" src="https://github.com/user-attachments/assets/e95af64a-a94d-416d-8c51-2f4624d9a583" />

<ins><mark>SF B2B Commerce Architecture ::</mark></ins>

Salesforce B2B Commerce Architecture as the complete journey of how a business customer logs in, sees products, gets their negotiated pricing, places an order, and how Salesforce communicates with ERP, inventory, tax, and payment systems.

 - ### Components:
  - Salesforce B2B Commerce is built on Experience Cloud and the Salesforce platform.
  - The storefront allows business customers to browse products, manage carts, and place orders.
  - Product catalogs, buyer groups, entitlements, and price books control product visibility and account-specific pricing.
  - Orders are stored in Salesforce and integrated with ERP, payment, tax, and shipping systems through APIs or MuleSoft. The architecture provides a unified commerce and CRM experience on a single platform.
  
  <img width="700" alt="image" src="https://github.com/user-attachments/assets/022f2de9-7b90-45a3-96ba-cc2c4d427279" />
  
  ### Core Component -
  
  - **1. Storefront (Experience Cloud) :**
    - Customer-facing website.
    - Built using Experience Builder and Lightning Web Components (LWC).
    - Provides product search, cart, checkout, and account management.
      
  - **2. Product Catalog :**
    - Stores products using the Product2 object.
    - Supports categories, product images, and variations.
    - Displays products based on customer entitlements.
      
  - **3. Pricing & Price Books :**
    - Uses Salesforce Price Books.
    - Different customers can have different negotiated prices.
    - Supports discounts and contract pricing.
      
  - **4. Buyer Groups & Entitlements :**
    - Buyer Groups control which products and catalogs a customer can access.
    - Entitlements determine product visibility and pricing.
      
  - **5. Cart and Checkout :**
    - Manages shopping cart functionality.
    - Supports bulk ordering and reordering.
    - Integrates with payment and tax services.
      
  - **6. Order Management :**
    - Creates and tracks orders.
    - Sends order information to ERP systems.
    - Supports order history and status visibility.
      
  - **7. Salesforce Core CRM :**
    - Uses standard objects:
      - Account
      - Contact
      - Product2
      - Order
      - Pricebook
      - PricebookEntry
        Provides a single source of customer data
  
  
   ### <ins>B2B Commerce Object Model and Relationships</ins> 

   ```text
Account
   │
   ├── Contact
   │      │
   │      └── Buyer User
   │
   └── Buyer Group
           │
           ├── Entitlement Policy
           ├── Catalog
           └── Price Book
                    │
                    └── PricebookEntry
                              │
Product2 ─────────────────────┘
   │
   └── Product Category

Account
   │
   └── Cart
          │
          └── Cart Item
                   │
                   └── Product2

Account
   │
   └── Order
           │
           └── Order Item
                    │
                    └── Product2

   ```


Salesforce B2B Commerce is built around Accounts, Contacts, Buyer Groups, Products, Price Books, Entitlements, Carts, and Orders. 

<details><summary><b>Accounts</b> - represent business customers</summary>
 In B2B Commerce, the Account is the primary customer entity. Multiple users (Contacts) can purchase on behalf of the same Account.

 
 **Relationships:**
 
   - Account → Contact (1:M)
   - Account → Buyer Group (M:M)
   - Account → Cart (1:M)
   - Account → Order (1:M)
     
</details>
  
<details><summary><b>Contacts</b> - represent buyers</summary>
 Represents an individual buyer working for a customer account.
 Contacts can be enabled as Buyer Users to access the storefront.

 **Relationship**
 ```text
 Account
    │
    └── Contact
 ```
</details>
  
<details><summary><b>Buyer</b> - Groups control access to catalogs and pricing</summary>
 Buyer Groups are used to segment customers and control purchasing experiences.
 
 **Controls**
- Catalog Access
- Product Visibility
- Promotions
- Pricing Rules
 
</details>
  
<details><summary><b>Product2</b> - stores product data</summary>
</details>
  
<details><summary><b>PriceBooks</b> - manage negotiated pricing</summary>
</details> 
  
<details><summary><b>Entitlements policy</b> - determine product visibility</summary>
</details>
  
<details><summary><b>Carts</b> - hold items before checkout,</summary>
</details>
  
<details><summary><b>Orders</b> - are created after successful purchase.</summary>
</details>

Together these objects provide a personalized B2B purchasing experience integrated with Salesforce CRM.

## <mark>Product ::</mark>


- ### Product Visibility Concepts -
  - Buyer Groups
  - Entitlement Policies
  - Catalogs
  - Categories
  - Price Books
    
- ### Product Visibility Flow -


## <mark>Customer Access Management ::</mark>


## <mark>Security Layers ::</mark>

1. Profile
2. Permission Set
3. Sharing
4. Buyer Group
5. Entitlement Policy

## <mark>Order Flow ::</mark>

## <mark>Checkout Flow ::</mark>

## <mark>Payment Flow::</mark>

