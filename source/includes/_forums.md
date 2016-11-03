#Forums
***(Coming soon)***
## Liste

>  Resultat JSON

```json
[
  {
      "uuid": "B3CCBF0E28004ECDA60AE54F7B0FB0C3",
      "account_id": "69518EF8A3814B1B9A7CBD455585D866",
      "vendor_id": null,
      "forums_category_id": "6015DB3B0057472B8CB6DF207C4FDDE8",
      "forum_id": null,
      "customer_id": "9018090F497F42EB8396C820034F11AF",
      "title": "test",
      "message": "test rest",
      "created_at": "2016-11-03 10:12:36",
      "updated_at": "2016-11-03 10:12:36",
      "last_answer_at": "2016-11-03 10:12:36"
  },
  {
      "uuid": "3A4101B2AB0B4C8BABCCA947FFC49ACD",
      "account_id": "69518EF8A3814B1B9A7CBD455585D866",
      "vendor_id": null,
      "forums_category_id": "6015DB3B0057472B8CB6DF207C4FDDE8",
      "forum_id": null,
      "customer_id": "9018090F497F42EB8396C820034F11AF",
      "title": "Test2",
      "message": "TEST2",
      "created_at": "2016-11-03 10:15:25",
      "updated_at": "2016-11-03 10:15:25",
      "last_answer_at": "2016-11-03 10:15:25"
  }
]
```

Permet de voir la liste des forums

### Authentification

Type : [Shop] (#shop)

### HTTP Request

`GET /api/forums`

### Query Parameters

Parameter | Type | Description
--------- | --------- | -----------
vendor_id | query | UUID du lieu
search | query | Filtre les forums contenant le mot dans le titre
order | query | ordre de tri (ex: created_at)
forums_category | query | UUID de la catégorie

### Return code
Code | Description
------- | ---------
200 | OK

##Visualisation

> Resultat JSON

```json
{
    "uuid": "3A4101B2AB0B4C8BABCCA947FFC49ACD",
    "account_id": "69518EF8A3814B1B9A7CBD455585D866",
    "vendor_id": null,
    "forums_category_id": "6015DB3B0057472B8CB6DF207C4FDDE8",
    "forum_id": null,
    "customer_id": "9018090F497F42EB8396C820034F11AF",
    "title": "Test2",
    "message": "TEST2",
    "created_at": "2016-11-03 10:15:25",
    "updated_at": "2016-11-03 10:15:25",
    "last_answer_at": "2016-11-03 10:15:25"
}
```

Permet de voir un forum

### Authentification

Type : [Shop] (#shop)

### HTTP Request

`GET /api/forums/{forumId}`

### Query Parameters

Parameter | Type | Description
--------- | --------- | -----------
forumId | path | UUID de du forum


### Return code
Code | Description
------- | ---------
200 | ok

##Créer

```json
{
    "forum": {
        "title": "Premier Message",
        "message": "Mon Premier message",
        "forums_category_id": "E27CCB7D9D0C48728F27966A04170DC0",
        "customer_id": "9018090F497F42EB8396C820034F11AF"
    }
}

{
    "forum": {
        "message": "Une réponse à mon Premier message",
        "forums_category_id": "E27CCB7D9D0C48728F27966A04170DC0",
        "customer_id": "9018090F497F42EB8396C820034F11AF",
        "forum_id" : "C54C675B947243099A0D8CE09A4512E8"
    }
}
```
> Resultat JSON

```json
{
    "uuid": "C54C675B947243099A0D8CE09A4512E8",
    "account_id": "69518EF8A3814B1B9A7CBD455585D866",
    "vendor_id": null,
    "forums_category_id": "E27CCB7D9D0C48728F27966A04170DC0",
    "forum_id": null,
    "customer_id": "9018090F497F42EB8396C820034F11AF",
    "title": "Premier Message",
    "message": "Mon Premier message",
    "created_at": "2016-11-03 16:49:49",
    "updated_at": "2016-11-03 16:49:49",
    "last_answer_at": "2016-11-03 16:49:49"
}
```

Permet de créer un forum

### Authentification

Type : [Shop] (#shop)

### HTTP Request

`POST /api/forums`

### Query Parameters
***Forum***

Parameter | Type | Description
--------- | --------- | -----------
title | body | Nom de du forum
forums_category_id | body | Catégorie d'forum de référence
message | body | Description de du forum
customer_id | body | UUID du client

### Return code
Code | Description
------- | ---------
201 | created

##Mettre à jour

```json
{
    "forum": {
        "title": "Premier Message (corrigé)",
    }
}
```
> Resultat JSON

```json
{
    "uuid": "C54C675B947243099A0D8CE09A4512E8",
    "account_id": "69518EF8A3814B1B9A7CBD455585D866",
    "vendor_id": null,
    "forums_category_id": "E27CCB7D9D0C48728F27966A04170DC0",
    "forum_id": null,
    "customer_id": "9018090F497F42EB8396C820034F11AF",
    "title": "Premier Message (corrigé)",
    "message": "Mon Premier message",
    "created_at": "2016-11-03 16:49:49",
    "updated_at": "2016-11-03 16:49:49",
    "last_answer_at": "2016-11-03 16:49:49"
}
```

Permet de mettre à jour un forum

### Authentification

Type : [Shop] (#shop)

### HTTP Request

`PUT /api/forums/{forumId}`

### Query Parameters
Parameter | Type | Description
--------- | --------- | -----------
forumId | path | UUID de l'événément

***Forum***

Parameter | Type | Description
--------- | --------- | -----------
title | body | Nom de du forum
forums_category_id | body | Catégorie d'forum de référence
message | body | Description de du forum
customer_id | body | UUID du client


### Return code
Code | Description
------- | ---------
200 | ok

##Suppression

> Resultat JSON

```json
{}
```

Permet de supprimer un forum

### Authentification

Type : [Shop] (#shop)

### HTTP Request

`DELETE /api/forums/{forumId}`

### Query Parameters
Parameter | Type | Description
--------- | --------- | -----------
forumId | path | UUID de l'événément


### Return code
Code | Description
------- | ---------
200 | ok
