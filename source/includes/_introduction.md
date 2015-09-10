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
