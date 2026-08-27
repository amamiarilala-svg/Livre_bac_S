# Journal de progression — Livre Bac S

Ce fichier retrace l'avancement du livre, du plus récent au plus ancien.
Une entrée = une session de travail ou un lot de changements cohérent.
Nouvelle entrée en haut, format : `## AAAA-MM-JJ — Titre court`.

---

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
