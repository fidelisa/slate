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
    "address1": "SAVOIE TECHNOLAC",
    "address2": "",
    "zipcode": "73370",
    "city": "LE BOURGET DU LAC",
    "country": "FR",
    "points" : 20,
    "replace_points": true,
    "reason" : "Initialisation de la carte"
  }
}
```

> Resultat JSON

```json

{
  "email": "pierre@martin.com",
  "phone": "+33763454341",
  "key": "CKHVAK1G8XZINR73FIKF",
  "created_at": "2016-05-04 15:25:10",
  "updated_at": "2016-05-04 15:25:13",
  "first_name": "Pierre",
  "last_name": "Martin",
  "longitude": null,
  "latitude": null,
  "gender": "Boy",
  "birth_day": 11,
  "birth_month": 5,
  "birth_year": 1985,
  "status": null,
  "country": "FR",
  "local_phone": "0763454341",
  "lot_import": null,
  "has_smartphone": 0,
  "init_sms_sent": false,
  "present_at": null,
  "first_mobil_at": null,
  "init_mail_sent": false,
  "facebook_id": null,
  "locale": "fr",
  "communication_channel": "Mail",
  "interne": false,
  "account_id": "719D4DFD14DE412488A01F9747346D6D",
  "createby_pos": null,
  "disallow_message": true,
  "godfather_id": null,
  "notes": "Notes",
  "external_id": "4F09958289134A21B3009B0AE07731C9",
  "third_id": null,
  "confirmed_at": null,
  "address1": "234 rue de la place",
  "address2": "Allée 34",
  "zipcode": "75014",
  "city": "Paris",
  "country_id": 1,
  "tag1": "REGULIER",
  "tag2": "SERVICES",
  "tag3": "",
  "created_by": "Bo",
  "uuid": "4F09958289134A21B3009B0AE07731C9",
  "status_name": null
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
third_id | body | ID tiers géré par le fournisseur

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
  "last_name"  : "Martin",
  "status_name" : "Premium",
  "created_at": "2015-01-09 16:17:21",
  "updated_at": "2016-04-12 17:22:14",
  "longitude": "2.3028957454648",
  "latitude": "48.83958350613",
  "gender": "Boy",
  "birth_day": 8,
  "birth_month": 11,
  "birth_year": null,
  "status": null,
  "country": "FR",
  "local_phone": "0650835162",
  "lot_import": null,
  "has_smartphone": 1,
  "init_sms_sent": true,
  "present_at": "2015-01-09 16:46:29",
  "first_mobil_at": "2015-01-09 16:25:12",
  "init_mail_sent": true,
  "facebook_id": null,
  "locale": "fr",
  "communication_channel": "Notification",
  "interne": false,
  "account_id": "0BEB6B01BAFA43AA859567F67C4480AB",
  "createby_pos": null,
  "disallow_message": null,
  "godfather_id": null,
  "notes": "",
  "external_id": "9091E19929B54E1FB7C9DCACB5C1DF09",
  "third_id": null,
  "confirmed_at": null,
  "address1": null,
  "address2": null,
  "zipcode": null,
  "city": null,
  "country_id": null,
  "tag1": null,
  "tag2": null,
  "tag3": null,
  "created_by": "None",
  "status_name": null
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
      "last_name" : "Martin",
      "status_name" : "Premium"
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
without_card| path | Filtre les clients sans carte si true
email| path | Filtre les clients avec cette email (non sensible à la casse)
phone| path | Filtre les clients avec ce n° de téléphone norme local (ex pour la france "0123456789")
third_id| path | Filtre les clients par ID tiers
devices| path | Filtre les clients qui ont activés les notifications push
date| path | Filtre les clients créés depuis la date
date_update| path | Filtre les clients modifiés depuis la date
page | path | Renvoie la liste par lot de 50 clients (ex: 1 = les 50 premiers, 2 = les 50 suivants,...)

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

## Parrain
>  Resultat JSON

```json
{
  "uuid": "D7BE44C125024FD299AFF47156227660",
  "first_name": "Pierre",
  "last_name": "Martin"
}
```

Permet de récupérer le parrain d'un client.

### Authentification

Type : [Shop] (#shop)

### HTTP Request

`GET /api/customers/:customer_id/godfather`

### Query Parameters

Parameter | Type | Description
--------- | --------- | -----------
customer_id | path | UUID du client

### Return code
Code | Description
------- | ---------
200 | OK

## Filleuls
>  Resultat JSON

```json
{
  "customers": [
    {
      "uuid": "70A8A8A5E56640456C23A0D922446DF3",
      "first_name": "Martin",
      "last_name": "Sophie",
      "date_gain": null
    }
  ]
}
```

Permet de récupérer la liste des filleuls d'un client.

### Authentification

Type : [Shop] (#shop)

### HTTP Request

`GET /api/customers/:customer_id/godsons`

### Query Parameters

Parameter | Type | Description
--------- | --------- | -----------
customer_id | path | UUID du client

### Return code
Code | Description
------- | ---------
200 | OK

## Code barre

> Exemple avec une carte

```json
{
    "card_id"  : "1DA03451947C4B91A0EAE4099AD01E26",
    "card_number" : "37634676873"
}
```

> Exemple sans carte

```json
{
    "card_number" : "37634676873"
}
```

Permet de modifier le code barre d'une (ou de toutes les) carte(s) d'un client

### Authentification

Type : [Shop] (#shop)

### HTTP Request

`POST /api/customers/{customer_id}/card_number`

### Query Parameters

Parameter | Type | Description
--------- | --------- | -----------
customer_id | path | UUID du client


Parameter | Type | Description
--------- | --------- | -----------
card_id | body | UUID de la carte (facultatif)
card_number | body | Numéro de la carte

### Return code
Code | Description
------- | ---------
200 | OK

<aside class="notice">
Si aucune carte n'est passée, le numéro de carte est appliqué à toutes les cartes
</aside>
