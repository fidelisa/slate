---
title: Fidelisa API Reference

language_tabs:
  - ruby
  - C#

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


# Exemple de scénario d’utilisation

  Cet exemple n’est cité qu'à titre indicatif. D’autres hypothèses sont envisageables et nous sommes à la disposition des éditeurs de TPV pour déterminer le scénario le plus adapté.
## Création du compte commerçant dans Fidelisa
  Le compte Fidelisa du commerce est créé dans Fidelisa (https://bo.fidelisa.com).
  Dans le logiciel Point de vente, l’utilisateur renseigne l’adresse mail qui a été utilisée pour le compte Fidelisa. Le TPV récupère l’ID du compte Fidelisa via l’API “Commerce-initialisation”, et la stocke.
    Cette opération ne sera réalisée qu’une seule fois.

## Création des clients dans Fidelisa depuis le TPV
  Cette opération n’est effectuée qu’une fois pour un client. Lorsque le client est créé dans Fidelisa, son identifiant est mémorisé dans le TPV qui peut indiquer visuellement que ce client est activé dans Fidelisa.
  API : “Client-création”
  Message de retour proposé dans le TPV : “Ce client a été ajouté à Fidelisa.”
  Les clients créés dans Fidelisa depuis le TPV ne peuvent être supprimés dans Fidelisa que depuis le TPV : API “Client-suppression”

## Transfert des informations relatives aux tickets à Fidelisa
  Cette opération peut être effectuée lors de chaque ticket (en mode asynchone) ou pour un ensemble de tickets.
  Interrogation des règles des cartes attachées au client (API “Rule basis-client”)

  Envoi des informations utiles des tickets (API “Ventes-ajout”)
  Les valeurs négatives sont acceptées par l’API : les annulations de tickets doivent être adressées comme des tickets de vente classique.
  Le paramétrage des règles de fidélité autorise le commerçant à exclure les ventes avec réduction de ses programmes de fidélité.Dans ce cas, l’API mentionne au niveau de chaque ligne ou agrégat du ticket l’exclusion ou non des lignes avec réduction.
  Le TPV gère l’information à envoyer en fonction de ce critère.
  Contrôle des envois vers Fidelisa
  Le contrôle de conformité et d’unicité des envois est effectué côté TPV.
  Une interface de contrôle des historiques (création et suppression clients, lignes de tickets adressés) est souhaitable pour faciliter la phase de tests de l’application.

  ## Disponibilité d’un cadeau pour le client

    Le commerçant peut être alerté de l’existence d’un cadeau disponible pour le client lors du passage en caisse.
    Cette information peut être gérée en mode asynchrone, par “balayage” de la liste des clients Fidelisa connus dans le TPV pour le commerce.
    Cette information est disponible via l’API “Cadeaux-client”


  ## Appel de Fidelisa depuis la caisse (mode client sélectionné) et depuis la fiche client
    Fidelisa propose l’intégration d’un bouton d’action qui prend 3 valeurs en fonction du statut client :

  *Grisé : client non géré dans Fidelisa

      *appelle l’API “client-ajout”
      *appelle le plug-in d’affichage Fidelisa avec accès direct à la fiche client (API “Client-visualisation”)


  *Couleur : client géré dans Fidelisa (UUID Fidelisa stocké)

      *appelle le plug-in affichage Fidelisa avec accès direct à la fiche client (API “Client-visualisation”)


  *Rouge : cadeau disponible pour le client

      *appelle le plug-in affichage Fidelisa avec accès direct à la fiche client (API “Client-visualisation”) pour consommation éventuelle du cadeau.



    Les icônes-boutons sont disponibles sur demande.
  ## Appel générique de Fidelisa
    Disponible par l’API “Commerce-visualisation”.
    Cet appel est le plus souvent implémenté à partir d’un bouton d’action symbolisé par l’icône Fidelisa .



  #Informations à stocker

    Pour faire fonctionner Fidelisa, Le logiciel de caisse doit mémoriser les informations suivantes :
    Identifiant du commerce dans Fidelisa
    Identifiants des clients dans Fidelisa (clients gérés dans le TPV)
    Cadeau disponible pour le client


  ---  Support


#Support
Fidelisa met à disposition des éditeurs :

Un support (mail ou téléphone) pour toute question technique ou fonctionnelle relative à l’implémentation de Fidelisa dans le TPV.

Les icônes (plusieurs formats disponibles) pour afficher dans le TPV par exemple l’état du client (inscrit sur Fidelisa ou non).

Des squelettes de code pour les principaux languages permettant de faciliter l’implémentation de l’API.


  ---  Support



  #Requêtes
  ## Logiciel de caisse
    Ces requêtes traitent de sujet concernant uniquement le fournisseur “logiciel de caisse” (ex: la création d’un commerce).

    Dans le header de la requête ajouter les éléments suivants :
  HTTP_FIDELISA_PROVIDER => code Fidelisa fourni par Fidelisa
  HTTP_FIDELISA_PROVIDER_KEY => signature de la requête (voir plus bas)
  HTTP_FIDELISA_JETON => code à usage unique généré par le provider

  ## Commerce
    Ce sont des requêtes qui traitent des sujets d’un commerce en particulier (ex: la création d’un client).

    Dans le header de la requête ajouter les éléments suivants :
  La partie Header du “fournisseur” (voir plus haut)
  HTTP_FIDELISA_APIUSER => code du commerce retourné lors de l’appel du init/shop (champ uuid du json)
  HTTP_FIDELISA_APIUSER_KEY => signature de la requête (voir plus bas)


    <ul id="signTab" class="nav nav-tabs">
      <li class="active"><a show-tab data-target="#sign_ruby, #head_ruby, #get_ruby, #post_ruby" data-toggle="tab">Ruby</a>
      <li class=""><a show-tab data-target="#sign_csharp, #head_csharp, #get_csharp, #post_csharp" data-toggle="tab">C#</a>



    <div id="signTabContent" class="tab-content">
      <div id="sign_ruby" class="tab-pane fade active in">
      <a href="samples/exemple.rb" target="_self">Télécharger exemple ruby</a>

  ## Calcul de la signature
      <div ng-include src="'views/api/sign_ruby.html'">


      <div id="sign_csharp" class="tab-pane fade">
        <a href="samples/exemple.cs" target="_self">Télécharger exemple c#</a>

  ## Calcul de la signature
        <div ng-include src="'views/api/sign_csharp.html'">



  ## Mise en place des entêtes de requêtes (headers)

    <div id="headTabContent" class="tab-content">
      <div id="head_ruby" class="tab-pane fade active in">
        <div ng-include src="'views/api/head_ruby.html'">

      <div id="head_csharp" class="tab-pane fade">
        <div ng-include src="'views/api/head_csharp.html'">



  ## Exemple d'appel de fonction GET

    <div id="getTabContent" class="tab-content">
      <div id="get_ruby" class="tab-pane fade active in">
        <div ng-include src="'views/api/get_ruby.html'">

      <div id="get_csharp" class="tab-pane fade">
        <div ng-include src="'views/api/get_csharp.html'">




  ## Exemple d'appel de fonction POST

    <div id="postTabContent" class="tab-content">
      <div id="post_ruby" class="tab-pane fade active in">
        <div ng-include src="'views/api/post_ruby.html'">

      <div id="post_csharp" class="tab-pane fade">
        <div ng-include src="'views/api/post_csharp.html'">



  ## Format Date et Montant
    Les dates sont au format YYYY-MM-DD
    Pour les montants, le séparateur de décimal est le “.” (point), il n’y a pas de séparateur de milliers.


  ---  Commerce



  #Commerce
  ## Initialisation
    Permet d’initialiser la relation entre le logiciel de caisse et Fidelisa pour un commerce
    POST /api/shops/init
    <h4>Paramètres
    cette requête nécessite les informations d'authentification <a href="" scrollTo="req-pos">"Editeur"</a>
  {
      shop: {
        user_email : "test3@fidelisa.com"
      }
  }
    <h4>Codes de retour
    200 OK
    <h4>Resultat JSON
  {
    title : "test3",
    uuid : "619E8B5AAD5E48138881C5E7774C86B2",
    key : "FrZN6UChpqXBRKVExXVB",
    user_email : "test3@fidelisa.com"
  }
    Le uuid récupéré doit être mémorisé. Il sera utilisé systématiquement dans toutes les requêtes (APIUSER)
    Le key doit également être mémorisé, il servira à calculer APIUSERKEY.


  ## Visualisation
    Permet de visualiser un commerce donné
    GET /api/shops/{uuid commerce}
    <h4>Paramètres
    cette requête nécessite les informations d'authentification <a href="" scrollTo="req-pos">"Editeur"</a>

    <h4>Codes de retour
    200 OK
    <h4>Resultat JSON
  {
    title : "test3",
    uuid : "619E8B5AAD5E48138881C5E7774C86B2",
    key : "FrZN6UChpqXBRKVExXVB",
    user_email : "test@test.com"
  }

  ## Liste
    Permet de récupérer la liste des commerces attachés au fournisseur
    GET /api/shops
    <h4>Paramètres
    cette requête nécessite les informations d'authentification <a href="" scrollTo="req-pos">"Editeur"</a>
    <h4>Codes de retour
    200 OK
    <h4>Resultat JSON
  {
    shops: [
      {
        title : "Test 1",
        uuid : "FD39A1AA85AC4F3FB977DEA5A5786263",
        key : "YAZX2TLVO19DEFVDFF8M",
        user_email : "bva7nntn1zfpn4uhvzaw@fidelisa.com"
      },
      {
        title : "Test 2",
        uuid : "D0114EE251D14C5180991418736A6ACC",
        key : "RCGQDPWTRQS2XZCHWEZB",
        user_email : "9bpxdq5hzzmuuayovbfx@fidelisa.com"
      }
    ]
  }

  ## Categories
    Permet de récupérer un tableau des catégories paramétrées par le commerce dans FIDELISA
    GET /api/shops/categories
    <h4>Paramètres
    cette requête nécessite les informations d'authentification <a href="" scrollTo="req-ven">"Commerce"</a>
    <h4>Codes de retour
    200 OK
    <h4>Resultat JSON
  {
    categories:
    {
      subtotal1: "SUBTOTAL1",
      subtotal2: "SUBTOTAL2",
      subtotal3: "SUBTOTAL3",
      subtotal4: null,
      subtotal5: null,
      subtotal6: null,
      subtotal7: null,
      subtotal8: null,
      subtotal9: null
    }
  }

  ## Programmes
    Permet de récupérer la liste des programmes d'un commerce
    GET /api/shops/programs
    <h4>Paramètres
    cette requête nécessite les informations d'authentification <a href="" scrollTo="req-ven">"Commerce"</a>
    <h4>Codes de retour
    200 OK
    <h4>Resultat JSON
  {
    programs : [
      {
        title : "Carte VIP"
        uuid : "67B222DC2A92672CA8E9D2C6DCB785CB"
      },
      {
        title : "Carte Privilèges"
        uuid : "8853A37D20967C9E099184814805AC31"
      }
    ]
  }




  ---  Clients


  #Clients
  ## Création
    Permet de créer un client pour le commerce
    <div class="well">
      Cas particulier : création d’un client sans email.
      Si le champ email est vide un pseudo mail sera généré automatiquement par l’API

      Les champs birth_day et birth_month sont facultatifs.

    POST /api/customers
    <h4>Paramètres
  {
    customer : {
      email  : "client@monmail.com",
      phone  : "0123456789",
      first_name  : "Pierre",
      last_name  : "Martin",
      birth_day  : 19,
      birth_month  : 10
    }
  }
    cette requête nécessite les informations d'authentification <a href="" scrollTo="req-ven">"Commerce"</a>

    <h4>Codes de retour
    201 Created
    <h4>Resultat JSON
  {
    uuid : "FD39A1AA85AC4F3FB977DEA5A5786263",
    email : "client@monmail.com",
    phone : "0123456789",
    first_name : "Pierre",
    last_name : "Martin"
  }
    Le uuid du client doit être mémorisé pour utilisation lors de l’envoi des ventes etc...

  ## Visualisation
    Permet de voir un client pour le commerce
    GET /api/customers/{uuid client}
    <h4>Paramètres
    cette requête nécessite les informations d'authentification <a href="" scrollTo="req-ven">"Commerce"</a>
    <h4>Codes de retour
    200 OK
    <h4>Resultat JSON
  {
    uuid : "FD39A1AA85AC4F3FB977DEA5A5786263",
    email  : "client@monmail.com",
    phone  : "0123456789",
    first_name  : "Pierre",
    last_name  : "Martin"
  }

  ## Suppression
    Permet de supprimer un client pour le commerce
    DELETE /api/customers/{uuid client}
    <h4>Paramètres
    cette requête nécessite les informations d'authentification <a href="" scrollTo="req-ven">"Commerce"</a>
    <h4>Codes de retour
    200 OK
    <h4>Resultat JSON

  ## Liste
    Permet de récupérer la liste des clients d’un commerce
    GET /api/customers
    <h4>Paramètres
    cette requête nécessite les informations d'authentification <a href="" scrollTo="req-ven">"Commerce"</a>
    <h4>Codes de retour
    200 OK
    <h4>Resultat JSON
  {
    customers : [
      {
        uuid : "FD39A1AA85AC4F3FB977DEA5A5786263",
        email : "client@monmail.com",
        phone : "0123456789",
        first_name : "Pierre",
        last_name : "Martin"
      }
    ]
  }

  ## Cartes
    Permet de récupérer la liste des cartes d'un client
    GET /api/customers/{uuid client}/cards
    <h4>Paramètres
    cette requête nécessite les informations d'authentification <a href="" scrollTo="req-ven">"Commerce"</a>
    <h4>Codes de retour
    200 OK
    <h4>Resultat JSON
  {
    cards : [
      {
        uuid : "1DA03451947C4B91A0EAE4099AD01E26",
        title : "Carte Privilèges",
        points : 20,
        expired_at : "2015-06-14"
      }
    ]
  }

  ## Date d'expiration
    Permet de modifier la date d'expiration d'une carte (ou de la carte si unique) d'un client
    POST /api/customers/{uuid client}/cards/expired_at
    <h4>Paramètres
  Avec un numéro de carte spécifique
  {
      id  : "1DA03451947C4B91A0EAE4099AD01E26",
      date : "2014-05-15"
  }
  Avec un numéro de carte spécifique et remise à zero des points de la carte
  {
      id  : "1DA03451947C4B91A0EAE4099AD01E26",
      date : "2014-06-20",
      reset : true
  }
  Sans numéro de carte spécifique (s'applique à la carte du client)
  {
      date : "2014-06-20"
      reset : false
  }


    cette requête nécessite les informations d'authentification <a href="" scrollTo="req-ven">"Commerce"</a>
    <h4>Codes de retour
    200 OK
    <h4>Resultat JSON
  {}


  ---  Rule Basis


  #Rule Basis
  ## Rule basis-commerce
    Permet de récupérer la liste des "bases" pour un commerce
    GET /api/rulebasis
    <h4>Paramètres
    cette requête nécessite les informations d'authentification <a href="" scrollTo="req-ven">"Commerce"</a>
    <h4>Codes de retour
    200 OK
    <h4>Resultat JSON
  {
    rulebasis : [
      {
        type : "SubTotal1",
        item : "N/A",
        exclude_discount : "f"
      },
      {
        type : "Item",
        item : "1234,4567",
        exclude_discount : "true"
      }
    ]
  }
    Liste des types : Passage, TotalAmount, SubTotal1, SubTotal2, SubTotal3, SubTotal4, SubTotal5, SubTotal6, SubTotal7, SubTotal8, SubTotal9, Item

  ## Rule basis-client
    Permet de récupérer la liste des "bases" à considérer pour le client
    GET /api/rulebasis?uuid_customer={UUID du customer}
    <h4>Paramètres
    cette requête nécessite les informations d'authentification <a href="" scrollTo="req-ven">"Commerce"</a>
    <h4>Codes de retour
    200 OK
    <h4>Resultat JSON
  {
    rulebasis : [
      {
        type : "Item",
        item : "1234",
        exclude_discount   : "true"
      }
    ]
  }


  ---  Ventes


  #Ventes
  ## Ajout
    Permet d’ajouter des resultats
    POST /api/sales/
    <h4>Paramètres
  {
    bill :
    {
      total : "123.50",
      date : "2013-01-15",
      uuid_customer : "FD39A1AA85AC4F3FB977DEA5A5786263",
      details : [
        {
          type : "SubTotal1",
          amount : "123.50",
          quantity : "2"
         },
        {
          type  : "Item",
          item  : "1234",
          amount  : "12.50",
          quantity  : "2"
        }
      ]
    }
  }

    <h4>Codes de retour
    201 CREATED404 NOT FOUND l’UUID client n’a pas été trouvé
    <h4>Resultat JSON
    S’il n’y a pas d’erreur :
  {
    bill :
    {
      date : "2013-01-15",
      total : "123.5"
    }
  }

    Si des lignes sont en anomalie, elles sont retournées avec la raison du rejet:
  {
    bill :
    {
      date : "2013-01-15",
      total : "123.5"
    },
    errors : [
      {
        type  : "Item",
        item  : "11234",
        amount  : "12.50",
        quantity  : "2",
        error  : "Not Use"
      }
    ]
  }


  ---  Cadeaux


  #Points
  ## Ajout
    Permet d'ajouter des résultats en points
    POST /api/corrections
    <h4>Paramètres
    cette requête nécessite les informations d'authentification <a href="" scrollTo="req-ven">"Commerce"</a>
  Avec un identifiant de carte connu
  {
    "correction" : {
      "points" : 20,
      "customer_id" : "FD39A1AA85AC4F3FB977DEA5A5786263",
      "card_id" : "1DA03451947C4B91A0EAE4099AD01E26"
    }
  }
  Si le client n'a qu'une seule carte, celle-ci sera créditée automatiquement
  {
    "correction" : {
      "points" : 20,
      "customer_id" : "FD39A1AA85AC4F3FB977DEA5A5786263"
    }
  }

    <h4>Codes de retour
    200 OK422 si une erreur est survenue



  ---  Cadeaux


  #Cadeaux
  ## Client
    Permet de récupérer la liste des cadeaux consommables par le client.
    Le paramètre “used” permet de sélectionner les cadeaux déjà offerts au client.
    GET /api/gifts?uuid_customer={UUID du customer}&amp;used={true ou false}
    <h4>Paramètres
    cette requête nécessite les informations d'authentification <a href="" scrollTo="req-ven">"Commerce"</a>
    <h4>Codes de retour
    200 OK404 NOT FOUND si l’UUID du client n’a pas été trouvé
    <h4>Resultat JSON
  {
    gifts : [
      {
        uuid : "FD39A1AA85AC4F3FB977DEA5A5786263",
        title : "10€ de bon d’achat",
        points : 123
      }
    ],
  }
    Remarques
    La propriété "points", du retour correspond au nombre de points collectés sur la carte correspondant au cadeau. Cette propriété n’est disponible que lors de l’appel des cadeaux disponibles.


  ## Consommation
    Permet d’indiquer que le client a consommé le cadeau
    POST /api/gifts/award
    <h4>Paramètres
    cette requête nécessite les informations d'authentification <a href="" scrollTo="req-ven">"Commerce"</a>
  {
    uuid : "UUID_CADEAU"
    uuid_customer : "FD39A1AA85AC4F3FB977DEA5A5786263"
  }

    <h4>Codes de retour
    200 OK400 si une erreur est survenue404 NOT FOUND si l’UUID du client n’a pas été trouvé
    <h4>Resultat JSON
    Si Status = 400
  {
    error : "Le client ne peut pas consommer ce cadeau"
  }

  ## Restauration
    Permet d’annuler la consommation d’un cadeau
    DELETE /api/gifts/<UUID_CADEAU>?uuid_customer={uuid customer}
    <h4>Paramètres
    cette requête nécessite les informations d'authentification <a href="" scrollTo="req-ven">"Commerce"</a>
    <h4>Codes de retour
    200 OK400 si une erreur est survenue404 NOT FOUND si l’UUID du client n’a pas été trouvé
    <h4>Resultat JSON
    Si Status = 400:
  {
    error : "Le client ne peut pas restaurer ce cadeau"
  }


  ---  Notifications


  #Notifications
  ## Envoi
    Permet d’envoyer une notification à un client ou à tous les clients d’un programme de fidelité
    POST /api/notifications
    <h4>Paramètres
    cette requête nécessite les informations d'authentification <a href="" scrollTo="req-ven">"Commerce"</a>
  Pour un client unique
  {
    customer : "FD39A1AA85AC4F3FB977DEA5A5786263",
    alert : "Message au client"
  }
  pour un programme
  {
    program : "FD39A1AA85AC4F3FB977DEA5A5786263",
    alert : "Message aux clients"
  }
  pour un ensemble de clients avec des urls spécifiques
  customers : {
      "D407587D800ECC6C629A52CD204C6E61" : "http://fidelisa.com/1",
      "FD39A1AA85AC4F3FB977DEA5A5786263" : "http://fidelisa.com/2"
      },
  alert : "Message aux clients"

    <h4>Codes de retour
    200 OK

    <h4>Resultat JSON





  # Authentication

  > To authorize, use this code:

  ```ruby
  require 'kittn'

  api = Kittn::APIClient.authorize!('meowmeowmeow')
  ```

  ```python
  import kittn

  api = kittn.authorize('meowmeowmeow')
  ```

  ```shell
  # With shell, you can just pass the correct header with each request
  curl "api_endpoint_here"
    -H "Authorization: meowmeowmeow"
  ```

  > Make sure to replace `meowmeowmeow` with your API key.

  Kittn uses API keys to allow access to the API. You can register a new Kittn API key at our [developer portal](http://example.com/developers).

  Kittn expects for the API key to be included in all API requests to the server in a header that looks like the following:

  `Authorization: meowmeowmeow`

  <aside class="notice">
  You must replace <code>meowmeowmeow</code> with your personal API key.
  </aside>

  # Kittens

  ##  Get All Kittens

  ```ruby
  require 'kittn'

  api = Kittn::APIClient.authorize!('meowmeowmeow')
  api.kittens.get
  ```

  ```python
  import kittn

  api = kittn.authorize('meowmeowmeow')
  api.kittens.get()
  ```

  ```shell
  curl "http://example.com/api/kittens"
    -H "Authorization: meowmeowmeow"
  ```

  > The above command returns JSON structured like this:

  ```json
  [
    {
      "id": 1,
      "name": "Fluffums",
      "breed": "calico",
      "fluffiness": 6,
      "cuteness": 7
    },
    {
      "id": 2,
      "name": "Isis",
      "breed": "unknown",
      "fluffiness": 5,
      "cuteness": 10
    }
  ]
  ```

  This endpoint retrieves all kittens.

  ## # HTTP Request

  `GET http://example.com/api/kittens`

  ## # Query Parameters

  Parameter | Default | Description
  --------- | ------- | -----------
  include_cats | false | If set to true, the result will also include cats.
  available | true | If set to false, the result will include kittens that have already been adopted.

  <aside class="success">
  Remember — a happy kitten is an authenticated kitten!
  </aside>

  ##  Get a Specific Kitten

  ```ruby
  require 'kittn'

  api = Kittn::APIClient.authorize!('meowmeowmeow')
  api.kittens.get(2)
  ```

  ```python
  import kittn

  api = kittn.authorize('meowmeowmeow')
  api.kittens.get(2)
  ```

  ```shell
  curl "http://example.com/api/kittens/2"
    -H "Authorization: meowmeowmeow"
  ```

  > The above command returns JSON structured like this:

  ```json
  {
    "id": 2,
    "name": "Isis",
    "breed": "unknown",
    "fluffiness": 5,
    "cuteness": 10
  }
  ```

  This endpoint retrieves a specific kitten.

  <aside class="warning">If you're not using an administrator API key, note that some kittens will return 403 Forbidden if they are hidden for admins only.</aside>

  ## # HTTP Request

  `GET http://example.com/kittens/<ID>`

  ## # URL Parameters

  Parameter | Description
  --------- | -----------
  ID | The ID of the kitten to retrieve
