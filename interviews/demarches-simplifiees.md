Entretien Démarches simplifiées
===
Le code est développé sur la machine :

Le disque dur est-il chiffré ?
Tous les DD sont chiffrés

Quelles données de production sur l’ordinateur ?
Pas de mot de passe chiffré
Pas de données de prod
Toutes les nuits on fait des backup, aujourd'hui c'est à la main, une copie du backup est anonymisée et déployée sur le staging, pg anonymizer plus tard
On a chacun un laptop connecté à la prod
Des Macs et des Linux

Comment réagissez-vous à une CVE qui apparaît sur une version de Mac ?
Nope, on a des Macs et Linux
Laxistes sur les postes de développement

Les modifications sont committées en local :
Code sur Github, PR sur main, on peut pas merge direct sur main
CI sur Github
On a un gitlab sur notre infra privée
Le build qui passe en prod est
On 
Les commits sont-ils signés ?
Nope, on y pense


Les modifications sont poussées en ligne :
Quels sont vos repositories ? Sont-ils publiques ? 
ds-proxy, depo-ansible sur gitlab, depo CLI de déploiement
Comment prévenez-vous le leaking de credentials ? Comment y réagissez-vous ?
Robot Github qui prévient,
Dans un K7, une mémoire d'un appel HTTP, un mock d'une API
On a à disposition les numéros de tout le monde
On remonte au chef de projet et RSSI 

Comment gérez-vous la mise à jour des bibliothèques utilisées ?
github : dependabot, 

Le code est buildé :
Comment est-il buildé ? Le build est-il signé ?

Le build est déposé sur le serveur :
Comment est-il déposé ? Manuellement ?

L’application est à jour en ligne :
Quelles mesures de sécurité web mettez-vous en place, de manière générale ?
Bug bounty
Rails => protections du framework de base, sanitizing des inputs, CSP, antivirus Clamab, XSS, headers de sécurité, verrouiller les iframes
Infra 
Full bouclier DDoS OVH, firewall en entrée: stormshield, req-limiting (sur les load balancer d'entrée)
Rails vient sur PostgreSQL, 


Y a-t-il une politique de mots de passe ? Pour vos utilisateurs ? Pour votre équipe ?
Tous les outils : on force le 2FA (Github, Gitlab, Sentry, prestataire de mail, logiciel de support)
Côté équipe pour les comptes persos dans les outils externes, chacun choisit
Pour l'infra sur les jetons maîtres d'accès aux API, c'est dans un vault
Connexion : France Connect, France Connect agent, le rôle le plus fort c'est manager, accès au dashbord (2FA)
Rôle administrateur : règles de mdp plus fortes 
Rôle normal : 8 caractères
Pour les usagers niveau 2/3, on utilise library dropbox : compare ton mdp avec les mots de passe avec dictionnaires

Pass key

Rien contre le phishing

Forcer au niveau client et serveur

Les emails envoyés sont toujours un lien vers l'applicatif, jamais d'infos stockées dans les mails

Des mesures particulières contre le phishing ? Les injections SQL ? Failles XSS ? Attaque type MITM ?
Avez-vous des mesures de disponibilité de votre produit ?
Oui, updown.io
Mais repère pas forcément si des sous-services sont down (bucket storage, et serveur d'envoi de mail)


Code est développé en local, on pousse sur Github, les tests passent, on pousse sur main, et à un moment on décide qu'on veut pousser en prod, on a un script "packet package", on lui dit la branche et le commit à partir desquels créer le package, il exécute le code sur le gitlab privé, il fetch le commit sur Github, il créé un package debian, puis commande qui deploy le package en staging ou en prod. Les commandes sont lancées depuis une CLI entre le poste de dev et le gitlab, 2FA.
Exigence du RSSI : migrer vers des machines avec uniquement accès à la prod
