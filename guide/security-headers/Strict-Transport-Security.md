# Strict-Transport-Security

## Le problème
Lorsque vous tentez d'accéder à un site web via le protocole HTTP (par exemple via l'URL http://example.gouv.fr), votre navigateur va effectuer un appel au serveur en HTTP. Selon les paramètres de votre serveur, celui-ci répondra éventuellement en HTTPS, si la redirection est forcée, ou bien en HTTP.
Seulement, quand bien même la redirection serait faite côté serveur, rien n'empêche un attaquant d'intercepter la requête initiale, avant qu'elle ne parvienne au serveur : à ce moment-là, l'appel est bien en HTTP, donc en clair, et l'attaquant est libre de lire le contenu de la requête, de répondre à la place du serveur, donc éventuellement de l'usurper.
La meilleure protection consiste donc à forcer l'appel en HTTP au niveau du serveur ET au niveau du navigateur.

## La solution
Le header `Strict-Transport-Security`, envoyé par le serveur lorsqu'il répond à votre requête, indique au navigateur que, pendant un certain temps (spécifié dans le header), chaque appel en HTTP à ce domaine devra être converti en appel HTTPS.

## L'implémentation
### Express
```javascript
app.use((req, res, next) => {
	res.header("Strict-Transport-Security", "max-age=31536000"); // convertit les appels en HTTPS pendant 1 an 
	next();
});
```

### Django
- Ajouter django.middleware.security.SecurityMiddleware à MIDDLEWARES

- Ajouter dans `settings.py`:
```python
# Convertit les appels en HTTPS pendant 1 an
SECURE_HSTS_SECONDS=31536000 
```
