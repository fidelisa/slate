#Happenings categories
***(Coming soon)***
## Liste

>  Resultat JSON

```json
[
    {
        "uuid": "0D15F6D525294DED8DCFF3BC6F313ECB",
        "account_id": "719D4DFD14DE412488A01F9747346D6D",
        "vendor_id": null,
        "title": "Sport",
        "image_id": "000009AC12464C9183091F34E003BF85",
        "type": null,
        "created_at": "2016-10-23 14:29:03",
        "updated_at": "2016-10-23 15:15:00"
    }
]
```

Permet de voir la liste des catégories d'événements

### Authentification

Type : [Shop] (#shop)

### HTTP Request

`GET /api/happenings_categories`

### Query Parameters

Parameter | Type | Description
--------- | --------- | -----------
vendor_id | query | UUID du lieu
search | query | Filtre les catégories contenant le mot dans le titre
order | query | ordre de tri (ex: created_at)

### Return code
Code | Description
------- | ---------
200 | OK

##Visualisation

> Resultat JSON

```json
{
    "uuid": "0D15F6D525294DED8DCFF3BC6F313ECB",
    "account_id": "719D4DFD14DE412488A01F9747346D6D",
    "vendor_id": null,
    "title": "Sport",
    "image_id": "000009AC12464C9183091F34E003BF85",
    "type": null,
    "created_at": "2016-10-23 14:29:03",
    "updated_at": "2016-10-23 15:15:00"
}
```

Permet de voir une catégorie d'événement

### Authentification

Type : [Shop] (#shop)

### HTTP Request

`GET /api/happenings_categories/{categoryId}`

### Query Parameters

Parameter | Type | Description
--------- | --------- | -----------
categoryId | path | UUID de la catégorie


### Return code
Code | Description
------- | ---------
200 | ok

##Créer

```json
{
    "happenings_category": {
        "title": "Danse",
        "vendor_id": "512E811DB8CF4AAC943CACFD84118099",
        "image_id": "000009AC12464C9183091F34E003BF85"
    }
}
```
> Resultat JSON

```json
{
    "uuid": "0D15F6D525294DED8DCFF3BC6F313ECB",
    "account_id": "719D4DFD14DE412488A01F9747346D6D",
    "vendor_id": null,
    "title": "Sport",
    "image_id": "000009AC12464C9183091F34E003BF85",
    "type": null,
    "created_at": "2016-10-23 14:29:03",
    "updated_at": "2016-10-23 15:15:00"
}
```

Permet de créer une catégorie

### Authentification

Type : [Shop] (#shop)

### HTTP Request

`POST /api/happenings_categories`

### Query Parameters
***Category***

Parameter | Type | Description
--------- | --------- | -----------
title | body | Nom de la catégorie
vendor_id | body | UUID du lieu (facultatif)
image_id | body | UUID de l'image (facultatif)

### Return code
Code | Description
------- | ---------
201 | created

##Mettre à jour

```json
{
    "happenings_category": {
        "title": "Equitation",
        "vendor_id": "512E811DB8CF4AAC943CACFD84118099",
        "image_id": "000009AC12464C9183091F34E003BF85"
    }
}
```
> Resultat JSON

```json
{
    "uuid": "0D15F6D525294DED8DCFF3BC6F313ECB",
    "account_id": "719D4DFD14DE412488A01F9747346D6D",
    "vendor_id": null,
    "title": "Sport",
    "image_id": "000009AC12464C9183091F34E003BF85",
    "type": null,
    "created_at": "2016-10-23 14:29:03",
    "updated_at": "2016-10-23 15:15:00"
}
```

Permet de mettre à jour une catégorie d'événement

### Authentification

Type : [Shop] (#shop)

### HTTP Request

`PUT /api/happenings_categories/{categoryId}`

### Query Parameters
Parameter | Type | Description
--------- | --------- | -----------
categoryId | path | UUID de la catégorie

***Category***

Parameter | Type | Description
--------- | --------- | -----------
title | body | Nom de la catégorie
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

Permet de supprimer une catégorie d'événement

### Authentification

Type : [Shop] (#shop)

### HTTP Request

`DELETE /api/happenings_categories/{categoryId}`

### Query Parameters
Parameter | Type | Description
--------- | --------- | -----------
categoryId | path | UUID de la catégorie


### Return code
Code | Description
------- | ---------
200 | ok
