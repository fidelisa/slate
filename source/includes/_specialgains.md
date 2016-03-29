#Gains Speciaux (Obsolète)
## Liste
<aside class="warning">Cette api est obsolète utilisez <a href="#gains">Gains</a></aside>

>  Resultat JSON

```json
{
  "special_gains": [
    {
      "uuid": "6DB912771BCA41A2ZZZDDA9C02A8B24B8",
      "customer_id": "5EE4E32CA6A4AA31EAAB68C381E4A825E",
      "vendor_id": "84D4B5BB95SSS31C12736ED9779E77E",
      "type": null,
      "title": "Cadeau spécial",
      "gived_at": null,
      "created_at": "2015-09-30 08:00:09",
      "updated_at": "2016-02-24 10:45:18",
      "expired_at": "2015-10-30",
      "account_id": "0BEB6DDDVVAFA43AA859567F67C4480AB",
      "card_id": "A6700E63DDFDFD5A78E12C387845B90E7",
      "image_id": null,
      "price": "20.0",
      "discount": "15",
      "code": "E23X45TT",
      "web": true
    }
  ]
}
```

Permet de voir la liste des cadeaux spéciaux d'un client

### Authentification

Type : [Shop] (#shop)

### HTTP Request

`GET /api/customers/{customer_id}/specialgains`

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
<aside class="warning">Cette api est obsolète utilisez <a href="#gains">Gains</a></aside>

> Resultat JSON

```json

{
  "uuid" : "FD39A1AA85AC4F3FB977DEA5A5786263",
  "points": 40,
  "price": "20.0",
  "discount": "15",
  "code": "E23X45TT"
}
```

Permet de consommer un cadeau spécial

### Authentification

Type : [Shop] (#shop)

### HTTP Request

`GET api/specialgains/{specialgain_id}/valid`

### Query Parameters

Parameter | Type | Description
--------- | --------- | -----------
specialgain_id | path | UUID du cadeau special

### Return code
Code | Description
------- | ---------
200 | ok

##Annuler la consommation
<aside class="warning">Cette api est obsolète utilisez <a href="#gains">Gains</a></aside>


> Resultat JSON

```json

{
  "uuid" : "FD39A1AA85AC4F3FB977DEA5A5786263",
  "points": 40,
  "price": "20.0",
  "discount": "15",
  "code": "E23X45TT"
}
```

Permet d'annuler la consommation d'un cadeau spécial

### Authentification

Type : [Shop] (#shop)

### HTTP Request

`GET api/specialgains/{specialgain_id}/unvalid`

### Query Parameters

Parameter | Type | Description
--------- | --------- | -----------
specialgain_id | path | UUID du cadeau special

### Return code
Code | Description
------- | ---------
200 | ok
