# État du projet — Livre Bac S

Ce fichier donne une photo de l'état actuel : ce qui est fait, ce qui
est en cours, et surtout ce qui bloque ou attend une information/décision
de l'utilisateur. Contrairement à `PROGRESS.md` (historique), ce fichier
est mis à jour *en place* — on modifie les sections existantes plutôt que
d'empiler des entrées datées.

---

## Résumé rapide

Livre de Terminale S en LaTeX (classe `book`, a5paper) couvrant Algèbre,
Analyse, Géométrie, Probabilités, les sujets officiels du Bacc Série S
(2021–2026) et un chapitre Entrainement (19 sujets types + sujets bac
étrangers). Compile sans erreur avec `latexmk -pdf`, et une passe de
relecture globale (2026-08-26) a réduit les débordements de marge
(`Overfull \hbox`) visibles de 27 à 13 occurrences uniques. Le livre fait
**380 pages** et est organisé en **5 parties** (Algèbre, Analyse,
Géométrie, Probabilités, Sujets et entraînement).

⚠️ Correction du 2026-08-27 : la note précédente affirmait que tous les
`Overfull` restants étaient « inférieurs à ~11pt et invisibles ». C'est
faux — il en reste **trois significatifs**, à traiter un jour :
`parties/algebre/arithmetique.tex` l. 1031–1035 (39,3pt),
`parties/probabilites/conditionnelles.tex` l. 364–367 (31,5pt),
`parties/probabilites/variables_aleatoires.tex` l. 185 (26,4pt).
Les dix autres sont bien < 13pt.

## Mise en page — conventions

Depuis le 2026-08-30, l'en-tête de chapitre est compact : les
espacements figés du style « Glenn » de `fncychap` sont redéfinis dans
`config/style.tex` via trois réglages (`\ChapAvant`, `\ChapApres`,
`\ChapNumSize`). Le dessin est inchangé, mais l'ouverture de chapitre
occupe ~3 cm au lieu de ~7 cm (398 → 393 pages). Dans la foulée,
l'interligne est revenu à la valeur normale (`\linespread{1.0}`) et
`\parskip` à 0.3em : 393 → 381 pages. Ces deux valeurs ont été
mesurées sur six compilations complètes ; plus bas (0.25em / 0.98)
le texte se tasse visiblement contre les encadrés.

Depuis le 2026-08-30, trois réglages globaux (dans
`config/environnements.tex`) tiennent la densité du livre : listes
resserrées, air réduit autour des formules centrées, et `\medskip` avant
les titres d'exercices. Pour toute nouvelle batterie de questions courtes,
utiliser `\begin{listecol}(2)` (ou `multicols`), et pour un QCM
`\begin{qcm}(2)` — 4 colonnes si les propositions tiennent en un ou deux
symboles. Ne pas utiliser `\dfrac` dans une proposition de QCM : la
hauteur de ligne double.

## Rubriques d'illustration (maquette du 2026-08-31)

Trois rubriques, définies dans `config/environnements.tex`, testées pour
l'instant sur le **seul chapitre Probabilités conditionnelles** :

| Rubrique | Usage | Quantité |
|---|---|---|
| `citationchapitre` (existante) | 2 lignes sous le titre du chapitre | 1 |
| `vraievie{Titre}` | un fait réel mis en équation avec la notion | **1 par chapitre**, ½ à 1 page |
| `reperehisto{Nom}` / `clindoeil` | notes de 3–5 lignes, filet à gauche, sans cadre | 2 au maximum |

Budget mesuré : **+1 page par chapitre**, toutes rubriques confondues
(chapitre conditionnelles 14 → 15 pages ; livre 381 → 382).

Règles :
- les maths d'un encadré `vraievie` doivent être **honnêtes** — tout
  modèle simplifié, tout arrondi est annoncé via `\reserve{}` en fin
  d'encadré ;
- pas de citation apocryphe (« d'après X » si la formulation est
  reconstituée) ;
- l'humour passe par l'**erreur classique** commentée, pas par la blague :
  ça vieillit mieux et ça sert à quelque chose ;
- ne pas dépasser deux notes courtes par chapitre, sinon l'élève en
  révision ne sait plus ce qu'il doit lire.

**Décision en attente de l'utilisateur** : généraliser ou non aux
19 autres chapitres (coût estimé : ~+20 pages, soit exactement ce qui a
été gagné le 2026-08-30 en compactant la mise en page).

## Arbres pondérés compacts (style `arbrepondere`)

Depuis le 2026-08-31, tout nouvel arbre pondéré à 2 niveaux doit utiliser
le style TikZ `arbrepondere` (défini dans `config/environnements.tex`) et
la syntaxe `child { ... }` imbriquée, **jamais** le positionnement manuel
`\path (Noeud) ++(x,y) node {...}` (ancienne méthode, ~7 cm de haut par
arbre — voir `parties/probabilites/conditionnelles.tex` avant le
2026-08-31 dans l'historique git pour l'ancien style à ne pas reproduire).

```latex
\begin{tikzpicture}[arbrepondere]
	\node {}
	child { node {B}
		child { node {A}     edge from parent node[above, pos=0.75] {p} }
		child { node {non A} edge from parent node[below, pos=0.75] {p} }
		edge from parent node[above, pos=0.65] {p}
	}
	child { ... };
\end{tikzpicture}
```

**Toujours préciser `pos=0.65` (niveau 1) / `pos=0.75` (niveau 2) sur
chaque étiquette `edge from parent`.** Au `pos` par défaut (0.5, le
milieu du segment), les deux étiquettes d'un même nœud (branche du
dessus et branche du dessous) tombent trop près l'une de l'autre et se
chevauchent silencieusement — aucun `Overfull`/`Underfull`, juste des
chiffres illisibles superposés une fois le PDF ouvert. Toujours vérifier
un nouvel arbre par un rendu PNG zoomé (`pdftoppm -r 300`), pas seulement
par l'absence de warning de compilation.

Ne pas essayer de resserrer davantage `level distance` / `sibling
distance` pour un arbre à libellés courts (fractions, décimales à 2
chiffres) en espérant une variante « compacte » : testé et abandonné le
2026-08-31, le même bug de chevauchement revient dès que le niveau 2 est
resserré sans réajuster `pos`. Un seul style, correctement positionné,
suffit pour tous les libellés (courts ou longs comme
`\Prob_{\overline B}(\overline A)`).

### Arbre + énoncé côte à côte (`minipage`)

Pour un exercice où un arbre pondéré est suivi de questions courtes,
mettre l'arbre et le texte côte à côte dans deux `minipage[t]` plutôt
que de les empiler économise encore de la hauteur. Patron à réutiliser :

```latex
\noindent
\begin{minipage}[t]{0.43\linewidth}
	\centering
	\begin{tikzpicture}[arbrepondere, baseline=(current bounding box.north)]
		...
	\end{tikzpicture}
\end{minipage}%
\hfill
\begin{minipage}[t]{0.54\linewidth}
	texte / \begin{enumerate} ... \end{enumerate}
\end{minipage}
```

Deux pièges :

- **Sans `baseline=(current bounding box.north)`, l'alignement `[t]` est
  cassé.** Un `tikzpicture` nu place sa « ligne de base » au BAS de son
  dessin (hauteur = tout le contenu, profondeur = 0) ; `minipage[t]`
  aligne alors le haut du texte voisin sur le BAS de l'arbre, pas sur
  son sommet — la colonne de texte se retrouve entièrement sous l'arbre
  au lieu d'à côté, sans aucun message d'erreur. Ne jamais mettre un
  arbre `arbrepondere` dans une `minipage[t]` sans cette option.
  Utiliser aussi `\centering` plutôt que
  `\begin{center}...\end{center}` autour du `tikzpicture` : `center`
  ajoute de l'espace vertical avant le contenu qui fausse à nouveau
  l'alignement.
- **Une colonne de texte trop étroite fait déborder les lignes sur
  2–3 lignes**, ce qui peut rendre le texte plus haut que l'arbre et
  annuler le gain — voire faire sauter tout le bloc (les deux
  `minipage` forment un seul bloc insécable) à la page suivante en
  laissant un grand blanc. Prévoir environ 0,43 pour l'arbre (il a
  besoin d'environ 5 cm de large pour ne pas déborder de son cadre) et
  0,54 pour le texte, plutôt qu'un partage 60/40 trop serré côté texte.

## Encadrés `methode` et blocs insécables

`methode` est bien `breakable` et se coupe normalement — **sauf si son
contenu est un bloc insécable** (`tabular`, `tikzpicture`, `includegraphics`).
Dans ce cas la boîte saute entière à la page suivante et peut laisser
jusqu'à un tiers de page de blanc (c'était le cas p. 119 avant le
2026-08-30). Pour un tableau « Situation → Réflexe » dans un encadré,
utiliser `tabmethode` (sécable) et non `tabular` :

```latex
\begin{tabmethode}[0.45]{Situation}{Réflexe}
    \ligne{situation}{réflexe}
\end{tabmethode}
```

L'argument optionnel est la largeur de la colonne de gauche (fraction de la
largeur disponible, 0.40 par défaut).

Audit du 2026-08-30 : `attention` (25 blocs), `astucebac` (34) et `resume`
(3) sont sains — aucun ne provoque de trou notable, même les quelques-uns
qui contiennent une figure ou une petite table, car la boîte peut se couper
autour. **La règle vaut surtout pour les figures hors encadré** : une
`tikzpicture` posée en plein texte dans un `center` est insécable et peut
laisser plus de 100 pt de blanc en bas de page. Pour une figure haute,
préférer un flottant `\begin{figure}[htbp]`, qui laisse le texte combler
le bas de page.

## Barèmes de points

Depuis le 2026-08-30 : **pas de barème dans les sujets types** (chapitres et
`entrainement.tex`). Le barème est réservé aux **annales officielles**
(`parties/annales/`), où il fait partie du document reproduit, avec le
« N points » en tête d'exercice. Ne pas en réintroduire dans un nouveau
sujet type.

## Chapitres — état

| Partie | État |
|---|---|
| Algèbre (arithmétique, matrices, complexes) | Terminé. Complexes enrichi le 2026-08-30 de trois résumés de cours illustrés (forme exponentielle, Moivre, linéarisation), via le nouvel environnement `resume`, **harmonisés avec les exercices** (2 exercices résolus, 3 items Vrai/Faux, 2 exercices progressifs, 1 sujet type Bac dédié, renvois `\pageref` croisés). Chapitres Complexes, Arithmétique et Calcul matriciel alignés sur le modèle type le 2026-08-27 (matriciel : les 6 sujets types matrices ont quitté `entrainement.tex` pour le chapitre). |
| Analyse (limites → équa diff) | **Terminé et aligné sur le modèle type (2026-08-27).** Fusion « Limites » + Continuité → `limites_continuite.tex` ; ancien ch.5 → « Dérivabilité » ; `fonctions.tex` → « Étude d'une fonction » ; `logarithme.tex` / `exponentielle.tex` resserrés en chapitres-référence ; `integrales.tex` aligné (+ correctif macro `\dd`) ; `suites.tex` aligné (n'était que la récurrence) ; `equadiff.tex` aligné (citation, méthode « vérifier une solution », méthode « second membre », échauffement figure + Vrai/Faux, 6 sujets types). `limites.tex` et `continuite.tex` supprimés. |
| Géométrie (barycentre → espace) | Terminé. Chapitres Isométries, Barycentre et Géométrie dans l'espace (créé de zéro) alignés sur le modèle type le 2026-08-27. **Isométries enrichi le 2026-08-30** : exercice résolu illustré sur la méthode de l'axe commun + deux nouvelles sous-sections d'exercices (« Batterie : composées d'isométries » et « Décomposer une rotation et une translation sur une figure », 12 exercices dont 7 avec figure TikZ), sujets types Bac regroupés sous leur propre sous-titre. |
| Probabilités (5 sous-chapitres) | **Terminé et aligné sur le modèle type (2026-08-27).** `probabilites`, `conditionnelles`, `variables_aleatoires`, `binomiale`, `normale` : citation, objectifs étoffés, dénombrement / Bayes / absence de mémoire / seuils ajoutés, section « Méthodes et exercices résolus », échauffement (lecture de figure + Vrai/Faux 7 items), batteries `multicols`, **5 sujets types Bac** par chapitre au format officiel (Partie A/B, points par question). |
| Sujets officiels Bacc Série S | 2021, 2022, 2023, 2024, 2025, 2026 transcrits. À compléter au fil des sessions envoyées par l'utilisateur (années manquantes : 2027+ à venir, années < 2021 non demandées pour l'instant). |
| Entrainement (sujets types) | 19 sujets types présents. |

## En attente / prochaine étape

- Aucun blocage actif en ce moment.

- **Structure en parties : FAIT** (branche `structure-parties`). Les cinq
  `\part{}` de `main.tex` sont actifs — Algèbre, Analyse, Géométrie,
  Probabilités, et une nouvelle partie « Sujets et entraînement » devant
  `sujet_types` / `entrainement`. Ordre des parties conservé (voir PROGRESS
  pour le raisonnement sur les dépendances).

- **Incohérences de progression repérées le 2026-08-27, PAS encore
  corrigées** (chantier « PR 2 » proposé à l'utilisateur) :
  1. **Circularité ln / primitives.** `integrales.tex` donne `1/x → ln|x|`
     et `e^x → e^x` dans le tableau des primitives usuelles
     (`integrales.tex:70` et `:72`), alors que `ln` est *défini* comme
     « la primitive de 1/x nulle en 1 » deux chapitres plus loin
     (`logarithme.tex:40`). Correctif retenu : garder dans Intégrales les
     primitives algébriques/trigo seules, et déplacer les lignes `ln|u|`,
     `u'/u`, `e^u`, `u'e^u` **dans les chapitres ln et exp eux-mêmes** —
     c'est d'ailleurs là que le programme officiel les range.
  2. **Section « Limites de référence : ln et exp »** (`limites_continuite.tex:82`)
     placée trois chapitres avant la définition de ln/exp. À encadrer en
     « Admis — démontré au ch. Logarithme / Exponentielle », sur le modèle
     déjà appliqué dans `derivation.tex:46`.
  3. **Récurrence utilisée avant d'être enseignée** : `derivation.tex:324`,
     `integrales.tex:664`, `binomiale.tex:333` s'en servent, mais elle
     n'est introduite qu'au ch. Suites (`suites.tex:39`). Piste : en faire
     un court chapitre-outil en tête de livre.

- **Déplacement des Complexes (optionnel, « PR 3 »)** : les placer dans
  l'Analyse entre Suites et Équations différentielles, comme le programme
  officiel qui les classe en ANALYSE. Réglerait le `e^{iθ}`
  (`complexes.tex:315`) employé avant l'exponentielle. Vérifié sans risque :
  seuls `equadiff.tex` et `isometries.tex` dépendent des complexes, tous
  deux resteraient après. Décision non tranchée par l'utilisateur.

- **`annexes/formulaire.tex` est vide (0 octet)** et n'est inclus nulle
  part ; le `\appendix` de `main.tex` est donc sans contenu. À écrire, ou à
  supprimer si le formulaire n'est plus voulu.

- **Frontmatter inutilisés** : `page_garde.tex`, `avant_propos.tex`,
  `table_matieres.tex` existent mais ne sont `\input` nulle part
  (`main.tex` charge `couverture`, `copyright`, `preface`, `mode_emploi`).
- **Chantier « aligner tous les chapitres sur le modèle type » : TERMINÉ.**
  Tous les chapitres du livre (algèbre, analyse, géométrie, probabilités)
  suivent le modèle type (voir `feedback_chapter_template`).
  - Faits, avec 5+ sujets types Bacc chacun : Isométries, Barycentre,
    Complexes, Géométrie dans l'espace, Arithmétique, Calcul matriciel,
    Limites et continuité, Dérivabilité, Étude d'une fonction,
    Primitives et intégrale, Suites numériques, Équations différentielles,
    **Probabilités, Probabilités conditionnelles, Variables aléatoires,
    Loi binomiale, Lois continues et loi normale** (les 5 chapitres proba
    alignés le 2026-08-27, branche `chapitres-probabilites-alignement`).
  - Traités en mode resserré (chapitres-référence) : Logarithme,
    Exponentielle.
    `equadiff.tex` aligné le 2026-08-27 (PR #24).
    `suites.tex` aligné le 2026-08-27 (PR #23) : récurrence, sens de
    variation (4 méthodes), majorées/minorées/bornées, convergence /
    divergence + théorèmes (limite monotone, comparaison, gendarmes),
    u_{n+1}=f(u_n) + point fixe, arith.-géo. + adjacentes ; nombreuses
    batteries dont convergence/divergence ; 5 sujets types.
    NB : `logarithme.tex` / `exponentielle.tex` volontairement resserrés
    en chapitres-référence (PR #21) — pas de 5 sujets types (couverts par
    « Limites et continuité », « Dérivabilité », « Étude d'une fonction »).
    `integrales.tex` aligné le 2026-08-27 (PR #22) : primitives (ln|x|,
    e^x, u'/u, u'e^u ajoutés), fonction définie par une intégrale, IPP,
    changement de variable affine, aire/moyenne/volume/moments d'inertie,
    5 batteries 2-3 colonnes + 5 sujets types.
- Si l'utilisateur envoie un nouveau sujet officiel (PDF ou photos), il
  s'ajoute dans `parties/annales/bac_20XX.tex` + une ligne `\input` dans
  `sujet_types.tex`, à la bonne place chronologique.

## Points de vigilance (pour éviter de refaire les mêmes erreurs)

- **Macro `\dd`** : corrigée le 2026-08-27 en `\,\mathrm{d}` (espace fine)
  au lieu de `,\mathrm{d}` (virgule visible). Impacte tout le livre —
  toutes les intégrales étaient rendues « $f(x)$ , $\mathrm{d}x$ ». Ne pas
  remettre la virgule. Éviter `\frac{\dd x}{\ldots}` : préférer
  `\frac{\mathrm{d}x}{\ldots}` ou `\frac1x\dd x`.

- **Transcription depuis PDF/photo** : toujours passer par une lecture
  visuelle nette (rendre les pages PDF en image à haute résolution avec
  PyMuPDF si le PDF est protégé/mal océrisé, ou demander une photo plus
  nette/non recadrée si le texte envoyé est flou). Ne jamais deviner un
  passage de contenu mathématique illisible — poser la question, sauf
  si un recoupement fiable existe (ex. vérifier une équation floue par
  le calcul, ou reconstituer une valeur de points manquante à partir du
  total annoncé qui doit toujours boucler exactement).
- **Ne pas confondre sujet officiel et sujet "blanc"** : un "Baccalauréat
  Blanc" (examen d'entraînement local/régional) n'est pas un sujet
  officiel MESUPRES — à ne pas mélanger dans `parties/annales/` sauf
  demande explicite d'un emplacement séparé.
- **Nesting LaTeX + a5paper** : les formules longues (grands ensembles,
  inégalités/égalités à plusieurs membres, plusieurs matrices sur une
  même ligne) débordent facilement de la marge sur ce format de page,
  surtout dans un `enumerate` imbriqué. Réflexes qui marchent :
  - passer en affichage centré (`$$...$$` / `\[...\]`) plutôt que de
    laisser une longue formule inline en fin de phrase ;
  - couper une formule multi-lignes en `\begin{aligned}...\end{aligned}`
    avec des `\\` explicites — un `\[...\]` sur plusieurs lignes sources
    SANS `\\` est traité comme une seule ligne et déborde silencieusement ;
  - pour un tableau (`tabular`), remplacer les colonnes `c`/`l` par des
    colonnes `>{\centering\arraybackslash}p{largeur}` (package `array`,
    déjà chargé dans `config/packages.tex`) dès que le contenu d'une
    cellule est long ;
  - pour un tableau `tkz-tab` trop large, réduire le paramètre `lgt`
    de `\tkzTabInit`.
  - ce qui NE marche PAS de façon fiable : forcer un saut de paragraphe
    (ligne blanche) juste pour raccourcir une phrase — TeX peut quand
    même produire un `Overfull` sur la ligne isolée résultante. Toujours
    vérifier via `latexmk` + regarder le contenu exact du warning
    (`grep -A5` sur le log) plutôt que supposer que le correctif a marché.
  - Toujours vérifier après coup qu'aucun `Overfull \hbox` significatif
    (> ~15pt) ne subsiste dans les fichiers touchés, et confirmer
    visuellement (rendu PNG de la page) que le correctif ne casse rien.
- **Ne pas ajouter du LaTeX avec un heredoc shell** (`cat >> f << 'EOF'`) :
  dans cet environnement, les `\\` (fin de ligne dans `pmatrix`, `cases`,
  `aligned`, systèmes…) sont réduits à un seul `\`, ce qui colle tout sur
  une ligne. Utiliser l'outil Write/Edit, ou un script Python qui écrit le
  fichier (chaîne `r'''...'''`). Vérifier ensuite : aucun `\` suivi d'un
  chiffre ou d'un `&` hors `\\`.
- **Workflow git** : toujours une branche de fonctionnalité + PR contre
  `main`, jamais de commit direct sur `main` (voir mémoire du projet).

---

*Pour mettre à jour : modifier les sections ci-dessus pour refléter la
réalité actuelle. Si un blocage apparaît (info manquante, ambiguïté à
trancher, décision à prendre avant de continuer), l'ajouter sous "En
attente / prochaine étape" avec assez de contexte pour reprendre sans
tout relire ; le retirer une fois résolu (et, si utile, en garder une
trace courte sous "Points de vigilance").*
