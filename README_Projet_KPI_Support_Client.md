# Projet — Pilotage KPI d'un centre de support client

## Description 
Projet de pilotage de la performance d'un centre de support client multicanal (email, téléphone, chat, réseaux sociaux, portail web). À partir d'un dataset brut de ~14 000 lignes réparti sur 4 tables (tickets, agents, productivité, enquêtes de satisfaction), l'objectif est de nettoyer et structurer les données (Power Query), construire un pilotage KPI complet couvrant qualité, satisfaction client (CSAT/NPS), productivité des agents et respect des délais (SLA), automatiser le reporting (VBA) et livrer un dashboard interactif (Power BI).

## Contexte
Centre de support client multicanal (~6000 tickets/an, 40 agents, 5 équipes). Objectif : construire un pilotage complet couvrant **qualité, satisfaction, productivité et SLA**.

## Fichier
**`Support_Client_KPI_BRUT.xlsx`** — 4 onglets, ~14 000 lignes, volontairement sale (dates, doublons, typos, valeurs aberrantes, unités mélangées...).

| Onglet | Contenu |
|---|---|
| `Tickets_BRUT` | ~6100 tickets |
| `Agents_Referentiel` | 40 agents |
| `Productivite_BRUT` | Suivi journalier agent × jour |
| `Enquetes_Satisfaction_BRUT` | CSAT / NPS liés aux tickets |

## Étapes à faire

1. **Nettoyage Power Query** — harmoniser dates, agents, catégories, unités ; construire le modèle en étoile.
2. **Excel avancé** — TCD, formules complexes, feuille de synthèse.
3. **Automatisation VBA** — macros, boutons, formulaire.
4. **Power BI** — modèle, mesures DAX, dashboard multi-pages.

1. **Nettoyage Power Query**

Corrections appliquées lors du nettoyage
Agents : résolution de 100% des agents via une clé normalisée insensible à la casse, aux espaces et à l'inversion nom/prénom, avec rattrapage manuel des cas "prénom seul".
Dates (Date_Ouverture, Date, Date_Reponse) : parsing multi-format (ISO, JJ/MM/AAAA, JJ-MM-AA, US), dates invalides mises à vide.
Canal / Catégorie / Statut : harmonisation de casse et fusion des variantes vers des libellés officiels uniques.
Priorité : fusion des deux systèmes de codification (Basse–Critique et P1–P4) en 4 niveaux uniques.
Temps_Resolution : conversion minutes → heures pour les valeurs > 100 (seuil déterminé par analyse de distribution), valeurs sentinelles (9999) et négatives mises à vide.
Réouvertures : conversion des valeurs textuelles en nombre, négatifs mis à vide.
CSAT : restreint à l'échelle 1–5, hors échelle ou texte mis à vide.
NPS : restreint à l'échelle 0–10, hors échelle mis à vide.
ID_Ticket (table Enquêtes) : harmonisation de casse pour permettre le rapprochement avec la table Tickets.
Doublons : suppression des doublons stricts sur les 3 tables de faits (tickets, productivité, enquêtes).
