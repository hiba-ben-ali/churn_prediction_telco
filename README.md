# Prédiction du churn client (Telco)

Projet de machine learning : prédire les clients d'un opérateur télécom qui risquent de résilier leur abonnement.

## Objectif
Identifier à l'avance les clients à risque pour pouvoir leur proposer une offre de rétention. Le critère principal est le **recall** : chaque client qui part sans avoir été détecté est une perte.

## Données
- Jeu de données *Telco Customer Churn* (IBM / Kaggle)
- 7 043 clients, 21 variables, environ 26 % de churn
- Fichier : `WA_Fn-UseC_-Telco-Customer-Churn.csv`

## Contenu du dépôt
- `churn_prediction_telco.ipynb` : notebook complet (nettoyage, analyse, modélisation, évaluation)
- `WA_Fn-UseC_-Telco-Customer-Churn.csv` : données

## Démarche
1. Nettoyage des données (`TotalCharges`, modalités « No internet service »)
2. Analyse exploratoire : le churn selon le contrat, l'ancienneté et les charges mensuelles
3. Préparation : encodage binaire et one-hot, séparation train/test 80/20 stratifiée
4. Modélisation : régression logistique et Random Forest
5. Évaluation : precision, recall, F1 et matrice de confusion
6. Optimisation du seuil de décision

## Résultats
| Modèle | Seuil | Precision | Recall | F1 |
|---|---|---|---|---|
| Random Forest | 0.5 | 61.2 % | 48.1 % | 53.9 % |
| Régression logistique | 0.5 | 63.6 % | 54.5 % | 58.7 % |
| **Régression logistique** | **0.3** | 52.3 % | **74.1 %** | **61.3 %** |

Avec le seuil par défaut (0.5), le modèle rate presque la moitié des clients qui partent. En abaissant le seuil à 0.3, le recall passe de 54.5 % à 74.1 %, et le F1 s'améliore aussi.

## Facteurs principaux du churn
D'après les coefficients de la régression logistique :
- **Réduisent le risque** : contrat de 2 ans, contrat de 1 an, absence de service internet
- **Augmentent le risque** : fibre optique, paiement par chèque électronique

## Limites
- Le seuil a été choisi en observant le jeu de test ; une validation croisée serait plus rigoureuse.
- Le seuil optimal dépend du coût d'une offre de rétention par rapport à celui d'un client perdu.

## Outils
Python, pandas, NumPy, matplotlib, seaborn, scikit-learn, Google Colab

## Auteur
[Ton nom]
