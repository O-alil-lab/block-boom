# BLOCK BOOM — v2

Puzzle de blocs hybrid-casual (style Block Blast), un seul fichier `index.html`, zéro dépendance
(seule la police Fredoka vient de Google Fonts, avec repli système).

## Lancer
```bash
python3 -m http.server 8000   # puis http://localhost:8000
```

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

## Pubs
Toujours des démos : remplacer `showAd(kind, onDone)` / `closeAd()` par AppLovin MAX ou AdMob.
