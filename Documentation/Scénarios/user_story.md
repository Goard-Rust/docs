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
4. Si les informations sont correctes, l’administrateur est redirigé vers le tableau de bord.
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
**Postconditions** : La tâche recherchée est trouvée et affichée si elle existe.

### Description :
1. L’administrateur accède à la barre de recherche des tâches.
2. Il saisit un mot-clé, un identifiant de tâche ou un critère spécifique.
3. Le système effectue une recherche et affiche les résultats correspondants.
4. L’administrateur peut sélectionner une tâche parmi les résultats.

---

## 4. Consulter les détails d’une tâche (UC4)
**Acteur** : Administrateur\
**Préconditions** : L’administrateur est authentifié et a trouvé une tâche via la recherche ou le planning Gantt.\
**Postconditions** : L’administrateur a consulté les informations complètes d’une tâche.

### Description :
1. L’administrateur sélectionne une tâche spécifique.
2. Le système affiche les informations détaillées de la tâche.
3. L’administrateur peut consulter ces détails et revenir à l’affichage précédent.
