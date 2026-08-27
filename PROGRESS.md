# Journal de progression — Livre Bac S

Ce fichier retrace l'avancement du livre, du plus récent au plus ancien.
Une entrée = une session de travail ou un lot de changements cohérent.
Nouvelle entrée en haut, format : `## AAAA-MM-JJ — Titre court`.

---

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
  13 exercices gradués, dont 2 sujets types Bac.
- Compile sans erreur ; aucun `Overfull \hbox` visible (> ~10pt) ajouté.
- Branche `chapitre-isometries-composition`, PR contre `main`.

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
