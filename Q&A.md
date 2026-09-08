<details><summary><h3><mark> 1. Different pricing for different accounts. </mark></h3></summary>
  In Salesforce B2B Commerce, different pricing for different accounts is typically implemented using Buyer Groups and Price Books. Each account is assigned to a Buyer Group, and the Buyer Group is linked to a specific Price Book containing the account-specific product prices. When users log in, B2B Commerce automatically displays the prices from the associated Price Book. For complex negotiated pricing, custom pricing logic or ERP/CPQ integration can be used.
</details>

<details><summary><h3><mark> 2. How would you display only entitled products on a custom LWC page? </mark></h3></summary>
  In a custom LWC page, I would use Salesforce Commerce Storefront APIs or Connect API product search APIs instead of querying Product2 directly. These APIs automatically filter products based on buyer groups, entitlement policies, catalog assignments, and pricing rules, ensuring that only products entitled to the logged-in buyer are displayed.

  - Option 1: Use Storefront APIs
    
    If custom LWC is running in a B2B storefront, call the Commerce Storefront API. The response already contains only the products the logged-in buyer is entitled to see.
    
</details>

<details><summary><h3><mark> 3. A customer says some products are missing from the storefront although they exist in Salesforce. </mark></h3></summary>
</details>

<details><summary><h3><mark> 4. Users can add products to cart but order placement fails during checkout. What would you do? </mark></h3></summary>
</details>


<details><summary><h3><mark> 5. A user says they cannot see an Account record. How do you troubleshoot? </mark></h3></summary>
</details>


<details><summary><h3><mark> 6. Validation Rule Not Working </mark></h3></summary>
</details>


<details><summary><h3><mark> 7. A flow is active but not working </mark></h3></summary>
</details>
