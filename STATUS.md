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
étrangers). Compile sans erreur avec `latexmk -pdf`.

## Chapitres — état

| Partie | État |
|---|---|
| Algèbre (arithmétique, matrices, complexes) | Terminé |
| Analyse (limites → équa diff) | Terminé |
| Géométrie (barycentre → espace) | Terminé |
| Probabilités (5 sous-chapitres) | Terminé |
| Sujets officiels Bacc Série S | 2021, 2022, 2023, 2024, 2025, 2026 transcrits. À compléter au fil des sessions envoyées par l'utilisateur (années manquantes : 2027+ à venir, années < 2021 non demandées pour l'instant). |
| Entrainement (sujets types) | 19 sujets types présents. |

## En attente / prochaine étape

- Aucun blocage actif en ce moment.
- Si l'utilisateur envoie un nouveau sujet officiel (PDF ou photos), il
  s'ajoute dans `parties/annales/bac_20XX.tex` + une ligne `\input` dans
  `sujet_types.tex`, à la bonne place chronologique.

## Points de vigilance (pour éviter de refaire les mêmes erreurs)

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
- **`\exercice` vs `\probleme`** : les sujets qui distinguent "Exercice"
  et "Problème" dans l'énoncé doivent utiliser la bonne macro (compteurs
  séparés, définis dans `config/environnements.tex`). Un sujet existant
  ne doit être retouché que si l'utilisateur le demande explicitement.
- **Nesting LaTeX + a5paper** : les formules longues (grands ensembles,
  inégalités à trois membres) dans un `enumerate` imbriqué à deux niveaux
  débordent facilement de la marge sur ce format de page. Réflexe :
  passer en affichage centré (`$$...$$`) ou couper en plusieurs lignes
  avec `aligned`, puis vérifier via `latexmk` qu'aucun `Overfull \hbox`
  significatif (> ~15pt) n'apparaît dans les fichiers touchés.
- **Workflow git** : toujours une branche de fonctionnalité + PR contre
  `main`, jamais de commit direct sur `main` (voir mémoire du projet).

---

*Pour mettre à jour : modifier les sections ci-dessus pour refléter la
réalité actuelle. Si un blocage apparaît (info manquante, ambiguïté à
trancher, décision à prendre avant de continuer), l'ajouter sous "En
attente / prochaine étape" avec assez de contexte pour reprendre sans
tout relire ; le retirer une fois résolu (et, si utile, en garder une
trace courte sous "Points de vigilance").*
