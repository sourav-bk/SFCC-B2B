# Salesforce B2B Commerce Object Model and Relationships

## Core B2B Commerce Object Model

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

---

# Important Objects and Relationships

## 1. Account

Represents a business customer organization.

### Relationships
- Account → Contact (1:M)
- Account → Buyer Group (M:M)
- Account → Cart (1:M)
- Account → Order (1:M)

### Interview Point
In B2B Commerce, the Account is the primary customer entity. Multiple users (Contacts) can purchase on behalf of the same Account.

---

## 2. Contact

Represents an individual buyer working for a customer account.

### Relationship

```text
Account
   │
   └── Contact
```

Contacts can be enabled as Buyer Users to access the storefront.

---

## 3. Buyer Group

Buyer Groups are used to segment customers and control purchasing experiences.

### Controls
- Catalog Access
- Product Visibility
- Promotions
- Pricing Rules

```text
Buyer Group
    │
    ├── Catalog
    ├── Price Book
    └── Entitlement Policy
```

### Interview Point
Buyer Groups allow businesses to provide different products and pricing to different customer segments.

---

## 4. Product2

Stores product information.

### Common Fields
- Product Name
- Product Code (SKU)
- Description
- Images
- Status

### Relationship

```text
Product2
    │
    └── Product Category
```

---

## 5. Product Category

Used to organize products into a catalog hierarchy.

### Example

```text
Electronics
 ├── Laptop
 ├── Mobile
 └── Tablet
```

### Benefits
- Easy Navigation
- Better Search Experience
- Catalog Management

---

## 6. Price Book and PricebookEntry

### Price Book
Stores a collection of product pricing.

### PricebookEntry
Stores price details for individual products.

### Relationship

```text
Price Book
    │
    ├── Product A → $100
    ├── Product B → $200
    └── Product C → $300
```

### Interview Point
Different customers can have different negotiated pricing through separate Price Books.

---

## 7. Entitlement Policy

Controls which products a customer can view and purchase.

### Controls
- Product Access
- Catalog Access
- Purchasing Rights

```text
Buyer Group
      │
      └── Entitlement Policy
                │
                └── Product Visibility
```

### Interview Point
Entitlements ensure that customers only see products they are authorized to purchase.

---

## 8. Cart

A temporary container used before checkout.

### Relationship

```text
Cart
   │
   └── Cart Item
          │
          └── Product2
```

### Stores
- Product
- Quantity
- Price
- Discount

### Features
- Bulk Ordering
- Saved Cart
- Reordering

---

## 9. Order

Created after successful checkout.

### Relationship

```text
Order
   │
   └── Order Item
           │
           └── Product2
```

### Stores
- Customer Information
- Shipping Details
- Billing Details
- Total Amount
- Order Status

### Interview Point
Orders are often integrated with ERP systems such as SAP and Oracle for fulfillment.

---

# Product Pricing Flow

```text
Product2
    │
    ▼
PricebookEntry
    │
    ▼
Price Book
    │
    ▼
Buyer Group
    │
    ▼
Account
```

### Explanation

1. Product information is stored in Product2.
2. Product pricing is stored in PricebookEntry.
3. Products are associated with a Price Book.
4. Price Books are assigned to Buyer Groups.
5. Buyer Groups are associated with Accounts.
6. Customers see negotiated pricing based on their Account access.

---

# End-to-End Purchasing Flow

```text
Account
   ↓
Contact
   ↓
Buyer Group
   ↓
Entitlement
   ↓
Catalog
   ↓
Product2
   ↓
Price Book
   ↓
Cart
   ↓
Checkout
   ↓
Order
```

---

# Frequently Asked Interview Question

## Explain the Salesforce B2B Commerce Object Model

**Answer:**

Salesforce B2B Commerce is built around Accounts, Contacts, Buyer Groups, Products, Price Books, Entitlements, Carts, and Orders. Accounts represent business customers, Contacts represent buyers, Buyer Groups control access to catalogs and pricing, Product2 stores product data, Price Books manage negotiated pricing, Entitlements determine product visibility, Carts hold items before checkout, and Orders are created after successful purchase. Together these objects provide a personalized B2B purchasing experience integrated with Salesforce CRM.

---

# Quick Revision Summary

| Object | Purpose |
|----------|----------|
| Account | Business Customer |
| Contact | Buyer/User |
| Buyer Group | Customer Segmentation |
| Entitlement | Product Access Control |
| Product2 | Product Information |
| Category | Product Organization |
| Price Book | Pricing Structure |
| PricebookEntry | Product Price |
| Cart | Temporary Shopping Basket |
| Order | Final Purchase Record |

---

# Interview Shortcut

Remember this sequence:

```text
Account
   ↓
Buyer Group
   ↓
Entitlement
   ↓
Catalog
   ↓
Product2
   ↓
Price Book
   ↓
Cart
   ↓
Order
```

This flow explains the complete Salesforce B2B Commerce Object Model in less than one minute during interviews.
