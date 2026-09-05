# Pass D — note de reprise

Dernière mise à jour : 5 septembre 2026.  
Branche active : `main`. Dernier commit : `84953bb`.

## Projet

- Application principale : `index.html` (HTML, CSS et JavaScript dans un seul fichier).
- Publication GitHub Pages : `https://raphaelfrauli.github.io/veymerange/`.
- Firebase est actif : Firebase Auth + Firestore temps réel.
- Les anciennes interfaces (`parents.html`, `legacy-admin.html`) sont volontairement ignorées et ne doivent pas être modifiées pour la nouvelle app.
- Les changements applicatifs sont systématiquement commités puis poussés sur `main`.

## Connexion et rôles

- Admin : l’identifiant visible `admin` est converti en interne vers l’e-mail Firebase réel. Cet e-mail ne doit jamais être affiché dans l’interface.
- Joueur / coach : `identifiant` est converti en interne vers `identifiant@veymerange.test`.
- Le rôle réel vient exclusivement de `users/{uid}` dans Firestore.
- `admin` est un compte caché des listes joueur/coach, des convocations et des compositions. Il reste visible dans l’administration.
- Un modérateur est un joueur avec un accès d’administration limité : il ne peut pas modifier, désactiver ou promouvoir l’admin.

Navigation actuelle :

- Joueur : `Accueil | Agenda`.
- Coach : `Coach | Accueil`. L’accueil Coach contient les accès Gérer l’équipe, ajout match, ajout entraînement et Info du coach.
- Modérateur : `Admin | Accueil`, avec l’accueil joueur.
- Admin : `Admin | Coach | Accueil`, avec l’accueil de gestion admin.
- Le bouton `Mon compte` est en haut. Il n’y a plus d’onglet Profil dans la navigation basse.

## Événements et convocations

- Les événements sont dans `events/{eventId}`.
- Réponses : `events/{eventId}/responses/{uid}`.
- Sélections match : `events/{eventId}/selection/{uid}`.
- Un coach crée matchs et entraînements ; les heures se choisissent maintenant avec heures 00–23 et minutes de 5 en 5 (`00`, `05`, … `55`).
- Les boutons coach de clôture des réponses ont été retirés. Les anciens événements déjà clôturés peuvent encore être réouverts depuis leur fiche.
- Sur l’accueil joueur, les deux prochaines cartes sont triées par date **et heure**, toutes catégories confondues. Un événement passé ne doit pas apparaître dans « Prochains événements ».
- Un match publié reste visible comme prochain match. Les statuts de sélection utilisent la sous-collection Firestore `selection` et se mettent à jour en temps réel.
- Dans une fiche joueur de match publié, ne pas afficher « Ma réponse », les boutons Présent/Absent ni le motif : seulement convocation et composition.
- Pour un entraînement, la réponse reste visible après rafraîchissement grâce à la sous-collection `responses`.

## Coach

La navigation interne Coach est :

`Matchs | Entraînements | Séances | Info du coach | Joueurs`

- Les événements sont des cartes dans Matchs ou Entraînements, jamais des onglets.
- `Joueurs` affiche poste et statistiques simples (matchs, convocations, présents, absents).
- `Info du coach` écrit dans `settings/coachInfo` et s’affiche en temps réel sur l’accueil joueur.
- Le raccourci « Info du coach » depuis l’Accueil Coach ouvre directement cet onglet.

## Sondages

- Sondages : `polls/{pollId}`.
- Votes : `polls/{pollId}/votes/{uid}`.
- Coach, admin et modérateur peuvent créer ou supprimer un sondage.
- Tout membre approuvé peut choisir une option ou modifier son choix.
- L’interface affiche uniquement le nombre de réponses par option, jamais les noms des répondants.
- Les règles Firestore des votes ont été publiées dans la console Firebase. Elles autorisent lecture aux membres approuvés et écriture seulement sur son propre document de vote.

## Vérifications utiles au prochain démarrage

1. Faire un `git status --short` : les icônes, `manifest.json`, `netlify.toml` et les anciennes notes peuvent être non suivis ; ne pas les ajouter sans demande.
2. Vérifier que GitHub Pages a fini de publier le dernier commit avant un test navigateur.
3. Tester un sondage avec un compte joueur : clic sur une option, compteur mis à jour, puis rafraîchissement.
4. Tester un match publié avec un joueur sélectionné et non sélectionné.
5. Tester l’ordre des cartes avec deux événements le même jour mais à des heures différentes.

## Commandes de contrôle

```powershell
git status --short
git log -6 --oneline

$source = Get-Content -Raw index.html
$body = [regex]::Match($source, '<script type="module">([\s\S]*?)</script>').Groups[1].Value -replace '(?m)^import.*$',''
$checkFile = Join-Path $env:TEMP 'veymerange-syntax-check.js'
[IO.File]::WriteAllText($checkFile, $body)
node --check $checkFile
```

Pour pousser une modification :

```powershell
git add -- index.html
git commit -m "Description courte"
git push origin main
```
