# BLOCK BOOM — édition Lanternbound

Puzzle de blocs hybrid-casual (style Block Blast) avec des compagnons à apprivoiser. Un seul fichier `index.html`,
zéro dépendance (police Fredoka via Google Fonts avec repli système, SDK CrazyGames v3).

## Lancer
```bash
python3 -m http.server 8000   # puis http://localhost:8000
```
En local (ou avec `?debug` dans l'adresse) : boîte d'erreur visible et hook de test `window.__bb`.
En production ces outils sont désactivés.

## Gameplay
- Grille **8×8**, **glisser-déposer** (la pièce flotte au-dessus du doigt pour rester visible)
- Aperçu : fantôme de la pièce + les lignes qui vont exploser s'illuminent à l'avance
- Pièces grisées quand elles ne rentrent plus nulle part
- **Combo** : refais une ligne dans les 3 coups suivants (pastilles du badge COMBO)
- **FEVER** au combo ×5 : points ×2, fond arc-en-ciel, la musique passe en mode « drop »
- 💎 **Gemmes** (pièces bonus) et 💣 **Bombes** (explosion 3×3, réactions en chaîne)
- **Grille parfaite** : +2 500 points + feu d'artifice
- Génération de pièces « juste » : au moins une pièce posable, pièce de secours quand la grille est pleine
- Modes **Aventure** (objectif de lignes, blocs de pierre et gemmes pré-placés) et **Classique** (score infini + records)

## Compagnons (Lanternbound)
- 18 créatures, 6 éléments (Sylve, Marée, Braise, Rafale, Roche, Lueur) ; chaque couleur de bloc = un élément
- Équipe de 3 : leur lanterne se charge quand tu fais exploser des blocs de leur élément ; touche-les pour lancer leur pouvoir
- Pouvoirs : Floraison, Raz-de-marée, Brasier, Vent arrière, Séisme, Prisme
- Chaque niveau Aventure réussi apprivoise une créature sauvage ; **Lanterne de cristal** (300 pièces) = créature au hasard
- Les doublons donnent de l'expérience (niveau max 6 : la lanterne se charge plus vite)

## Rétention (v3)
- **Rangs** Bois → Bronze → Argent → Or → Platine → Diamant → Maître → Légende, barre d'XP animée après chaque partie
- **Coffre mystère** toutes les 3 parties — chances affichées = chances réelles : Commun 60 % · Rare 26 % · Épique 10 % · Légendaire (créature) 4 %
- **Série quotidienne** sur 7 jours (20 → 300 pièces), remise à zéro si un jour est manqué
- **Défi du jour** : graine fixe basée sur la date **UTC** (mêmes pièces pour tous, partout dans le monde), pas d'annulation ni de relance, bouton « Défier mes amis »
- **Presque !** : la case qui manque pour finir une ligne clignote en doré
- **Danger** : grille pleine à 66 % → battements de cœur + bord rouge
- **Objectif visible** : barre vers le record pendant la partie, « Plus que X pts » à la fin
- Premières parties assistées pour vivre de grosses explosions tout de suite
- Aucune manipulation cachée : pas de main truquée, difficulté identique pour tous

## Effets & son (100 % générés, aucun fichier audio)
- Particules (éclats, étincelles, ondes de choc, rayons laser sur les lignes), tremblement d'écran, flash
- Textes « Super ! / Génial ! / Incroyable ! / LÉGENDAIRE ! », score qui défile, pièces qui volent jusqu'au compteur
- Vibrations (Android)
- **Musique générative** WebAudio (la mineur, vi–IV–I–V, 104 BPM) avec 4 niveaux d'intensité
  qui suivent ton jeu : calme au menu → rythme en partie → arpèges en combo → batterie complète en FEVER
- Effets sonores **accordés sur la musique** : plus ton combo monte, plus les notes montent
- Réverbération + écho, compresseur master

## Corrections par rapport à la v1
- Poser une pièce au doigt ne marchait pas (position calculée seulement au survol) → glisser-déposer
- Domino et P5 n'apparaissaient jamais (poids total 113, tirage sur 103)
- Défis du jour validés automatiquement le lendemain (stats cumulées) → progression du jour seulement
- Pub récompensée infinie dans la boutique → 5 par jour ; relance après game over → 1 par partie
- Pub interstitielle à chaque niveau dès le niveau 1 → jamais avant le niveau 5, puis tous les 3 niveaux
- Faux classement remplacé par tes vrais records
- Fautes « DÉBLOCÉ », « effacéées »

## CrazyGames & pubs
- Le SDK v3 est chargé dans `<head>` ; il n'est activé que si `SDK.environment` vaut `crazygames` (ou `local`).
  Ailleurs (GitHub Pages) le jeu reste en mode démo.
- `ADS_ENABLED = false` pendant le **Basic Launch** (pubs interdites sur CrazyGames). Passer à `true` au Full Launch.
- Hors CrazyGames, les pubs sont des démos (`showAd` / `closeAd`).
- Garde-fou : si une pub ne démarre pas en 8 s (ou ne se termine jamais), le jeu se débloque tout seul.

## Corrections (audit Claude Code Game Studios, oct. 2026)
- SDK CrazyGames jamais chargé → fausses pubs démo, pas de gameplayStart/Stop ni de sauvegarde cloud sur CrazyGames
- Chances du coffre affichées ≠ réelles (Épique 8 % au lieu de 10 %)
- Une fin de niveau / de partie différée pouvait terminer la partie suivante (Pause → Menu pendant l'animation)
- « Continuer » comptait la partie deux fois (2 records, XP et coffre doublés)
- Compteur de pièces faux si on relançait pendant que les pièces volaient encore
- Annuler ne rendait pas les pièces / la progression des défis gagnées par le coup (petite triche possible)
- Sauvegarde abîmée → plantage à chaque lancement ; maintenant réparée au chargement
- Hook de test `window.__bb` et boîte d'erreur retirés de la version publique
