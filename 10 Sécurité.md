---
layout: default
title: Sécurité
nav_order: 10
---

# Sécurité

La gestion de la sécurité dans JMap englobe plusieurs éléments.

La gestion des identités peut être faite par JMap Server ou être déléguée à un autre système tel qu'un annuaire LDAP ou Microsoft Active Directory. Consultez les sections [Gestionnaires d'utilisateurs](#Gestionnaires d'utilisateurs) et [Gestion des comptes d'utilisateurs et des groupes](#Gestion des comptes d'utilisateurs et des groupes) pour plus d'information. JMap permet aussi l'authentification unique pour JMap Pro. Consultez la section [Authentification unique](#Authentification unique) pour plus d'information.

La gestion des accès, ou gestion des permissions, est appliquée sur l'ensemble des ressources prises en charge par JMap. Cela inclut les accès des utilisateurs des applications JMap et aussi les accès des administrateurs de JMap. Consultez la section [Gestion des permissions](#Gestion des permissions) pour plus d'information.

JMap permet facilement l'utilisation du protocole HTTPS pour JMap Admin et pour les différentes applications. Consultez la section [Utilisation de HTTPS avec JMap](#Utilisation de HTTPS avec JMap) pour plus d'information.



## Gestionnaires d'utilisateurs

Vous pouvez accéder à la configuration du gestionnaire d'utilisateurs dans JMap Admin en appuyant sur **Utilisateurs / Groupes** à partir de la section JMap Server. Sélectionnez l'onglet **Gestionnaire**.

Le gestionnaire d'utilisateurs permet de définir comment JMap gère les compte d'utilisateurs et les groupes. Il existe deux façons de gérer ces informations avec JMap :

- En utilisant la base de données de comptes d'utilisateurs de JMap, vous créez et supprimez les comptes d'utilisateurs directement à partir de JMap Admin;
- En vous connectant à une base de données de comptes d'utilisateurs existante telle qu'un système Windows Active Directory, un système compatible avec LDAP ou une base de données relationnelle.

Il est aussi possible combiner plusieurs systèmes pour les utiliser simultanément (p. ex. la base de données de JMap et Windows Active Directory). Les différents systèmes sont alors utilisés comme un seul système. Quand JMap Server se connecte à une base de données existante, la gestion des comptes d'utilisateurs est simplifiée car aucun compte ni groupe d'utilisateurs n'ont besoin d'être créés et gérés dans JMap.

Les sections suivantes décrivent chacune des options disponibles.



### Gestionnaire d'utilisateurs JMap DB

Ce type de gestion des comptes d'utilisateurs enregistre les utilisateurs et groupes directement dans la base de données System de JMap Server, ou dans une base de données externe qui comporte les tables et champs requis. L'administrateur JMap doit créer et gérer tous les comptes et groupes d'utilisateurs.

À partir de la section **Utilisateurs / Groupes**, cliquez sur l'onglet **Gestionnaire**. Sélectionnez **Gestionnaire d'utilisateurs JMap DB** afin d'indiquer que les comptes d'utilisateurs seront gérés à l'intérieur d'une base de données relationnelle. Pour stocker les informations dans la base de données System de JMap Server, sélectionnez l'option **Base de données de JMap Server**.

Vous pouvez aussi utiliser toute base de données relationnelle qui contient au moins les tables et champs requis, en sélectionnant l'option **Base de données externe**. Lorsque vous le faites, une interface s'affiche, vous permettant de spécifier les paramètres de configuration. En utilisant l'interface de configuration, sélectionnez la base de données à utiliser. Sélectionnez ensuite les tables et champs qui contiennent les diverses informations relatives aux utilisateurs et aux groupes. Au besoin, vous pouvez sélectionner le mode lecture seule pour empêcher les informations des comptes d'être modifiées par JMap Admin.

Une fois cette configuration définie, vous pouvez créer, modifier et supprimer des comptes d'utilisateurs directement à partir de JMap Admin.



### Gestionnaire d'utilisateurs Active Directory

Vous pouvez vous connecter à Windows Active Directory (en lecture seulement) en sélectionnant **Gestionnaire d'utilisateurs Active Directory** sous **Gestionnaire d'utilisateurs**. Lorsque vous sélectionnez cette option, une nouvelle interface s'affiche, vous permettant de spécifier les paramètres de configuration. 

| **Active Directory**                      |                                                              |
| ----------------------------------------- | ------------------------------------------------------------ |
| Adresse du serveur                        | Adresse du serveur contrôleur de domaine Windows configuré avec Active Directory. |
| DN                                        | Identifiant unique (Distinguished Name) permettant de définir la racine de l'annuaire. Composé d'une liste d'entrées DC (Domain Component). Exemple: dc=ABC,dc=COM |
| Domaine                                   | Nom du domaine Windows (p.e. ABC.COM).                       |
| Utilisateur / SPN                         | Nom de l'utilisateur que JMap Server utilisera pour se connecter au Active Directory. Il est conseillé de créer un utilisateur spécialement pour les besoins de JMap. Son mot de passe ne devrait jamais expirer.Si vous souhaitez utiliser l'authentification unique, vous devrez créer un SPN (Service Principal Name) associé à cet utilisateur. Voir [Authentification Unique](#Authentification unique) pour plus de détails. |
| Mot de passe                              | Mot de passe de l'utilisateur que JMap Server utilisera pour se connecter au Active Directory. |
| Mot de passe admin.                       | Un utilisateur nommé administrator doit toujours exister dans JMap. S'il n'existe pas d'utilisateur administrator dans l'Active Directory, JMap se chargera d'en simuler un. Dans un tel cas, fournir le mot de passe associé à cet utilisateur. Si jamais l'utilisateur administrator existe dans l'Active Directory et qu'un mot de passe est saisi, ce dernier sera ignoré. |
| Activer l'authentification unique         | Permet d'activer l'authentification unique. Voir [Authentification Unique](#Authentification unique) pour plus de détails. |
| Configuration LDAP(9 paramètres suivants) | Active Directory est basé sur le protocole LDAP. Les paramètres LDAP qui sont configurés par défaut sont ceux qui sont le plus souvent en application avec Active Directory. Par contre, si ces paramètres ne correspondent pas à ceux utilisés, il est possible de modifier les valeurs. |
| Taille maximale de la page                | Active Directory limite la taille de transactions à un nombre maximal d'enregistrements à la fois (taille de la page). La valeur de ce paramètre ne doit pas dépasser la taille maximale autorisée par Active Directory (1000 est la valeur par défaut dans Active Directory). Une taille trop petite peut réduire les performances. Une taille plus grande que la limite autorisée causera des données manquantes dans la liste des utilisateurs. |



### Gestionnaire d'utilisateurs JMap LDAP

Vous pouvez vous connecter à tout annuaire compatible avec LDAP (en lecture seulement). Il existe de nombreux annuaires compatibles avec LDAP sur les systèmes Unix, Linux et Windows.

Afin d'utiliser cette option, sélectionnez **Gestionnaire d'utilisateurs JMap LDAP** sous **Gestionnaire d'utilisateurs**. Lorsque vous sélectionnez cette option, une nouvelle interface s'affiche, vous permettant de spécifier les paramètres de configuration. 

| **Gestionnaire d'utilisateurs LDAP** |                                                              |
| ------------------------------------ | ------------------------------------------------------------ |
| URL du serveur                       | Adresse du serveur LDAP.                                     |
| DN                                   | Identifiant unique (Distinguished Name) permettant de définir la racine de l'annuaire. Composé d'une liste d'entrées DC (Domain Component). <br />**Exemple** : <br />dc=ABC,dc=COM |
| Utilisateur                          | Nom de l'utilisateur que JMap Server utilisera pour se connecter à l'annuaire LDAP. Il est conseillé de créer un utilisateur spécialement pour les besoins de JMap. Son mot de passe ne devrait jamais expirer. |
| Mot de passe                         | Mot de passe de l'utilisateur que JMap Server utilisera pour se connecter à l'annuaire LDAP. |
| Mot de passe admin.                  | Un utilisateur nommé **administrator** doit toujours exister dans JMap. S'il n'existe pas d'utilisateur **administrator** dans l'annuaire LDAP, JMap se chargera d'en simuler un. Dans un tel cas, fournir le mot de passe associé à cet utilisateur. Si jamais l'utilisateur **administrator** existe dans l'annuaire LDAP et qu'un mot de passe est saisi, ce dernier sera ignoré. |
| Préfixe d'authentification           | Certains serveurs LDAP nécessitent qu'un préfixe soit concaténé au nom de l'utilisateur pour effectuer l'authentification.<br />**Exemple** :<br />Préfixe : un_domaine\<br /><br />Utilisateur : un_utilisateur<br />Résultat : un_domaine\un_utilisateur |
| Suffixe d'authentification           | Certains serveurs LDAP nécessitent qu'un suffixe soit concaténé au nom de l'utilisateur pour effectuer l'authentification.<br />**Exemple** :<br />Suffixe=@un_domaine<br />Utilisateur=un_utilisateur<br />Résultat : un_utilisateur@un_domaine |
| Classe des utilisateurs              | Nom de la classe d'objets LDAP à utiliser pour identifier un utilisateur dans l'annuaire LDAP. |
| Classe des groupes                   | Nom de la classe d'objets LDAP à utiliser pour identifier un groupe dans l'annuaire LDAP. |
| Filtre d'utilisateur                 | Filtre de recherche à utiliser pour extraire les utilisateurs de l'annuaire LDAP. Ce filtre doit être formaté selon la syntaxe standard LDAP. |
| Filtre de groupe                     | Filtre de recherche à utiliser pour extraire les groupes de l'annuaire LDAP. Ce filtre doit être formaté selon la syntaxe standard LDAP. |
| Attribut utilisateur                 | Attribut d'un utilisateur LDAP pour définir l'identité de celui-ci. |
| Attribut groupe                      | Attribut d'un groupe LDAP pour définir l'identité de celui-ci. |
| Attribut membre                      | Attribut d'un groupe LDAP pour définir quels utilisateurs sont membres de celui-ci. |
| Attribut nom complet                 | Attribut d'un utilisateur LDAP pour définir le nom complet de celui-ci. |
| Attribut courriel                    | Attribut d'un utilisateur LDAP pour définir l'adresse de courriel de celui-ci. |
| Taille maximale de la page           | Dans les annuaires LDAP, la taille de transactions est limitée à un nombre maximal d'enregistrements à la fois (taille de la page). La valeur de ce paramètre ne doit pas dépasser la taille maximale autorisée par l'annuaire (1000 est la valeur par défaut dans les annuaires LDAP). Une taille trop petite peut réduire les performances. Une taille plus grande que la limite autorisée causera des données manquantes dans la liste des utilisateurs. |

Pour plus de détails sur le protocole LDAP, consultez [http://en.wikipedia.org/wiki/Lightweight_Directory_Access_Protocol](http://en.wikipedia.org/wiki/Lightweight_Directory_Access_Protocol).



### Gestionnaire d'utilisateurs composite

Ce type de gestion d'utilisateurs permet de combiner plusieurs gestionnaires ensemble. Vous pouvez ajouter autant de gestionnaires que nécessaire. Tous les gestionnaires fonctionneront comme un seul et unique gestionnaire d'utilisateurs. Consultez les sections précédentes pour la configuration des gestionnaires d'utilisateurs.



### Synchronisation des permissions d'utilisateurs

Lorsque vous vous connectez à une base de données de comptes d'utilisateurs existante (Active Directory, LDAP ou une base de données relationnelle externe), il peut être utile de synchroniser JMap Server avec la base de données pour 2 raisons :

•Lorsque des utilisateurs ou groupes sont supprimés de la base de données et que ceux-ci détenaient des permissions dans JMap (p. ex. ouverture d'un projet ou permission de visualiser certaines couches), les permissions ne sont pas supprimées des listes de permissions dans JMap Server. Cette situation peut se produire parce que JMap Server n'est pas au courant de la suppression des utilisateurs et des groupes de la base de données. En effectuant la synchronisation, JMap Server supprime toutes les permissions qui existent pour les utilisateurs et groupes supprimés. Toutefois, même si vous n'effectuez pas de synchronisation, cette situation n'entraîne pas de problèmes de sécurité car les utilisateurs supprimés ne seront pas en mesure de s'authentifier.

•Lorsque la composition des groupes d'utilisateurs est modifiée (membres ajoutés ou enlevés) pour que JMap Server charge à nouveau la liste des membres des groupes. JMap Server conserve la liste des membres en mémoire pour des raisons de performances.

Vous pouvez automatiser la synchronisation en activant l'option **Synchronisation automatique à chaque** et en spécifiant une période de temps.

 

## Gestion des comptes d'utilisateurs et des groupes

Dans JMap, les comptes d'utilisateurs et les groupes servent au contrôle d'accès et à la collaboration. Vous pouvez gérer les utilisateurs et les groupes dans JMap Admin en appuyant sur **Utilisateurs / Groupes** à partir de la section JMap Server.

Il existe deux utilisateurs et deux groupes spéciaux qui sont toujours présents dans JMap : **administrator**, **anonymous,** **everyone**et **authenticated users**.

| **Utilisateurs et groupes spéciaux** |                                                              |
| ------------------------------------ | ------------------------------------------------------------ |
| Administrator                        | L'utilisateur **administrator** est utilisé pour accéder à JMap Admin à la suite d'une nouvelle installation (il détient les droits d'administration de JMap). Son champ de mot de passe est laissé en blanc, donc il est fortement recommandé d'ajouter un mot de passe aussitôt que possible. Voir plus bas pour obtenir des détails supplémentaires. L'utilisateur **administrator** existe toujours dans JMap et il ne peut pas être supprimé. |
| Anonymous                            | L'utilisateur **anonymous** permet de donner accès à des ressources à des utilisateurs qui ne sont pas authentifiés. Cela permet par exemple de configurer un accès sans authentification à un projet. L'utilisateur **anonymous** existe toujours dans JMap, il ne peut pas être supprimé et son mot de passe (vide) ne peut pas être modifié. |
| Everyone                             | Le groupe **everyone** est utilisé pour donner accès à une ressource à tous les utilisateurs, incluant l'utilisateur **anonymous** (sans authentification). L'utilisateur **everyone** n'apparaît pas dans la liste des groupes de JMap. Il est visible uniquement dans les interfaces permettant de définir les permissions, lorsque cela est pertinent. |
| Authenticated users                  | Le groupe **authenticated users** est utilisé pour donner accès a une ressource à tous les utilisateurs à l'exception de l'utilisateur **anonymous**. Pour ce groupe l'authentification est obligatoire. |



### Création d'utilisateurs et de groupes

Vous pouvez créer un nouvel utilisateur ou un nouveau groupe en cliquant sur **Créer** dans la section **Utilisateurs / Groupes**. Vous serez alors dirigé vers la section de configuration du nouveau groupe ou utilisateur. Notez que vous pouvez uniquement créer des utilisateurs et des groupes si vous utilisez la base de données des comptes JMap ou une base de données externe qui n'est pas en lecture seule.

| **Utilisateurs**       |                                                              |
| ---------------------- | ------------------------------------------------------------ |
| Nom d'utilisateur      | Entrez un nom d'utilisateur unique pour le nouvel utilisateur (nom utilisé lors de l'authentification). Vous ne pourrez pas sauvegarder l'utilisateur si le nom spécifié existe déjà. |
| Mot de passe           | Entrez un mot de passe pour le nouvel utilisateur. Ce champ peut être laissé en blanc, mais il n'est pas recommandé de le faire. Les utilisateurs des applications JMap Web peuvent changer leur mot de passe à partir de l'application. Ceci est possible seulement si les comptes utilisateurs sont gérés avec JMap DB. |
| Confirmer mot de passe | Entrez le mot de passe une seconde fois pour le confirmer.   |
| Nom & prénom(s)        | (Optionnel) Entrez le nom complet (prénom(s) et nom de famille) du nouvel utilisateur. |
| Courriel               | (Optionnel) Entrez l'adresse courriel du nouvel utilisateur. Celle‑ci sera utilisée pour envoyer des cartes à l'utilisateur. |
| Caché                  | Sélectionnez cette option si vous désirez que le nouvel utilisateur soit caché des répertoires d'utilisateurs. |

| **Groupes**   |                                                              |
| ------------- | ------------------------------------------------------------ |
| Nom du groupe | Entrez un nom unique pour le nouveau groupe. Vous ne pourrez pas sauvegarder le groupe si le nom spécifié existe déjà. |



### Modification d'utilisateurs et de groupes

Vous pouvez modifier des utilisateurs ou groupes existants en cliquant sur leur nom dans la liste. Notez qu'une fois qu'un utilisateur a été créé, son nom d'utilisateur ne peut plus être modifié. Afin d'ajouter des utilisateurs à un groupe, appuyez sur ![img](assets/2017-01-06_16-00-52.png) et une liste des utilisateurs disponibles s'affichera. Sélectionnez les utilisateurs à ajouter au groupe et appuyez sur **Ajouter**. Afin de supprimer des utilisateurs d'un groupe, sélectionnez‑les et appuyez sur ![img](assets/2017-02-07_14-39-04.png).



### Suppression d'utilisateurs et de groupes

Vous pouvez supprimer un utilisateur ou un groupe en le sélectionnant dans la liste et en appuyant sur **Supprimer**.



## Gestion des permissions

Les permissions dans JMap sont de deux familles : les permissions pour les utilisateurs des applications (Pro, Web et Survey) et les permissions pour les administrateurs (JMap Admin).



### Permissions pour les utilisateurs

Les permissions pour les utilisateurs déterminent ce que les utilisateurs sont autorisés à faire dans les applications JMap Pro, JMap Web et JMap Survey.

Le tableau suivant présente les différents groupes de permissions disponibles pour les utilisateurs.

| **Permissions pour les utilisateurs**    |                                                              |
| ---------------------------------------- | ------------------------------------------------------------ |
| Permissions sur les projets              | Voir la section [Permissions des projets](05 Projets.md) pour plus d'information. |
| Permissions sur les couches              | Voir la section [Permissions des couches](06 Couches.md) pour plus d'information. |
| Permissions sur les couches personnelles | **Créer des couches personnelles**<br />Cette permission donne à un utilisateur le droit de créer des couches personnelles dans les applications JMap Pro. Par défaut, le utilisateurs JMap ne sont pas autorisés à créer des couches personnelles.<br />Vous pouvez configurer cette permission dans la sous-section **Permissions** de la section JMap Server. |
| Permissions sur les formulaires          | Voir la section [Formulaires de base de données](07 Formulaires.md) pour plus d'information. |



### Permissions pour les administrateurs

Les permissions pour les administrateurs déterminent ce que les administrateurs de JMap sont autorisés à faire dans JMap Admin. Certaines permissions sont globales (permissions d'effectuer certaines tâches) alors que d'autres permissions concernent des ressources en particulier.

Plusieurs des permissions globales peuvent être configurées dans la sous-section **Permissions** de la section JMap Server.

Le tableau suivant décrit les permissions globales d'administration.

| **Permissions globales d'administration** |                                                              |
| ----------------------------------------- | ------------------------------------------------------------ |
| Accéder à JMap Admin                      | Cette permission est nécessaire pour qu'un administrateur puisse entrer dans JMap Admin. Après l'installation de JMap, seul l'utilisateur **administrator** possède cette permission. Notez que le mot de passe est initialement vide pour cet utilisateur. Il est fortement recommandé d'entrer un mot de passe pour l'utilisateur **administrator**. Reportez‑vous à la section [Gestion d'utilisateurs et de groupes](#Gestion des comptes d'utilisateurs et des groupes) pour plus d'informations sur la modification des mots de passe.<br />Assurez‑vous de laisser au moins un utilisateur dans la liste d'autorisation et de vous rappeler du mot de passe. Autrement, il sera impossible d'accéder à JMap Admin. |
| Créer des bases de données                | Cette permission est requise pour qu'un administrateur puisse créer de nouvelles bases de données dans JMap Admin. |
| Créer des connexions distantes            | Cette permission est requise pour qu'un administrateur puisse créer de nouvelles connexions vers d'autres instances de JMap Server dans JMap Admin. |
| Créer des déploiements                    | Cette permission est requise pour qu'un administrateur puisse créer de nouveaux déploiements d'applications dans JMap Admin. |
| Créer des modèles de métadonnées          | Cette permission est requise pour qu'un administrateur puisse créer de nouveaux modèles pour les métadonnées dans JMap Admin. |
| Créer des modèles de styles               | Cette permission est requise pour qu'un administrateur puisse créer de nouveaux modèles de styles dans JMap Admin. |
| Créer des projets                         | Cette permission est requise pour qu'un administrateur puisse créer de nouveaux projets dans JMap Admin. |
| Créer des sources de données              | Cette permission est requise pour qu'un administrateur puisse créer de nouvelles sources de données spatiales dans JMap Admin. |

Les permissions d'administration sur les ressources déterminent ce que l'administrateur peut faire avec chaque ressource. Le tableau suivant décrit ces permissions.

| **Permissions d'administration sur les ressources** |                                                              |
| --------------------------------------------------- | ------------------------------------------------------------ |
| Accéder à ...                                       | Permet de voir les informations détaillées de la ressource et permet d'utiliser la ressource, sans pouvoir la modifier.<br />**Exemple** : <br />Pour utiliser une source de données spatiales pour créer une couche, l'administrateur doit au minimum posséder la permission **Accéder à** sur la source de données. |
| Administrer ...                                     | Permet de modifier la ressource, de gérer les permissions des utilisateurs sur la ressource. Ne permet pas de supprimer la ressource ni d'en gérer les permissions d'administration.<br />**Exemple** : <br />Pour ajouter une couche dans un projet, l'administrateur doit posséder la permission **Administrer** sur le projet. |
| Utiliser la console SQL                             | (Ne s'applique qu'aux bases de données) Permet d'utiliser la console SQL sur la base de données. La console SQL permet de voir la structure de la base de données et d'exécuter des requêtes SQL sur la base de données. |
| Accéder à distance                                  | Permet d'accéder à la ressource à partir d'une autre instance de JMap Server. Cette permission est généralement donnée à un compte générique utilisé pour ouvrir les sessions de communication entre instances de JMap Server.<br />Pour plus d'information, consultez les sections [Partage des couches](06 Couches.md) et [Partage de sources de données spatiales](04 SDS.md). |



### Propriétaires d'une ressource

La plupart des ressources gérées dans JMap Admin possèdent un ou plusieurs propriétaires. Les propriétaires d'une ressource sont les seuls à pouvoir :

- Gérer les permissions d'administration pour cette ressource;
- Gérer la liste des propriétaires de cette ressource,
- Supprimer la ressource. 



### Super administrateurs

Les super administrateurs peuvent tout faire dans JMap Admin. Ils sont les seuls à pouvoir :

- Gérer la liste des super administrateurs;
- Gérer les permissions globales d'administration;
- Gérer les utilisateurs et les groupes;
- Modifier les paramètres de fonctionnement de JMap Server;
- Afficher les fichiers de journalisation;
- Importer et exporter des configurations.

Vous pouvez gérer la liste des super administrateurs dans la sous-section **Permissions** de la section JMap Server. Sélectionnez l'onglet **Super administrateurs**.



Le tableau suivant présente des tâches d'administration avec exemples et indique quel profil ou quelles permissions sont requises pour effectuer ces tâches.

| **Tâches**                                                   | **Super Administrateur** | **Administrateur**                                           |
| ------------------------------------------------------------ | ------------------------ | ------------------------------------------------------------ |
| **Accéder à JMap Admin**                                     | OUI                      | Si permission *Accéder à JMap Admin*                         |
| **Gérer la liste des Super administrateurs**                 | OUI                      | NON                                                          |
| **Gérer les permissions globales d'administration**<br />Donner à un administrateur la permission de créer des projets<br />Retirer à un administrateur la permission de créer des sources de données spatiales<br />Donner à un administrateur la permission de créer des modèles de métadonnées des couches. | OUI                      | NON                                                          |
| **Effectuer des tâches de gestion de JMap Server**<br />Modifier les paramètres de JMap Server (ports, mémoire, etc.)<br />Gérer les utilisateurs et les groupes<br />Importer ou exporter les configurations de JMap Server<br />Voir les journaux ou en modifier les paramètres | OUI                      | NON <br />Peut modifier le mot de passe de son compte utilisateur |
| **Créer une ressource**<br />Créer un projet<br />Créer une base de données<br />Créer un déploiement d'application | OUI                      | Si permission *Créer ...*                                    |
| **Utiliser une ressource**<br />Utiliser une base de données pour créer une source de données spatiales<br />Utiliser une source de données pour créer une couche•Utiliser une connexion à JMap Server pour créer une couche par référence | OUI                      | Si permission *Accéder à ...*                                |
| **Voir les informations détaillées d'une ressource**<br />Cliquer sur une base de données pour voir l'ensemble de ses paramètres<br />Cliquer sur un projet pour voir l'ensemble de ses paramètres | OUI                      | Si permission *Accéder à ...*                                |
| **Modifier une ressource**•<br />Changer le nom d'un projet<br />Ajouter une couche dans un projet<br />Modifier les paramètres de connexion d'une base de données<br />Modifier la projection d'une source de données spatiales | OUI                      | Si permission *Administrer ...*                              |
| **Supprimer une ressource**<br />Supprimer un projet<br />Supprimer un déploiement d'application<br />Supprimer un modèle de style | OUI                      | Si propriétaire de la ressource                              |
| **Gérer les permissions des utilisateurs d'une ressource**<br />Donner à un utilisateur la permission d'ouvrir un projet<br />Donner à un utilisateur la permission d'éditer les éléments d'une couche d'un projet<br />Retirer à un utilisateur la permission de copier les données d'une couche d'un projet | OUI                      | Si permission *Administrer ...*                              |
| **Gérer les permissions d'administration d'une ressource**<br />Donner à un administrateur la permission d'utiliser une source de données spatiales<br />Donner à un administrateur la permission de modifier un projet<br />Retirer à un administrateur la permission de modifier une base de données | OUI                      | Si propriétaire de la ressource                              |
| **Gérer la liste des propriétaires d'une ressource**         | OUI                      | Si propriétaire de la ressource                              |



### Rapports de permissions

Les rapports de permissions permettent de visualiser sur un même rapport l'ensemble des permissions que possède un utilisateur ou un groupe. C'est un moyen rapide d'obtenir l'information sans avoir à vérifier chaque ressource. Les rapports sont accessibles à partir des onglets **Utilisateurs** et **Groupes** de la section **Utilisateurs / Groupes** en appuyant sur ![img](assets/2017-02-08_14-55-36.png).

 

## Authentification unique

L'authentification unique permet aux utilisateurs d'accéder aux applications JMap Pro, de manière sécurisée, mais sans avoir à s'authentifier. C'est l'authentification de la session Windows qui est utilisée pour ouvrir automatiquement la session JMap. L'authentification unique n'est disponible que sur les environnements Windows utilisant Active Directory. Une configuration spéciale doit être faite sur le serveur Windows ainsi que sur chacun des ordinateurs où l'authentification unique est souhaitée. Notez que l'option Authentification Unique doit aussi être activée lors du déploiement d'une application JMap Pro.

Pour plus de détails sur la configuration de l'authentification unique, consultez [cet article](https://k2geospatial.atlassian.net/wiki/x/bAAtAQ).



## Gestion des sessions

Tout utilisateur qui se connecte à JMap Server en utilisant une application JMap possède une session ouverte sur le serveur. La session demeure ouverte tant que l'application JMap n'est pas fermée. Les sessions contiennent des informations sur l'identité de l'utilisateur. Il se peut que votre licence d'utilisation JMap limite le nombre de sessions simultanées permises.

Pour accéder à la section de gestion des sessions, appuyez sur **Sessions** depuis la section JMap Server.

Les sessions peuvent être de 5 types différents. Le tableau suivant décrit chaque type de session.

| **Types de sessions JMap** |                                                              |
| -------------------------- | ------------------------------------------------------------ |
| JMap Pro                   | Ce type de session est utilisé lorsqu'un utilisateur se connecte à JMap Server en utilisant une application JMap Pro. Le nombre de sessions concurrentes de ce type est défini par votre licence d'utilisation de JMap. |
| JMap Survey                | Ce type de session est utilisé lorsqu'un utilisateur se connecte à JMap Server en utilisant une application JMap Survey. Le nombre de sessions concurrentes de ce type est défini par votre licence d'utilisation de JMap. |
| JMap Web                   | Ce type de session est utilisé lorsqu'un utilisateur se connecte à JMap Server en utilisant une application JMap Web. Le nombre de sessions concurrentes de ce type est défini par votre licence d'utilisation de JMap. |
| JMap Admin                 | Une session de ce type est ouverte quand un utilisateur se connecte à JMap Admin pour administrer JMap Server. Ce type de session n'est pas contrôlé et, par conséquent, le nombre de sessions JMap Admin concurrentes n'est pas limité. |
| JMap Server                | Ce type de session est utilisé lorsqu'un JMap Server se connecte à un autre JMap Server. La session s'ouvre sur le serveur qui accepte la connexion. Ce type de session est utilisé pour le partage de données de JMap à JMap. Ce type de session doit être autorisé par votre licence d'utilisation de JMap. |



### Sessions actives

Vous pouvez visualiser la liste des sessions ouvertes. En sélectionnant l'onglet **Sessions actives**, la liste des sessions en cours s'affiche, de même que des informations utiles sur chaque session. Vous pouvez terminer des sessions ouvertes en les sélectionnant et en appuyant sur **Fermer les sessions**.



### Sessions réservées

Les sessions réservées sont des sessions spéciales pour des utilisateurs qui ont priorité sur les autres. Ces utilisateurs pourront toujours ouvrir une session JMap Pro, Web ou Survey, même si le nombre maximal de sessions est déjà atteint, en fonction de votre licence. Ces sessions réservées sont comptabilisées séparément du reste des sessions.

Si votre licence d'utilisation de JMap le permet, vous pouvez donc assigner un certain nombre de sessions réservées aux utilisateurs de votre choix. Appuyez sur ![img](assets/2017-01-06_16-00-52.png) pour sélectionner un utilisateur et lui assigner une session réservée. Une fois le nombre maximal de sessions réservées assignées atteint, vous ne pouvez pas en assigner à d'autres utilisateurs. Vous pouvez retirer une session réservée à un utilisateur en sélectionnant son nom et en appuyant sur ![img](assets/2017-02-07_14-39-04.png).



### Statistiques

Les statistiques sur les sessions fournissent des informations sommaires sur les activités des utilisateurs au cours d'une période donnée. Vous pouvez connaître le nombre total de sessions au cours d'une période donnée et le plus grand nombre de sessions concurrentes atteint par période de temps. Les statistiques sont présentées sous forme de diagrammes à barres. Appuyez sur **Mise à jour** pour générer le graphique.

| **Statistiques sur les sessions** |                                                              |
| --------------------------------- | ------------------------------------------------------------ |
| Afficher                          | Sélectionnez l'information à afficher. Il peut s'agir soit du **Nombre total de sessions** ou du **Plus grand nombre de sessions concurrentes**. |
| Utilisateurs                      | Sélectionnez un ou plusieurs utilisateurs pour lesquels les informations seront affichées. |
| Unité de temps                    | Sélectionnez l'unité de temps à utiliser pour afficher l'information. Les unités possibles sont **Heure**, **Jour**, **Semaine** ou **Mois**. |

Les informations sur les sessions sont conservées dans la base de données System de JMap pendant une période de 18 mois. Les sessions qui datent de plus de 18 mois sont automatiquement effacées de la base de données System.

 

## Utilisation de HTTPS avec JMap

Le protocole HTTPS permet d'utiliser JMap de manière plus sécuritaire en chiffrant toutes les communications entre les applications JMap, JMap Admin et JMap Server.



### Utilisation de HTTPS avec JMap Admin

Pour utiliser HTTPS avec JMap Admin, vous devez installer un certificat de sécurité dans JMap Server. Un certificat de sécurité est requis pour effectuer le chiffrement des données. 

Durant l'installation de JMap, une option est proposée pour la création et l'installation automatique d'un certificat de sécurité temporaire. Un tel certificat permet de bien sécuriser les communications, mais causera l'affichage de messages d'avertissements dans les navigateurs web, car il n'est pas émis par une organisation de sécurité reconnue (CA, ou Certificate Authority).

Vous pouvez aussi installer un certificat de sécurité émis spécialement pour votre organisation, si vous en possédez un. Pour la procédure détaillée d'installation d'un certificat, consultez cet article [https://k2geospatial.atlassian.net/wiki/x/EQAtAQ](https://k2geospatial.atlassian.net/wiki/x/EQAtAQ).

Une fois le certificat de sécurité installé dans JMap Server, vous pouvez lancer JMap Admin avec une URL comme celle-ci :

[https://monserveurjmap](https://monserveurjmap/) (assumant que le port par défaut 443 est utilisé)

Si vous souhaitez forcer en tout temps l'utilisation du protocole HTTPS pour JMap Admin, vous pouvez activer la redirection automatique. Pour plus d'information, consultez la section [Paramètres de JMap Server](11 Gestion de JMap Server.md).



### Utilisation de HTTPS avec les applications JMap

Lorsque vous déployez des applications JMap (Pro ou Web) avec JMap Admin, vous pouvez spécifier quel protocole (HTTP ou HTTPS) sera utilisé pour les communications entre l'application et JMap Server. Si le type de déploiement est **local** (application hébergée sur JMap Server), le protocole HTTPS est proposé seulement si un certificat de sécurité est installé sur JMap Server. Il s'agit du même certificat que pour JMap Admin (voir plus haut). Si le type de déploiement est **externe** (application hébergée sur un autre serveur web), les deux protocoles sont toujours offerts.

Dans le cas de JMap Pro, les protocoles HTTP ou HTTPS sont utilisés uniquement si l'option de connexion par **Proxy** est sélectionnée durant le déploiement.

  