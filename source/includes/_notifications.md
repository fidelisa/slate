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

Permet d’envoyer une notification à un client ou à tous les clients d’un programme

### Authentification

Type : [Shop] (#shop)

### HTTP Request

`POST /api/notifications`

### Query Parameters
***Cas 1 : pour un client unique***

Parameter | Type | Description
--------- | --------- | -----------
customer | body | UUID du client
alert | body | Texte du message


***Cas 2 : pour tous clients d'un programme***

Parameter | Type | Description
--------- | --------- | -----------
program | body | UUID du programme
alert | body | Texte du message

***Cas 3 : pour des clients***

Parameter | Type | Description
--------- | --------- | -----------
customers | body | Tabelau de clients
alert | body | Texte du message

### Return code
Code | Description
------- | ---------
200 | OK
