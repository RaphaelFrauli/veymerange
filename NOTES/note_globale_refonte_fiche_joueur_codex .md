# Refonte globale de la fiche joueur — Note pour Codex

## Objectif

Refondre la fiche joueur pour obtenir un rendu beaucoup plus professionnel, moderne et cohérent avec l’identité visuelle du **CS Veymerange-Élange**.

La maquette visuelle fournie doit servir uniquement de **référence graphique**.

**Important : ne pas utiliser la bannière comme une image fixe.**  
Le rendu doit être recréé en **HTML/CSS**, avec toutes les données du joueur dynamiques et modifiables depuis le popup d’édition actuel.

---

# 1. Structure générale de la fiche

La fiche doit être composée de deux parties :

## Partie A — Bannière principale toujours visible

La bannière doit afficher :

- Numéro du joueur en grand
- Nom
- Prénom
- Surnom sous le prénom
- Poste du joueur, de manière discrète
- Photo du joueur à droite
- Logo du club en watermark léger dans le fond
- Design vert / blanc inspiré du CS Veymerange-Élange
- Fond graphique moderne avec diagonales, formes légères, dégradés et texture discrète

Ne pas afficher :

- Nationalité
- Drapeau
- Bâtiment
- Arbres
- Décor photo inutile
- Texte décoratif du type :
  - `CS VEYMERANGE - ELANGE`
  - `DEPUIS 1965`
  - `PASSION`
  - `RESPECT`
  - `ESPRIT D'ÉQUIPE`
  - `PLUS QU'UN CLUB`

Le design doit rester épuré.

---

# 2. Poste du joueur

Le poste doit apparaître dans la bannière, sous le surnom ou à proximité.

Le poste doit être **beaucoup plus discret** que sur la maquette précédente.

Ne pas utiliser :

- gros bouton vert
- grosse pastille
- icône chaussure

Afficher quelque chose de sobre, par exemple :

- `DC`
- `MC`
- `MDC`
- `MOC`
- `AD`
- `AG`
- `BU`
- `GB`

Ou éventuellement :

`Défenseur central · DC`

Le poste doit être lisible mais secondaire par rapport au numéro, nom et prénom.

---

# 3. Photo du joueur

La photo doit être indépendante du fond de la bannière.

Prévoir :

- photo alignée à droite
- cadrage poitrine
- intégration propre dans la bannière
- léger fondu en bas si nécessaire
- pas de carré blanc ou gris autour de la photo

Idéalement, utiliser :

**PNG avec fond transparent**

Si la photo uploadée possède déjà un fond transparent, le joueur doit s’intégrer naturellement au fond graphique.

À terme, prévoir la possibilité d’ajouter un détourage automatique, mais pour l’instant conserver le système d’upload / URL photo existant.

La photo ne doit jamais être fusionnée dans une image fixe de bannière.

---

# 4. Bannière de référence

La bannière générée fournie avec cette note sert uniquement de **référence visuelle**.

Codex doit reproduire :

- la composition générale
- les couleurs
- la hiérarchie visuelle
- le numéro à gauche
- l’identité joueur à gauche
- le joueur détouré à droite
- le logo du club en watermark
- le style vert / blanc moderne

Mais le tout doit être recréé en HTML/CSS avec des éléments dynamiques.

---

# 5. Informations détaillées sous la bannière

La partie située sous la bannière doit être **masquée par défaut**.

Seule la bannière est visible au chargement.

Ajouter un bouton discret du type :

`Voir la fiche`

avec un petit chevron.

Au clic, afficher avec une animation fluide :

## Informations joueur

Dans cet ordre :

`Date de naissance | Taille / Poids | Pied fort`

Disposition propre et horizontale sur desktop.

Sur mobile, passer en disposition verticale si nécessaire.

---

# 6. Stats

Sous les informations joueur, afficher une section :

`STATS`

Avec uniquement :

- Matchs
- Buts
- Passes décisives

Supprimer :

- Minutes
- gros carrés gris
- gros blocs lourds

Le rendu doit être léger :

- intitulé petit
- chiffre plus visible
- séparateurs fins
- beaucoup d’espace
- design minimaliste et professionnel

Exemple :

`MATCHS     BUTS     PASSES DÉCISIVES`

avec les valeurs juste en dessous.

Au second clic sur le bouton, la partie détaillée se replie.

Le bouton peut devenir :

`Masquer la fiche`

---

# 7. Popup “Modifier joueur”

Le popup actuel doit devenir la source de toutes les données affichées dans la fiche.

Tous les champs doivent être modifiables.

Champs à conserver / ajouter :

- Prénom
- Nom
- Poste
- Numéro
- Surnom
- Poids
- Taille
- Date de naissance
- Pied fort
- Matchs
- Buts
- Passes décisives
- Photo / URL photo

---

# 8. Taille et date de naissance

Le bloc actuel en lecture seule doit être supprimé.

Supprimer complètement :

- `Date de naissance Non renseignée`
- `Taille Non renseignée`
- `Ces deux informations restent en lecture seule`

À la place, ajouter deux vrais champs éditables :

## Date de naissance

Utiliser :

`input type="date"`

## Taille

Utiliser :

`input type="number"`

avec unité en cm.

Exemple :

`Taille (cm)`

Ces deux valeurs doivent être sauvegardées avec les autres données du joueur.

---

# 9. Synchronisation des données

Toute modification réalisée dans le popup doit mettre à jour automatiquement la fiche correspondante.

Exemples :

- Numéro modifié → numéro de bannière mis à jour
- Nom modifié → nom de bannière mis à jour
- Prénom modifié → prénom de bannière mis à jour
- Surnom modifié → surnom mis à jour
- Poste modifié → poste mis à jour
- Photo modifiée → nouvelle photo affichée
- Date de naissance modifiée → information mise à jour
- Taille modifiée → information mise à jour
- Poids modifié → information mise à jour
- Pied fort modifié → information mise à jour
- Matchs modifiés → stats mises à jour
- Buts modifiés → stats mises à jour
- Passes décisives modifiées → stats mises à jour

Éviter autant que possible d’avoir besoin de recharger manuellement la page.

---

# 10. Gestion des valeurs absentes

Si une donnée n’est pas renseignée, afficher une valeur propre du type :

`—`

ou :

`Non renseigné`

Éviter les textes techniques ou visuellement lourds.

La fiche doit rester propre même quand certaines informations sont absentes.

---

# 11. Responsive

La fiche doit être responsive.

## Desktop

- bannière large
- numéro / identité à gauche
- photo à droite
- infos détaillées sur une ligne
- stats sur une ligne

## Mobile

- bannière adaptée
- texte lisible
- photo correctement recadrée
- aucune information coupée
- informations détaillées empilées proprement si nécessaire
- bouton Voir la fiche toujours accessible

---

# 12. Architecture HTML / CSS souhaitée

Créer une structure claire et maintenable, par exemple :

- `player-card`
- `player-banner`
- `player-number`
- `player-identity`
- `player-name`
- `player-nickname`
- `player-position`
- `player-photo`
- `player-details-toggle`
- `player-details`
- `player-info-row`
- `player-info-item`
- `player-stats`
- `player-stat-item`

Le but est d’éviter une structure monolithique difficile à modifier.

---

# 13. Contraintes techniques importantes

- Ne pas casser Firebase
- Ne pas refaire toute l’application inutilement
- Réutiliser les données existantes
- Réutiliser les fonctions actuelles lorsque c’est possible
- Ne pas modifier les autres fonctionnalités non concernées
- Ne pas casser la fenêtre Modifier joueur
- Ne pas casser l’upload photo existant
- Vérifier que la sauvegarde fonctionne toujours
- Vérifier que les données se mettent à jour après modification
- Garder la cohérence avec le thème actuel du site

---

# 14. Résultat attendu

Au chargement de la page :

- afficher uniquement une belle bannière compacte par joueur
- numéro, nom, prénom, surnom, poste et photo visibles directement
- design inspiré du CS Veymerange-Élange

Quand on clique sur `Voir la fiche` :

- afficher Date de naissance
- afficher Taille / Poids
- afficher Pied fort
- afficher Matchs
- afficher Buts
- afficher Passes décisives

Toutes les informations doivent provenir des données du joueur et rester modifiables via le popup.

---

# 15. Consigne essentielle avant de coder

**Avant de coder, inspecte l’architecture actuelle et réutilise au maximum les composants, fonctions Firebase, styles et champs existants. Ne remplace pas toute la logique si ce n’est pas nécessaire.**

Commencer par identifier :

- où sont stockées les données joueur
- comment la fiche actuelle est générée
- comment le popup Modifier joueur sauvegarde les données
- comment la photo est stockée / chargée
- quels champs existent déjà dans Firebase
- quels champs doivent être ajoutés

Ensuite seulement, appliquer la refonte.
