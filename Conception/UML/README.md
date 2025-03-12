# Diagrammes UML

Ce dossier contient tous les diagrammes UML liés à la modélisation du projet Dashboard Rust/Egui.

## Diagrammes disponibles

### Diagramme de Classes Simplifié
<p align="center">
    <img src="./Class%20Diagram/Diagrammes%20UML%20-%20Diagramme%20de%20classe%20simplifié.png" alt="Diagramme de Classes">
</p>

> Représente la structure statique du système en montrant les classes et les relations entre elles de manière simplifiée. Cela décrit en partie le modèle MVC.

### Diagramme de Cas d'Utilisation
<p align="center">
    <img src="./Use_Case/use_case.png" alt="Diagramme de Cas d'Utilisation">
</p>

> Montre les différentes fonctionnalités du système du point de vue de l'utilisateur.

### Diagramme de Séquence - Fetching & Parsing of Data
<p align="center">
    <img src="./Sequence%20Diagram/Diagrammes%20UML-Diagramme%20de%20Séquence%20-%20Fetching%20&%20Parsing%20of%20Data.png" alt="Diagramme de Séquence">
</p>

> Montre le déroulement des actions entre les objets du système pour récupérer et traiter les données.
> L'application envoie des requêtes d'actualisation de données de façon périodique sur une plage de temps donnée.
> Elle crée un thread pour chaque requête et attend la réponse pour traiter les données.
> Une connexion SSH est établie pour récupérer les données en format JSON qui seront ensuite traitées et parsées afin de créer les objets nécessaires pour l'affichage.

### Diagramme d'États
⚠️ **TODO**

> Décrit les différents états possibles d'un objet et les transitions entre ces états.

### Diagramme d'Activités
⚠️ **TODO**

> Représente le flux de contrôle d'une activité à une autre dans le système.

## Edition des diagrammes 

Les diagrammes ont été réalisés avec l'outil [drawio](https://app.diagrams.net/). Vous pouvez les éditer en important le fichier `.drawio` se trouvant à la base de ce dossier.
