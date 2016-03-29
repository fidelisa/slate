#Gains
## Liste

>  Resultat JSON

```json
[
  {
    "uuid": "EB846456B1979BAB763DB04ECEC481C4",
    "customer_id": "512E811DB8CF4AAC943CACFD84118099",
    "vendor_id": null,
    "type": "GiftGain",
    "gived_at": null,
    "created_at": "2016-03-29 10:06:25",
    "updated_at": "2016-03-29 10:14:02",
    "expired_at": null,
    "account_id": "4C0741AF77EE4410948EA9FB925A0A1A",
    "card_id": "48AA097CFF8146CBA809D12BAD225686",
    "image_id": null,
    "price": "0.0",
    "points": 100,
    "discount": 5,
    "code": "12345",
    "web": false,
    "title": "5% sur prochain achat"
  }
]
```

Permet de voir la liste des cadeaux (paliers et spéciaux) d'un client

### Authentification

Type : [Shop] (#shop)

### HTTP Request

`GET /api/customers/{customer_id}/gains`

### Query Parameters

Parameter | Type | Description
--------- | --------- | -----------
customer_id | path | UUID du client
used | query | Filtre les gains consommés
web | query | Filtre les gains consommables uniquement sur le web

### Return code
Code | Description
------- | ---------
200 | OK

##Consommation

> Resultat JSON

```json
{
  "uuid": "EB846456B1979BAB763DB04ECEC481C4",
  "customer_id": "512E811DB8CF4AAC943CACFD84118099",
  "vendor_id": null,
  "type": "GiftGain",
  "gived_at": null,
  "created_at": "2016-03-29 10:06:25",
  "updated_at": "2016-03-29 10:14:02",
  "expired_at": null,
  "account_id": "4C0741AF77EE4410948EA9FB925A0A1A",
  "card_id": "48AA097CFF8146CBA809D12BAD225686",
  "image_id": null,
  "price": "0.0",
  "points": 100,
  "discount": 5,
  "code": "12345",
  "web": false,
  "title": "5% sur prochain achat"
}
```

Permet de consommer un cadeau

### Authentification

Type : [Shop] (#shop)

### HTTP Request

`GET /api/customers/{customer_id}/gains/{gain_id}/valid`

### Query Parameters

Parameter | Type | Description
--------- | --------- | -----------
customer_id | path | UUID du client
gain_id | path | UUID du cadeau

### Return code
Code | Description
------- | ---------
200 | ok

##Annuler la consommation

> Resultat JSON

```json
{
  "uuid": "EB846456B1979BAB763DB04ECEC481C4",
  "customer_id": "512E811DB8CF4AAC943CACFD84118099",
  "vendor_id": null,
  "type": "GiftGain",
  "gived_at": null,
  "created_at": "2016-03-29 10:06:25",
  "updated_at": "2016-03-29 10:14:02",
  "expired_at": null,
  "account_id": "4C0741AF77EE4410948EA9FB925A0A1A",
  "card_id": "48AA097CFF8146CBA809D12BAD225686",
  "image_id": null,
  "price": "0.0",
  "points": 100,
  "discount": 5,
  "code": "12345",
  "web": false,
  "title": "5% sur prochain achat"
}
```

Permet d'annuler la consommation d'un cadeau

### Authentification

Type : [Shop] (#shop)

### HTTP Request

`GET /api/customers/{customer_id}/gains/{gain_id}/unvalid`

### Query Parameters

Parameter | Type | Description
--------- | --------- | -----------
customer_id | path | UUID du client
gain_id | path | UUID du cadeau

### Return code
Code | Description
------- | ---------
200 | ok
