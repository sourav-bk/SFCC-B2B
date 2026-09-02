
## Create REST API ::

- Step 1: Create Apex REST Class


```apex

@RestResource(urlMapping='/products/*')
global with sharing class ProductAPI {

    @HttpGet
    global static List<Product2> getProducts() {

        return [
            SELECT Id, Name, ProductCode
            FROM Product2
            LIMIT 10
        ];
    }
	
	  @HttpPost
    global static String createAccount() {

        RestRequest req = RestContext.request;

        String accountName = req.requestBody.toString();

        Account acc = new Account(
            Name = accountName
        );

        insert acc;

        return acc.Id;
    }	
}
```


## Explanation::

- @RestResource → Exposes class as REST endpoint.
- urlMapping → API URL path.
- @HttpGet → Handles GET requests.
- @HttpPost-> Handles POST requests.
- global → Required for external access.

```
GET /services/apexrest/products

respond : 
[
  {
    "Id": "01txxx",
    "Name": "Laptop"
  },
  {
    "Id": "01tyyy",
    "Name": "Mouse"
  }
]
```

```
POST /services/apexrest/products

body : 
{
	"name":"ABC Industries"
}

respond : Id

```
