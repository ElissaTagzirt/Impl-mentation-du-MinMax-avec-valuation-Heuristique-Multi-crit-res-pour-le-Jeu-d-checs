# ♟️ TP MinMax – Jeu d'Échecs avec Évaluation Heuristique Avancée

Ce projet est une implémentation en langage **C** d’un moteur de jeu d’échecs simplifié. Il a été réalisé dans le cadre d’un TP du module **TPGO (Techniques de Programmation pour les Jeux et l’Optimisation)** à l’ESI.

Le moteur repose sur l’algorithme **MinMax avec élagage alpha-bêta**, utilisé pour explorer l’arbre des coups et choisir le meilleur mouvement. L'utilisateur joue les **Blancs (+)**, tandis que la machine joue les **Noirs (-)**.

---

## 🎯 Objectif du TP

L’objectif principal est d’**améliorer la fonction d’estimation `estim(...)`**, qui évalue la qualité d’une configuration d’échiquier. La version de base ne considérait que le matériel (comptage des pièces). Le but ici est d’implémenter une **évaluation positionnelle enrichie**, tenant compte de plusieurs critères stratégiques.

---

## 🧠 Fonction `estim(...)` : Évaluation multi-critères

La fonction `estim()` retourne une note dans l’intervalle **]-100, +100[**, représentant l’avantage des Blancs sur les Noirs.

### ✅ Critères utilisés dans l'évaluation :

| Critère analysé                  | Description                                                                 |
|----------------------------------|-----------------------------------------------------------------------------|
| **ScoreBrute**                   | Matériel total selon des poids personnalisés (pion=1, fou/cavalier=6...)   |
| **ScorePositions**              | Valeur des positions selon une matrice (bonus pour cases centrales)         |
| **ScoreCentre**                 | Contrôle du centre de l’échiquier (bonus pour pièces occupant les 4 cases centrales) |
| **ScoreConnectivity**           | Connectivité entre pièces alliées (proximité immédiate = meilleure défense) |
| **ScoreSecurity**               | Sécurité du roi (pénalité si des pièces ennemies sont proches)              |
| **ScoreColonnes**              | Bonus pour les colonnes ouvertes ou semi-ouvertes utilisées par les tours   |

---

## 🧮 Formule finale utilisée

La valeur retournée par la fonction est calculée par la formule suivante :

```c
ScrQte = (
    c_Brute * ScoreBrute +
    c_Positions * ScorePositions +
    c_Centre * ScoreCentre +
    c_Connectivity * ScoreConnectivity +
    c_Security * ScoreSecurity +
    c_Colonnes * ScoreColonnes
) / (c_Brute + c_Positions + c_Centre + c_Connectivity + c_Security + c_Colonnes);
