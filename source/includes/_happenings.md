#Happenings
***(Coming soon)***
## Liste

>  Resultat JSON

```json
[
  {
      "uuid": "2457B2F6FDAA4625994E5A5A46C71D0D",
      "account_id": "719D4DFD14DE412488A01F9747346D6D",
      "vendor_id": null,
      "title": "Fête du sport",
      "description": "Fête du sport description",
      "image_id": null,
      "happenings_category_id": "A1B878BB9D7E416F87BAB889A755FFCC",
      "started_at": "2017-01-20 00:00:00",
      "quota": 200,
      "reminder_time": 2,
      "created_at": "2016-10-25 07:00:22",
      "updated_at": "2016-10-25 07:00:22",
      "duration": 120,
      "confirmed_customers": 80
  }
]
```

Permet de voir la liste des événements

### Authentification

Type : [Shop] (#shop)

### HTTP Request

`GET /api/happenings`

### Query Parameters

Parameter | Type | Description
--------- | --------- | -----------
vendor_id | query | UUID du lieu
search | query | Filtre les événements contenant le mot dans le titre
order | query | ordre de tri (ex: created_at)
happenings_category | query | UUID de la catégorie
started_at | query | Filtrer les événements quie commencent après une date
started | query | Tous les événements en cours
customer_id | query | Les événements auxquels participe le client

### Return code
Code | Description
------- | ---------
200 | OK

##Visualisation

> Resultat JSON

```json
{
    "uuid": "2457B2F6FDAA4625994E5A5A46C71D0D",
    "account_id": "719D4DFD14DE412488A01F9747346D6D",
    "vendor_id": null,
    "title": "Fête du sport",
    "description": "Fête du sport description",
    "image_id": null,
    "happenings_category_id": "A1B878BB9D7E416F87BAB889A755FFCC",
    "started_at": "2017-01-20 00:00:00",
    "quota": 200,
    "reminder_time": 2,
    "created_at": "2016-10-25 07:00:22",
    "updated_at": "2016-10-25 07:00:22",
    "duration": 120,
    "confirmed_customers": 80
}
```

Permet de voir un événement

### Authentification

Type : [Shop] (#shop)

### HTTP Request

`GET /api/happenings/{happeningId}`

### Query Parameters

Parameter | Type | Description
--------- | --------- | -----------
happeningId | path | UUID de l'événement
with_customers | path | Permet de récupérer les clients participant


### Return code
Code | Description
------- | ---------
200 | ok

##Créer

```json
{
    "happening" : {
        "title": "Fête du sport",
        "description": "Fête du sport description",
        "happenings_category_id": "A1B878BB9D7E416F87BAB889A755FFCC",
        "started_at": "2017-01-20",
        "quota" : 200,
        "reminder_time" : 2
    }
}
```
> Resultat JSON

```json
{
    "uuid": "2457B2F6FDAA4625994E5A5A46C71D0D",
    "account_id": "719D4DFD14DE412488A01F9747346D6D",
    "vendor_id": null,
    "title": "Fête du sport",
    "description": "Fête du sport description",
    "image_id": null,
    "happenings_category_id": "A1B878BB9D7E416F87BAB889A755FFCC",
    "started_at": "2017-01-20 00:00:00",
    "quota": 200,
    "reminder_time": 2,
    "created_at": "2016-10-25 07:00:22",
    "updated_at": "2016-10-25 07:00:22",
    "duration": 120,
    "confirmed_customers": 80
}
```

Permet de créer un événement

### Authentification

Type : [Shop] (#shop)

### HTTP Request

`POST /api/happenings`

### Query Parameters
***Happening***

Parameter | Type | Description
--------- | --------- | -----------
title | body | Nom de l'événement
happenings_category_id | body | Catégorie d'événement de référence
description | body | Description de l'événement
started_at | body | Date/heure de départ de l'événement
quota | body | Nombre maximum de participant
reminder_time | body | Délai (en heure) de rappel de l'événement
vendor_id | body | UUID du lieu (facultatif)
image_id | body | UUID de l'image (facultatif)

### Return code
Code | Description
------- | ---------
201 | created

##Mettre à jour

```json
{
    "happening" : {
        "title": "Fête du sport",
        "description": "Fête du sport description",
        "happenings_category_id": "A1B878BB9D7E416F87BAB889A755FFCC",
        "started_at": "2017-01-20",
        "image_id": "000009AC12464C9183091F34E003BF85",
        "quota" : 200,
        "reminder_time" : 2
    }
}
```
> Resultat JSON

```json
{
    "uuid": "2457B2F6FDAA4625994E5A5A46C71D0D",
    "account_id": "719D4DFD14DE412488A01F9747346D6D",
    "vendor_id": null,
    "title": "Fête du sport",
    "description": "Fête du sport description",
    "image_id": "000009AC12464C9183091F34E003BF85",
    "happenings_category_id": "A1B878BB9D7E416F87BAB889A755FFCC",
    "started_at": "2017-01-20 00:00:00",
    "quota": 200,
    "reminder_time": 2,
    "created_at": "2016-10-25 07:00:22",
    "updated_at": "2016-10-25 07:00:22"
}
```

Permet de mettre à jour un événement

### Authentification

Type : [Shop] (#shop)

### HTTP Request

`PUT /api/happenings/{happeningId}`

### Query Parameters
Parameter | Type | Description
--------- | --------- | -----------
happeningId | path | UUID de l'événément

***Happening***

Parameter | Type | Description
--------- | --------- | -----------
title | body | Nom de l'événement
happenings_category_id | body | Catégorie d'événement de référence
description | body | Description de l'événement
started_at | body | Date/heure de départ de l'événement
quota | body | Nombre maximum de participant
reminder_time | body | Délai (en heure) de rappel de l'événement
vendor_id | body | UUID du lieu (facultatif)
image_id | body | UUID de l'image (facultatif)




### Return code
Code | Description
------- | ---------
200 | ok

##Suppression

> Resultat JSON

```json
{}
```

Permet de supprimer un événement

### Authentification

Type : [Shop] (#shop)

### HTTP Request

`DELETE /api/happenings/{happeningId}`

### Query Parameters
Parameter | Type | Description
--------- | --------- | -----------
happeningId | path | UUID de l'événément


### Return code
Code | Description
------- | ---------
200 | ok
