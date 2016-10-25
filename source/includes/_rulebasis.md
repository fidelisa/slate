#Rule Basis
## Visualisation

>  Resultat JSON

```json
{
  "rulebasis" : [
    {
      "type" : "SubTotal1",
      "item" : "N/A",
      "exclude_discount" : "f"
    },
    {
      "type" : "Item",
      "item" : "1234,4567",
      "exclude_discount" : "true"
    }
  ]
}
```

Permet de récupérer les règles liées aux programmes d'un lieu

### Authentification

Type : [Shop] (#shop)

### HTTP Request

`GET /api/rulebasis`

### Query Parameters

Parameter | Type | Description
--------- | --------- | -----------
customer_id | query | UUID d'un client

### Return code
Code | Description
------- | ---------
200 | OK

<aside class="notice">
Liste des types : Passage, TotalAmount, SubTotal1, SubTotal2, SubTotal3, SubTotal4, SubTotal5, SubTotal6, SubTotal7, SubTotal8, SubTotal9, Item
</aside>
