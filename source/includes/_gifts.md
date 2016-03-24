#Gifts
## Client

>  Resultat JSON

```json
{
  "gifts" : [
    {
      "uuid" : "FD39A1AA85AC4F3FB977DEA5A5786263",
      "title" : "10€ de bon d’achat",
      "points" : 123,
      "price": "25.00",
      "discount": "15",
      "code": "E23X45TT"
    }
  ]
}
```

Permet de récupérer la liste des cadeaux consommables par le client.

### Authentification

Type : [Shop] (#shop)

### HTTP Request

`GET /api/gifts`

### Query Parameters

Parameter | Type | Description
--------- | --------- | -----------
customer_id | query | UUID du client
used | query | Filtrer les cadeaux déjà offerts (facultatif)

### Return code
Code | Description
------- | ---------
201 | CREATED
404 | NOT FOUND

<aside class="notice">
La propriété "points", du retour correspond au nombre de points collectés sur la carte correspondant au cadeau. Cette propriété n’est disponible que lors de l’appel des cadeaux disponibles.
</aside>


## Consommation

```json  
{
  "uuid" : "AZEFDFD39A1AA85AC423JJL34NEZOJ3E",
  "customer_id" : "FD39A1AA85AC4F3FB977DEA5A5786263"
}
```

Permet d’indiquer que le customer a consommé le cadeau.

### Authentification

Type : [Shop] (#shop)

### HTTP Request

`POST /api/gifts/award`

### Query Parameters

Parameter | Type | Description
--------- | --------- | -----------
uuid | body | UUID du cadeaux
customer_id | body | UUID du client


### Return code
Code | Description
------- | ---------
200 | OK
404 | NOT FOUND


## Restauration
Permet d’annuler la consommation d’un cadeau

### Authentification

Type : [Shop] (#shop)

### HTTP Request

`DELETE /api/gifts/{gift_id}`

### Query Parameters

Parameter | Type | Description
--------- | --------- | -----------
gift_id | path | UUID du cadeaux
customer_id | query | UUID du client


### Return code
Code | Description
------- | ---------
200 | OK
404 | NOT FOUND
