---
title: Fidelisa API Reference

language_tabs:
- ruby
- csharp

toc_footers:
- <a href='#'>Sign Up for a Developer Key</a>
- <a href='http://github.com/tripit/slate'>Documentation Powered by Slate</a>

includes:
- errors

search: true
---

# Introduction

L’interfaçage entre le logiciel de caisse et Fidelisa repose sur l’API Fidelisa (API REST).
Pour faire fonctionner les API, l’éditeur de logiciel de caisse doit être référencé par Fidelisa. Dans Fidelisa, le nom du logiciel de caisse figure dans le compte commerçant et permet l’authentification Editeur nécessaire à la connexion aux API.

Fonctionnellement, plusieurs scénarios sont possibles. L’éditeur du logiciel de caisse détermine ce scénario en fonction du niveau d’intégration qu’il souhaite.

Le commerçant crée ses cartes de fidélité dans Fidelisa et indique sur quelles bases s’effectue le calcul des points fidélité.

Ces bases peuvent être de 5 types :

* Total des achats
* Nombre de visites
* Catégories
* Marques de produits
* Certaines lignes de ticket

Le TPV transmet les informations utiles au calcul de fidélité et Fidelisa met automatiquement à jour les cartes de fidélité en temps réel, jusqu’au smartphone du client.

**Gestion des catégories TPV**
Le TPV dispose de 9 catégories personnalisables proposées sous la forme d’agrégats utilisables par Fidelisa (catégories). Le paramétrage de ces catégories est effectué par nos soins lors du référencement du TPV.

**Communication avec les clients**
Fidelisa apporte également un canal de communication aux commerçants via notification (pour les clients équipés de smartphone), mail ou SMS.
Cette “messagerie” peut être directement utilisée depuis le TPV via l’API correspondante : “Notification-création”.

#Lexique

Nom | Définition
------- | ------
Provider | Editeur de logiciel, agence, fournisseur, ...
Shop | Point de vente, ecommerce, ...
Customer | Client d'un shop

#Support
Un support (mail ou téléphone) pour toute question technique ou fonctionnelle relative à l’implémentation de Fidelisa.

Les icônes (plusieurs formats disponibles) pour afficher dans le TPV par exemple l’état du client (inscrit sur Fidelisa ou non).

Des squelettes de code pour les principaux languages permettant de faciliter l’implémentation de l’API.


#Authentification
##Provider
> Calcul de la cle

```
FIDELISA_JETON est un jeton aléatoire (différent à chaque appel)

FIDELISA_PROVIDER_KEY correspond au calcul de la signature avec comme paramètres :
  request : concatenation de FIDELISA_PROVIDER et FIDELISA_JETON.
  secret_key : FIDELISA_PROVIDER
```

Ces requêtes nécessitent les droits fournisseur (ex: Initialisation d'un shop).

Dans le header de la requête ajouter les éléments suivants :

Nom |  Description
--------- | -----------
FIDELISA_JETON  | code à usage unique généré par le provider
FIDELISA_PROVIDER |  code Fidelisa fourni par Fidelisa
FIDELISA_PROVIDER_KEY  | signature de la requête




##Shop
> Calcul de la cle

```
FIDELISA_JETON est un jeton aléatoire (différent à chaque appel)

FIDELISA_PROVIDER_KEY correspond au calcul de la signature avec comme paramètres :
  request : concatenation de FIDELISA_PROVIDER et FIDELISA_JETON.
  secret_key : FIDELISA_PROVIDER

FIDELISA_APIUSER_KEY correspond au calcul de la [signature](#Signature) avec comme paramètres :
  request : concatenation de FIDELISA_APIUSER et FIDELISA_JETON.
  secret_key : FIDELISA_APIUSER
```

Ces requêtes nécessitent les droits shop (ex: la création d’un client).

Dans le header de la requête ajouter les éléments suivants :
La partie Header du “fournisseur” (voir plus haut)

Nom |  Description
--------- | -----------
FIDELISA_JETON  | code à usage unique généré par le provider
FIDELISA_PROVIDER |  code Fidelisa fourni par Fidelisa
FIDELISA_PROVIDER_KEY  | signature de la requête
FIDELISA_APIUSER | code du commerce retourné lors de l’appel du init/shop (champ uuid du json)
FIDELISA_APIUSER_KEY | [signature de la requête](#signature)



# Exemples de code
## Signature
```ruby
def sign_request(request, secret_key)
  #encode base 64
  policy = Base64.strict_encode64(request)

  # Sign policy with secret key
  digest = OpenSSL::Digest.new('sha1')
  hmac=OpenSSL::HMAC.hexdigest(digest, secret_key, policy)

  # encode base 64
  signature = Base64.strict_encode64(hmac)
  signature
end
```

```csharp
private string SignRequest(string request, string secretKey)
{
    // encode base 64
    string policy = System.Convert.ToBase64String(System.Text.ASCIIEncoding.ASCII.GetBytes(request));
    // hmac-sha1 with secretKey
    var digest = new HMACSHA1(System.Text.ASCIIEncoding.ASCII.GetBytes(secretKey));
    digest.Initialize();
    var tmp = BitConverter.ToString(digest.ComputeHash(Encoding.ASCII.GetBytes(policy)));
    // remove "-" and downcase
    var hmac = tmp.Replace("-", "").ToLower();
    // encode base64
    string signature = System.Convert.ToBase64String(System.Text.ASCIIEncoding.ASCII.GetBytes(hmac));
    return signature;
}
```
Exemple de fonction permettant de calculer une signature.

###Function parameters
Nom | Description
------- | ---------
request | Chaine à crypter
secret_key | Clé de cryptage

###Function return
Nom | Description
------- | ---------
retour | Chaine cryptée


## Headers

```ruby
def make_hearders_request(request, withshop = false)
  jeton = rand(99999999).to_s
  request["FIDELISA_JETON"] = jeton
  request["FIDELISA_PROVIDER"] = @provider
  request["FIDELISA_PROVIDER_KEY"] = sign_request(@provider + jeton, @provider_key )

  if (withshop)
    request["FIDELISA_APIUSER"] = @shop
    request["FIDELISA_APIUSER_KEY"] = sign_request(@shop + jeton, @shop_key )
  end
end
```

```csharp
public void MakeHeadersRequest(HttpWebRequest request, bool withshop = false)
{
    Random rnd = new Random();
    int jeton = rnd.Next(99999999);
    request.Headers.Add("FIDELISA_JETON", jeton.ToString());
    request.Headers.Add("FIDELISA_PROVIDER", provider);
    request.Headers.Add("FIDELISA_PROVIDER_KEY", SignRequest(provider + jeton, providerKey));
    if (withshop)
    {
        request.Headers.Add("FIDELISA_APIUSER", shop);
        request.Headers.Add("FIDELISA_APIUSER_KEY", SignRequest(shop + jeton, shopKey));
    }
}
```

Fabrique des entêtes Fidelisa d'une requête

###Function parameters
Nom | Description
------- | ---------
request | Requête à signer
withshop | Requête de type shop ? true/false


## Get
```ruby
def get_programs
  http = Net::HTTP.new(@uri.host, @uri.port)
  http.use_ssl = true

  request = Net::HTTP::Get.new("/api/shops/programs")
  make_hearders_request(request, true)
  response = http.request(request)
  body = JSON.parse(response.body)
  body["programs"]
end
```

```csharp
public Programs GetPrograms()
{
    String requestUrl = HOST_FIDELISA + "/api/shops/programs";
    HttpWebRequest request = WebRequest.Create(requestUrl) as HttpWebRequest;
    MakeHeadersRequest(request, true);

    using (HttpWebResponse response = request.GetResponse() as HttpWebResponse)
    {
        DataContractJsonSerializer jsonSerializer = new DataContractJsonSerializer(typeof(Programs));
        Object objResponse = jsonSerializer.ReadObject(response.GetResponseStream());
        return objResponse as Programs;
    }
}
```

Exemple d'appel d'une fonction Get (Liste des programmes)

###Function parameters
Nom | Description
------- | ---------

###Function return
Nom | Description
------- | ---------
retour | Tableaux de programmes

## Post

```ruby
def init_shop
  http = Net::HTTP.new(@uri.host, @uri.port)
  http.use_ssl = true

  request = Net::HTTP::Post.new("/api/shops/init")
  request['Content-Type'] = 'application/json'
  make_hearders_request(request, false)
  request.body = ({ :shop => { "user_email" => @shop_mail } }).to_json
  response = http.request(request)
  body = JSON.parse(response.body)
end
```

```csharp
public Shop InitShop()
{
    String requestUrl = HOST_FIDELISA + "/api/shops/init";
    HttpWebRequest request = (HttpWebRequest)WebRequest.Create(requestUrl);
    request.Method = "POST";
    MakeHeadersRequest(request);
    request.ContentType = "application/json; charset=utf-8";

    Shop shop = new Shop { userMail = shopMail };
    DataContractJsonSerializer ser = new DataContractJsonSerializer(shop.GetType());
    MemoryStream ms = new MemoryStream();
    ser.WriteObject(ms, shop);
    String json = Encoding.UTF8.GetString(ms.ToArray());
    StreamWriter writer = new StreamWriter(request.GetRequestStream());
    writer.Write(json);
    writer.Close();

    using (HttpWebResponse response = request.GetResponse() as HttpWebResponse)
    {
        DataContractJsonSerializer jsonSerializer = new DataContractJsonSerializer(typeof(Shop));
        Object objResponse = jsonSerializer.ReadObject(response.GetResponseStream());
        return objResponse as Shop;
    }

}
```

Exemple d'appel d'une fonction Post (Initialisation du shop)

###Function parameters
Nom | Description
------- | ---------

###Function return
Nom | Description
------- | ---------
retour | Le shop initialisé



## Date et Montant
Les dates sont au format YYYY-MM-DD
Pour les montants, le séparateur de décimal est le “.” (point), il n’y a pas de séparateur de milliers.

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

Permet d’initialiser la relation entre le shop et Fidelisa

### Authentification

Type : [Provider] (#provider)

### HTTP Request

`POST /api/shops/init`

### Query Parameters

Parameter | Type | Description
--------- | ----------- | -----------
user_email | body | Email du shop  


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

Permet de visualiser un shop

### Authentification

Type : [Provider] (#provider)

### HTTP Request

`GET /api/shops/{ShopId}`

### Query Parameters

Parameter | Type | Description
--------- | --------- | -----------
ShopId | path | UUID du shop


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

Permet de récupérer la liste des boutiques attachés au fournisseur

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

Permet de récupérer un tableau des catégories paramétrées par le shop

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

#Rule Basis
## Visualisation

>  Resultat JSON

```json
{
  "rulebasis" : [
    {
      "type" : "SubTotal1",
      "item" : "N/A",
      "exclude_discount" : "f"
    },
    {
      "type" : "Item",
      "item" : "1234,4567",
      "exclude_discount" : "true"
    }
  ]
}
```

Permet de récupérer les rulebasis pour un shop

### Authentification

Type : [Shop] (#shop)

### HTTP Request

`GET /api/rulebasis`

### Query Parameters

Parameter | Type | Description
--------- | --------- | -----------
customer_id | query | UUID d'un customer

### Return code
Code | Description
------- | ---------
200 | OK

<aside class="notice">
Liste des types : Passage, TotalAmount, SubTotal1, SubTotal2, SubTotal3, SubTotal4, SubTotal5, SubTotal6, SubTotal7, SubTotal8, SubTotal9, Item
</aside>

#Sales
## Creation
```json  
{
  "bill" :
  {
    "total" : "123.50",
    "date" : "2013-01-15",
    "customer_id" : "FD39A1AA85AC4F3FB977DEA5A5786263",
    "details" : [
      {
        "type" : "SubTotal1",
        "amount" : "123.50",
        "quantity" : "2"
       },
      {
        "type"  : "Item",
        "item"  : "1234",
        "amount"  : "12.50",
        "quantity"  : "2"
      }
    ]
  }
}
```

>  Resultat JSON

```json
{
  "bill" :
  {
    "date" : "2013-01-15",
    "total" : "123.5"
  },
  "errors" : [
    {
      "type"  : "Item",
      "item"  : "11234",
      "amount"  : "12.50",
      "quantity"  : "2",
      "error"  : "Not Use"
    }
  ]
}
```

Permet d’ajouter des sales.

### Authentification

Type : [Shop] (#shop)

### HTTP Request

`POST /api/sales/`

### Query Parameters

Parameter | Type | Description
--------- | --------- | -----------
total | body | Montant total l'opération
date | body | Date de l'opération
customer_id | body | UUID du customer
details | body | Tableau de details

### Return code
Code | Description
------- | ---------
201 | CREATED
404 | NOT FOUND

<aside class="warning">
S'il existe des erreurs, elles sont retournées dans un tableau.
</aside>

#Points
##Creation
Permet d'ajouter des points à une card

>Avec un identifiant de carte connu

```json
{
  "correction" : {
    "points" : 20,
    "customer_id" : "FD39A1AA85AC4F3FB977DEA5A5786263",
    "card_id" : "1DA03451947C4B91A0EAE4099AD01E26"
  }
}
```

>Si le customer n'a qu'une seule carte, celle-ci sera créditée automatiquement

```json
{
  "correction" : {
    "points" : 20,
    "customer_id" : "FD39A1AA85AC4F3FB977DEA5A5786263"
  }
}
```

### Authentification

Type : [Shop] (#shop)

### HTTP Request

`POST /api/corrections`

### Query Parameters

Parameter | Type | Description
--------- | --------- | -----------
points | body | Nombre de points à créditer sur la card
customer_id | body | UUID du customer
card_id | body | Card du customer (facultatif)

### Return code
Code | Description
------- | ---------
201 | CREATED
422 | UNPROCESSABLE ENTITY



#Gifts
## Client

>  Resultat JSON

```json
{
  "gifts" : [
    {
      "uuid" : "FD39A1AA85AC4F3FB977DEA5A5786263",
      "title" : "10€ de bon d’achat",
      "points" : 123
    }
  ]
}
```

Permet de récupérer la liste des cadeaux consommables par le client.

### Authentification

Type : [Shop] (#shop)

### HTTP Request

`GET /api/gifts`

### Query Parameters

Parameter | Type | Description
--------- | --------- | -----------
customer_id | query | UUID du customer
used | query | Filtrer les cadeaux déjà offerts (facultatif)

### Return code
Code | Description
------- | ---------
201 | CREATED
404 | NOT FOUND

<aside class="notice">
La propriété "points", du retour correspond au nombre de points collectés sur la carte correspondant au cadeau. Cette propriété n’est disponible que lors de l’appel des cadeaux disponibles.
</aside>


## Consommation

```json  
{
  "uuid" : "AZEFDFD39A1AA85AC423JJL34NEZOJ3E",
  "customer_id" : "FD39A1AA85AC4F3FB977DEA5A5786263"
}
```

Permet d’indiquer que le customer a consommé le cadeau

### Authentification

Type : [Shop] (#shop)

### HTTP Request

`POST /api/gifts/award`

### Query Parameters

Parameter | Type | Description
--------- | --------- | -----------
uuid | body | UUID du cadeaux
customer_id | body | UUID du customer


### Return code
Code | Description
------- | ---------
200 | OK
404 | NOT FOUND


## Restauration
Permet d’annuler la consommation d’un cadeau

### Authentification

Type : [Shop] (#shop)

### HTTP Request

`DELETE /api/gifts/{gift_id}`

### Query Parameters

Parameter | Type | Description
--------- | --------- | -----------
gift_id | path | UUID du cadeaux
customer_id | query | UUID du customer


### Return code
Code | Description
------- | ---------
200 | OK
404 | NOT FOUND


#Notifications
## Envoi

> Pour un client unique

```json
{
  "customer" : "FD39A1AA85AC4F3FB977DEA5A5786263",
  "alert" : "Message au client"
}
```

> pour un programme

```json
{
  "program" : "FD39A1AA85AC4F3FB977DEA5A5786263",
  "alert" : "Message aux clients"
}
```

> pour un ensemble de clients avec des urls spécifiques

```json
{
  "customers" : {
    "D407587D800ECC6C629A52CD204C6E61" : "http://fidelisa.com/1",
    "FD39A1AA85AC4F3FB977DEA5A5786263" : "http://fidelisa.com/2"
    },
    "alert" : "Message aux clients"
}
```

Permet d’envoyer une notification à un customer ou à tous les customers d’un programme de fidelité

### Authentification

Type : [Shop] (#shop)

### HTTP Request

`POST /api/notifications`

### Query Parameters

Parameter | Type | Description
--------- | --------- | -----------


### Return code
Code | Description
------- | ---------
200 | OK
