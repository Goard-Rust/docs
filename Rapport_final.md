<h1 align="center">Rapport final - Dashboard en Rust pour OAR</h1>
<p align="center">Rémi DEL MEDICO - Romain MIRAS - Alexandre ARLE - Amaury GOGUILLOT</p>

## Table des matières

- [Table des matières](#table-des-matières)
- [Rappel du sujet](#rappel-du-sujet)
  - [Contexte](#contexte)
  - [Cahier des charges](#cahier-des-charges)
- [Technologies employées](#technologies-employées)
  - [Rust](#rust)
  - [Cargo](#cargo)
  - [Egui](#egui)
  - [Puffin](#puffin)
  - [OAR](#oar)
- [Architecture technique](#architecture-technique)
  - [Architecture MVC](#architecture-mvc)
    - [1. Modèle](#1-modèle)
    - [2. Vue](#2-vue)
    - [3. Contrôleur](#3-contrôleur)
- [Réalisation technique](#réalisation-technique)
  - [Communication avec OAR](#communication-avec-oar)
  - [Diagramme de Gantt](#diagramme-de-gantt)
  - [Tableau de bord détaillé](#tableau-de-bord-détaillé)
  - [Fenêtre de détails des jobs](#fenêtre-de-détails-des-jobs)
  - [Filtrage et recherche avancés](#filtrage-et-recherche-avancés)
  - [Interface utilisateur adaptée](#interface-utilisateur-adaptée)
- [Gestion de projet](#gestion-de-projet)
  - [Organisation de l'équipe](#organisation-de-léquipe)
  - [Méthodologie Agile \& Sprints](#méthodologie-agile--sprints)
  - [Gestion des Tâches avec un Système de Tickets](#gestion-des-tâches-avec-un-système-de-tickets)
  - [Gestion de projet et collaboration](#gestion-de-projet-et-collaboration)
  - [Suivi du Projet et Communication](#suivi-du-projet-et-communication)
- [Outils](#outils)
  - [Gestion de projet et collaboration](#gestion-de-projet-et-collaboration-1)
    - [GitHub](#github)
    - [Discord](#discord)
  - [Documentation](#documentation)
    - [Diagrammes UML](#diagrammes-uml)
  - [Environnement de développement](#environnement-de-développement)
    - [Visual Studio Code](#visual-studio-code)
- [Métriques logicielles](#métriques-logicielles)
  - [Statistiques globales](#statistiques-globales)
  - [Distribution des langages](#distribution-des-langages)
  - [Contribution des développeurs](#contribution-des-développeurs)
    - [En nombre de lignes de code](#en-nombre-de-lignes-de-code)
    - [En nombre de commits](#en-nombre-de-commits)
  - [Notes additionnelles](#notes-additionnelles)
- [Conclusion](#conclusion)
  - [Résultats Obtenus](#résultats-obtenus)
  - [Améliorations et Évolutions Futures](#améliorations-et-évolutions-futures)
  - [Conclusion](#conclusion-1)
- [Bibliographie](#bibliographie)
- [Glossaire](#glossaire)


## Rappel du sujet

### Contexte
[OAR](https://oar.imag.fr/) est un gestionnaire de tâches et de ressources utilisé dans les environnements HPC (High Performance Computing) pour orchestrer et gérer efficacement les ressources de calcul d'un cluster. Développé par l'équipe [DATAMOVE](https://team.inria.fr/datamove/), équipe de recherche commune entre le laboratoire [INRIA](https://www.inria.fr/fr) et le [LIG](https://www.liglab.fr/fr) (Laboratoire d'Informatique de Grenoble), il est largement utilisé dans le milieu académique et de la recherche. Cependant, malgré ses fonctionnalités avancées, peu d'outils interactifs en temps réel existent pour visualiser et administrer les ressources gérées par OAR.

L'objectif de ce projet est de développer une interface utilisateur moderne, intuitive et performante pour OAR, permettant de visualiser et d'interagir avec les tâches et les ressources d'un cluster. Cette interface doit notamment proposer :

- Un diagramme de Gantt interactif pour visualiser l'occupation des ressources dans le temps
- Une vue détaillée des tâches et de leur état (en attente, en cours, terminées, erreurs...)
- Des filtres et options de recherche avancés pour faciliter la gestion d'un grand nombre de tâches
- Une interface réactive malgré de grands volumes de données
- Une intégration avec la dernière API Rest existante d'OAR

### Cahier des charges
Au cours de la première semaine de projet, nous avons rédigé un [cahier des charges](https://github.com/info5-groupe-9-dashboard-rust/docs/blob/main/Cahier_des_charges.pdf) en collaboration avec notre porteur de projet, Monsieur Olivier Richard, enseignant-chercheur à l'UGA-INP et membre du projet OAR. Nous avons ainsi défini les besoins suivants :

1. **Fonctionnalités essentielles** :
    - Visualisation des jobs et de leur état en temps réel dans un      diagramme de Gantt interactif
    - Filtrage des jobs par utilisateur, état, ressources utilisées
    - Affichage détaillé des propriétés d'un job sélectionné
    - Navigation temporelle dans le calendrier d'exécution

2. **Contraintes techniques** :
    - Développement en Rust pour garantir performances et fiabilité
    - Interface utilisateur avec la bibliothèque Egui
    - Communication avec l'API REST d'OAR
    - Support multi-plateforme (Linux, macOS, Windows)

3. **Livrables attendus** :
    - Application exécutable nativement avec interface graphique complète
    - Application exécutable dans un navigateur en mode interface web
    - Documentation technique et manuel utilisateur
    - Code source documenté sous GitHub

## Technologies employées

### Rust

[Rust](https://www.rust-lang.org/) est un langage de programmation système développé initialement par Mozilla, axé sur la sécurité, la vitesse et la concurrence. Nous avons choisi Rust pour les raisons suivantes :

- **Sécurité mémoire** : Son système de propriété (ownership) et d'emprunt (borrowing) permet d'éviter les problèmes de mémoire couramment rencontrés en C/C++
- **Performances** : Des performances comparables au C++ tout en garantissant une sécurité accrue
- **Robustesse** : Détection d'erreurs à la compilation plutôt qu'à l'exécution
- **Concurrence sans danger** : Facilite la programmation parallèle sans risque de data races
- **Écosystème moderne** : Un gestionnaire de paquets intégré et une communauté active

### Cargo

Cargo est le gestionnaire de paquets et système de build officiel de Rust. Dans notre projet, il nous a fourni :

- **Gestion des dépendances** : Installation et mise à jour automatiques des bibliothèques
- **Build system** : Compilation, tests et génération des binaires
- **Documentation** : Génération de documentation via `cargo doc`
- **Tests automatisés** : Exécution de tests unitaires et d'intégration
- **Environnements de développement** : Support des profils (développement/production)

Notre fichier `Cargo.toml` centralise la configuration du projet et toutes ses dépendances, facilitant la reproductibilité et le déploiement.

### Egui

[Egui](https://github.com/emilk/egui) est une bibliothèque d'interface graphique immédiate (immediate mode GUI) pour Rust. Nous l'avons choisie pour notre dashboard pour plusieurs raisons:

- **Simplicité d'utilisation** : API intuitive et concise, réduisant la complexité du code UI
- **Performance** : Optimisée pour le rendu rapide avec une empreinte mémoire minimale
- **Multi-plateforme** : Fonctionne sur Windows, macOS, Linux et Web (via WebAssembly)
- **Intégration Rust native** : S'intègre parfaitement avec l'écosystème Rust
- **Maintenance active** : Communauté dynamique et mises à jour régulières

Egui nous a permis de créer rapidement une interface réactive pour visualiser les données du système OAR sans avoir à recourir à des technologies web plus complexes.

### Puffin

[Puffin](https://github.com/EmbarkStudios/puffin) est un profileur de performance open source intégré pour les applications Rust basé sur egui. Dans notre application, il nous a aidés à :

- **Base de code du diagramme** : Base de code pour le diagramme de Gantt
- **Gestion Temporelle dynamique** : Déplacement et zoom sur les événements temporels
- **Optimiser le rendu** : Améliorer la fluidité de l'interface en ciblant les optimisations
- **Déboguer la latence** : Comprendre les causes des ralentissements lors de l'affichage des données

Son intégration avec Egui nous a fourni un outil précieux pour maintenir les performances optimales de notre dashboard, même lors de l'affichage de grandes quantités de données OAR.

### OAR

[OAR](https://oar.imag.fr/) est un gestionnaire de ressources et d'ordonnancement de tâches pour clusters de calcul haute performance. Dans notre projet, nous interagissons avec OAR pour:

- **Récupérer l'état des ressources** : Nœuds disponibles, occupés ou en maintenance
- **Surveiller les jobs** : État des tâches en cours, en attente ou terminées
- **Analyser l'utilisation** : Statistiques d'utilisation des ressources du cluster
- **Visualiser la topologie** : Représentation graphique de l'architecture du cluster
- **Interagir avec le système** : Soumission de requêtes et gestion des tâches via l'API

Notre dashboard s'interface avec OAR via une instance de OAR via des requêtes, permettant une visualisation en quasi temps réel de l'état du cluster et une meilleure compréhension de son utilisation pour les administrateurs système.

## Architecture technique

Notre application suit l'architecture Modèle-Vue-Contrôleur (MVC), un patron de conception qui sépare les préoccupations de l'application en trois composants distincts:

### Architecture MVC
![Architecture MVC du Dashboard OAR](./Conception/UML/Class%20Diagram/Diagrammes%20UML%20-%20Diagramme%20de%20classe%20simplifié.png)

*Figure 1: Diagramme de classes simplifié illustrant l'architecture MVC de notre application*

#### 1. Modèle

Le **modèle** représente les **données** et la **logique métier** de l'application:
- Gestion des **jobs OAR** et leurs **états**
- Stockage des informations sur les **ressources** du cluster
- Gestion des données de **configuration** et des **paramètres utilisateur**
- Communication en **SSH** avec l'instance OAR pour récupérer les données
- **Traitement** et **transformation** des données (filtrage, tri, etc.)

Ce composant est **indépendant** de l'interface utilisateur et encapsule toute la logique de récupération et manipulation des données.

#### 2. Vue

La **vue** est responsable de **l'affichage des données** à l'utilisateur:
- **Diagramme de Gantt** interactif utilisant Egui et basé Puffin
- **Tableau de bord** détaillées sur la liste des jobs visualisés
- **Filtres** et contrôles d'interface
- **Rendu graphique** de l'état des ressources
- **Menu** de navigation
- Page **d'authentification** prévue en cas de besoin

La vue ne contient aucune logique métier et se concentre uniquement sur la **présentation des données**.

#### 3. Contrôleur

Le **contrôleur** fait le lien entre le modèle et la vue:
- **Intercepte** les actions utilisateur provenant de l'interface
- **Met à jour** le modèle en conséquence
- Déclenche le **rafraîchissement** de la vue avec les nouvelles données
- Gère la **logique de navigation** et les **interactions**

Cette séparation nous permet de maintenir un code **modulaire**, facilement **testable**, et de faire évoluer chaque composant **indépendamment**.

## Réalisation technique

### Communication avec OAR

Notre dashboard interagit avec une instance OAR sur une plateforme spécifique en **SSH** via la commande `oarstat` pour récupérer les informations nécessaires à la visualisation des jobs et des ressources:

```bash
oarstat -J --gantt [--start-time START] [--stop-time STOP]
```

Cette commande génère des données au format JSON que nous traitons ensuite dans notre application:

- **Parser JSON**: Utilise la bibliothèque `serde` pour désérialiser les données JSON en structures Rust
- **Modèles de données**: Structures personnalisées représentant fidèlement les jobs et ressources
- **Cache intelligent**: Optimise les performances en évitant les appels répétés à `oarstat`
- **Gestion d'erreurs robuste**: Traitement des cas particuliers et récupération en cas d'échecs

Cette approche nous permet de manipuler efficacement les données OAR et d'offrir une interface réactive même avec un grand volume d'informations.

### Diagramme de Gantt

Le cœur visuel de notre application est un diagramme de Gantt interactif basé sur le framework Puffin, adapté pour visualiser les jobs OAR:

![Diagramme de Gantt](./screenshots/gantt.png)

*Figure 2: Diagramme de Gantt montrant l'allocation des ressources*

Caractéristiques principales:
- **Navigation temporelle**: Zoom et déplacement fluides sur l'axe temporel
- **Sélection interactive**: Focus sur un job spécifique pour plus de détails
- **Code couleur intuitif**: Représentation visuelle différente pour chaque job basée sur son id
- **Regroupement des ressources**: Affichage hiérarchique des nœuds et cœurs
- **Performance optimisée**: Rendu efficace même avec des milliers de jobs
- **Aggrégation des données**: Plusieurs niveaux d'aggréation sont disponibles pour une vue synthétique

Ce diagramme permet aux administrateurs de cluster de visualiser rapidement l'état du système, d'identifier les problèmes potentiels et de planifier efficacement les tâches.

### Tableau de bord détaillé

En complément du diagramme de Gantt, nous avons développé un tableau de bord détaillé fournissant une vue approfondie des jobs et ressources:

![Tableau de bord détaillé](./screenshots/dashboard.png)

*Figure 3: Tableau de bord montrant les détails des jobs sélectionnés*

Ce tableau de bord comprend:
- **Vue liste des jobs**: Affichage tabulaire avec tri par colonne et pagination avec des colonnes personnalisables
- **Informations détaillées**: Possibilité d'ouvrir une fenêtre de détails pour un job
- **Métriques en temps réel**: Le nombre de jobs dans chaque état est mis à jour en temps réel ainsi que les périodes d'activités visualisées
- **Graphiques du système**: Graphiques interactifs pour suivre l'évolution des états des jobs

Cette vue permet une analyse fine des jobs en cours, une gestion efficace des ressources et une prise de décision éclairée pour l'administration du cluster.

### Fenêtre de détails des jobs

Pour une compréhension approfondie des jobs, nous avons développé une fenêtre de détails affichant toutes les propriétés et métadonnées associées à un job:

![Détails des jobs](./screenshots/details.png)

*Figure 4: Fenêtre de détails des jobs avec toutes les informations pertinentes*

Cette fenêtre affiche:
- **Propriétés du job**: ID, propriétaire, état, messages, etc.
- **Historique des temporelles**: Dates de soumission, démarrage, fin, etc.
- **Resources associées**: Nombre de cœurs, nœuds, cluster, etc.

Cette fenêtre fournit une vue complète et détaillée de chaque job, permettant une analyse approfondie et une gestion efficace des tâches.

### Filtrage et recherche avancés

Pour faciliter la gestion d'un grand nombre de jobs, nous avons implémenté un système de filtrage multi-critères:

- **Filtrage par utilisateur**: Visualisation des jobs par propriétaire
- **Filtrage par état**: Sélection des jobs selon leur état (waiting, running, terminated, etc.)
- **Filtrage par ressources**: Sélection selon les clusters et hosts où s'exécutent les jobs
- **Filtrage par date**: Sélection des jobs selon leur date de d'exécution (le gantt lui-même permet d'ajuster ce filtre)

Ces filtres peuvent être combinés pour affiner progressivement la visualisation selon les besoins de l'utilisateur.

![Filtres avancés](./screenshots/filters.png)

*Figure 5: Interface de filtrage avancé pour les jobs OAR*

### Interface utilisateur adaptée

L'interface utilisateur a été conçue pour s'adapter aux différents contextes d'utilisation:

- **Mise en page adaptative**: Organisation dynamique des panneaux selon l'espace disponible
- **Mode compact/étendu**: Basculement facile entre différents niveaux de détail
- **Thèmes clair/sombre**: Adaptation aux préférences visuelles et conditions d'éclairage
- **Persistance des préférences**: Sauvegarde automatique des paramètres utilisateur
- **Intégréation i18n**: Prise en charge de plusieurs langues pour une portée internationale
- **Personnalisation de la taille de la police**: Ajustement de la taille du texte pour une meilleure lisibilité
- **Multi-plateforme**: Support de Linux, macOS, Windows et WebAssembly (Via trunk)
- **Mockup de données pour la version Web**: Possibilité de tester l'interface sans connexion à un serveur OAR avec des données fictives

![Page d'option utilisateur](./screenshots/option.png)

*Figure 6: Page d'options utilisateur pour personnaliser l'interface*

## Gestion de projet

### Organisation de l'équipe
Notre équipe de développement était composée de quatre membres, chacun ayant un rôle bien défini :

- DEL MEDICO Rémi - **Chef de projet** / **Développeur** : responsable du suivi global du projet, de la répartition des tâches, des communications avec le porteur du projet et dans une moindre mesure du même rôle que les développeurs.
- ARLE Alexandre - **Git Master** / **Développeur** : en charge de la mise en place et du maintient du répertoire Git. Une fois le répertoire configurer transfert sur un rôle de développeur.
- GOGUILLOT Amaury - **Développeur** : chargés de la conception et de l’implémentation des fonctionnalités ainsi que de la correction des bugs.
- MIRAS Romain - **Développeur** : chargés de la conception et de l’implémentation des fonctionnalités ainsi que de la correction des bugs.

### Méthodologie Agile & Sprints
![Gantt sprints](./screenshots/sprints.png)
*Figure 7: Gantt pour les phases de développement*

Nous avons adopté une approche Agile, en organisant notre travail sous forme de sprints (cf. Figure 7). Ainsi il y avait 5 phases avec 2 phases dédié au développement. Les 2 premières phases pour la mise en place du projet avec l'analyse du projet puis sa conception. Suite à cette étape de préparation, nous avons attaqué la partie développement avec dans un premier temps un focus sur la création des interfaces et des fonctionnalités de base puis lors d'une seconde phase de développement, un focus sur la correction des bugs et l'amélioration des fonctionnalités. Enfin lors de la dernière phase nous avons réaliser tous le travail de documentation.

### Gestion des Tâches avec un Système de Tickets
Chaque élément à développer ou à corriger était représenté par un ticket, qui pouvait correspondre à :

- Des fonctionnalités à implémenter,
- Des bugs à corriger,
- D’autres issues techniques à traiter.

Les tickets étaient priorisés et attribués aux développeurs, permettant une répartition claire des tâches et un suivi efficace de l'avancement du projet.

### Gestion de projet et collaboration
Pour assurer une bonne coordination et un suivi régulier du projet, nous avions mis en place un rituel hebdomadaire avec notre porteur de projet :

- Soit une réunion physique, favorisant une discussion plus approfondie sur les avancées, les éventuels obstacles et les décisions stratégiques à prendre.
- Soit un échange par e-mail, permettant de faire un point sur l’avancement et de lever d’éventuelles questions.

Ce suivi régulier nous a permis d’adapter notre travail aux attentes du porteur de projet et de garantir une bonne transparence tout au long du développement.

### Suivi du Projet et Communication
Le développement suivait un workflow précis basé sur Git :

- Un développeur créait une branche à partir de dev et y implémentait sa fonctionnalité.
- Une Pull Request (PR) était ensuite ouverte vers la branche dev.
- Généralement, le chef de projet se chargeait de la revue de code, ce qui permettait d’avoir une vision globale du projet et d’assurer la qualité du code.
- Après validation, la PR était fusionnée dans dev.
- Une fois que la branche dev avait atteind un niveaux de développement suffisant, elle pouvait être intégrée à la branche main pour la mise en production d'une nouvelle version.

## Outils

### Gestion de projet et collaboration

#### GitHub

Nous avons choisi GitHub comme plateforme de gestion du code source :

- **Repositories** : Organisation du code et de la documentation dans des dépôts dédiés ([app](https://github.com/info5-groupe-9-dashboard-rust/app) et [docs](https://github.com/info5-groupe-9-dashboard-rust/docs))
- **Issues** : Suivi des tâches, bugs et améliorations avec système d'assignation
- **Pull Requests** : Révision de code et intégration des fonctionnalités
- **Projects** : Tableau Kanban pour visualiser l'avancement global du projet

GitHub nous a permis de maintenir un flux de travail structuré et de garder une traçabilité complète des modifications et des décisions prises au cours du développement.

#### Discord

Discord a servi de hub de communication pour notre équipe :

- **Canaux thématiques** : Séparation des discussions concernant (général, ressources, questions, todo)
- **Partage de fichiers** : Échange rapide de code, captures d'écran et documents

Cet outil a facilité la communication pour notre équipe.

### Documentation

#### Diagrammes UML

Pour la conception et la documentation technique, nous avons utilisé des diagrammes UML :

- **Diagramme de contexte** : Illustre le système dans son contexte d'utilisation et ses interactions avec les acteurs externes
- **Vue de haut niveau** : Architecture générale et composants principaux
- **Vues détaillées** : Détaille la structure des différents composants
- **Vue système** : Présente une vue d'ensemble du système et ses interactions avec l'environnement extérieur.
- **Diagrammes de cas d'utilisation** : Fonctionnalités et intéractions utilisateur
- **Diagrammes de classes** : Structure et relations entre les composants
- **Diagrammes de séquence** : Flux d'interactions entre les modules

Ces représentations visuelles ont été essentielles pour clarifier l'architecture et faciliter la communication technique entre les membres de l'équipe.

### Environnement de développement

#### Visual Studio Code

VS Code a été notre IDE de prédilection, configuré avec une extension spécifique pour Rust :

- **rust-analyzer** : Support avancé pour le langage Rust avec autocomplétion intelligente, vérification d'erreurs en temps réel et navigation de code

Cette extension a considérablement amélioré notre productivité en offrant des fonctionnalités d'IDE complètes pour le développement Rust, permettant une meilleure expérience de développement pour les membres de l'équipe.

## Métriques logicielles

### Statistiques globales

- Total lignes de code : **6 450 lignes**
- Total GitHub issues complétées : **84 issues**
- Total commits : **177 commits**
- Total merged pull requests : **94 pull requests**

### Distribution des langages

| Langage    | Pourcentage | Représentation                                  |
|------------|-------------|--------------------------------------------------|
| Rust       | 97.7%       | 🦀 ████████████████████████████████████████████ |
| HTML       | 2.0%        | 🌐 █                                             |
| JavaScript | 0.3%        | 📜                                               |

### Contribution des développeurs

#### En nombre de lignes de code

| Contributeur      | Lignes  | Pourcentage | Représentation                                  |
|-------------------|---------|-------------|--------------------------------------------------|
| Rémi DEL MEDICO   | 2871    | 44.5%       | 🟡 ███████████████████████████████████          |
| Alexandre ARLE    | 1391    | 21.5%       | 🟢 █████████████████                            |
| Romain MIRAS      | 1371    | 21.3%       | 🔵 █████████████████                            |
| Amaury GOGUILLOT  | 817     | 12.7%       | 🟠 ████████                                     |

#### En nombre de commits

| Contributeur      | Commits | Pourcentage | Représentation                                  |
|-------------------|---------|-------------|--------------------------------------------------|
| Rémi DEL MEDICO   | 65      | 36.7%       | 🟡 ██████████████████████████████████           |
| Alexandre ARLE    | 44      | 24.8%       | 🟢 ██████████████████████                       |
| Romain MIRAS      | 42      | 23.8%       | 🔵 █████████████████████                        |
| Amaury GOGUILLOT  | 26      | 14.7%       | 🟠 ████████████                                 |

### Notes additionnelles
Ces métriques reflètent l'état du projet au 10 mars 2025 et sont susceptibles d'évoluer.

## Conclusion
### Résultats Obtenus
Au terme du projet, nous avons livré une application fonctionnelle respectant les principales exigences du cahier des charges. Parmi les résultats concrets :

- Un tableau de bord réactif avec un diagramme de Gantt interactif affichant l’état des jobs en temps réel
- Une interface ergonomique permettant une navigation fluide et intuitive
- Une intégration réussie avec OAR via SSH et JSON
- Une gestion avancée des filtres pour affiner la visualisation des tâches et des ressources
- Un code Rust robuste et documenté garantissant la maintenabilité et la performance
- Une version web (WebAssembly) expérimentale pour offrir plus de flexibilité d’utilisation

### Améliorations et Évolutions Futures
Le projet ouvre la voie à plusieurs évolutions intéressantes :

- Amélioration du mode WebAssembly pour une meilleure compatibilité et performance
- Personnalisation avancée de l’interface pour adapter l'affichage aux préférences utilisateur
- Prise en charge d’autres gestionnaires de tâches pour étendre l’usage au-delà d’OAR
- Ajout de statistiques et d’analyses pour aider à optimiser l’utilisation du cluster
- Éventuellement ajout de la gestion des jobs directement via l'application en plus du monitoring

### Conclusion
Ce projet a permis de moderniser l’administration des clusters OAR en fournissant un outil graphique performant, ergonomique et évolutif. En utilisant Rust, Egui et Puffin, nous avons pu garantir sécurité, fluidité et maintenabilité.

L’application développée est un premier jalon pour une meilleure gestion des ressources HPC et peut être enrichie à l’avenir par la communauté open source ou des équipes académiques.

Nous sommes fier de notre réalisation !

## Bibliographie
- [Description du projet](https://air.imag.fr/index.php/Dashboard_en_technologie_egui/rust_pour_plateforme_HPC)  
- [Documentation Rust](https://doc.rust-lang.org/book/)  
- [Documentation OAR Rest API](https://oar.imag.fr/docs/2.5/user/api.html)  
- [Documentation Grid'5000](https://api.grid5000.fr/doc/stable/)  
- [Outil gantt statique existant](https://intranet.grid5000.fr/oar/Grenoble/drawgantt-svg/)  
- [Github egui](https://github.com/emilk/egui)  
- [Github puffin](https://github.com/EmbarkStudios/puffin)  
- [Documentation eframe](https://docs.rs/eframe/latest/eframe/)  


## Glossaire

| Terme | Définition |
|-------|------------|
| **API REST** | Interface de programmation applicative utilisant des méthodes HTTP standard qui permet la communication entre systèmes distribués |
| **Cargo** | Le gestionnaire de paquets et système de build officiel pour Rust |
| **Cluster** | Ensemble d'ordinateurs connectés travaillant ensemble comme un système unifié |
| **CPU Core (Cœur)** | Unité de traitement indépendante au sein d'un processeur capable d'exécuter des instructions |
| **Dashboard** | Interface graphique présentant des informations clés et des métriques de manière synthétique |
| **Egui** | Bibliothèque d'interface utilisateur immédiate (immediate mode GUI) pour Rust |
| **Gantt (Diagramme)** | Outil de planification illustrant la relation entre les activités et le temps |
| **HPC** | High Performance Computing - Calcul haute performance utilisant des supercalculateurs pour résoudre des problèmes complexes |
| **Job** | Tâche de calcul soumise à OAR pour être exécutée sur le cluster |
| **MVC** | Modèle-Vue-Contrôleur, patron de conception séparant la logique métier, l'interface et le contrôle |
| **Nœud** | Machine individuelle (serveur) au sein d'un cluster |
| **OAR** | Gestionnaire de ressources et d'ordonnancement de tâches pour clusters HPC |
| **Puffin** | Profileur de performance open source pour les applications Rust |
| **Rust** | Langage de programmation système axé sur la sécurité, la concurrence et les performances |
| **SSH** | Secure Shell, protocole réseau sécurisé pour l'accès à distance à des systèmes informatiques |
| **WebAssembly** | Format de bytecode permettant l'exécution de code compilé dans les navigateurs web |
