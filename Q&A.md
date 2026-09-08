<details><summary><h3><mark> 1. Different pricing for different accounts. </mark></h3></summary>
  On a custom LWC page, I would use Salesforce Commerce Storefront APIs or Connect API product search APIs instead of querying Product2 directly. These APIs automatically filter products based on buyer groups, entitlement policies, catalog assignments, and pricing rules, ensuring that only products entitled to the logged-in buyer are displayed.

  - Option 1: Use Storefront APIs

    If custom LWC is running in a B2B storefront, call the Commerce Storefront API. The response already contains only the products the logged-in buyer is entitled to see.
    

</details>

<details><summary><h3><mark> 2. How would you display only entitled products on a custom LWC page? </mark></h3></summary>
  In Salesforce B2B Commerce, the recommended approach is to use the Commerce APIs (Storefront APIs / Connect APIs) rather than querying Product2 directly. These APIs automatically apply the buyer's entitlements, buyer groups, catalog visibility, and pricing rules.
</details>


4. A customer says some products are missing from the storefront although they exist in Salesforce.
5. Users can add products to cart but order placement fails during checkout. What would you do?
6. A user says they cannot see an Account record. How do you troubleshoot?
7. Validation Rule Not Working
8. A flow is active but not working
