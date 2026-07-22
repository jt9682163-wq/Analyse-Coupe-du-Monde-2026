# Analyse-Coupe-du-Monde-2026
# 🏆 Dashboard Power BI - Coupe du Monde 2026

Ce projet présente un **dashboard interactif Power BI** retraçant les moments forts de la Coupe du Monde 2026.  
Il illustre comment transformer des données sportives en **insights clairs et engageants** grâce à la data visualisation.


Table,ID,Nom,Continent,Date,Stade,Équipe_A,Équipe_B,Buts_A,Buts_B,Phase,Poste,Passes,Arrêts,Ville,Pays,Capacité
Équipe,1,Espagne,Europe,,,,,,,,,,,,,
Équipe,2,Argentine,Amérique du Sud,,,,,,,,,,,,,
Équipe,3,France,Europe,,,,,,,,,,,,,
Équipe,4,Angleterre,Europe,,,,,,,,,,,,,
Équipe,5,Brésil,Amérique du Sud,,,,,,,,,,,,,
Équipe,6,Sénégal,Afrique,,,,,,,,,,,,,
Équipe,7,Maroc,Afrique,,,,,,,,,,,,,
Équipe,8,Norvège,Europe,,,,,,,,,,,,,
Match,1,,,,2026-07-19,New York,Espagne,Argentine,1,0,Finale,,,,,,,,
Match,2,,,,2026-07-18,Miami,Angleterre,France,6,4,3e place,,,,,,,,
Match,3,,,,2026-07-10,Los Angeles,Brésil,Maroc,3,1,1/8e,,,,,,,,
Match,4,,,,2026-07-05,Mexico City,Sénégal,Norvège,2,2,Groupes,,,,,,,,
Joueur,1,Kylian Mbappé,France,,,,,,,,,,Attaquant,2,0,,,,,
Joueur,2,Rodri,Espagne,,,,,,,,,,Milieu,3,0,,,,,
Joueur,3,Michael Olise,France,,,,,,,,,,Milieu,7,0,,,,,
Joueur,4,Unai Simón,Espagne,,,,,,,,,,Gardien,0,25,,,,,
Joueur,5,Ferran Torres,Espagne,,,,,,,,,,Attaquant,1,0,,,,,
Joueur,6,Lionel Messi,Argentine,,,,,,,,,,Attaquant,2,0,,,,,
Stade,1,,,,,,,,,,,,,,,New York,USA,80000
Stade,2,,,,,,,,,,,,,,,Miami,USA,65000
Stade,3,,,,,,,,,,,,,,,Los Angeles,USA,75000
Stade,4,,,,,,,,,,,,,,,Mexico City,Mexique,90000


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
