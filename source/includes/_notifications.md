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
