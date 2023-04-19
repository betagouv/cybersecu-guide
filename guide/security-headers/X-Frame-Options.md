# X-Frame-Options

## Le problème
Un site pirate pourrait choisir d'afficher votre site dans une `iframe`, choisir un nom de domaine similaire au vôtre (comme `http://example-gouv.fr`), et ainsi usurper l'identité de votre site. Il faut donc que votre site trouve un moyen d'indiquer, par exemple, qu'il ne "souhaite pas" être affiché dans un iframe depuis un autre site.

## La solution
L'en-tête de réponse HTTP X-Frame-Options peut être utilisé afin d'indiquer si un navigateur devrait être autorisé à afficher une page au sein d'un élément `<frame>`, `<iframe />`, `<embed>` ou `<object>`. Les sites peuvent utiliser cet en-tête afin d'éviter les attaques de clickjacking (ou « détournement de clic ») pour s'assurer que leur contenu ne soit pas embarqué dans d'autres sites.

## L'implémentation
### Express
```javascript
app.use((req, res, next) => {
	res.header("X-Frame-Options", "deny"); // le navigateur refusera d'afficher votre site dans un iframe
	next();
});
```

### Django
- Ajouter django.middleware.clickjacking.XFrameOptionsMiddleware à MIDDLEWARES

- Ajouter dans `settings.py`:
```python
# Le navigateur refusera d'afficher votre site dans un iframe
X_FRAME_OPTIONS='DENY'
```

## Ressources
- [https://developer.mozilla.org/fr/docs/Web/HTTP/Headers/X-Frame-Options](https://developer.mozilla.org/fr/docs/Web/HTTP/Headers/X-Frame-Options)
