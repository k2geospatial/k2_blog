---
layout: default
title: Bases de données
nav_order: 2
---

# Bases de données

JMap Server gère les connexions de bases de données en les plaçant dans des réserves. Les réserves comportent un certain nombre de connexions ouvertes vers les bases de données. Les connexions sont partagées à l'ensemble du système et utilisées selon les besoins d'accès aux bases de données.

Toutes les réserves de connexions aux bases de données (ci-après nommées bases de données afin de simplifier le texte) sont gérées centralement à l'aide de JMap Admin. De façon générale, les bases de données sont utilisées par JMap Server pour lire les données spatiales stockées dans les tables et pour accéder aux données descriptives associées aux données spatiales. Une fois que les bases de données ont été configurées dans JMap Admin, on peut les utiliser à partir d'autres sections et à différentes fins lors du processus d'administration.

La section Bases de données de JMap Admin affiche une table des bases de données existantes et montre leurs statuts.

**Base de données System**

JMap possède une base de données nommée System qui contient des tables de géométries et de configurations de JMap Server. Cette base de données est essentielle et, en règle générale, ne doit pas être modifiée. La base de données System ne peut pas être supprimée et elle ne devrait être manipulée que par des administrateurs avertis. Reportez‑vous à la section [Base de données System de JMap Server](11 Gestion de JMap Server.md) pour plus de détails à ce sujet.



## Création de bases de données

Pour amorcer la création d'une nouvelle connexion à une base de données, appuyez sur le bouton Créer dans la page listant les bases de données et suivez les étapes requises.

| **Identification** |                                                              |
| ------------------ | ------------------------------------------------------------ |
| Nom                | Entrez un nom pour la nouvelle base de données. Le nom choisi doit être unique. |
| Description        | (Optionnel) Entrez une description pour la nouvelle base de données. La description n'est visible que par les administrateurs dans JMap Admin. |

| **Paramètres de connexion** |                                                              |
| --------------------------- | ------------------------------------------------------------ |
| Pilote                      | Sélectionnez le pilote qui correspond au système de base de données auquel vous voulez vous connecter.<br />Vous pouvez ajouter de nouveaux pilotes en créant de nouveaux fichiers de configuration dans le répertoire *JMAP_HOME/conf/db* sur le serveur. |
| Hôte                        | (Selon le pilote sélectionné) Le nom ou l'adresse TCP/IP du serveur de bases de données. |
| Port                        | (Selon le pilote sélectionné) Le port TCP/IP du serveur de bases de données. |
| Base de données             | (Selon le pilote sélectionné) Le nom de la base de données à accéder, tel que défini dans le serveur de bases de données. |
| Fichier                     | (Selon le pilote sélectionné) Le chemin d'accès vers le fichier de bases de données. |
| Paramètres supplémentaires  | Dans certaines situations exceptionnelles, les systèmes de bases de données peuvent exiger des paramètres supplémentaires. Ils peuvent être entrés dans ce champ. |
| Nom d'utilisateur           | Entrez le nom d'utilisateur pour la connexion à la base de données. L'authentification d'utilisateurs de domaine n'est pas supportée. Vous devez vérifier que la base de données permet l'authentification à ce niveau. |
| Mot de passe                | Entrez le mot de passe pour la connexion à la base de données. |

| **Connexions**        |                                                              |
| --------------------- | ------------------------------------------------------------ |
| Nombre de connexions  | Entrez la taille initiale de la réserve de connexions afin de déterminer le nombre de connexions à la base de données qui demeureront ouvertes. |
| Maximum de connexions | Entrez le nombre maximal de connexions permises pour cette réserve. Le nombre entré doit être égal ou supérieur au nombre initial de connexions. Si la réserve doit s'agrandir, de nouvelles connexions seront automatiquement créées jusqu'à ce que la valeur maximale soit atteinte. Après un certain délai, les connexions supplémentaires sont automatiquement fermées et la réserve reprend sa taille initiale.<br />La valeur maximale peut être désactivée en désélectionnant la case à cocher, afin de permettre d'agrandir la réserve sans contrainte. |



### Paramètres avancés

En règle générale, les paramètres avancés qui suivent ne doivent pas être modifiés.

| **Paramètres**                     |                                                              |
| ---------------------------------- | ------------------------------------------------------------ |
| Paramètres additionnels            | Dans certaines situations exceptionnelles, les systèmes de bases de données peuvent exiger des paramètres additionnels. Ils peuvent être entrés dans ce champ. |
| Requête de validation              | JMap utilise un mécanisme de validation des requêtes afin d'assurer que les connexions à la base de données sont valides. Cette requête est utilisée pour tester la connexion chaque fois qu'une requête doit être exécutée. Si la requête de validation échoue, ce qui signifie généralement que la connexion à la base de données est rompue, JMap Server tentera automatiquement d'établir une nouvelle connexion. Ce mécanisme permet d'assurer que les connexions à la base de données ne cessent jamais de fonctionner.<br />La requête doit être valide et doit s'exécuter très rapidement. Afin de réduire l'impact sur la performance, assurez-vous de minimiser le nombre d'enregistrements retournés (la valeur zéro est idéale) et utilisez des champs indexés dans la clause WHERE.<br />Des requêtes par défaut sont fournies. En règle générale, elles n'ont pas besoin d'être modifiées |
| Délai d'expiration de la connexion | Le délai d'inactivité est utilisé pour fermer et ouvrir à nouveau les connexions qui demeurent inactives pendant une période prolongée. Ce mécanisme permet d'assurer que le système de base de données ne ferme pas les connexions inactives. Assurez‑vous que cette valeur est inférieure au délai d'attente de connexion de votre système de base de données. La valeur par défaut de 2 heures convient la plupart du temps. |
| Délai maximal de connexion         | Le délai d'attente maximal lors de l'ouverture d'une connexion réseau vers la base de données. Ce paramètre sert à prévenir les blocages dans l’éventualité où le serveur de base de données ne répond plus. La valeur par défaut est de 60 sec. Activez cette option pour définir une valeur différente pour cette connexion. |
| Type de connexion                  | Indiquez le type de connexion devant être créée. Les connexions génériques utilisent toutes les mêmes informations d'utilisateur (nom d'utilisateur et mot de passe) définies précédemment. Du point de vue du système de base de données, c'est comme si le même utilisateur effectuait toutes les requêtes. Ce type de connexion est utilisé la plupart du temps.<br />Les connexions identifiées sont créées à la volée pour chaque utilisateur connecté à JMap Server. La même connexion est réutilisée au cours de la session pour chaque utilisateur. Du point de vue du système de gestion de bases de données, chaque requête est effectuée par l'utilisateur qui est connecté à JMap Server. Ce mode de connexion est utile dans les environnements où la sécurité est gérée au niveau de la base de données. Afin d'assurer le fonctionnement du mode de connexion identifié, JMap et le système de base de données doivent partager la même liste d'utilisateurs, ce qui peut être le cas lorsque le module de gestion des utilisateurs d'Oracle est utilisé pour gérer les utilisateurs. |



## Configuration et gestion des bases de données

Lorsque vous cliquez sur le nom d'une base de données dans la section **Base de données**, l'interface **Configuration des bases de données** s'affiche.

Celle-ci comporte des boutons pour **Éditer**, [Réinitialiser](#réinitialisation-des-bases-de-données), [Désactiver](#Désactivation-des-bases-de-données) ou [Supprimer](#Suppression des bases de données) la base de données. Le bouton ![img](assets/clip0058.png) permet l'accès aux sections [Console SQL](#Console SQL) et [Permissions](10 Sécurité.md).

Des sous-sections présentent des informations sur la base de données. Les valeurs des paramètres indiqués ont été définies lors de la création de la connexion à la base des données. Référez-vous à la section [Création de bases de données](#Création-de-bases-de-données) pour obtenir les détails de chaque paramètre. Les paramètres peuvent être modifiés en appuyant sur **Éditer**.



### Information générale

Cette sous-section affiche le nom, l'id (identifiant interne de JMap), la description et le propriétaire de la base de données.

#### Réserve de connexions

Cette sous-section affiche les détails de la réserve des connexions. Les paramètres indiqués sont : taille initiale, taille maximale, utilisation de la réserve, pointe d'utilisation de la réserve, délai d'expiration de la connexion, délai maximal de connexion.

#### Connexion

Cette sous-section affiche les détails de la connexion à la base de données. Les paramètres indiqués sont : [état](#États des bases de données), base de données (indique le type), pilote, chaîne de connexion, nom d'utilisateur, requête de validation et type de connexion.

#### Références

Cette sous-section affiche toutes les ressources dans lesquelles sont utilisées les données de la base de données. De manière hiérarchique les sources des données spatiales sont présentées, ainsi que les projets avec les couches, les rapports et les formulaires, tous avec les attributs utilisés. Cette information est utile pour visualiser les ressources qui seraient affectés par les modifications de la base de données.

#### Réinitialisation des bases de données

La réinitialisation d'une base de données ferme toutes les connexions ouvertes et en crée de nouvelles. Cette action peut être utile pour forcer le rétablissement de la connexion à un système de base de données.

#### Désactivation des bases de données

La désactivation d'une base de données ferme les connexions vers celle-ci sans supprimer sa configuration. JMap Server ne peut plus interroger la base de données. La désactivation est utile lorsque la base de données ne répond plus et entraîne des délais dans le serveur local.

#### Suppression des bases de données

La suppression d'une base de données supprime la configuration de la connexion pour ce système de base de données. Les données contenues dans la base de données ne sont aucunement affectées.

#### États des bases de données

Chaque base de données possède un état. Celui-ci indique la condition de la connexion à la base de données. Le tableau suivant décrit les états possibles pour une base de données.

| **États** |                                                              |
| --------- | ------------------------------------------------------------ |
| Erreur    | Les connexions à la base de données sont rompues. La base de données ne peut être utilisée tant que l'erreur n'a pas été corrigée et que les connexions n'ont pas été ouvertes de nouveau. La réinitialisation de la base de données corrige parfois ce problème. Vous pouvez obtenir une description de l'erreur en cliquant sur le mot **Erreur** en rouge. |
| Inactive  | Les connexions à la base de données sont fermées mais elles sont configurées. JMap ne peut plus interroger la base de données. |
| Connecté  | Les connexions à la base de données ont été créées avec succès et sont prêtes à être utilisées. |



### Console SQL

JMap Admin fournit une console SQL générique qui permet de visualiser les structures de bases de données, d'exécuter des requêtes SQL, d'inspecter le contenu des tables, de tester la vitesse d'exécution des requêtes, etc. Toutes les bases de données configurées sont accessibles à partir de cette console.

Lorsque vous effectuez une requête SQL, l'exécution de la requête est sujette aux permissions de sécurité accordées à l'utilisateur qui est connecté à la base de données. Reportez‑vous à la section [Création de bases de données](#Création-de-bases-de-données) afin d'obtenir plus de détails sur la définition de l'utilisateur pour les connexions à la base de données.

| **Console SQL**              |                                                              |
| ---------------------------- | ------------------------------------------------------------ |
| Base de données              | Sélectionnez la base de données à utiliser.                  |
| Afficher la structure        | Cliquez sur ![img](assets/clip_0070.png) pour ouvrir une fenêtre qui vous permet de naviguer dans la structure de la base de données. Vous pouvez visualiser les schémas, les tables et les vues, de même que de l'information sur chaque champ d'une table ou d'une vue. |
| Max. d'enregistrements       | Lorsque vous exécutez une requête SQL de type SELECT, vous pouvez entrer une valeur pour limiter le nombre d'enregistrements retournés. |
| Commit automatique           | Si vous effectuez des transactions SQL (p. ex. Insert, Update), sélectionnez cette option pour valider les transactions automatiquement (opération commit en SQL). Autrement, vous devrez effectuer les validations manuellement. |
| Tester la vitesse uniquement | Lorsque vous exécutez une requête SQL, sélectionnez cette option pour répéter la requête un certain nombre de fois et pour afficher les temps d'exécution. |
| Requête SQL                  | Entrez la requête SQL à exécuter. Le résultat sera affiché dans une table. |

Les résultats des requêtes s'affichent dans une nouvelle fenêtre. Les résultats des requêtes de type Insert, Update et Delete sont groupés dans le même onglet. Les résultats des requêtes de type Select s'affichent dans des onglets séparés.
