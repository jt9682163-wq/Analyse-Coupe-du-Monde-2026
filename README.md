# Analyse-Coupe-du-Monde-2026
# 🏆 Dashboard Power BI - Coupe du Monde 2026

Ce projet présente un **dashboard interactif Power BI** retraçant les moments forts de la Coupe du Monde 2026.  
Il illustre comment transformer des données sportives en **insights clairs et engageants** grâce à la data visualisation.

---

## 📊 Structure du Modèle

### Tables
- **Équipes**
  - ID_Équipe
  - Nom_Équipe
  - Continent

- **Matchs**
  - ID_Match
  - Date
  - Stade
  - Équipe_A
  - Équipe_B
  - Buts_A
  - Buts_B
  - Phase

- **Joueurs**
  - ID_Joueur
  - Nom
  - Équipe
  - Poste
  - Buts
  - Passes
  - Arrêts

- **Stades**
  - ID_Stade
  - Ville
  - Pays
  - Capacité

---

## 🔗 Relations
- `Équipes` (1) ↔ (N) `Matchs`
- `Équipes` (1) ↔ (N) `Joueurs`
- `Stades` (1) ↔ (N) `Matchs`

---

## 📈 Mesures DAX

```DAX
Total_Buts = SUM(Matchs[Buts_A]) + SUM(Matchs[Buts_B])

Moyenne_Buts = DIVIDE([Total_Buts], COUNTROWS(Matchs))

Meilleur_Buteur = CALCULATE(MAX(Joueurs[Buts]), Joueurs[Tournoi] = "Coupe du Monde 2026")

Meilleur_Passeur = CALCULATE(MAX(Joueurs[Passes]), Joueurs[Tournoi] = "Coupe du Monde 2026")

Taux_Victoire = DIVIDE(
    COUNTROWS(FILTER(Matchs, Matchs[Buts_A] > Matchs[Buts_B])),
    COUNTROWS(Matchs)
)
