#Lexique
##Definitions
***Vocabulaire***

Nom | Définition
------- | ------
Fournisseur | Partenaires, Editeur de logiciel, Agence, ...
Point de vente | Point de vente, Commerce, eCommerce, ...
Client | Client d'un point de vente

***Paramètres des requêtes***

Type | Definitions
-----| --------
body | Elément du JSON envoyé au serveur
path | Elément de l'url
query | Paramètres de l'url

## Date et Montant
Les dates sont au format YYYY-MM-DD

Le séparateur de décimal des montants est le “.” (point), il n’y a pas de séparateur de milliers.

## Boolean
Les filtres des requêtes de type boolean ont trois positions :

Valeur du filtre | Réponse de la requête
---------------- | ------------------------
t | les éléments qui valident le filtre
f | les éléments qui ne valident pas le filtre
  | tous les éléments.

### Exemple
Si je souhaite les gains spéciaux consomés, je vais utiliser la requête suivante:

`/api/customers/{customer_id}/specialgains?user=t`

Pour les non consomés :

`/api/customers/{customer_id}/specialgains?user=f`

Pour tous les gains :

`/api/customers/{customer_id}/specialgains`
