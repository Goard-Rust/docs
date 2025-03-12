### **Rapport Technique : Technologies Employées (Détail)**

---

#### **Introduction**

Ce rapport technique détaille les technologies sélectionnées pour le développement du projet de **Dashboard en technologie egui/Rust pour plateforme HPC**. Le choix des technologies repose sur leur performance, leur compatibilité avec les besoins du projet et leur capacité à s’intégrer dans l’écosystème HPC. Notamment, l’utilisation de la bibliothèque **Puffin** comme base de code pour la création d’un diagramme de Gantt est un aspect clé de ce projet.

---

### **1\. Langage de Programmation : Rust**

#### **Présentation**

Rust est un langage de programmation moderne, orienté performance et sécurité. Conçu pour remplacer des langages comme C/C++ dans des contextes exigeants, Rust propose une gestion fine de la mémoire grâce à son modèle d’ownership.

#### **Pourquoi Rust pour ce projet ?**

1. **Performance** : Les applications Rust offrent des performances comparables à celles de C/C++, idéales pour les environnements HPC où l'efficacité est cruciale.  
2. **Sécurité mémoire** : Le système de vérification de la mémoire réduit les erreurs critiques comme les dépassements de tampon ou les *data races*.  
3. **Richesse de l’écosystème** : Rust dispose d’outils comme Cargo pour simplifier la gestion des dépendances, des tests, et des builds.  
4. **Conception asynchrone** : Grâce à son support natif de l’asynchronisme, Rust facilite la gestion des I/O nécessaires pour la visualisation et l’analyse des tâches.

#### **Limites**

* Une courbe d’apprentissage relativement abrupte, surtout pour les développeurs novices.  
* Une communauté encore émergente en matière de GUI comparée à des langages comme Python ou JavaScript.

---

### **2\. Bibliothèque GUI : Egui (Immediate Mode GUI)**

#### **Présentation**

Egui est une bibliothèque graphique légère pour Rust qui adopte un mode immédiat (*Immediate Mode GUI*). Ce paradigme est plus simple et souvent plus rapide à utiliser pour des projets nécessitant des interfaces simples et dynamiques.

#### **Caractéristiques principales**

1. **Mode immédiat** : Pas besoin de stocker explicitement l’état de l’interface entre les images, ce qui rend le développement plus intuitif.  
2. **Performance et légèreté** : Optimisé pour des mises à jour fréquentes, comme celles nécessaires pour des diagrammes interactifs.  
3. **Simplicité de développement** : Facile à configurer et à étendre, avec une documentation claire et active.  
4. **Support multi-plateforme** : Fonctionne sur les principaux systèmes d'exploitation : Windows, macOS, et Linux.

#### **Pourquoi utiliser Egui pour ce projet ?**

* **Prototype rapide** : Permet de concevoir une interface utilisateur fonctionnelle sans une courbe d’apprentissage trop longue.  
* **Compatibilité avec Puffin** : Les widgets d’Egui permettent d’intégrer facilement les visualisations de Puffin pour le diagramme de Gantt.

#### **Limites**

* Moins adapté pour les interfaces complexes ou très personnalisées.  
* Manque d'outils graphiques avancés par rapport à d'autres bibliothèques comme GTK ou Qt.

---

### **3\. Visualisation : Puffin pour le Diagramme de Gantt**

#### **Présentation**

Puffin est une bibliothèque Rust conçue pour la création de profils interactifs et de diagrammes visuels. Elle est particulièrement utilisée pour analyser les performances d’applications en traçant des événements temporels sous forme de *flamegraphs*.

#### **Caractéristiques principales**

1. **Flamegraphs dynamiques** : Permet de visualiser les tâches et sous-tâches en parallèle dans un format interactif.  
2. **Intégration avec Egui** : Puffin utilise directement les outils graphiques d’Egui, ce qui simplifie son utilisation dans le projet.  
3. **Performant** : Conçu pour les environnements où les données à visualiser sont massives, comme les tâches d’un gestionnaire de ressources HPC.

#### **Pourquoi reutiliser Puffin pour ce projet ?**

1. **Diagramme de Gantt** : Puffin peut être adapté pour afficher un diagramme de Gantt montrant la chronologie des tâches HPC.  
   * Chaque tâche peut être représentée comme une barre horizontale, positionnée selon son début et sa fin.  
   * Les sous-tâches ou dépendances peuvent être imbriquées ou reliées entre elles.  
2. **Analyse interactive** : Puffin permet aux utilisateurs de zoomer et de naviguer dans le diagramme pour une analyse détaillée des tâches.  
3. **Écosystème Rust natif** : Écrit en Rust, Puffin s’intègre parfaitement au reste des technologies du projet, sans dépendances externes lourdes.

#### **Exemples d’utilisation**

* Visualisation des tâches OAR, montrant le début, la durée, et l’état de chaque tâche.  
* Mise en évidence des ressources utilisées ou des conflits éventuels dans le calendrier.

#### **Limites**

* La personnalisation des graphes pour un cas d’utilisation précis (comme un diagramme de Gantt) peut nécessiter un travail supplémentaire.  
* Documentation parfois insuffisante pour des usages avancés.

---

### **4\. Gestionnaire de tâches et de ressources : OAR**

#### **Présentation**

OAR est un gestionnaire de ressources open source largement utilisé pour la planification et l’exécution de tâches sur des clusters HPC.

#### **Caractéristiques principales**

1. **Planification des tâches** : Gère l’allocation des ressources en fonction des priorités et des contraintes définies.  
2. **Extensibilité** : Offre des API et des interfaces pour interagir avec des outils tiers, comme le dashboard développé dans ce projet.  
3. **Open source** : Possibilité de simuler ou d’intégrer OAR dans un environnement Rust pour tester l’application.

---

### **5\. Outils de développement et gestion de projet**

#### **5.1. Environnement de Développement**

* **IDE : Visual Studio Code**  
  * Extension : **Rust Analyzer** pour l’auto-complétion et le diagnostic en temps réel.

#### **5.2. Gestion de version**

* **Git** pour le contrôle de version. Hébergement sur des plateformes comme GitHub ou GitLab.  
* Suivi des tâches avec un système de branches clair (e.g., `feature/diagramme-gantt`, `feature/visualisation-ressources`).

#### **5.3. Gestion des dépendances**

* Utilisation de **Cargo** pour gérer les bibliothèques comme `eframe`, `egui` et `puffin`.  
* Automatisation des tests et des builds avec des commandes comme `cargo test` et `cargo-tarpaulin`.

#### **5.4. Centralisation du code**

* Choix de l’envionnement de **Github** pour la centralisation des dêpots de code et de documentation  
* Création d’une organisation avec deux dêpots public

---

### **Conclusion**

Le choix des technologies Rust, Egui, Eframe, et Puffin, associé à OAR, constitue une solution cohérente et robuste pour développer un dashboard HPC performant et moderne. L’intégration de Puffin pour la création d’un diagramme de Gantt permet une visualisation détaillée et interactive des tâches et des ressources.

Ce rapport met en évidence les avantages et limitations des technologies employées, offrant un cadre clair pour la mise en œuvre du projet.

