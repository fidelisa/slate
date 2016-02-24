#Points
##Ajout/Remplace
Permet d'ajouter des points à une carte ou de remplacer les points d'une carte.

>Avec un identifiant de carte connu

```json
{
  "correction" : {
    "points" : 20,
    "customer_id" : "FD39A1AA85AC4F3FB977DEA5A5786263",
    "card_id" : "1DA03451947C4B91A0EAE4099AD01E26",
    "replace_points": true    
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
*Correction*

Parameter | Type | Description
--------- | --------- | -----------
points | body | Nombre de points à créditer sur la carte
customer_id | body | UUID du client
card_id | body | Carte du client (facultatif)
replace_points | body | Remplace les points existants (facultatif)
reason | body | Raison de la mise en place des points (facultatif)


### Return code
Code | Description
------- | ---------
201 | CREATED
