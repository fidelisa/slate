#Sales
## Creation
```json  
{
  "bill" :
  {
    "total" : "123.50",
    "date" : "2013-01-15",
    "customer_id" : "FD39A1AA85AC4F3FB977DEA5A5786263",
    "details" : [
      {
        "type" : "SubTotal1",
        "amount" : "123.50",
        "quantity" : "2"
       },
      {
        "type"  : "Item",
        "item"  : "1234",
        "amount"  : "12.50",
        "quantity"  : "2"
      }
    ]
  }
}
```

>  Resultat JSON

```json
{
  "bill" :
  {
    "date" : "2013-01-15",
    "total" : "123.5"
  },
  "errors" : [
    {
      "type"  : "Item",
      "item"  : "11234",
      "amount"  : "12.50",
      "quantity"  : "2",
      "error"  : "Not Use"
    }
  ]
}
```

Permet d’ajouter des sales.

### Authentification

Type : [Shop] (#shop)

### HTTP Request

`POST /api/sales/`

### Query Parameters

Parameter | Type | Description
--------- | --------- | -----------
total | body | Montant total l'opération
date | body | Date de l'opération
customer_id | body | UUID du customer
details | body | Tableau de details

### Return code
Code | Description
------- | ---------
201 | CREATED
404 | NOT FOUND

<aside class="warning">
S'il existe des erreurs, elles sont retournées dans un tableau.
</aside>
