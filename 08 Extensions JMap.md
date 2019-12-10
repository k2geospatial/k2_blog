---
layout: default
title: Extensions de JMap
nav_order: 8
---

# Extensions JMap

Les fonctionnalités standard de JMap peuvent être étendues par de nouvelles fonctions spécialisées. Ceci s'effectue à l'aide des extensions JMap. Une extension JMap est un module complémentaire qui peut se greffer à JMap Server et/ou aux applications JMap afin de fournir les nouvelles fonctionnalités désirées. Certaines extensions JMap existent déjà et sont disponibles en tant que produits séparés, tandis que d'autres seront disponibles dans le futur. Les organisations peuvent aussi développer leurs propres extensions en utilisant le SDK JMap.

La section des extensions de JMap Admin montre la liste des extensions présentes pour chaque type d'extension : Serveur, client, web, mobile.



## Extensions Server

Les extensions JMap Server ajoutent de nouvelles fonctionnalités du côté serveur. Elles peuvent inclure leurs propres interfaces de configuration, qui sont intégrées dans JMap Admin. Simplement cliquer sur le nom d'une extension serveur pour accéder à son interface de configuration.

Les extensions serveur peuvent être activées ou désactivées en appuyant sur les boutons **Activer** et **Désactiver** respectivement. Les extensions désactivées sont inactives et ne traitent pas de requêtes. Les extensions peuvent aussi être réinitialisées en appuyant sur le bouton **Réinitialiser**. Dans ce cas, elles sont arrêtées et redémarrées, ce qui peut être utile si une extension doit par exemple lire des fichiers de configuration modifiés. 



## Extensions Client

Les extensions client JMap ajoutent des fonctionnalités aux applications JMap Pro. De façon générale, une extension ajoute une nouvelle barre d'outils ou de nouveaux items de menu à l'application. En utilisant l'outil de déploiement d'applications, vous pouvez sélectionner les extensions qui seront incluses dans une application JMap Pro. Consultez la section [Déploiement d'applications JMap Pro](09 Déploiement d'applications JMap.md) pour plus de détails à ce sujet. Les extensions client de JMap sont énumérées dans cette section à titre indicatif seulement.



## Extensions Web

Les extensions JMap Web ajoutent des fonctionnalités aux applications JMap Web. Les extensions JMap Web sont énumérées dans cette section à titre indicatif seulement.



## Permissions des extensions



### Permissions administrateur

Les permissions administrateur des extensions de JMap Server définissent les droits d'administration de l'extension par les utilisateurs autorisés à utiliser JMap Admin. Les extensions client, web et mobile ne sont pas affectées par des permissions. Pour plus d'information sur les concepts de permissions et rôles d'administration dans JMap Admin, consultez la section [Gestion des permissions](10 Sécurité.md).

| **Permissions**         |                                                              |
| ----------------------- | ------------------------------------------------------------ |
| Administrer l'extension | Permet à un administrateur d'accéder aux sections de configuration de l'extension et de faire des modifications à la configuration. |

 

