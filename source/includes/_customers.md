#Customers
##Creation

```json
{
  "customer" : {
    "email"  : "client@monmail.com",
    "phone"  : "0123456789",
    "first_name"  : "Pierre",
    "last_name"  : "Martin",
    "birth_day"  : 19,
    "birth_month"  : 10,
    "points" : 20,
    "replace_points": true,
    "reason" : "Initialisation de la carte"
  }
}
```

> Resultat JSON

```json

{
  "uuid" : "FD39A1AA85AC4F3FB977DEA5A5786263",
  "email" : "client@monmail.com",
  "phone" : "0123456789",
  "first_name" : "Pierre",
  "last_name" : "Martin"
}
```

Permet de créer un client pour le point de vente

### Authentification

Type : [Shop] (#shop)

### HTTP Request

`POST /api/customers`

### Query Parameters
*Customer*

Parameter | Type | Description
--------- | --------- | -----------
email | body | Email
phone | body | Phone
first_name | body | Prénom
last_name | body | Nom
birth_day | body | Jour anniversaire (facultatif)
birth_month | body | Mois anniversaire  (facultatif)

*Les paramètres suivants permettent d'initialiser (ou d'ajouter)
 des points à la carte du client créé (ou existant)*

Parameter | Type | Description
--------- | --------- | -----------
points | body | Nombre de points (facultatif)
replace_points | body | Remplace les points existants (facultatif)
reason | body | Raison de la mise en place des points (facultatif)

### Return code
Code | Description
------- | ---------
201 | Created


## Visualisation

>  Resultat JSON

```json
{
  "uuid" : "FD39A1AA85AC4F3FB977DEA5A5786263",
  "email"  : "client@monmail.com",
  "phone"  : "0123456789",
  "first_name"  : "Pierre",
  "last_name"  : "Martin"
}
```

Permet de voir un client pour le point de vente

### Authentification

Type : [Shop] (#shop)

### HTTP Request

`GET /api/customers/{customer_id}`

### Query Parameters

Parameter | Type | Description
--------- | --------- | -----------
customer_id | path | UUID du client

### Return code
Code | Description
------- | ---------
200 | OK



## Suppression
Permet de supprimer un client pour le point de vente

### Authentification

Type : [Shop] (#shop)

### HTTP Request

`DELETE /api/customers/{customer_id}`

### Query Parameters

Parameter | Type | Description
--------- | --------- | -----------
customer_id | path | UUID du client

### Return code
Code | Description
------- | ---------
200 | OK

## Liste
>  Resultat JSON

```json
{
  "customers" : [
    {
      "uuid" : "FD39A1AA85AC4F3FB977DEA5A5786263",
      "email" : "client@monmail.com",
      "phone" : "0123456789",
      "first_name" : "Pierre",
      "last_name" : "Martin"
    }
  ]
}
```

Permet de récupérer la liste des clients d’un point de vente

### Authentification

Type : [Shop] (#shop)

### HTTP Request

`GET /api/customers`

### Query Parameters

Parameter | Type | Description
--------- | --------- | -----------

### Return code
Code | Description
------- | ---------
200 | OK



## Cartes

>  Resultat JSON

```json
{
  "cards" : [
    {
      "uuid" : "1DA03451947C4B91A0EAE4099AD01E26",
      "title" : "Carte Privilèges",
      "points" : 20,
      "expired_at" : "2015-06-14"
    }
  ]
}
```

Permet de récupérer la liste des cartes d'un client

### Authentification

Type : [Shop] (#shop)

### HTTP Request

`GET /api/customers/{customer_id}/cards`

### Query Parameters

Parameter | Type | Description
--------- | --------- | -----------
customer_id | path | UUID du client

### Return code
Code | Description
------- | ---------
200 | OK



## Date d'expiration

```json
{
    "id"  : "1DA03451947C4B91A0EAE4099AD01E26",
    "date" : "2014-06-20",
    "reset" : true
}
```

Permet de modifier la date d'expiration d'une carte d'un client

### Authentification

Type : [Shop] (#shop)

### HTTP Request

`POST /api/customers/{customer_id}/cards/expired_at`

### Query Parameters

Parameter | Type | Description
--------- | --------- | -----------
customer_id | path | UUID du client


Parameter | Type | Description
--------- | --------- | -----------
id | body | UUID de la carte (facultatif)
date | body | Date d'expiration de la carte
reset | body | Remise à zero des points

### Return code
Code | Description
------- | ---------
200 | OK

<aside class="notice">
Si aucune carte n'est passée en paramètre, c'est la carte par défaut du client qui est expirée
</aside>
