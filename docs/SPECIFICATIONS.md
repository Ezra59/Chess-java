# Cahier des charges — Jeu d'échecs Java

**Version du document :** 1.0  
**Date :** 24 novembre 2026  
**Type de projet :** Application de bureau  
**Langage principal :** Java  
**Outil de build :** Maven  
**Statut :** Phase de conception

---

# 1. Présentation du projet

## 1.1. Contexte

Le projet consiste à concevoir et développer une application permettant de jouer aux échecs dans le respect des règles officielles du jeu.

Le développement devra privilégier la fiabilité du moteur de jeu, la qualité du code, la maintenabilité et l'évolutivité de l'application.

Le moteur devra être développé indépendamment de toute interface graphique afin de permettre son exploitation dans différents environnements.

## 1.2. Objectifs principaux

- Développer un moteur d'échecs fiable et autonome.
- Respecter l'ensemble des règles échiquéennes retenues pour la première version.
- Permettre à deux joueurs de s'affronter localement.
- Garantir la cohérence de l'état d'une partie.
- Concevoir une architecture maintenable et évolutive.
- Disposer d'une couverture de tests significative.
- Permettre l'intégration future de nouvelles fonctionnalités sans refonte majeure du moteur.

## 1.3. Public cible

L'application s'adresse principalement :

- Aux joueurs débutants.
- Aux joueurs occasionnels.
- Aux joueurs expérimentés souhaitant jouer localement.
- Aux utilisateurs souhaitant analyser leurs parties lors des futures évolutions.

# 2. Périmètre du projet

## 2.1. Fonctionnalités de la première version

La version 1.0 devra permettre :

- La création d'une partie.
- L'affrontement entre deux joueurs locaux.
- La représentation graphique de l'échiquier.
- La gestion complète des déplacements.
- La gestion des captures.
- La gestion des règles spéciales.
- La détection des échecs et des fins de partie.
- La consultation de l'historique des coups.
- La sauvegarde et le chargement d'une partie.
- L'abandon d'une partie.
- Le lancement d'une nouvelle partie.

## 2.2. Fonctionnalités secondaires

Les fonctionnalités suivantes sont souhaitables, mais ne devront pas compromettre la qualité du moteur :

- Chronomètre individuel.
- Personnalisation de l'échiquier.
- Affichage des pièces capturées.
- Rotation de l'échiquier.
- Effets sonores.
- Annulation et rétablissement des coups en mode entraînement.
- Affichage des déplacements possibles.

## 2.3. Évolutions futures

Les fonctionnalités suivantes sont exclues du périmètre initial :

- Intelligence artificielle.
- Multijoueur en ligne.
- Création de comptes utilisateurs.
- Système de classement ELO.
- Système de matchmaking.
- Historique des parties en ligne.
- Analyse automatique des parties.
- Mode spectateur.
- Tournois.
- Application mobile.
- Détection de triche.

Leur absence dans la première version ne devra pas empêcher leur intégration ultérieure.

# 3. Priorisation des exigences

Les exigences seront classées selon la méthode MoSCoW :

| Priorité | Signification |
|---|---|
| MUST | Indispensable à la livraison |
| SHOULD | Importante, mais reportable |
| COULD | Facultative |
| WON'T | Exclue de la version actuelle |

La fiabilité des règles métier est prioritaire sur les fonctionnalités graphiques et secondaires.

# 4. Exigences fonctionnelles — Moteur de jeu

## 4.1. Initialisation de l'échiquier

**Référence : FONC-001 — MUST**

Le système devra :

- Représenter un échiquier de 8 × 8 cases.
- Identifier chaque case par des coordonnées uniques.
- Initialiser les 32 pièces conformément aux règles officielles.
- Attribuer une couleur à chaque pièce.
- Garantir qu'une case ne puisse contenir qu'une seule pièce.
- Garantir que chaque pièce présente en jeu n'occupe qu'une seule case.
- Initialiser correctement les droits de déplacement particuliers.
- Attribuer le premier tour au joueur blanc.

Toute nouvelle partie devra être indépendante des parties précédentes.

## 4.2. Gestion des pièces

**Référence : FONC-002 — MUST**

Le moteur devra prendre en charge les six types de pièces :

- Pion.
- Tour.
- Cavalier.
- Fou.
- Dame.
- Roi.

Chaque pièce devra respecter ses caractéristiques et ses comportements propres.

Le moteur devra permettre de distinguer les pièces alliées des pièces adverses.

Une pièce ne pourra pas changer de couleur au cours d'une partie.

## 4.3. Gestion des déplacements

**Référence : FONC-003 — MUST**

Le moteur devra vérifier la légalité de chaque déplacement avant son application.

La validation devra notamment prendre en compte :

- L'existence d'une pièce sur la case de départ.
- Le joueur dont c'est le tour.
- Les limites de l'échiquier.
- Les règles propres à la pièce.
- Les obstacles éventuels.
- L'occupation de la case de destination.
- Les règles spéciales applicables.
- La sécurité du roi du joueur concerné.
- L'état actuel de la partie.

Un déplacement vers la case de départ devra être refusé.

Un déplacement refusé ne devra entraîner aucune modification de l'état de la partie.

## 4.4. Déplacements propres aux pièces

**Référence : FONC-004 — MUST**

Le moteur devra respecter les déplacements suivants :

| Pièce | Déplacement |
|---|---|
| Pion | Avance rectiligne, capture diagonale |
| Tour | Horizontal ou vertical |
| Cavalier | Déplacement en L |
| Fou | Diagonal |
| Dame | Horizontal, vertical ou diagonal |
| Roi | Une case dans toutes les directions |

Le premier déplacement du pion, les obstacles, les captures et les exceptions devront être traités conformément au règlement de référence.

## 4.5. Gestion des obstacles

**Référence : FONC-005 — MUST**

Le moteur devra empêcher les pièces concernées de traverser une case occupée.

Le cavalier devra pouvoir franchir les pièces intermédiaires.

La présence d'un obstacle devra être prise en compte indépendamment de sa couleur.

## 4.6. Gestion des captures

**Référence : FONC-006 — MUST**

Le moteur devra permettre la capture des pièces adverses lorsque les conditions réglementaires sont respectées.

Il devra empêcher :

- La capture d'une pièce alliée.
- La capture d'une pièce inaccessible.
- Toute capture contraire aux règles de déplacement.
- La capture effective d'un roi.

Une pièce capturée devra être retirée de l'échiquier et ne pourra plus intervenir dans la partie.

Une capture valide devra être enregistrée dans l'historique.

## 4.7. Gestion du roque

**Référence : FONC-007 — MUST**

Le moteur devra prendre en charge le petit roque et le grand roque pour les deux couleurs.

Il devra vérifier :

- Les droits de roque du joueur.
- La présence du roi et de la tour concernés sur leurs cases requises.
- L'absence d'obstacles entre les deux pièces.
- L'absence d'échec du roi avant le déplacement.
- La sécurité des cases traversées et atteintes par le roi.

Le déplacement des deux pièces devra constituer une seule opération de jeu.

Un roi ou une tour ayant perdu son droit de roque ne devra pas le retrouver simplement en revenant sur sa case initiale.

## 4.8. Gestion de la prise en passant

**Référence : FONC-008 — MUST**

Le moteur devra autoriser la prise en passant uniquement lorsque les conditions réglementaires sont réunies.

Il devra prendre en compte le dernier coup effectué et la durée de validité de cette possibilité.

La pièce capturée devra être retirée de sa case réelle, même lorsque cette case diffère de la destination du pion effectuant la capture.

## 4.9. Gestion de la promotion

**Référence : FONC-009 — MUST**

Lorsqu'un pion atteint la dernière rangée, le système devra permettre sa promotion en :

- Dame.
- Tour.
- Fou.
- Cavalier.

Le choix ne devra pas dépendre des pièces précédemment capturées.

Le moteur devra permettre la présence de plusieurs pièces issues d'une promotion appartenant au même type.

La promotion devra être intégrée au coup concerné avant le passage au joueur suivant.

## 4.10. Gestion des tours

**Référence : FONC-010 — MUST**

Les joueurs devront jouer alternativement.

Le joueur blanc devra commencer la partie.

Un changement de tour ne devra intervenir qu'après l'exécution complète d'un coup légal.

Un déplacement invalide ne devra pas provoquer de changement de joueur.

## 4.11. Détection des cases attaquées

**Référence : FONC-011 — MUST**

Le moteur devra déterminer les cases attaquées par chaque couleur.

Il devra distinguer :

- Une case attaquée.
- Une destination géométriquement accessible.
- Un déplacement légal.

Cette distinction devra notamment permettre de traiter correctement les pièces clouées, les attaques des pions, les déplacements du roi et le roque.

## 4.12. Gestion de l'échec

**Référence : FONC-012 — MUST**

Le moteur devra détecter lorsqu'un roi est menacé.

Un joueur en échec ne pourra effectuer qu'un coup permettant de supprimer cette menace.

Le moteur devra empêcher tout déplacement exposant ou laissant son propre roi en échec.

Les situations d'échec simple et d'échec double devront être prises en charge.

## 4.13. Gestion de l'échec et mat

**Référence : FONC-013 — MUST**

Le moteur devra reconnaître les situations d'échec et mat.

Lorsqu'un mat est détecté :

- La partie devra être terminée.
- Le vainqueur devra être identifié.
- Aucun nouveau déplacement ne devra être autorisé.

## 4.14. Gestion des parties nulles

**Référence : FONC-014 — MUST**

Le moteur devra traiter les différentes conditions de partie nulle :

- Pat.
- Position morte.
- Accord mutuel des joueurs.
- Répétition de position.
- Règles relatives au nombre de coups sans progression de pion ni capture.

Le système devra distinguer les nulles nécessitant une réclamation du joueur des nulles automatiques.

Il devra notamment prendre en charge les réclamations après trois répétitions ou 50 coups de chaque joueur, ainsi que les nulles automatiques après cinq répétitions ou 75 coups de chaque joueur.

Les réclamations fondées sur un coup légal envisagé devront également être possibles.

La comparaison des positions devra tenir compte des droits de jeu, et pas uniquement de la disposition visible des pièces.

Une position morte ne devra pas être assimilée exclusivement à un nombre insuffisant de pièces.

Les priorités entre les différentes conditions de fin de partie devront suivre le règlement officiel.

## 4.15. Abandon de partie

**Référence : FONC-015 — MUST**

Chaque joueur devra pouvoir abandonner une partie en cours.

Le résultat devra être établi conformément aux règles retenues, notamment lorsque l'adversaire ne dispose d'aucune possibilité légale de réaliser un mat.

## 4.16. États de la partie

**Référence : FONC-016 — MUST**

Le système devra permettre de déterminer si une partie est :

- En cours.
- Terminée par une victoire blanche.
- Terminée par une victoire noire.
- Terminée par une partie nulle.

Le moteur devra également pouvoir fournir le motif de fin de partie.

Une partie terminée ne devra plus accepter de nouveaux coups.

## 4.17. Historique des coups

**Référence : FONC-017 — MUST**

Chaque coup légal devra être enregistré.

L'historique devra contenir suffisamment d'informations pour :

- Identifier le coup joué.
- Identifier le joueur concerné.
- Identifier les cases de départ et d'arrivée.
- Identifier les captures éventuelles.
- Identifier les promotions et déplacements spéciaux.
- Reconstituer une partie depuis sa position initiale.

L'historique affiché devra respecter la notation algébrique standard des échecs.

Les déplacements invalides ne devront pas apparaître dans l'historique.

# 5. Exigences fonctionnelles — Gestion des parties

## 5.1. Création d'une partie

**Référence : FONC-018 — MUST**

L'utilisateur devra pouvoir :

- Créer une nouvelle partie.
- Renseigner le nom des joueurs.
- Attribuer les couleurs.
- Recommencer une partie terminée.

La création d'une nouvelle partie ne devra pas réutiliser accidentellement l'état d'une partie précédente.

## 5.2. Sauvegarde

**Référence : FONC-019 — MUST**

Le système devra permettre de sauvegarder une partie localement.

La sauvegarde devra conserver toutes les informations nécessaires à une reprise exacte de la partie, notamment :

- La disposition des pièces.
- Le joueur actif.
- Les droits de roque.
- Les possibilités de prise en passant.
- L'historique nécessaire aux règles de répétition.
- Les compteurs réglementaires.
- Le résultat éventuel.
- Les paramètres de la partie.
- Les temps restants si un chronomètre est utilisé.

Le format de sauvegarde devra être documenté et versionné.

## 5.3. Chargement

**Référence : FONC-020 — MUST**

L'utilisateur devra pouvoir reprendre une partie sauvegardée.

Le système devra vérifier la validité et la cohérence des données chargées.

Un fichier absent, corrompu, invalide ou incompatible devra être refusé proprement.

Un échec de chargement ne devra pas altérer une partie déjà en cours.

## 5.4. Annulation d'un coup

**Référence : FONC-021 — COULD**

En mode entraînement, le système pourra permettre l'annulation et le rétablissement d'un coup.

Cette opération devra restaurer l'intégralité de l'état concerné, y compris les droits particuliers, les compteurs, les pièces capturées et le joueur actif.

Cette fonctionnalité devra être désactivée dans les futurs modes compétitifs.

## 5.5. Chronomètre

**Référence : FONC-022 — SHOULD**

Le système pourra permettre de configurer une durée de jeu individuelle.

Il devra alors :

- Décompter le temps du joueur actif.
- Suspendre le décompte du joueur inactif.
- Gérer les éventuels incréments.
- Détecter l'expiration du temps.
- Déterminer le résultat conformément aux règles applicables.
- Arrêter les chronomètres lorsque la partie se termine.

# 6. Exigences relatives à l'interface graphique

## 6.1. Principes généraux

**Référence : IHM-001 — MUST**

L'application devra proposer une interface graphique intuitive, lisible et indépendante de la logique métier.

La technologie JavaFX est envisagée, sous réserve de validation technique.

## 6.2. Écran d'accueil

**Référence : IHM-002 — MUST**

L'écran d'accueil devra permettre :

- De créer une partie.
- De charger une sauvegarde.
- D'accéder aux paramètres.
- De quitter l'application.

## 6.3. Écran de jeu

**Référence : IHM-003 — MUST**

L'écran de jeu devra afficher :

- L'échiquier.
- Les pièces en jeu.
- Les noms des joueurs.
- Le joueur actif.
- L'historique des coups.
- Les informations d'échec.
- Le résultat de la partie.

L'utilisateur devra pouvoir sélectionner une pièce et sa case de destination.

Les actions impossibles devront être refusées de manière compréhensible.

## 6.4. Assistance visuelle

**Référence : IHM-004 — SHOULD**

L'interface pourra afficher :

- La pièce sélectionnée.
- Les destinations légales.
- Le dernier déplacement effectué.
- Les pièces capturées.
- Les coordonnées de l'échiquier.
- Le roi en échec.

Les indications devront être calculées à partir des informations fournies par le moteur.

## 6.5. Promotion

**Référence : IHM-005 — MUST**

Lors d'une promotion, l'interface devra permettre au joueur de sélectionner l'une des quatre pièces autorisées.

Le joueur suivant ne devra pas pouvoir intervenir avant la validation de cette sélection.

## 6.6. Accessibilité

**Référence : IHM-006 — SHOULD**

L'interface devra privilégier :

- Une taille de texte lisible.
- Un contraste suffisant.
- Une identification claire des pièces.
- Des indications ne reposant pas uniquement sur la couleur.
- Une utilisation au clavier lorsque cela est possible.
- Une adaptation aux dimensions de la fenêtre.

## 6.7. Gestion des erreurs

**Référence : IHM-007 — MUST**

Les messages d'erreur devront être explicites et compréhensibles.

Les détails techniques internes ne devront pas être présentés directement à l'utilisateur.

# 7. Contraintes techniques

## 7.1. Langage et environnement

**Référence : TECH-001 — MUST**

- Langage : Java.
- Outil de build : Maven.
- Gestion de versions : Git.
- Gestion des dépendances : Maven.
- Tests unitaires : JUnit.
- Dépôt distant : GitHub recommandé.
- Intégration continue : GitHub Actions recommandé.

Une version LTS de Java devra être sélectionnée, documentée et utilisée de manière cohérente dans tous les environnements.

La version exacte des outils reste à valider.

## 7.2. Architecture logicielle

**Référence : TECH-002 — MUST**

L'architecture devra respecter les exigences suivantes :

- Séparation de la logique métier et de l'interface graphique.
- Responsabilités clairement définies.
- Encapsulation des données.
- Maîtrise des dépendances entre les composants.
- Faible couplage lorsque cela est pertinent.
- Forte cohésion des composants.
- Absence de duplication injustifiée des informations métier.
- Possibilité de tester le moteur indépendamment.
- Limitation de la complexité inutile.

Le choix des classes, interfaces, relations et design patterns relève de la phase de conception.

Aucun pattern ne devra être introduit sans justification technique.

## 7.3. Indépendance du moteur

**Référence : TECH-003 — MUST**

Le moteur devra pouvoir fonctionner :

- Sans interface graphique.
- Sans connexion Internet.
- Sans base de données distante.
- Sans intervention manuelle pendant les tests.

Une modification de l'interface graphique ne devra pas nécessiter de modification des règles métier.

Les futurs clients graphiques, réseau ou d'intelligence artificielle devront pouvoir exploiter les fonctionnalités du moteur à travers des contrats clairement définis.

## 7.4. Intégrité des données

**Référence : TECH-004 — MUST**

Le moteur devra garantir les invariants suivants :

- Une case ne contient jamais plusieurs pièces.
- Une pièce en jeu n'occupe jamais plusieurs cases.
- Les deux rois restent présents pendant une partie normale.
- Une pièce capturée ne peut plus jouer.
- Un coup illégal ne modifie pas la partie.
- Les informations relatives aux droits de jeu restent cohérentes.
- Une partie terminée ne peut pas être poursuivie.
- Les informations dupliquées, lorsqu'elles sont nécessaires, restent synchronisées.

Les opérations publiques du moteur devront empêcher la création accidentelle d'états incohérents.

## 7.5. Gestion des erreurs

**Référence : TECH-005 — MUST**

Le logiciel devra distinguer :

- Les erreurs de saisie.
- Les coups illégaux.
- Les erreurs de sauvegarde.
- Les erreurs de chargement.
- Les erreurs internes inattendues.

Les erreurs attendues devront être traitées sans arrêt brutal de l'application.

Les conventions de gestion des erreurs devront être documentées.

## 7.6. Qualité du code

**Référence : TECH-006 — MUST**

Le code devra :

- Respecter les conventions de nommage Java.
- Employer des noms de classes et de méthodes explicites.
- Éviter les nombres magiques.
- Limiter les duplications.
- Éviter les dépendances circulaires injustifiées.
- Éviter les méthodes excessivement complexes.
- Documenter les comportements non évidents.
- Privilégier la lisibilité.

Les principes SOLID, DRY, KISS et YAGNI serviront de références de conception.

## 7.7. Dépendances externes

**Référence : TECH-007 — MUST**

Toute dépendance devra être justifiée.

Les dépendances devront être :

- Maintenues.
- Compatibles avec la version Java retenue.
- Associées à une licence compatible avec le projet.
- Déclarées dans le fichier de configuration Maven.
- Vérifiées vis-à-vis des vulnérabilités connues.

Le développement de la logique échiquéenne devra rester à la charge du projet. Les bibliothèques externes pourront néanmoins servir de références indépendantes pour les tests.

# 8. Exigences non fonctionnelles

## 8.1. Performances

**Référence : NF-001 — SHOULD**

Les objectifs initiaux de performance sont les suivants :

| Opération | Objectif |
|---|---|
| Validation d'un déplacement | Moins de 10 ms |
| Génération des coups légaux | Moins de 50 ms |
| Retour visuel après une action | Moins de 100 ms |
| Sauvegarde d'une partie | Moins de 1 seconde |
| Chargement d'une partie | Moins de 1 seconde |
| Démarrage de l'application | Moins de 5 secondes |

Ces objectifs devront être mesurés sur une configuration de référence documentée.

Les mesures du moteur devront être réalisées après échauffement de la JVM, sur un ensemble représentatif de positions.

Aucune optimisation ne devra compromettre la fiabilité du moteur.

## 8.2. Fiabilité

**Référence : NF-002 — MUST**

Le moteur devra produire un résultat déterministe lorsque les mêmes conditions initiales et les mêmes coups lui sont fournis.

Aucun état incohérent connu ne devra subsister à la livraison.

Une erreur lors de l'application d'un coup ne devra pas laisser une modification partielle de la partie.

## 8.3. Maintenabilité

**Référence : NF-003 — MUST**

Un développeur découvrant le projet devra pouvoir :

- Installer les outils nécessaires.
- Compiler le projet.
- Exécuter les tests.
- Identifier les principaux composants.
- Comprendre les règles d'organisation du code.
- Ajouter ou modifier une fonctionnalité.

La documentation devra rester synchronisée avec l'implémentation.

## 8.4. Portabilité

**Référence : NF-004 — SHOULD**

Le projet devra viser une compatibilité avec :

- Windows.
- macOS.
- Linux.

La compatibilité ne pourra être annoncée que pour les plateformes effectivement testées.

Les dépendances spécifiques à un système devront être limitées et documentées.

## 8.5. Sécurité

**Référence : NF-005 — MUST**

Même dans le cadre d'une application locale, le système devra :

- Valider les entrées utilisateurs.
- Valider les fichiers importés.
- Limiter la taille des fichiers acceptés.
- Éviter la désérialisation Java native de données non fiables.
- Empêcher les accès arbitraires aux fichiers.
- Ne contenir aucun secret dans le dépôt Git.
- Vérifier les dépendances externes.
- Utiliser des permissions minimales.

Aucune collecte de données personnelles ne sera nécessaire pour la version locale.

## 8.6. Évolutivité

**Référence : NF-006 — MUST**

L'architecture devra permettre l'ajout ultérieur :

- D'une intelligence artificielle.
- D'une communication réseau.
- D'autres interfaces graphiques.
- De nouveaux mécanismes de sauvegarde.
- D'outils d'analyse.

Les fonctionnalités futures ne devront toutefois pas être implémentées par anticipation sans besoin identifié.

# 9. Gestion des tests

## 9.1. Tests unitaires

**Référence : TEST-001 — MUST**

Les tests unitaires devront couvrir :

- L'initialisation de l'échiquier.
- Les déplacements de chaque type de pièce.
- Les limites de l'échiquier.
- Les obstacles.
- Les captures.
- Les règles spéciales.
- La détection des attaques.
- Les coups légaux et illégaux.
- Les conditions de fin de partie.
- L'intégrité des états.

Chaque anomalie corrigée devra, lorsque cela est possible, faire l'objet d'un test de non-régression.

## 9.2. Tests d'intégration

**Référence : TEST-002 — MUST**

Des tests d'intégration devront vérifier les interactions entre les composants.

Ils devront notamment couvrir :

- Le déroulement d'une partie complète.
- L'enchaînement des tours.
- Les captures successives.
- Les déplacements spéciaux.
- La sauvegarde et la reprise d'une partie.
- La cohérence entre le moteur et l'interface.

## 9.3. Tests des cas limites

**Référence : TEST-003 — MUST**

Les situations suivantes devront notamment être testées :

| Référence | Scénario | Résultat attendu |
|---|---|---|
| T-001 | Nouvelle partie | 32 pièces correctement positionnées |
| T-002 | Départ depuis une case vide | Refus |
| T-003 | Déplacement hors échiquier | Refus |
| T-004 | Déplacement sans changement de case | Refus |
| T-005 | Déplacement d'une pièce adverse | Refus |
| T-006 | Tour bloquée par une pièce | Refus |
| T-007 | Cavalier franchissant un obstacle | Acceptation si le coup est légal |
| T-008 | Capture d'une pièce alliée | Refus |
| T-009 | Pion tentant de reculer | Refus |
| T-010 | Pion avançant sur une case occupée | Refus |
| T-011 | Pion avançant de deux cases avec obstacle | Refus |
| T-012 | Roi se déplaçant sur une case attaquée | Refus |
| T-013 | Déplacement exposant son propre roi | Refus |
| T-014 | Roi revenu sur sa case initiale après déplacement | Roque interdit |
| T-015 | Tour revenue sur sa case initiale après déplacement | Roque interdit avec cette tour |
| T-016 | Roque à travers une case attaquée | Refus |
| T-017 | Roque avec une tour attaquée, autres conditions réunies | Acceptation |
| T-018 | Prise en passant immédiate et légale | Acceptation |
| T-019 | Prise en passant après un coup intermédiaire | Refus |
| T-020 | Prise en passant exposant son propre roi | Refus |
| T-021 | Promotion alors que la dame est toujours présente | Acceptation |
| T-022 | Promotion en cavalier | Acceptation |
| T-023 | Déplacement ne supprimant pas un échec | Refus |
| T-024 | Situation d'échec double | Seuls les coups légaux du roi sont autorisés |
| T-025 | Tentative de capture d'un roi | Refus |
| T-026 | Situation de mat | Partie terminée |
| T-027 | Situation de pat | Partie nulle |
| T-028 | Position morte | Partie nulle |
| T-029 | Position identique en apparence, droits de roque différents | Positions distinctes pour la répétition |
| T-030 | Réclamation valide après trois répétitions | Partie nulle |
| T-031 | Cinquième répétition | Partie nulle automatique |
| T-032 | Coup de pion ou capture | Remise à zéro du compteur concerné |
| T-033 | Coup joué après la fin d'une partie | Refus |
| T-034 | Fichier de sauvegarde corrompu | Refus sans plantage |
| T-035 | Sauvegarde puis rechargement | État strictement équivalent |
| T-036 | Création de deux parties indépendantes | Aucune interférence |
| T-037 | Déplacement invalide | État initial intégralement conservé |

Cette liste constitue une base minimale et devra être enrichie pendant la conception.

## 9.4. Validation algorithmique — Perft

**Référence : TEST-004 — MUST**

Le moteur devra être soumis à des tests de type Perft (Performance Test).

Cette méthode permet de vérifier la génération des coups légaux en comptant le nombre de positions obtenues à une profondeur donnée.

Les valeurs de référence depuis la position initiale sont :

| Profondeur | Nombre attendu |
|---|---:|
| 1 | 20 |
| 2 | 400 |
| 3 | 8 902 |
| 4 | 197 281 |
| 5 | 4 865 609 |

Les résultats devront correspondre exactement aux valeurs de référence.

Des positions complexes supplémentaires devront être testées pour vérifier les règles spéciales.

Les tests Perft ne remplacent pas les tests des conditions de fin de partie et des réclamations de nullité.

## 9.5. Couverture de tests

**Référence : TEST-005 — SHOULD**

Objectifs initiaux :

- Au moins 85 % de couverture des lignes du moteur.
- Au moins 80 % de couverture des branches du moteur.
- Couverture explicite de chaque règle métier critique.
- Aucun test en échec avant livraison.

La couverture pourra être mesurée avec JaCoCo.

Un pourcentage élevé ne constitue pas, à lui seul, une preuve d'absence de bugs.

# 10. Gestion du développement

## 10.1. Gestion de versions

Le code source devra être versionné avec Git.

L'organisation devra permettre de distinguer :

- Les versions stables.
- Les développements en cours.
- Les corrections d'anomalies.
- Les nouvelles fonctionnalités.

Les commits devront être suffisamment petits, cohérents et explicites.

Chaque version livrable devra être identifiable par un tag Git.

## 10.2. Revue de code

Toute fonctionnalité importante devra faire l'objet d'une revue avant son intégration.

La revue devra notamment porter sur :

- La conformité au besoin.
- La lisibilité.
- La cohérence architecturale.
- La sécurité.
- Les performances lorsque nécessaire.
- La présence de tests.
- Les risques de régression.

Dans le cadre d'un projet individuel, cette revue pourra prendre la forme d'une auto-revue documentée.

## 10.3. Intégration continue

Le pipeline devra progressivement permettre :

1. La récupération du code.
2. L'installation de l'environnement Java.
3. La compilation.
4. L'exécution des tests.
5. La mesure de couverture.
6. L'analyse statique.
7. La vérification des dépendances.
8. La génération des artefacts.

Un échec des tests devra empêcher la validation automatique d'une version.

## 10.4. Traçabilité des décisions techniques

Les décisions architecturales importantes devront être documentées à l'aide d'ADR (Architecture Decision Records).

Chaque décision devra préciser :

- Le contexte.
- Le problème rencontré.
- Les solutions envisagées.
- La solution retenue.
- La justification.
- Les avantages.
- Les inconvénients.
- Les conséquences techniques.

Exemples de décisions à documenter :

- Choix de Maven.
- Représentation de l'échiquier.
- Modélisation des pièces.
- Répartition des responsabilités.
- Validation et application des déplacements.
- Gestion de l'historique.
- Stratégie de sauvegarde.

# 11. Documentation attendue

Les éléments suivants devront être produits :

- Cahier des charges.
- Diagramme de cas d'utilisation.
- Diagramme de classes UML.
- Diagrammes de séquence pour les opérations complexes.
- Description de l'architecture.
- Documentation des contrats publics du moteur.
- Documentation des décisions techniques.
- Documentation du format de sauvegarde.
- Plan de tests.
- Guide d'installation.
- Guide utilisateur.
- README du dépôt GitHub.
- Historique des versions.
- Liste des limitations connues.

La documentation devra être proportionnée à la taille du projet et maintenue au fur et à mesure du développement.

# 12. Planification prévisionnelle

Le projet sera découpé en jalons.

| Phase | Objectif | Charge indicative |
|---|---|---:|
| P1 | Analyse et conception | 12–20 h |
| P2 | Initialisation du projet et outils | 3–6 h |
| P3 | Représentation du jeu | 8–14 h |
| P4 | Déplacements et captures | 12–20 h |
| P5 | Validation des coups et échecs | 15–25 h |
| P6 | Règles spéciales | 12–20 h |
| P7 | Fins de partie | 15–30 h |
| P8 | Historique et sauvegardes | 12–20 h |
| P9 | Tests approfondis du moteur | 15–25 h |
| P10 | Interface graphique | 20–40 h |
| P11 | Intégration continue et packaging | 6–12 h |
| P12 | Recette et documentation finale | 10–18 h |

**Charge totale indicative : 140 à 250 heures.**

Une marge supplémentaire devra être prévue pour les difficultés techniques et les phases d'apprentissage.

Les tests devront être écrits pendant toutes les phases de développement. La phase P9 correspond à une validation approfondie supplémentaire.

La planification devra être réévaluée après chaque jalon.

# 13. Gestion des risques

| Risque | Probabilité estimée | Impact | Prévention |
|---|---|---|---|
| Mauvaise répartition des responsabilités | Moyenne | Élevé | Conception et revue architecturale |
| Erreurs dans les règles spéciales | Élevée | Critique | Tests ciblés |
| Incohérence de l'état du jeu | Moyenne | Critique | Invariants et encapsulation |
| Surconception | Moyenne | Élevé | Justification des abstractions |
| Dépendance à l'interface graphique | Moyenne | Élevé | Isolation du moteur |
| Régression lors d'une modification | Élevée | Élevé | Tests automatisés |
| Sous-estimation du temps de développement | Élevée | Moyen | Réévaluation des charges |
| Perte du code source | Faible | Élevé | Git et dépôt distant |
| Dépendances vulnérables | Moyenne | Élevé | Analyse des dépendances |
| Abandon du projet par accumulation de complexité | Moyenne | Élevé | Livraisons intermédiaires |

# 14. Critères de recette et de livraison

La version 1.0 sera considérée comme livrable lorsque :

- Toutes les exigences MUST seront satisfaites.
- Les règles métier critiques seront validées.
- Les tests automatisés seront réussis.
- Les résultats Perft seront conformes aux références retenues.
- Aucun bug critique ou bloquant connu ne subsistera.
- Deux joueurs pourront terminer une partie complète.
- Les déplacements invalides seront correctement refusés.
- Une partie pourra être sauvegardée et reprise.
- Le moteur fonctionnera indépendamment de l'interface.
- Le projet pourra être compilé à partir du dépôt Git.
- Un artefact exécutable sera disponible sur les plateformes annoncées.
- Les instructions d'installation seront vérifiées.
- Les limitations restantes seront documentées.

# 15. Definition of Done

Une fonctionnalité sera considérée comme terminée lorsque :

- Son besoin est clairement identifié.
- Son implémentation respecte l'architecture retenue.
- Les cas nominaux sont fonctionnels.
- Les cas limites sont traités.
- Les tests correspondants sont écrits.
- Les tests existants restent valides.
- Le code a été relu.
- La documentation nécessaire est mise à jour.
- Le pipeline d'intégration continue est réussi.
- Aucun défaut bloquant connu ne subsiste.

# 16. Livrables finaux

La livraison du projet comprendra :

- Le code source Java.
- Le fichier de configuration Maven.
- Les tests automatisés.
- Le moteur de jeu exploitable indépendamment.
- L'application graphique.
- Les artefacts exécutables.
- Les rapports de tests et de couverture.
- La documentation technique.
- La documentation utilisateur.
- Les diagrammes UML.
- Les décisions architecturales.
- Le pipeline CI/CD.
- Une version stable identifiée dans Git.

# 17. Conditions de réussite du projet

La réussite du projet ne sera pas uniquement évaluée sur la présence d'une interface permettant de jouer aux échecs.

Elle sera principalement évaluée sur :

- La conformité des règles métier.
- La robustesse du moteur.
- La cohérence de l'architecture.
- La qualité des tests.
- La maintenabilité du code.
- La capacité à justifier les choix techniques.
- La facilité d'intégration de fonctionnalités futures.

# 18. Références

- Règlement officiel de la FIDE : https://handbook.fide.com/chapter/E012023
- Documentation Java : https://docs.oracle.com/en/java/
- Documentation Maven : https://maven.apache.org/
- Documentation JUnit : https://junit.org/
- Documentation JavaFX : https://openjfx.io/
- Références Perft : https://www.chessprogramming.org/Perft_Results

# 19. Points restant à valider

- Version exacte de Java.
- Version des outils et dépendances.
- Technologie graphique définitive.
- Architecture logicielle.
- Représentation interne de l'échiquier.
- Format de sauvegarde.
- Contrats publics du moteur.
- Stratégie de gestion des erreurs.
- Organisation des packages.
- Stratégie Git.
- Configuration de référence pour les performances.
- Calendrier définitif du développement.

Les procédures propres aux compétitions physiques, notamment l'arbitrage, les pénalités et la règle de la pièce touchée, sont exclues du périmètre initial.

---

**Principe directeur du projet : la fiabilité du moteur et la cohérence de la logique métier priment sur la quantité de fonctionnalités disponibles.**
