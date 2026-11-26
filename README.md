<p align="center">
  <a href="https://ag.tavardt.com/fr/">
    <img src="https://ag.tavardt.com/img/tavardt-banner.png" alt="TAVARDT" width="1024" />
  </a>
</p>

# Intelligence et Modélisation Mathématique du ROI en Acquisition Payante

[![Calculateur ROI](https://img.shields.io/badge/TAVARDT-Calculateur%20ROI-5b3cf5.svg)](https://tools.tavardt.com/fr/calculateur-roi-acquisition-payante/)
[![Python](https://img.shields.io/badge/Python-3.8%2B-blue.svg)](https://www.python.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

Moteur mathématique déterministe pour l'analyse du ROAS, du ROI et la projection de rendements décroissants lors de la mise à l'échelle des investissements publicitaires.

L'outil offre aux responsables de la performance, aux directeurs de croissance et aux analystes de données un cadre économétrique rigoureux pour simuler l'expansion budgétaire sans supposer des rendements linéaires illusoires. Conçu sans aucune dépendance externe, il s'exécute nativement en Python et JavaScript.

***

## Fondements Algorithmiques et Modélisation Mathématique

Projeter les investissements publicitaires de manière linéaire engendre des distorsions financières et de fausses estimations de rentabilité. Dans les enchères publicitaires réelles, l'augmentation des budgets entraîne une saturation des audiences, une lassitude créative et une hausse du coût marginal.

* **Calcul du ROAS Initial**: Rapport direct entre le chiffre d'affaires brut et les dépenses publicitaires (`revenue / spend`), mesurant l'efficacité brute.
* **Calcul du ROI Initial**: Rendement net en pourcentage sur le capital engagé (`((revenue - spend) / spend) * 100`), isolant la marge financière réelle.
* **Modélisation des Rendements Décroissants**: Application d'un exposant d'atténuation `(decay_factor - 1)` au ratio d'expansion budgétaire `(target_spend / current_spend)` pour anticiper la compression du ROAS.
* **Perte d'Efficacité Marginale**: Mesure de la réduction en pourcentage de l'efficacité résultant du passage à un palier budgétaire supérieur.
* **Architecture Double Isomorphe**: Formules mathématiques rigoureusement identiques implémentées dans la bibliothèque standard Python (`roi_engine.py`) et en JavaScript pur (`calculator.js`).

***

## Matrice des Métriques et Modélisation Mathématique

<table>
  <thead>
    <tr>
      <th align="left">Métrique / Paramètre</th>
      <th align="left">Formule Algorithmique</th>
      <th align="left">Comportement Mathématique</th>
      <th align="left">Utilité pour la Prise de Décision Stratégique</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><strong>ROAS Initial</strong></td>
      <td><code>revenue / spend</code></td>
      <td>Quotient linéaire direct arrondi à deux décimales.</td>
      <td>Mesure l'efficacité opérationnelle immédiate pour chaque euro investi.</td>
    </tr>
    <tr>
      <td><strong>ROI Initial</strong></td>
      <td><code>((revenue - spend) / spend) * 100</code></td>
      <td>Pourcentage de marge nette résultant des investissements engagés.</td>
      <td>Confirme la rentabilité financière nette après récupération complète du capital.</td>
    </tr>
    <tr>
      <td><strong>Ratio Budgétaire</strong></td>
      <td><code>target_spend / current_spend</code></td>
      <td>Multiplicateur d'expansion budgétaire lors des tests de croissance.</td>
      <td>Mesure la hausse relative du capital injecté dans les enchères publicitaires.</td>
    </tr>
    <tr>
      <td><strong>ROAS Projeté</strong></td>
      <td><code>current_roas * (spend_ratio ** (decay_factor - 1))</code></td>
      <td>Dégradation en loi de puissance causée par la saturation des audiences.</td>
      <td>Évite de surestimer les recettes prévisionnelles lors des phases d'accélération.</td>
    </tr>
    <tr>
      <td><strong>Revenus Projetés</strong></td>
      <td><code>target_spend * projected_roas</code></td>
      <td>Chiffre d'affaires brut anticipé sous la courbe des rendements décroissants.</td>
      <td>Vérifie si les revenus additionnels absorbent les coûts de structure induits.</td>
    </tr>
    <tr>
      <td><strong>Perte d'Efficacité</strong></td>
      <td><code>(1 - (projected_roas / current_roas)) * 100</code></td>
      <td>Contraction en pourcentage de l'efficacité brute lors de l'expansion.</td>
      <td>Quantifie précisément le sacrifice d'efficacité consenti pour conquérir du volume.</td>
    </tr>
  </tbody>
</table>

***

## Installation et Guide d'Exécution Rapide

Exécute nativement sous Python 3.8 ou supérieur en exploitant uniquement les bibliothèques standard (`sys`, `json`, `argparse`). Aucune installation externe via pip n'est requise.

Clonez le dépôt et lancez l'évaluation préliminaire dans le terminal:

```bash
git clone https://github.com/TAVARDT-France/ads-roi-intelligence-fr.git
cd ads-roi-intelligence-fr
python roi_engine.py -s 10000 -r 50000 -ts 25000
```

Pour générer un résultat structuré au format JSON:

```bash
python roi_engine.py -s 10000 -r 50000 -ts 25000 -j
```

Ajustez le coefficient d'atténuation pour les segments de marché très saturés:

```bash
python roi_engine.py -s 10000 -r 50000 -ts 30000 -d 0.78
```

Pour les environnements Node.js ou une intégration web côté client, utilisez `calculator.js`:

```javascript
const ROI_Calculator = require('./calculator.js');

const base = ROI_Calculator.calculateBaseMetrics(10000, 50000);
console.log('ROAS Initial:', base.roas, 'ROI Initial:', base.roi);

const projection = ROI_Calculator.projectScale(10000, 25000, base.roas, 0.85);
console.log('ROAS Projeté:', projection.projectedROAS);
console.log('Perte d'Efficacité:', projection.efficiencyLoss + '%');
```

Exemple de structure de données JSON produite:

```json
{
  "currency": "EUR",
  "current_spend": 10000.0,
  "current_revenue": 50000.0,
  "base_metrics": {
    "roas": 5.0,
    "roi": 400.0
  },
  "scaling_projection": {
    "target_spend": 25000.0,
    "decay_factor": 0.85,
    "projection": {
      "projected_roas": 4.36,
      "projected_revenue": 109000.0,
      "efficiency_loss": 12.8
    }
  }
}
```

***

## Foire Aux Questions (FAQ Technique)

### Comment le facteur d'atténuation modélise-t-il la baisse de rendement lors de l'expansion budgétaire?
Le facteur d'atténuation (`-d`, valeur par défaut 0.85) applique un exposant de puissance `(decay_factor - 1)` au ratio d'augmentation des dépenses. Lorsque le budget augmente, les impressions additionnelles se heurtent à la concurrence et à la saturation des segments cibles, comprimant le ROAS selon une courbe économétrique validée.

### Quelles différences opérationnelles distinguent le script Python du module JavaScript?
Les deux moteurs partagent scrupuleusement la même formulation mathématique et les mêmes règles d'arrondi. Le script Python (`roi_engine.py`) s'adresse aux exécutions en ligne de commande et aux tâches planifiées, tandis que `calculator.js` s'intègre directement dans les architectures Node.js et les interfaces web.

### Comment intégrer les résultats JSON dans des pipelines décisionnels et de BI?
En spécifiant le paramètre `-j`, le script transmet un flux JSON valide directement sur la sortie standard. Ce format peut être filtré par des utilitaires comme jq ou injecté sans transformation dans des plateformes analytiques comme BigQuery, Snowflake ou des entrepôts de données cloud.

### Pourquoi le moteur s'abstient-il de toute dépendance tierce et d'appel réseau?
L'absence de dépendances externes assure une exécution déterministe, protège le code contre les vulnérabilités de dépendances et garantit un calcul quasi instantané. Cela autorise son déploiement dans des environnements d'intégration continue sécurisés ou des conteneurs isolés.

### En quoi la métrique de perte d'efficacité prévient-elle les investissements déficitaires?
La perte d'efficacité marginale calcule le pourcentage de dégradation entre le ROAS d'origine et le ROAS anticipé. Si la diminution estimée fait passer la performance sous le seuil de rentabilité de l'organisation, les décideurs peuvent plafonner les budgets avant de déployer du capital à perte.

***

## Conseil en Ingénierie des Revenus

Pour l'optimisation des investissements médias, la modélisation économétrique et le passage à l'échelle en acquisition B2B en France, contactez les experts de **TAVARDT France**.

***

## Liens Utiles

* **Portail Corporatif:** https://ag.tavardt.com/fr/
* **Suite de Diagnostics:** https://tools.tavardt.com/fr/
* **Contact Technique:** https://ag.tavardt.com/fr/contact/

***

### Licence
Distribué sous la Licence MIT.

***

© 2026 TAVARDT. Tous droits réservés.
