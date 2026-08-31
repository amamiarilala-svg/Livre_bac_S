# Journal de progression — Livre Bac S

Ce fichier retrace l'avancement du livre, du plus récent au plus ancien.
Une entrée = une session de travail ou un lot de changements cohérent.
Nouvelle entrée en haut, format : `## AAAA-MM-JJ — Titre court`.

---

## 2026-08-31 — Arbres pondérés compactés (Probabilités conditionnelles)

Les 5 arbres pondérés du chapitre (arbre générique, tirages avec/sans
remise, exercice résolu M1/M2, échauffement) occupaient jusqu'à
**7,2 cm de haut** chacun : positionnement manuel (`\path ... ++(x,y)`)
avec des espacements choisis très larges (`sibling distance` 3,4 à
4,2 cm, second niveau décalé de ±1,1 à ±1,5 cm).

Remplacés par un style `tikz` commun (`arbrepondere`, dans
`config/environnements.tex`) utilisant la syntaxe `child { ... }`
imbriquée native de TikZ, qui laisse le moteur calculer l'encombrement
réel de l'arbre : hauteur ramenée à **~4,2 cm** (perte ~42 %), largeur
inchangée.

Piège rencontré et documenté dans `environnements.tex` : au `pos`
par défaut (0.5, le milieu du segment), les deux étiquettes d'un même
nœud (branche du dessus et branche du dessous) tombent trop près l'une
de l'autre et se **chevauchent silencieusement** — aucune erreur de
compilation, juste des chiffres illisibles superposés. Repéré d'abord
sur l'arbre M1/M2 (labels `0,92`/`0,08` fusionnés), confirmé ensuite
même sur l'arbre générique aux libellés `\Prob_B(A)`. Corrigé en
poussant les étiquettes vers l'extrémité de la branche où elle diverge
(`pos=0.65` niveau 1, `pos=0.75` niveau 2) plutôt qu'en élargissant
l'arbre. Une tentative intermédiaire avec deux styles (un large, un
« compact ») a été abandonnée : le style compact réapparaissait avec le
même bug de chevauchement dès que le niveau 2 était resserré sans
corriger le `pos` — un seul style unifié, correctement positionné, est
plus sûr que deux tailles à surveiller séparément.

Un `\enlargethispage{1.5cm}` a été ajouté avant l'arbre de l'exercice
résolu M1/M2 : même compact, l'arbre ne tenait pas dans l'espace restant
en bas de page et sautait entier à la page suivante en laissant un grand
blanc (piège déjà documenté plus bas — bloc `tikzpicture` insécable dans
un `center`).

Résultat : chapitre 14 → 13 pages, livre entier **382 → 380 pages**.
Aucun `Overfull \hbox` introduit.

## 2026-08-31 — Énoncé/arbre côte à côte (deux `minipage`)

Sur demande, les deux exercices du chapitre où un arbre pondéré est
directement suivi de questions courtes (échauffement « Lire un arbre
pondéré », exercice résolu M1/M2) passent d'un empilement vertical
(arbre puis liste de questions) à deux `minipage[t]` côte à côte
(arbre à gauche ~0,43 largeur, texte à droite ~0,54).

Piège TikZ rencontré : un `tikzpicture` placé tel quel dans une
`minipage[t]` ne s'aligne PAS par le haut avec sa colonne voisine — par
défaut, la « ligne de base » d'une image TikZ est calée sur le BAS de
son cadre (hauteur = tout le dessin, profondeur = 0), donc `minipage[t]`
aligne le haut du texte voisin sur le bas de l'arbre, pas sur son haut.
Résultat observé : la liste de questions apparaissait entièrement sous
l'arbre au lieu d'à côté. Corrigé avec l'option TikZ
`baseline=(current bounding box.north)`, qui cale le point de référence
sur le sommet du dessin ; le `\begin{center}...\end{center}` autour de
l'arbre a aussi été remplacé par `\centering` (le premier ajoute de
l'espace vertical avant le contenu, ce qui aurait faussé à nouveau
l'alignement).

Second piège : une colonne de texte trop étroite (~0,53 de largeur)
fait déborder les lignes calculées sur 2–3 lignes au lieu d'une seule,
ce qui peut rendre le bloc texte plus haut que l'arbre lui-même et
annuler le gain d'espace, voire faire sauter tout le bloc (minipages
côte à côte = un seul bloc insécable) à la page suivante en laissant un
grand blanc. Équilibre retenu après plusieurs essais : arbre 0,43,
texte 0,54 (proche de moitié-moitié, l'arbre ayant besoin d'environ
5 cm de large pour ne pas déborder de son cadre).

Résultat : le chapitre passe à 13 pages (contre 13 déjà après la
compaction des arbres seule — le gain se voit surtout en confort de
lecture et en marge de sécurité pour de futurs ajouts, la compaction
des arbres avait déjà absorbé l'essentiel du gain de pages). Le même
patron (`minipage[t]` + `baseline=(current bounding box.north)` +
`\centering`) est réutilisable pour tout futur exercice associant un
schéma TikZ à un énoncé ou une liste de questions courte.

## 2026-08-31 — Maquette : rubriques d'illustration (Probabilités conditionnelles)

Essai, sur un seul chapitre, de rubriques destinées à aérer le cours et à
donner au livre une identité propre. Trois environnements ajoutés dans
`config/environnements.tex` :

- **`vraievie`** (encadré, une seule par chapitre) : un fait réel mis en
  équation avec la notion du chapitre. Ici « Un test positif, est-on
  vraiment malade ? » — TDR du paludisme, sensibilité et spécificité à
  95 %, prévalence 2 % : $\Prob(T) = 0{,}068$ puis Bayes donne
  $\Prob_T(M) \approx 0{,}28$. Pictogramme TikZ des 68 tests positifs
  pour 1 000 consultants (19 malades / 49 non-malades), et rappel que le
  résultat tient à la prévalence : à $\Prob(M) = 0{,}4$ on remonte à 0,93.
- **`reperehisto`** (note courte, filet à gauche, sans cadre) : Thomas
  Bayes, texte lu à la Royal Society en 1763 par Richard Price, portée
  générale donnée par Laplace vers 1774. Placée sous le théorème.
- **`clindoeil`** (même style, en italique) : « indépendants » et
  « incompatibles » ne sont pas synonymes mais presque contraires.
  Placée sous l'encadré `attention` correspondant.

Commande `\reserve{}` pour signaler, en fin d'encadré `vraievie`, les
hypothèses et arrondis du modèle — les maths des encadrés doivent rester
honnêtes.

Coût mesuré : chapitre 14 → 15 pages, livre **381 → 382 pages**, soit
exactement le budget visé d'une page par chapitre. Aucun nouveau
débordement de marge.

## 2026-08-30 — En-tête de chapitre compact

- Les espacements figés du style « Glenn » de `fncychap` (50 pt avant,
  80 pt après le titre, numéro en corps 60) sont redéfinis dans
  `config/style.tex` et pilotés par `\ChapAvant`, `\ChapApres` et
  `\ChapNumSize`. Même dessin, ouverture de chapitre deux fois moins
  haute : le livre passe de 398 à 393 pages.
- Densité du texte : `\linespread` ramené de 1.05 à 1.0 et `\parskip`
  de 0.4em à 0.3em, après comparaison de six réglages compilés en entier.
  393 → 381 pages, sans nouveau débordement de marge.

## 2026-08-30 — Isométries : batteries d'exercices sur les composées

Enrichissement du chapitre **Les Isométries du Plan** (12 nouveaux
exercices, 10 nouvelles pages), autour de deux axes demandés :

- **Nouvel exercice résolu illustré** « Décomposer $r$ et $t$ à partir
  d'une figure » : la méthode de l'axe commun est cette fois *construite*
  sur une figure TikZ (carré, axes $\Delta$, $\Delta_1$, $\Delta_3$, centre
  $\Omega = O$ lu à l'intersection).
- **§ Batterie : composées d'isométries** (6 exercices) : reconnaissance
  rapide de 12 composées, enchaînements par les complexes, le groupe des
  8 isométries du carré (avec figure), produit de trois réflexions,
  décomposition imposée ($f = t\circ r$ avec centre choisi), composées et
  points fixes.
- **§ Décomposer une rotation et une translation sur une figure**
  (6 exercices, tous accompagnés d'une figure) : rectangle (symétrie
  centrale), carré et l'ordre des facteurs ($t\circ r$ vs $r\circ t$,
  centre $r(\Omega)$), triangle équilatéral (le centre est le sommet $C$),
  hexagone régulier (centres $D$ et $E$), reconnaissance d'une rotation
  sur un repère quadrillé puis retour à l'axe commun, et une symétrie
  glissée à réduire (niveau ★★★).
- Les sujets types Bac existants sont désormais regroupés sous un
  sous-titre dédié « Sujets types Bac et synthèse ».

Le livre passe de 390 à 398 pages ; aucun nouveau débordement de marge
(un seul `Overfull` dans le chapitre, préexistant, de 0,8 pt).

## 2026-08-30 — Audit des autres encadrés (`attention`, `astucebac`, `resume`)

Même vérification que pour `methode`. **Les trois sont sains.**

| Encadré | Blocs | Contenu insécable | Trou constaté |
|---|---|---|---|
| `attention` | 25 | 0 | aucun |
| `astucebac` | 34 | 2 | 4,6 pt et 18 pt — négligeables |
| `resume` | 3 | 3 (figures TikZ) | ≤ 10 pt, les boîtes se coupent bien |
| `objectifs` | 20 | 0 | aucun |

Les deux `astucebac` à contenu insécable (organigramme TikZ des
transformations, petite table de la loi normale) ne posent pas de problème :
ils sont entourés de texte dans la boîte, qui peut donc se couper autour.
Les trois `resume` contiennent une figure TikZ mais se coupent correctement,
la figure passant en bloc à la page suivante.

**Trouvé en revanche : un vrai trou de 109 pt** en page 213 (Barycentre),
causé non pas par un encadré mais par une **figure TikZ posée en plein
texte** (`\begin{center}\begin{tikzpicture}`), donc insécable. Passée en
flottant `[htbp]` : la figure reste juste après la propriété qu'elle
illustre (haut de la page suivante) et le bas de page est désormais rempli.

Restent 4 blancs > 45 pt dans le livre, tous **normaux** : ce sont des
titres de section ou de sous-section que LaTeX refuse de laisser seuls en
bas de page (p. 73, 157, 284), plus un cas limite à 54 pt où l'encadré ne
tient réellement pas (p. 168). 390 pages, 12 `Overfull` inchangés.

---

## 2026-08-30 — `methode` : le saut de page forcé, vérifié et corrigé

**Vérification.** Contrairement à ce qu'on pouvait craindre, l'option
`breakable` de la boîte `methode` **fonctionne** : un test dédié montre
qu'une boîte au contenu textuel se coupe normalement d'une page à l'autre.
Elle ne « force » donc pas un saut de page en général.

**Vraie cause.** La boîte saute entière à la page suivante uniquement quand
son contenu est un **bloc insécable**. Sur les 68 blocs `methode` du livre,
**4** étaient dans ce cas : ceux dont le contenu est un `tabular`
(`limites_continuite`, `fonctions`, `integrales`, `suites`). Un `tabular` ne
peut pas être coupé, donc la boîte non plus.

**Conséquence mesurée.** Page 119 (chapitre Limites et continuité) perdait
**222 pt de blanc**, soit un tiers de page, et le titre de section
« Méthodes et exercices résolus » restait seul en bas de page.

**Correctif.** Nouvel environnement `tabmethode` dans
`config/environnements.tex` : même rendu à deux colonnes alignées avec filets,
mais construit ligne par ligne (`\ligne{gauche}{droite}`, en `parbox`), donc
**sécable entre deux lignes**. Les 4 tableaux y sont convertis.

**Résultat.** Le trou de 222 pt a disparu : le titre de section et la boîte
entière tiennent maintenant en page 119. Les deux autres blancs signalés par
la détection (p. 157 et p. 284) ne viennent pas de `methode` : ce sont des
titres de section reportés en début de page, comportement normal et
souhaitable. 390 pages, 12 `Overfull` inchangés, aucun `vbox`.

---

## 2026-08-30 — Économie de pages sur tout le livre

Objectif demandé : gagner un maximum de pages sans nuire à la lisibilité.
**Résultat : 398 → 390 pages (−8), 13 `Overfull \hbox` (baseline inchangée),
aucun `Overfull`/`Underfull \vbox`.**

- **Trois réglages globaux** dans `config/environnements.tex` :
  - listes resserrées : `\setlist{topsep=2pt, itemsep=1pt, parsep=0pt,
    partopsep=0pt}` ;
  - air autour des formules centrées réduit (`abovedisplayskip` /
    `belowdisplayskip` 10pt → 4pt) — **c'est le plus gros gisement** :
    le livre compte plus de 250 formules en display ;
  - moins d'air avant chaque titre d'exercice (`\bigskip` → `\medskip`).
  Les formules gardent leur taille : on enlève de l'air, pas du contenu.
- **Deux environnements réutilisables** (paquet `tasks`) :
  - `qcm` : propositions (A)(B)(C)(D) en colonnes ;
  - `listecol` : liste numérotée courte en colonnes.
- **Chapitre Complexes** : les 12 blocs de propositions de QCM passent de
  4 lignes à 2 (ou 1) ; libellés resserrés ; `\dfrac` remplacé par des
  quotients en ligne dans les propositions de QCM (ils doublaient la
  hauteur des lignes).
- **Reste du livre** : seules 6 listes courtes étaient encore en une seule
  colonne (arithmétique, complexes, barycentre, isométries) — les batteries
  d'exercices d'analyse et de probabilités utilisaient déjà `multicols`.
- Trois QCM du chapitre Complexes avaient **plusieurs réponses correctes** ;
  corrigés (voir le commit dédié).
- Gains par chapitre : Arithmétique 30 → 28 p, Complexes 44 → 42 p,
  Calcul matriciel 18 → 17 p, etc.
- **Barèmes retirés des sujets types** : les 507 mentions de points
  (« \hfill (0,5 pt) » et « \hfill \mbox{(0,75~pt)} », plus 4 barèmes
  composites du chapitre Barycentre) disparaîssent des sujets types des
  17 chapitres et de `entrainement.tex`. **Les annales officielles
  (`parties/annales/`) ne sont pas touchées** : le barème y fait partie du
  document original, de même que le « N points » en tête de chaque exercice.
- **Rédaction des exercices résolus** : audit des 84 exercices résolus du
  livre. Les 10 enchaînements de formules écrits en `$$` séparés
  (développement du binôme, algorithme d'Euclide, longueurs d'un triangle,
  tests de Pythagore, les deux expressions du produit scalaire…) sont
  regroupés en un seul bloc `aligned` : les « = » s'alignent, la chaîne de
  calcul se lit d'un coup d'œil, et les blancs intermédiaires disparaissent.

---

## 2026-08-30 — Complexes : trois résumés de cours illustrés

- Nouvel environnement `resume` dans `config/environnements.tex`
  (`\begin{resume}{Titre}`), même famille visuelle que `methode` /
  `astucebac` : encadré gris, filet noir à gauche, icône `\faBookmark`.
  Réutilisable dans tous les chapitres.
- Trois résumés courts ajoutés au chapitre Complexes, chacun avec sa
  figure TikZ :
  - **Forme exponentielle** — notation, les 6 règles de calcul (produit,
    quotient, puissance, conjugué, inverse, opposé), condition d'égalité ;
    figure : cercle unité avec $\e^{\ii\theta}$ et les valeurs
    remarquables ($1$, $\e^{\ii\pi/6}$, $\e^{\ii\pi/4}$,
    $\e^{\ii\pi/3}$, $\ii$, $-1$, $-\ii$).
  - **Formule de Moivre** — l'énoncé encadré, à quoi elle sert
    (développer, l'inverse de la linéarisation), la méthode en 3 gestes,
    l'exemple $n = 3$ ; figure : $z$, $z^2$, $z^3$, $z^4$ sur le cercle,
    « multiplier par $z$, c'est tourner de $\theta$ ».
  - **Linéarisation** — but (intégrer), formules d'Euler, les quatre
    identités à connaître par cœur, le piège du $\ii$ au dénominateur ;
    figure : schéma en 4 étapes de la méthode.
- **Harmonisation avec les exercices et les sujets types** — les trois
  résumés ne restent pas isolés du reste du chapitre :
  - deux exercices résolus ajoutés : *calculer une puissance avec la forme
    exponentielle* ($(1+\ii)^{12}$, $(\sqrt3-\ii)^9$) et *linéariser
    $\cos^4\theta$ puis calculer $\int_0^{\pi/2}\cos^4\theta\dd\theta$* ;
  - trois items ajoutés au Vrai/Faux d'échauffement (validité de
    $(\e^{\ii\theta})^n = \e^{\ii n\theta}$ pour $n$ négatif, égalité de
    deux exponentielles modulo $2\pi$, identité $\cos^2$) ;
  - deux exercices d'entraînement progressifs avant l'exercice
    « Trigonométrie » (★☆☆ *Forme exponentielle : calculer vite*, puis
    ★★☆ *Puissances et formule de Moivre*), et l'exercice ★★★ complété
    d'une question d'intégration ;
  - un **sujet type Bac** dédié au format officiel (Partie A forme
    exponentielle et puissances / Partie B Moivre / Partie C linéarisation
    et intégrale, points par question) ;
  - renvois croisés `\pageref` depuis chaque exercice vers le résumé
    correspondant (labels `res:cplx_expo`, `res:cplx_moivre`,
    `res:cplx_linear`).
- Vérification : `latexmk -pdf` OK, 398 pages, **13 `Overfull \hbox`, soit
  exactement la baseline de `main`** (le schéma de linéarisation, d'abord
  trop large de 18,7pt, a été resserré). Résumés, exercices résolus,
  exercices et sujet type relus au rendu PNG ; deux figures retouchées pour
  que les étiquettes ne se chevauchent pas.

---

## 2026-08-27 — Structure : les parties du livre activées

- Les cinq `\part{}` de `main.tex` étaient **écrits mais commentés** : la
  structure Algèbre / Analyse / Géométrie / Probabilités n'apparaissait ni
  dans le PDF ni dans la table des matières, le livre se lisant comme une
  suite plate de 20 chapitres. Ils sont désormais actifs.
- Ajout d'une 5ᵉ partie **« Sujets et entraînement »** devant
  `sujet_types` et `entrainement` : sans elle, les annales et les 19 sujets
  types semblaient appartenir à la partie Probabilités.
- Ordre des parties **inchangé** (Algèbre → Analyse → Géométrie →
  Probabilités) : c'est le seul qui respecte toutes les dépendances réelles
  (Probabilités a besoin d'Intégrales et de `exp` pour les lois à densité ;
  Isométries a besoin des Complexes ; Équa diff a besoin des racines
  complexes) et il suit le programme officiel. Ajouter un `\part` ne
  renumérote aucun chapitre — aucune référence croisée touchée.
- Vérification : `latexmk -pdf` OK, 394 pages, 5 `\contentsline {part}`
  dans `main.toc`, et **13 `Overfull \hbox` avant comme après** (baseline
  `main` recompilée pour comparaison) — zéro régression.
- Constat au passage : `annexes/formulaire.tex` est **vide (0 octet)**, donc
  rien à brancher sous le `\appendix` qui reste inutilisé. Voir STATUS.

---

## 2026-08-27 — Les 5 chapitres de probabilités alignés

- Fin du chantier « modèle type » : `parties/probabilites/probabilites.tex`,
  `conditionnelles.tex`, `variables_aleatoires.tex`, `binomiale.tex`,
  `normale.tex` refondus selon le modèle type et le programme officiel.
- Ajouts de cours : **dénombrement** (principe multiplicatif, $p$-listes,
  arrangements, permutations, combinaisons, tableau des 3 modèles) et
  système complet dans « Probabilités » ; **probabilités totales
  généralisées + formule de Bayes** dans « Probabilités conditionnelles » ;
  linéarité $\Var(aX+b)$, $\sigma(aX+b)=|a|\sigma$, notion de jeu
  équitable / favorable dans « Variables aléatoires » ; **méthode de seuil**
  ($(1-p)^n\le\alpha$ par le logarithme) + identités du binôme par
  dérivation dans « Loi binomiale » ; **espérances** des lois continues,
  **absence de mémoire** de la loi exponentielle, **standardisation** et
  méthode du quantile, table courte de $\Phi$ dans « Loi normale ».
- Chaque chapitre : citation, objectifs étoffés, section « Méthodes et
  exercices résolus » (3 exercices résolus), section « Exercices
  d'entraînement » en sous-sections — Échauffement (lecture d'arbre / de
  diagramme + **Vrai/Faux** 7 items), batteries `multicols`, et **5 sujets
  types Bac** au format officiel (Partie A / Partie B, sous-questions
  cotées 0,25–1,25 pt, « Montrer que … » avec cible fournie). Sujets phares :
  urne + tirage simultané, dé pipé, digicode, comité mixte, sondage
  (Poincaré) ; test de dépistage (Bayes), chaîne de production, **marche
  aléatoire** $p_{n+1}=\frac{7}{12}p_n+\frac14$ ; roue de loterie,
  assurance, comparaison de deux jeux ; contrôle qualité + seuil, QCM,
  jeu répété + suite $u_n$, binôme de Newton ; masse de paquets, durée de
  vie exponentielle, temps d'attente, notes d'examen (quantile), réglage
  d'une machine.
- Figures TikZ conservées + nouvelle figure « système complet » pour les
  probabilités totales, diagrammes en bâtons pour les échauffements.
- `latexmk -pdf main.tex` : **389 pages**, 0 erreur, aucune référence non
  résolue, **aucun `Overfull`** dans tout le livre.
- Branche `chapitres-probabilites-alignement` → PR contre `main`.

## 2026-08-27 — Chapitre « Équations différentielles » aligné

- `parties/analyse/equadiff.tex` : le cours mathématique était déjà
  complet et correct ; réaligné sur le modèle type.
  - ajout d'une **citation** (`citationchapitre`, guillemets « ») et
    objectifs resserrés ;
  - nouvelle **méthode « vérifier qu'une fonction est solution »**
    (au programme) + exemple ;
  - section **« Équations avec second membre »** : théorème de structure
    (solution générale = particulière + homogène) + méthode + exercice
    résolu ;
  - cours 1er / 2nd ordre présenté en théorèmes + tableau des 3 cas selon
    Δ ; cas particuliers `y''=±m²y` ;
  - **échauffement** : figure « faisceau de courbes intégrales » de
    `y'+y=0` (TikZ, scope clippé) + **Vrai/Faux** (7 items) ;
  - exercices progressifs : 1er ordre (solution générale, Cauchy,
    décroissance radioactive), 2nd ordre (équation caractéristique,
    Cauchy, oscillations) en `multicols` ;
  - **6 sujets types Bac** : refroidissement (second membre + modèle
    thermique) ; vérifier que `g` est solution puis résoudre (récupère
    l'exercice `f_n` retiré du chapitre exponentielle) ; tangente imposée
    `y''-3y'+2y=0` ; pendule + conservation de l'énergie ; `y''+y=cos x`
    (solution particulière + intégrale) ; changement d'inconnue
    `x²y''+3xy'+y=0`.
- `latexmk -pdf main.tex` : **363 pages**, 0 erreur, aucune référence non
  résolue, aucun `Overfull`.
- Branche `chapitre-equadiff` → PR contre `main`.
- **Tout le bloc analyse est désormais aligné** ; il ne reste que les
  5 chapitres de probabilités.

## 2026-08-27 — Chapitre « Suites numériques » aligné

- `parties/analyse/suites.tex` : le chapitre ne contenait que la
  récurrence (sans objectifs, sans citation). Refondu selon le modèle
  type et le programme officiel :
  - récurrence (domino + figure `resume_recurrence` conservées, méthode
    de rédaction, exemple résolu, `attention` sur l'hérédité seule) ;
  - **sens de variation d'une suite : les 4 méthodes** (différence
    u_{n+1}−u_n ; quotient u_{n+1}/u_n si u_n>0 ; fonction associée
    u_n=f(n) ; récurrence) — demande utilisateur explicite ;
  - suites majorées / minorées / bornées ;
  - **limite : convergence / divergence**, unicité, limites de référence
    (1/n^α, q^n, croissances comparées), opérations ;
  - **théorèmes de convergence et de divergence** : limite monotone,
    comparaison (divergence), gendarmes, comparaison (limite finie),
    passage à la limite ;
  - suites u_{n+1}=f(u_n) : méthode (stabilité + monotonie + point fixe)
    + théorème du point fixe + `attention` ;
  - suites particulières : arithmétiques / géométriques (table),
    arithmético-géométriques (méthode v_n=u_n−ℓ), suites adjacentes.
- Exercices : Vrai/Faux + **batteries multicolonnes** — premiers termes,
  récurrence (égalités, suites, inégalités dont Bernoulli), sens de
  variation, limites directes (3 col), **convergente ou divergente ?**,
  **par les gendarmes**, **limite monotone**, arithmético-géométrique —
  + **5 sujets types Bac** (suite √ + vitesse |u_n−2|≤2(1/2)^n ;
  arith.-géo. + somme S_n ; suites adjacentes Σ1/k² ; Héron → √3 ;
  n!/n^n comparaison + croissances comparées).
- `latexmk -pdf main.tex` : **361 pages**, 0 erreur, aucune référence non
  résolue, aucun `Overfull`.
- Branche `chapitre-suites` → PR contre `main`.

## 2026-08-27 — Chapitre « Primitives et intégrale » aligné + correctif `\dd`

- `parties/analyse/integrales.tex` refondu selon le modèle type et le
  programme officiel. Ajouts / affinages :
  - primitives usuelles : ajout de **1/x → ln|x|** et **e^x → e^x**
    (absents) ; primitives composées : ajout de **u'/u → ln|u|** et
    **u'e^u → e^u** (c'est ici que renvoient les chapitres ln/exp) ;
  - **section « Fonction définie par une intégrale »** (théorème
    fondamental + dérivée à bornes variables `∫_{u(x)}^{v(x)}`) — était
    absente, au programme ;
  - **section « Changement de variable affine »** — était absente ;
  - **moments d'inertie d'une plaque** (I_{Oy}, I_{Ox}) ajoutés aux
    applications (aire / valeur moyenne / volume déjà présents) ;
  - exemples réécrits avec ln/exp (cohérence bloc analyse) ;
  - méthode « quelle technique ? » + 3 exercices résolus.
- Exercices : Vrai/Faux + **5 batteries `multicols` 2–3 colonnes**
  (primitives usuelles en 3 col, primitives composées, intégrales
  directes, changement de variable affine, IPP, dérivée d'une fonction
  intégrale) + applications + **5 sujets types Bac** (suite I_n=∫x^n e^{-x},
  fonction ∫ ln t/t², aire/volume/encadrement de ln 2, sommes de Riemann,
  IPP itérée → Σ 1/k! → e).
- **Correctif global** : `config/commandes.tex`, macro `\dd` passée de
  `,\mathrm{d}` (virgule visible) à `\,\mathrm{d}` (espace fine). Toutes
  les intégrales du livre étaient rendues « f(x) , dx ». Voir
  vigilance dans STATUS.md.
- `latexmk -pdf main.tex` : **351 pages**, 0 erreur, aucune référence non
  résolue, aucun `Overfull`.
- Branche `chapitre-integrales` → PR contre `main`.

## 2026-08-27 — Chapitres « Logarithme » et « Exponentielle » resserrés

- Demande utilisateur : revoir les contenus (définition, propriétés,
  théorèmes, dérivée de ln(u) / e^u), ne garder que l'essentiel des
  **exercices de calcul direct en deux colonnes**, **éviter les doublons**.
- `parties/analyse/logarithme.tex` : cours compact (def comme primitive de
  1/x ; variation + signe + courbe ; propriétés algébriques ; limites
  usuelles en table ; dérivée ln(u), ln|u|, ln(ax+b) ; équations /
  inéquations / **systèmes** ; **logarithme de base a et décimal** —
  ajout au programme). Exercices : Vrai/Faux + 5 batteries `multicols{2}`
  (simplifier, équations, inéquations, dériver, limites directes) + 3
  synthèses courtes. Renvois « voir Limites et continuité » (FI) et
  « voir Primitives et intégrale » (u'/u).
- `parties/analyse/exponentielle.tex` : même structure (def réciproque de
  ln ; variation + courbe ; propriétés ; limites usuelles ; dérivée e^u,
  e^{ax+b} ; équations / inéquations / systèmes ; **fonctions a^x et
  u^v**). Exercices : Vrai/Faux + 5 batteries `multicols{2}` + 3
  synthèses. **Section « Équations différentielles » supprimée**
  (doublon avec `equadiff.tex`), ainsi que le gros Problème 2 sur f_n
  (couvert par « Étude d'une fonction »).
- `latexmk -pdf main.tex` : **346 pages** (−8), 0 erreur, aucune référence
  non résolue, aucun `Overfull`.
- Branche `chapitres-ln-exp` → PR contre `main`.

## 2026-08-27 — Chapitre « Étude d'une fonction » (ex-« Généralités »)

- `parties/analyse/fonctions.tex` **entièrement recentré** (demande
  utilisateur). Le chapitre ne traite plus que :
  - le **plan d'étude** d'une fonction (méthode 8 étapes + propriété
    signe de f' / variations + étude complète résolue de (x−1)eˣ) ;
  - le **diagramme d'étude des branches infinies** (schéma TikZ en
    escalier : limite → f/x → f−ax ; asymptote H/V/oblique, direction
    asymptotique, branche parabolique) ;
  - **convexité / concavité / point d'inflexion** : théorème
    (f″ ≥ 0 ⟺ convexe), propriété (inégalités eˣ ≥ 1+x, ln x ≤ x−1),
    figure, application résolue ;
  - **position relative d'une courbe et d'une droite** (asymptote /
    tangente / sécante ; résolution graphique) ;
  - **identification de f, f', f″ sur une même figure** (méthode +
    exercice résolu sur e^{−x²}).
- Ancien contenu « généralités » (domaine, parité, monotonie, extrema
  détaillés) : replié dans les étapes du plan / la propriété signe de f'.
  Titre du chapitre : « Étude d'une fonction ».
- Tous les exemples et exercices sur ln/exp.
- Exercices : échauffement (lire courbe + dérivée, diagramme branches
  infinies, \textbf{Vrai/Faux} 8 items) ; batteries (branches infinies,
  convexité, inégalités, position) ; \textbf{identification $f/f'/f''$}
  (2 exercices avec figure) ; \textbf{5 sujets types Bac} (étude complète
  $(x+1)\e^{-x}$ ; $\tfrac{\ln x}{x}$ ; asymptote oblique
  $x-2+\tfrac{\ln x}{x}$ ; identification sur $\ln(1+x^2)$ ; famille
  $x+m\e^{-x}$).
- `latexmk -pdf main.tex` : **354 pages, 0 erreur**, aucune référence non
  résolue, aucun `Overfull`.
- Branche `chapitre-etude-fonctions` → PR contre `main`.

## 2026-08-27 — Chapitre « Dérivabilité » aligné sur le modèle type

- `parties/analyse/derivation.tex` entièrement refondu selon le modèle type
  (Isométries) et le programme officiel. **Parti pris : ln et exp
  uniquement** dans tous les exemples et exercices.
- Cours : citation + objectifs étoffés ; dérivabilité en un point
  (point anguleux $|\e^x-1|$, demi-tangente verticale $\sqrt{\ln x}$) ;
  interprétation géométrique + figure ; fonction dérivée, tables
  (dérivées usuelles avec $\ln$/$\e^x$, opérations) et **dérivée d'une
  composée** ; **dérivée de la réciproque d'une bijection** ($\ln$ via
  $\exp$) ; **dérivées successives** (récurrence $x\e^x$) ; **convexité /
  concavité / points d'inflexion** + figure + inégalités $\e^x\ge 1+x$,
  $\ln x\le x-1$ ; **TAF et IAF** (encadrement de $\ln 1{,}2$).
- **Nouvelle section « Familles de fonctions dépendant d'un paramètre »**
  (demande utilisateur) : méthode (point fixe commun, lieu des extremums
  par élimination de $m$, tangentes) + 2 exercices résolus
  ($\e^x-mx$, $(x-m)\e^x$).
- Section « Méthodes et exercices résolus » : méthode de raccord + 3
  exercices résolus (calcul de dérivées, raccord + demi-tangentes,
  encadrement par IAF).
- **Section « Exercices d'entraînement »** : échauffement (lecture de
  courbe + figure, dérivable ou non, **Vrai/Faux** 8 items) ; batteries
  de calcul de dérivées en colonnes ; tangentes / convexité / réciproque ;
  **familles à paramètre** ($\e^x+mx$, $x-m\e^x$, $x^n\e^{-x}$) ;
  **5 sujets types Bac** (point anguleux + réseau ; fonction auxiliaire
  $\e^x-x^2$ ; réseau $(x+m)\e^{-x}$ ; bijection réciproque + suite avec
  IAF ; dérivées successives $x^2\e^x$ + discussion selon $m$).
- La continuité et le TVI restent au chapitre précédent ; une `remarque`
  d'ouverture y renvoie.
- `latexmk -pdf main.tex` : **349 pages, 0 erreur**, aucune référence non
  résolue, aucun `Overfull` dans le chapitre.
- Branche `chapitre-derivabilite` → PR contre `main`.

## 2026-08-27 — Fusion « Limites et continuité » + chapitre « Dérivabilité »

- Nouveau fichier `parties/analyse/limites_continuite.tex` : chapitre unique
  regroupant les limites (ancien `limites.tex`) et la continuité (partie
  détachée de `derivation.tex`). **Parti pris** : tous les exemples et
  exercices s'appuient sur $\ln$ et $\exp$ ; les puissances n'apparaissent
  que comme terme de comparaison (croissances comparées).
- Cours : limites de référence $\ln$/$\exp$ + croissances comparées +
  limites usuelles ; 4 techniques de levée d'indétermination (terme
  dominant, division, limite usuelle, changement de variable) ; composée ;
  comparaison / gendarmes ; continuité + prolongement ; TVI + corollaire +
  image d'un intervalle ; asymptotes. Figures TikZ : courbes $\ln$/$\exp$,
  schéma TVI, lecture graphique.
- Exercices : échauffement (lecture graphique, continuité, Vrai/Faux) ;
  **5 batteries de calcul de limites en 2–3 colonnes** (`multicols`) avec
  clé de réponses ; continuité/prolongement/TVI ; **5 sujets types Bac**
  (fonction par morceaux, $\frac{\ln x}{x}$, suite implicite $\e^x+x=n$,
  fonction auxiliaire + TVI, symétrie et asymptotes).
- **Intégration dans `main.tex`** : `\input{parties/analyse/limites}` et
  `\input{parties/analyse/continuite}` remplacés par
  `\input{parties/analyse/limites_continuite}`. Fichiers `limites.tex` et
  `continuite.tex` (ce dernier était vide) supprimés (`git rm`).
- **`derivation.tex` devient le chapitre « Dérivabilité »** : titre changé,
  objectifs recentrés sur la dérivation, sections « Continuité » et
  « Théorème des valeurs intermédiaires » retirées (désormais dans le
  chapitre précédent), `\begin{remarque}` d'ouverture renvoyant vers lui.
  Le reste (dérivabilité en un point, interprétation géométrique, fonction
  dérivée, TAF, exercices) est inchangé.
- Prévisualisation isolée conservée : `apercu_limites_continuite.tex`
  (non incluse dans `main.tex`).
- `latexmk -pdf main.tex` : **339 pages, 0 erreur**, pas de référence
  non résolue, aucun `Overfull` ajouté dans les fichiers touchés.
- Branche `chapitre-limites-continuite` → PR contre `main`.

## 2026-08-27 — Chapitre Calcul matriciel aligné sur le modèle type

- `parties/algebre/matrices.tex` : ajout d'une citation, objectifs étoffés,
  3 blocs `\begin{methode}` (inverse par relation polynomiale ; calcul de
  $A^n$ par récurrence / décomposition $\lambda I + N$ / relation du 2ᵈ
  degré ; système $AX = B$).
- **Nouvelle section « Exercices d'entraînement »** : Échauffement (calculs
  de base, déterminant/inverse, puissances, **Vrai/Faux**), sous-section
  « Opérations, déterminant, puissances », et **6 sujets types Bac**
  (relation polynomiale + récurrence ; opérations/trace/transposée ;
  système $2\times2$ ; puissance par décomposition ; inverse par relation +
  système $3\times3$ ; déterminant/trace/inversibilité).
- **Déplacement demandé** : la section `\section*{Sujets type : Calcul
  matriciel}` (6 sujets) a été retirée de `entrainement.tex` et intégrée au
  chapitre (Sujet 1 légèrement modifié pour ne pas dupliquer le sujet
  officiel 2026).
- Compile sans erreur (332 pages) ; aucun `Overfull \hbox` visible ajouté.
- Branche `chapitre-matrices`, PR contre `main`.

## 2026-08-27 — Chapitre Arithmétique aligné sur le modèle type

- `parties/algebre/arithmetique.tex` complété selon le modèle type et le
  programme officiel.
- Cours : ajout du **petit théorème de Fermat** (restes de puissances) ;
  nouvelle section **$\Z/n\Z$** (classes, opérations, table de $\Z/5\Z$,
  méthode de résolution des équations et systèmes) ; nouvelle section
  **PPCM** (relation $\mathrm{PGCD}\times\mathrm{PPCM} = |ab|$, décomposition
  en facteurs premiers, astuce « système $\{\mathrm{PGCD} = d\ ;\ x+y=s\}$ »
  + exercice résolu) ; nouvelle section **Systèmes de numération** (écriture
  en base $b$, conversions, hexadécimal, critères de divisibilité).
- Exercices restructurés : « Exercices d'entraînement » avec Échauffement
  (divisibilité/bases, PGCD-PPCM, calculs dans $\Z/n\Z$, Vrai/Faux) puis
  deux sous-sections thématiques, et **5 sujets types Bac** calqués sur
  l'Exercice 1 (arithmétique) des sessions : divisibilité + $\Z/5\Z$ +
  Bézout ; systèmes PGCD-somme + système dans $\Z/5\Z$ ; restes de
  puissances + équation diophantienne ; systèmes de numération ; PGCD de
  deux expressions + Gauss.
- Corrigé au passage : un `\\` de fin de ligne perdu dans un `\begin{cases}`
  du 5e sujet type Bac de `complexes.tex` (PR de correctif séparée).
- Compile sans erreur (328 pages) ; aucun `Overfull \hbox` visible ajouté.
- Branche `chapitre-arithmetique`, PR contre `main`.

## 2026-08-27 — Chapitre Géométrie dans l'espace (création)

- `parties/geometrie/espace.tex` était vide : rédaction complète du chapitre
  sur le modèle type, en couvrant tout le programme officiel.
- Cours : repérage et vecteurs de l'espace ; colinéarité / coplanarité /
  décomposition dans une base ; **produit scalaire** (analytique +
  géométrique, orthogonalité) ; **produit vectoriel** (analytique +
  géométrique, aire, volume par produit mixte) ; le plan (représentation
  paramétrique, vecteur normal, équation cartésienne, plan $(ABC)$) ; la
  droite (paramétrique, intersection de deux plans) ; positions relatives
  (2 plans / plan-droite / 2 droites, avec tableau) ; distances
  (point-plan, point-droite, plans parallèles) et projeté orthogonal ; la
  sphère (équation, intersection sphère-plan).
- 3 figures TikZ (repère 3D, plan + vecteur normal, cube) + tableau
  récapitulatif des positions relatives.
- 4 exercices résolus (plan $(ABC)$ + position d'une droite ; distance et
  projeté ; sphère et plan ; deux droites non coplanaires).
- Exercices d'entraînement : Échauffement (cube, tétraèdre, Vrai/Faux),
  « Vecteurs, produit scalaire et produit vectoriel », « Droites et
  plans », et **5 sujets types Bac** calqués sur l'Exercice 2 des sessions
  2021–2026 (plan + droite + distance ; produit vectoriel + parallélisme ;
  deux plans parallèles ; sphère + droite perpendiculaire à un plan ; deux
  droites orthogonales + plan commun).
- Compile sans erreur (320 pages) ; aucun `Overfull \hbox` visible ajouté.
- Branche `chapitre-espace`, PR contre `main`.

## 2026-08-27 — Refonte du chapitre Nombres complexes

- `parties/algebre/complexes.tex` recentré sur le contenu demandé : quatre
  formes (algébrique, trigonométrique, exponentielle, **polaire** — ajout
  d'une définition + tableau récapitulatif), équations polynomiales de
  degré **2, 3 et 4** (racine évidente/donnée, factorisation, bicarrée,
  racines $n$-ièmes d'un complexe), **systèmes de deux équations à deux
  inconnues** (somme–produit et linéaire à coefficients complexes),
  applications trigonométriques (linéarisation, Moivre, réduction
  $a\cos x + b\sin x$).
- **Accent géométrie + ensembles de points** : section « Nombres complexes
  et géométrie » enrichie (quotient d'affixes, conditions d'alignement /
  orthogonalité / cocyclicité, nature d'un triangle) ; nouvelle section
  « Ensembles de points » (module, argument, quotient, partie réelle /
  imaginaire) avec 3 figures TikZ et un tableau récapitulatif.
- Section exercices restructurée : « Méthodes et exercices résolus »
  (2 blocs méthode + 3 exercices résolus neufs : degré 3, système
  somme–produit, ensemble de points) puis « Exercices d'entraînement » en
  sous-sections — Échauffement (5 exercices figure + Vrai/Faux),
  Formes/équations/systèmes, Géométrie et ensembles de points,
  Transformations (exercices existants regroupés), et **5 sujets types
  Bac** centrés sur équations + configuration + ensembles de points.
- Compile sans erreur ; aucun `Overfull \hbox` visible ajouté ; figures
  vérifiées au rendu.
- Branche `chapitre-complexes-refonte`, PR contre `main`.

## 2026-08-27 — Refonte du chapitre Isométries du Plan

- Réécriture complète de `parties/geometrie/isometries.tex` autour de la
  composition et de la décomposition des isométries (demande utilisateur :
  pas assez d'exercices de ce type).
- Cours développé : composée de deux réflexions (axes parallèles →
  translation, axes sécants → rotation) ; décomposition d'une translation
  et d'une rotation en deux réflexions avec l'axe libre ; méthode de
  l'axe commun pour $t\circ r$, $r\circ t$, $r_1\circ r_2$ ; symétrie
  glissée et sa réduction ; écritures complexes (déplacements /
  antidéplacements) ; extension aux homothéties et similitudes directes
  (composées, cas particuliers).
- 6 figures TikZ + 1 arbre de décision + 3 tableaux récapitulatifs.
- 3 exercices résolus (méthode géométrique + contrôle complexe) et
  24 exercices gradués répartis en deux sous-sections :
  « Échauffement : lire une figure » (5 exercices courts basés sur une
  figure — carré, rectangle, triangle équilatéral, triangle rectangle
  isocèle, vrai/faux — avec questions de compréhension) et
  « Composition et décomposition » à difficulté progressive, comprenant
  **5 sujets types Bac** (synthèse transformations ; similitude et
  isométries ; carré + $t\circ r$ + homothétie ; deux rotations et
  symétrie glissée ; similitude indirecte) et 3 exercices difficiles
  centrés sur la décomposition (double décomposition sur un triangle
  équilatéral ; réduction d'un produit de trois réflexions ; composée à
  paramètre et lieu du centre).
- Compile sans erreur ; aucun `Overfull \hbox` visible (> ~10pt) ajouté.
- Branches `chapitre-isometries-composition` (PR #7, mergée) puis
  `isometries-plus-sujets-bac` (PR pour les 3 sujets types Bac ajoutés
  après la consigne du 2026-08-27).

## 2026-08-27 — Chapitre Barycentre aligné sur le modèle type

- Refonte de `parties/geometrie/barycentre.tex` selon la structure de
  référence (cf. modèle du chapitre Isométries) : cours enrichi de
  **6 figures TikZ** (barycentre de 2 points, associativité, centre de
  gravité, ligne de niveau…), homogénéité + conservation par isométrie
  ajoutées, section renommée « Méthodes et exercices résolus » avec un
  `\begin{methode}` et un 4ᵉ exercice résolu (ligne de niveau *droite*,
  σ = 0).
- Section « Exercices d'entraînement » restructurée en deux sous-sections :
  « Échauffement : lire une figure » (segment, triangle, parallélogramme,
  lecture d'une ligne de niveau, Vrai/Faux à 7 items) puis « Barycentre et
  lignes de niveau » à difficulté progressive, terminée par **5 sujets
  types Bac**, chacun en Partie A synthétique / Partie B analytique, calqués
  sur les Problèmes 1 des sessions 2021–2026 : barycentre + discussion de
  $(E_k)$ ; norme = norme donnant un cercle ; fonctions vectorielle et
  scalaire de Leibniz ; cercle d'Apollonius + cercle de diamètre ;
  isobarycentre de 4 points + affixes (couvre aussi la ligne de niveau
  droite, σ = 0).
- `calc`, `angles`, `quotes` ajoutés aux librairies TikZ dans
  `config/packages.tex`.
- Compile sans erreur ; aucun `Overfull \hbox` visible ajouté ; figures
  vérifiées au rendu.
- Branche `chapitre-barycentre-refonte`, PR contre `main`.

## 2026-08-27 — Calcul matriciel : exercice résolu d'inversion polynomiale

- Dans `parties/algebre/matrices.tex`, l'exercice résolu « Utiliser une
  relation polynomiale pour inverser une matrice » utilisait la matrice
  $A$ du sujet Bacc 2022 (Exercice 1.II) — doublon cours/annale.
- Remplacée par $C = (1\,2\,2\,/\,2\,1\,2\,/\,2\,2\,1)$, avec la relation
  $C^3 - 21C - 20\,I_3 = O_3$ d'où
  $C^{-1} = \tfrac15(-3\,2\,2\,/\,2\,-3\,2\,/\,2\,2\,-3)$.
- Même méthode pédagogique, matrice différente. Compile sans erreur.
- Branche `matrices-exercice-inverse-polynomiale`, PR #8, mergée dans `main`.

## 2026-08-26 — Passe de relecture globale (débordements de marge)

- Compilation complète du livre et audit systématique de tous les
  `Overfull`/`Underfull \hbox` (pas seulement les fichiers des sujets
  Bacc) : 27 débordements visibles uniques trouvés dans 8 fichiers
  (`arithmetique.tex`, `matrices.tex`, `limites.tex`, `fonctions.tex`,
  `integrales.tex`, `logarithme.tex`, `barycentre.tex`,
  `variables_aleatoires.tex`), en plus de ceux déjà connus dans
  `entrainement.tex` et les sujets Bacc.
- Corrigés : formules multi-lignes sans `\\` (traitées à tort comme une
  seule ligne), grands ensembles/systèmes en `enumerate` imbriqué,
  plusieurs matrices sur une même ligne, tableaux avec colonnes `c`/`l`
  non adaptées à du contenu long (passage à `array`'s
  `p{largeur}`), et un tableau `tkz-tab` trop large (réduction de `lgt`).
  Ajout du package `array` dans `config/packages.tex`.
- Résultat : 27 → 10 débordements uniques restants, tous soit internes
  (`Underfull`, sans effet visuel), soit vérifiés invisibles au rendu
  (< ~11pt). Vérification visuelle (rendu PNG) de chaque zone corrigée.
- Non touché : les avertissements `Underfull` liés au `\newline` de fin
  de la macro `\exerciceresolu` (cosmétiques, pas de défaut visuel).

## 2026-08-26 — Sujets officiels du Bacc Série S (2021–2026)

- Transcription fidèle des sujets officiels 2021, 2023, 2024, 2025, 2026
  depuis les PDF/photos envoyés par l'utilisateur, chacun dans son propre
  fichier (`parties/annales/bac_20XX.tex`).
- Nouvelle commande `\sujetbacheader{année}` (dans `config/environnements.tex`)
  pour un entête uniforme (année, épreuve, durée, coefficient) sur toutes
  les sessions.
- Nouvelle commande `\probleme` (compteur séparé de `\exercice`) pour que
  les énoncés qui distinguent "Exercice" et "Problème" affichent le bon
  libellé.
- `sujet_types.tex` charge désormais les sessions dans l'ordre
  chronologique via `\input`.
- Le sujet 2022 déjà présent n'a été touché que dans son entête ; son
  contenu est resté intact.
- Travail fait sur la branche `chapitre-bac-officiels`, PR #2, mergée
  dans `main`.

## 2026-08-26 — Chapitre Probabilités + préface/copyright

- Chapitre Probabilités complet (5 sous-chapitres : probabilités,
  conditionnelles, variables aléatoires, binomiale, normale).
- Ajout de la page de copyright et de la préface.
- Travail fait sur la branche `chapitre-probabilites`, PR #1, mergée
  dans `main`.

## 2026-08-22 — 15 sujets types supplémentaires

- Ajout des sujets types n°5 à n°19 dans `entrainement.tex`.

## 2026-08-10 — Chapitre Calcul matriciel

- Ajout du chapitre Calcul matriciel (`parties/algebre/matrices.tex`).
- Ajout de 6 sujets types sur le calcul matriciel dans `entrainement.tex`.
- Corrections de syntaxe (`\begin{theoreme}{Titre}`, `\begin{methode}[Titre]`
  mal utilisés à plusieurs endroits).

## 2026-08-09 — Grosse session de nettoyage et mise en page

- Ajout du chapitre Les Isométries du Plan.
- Ajout du chapitre Entrainement (sujets types + sujets bac étrangers).
- Amélioration de la mise en page : table des matières, boîtes sécables,
  entête renommé "Objectif Bac".
- Corrections diverses : doublons dans Arithmétique, titre du chapitre
  Intégrales, casse des titres (Complexes), fichiers vides supprimés.

## 2026-06-17 → 2026-07-14 — Structure initiale et premiers chapitres

- Structure initiale du projet (classe `book`, a5paper, style, packages,
  environnements tcolorbox).
- Chapitre Arithmétique (divisibilité, récurrence, division euclidienne)
  + premier sujet type Bac S 2022 dans `sujet_types.tex`.
- Chapitre Calcul matriciel (première version) et refonte du chapitre
  Complexes.
- Chapitres Logarithme/Exponentielle et Équations différentielles.

---

*Pour ajouter une entrée : décrire ce qui a été fait, pas comment (le
détail technique est dans les commits git). Une phrase par changement
notable suffit.*
