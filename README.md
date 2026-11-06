# Boutique Diayma


## 1. Projets de la solution
- Un seul projet : `Diayma.csproj` (dossier P2FixAnAppDotNetCode)

## 2. Version du SDK .NET
- Framework cible du projet : netcoreapp2.0 (.NET Core 2.0)
- SDK installé : 2.1.818 (fixé avec global.json), en plus du SDK 10.0.403
- 
### Bug 1 : Le stock ne diminue pas après une commande
- Où:page d'accueil, colonne « Stock »
- Reproduction :ajouter un produit au panier, passer la commande et la terminer, puis revenir à l'accueil
- Résultat obtenu : le stock reste inchangé (ex. 20)
- Résultat attendu : le stock diminue de la quantité commandée

### Bug 2 : prix incohérents
- Où :toutes les pages
- Constat :les prix affichés en euros (ex. Galaxy A25 à 130 000,00 €) sont incohérents comment un galaxy A25 peut couter 130 000 euros 
- Résultat attendu : prix cohérents avec la devise
