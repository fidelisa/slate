#Targets
##Creation (avec fichier)

```json
{
  "target" :{
    "title": "Campagne n°1",
    "external_id": "Campagne_201670292",
    "file_id":"EA8C650C379E4D7C921085A39D3084D5"
  }
}
```
> Resultat JSON

```json
{
  "uuid": "CAC539ED500841229765A503715B0312",
  "title": "Campagne n°1",
  "created_at": "2016-07-05 07:29:12",
  "updated_at": "2016-07-05 07:29:12",
  "file_id": "EA8C650C379E4D7C921085A39D3084D5",
  "account_id": "BADAD0FA3EAF46CBA11CF2348F85B8F4",
  "external_id": "Campagne_201670292",
  "status": null,
  "synced_at": null,
  "vendor_id": "D56EFC4B67084B168E9DC723F9D6F77A",
  "customers_count": null
}
```

Permet de créer une cible à partir d'un [fichier téléchargé] (/#upload)

### Authentification

Type : [Shop] (#shop)

### HTTP Request

`POST /api/targets`

### Query Parameters
***Customer***

Parameter | Type | Description
--------- | --------- | -----------
title | body | Titre de la campagne
external_id | body | ID tiers géré par le fournisseur (facultatif)
file_id | body | ID du fichier téléchargé

### Return code
Code | Description
------- | ---------
201 | Created

##Creation (avec filtre)
```json
{
  "target" :{
    "title": "Campagne n°1",
    "external_id": "Campagne_201670292",
    "filter": {   
      "application": "t",
      "with_email":"t"
    }
  }
}
```

> Resultat JSON

```json

{
  "uuid": "50A271F87C934F34BEFAF12008534533",
  "title": "Campagne n°1",
  "created_at": "2016-07-05 15:30:05",
  "updated_at": "2016-07-05 15:30:05",
  "filter": {
    "application": "t",
    "with_email": "t"    
  },
  "file_id": null,
  "account_id": "BADAD0FA3EAF46CBA11CF2348F85B8F4",
  "external_id": "Campagne_201670292",
  "status": null,
  "synced_at": null,
  "vendor_id": "D56EFC4B67084B168E9DC723F9D6F77A",
  "customers_count": null
}
```

Permet de créer une cible à partir d'un filtre

### Authentification

Type : [Shop] (#shop)

### HTTP Request

`POST /api/targets`

### Query Parameters
***Customer***

Parameter | Type | Description
--------- | --------- | -----------
title | body | Titre de la campagne
external_id | body | ID tiers géré par le fournisseur (facultatif)
filter | body | Filtre à appliquer sur les clients

***Filtre***

Parameter | Description | Valeurs/exemples
--------- | --------- | -----------
application | Utilise l'applicatoin mobile | 't'
channel | Canal de communication | 'Notification', 'Mail'
gender | Sexe | 'Boy', 'Girl'
age_min | Age minimum | 30
age_max | Age maximum | 40
city | Ville | Le Bourget du Lac
country | Pays au format ISO3166 | FR
zipcode | Code postal | 78000
notes | Mot clé (recherche dans les notes) |
tag1 | Valeur du tag 1 |
tag2 | Valeur du tag 2 |
tag3 | Valeur du tag 3 |
last_connexion_max | Ne s'est pas connecté depuis le AAAA-MM-DD | 2016-07-03
last_visit_max | N'est pas venu depuis le AAAA-MM-DD | 2016-07-03
with_phone | 	Numéro de téléphone renseigné | 't'
with_email | 	Adresse mail renseignée | 't'

### Return code
Code | Description
------- | ---------
201 | Created


##Mise à jour
```json
{
  "json": "idem création"
}
```

> Resultat JSON

```json

{
  "json": "idem création"
}
```

Permet de modifier une cible

### Authentification

Type : [Shop] (#shop)

### HTTP Request

`PUT /api/targets`

`PATCH /api/targets`

### Query Parameters
idem création

### Return code
Code | Description
------- | ---------
200 | OK


## Visualisation

>  Resultat JSON

```json
{
  "uuid": "CAC539ED500841229765A503715B0312",
  "title": "Campagne n°1",
  "created_at": "2016-07-05 07:29:12",
  "updated_at": "2016-07-05 07:29:12",  
  "file_id": "EA8C650C379E4D7C921085A39D3084D5",
  "account_id": "BADAD0FA3EAF46CBA11CF2348F85B8F4",
  "external_id": "Campagne_201670292",
  "status": null,
  "synced_at": null,
  "vendor_id": "D56EFC4B67084B168E9DC723F9D6F77A",
  "customers_count": null
}
```

Permet de voir une cible

### Authentification

Type : [Shop] (#shop)

### HTTP Request

`GET /api/targets/{target_id}`

### Query Parameters

Parameter | Type | Description
--------- | --------- | -----------
target_id | path | UUID de la cible

### Return code
Code | Description
------- | ---------
200 | OK



## Suppression
Permet de supprimer une cible

### Authentification

Type : [Shop] (#shop)

### HTTP Request

`DELETE /api/targets/{target_id}`

### Query Parameters

Parameter | Type | Description
--------- | --------- | -----------
target_id | path | UUID du client

### Return code
Code | Description
------- | ---------
200 | OK


## Rafraichissement
Permet de rafraichir une cible

### Authentification

Type : [Shop] (#shop)

### HTTP Request

`GET /api/targets/{target_id}/refresh`

### Query Parameters

Parameter | Type | Description
--------- | --------- | -----------
target_id | path | UUID du client

### Return code
Code | Description
------- | ---------
200 | OK

## Liste
>  Resultat JSON

```json
{
  "targets" : [
    {
      "uuid": "CAC539ED500841229765A503715B0312",
      "title": "Campagne n°1",
      "created_at": "2016-07-05 07:29:12",
      "updated_at": "2016-07-05 07:29:12",  
      "file_id": "EA8C650C379E4D7C921085A39D3084D5",
      "account_id": "BADAD0FA3EAF46CBA11CF2348F85B8F4",
      "external_id": "Campagne_201670292",
      "status": null,
      "synced_at": null,
      "vendor_id": "D56EFC4B67084B168E9DC723F9D6F77A",
      "customers_count": null
    }
  ]
}
```

Permet de récupérer la liste des cibles

### Authentification

Type : [Shop] (#shop)

### HTTP Request

`GET /api/targets`

### Query Parameters

Parameter | Type | Description
--------- | --------- | -----------
search| path | Filtre les cibles par leur titre


### Return code
Code | Description
------- | ---------
200 | OK


## Upload
>  Resultat JSON

```json
{
  "uuid" : "1234587A32784B168E9DC723F9D6F77A"            
}
```
Permet d'envoyer un fichier contenant des clients.Le fichier doit contenir un UUID par ligne.

La requête retourne un UUID qui peut-être utilisé lors de la création/mise à jour d'une cible (file_id).

### Authentification

Type : [Shop] (#shop)

### HTTP Request

`GET /api/targets/upload`

### Query Parameters

Parameter | Type | Description
--------- | --------- | -----------
Content-type | header | multipart/form-data
file | body | fichier contenant les uuid clients


### Return code
Code | Description
------- | ---------
200 | OK
