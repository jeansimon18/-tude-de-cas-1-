# Fonds Macro Global – Mémo interne

**À :** Analyste quantitatif junior  
**De :** Directeur de la stratégie quantitative  
**Date :** 5 septembre 2025  
**Objet :** Mandat de projet – Révision de notre modèle de risque de corrélation internationale

---

## 1. Problématique et mandat

Bonjour,  

Je vous confie un projet qui touche au cœur de notre cadre de gestion des risques. Comme vous le savez, la performance de notre fonds durant les récentes périodes de tensions sur les marchés — notamment le choc de la COVID-19 en 2020 et les turbulences inflationnistes de 2022 — a été considérablement entravée par l’échec de nos stratégies de diversification internationale.

Une analyse post-mortem a révélé que nos modèles de VaR (valeur à risque) ont été violés à un niveau sans précédent. Le principal responsable était une incompréhension fondamentale de la dynamique des corrélations : les avantages historiques de la détention d’actifs non corrélés ont disparu bien plus rapidement et complètement que nos modèles ne l’avaient prédit, nous exposant à un risque imprévu.

Notre examen préliminaire suggère que nos modèles existants reposent sur deux piliers trop simplistes :  
1. un modèle **autoregressif (AR)** de base pour la prévision à court terme, et  
2. un **modèle linéaire simple** reliant la corrélation à la peur du marché.  

Les deux se sont avérés inadéquats.

### Votre mandat
Mener une **analyse diagnostique complète** et proposer un **nouveau cadre plus robuste** pour la modélisation et la prévision de la dynamique des corrélations.

Vous sélectionnerez **un portefeuille de cinq indices boursiers internationaux**, comprenant :
- au moins **deux marchés développés** ;
- au moins **deux marchés émergents** ;
- le **cinquième marché** à votre discrétion.

Vous analyserez la **corrélation entre chacun de ces indices et le marché américain (S&P 500)**, pour développer une nouvelle vision interne du risque de corrélation.

Le livrable final sera un **rapport de recherche complet**, destiné au comité de risque.

---

## 2. Plan de recherche proposé

### 2.1. Caractérisation de la variable dépendante

1. Calculez la **corrélation mobile sur 6 mois (126 jours)** entre le S&P 500 et chacun des cinq indices internationaux, à partir de données quotidiennes (2010 à aujourd’hui).  
2. Testez la **stationnarité** des séries de corrélation à l’aide du test **Dickey-Fuller augmenté (ADF)**.  
3. Comparez les marchés développés et émergents :
   - Y a-t-il retour à une moyenne stable ?  
   - Ou persistance des chocs ?
4. Analysez visuellement et décrivez statistiquement vos séries avant de tirer des conclusions.

---

### 2.2. Évaluation du modèle de prévision existant

1. Construisez un **modèle autoregressif (AR(p))** pour chaque marché afin de prévoir la corrélation *one-step-ahead*.  
2. Testez les deux approches :  
   - corrélation **en niveaux** ;  
   - corrélation **en différences**.
3. Présentez les résultats :
   - coefficients et erreurs-types dans un **tableau professionnel** ;  
   - évaluez la précision hors échantillon avec la **RMSE** ;  
   - illustrez vos prévisions avec des **graphiques** et **intervalles de confiance à 95 %**.  
4. Discutez des limites du modèle (ex. hypothèse de normalité des résidus) et suggérez l’usage du **bootstrap** si nécessaire.  
5. Recommandez la meilleure approche (**niveaux vs différences**) pour chaque marché.

---

### 2.3. Développement d’un cadre explicatif plus riche

Les modèles AR sont peu explicatifs : il faut comprendre **ce qui influence la corrélation**.

#### Modèles à estimer

1. **Modèle linéaire existant :**
   \[
   Corr_t = β_0 + β_1 \log(VIX_t) + ε_t
   \]

2. **Modèle quadratique (hypothèse du “point de bascule”) :**
   \[
   Corr_t = β_0 + β_1 \log(VIX_t) + β_2 (\log(VIX_t))^2 + ε_t
   \]

#### Étapes :
- Estimez les deux modèles pour les cinq marchés.  
- Comparez les coefficients, erreurs-types et R².  
- Analysez la significativité du terme quadratique β₂ :
  - S’il est positif avec β₁ < 0, cela confirme une **relation convexe** (en U).  
- Calculez le **niveau du VIX au point de bascule** :  
  \[
  VIX^* = \exp\left(-\frac{β_1}{2β_2}\right)
  \]
- Discutez la signification économique pour la diversification.
- Présentez un **graphique comparatif** entre corrélation réelle et valeurs ajustées.

---

### 2.4. Synthèse : vers un modèle de pointe

Développez un **modèle ARX** combinant :
- les retards autoregressifs (de la section 2.2) ;
- les termes non linéaires du VIX (de la section 2.3).

⚠️ Utilisez uniquement des **valeurs retardées du VIX** pour conserver un cadre *prédictif* et non explicatif.

Comparez la **performance de prévision** du modèle ARX à celle des modèles AR simples.

---

### 2.5. Implications stratégiques pour la gestion du risque

Discutez des conséquences pratiques :

- Que se passe-t-il si nos **corrélations d’entrée sont erronées** dans les modèles de portefeuille moyenne-variance ?  
- Comment la **frontière efficiente** se déforme-t-elle si le monde réel suit une dynamique non linéaire ?  
- Quels effets sur :
  - les **modèles de VaR** ;  
  - les **estimations d’Expected Shortfall (ES)** ;  
  - la **gestion du capital à risque** ?  

Une sous-estimation de la corrélation en période de stress amplifie le risque de dépassements de VaR.

---

## 3. Le livrable final

Le rapport de recherche doit comporter :

### Structure :
1. **Introduction**
   - Contexte et objectif du projet.
2. **Données et méthodologie**
   - Description des indices, du calcul de corrélation, des tests de stationnarité, des critères de modèle, etc.
3. **Résultats empiriques**
   - Tableaux et graphiques clairs (stationnarité, performance, non-linéarité).
4. **Conclusion et recommandations**
   - Résumé des résultats et recommandations au comité de risque.

### Détails :
- Maximum **5 pages** (hors tableaux/figures/références)  
- **Simple interligne**, **Times New Roman 12 pts**, **marges de 1 pouce**
- Fournir séparément le **script/code Python** (ou équivalent)
- Le code n’est **pas noté**, mais les **justifications économiques et statistiques** le sont.
- Si vous ne pouvez pas coder une section, décrivez **comment** vous l’auriez fait.

---

> La clarté de votre raisonnement et la justification de vos choix économétriques seront **aussi importantes que vos résultats**.  
> J’ai hâte de lire votre rapport.

---
