### Le problème
![[user_login.png]]
notes:
Nos sites web sont servis par le protocole HTTP.

Ce dernier est sans état(stateless), ce qui signifie que lorsqu'on accède à une page d'un site web, celui-ci ne peut pas, par défaut, conserver des informations d'état à notre sujet.

`Comment peut-on alors maintenir les achats dans un panier d'achat ?`

`Comment peut-on garder l'utilisateur connecté ?`

---
#### Méthode de stockage web
![[website_storage.png | 512x384]]
notes:
Le navigateur offre de nombreuses options pour stocker nos données ou les conserver à travers l'accès aux différentes pages de notre site.

Certains peuvent garder plus ou moins d'informations et auront une durée de vie plus ou moins grande.

Les cookies sont un excellent moyen de partager l'état du client avec le serveur. Ils sont principalement utilisés pour l'authentification, la personnalisation et le pistage.

---
### Qu'est-ce qu'un cookie ?
![[cookie_image.png]]
notes:
Les cookies sont de petits fichiers de données stockés sur l'ordinateur de l'utilisateur par le navigateur web.

Les cookies sont un moyen courant de stocker des données de petite taille.

La plupart des navigateurs limitent le nombre total de cookies par domaine à environ 20 à 50.

---

### Types de cookies
![[diff_cookies.png]]
notes:
- **Cookies de session** : Ils sont temporaires et supprimés lorsque le navigateur est fermé. Habituellement, ils sont utilisés pour maintenir le panier d'achats ou gérer des configurations temporaires.
- **Cookies persistants** : Ils ont une durée de vie prolongée et sont habituellement utilisés pour mémoriser les préférences des utilisateurs ou les informations de connexion.
- **Cookies tiers** : Cookies créés par un autre domaine que celui visité, qui tentent de suivre le comportement des utilisateurs afin de leur présenter de la publicité ajustée pour eux.

Le but des cookies créés par le domaine principal est de donner une meilleure expérience utilisateur. Ceux des tiers visent à sous-tirer des informations sur les utilisateurs afin de monétiser leur comportement.

---
### Création et interaction
Requête HTTP(Header):
```HTTP
Set-Cookie: loginId="abc123";
Expires=Wed, 21 Oct 2025 07:28:00 GMT; 
...
```

notes:
Un cookie est défini par une paire clé-valeur. Son comportement sera contrôlé davantage par différents attributs.

L'attribut `Expires` indique le temps de vie maximal d'un cookie sous la forme d'une date HTTP (GMT ou UTC). Si `Expires` n'est pas spécifié, le cookie devient un cookie de session.

---
### Autres attributs
```HTTP
Set-Cookie: ... Secure; HttpOnly; SameSite=Strict
```
notes:
L'attribut `Secure` oblige l'accès par HTTPS, permettant d'encrypter les transferts de cookies, ce qui protège contre l'interception par des attaquants sur des réseaux non sécurisés.

L'attribut `HttpOnly` empêche l'accès au cookie à partir du JavaScript (DOM). Cela permet de protéger contre les attaques XSS (Cross-Site Scripting), où un attaquant pourrait injecter du code malveillant pour accéder aux données du cookie.

L'attribut `SameSite` détermine si un cookie est envoyé avec des requêtes provenant d'autres sites(nom de domaine), ce qui aide à protéger contre les attaques CSRF (Cross-Site Request Forgery).

---
### Activité en javascript
```js
const d = new Date()
d.setTime(d.getTime() + (31*24*60*60*1000)) // 31 jours
let expires = "expires="+ d.toUTCString()
let him_cook = "loginId" + "=" + username + ";"
document.cookie =  him_cook + expires + ";path=/"
```

notes:
https://cosmo.zip/pub/cosmos/bin/python