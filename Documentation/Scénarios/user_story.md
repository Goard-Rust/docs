# Scénarios d'utilisation du Dashboard Rust/Egui

Ce document est associé au diagramme de cas d'utilisation suivant :

![Diagramme de cas d'utilisation](https://github.com/info5-groupe-9-dashboard-rust/docs/blob/main/Conception/UML/Use_Case/use_case.png)

## 1. Authentification (UC1)
**Acteur** : Administrateur\
**Préconditions** : L’administrateur dispose d’un compte valide.\
**Postconditions** : L’administrateur est connecté et peut accéder aux fonctionnalités du dashboard.

### Description :
1. L’administrateur accède à l’interface de connexion.
2. Il saisit ses identifiants (nom d’utilisateur et mot de passe).
3. Le système vérifie les informations d’authentification.
4. Si les informations sont correctes, l’administrateur est redirigé vers l'interface Gantt.
5. En cas d’échec, un message d’erreur est affiché, et il peut réessayer.

---

## 2. Consulter le planning des tâches (Gantt) (UC2)
**Acteur** : Administrateur\
**Préconditions** : L’administrateur est authentifié.\
**Postconditions** : L’administrateur a une vue d’ensemble des tâches planifiées.

### Description :
1. L’administrateur accède à l'onglet du planning Gantt via le menu de navigation.
2. Le système affiche un diagramme Gantt des tâches planifiées.
3. L’administrateur peut naviguer dans le planning, zoomer, se déplacer dans le temps ou filtrer les tâches affichées.

---

## 3. Rechercher une tâche (UC3)
**Acteur** : Administrateur\
**Préconditions** : L’administrateur est authentifié.\
**Postconditions** : La tâche recherchée est affichée dans la vue Dashboard et Gantt si elle existe.

### Description :
1. L’administrateur accède à la fenêtre de filtrage en cliquant sur le bouton `Filtres`.
2. L'administrateur sélectionne des options de filtrages selon le critère choisi (owner, state, cluster, host).
3. L'administrateur clique sur le bouton `Appliquer`.
4. Le système effectue un filtrage et affiche les résultats (jobs) correspondants à la fois dans la vue Dashboard et Gantt.

---

## 4. Consulter les détails d’une tâche (UC4)
**Acteur** : Administrateur\
**Préconditions** : L’administrateur est authentifié et a trouvé une tâche via la recherche, le dashboard ou le planning Gantt.\
**Postconditions** : L’administrateur a consulté les informations complètes d’une tâche.

### Description :
1. L’administrateur sélectionne une tâche spécifique dans l'interface Dashboard ou Gantt.
2. Le système affiche les informations détaillées de la tâche sélectionnée dans une nouvelle fenêtre.
3. L’administrateur peut consulter ces détails tout en gardant oeil sur l'interface Dashboard ou Gantt.
4. L'administrateur peut fermer cette fenêtre.
