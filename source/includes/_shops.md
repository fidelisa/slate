#Shops
## Initialisation

```json
{
    "shop": {
      "user_email" : "test3@fidelisa.com"
    }
}
```

> Resultat JSON

```json
{
  "title" : "test3",
  "uuid" : "619E8B5AAD5E48138881C5E7774C86B2",
  "key" : "FrZN6UChpqXBRKVExXVB",
  "user_email" : "test3@fidelisa.com"
}
```

Permet d’initialiser la relation entre le lieu et Fidelisa

### Authentification

Type : [Provider] (#provider)

### HTTP Request

`POST /api/shops/init`

### Query Parameters
***Shop***

Parameter | Type | Description
--------- | ----------- | -----------
user_email | body | Email du lieu  

### Return code
Code | Description
------- | ---------
200 | OK


## Visualisation
> Resultat JSON

```json
{
  "title" : "test3",
  "uuid" : "619E8B5AAD5E48138881C5E7774C86B2",
  "key" : "FrZN6UChpqXBRKVExXVB",
  "user_email" : "test@test.com"
}
```

Permet de visualiser un lieu

### Authentification

Type : [Provider] (#provider)

### HTTP Request

`GET /api/shops/{ShopId}`

### Query Parameters

Parameter | Type | Description
--------- | --------- | -----------
ShopId | path | UUID du lieu


### Return code
Code | Description
------- | ---------
200 | OK

## Liste

>  Resultat JSON

```json
{
  "shops": [
    {
      "title" : "Test 1",
      "uuid" : "FD39A1AA85AC4F3FB977DEA5A5786263",
      "key" : "YAZX2TLVO19DEFVDFF8M",
      "user_email" : "bva7nntn1zfpn4uhvzaw@fidelisa.com"
    },
    {
      "title" : "Test 2",
      "uuid" : "D0114EE251D14C5180991418736A6ACC",
      "key" : "RCGQDPWTRQS2XZCHWEZB",
      "user_email" : "9bpxdq5hzzmuuayovbfx@fidelisa.com"
    }
  ]
}
```

Permet de récupérer la liste des points de vente attachés au fournisseur

### Authentification

Type : [Provider] (#provider)

### HTTP Request

`GET /api/shops`

### Query Parameters

Parameter | Type | Description
--------- | --------- | -----------

### Return code
Code | Description
------- | ---------
200 | OK


## Categories

> Resultat JSON

```json
{
  "categories":
  {
    "subtotal1": "SUBTOTAL1",
    "subtotal2": "SUBTOTAL2",
    "subtotal3": "SUBTOTAL3",
    "subtotal4": null,
    "subtotal5": null,
    "subtotal6": null,
    "subtotal7": null,
    "subtotal8": null,
    "subtotal9": null
  }
}
```

Permet de récupérer un tableau des catégories paramétrées par le lieu

### Authentification

Type : [Provider] (#provider)

### HTTP Request

`GET /api/shops/categories`

### Query Parameters

Parameter | Type | Description
--------- | --------- | -----------

### Return code
Code | Description
------- | ---------
200 | OK


## Programmes

> Resultat JSON

```json
{
  "programs" : [
    {
      "title" : "Carte VIP",
      "uuid" : "67B222DC2A92672CA8E9D2C6DCB785CB"
    },
    {
      "title" : "Carte Privilèges",
      "uuid" : "8853A37D20967C9E099184814805AC31"
    }
  ]
}
```

Permet de récupérer la liste des programmes d'un commerce

### Authentification

Type : [Provider] (#provider)

### HTTP Request

`GET /api/shops/programs`

### Query Parameters

Parameter | Type | Description
--------- | --------- | -----------

### Return code
Code | Description
------- | ---------
200 | OK
