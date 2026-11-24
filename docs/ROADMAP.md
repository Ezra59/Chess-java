# Roadmap — Chess Java

## Objectif

Développer un jeu d'échecs en Java disposant d'un moteur fiable, autonome, maintenable et évolutif, conformément au cahier des charges.

La priorité est donnée à la qualité de la logique métier avant le développement de l'interface graphique.

## Phase 1 — Analyse et conception

**Objectif : définir les fondations du projet.**

- [x] Définir les objectifs du projet
- [x] Choisir le langage de programmation
- [x] Choisir l'outil de build
- [x] Rédiger le cahier des charges
- [x] Créer le dépôt GitHub
- [ ] Valider le cahier des charges
- [ ] Intégrer le cahier des charges au dépôt
- [ ] Établir la feuille de route
- [ ] Réaliser le diagramme de cas d'utilisation
- [ ] Choisir et justifier l'architecture logicielle
- [ ] Définir les responsabilités des composants
- [ ] Réaliser le diagramme de classes UML initial
- [ ] Définir les contrats des classes
- [ ] Définir la stratégie de tests

## Phase 2 — Initialisation technique

**Objectif : disposer d'un environnement de développement opérationnel.**

- [ ] Initialiser le projet Maven
- [ ] Sélectionner la version de Java
- [ ] Définir l'organisation des packages
- [ ] Configurer le fichier .gitignore
- [ ] Configurer JUnit
- [ ] Configurer GitHub Actions
- [ ] Vérifier la compilation et l'exécution des tests

## Phase 3 — Fondations du moteur

**Objectif : représenter correctement l'état du jeu.**

- [ ] Implémenter la classe abstraite Piece
- [ ] Implémenter les différents types de pièces
- [ ] Implémenter la représentation de l'échiquier
- [ ] Gérer les coordonnées des cases
- [ ] Gérer les couleurs
- [ ] Initialiser les pièces
- [ ] Représenter une partie
- [ ] Gérer l'alternance des joueurs
- [ ] Tester la cohérence de l'état initial

## Phase 4 — Déplacements et interactions

**Objectif : gérer les déplacements élémentaires des pièces.**

- [ ] Implémenter les déplacements du pion
- [ ] Implémenter les déplacements de la tour
- [ ] Implémenter les déplacements du cavalier
- [ ] Implémenter les déplacements du fou
- [ ] Implémenter les déplacements de la dame
- [ ] Implémenter les déplacements du roi
- [ ] Gérer les obstacles
- [ ] Gérer les captures
- [ ] Gérer les limites de l'échiquier
- [ ] Enregistrer les coups joués
- [ ] Garantir l'intégrité des états
- [ ] Tester les déplacements et les interactions

## Phase 5 — Règles avancées

**Objectif : garantir la conformité du moteur aux règles des échecs.**

- [ ] Détecter les cases attaquées
- [ ] Détecter les situations d'échec
- [ ] Gérer les pièces clouées
- [ ] Garantir la légalité des déplacements
- [ ] Implémenter le roque
- [ ] Implémenter la prise en passant
- [ ] Implémenter la promotion
- [ ] Détecter l'échec et mat
- [ ] Détecter le pat
- [ ] Détecter les positions mortes
- [ ] Gérer les répétitions de position
- [ ] Gérer les règles des 50 et 75 coups
- [ ] Gérer les réclamations et accords de nullité
- [ ] Gérer l'abandon
- [ ] Gérer les résultats et les états de fin de partie
- [ ] Tester l'ensemble des règles avancées

## Phase 6 — Gestion des parties

**Objectif : permettre la conservation et la reprise des parties.**

- [ ] Compléter l'historique des coups
- [ ] Implémenter la notation algébrique standard
- [ ] Définir le format de sauvegarde
- [ ] Implémenter la sauvegarde
- [ ] Implémenter le chargement
- [ ] Valider les données importées
- [ ] Tester la restauration complète d'une partie

## Phase 7 — Validation du moteur

**Objectif : disposer d'un moteur fiable avant le développement graphique.**

- [ ] Vérifier la conformité au cahier des charges
- [ ] Exécuter les tests unitaires
- [ ] Exécuter les tests d'intégration
- [ ] Vérifier les cas limites
- [ ] Réaliser les tests Perft
- [ ] Mesurer la couverture des tests
- [ ] Mesurer les performances
- [ ] Analyser la qualité du code
- [ ] Corriger les anomalies
- [ ] Effectuer les refactorisations nécessaires
- [ ] Finaliser la documentation du moteur
- [ ] Valider une version stable du moteur

## Phase 8 — Interface graphique

**Objectif : proposer une application jouable par deux utilisateurs en local.**

- [ ] Choisir la technologie graphique
- [ ] Concevoir les interfaces
- [ ] Implémenter l'écran d'accueil
- [ ] Afficher l'échiquier et les pièces
- [ ] Gérer les interactions utilisateur
- [ ] Connecter l'interface au moteur
- [ ] Afficher les informations de la partie
- [ ] Gérer visuellement les promotions
- [ ] Intégrer la sauvegarde et le chargement
- [ ] Afficher les résultats
- [ ] Évaluer les fonctionnalités secondaires
- [ ] Tester l'application graphique

## Phase 9 — Recette et livraison

**Objectif : publier la première version stable.**

- [ ] Vérifier toutes les exigences obligatoires
- [ ] Effectuer la recette fonctionnelle
- [ ] Vérifier la sécurité des dépendances
- [ ] Vérifier la portabilité
- [ ] Finaliser la documentation technique
- [ ] Rédiger le guide utilisateur
- [ ] Finaliser le README
- [ ] Générer les artefacts exécutables
- [ ] Documenter les limitations connues
- [ ] Publier la release v1.0.0

## Évolutions futures

Hors périmètre de la version 1.0 :

- [ ] Intelligence artificielle
- [ ] Multijoueur en ligne
- [ ] Système de comptes utilisateurs
- [ ] Classement ELO
- [ ] Matchmaking
- [ ] Analyse des parties
- [ ] Mode spectateur
- [ ] Tournois

## Règles de suivi

- Les tests sont développés tout au long du projet.
- Chaque décision technique importante doit être justifiée.
- Les modifications architecturales doivent être documentées.
- Une tâche ne peut être considérée comme terminée que si elle respecte les critères de validation applicables.
- La feuille de route peut évoluer en fonction des contraintes rencontrées.
- La qualité du moteur reste prioritaire sur les fonctionnalités secondaires.
