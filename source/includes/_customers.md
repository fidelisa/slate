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
    "birth_month"  : 10
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

Permet de créer un client pour le shop

### Authentification

Type : [Shop] (#shop)

### HTTP Request

`POST /api/customers`

### Query Parameters

Parameter | Type | Description
--------- | --------- | -----------
email | body | Email du customer
phone | body | Phone du customer
first_name | body | Prénom du customer
last_name | body | Nom du customer
birth_day | body | Jour anniversaire du customer (facultatif)
birth_month | body | Mois anniversaire du customer (facultatif)

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

Permet de voir un customer pour le shop

### Authentification

Type : [Shop] (#shop)

### HTTP Request

`GET /api/customers/{customer_id}`

### Query Parameters

Parameter | Type | Description
--------- | --------- | -----------
customer_id | path | UUID du customer

### Return code
Code | Description
------- | ---------
200 | OK



## Suppression
Permet de supprimer un customer pour le shop

### Authentification

Type : [Shop] (#shop)

### HTTP Request

`DELETE /api/customers/{customer_id}`

### Query Parameters

Parameter | Type | Description
--------- | --------- | -----------
customer_id | path | UUID du customer

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

Permet de récupérer la liste des customers d’un shop

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

Permet de récupérer la liste des cards d'un customer

### Authentification

Type : [Shop] (#shop)

### HTTP Request

`GET /api/customers/{customer_id}/cards`

### Query Parameters

Parameter | Type | Description
--------- | --------- | -----------
customer_id | path | UUID du customer

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

Permet de modifier la date d'expiration d'une card d'un customer

### Authentification

Type : [Shop] (#shop)

### HTTP Request

`POST /api/customers/{customer_id}/cards/expired_at`

### Query Parameters

Parameter | Type | Description
--------- | --------- | -----------
customer_id | path | UUID du customer
id | body | UUID de la card (facultatif)
date | body | Date d'expiration de la card
reset | body | Remise à zero des points

### Return code
Code | Description
------- | ---------
200 | OK

<aside class="notice">
Si aucune carte n'est passée en paramètre, c'est la carte par défaut du client qui est expirée
</aside>
