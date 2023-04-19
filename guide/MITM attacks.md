# Protection contre les attaques MITM
## Description de l'attaque
Une attaque MITM (Man In The Middle) consiste, pour un attaquant, à se placer sur le réseau entre un utilisateur et le site web. Il peut ainsi observer les requêtes faites, les modifier, usurper l’identité du site. La meilleure protection contre cette attaque est le protocole HTTPS. Contrairement au protocole HTTP, il assure à vos utilisateurs :
- qu'ils communiquent bien avec votre site (et non une version malicieuse de votre site hébergée sur un ordinateur pirate, par exemple)
- qu'un pirate sur votre réseau Wi-fi (par exemple) ne pourra pas lire vos communications (ni a fortiori les modifier)

## Actions
### Autoriser la connexion en HTTPS à votre application web
Si votre application est hébergée sur Scalingo, la connexion est automatiquement autorisée en HTTPS.

Sinon, contactez Philippe Libat.
- ✅ le site ne renvoie pas d'erreur lorsque vous accédez à https://example.gouv.fr.

### Forcer **le serveur** à rediriger l'appel en HTTPS lorsque vous tentez d'y accéder en HTTP
Si votre application est hébergée sur Scalingo :
- Accédez à [https://dashboard.scalingo.com/apps](https://dashboard.scalingo.com/apps)
- Sélectionnez votre application web
- Sélectionnez l'onglet `Settings`, puis `Routing`, et cocher l'option : `Force HTTPS`

Sinon, contactez Philippe Libat.

- ✅ lorsque vous tentez d'accéder à http://example.gouv.fr, le site vous renvoie https://example.gouv.fr.

### Forcer **le client** à rediriger l'appel en HTTPS lorsque vous tentez d'y accéder en HTTP


- ✅ lorsque vous tentez d'accéder à http://example.gouv.fr, le site vous renvoie https://example.gouv.fr.
