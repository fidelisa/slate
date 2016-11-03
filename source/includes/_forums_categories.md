#Forums categories
***(Coming soon)***
## Liste

>  Resultat JSON

```json
[
  {
    "uuid": "6015DB3B0057472B8CB6DF207C4FDDE8",
    "account_id": "69518EF8A3814B1B9A7CBD455585D866",
    "vendor_id": null,
    "title": "Tennis",
    "created_at": "2016-11-03 09:10:07",
    "updated_at": "2016-11-03 09:10:07",
    "forums": {
      "count": 5,
      "last": "2016-11-03 15:20:03"
    }
  },
  {
    "uuid": "C60EB9C9E485429AB6DE228B8E8F31BC",
    "account_id": "69518EF8A3814B1B9A7CBD455585D866",
    "vendor_id": null,
    "title": "Running",
    "created_at": "2016-11-03 13:12:25",
    "updated_at": "2016-11-03 13:12:25",
    "forums": {
      "count": 2,
      "last": "2016-11-03 15:56:30"
    }
  }
]
```

Permet de voir la liste des catégories de forums

### Authentification

Type : [Shop] (#shop)

### HTTP Request

`GET /api/forums_categories`

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
    "uuid": "1EC207C1F80F4DCD8796E9ED720E3635",
    "account_id": "69518EF8A3814B1B9A7CBD455585D866",
    "vendor_id": null,
    "title": "Natation",
    "created_at": "2016-11-03 16:41:04",
    "updated_at": "2016-11-03 16:41:04",
    "forums": {
        "count": 0,
        "last": null
    }
}
```

Permet de voir une catégorie de forum

### Authentification

Type : [Shop] (#shop)

### HTTP Request

`GET /api/forums_categories/{categoryId}`

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
    "forums_category": {
        "title": "Danse",
        "vendor_id": "512E811DB8CF4AAC943CACFD84118099"
    }
}
```
> Resultat JSON

```json
{
    "uuid": "E27CCB7D9D0C48728F27966A04170DC0",
    "account_id": "69518EF8A3814B1B9A7CBD455585D866",
    "vendor_id": "512E811DB8CF4AAC943CACFD84118099",
    "title": "Danse",
    "created_at": "2016-11-03 16:43:41",
    "updated_at": "2016-11-03 16:43:41",
    "forums": {
        "count": 0,
        "last": null
    }
}
```

Permet de créer une catégorie

### Authentification

Type : [Shop] (#shop)

### HTTP Request

`POST /api/forums_categories`

### Query Parameters
***Category***

Parameter | Type | Description
--------- | --------- | -----------
title | body | Nom de la catégorie
vendor_id | body | UUID du lieu (facultatif)

### Return code
Code | Description
------- | ---------
201 | created

##Mettre à jour

```json
{
    "forums_category": {
        "title": "Equitation",
        "vendor_id": "512E811DB8CF4AAC943CACFD84118099"
    }
}
```
> Resultat JSON

```json
{
    "uuid": "E27CCB7D9D0C48728F27966A04170DC0",
    "account_id": "69518EF8A3814B1B9A7CBD455585D866",
    "vendor_id": "512E811DB8CF4AAC943CACFD84118099",
    "title": "Equitation",
    "created_at": "2016-11-03 16:43:41",
    "updated_at": "2016-11-03 16:43:41",
    "forums": {
        "count": 0,
        "last": null
    }
}
```

Permet de mettre à jour une catégorie de forum

### Authentification

Type : [Shop] (#shop)

### HTTP Request

`PUT /api/forums_categories/{categoryId}`

### Query Parameters
Parameter | Type | Description
--------- | --------- | -----------
categoryId | path | UUID de la catégorie

***Category***

Parameter | Type | Description
--------- | --------- | -----------
title | body | Nom de la catégorie
vendor_id | body | UUID du lieu (facultatif)



### Return code
Code | Description
------- | ---------
200 | ok

##Suppression

> Resultat JSON

```json
{}
```

Permet de supprimer une catégorie de forum

### Authentification

Type : [Shop] (#shop)

### HTTP Request

`DELETE /api/forums_categories/{categoryId}`

### Query Parameters
Parameter | Type | Description
--------- | --------- | -----------
categoryId | path | UUID de la catégorie


### Return code
Code | Description
------- | ---------
200 | ok
