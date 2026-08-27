# Livre Bac S — Mathématiques Terminale S

Manuel de mathématiques pour la classe de **Terminale S** / le **Baccalauréat
Série S** (MESUPRES, Madagascar), rédigé en LaTeX (classe `book`, format
`a5paper`).

Il couvre l'intégralité du programme officiel — Algèbre, Analyse, Géométrie,
Probabilités — complété par les **sujets officiels du Bacc Série S 2021–2026**
et un chapitre **Entrainement** (sujets types + sujets bac étrangers).

## État du projet

**Tous les chapitres sont alignés sur le modèle type** (cours illustré →
méthodes et exercices résolus → échauffement « lire une figure » + Vrai/Faux
→ exercices à difficulté progressive → ≥ 5 sujets types Bac au format
officiel). Le livre compile sans erreur ni débordement de marge
(`389 pages`).

- `STATUS.md` — photo de l'état courant (ce qui est fait, ce qui bloque).
- `PROGRESS.md` — journal de progression daté.

## Compilation

Pré-requis : une distribution TeX Live complète (`latexmk`, `pdflatex`,
packages `tcolorbox`, `tikz`, `newtx`, `fontawesome5`, `array`…).

```bash
latexmk -pdf main.tex
```

Le PDF est produit dans `main.pdf`. Nettoyage : `latexmk -c`.

## Structure du dépôt

| Dossier / fichier | Contenu |
|---|---|
| `main.tex` | point d'entrée : frontmatter, chapitres, annales, annexes |
| `config/` | `packages.tex`, `environnements.tex` (boîtes `definition`, `theoreme`, `methode`, `objectifs`, `citationchapitre`…), `commandes.tex` (`\Prob`, `\Esp`, `\dd`, `\facile`/`\moyen`/`\difficile`…), `style.tex` |
| `frontmatter/` | couverture, copyright, préface, mode d'emploi |
| `parties/algebre/` | Arithmétique, Calcul matriciel, Nombres complexes |
| `parties/analyse/` | Limites et continuité, Dérivabilité, Étude d'une fonction, Primitives et intégrale, Logarithme, Exponentielle, Suites numériques, Équations différentielles |
| `parties/geometrie/` | Barycentre, Isométries du plan, Géométrie dans l'espace |
| `parties/probabilites/` | Probabilités, Probabilités conditionnelles, Variables aléatoires, Loi binomiale, Lois continues et loi normale |
| `parties/annales/` | `bac_2021.tex` … `bac_2026.tex` (sujets officiels transcrits) |
| `sujet_types.tex` | charge les annales dans l'ordre chronologique |
| `entrainement.tex` | sujets types et sujets bac étrangers |
| `annexes/` | formulaire |

## Chapitres

### Algèbre
1. Arithmétique dans $\mathbb{Z}$
2. Calcul matriciel
3. L'ensemble des nombres complexes

### Analyse
4. Limites et continuité
5. Dérivabilité
6. Étude d'une fonction
7. Primitives et intégrale
8. Fonction logarithme népérien *(chapitre-référence resserré)*
9. Fonction exponentielle *(chapitre-référence resserré)*
10. Suites numériques
11. Équations différentielles

### Géométrie
12. Barycentre
13. Les Isométries du plan
14. Géométrie dans l'espace

### Probabilités
15. Probabilités
16. Probabilités conditionnelles
17. Variables aléatoires
18. Loi binomiale
19. Lois continues et loi normale

### Compléments
- Sujets officiels du Bacc Série S 2021 à 2026
- Entrainement : sujets types + sujets bac étrangers

> Les chapitres *Logarithme* et *Exponentielle* sont volontairement resserrés
> en chapitres-référence (définitions, propriétés, dérivées, batteries de
> calcul direct, Vrai/Faux) : les sujets types correspondants sont traités
> dans *Limites et continuité*, *Dérivabilité* et *Étude d'une fonction*.

## Workflow de contribution

Toute modification — y compris documentaire — passe par une **branche de
fonctionnalité + une pull request contre `main`** ; pas de commit direct sur
`main`. Après édition : `latexmk -pdf main.tex`, vérification du log (0 erreur,
pas de `Overfull \hbox` significatif), contrôle visuel des figures modifiées.
