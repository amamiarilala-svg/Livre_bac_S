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
(`Overfull \hbox`) visibles de 27 à 10 occurrences uniques ; celles qui
restent sont soit purement internes (`Underfull`, sans effet visuel),
soit inférieures à ~11pt et vérifiées invisibles au rendu.

## Chapitres — état

| Partie | État |
|---|---|
| Algèbre (arithmétique, matrices, complexes) | Terminé. Chapitres Complexes, Arithmétique et Calcul matriciel alignés sur le modèle type le 2026-08-27 (matriciel : les 6 sujets types matrices ont quitté `entrainement.tex` pour le chapitre). |
| Analyse (limites → équa diff) | Terminé. **2026-08-27 :** fusion de « Limites » et de la partie Continuité de « Continuité et dérivabilité » en un chapitre unique `limites_continuite.tex` (exemples/exercices sur $\ln$/$\exp$, aligné modèle type, 5 sujets types Bac) ; l'ancien chapitre 5 devient « Dérivabilité » ; `fonctions.tex` recentré en « Étude d'une fonction » ; `logarithme.tex` et `exponentielle.tex` resserrés en chapitres-référence (def/propriétés/théorème/dérivée $\ln u$ et $\e^u$ + batteries de calcul direct en 2 colonnes ; section équa-diff retirée de `exponentielle.tex`, doublons FI/études renvoyés aux chapitres concernés). `limites.tex` et `continuite.tex` supprimés. |
| Géométrie (barycentre → espace) | Terminé. Chapitres Isométries, Barycentre et Géométrie dans l'espace (créé de zéro) alignés sur le modèle type le 2026-08-27. |
| Probabilités (5 sous-chapitres) | Terminé |
| Sujets officiels Bacc Série S | 2021, 2022, 2023, 2024, 2025, 2026 transcrits. À compléter au fil des sessions envoyées par l'utilisateur (années manquantes : 2027+ à venir, années < 2021 non demandées pour l'instant). |
| Entrainement (sujets types) | 19 sujets types présents. |

## En attente / prochaine étape

- Aucun blocage actif en ce moment.
- **Chantier en cours : aligner tous les chapitres sur le modèle type**
  (voir mémoires `feedback_chapter_template`, `reference_programme_officiel_ts`).
  Un chapitre à la fois, choisi par l'utilisateur au coup par coup.
  Exigences par chapitre : structure type (échauffement figure + Vrai/Faux +
  difficulté progressive), **≥ 5 sujets types Bacc**, couverture de tout le
  programme officiel en privilégiant les notions déjà vues aux annales.
  - Faits, avec 5+ sujets types Bacc chacun : Isométries, Barycentre,
    Complexes, Géométrie dans l'espace, Arithmétique, Calcul matriciel,
    **Limites et continuité**, **Dérivabilité**, **Étude d'une fonction**
    (ex-« Généralités sur les fonctions », recentré le 2026-08-27 sur :
    plan d'étude, diagramme des branches infinies, convexité, position
    courbe/droite, identification f/f'/f'' sur figure ; ln/exp uniquement ;
    5 sujets types Bac ; PR `chapitre-etude-fonctions`).
  - Restent : analyse (suites ; équa diff a déjà 2 sujets bac mais ni
    citation ni échauffement/V-F), probabilités (5 fichiers).
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
