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

Ces requêtes nécessitent les droits lieu (ex: la création d’un client).

Dans le header de la requête ajouter les éléments suivants :

Nom |  Description
--------- | -----------
FIDELISA_JETON  | code à usage unique généré par le provider
FIDELISA_PROVIDER |  code Fidelisa fourni par Fidelisa
FIDELISA_PROVIDER_KEY  | signature de la requête
FIDELISA_APIUSER | code du commerce retourné lors de l’appel du init/shop (champ uuid du json)
FIDELISA_APIUSER_KEY | [signature de la requête](#signature)
