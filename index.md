---
layout: default
title: "PMLSeg"
---

# PMLSeg

**PMLSeg** est un package **R** dédié à la **segmentation de séries temporelles univariées** à l’aide de la **vraisemblance pénalisée** (*Penalized Maximum Likelihood*).  
Il permet également de **valider les ruptures détectées** grâce à des métadonnées et de **visualiser les résultats** de manière intuitive.

Ce site présente le projet, ses fonctionnalités principales, ainsi que des exemples d’utilisation.

---

## 🎯 Objectifs du package

- Détecter des ruptures dans des séries temporelles univariées.  
- Utiliser des critères de vraisemblance pénalisée pour sélectionner le nombre optimal de segments.  
- Valider les ruptures détectées à l’aide de métadonnées externes.  
- Proposer des outils de visualisation pour interpréter les résultats.

---

## 📦 Fonctionnalités principales

- Segmentation automatique ou guidée.  
- Choix du nombre de segments (K) selon plusieurs stratégies.  
- Gestion de séries temporelles avec variabilité mensuelle.  
- Validation croisée avec métadonnées.  
- Visualisation des ruptures et des segments.

---

## 📘 Documentation & exemples

Le dépôt contient plusieurs ressources utiles :

- **README du package** : présentation générale et exemples rapides.  
- **Examples.md** : démonstrations d’utilisation du package.  
- **Use_cases/** : cas d’usage complets, dont :
  - *Use case #1 : séries journalières de différences IWV (GNSS – ERA5)*

---

## 🚀 Installation

Dans R :

```r
# Installation depuis GitHub
devtools::install_github("khanhninhnguyen/PMLSeg")
