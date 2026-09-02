### Salesforce:
Salesforce is a cloud-based Customer Relationship Management (CRM) platform that helps businesses manage their customers, sales processes, marketing activities, customer service, and business operations from a single system.

##B2B Commerce :
Salesforce B2B Commerce is an eCommerce solution built on Salesforce for businesses selling products to other businesses. It supports catalogs, pricing, buyer groups, checkout, orders, and account-based purchasing.

<img width="801" height="601" alt="image" src="https://github.com/user-attachments/assets/e95af64a-a94d-416d-8c51-2f4624d9a583" />

+--------------------------------------------------+
|                  Buyer/User                      |
+------------------+-------------------------------+
                   |
                   v
+--------------------------------------------------+
|          Storefront (Experience Cloud)           |
|            LWR + Standard Commerce UI            |
|                  Custom LWC                       |
+--------------------------------------------------+
                   |
                   v
+--------------------------------------------------+
|              Commerce APIs / Services            |
|                                                  |
|  Product API     Cart API     Checkout API       |
|  Pricing API     Order API    Search API         |
+--------------------------------------------------+
                   |
                   v
+--------------------------------------------------+
|            Salesforce Core Platform              |
|                                                  |
| Product2                                          |
| Price Books                                       |
| Buyer Groups                                      |
| Cart & Order Objects                              |
| Accounts & Contacts                               |
| Entitlements                                      |
+--------------------------------------------------+
                   |
                   v
+--------------------------------------------------+
|      Customization Layer (Apex & Flows)          |
|                                                  |
| Triggers | Apex Classes | Batch | Queueable      |
| Platform Events | Flows | Integrations           |
+--------------------------------------------------+
                   |
                   v
+--------------------------------------------------+
|           External Systems (ERP/PIM/WMS)         |
|                                                  |
| SAP | Oracle | NetSuite | Inventory Systems      |
+--------------------------------------------------+

