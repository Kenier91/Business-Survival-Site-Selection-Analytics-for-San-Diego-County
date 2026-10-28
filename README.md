# Strategic Location and Survival Dynamics of Businesses in San Diego County
### A Comparative Machine Learning and Geospatial Approach

## Table of Contents
1. [Executive Summary](#executive-summary)
2. [Project Overview](#project-overview)
3. [Business Survival Predictive Model](#business-survival-predictive-model)
4. [Research Question & Hypotheses](#research-question--hypotheses)
5. [Context & Findings](#context--findings)
6. [Data](#data)
7. [Limitations & Delimitations](#limitations--delimitations)
8. [Tools and Techniques](#tools-and-techniques)
9. [Project Outcomes](#project-outcomes)
10. [References](#references)

---

## Executive Summary 
<details>
<summary>Click to expand</summary>

**Project Focus:** Predictive Modeling, Machine Learning & Spatial Intelligence for Investment, Development, and Site Selection in San Diego County.

This project delivers a validated, data-driven decision-support system for assessing business survival risk and location stability. By evaluating a merged open-data corpus of 158,330 registered businesses alongside public census and spatial data, this study contrasts traditional parametric modeling against advanced tree-based ensemble methods to identify key drivers of firm longevity.

The results are designed to support:
* Site selection and geographic expansion
* Real estate and housing development
* Infrastructure and healthcare facility planning
* Franchise and retail market entry
* Investment and lending risk assessment

The project is fully reproducible, well-documented, and includes an interactive executive dashboard suitable for non-technical stakeholders.

🔗 **Interactive Dashboard (Tableau Public):**
[San Diego County Businesses Analysis](https://public.tableau.com/app/profile/kenier.ramirez6937/viz/SanDiegoCountyBusinessesAnalysis/MainDashboard?publish=yes)

**This project uses only public open data and does not involve human subjects research (IRB exempt).**

### Key Outputs
* **Predictive Superiority:** A LightGBM model achieving 84.4% accuracy (F1-score = 0.779, ROC-AUC = 0.909).
* **SHAP Interpretability:** Granular feature importance revealing that structural attributes (firm age, legal structure) strictly outweigh raw spatial coordinates in predicting survival.
* **Geospatial & Unsupervised Analytics:** Unsupervised segmentation via K-Prototypes and spatial K-Means identifying latent regional business clusters.
* **Executive Dashboard:** Interactive spatial risk maps and business clustering visualizers.

</details>

---

## Project Overview
<details>
<summary>Click to expand</summary>

**Project Topic:** Strategic Location and Survival Dynamics of Businesses in San Diego County.

Despite the growing availability of municipal open data, municipal business registries remain underutilized for predictive decision support. Entrepreneurs frequently select expansion locations based on soft intuition or gross demographic metrics rather than non-linear risk modeling. 

This project applies statistical hypothesis testing, machine learning (Gradient Boosting, XGBoost, LightGBM, Random Forest, Logistic Regression), and geospatial analysis to evaluate survival outcomes of registered businesses in San Diego County. The study assesses the feasibility of building an accurate predictive model, decodes the "black box" of AI predictions using SHAP (SHapley Additive exPlanations), and translates complex geospatial market dynamics into actionable business intelligence.

</details>

---

## Business Survival Predictive Model 
<details>
<summary>Click to expand</summary>

**A Reproducible Decision-Support Tool**

### Required Files 
To run the model locally, the following files are required in your environment:
1. `best_survival_model.pkl` (Tuned LightGBM Model)
2. `preprocessor.pkl`
3. `predict_business_survival.ipynb`
    * *Files are located under the `/Model` directory.*

### Additional Resources
- **Project Report and Presentation:** Located under the `/Report` directory.
- **Interactive Dashboard:** Available via [Tableau Public](https://public.tableau.com/app/profile/kenier.ramirez6937/viz/SanDiegoCountyBusinessesAnalysis/MainDashboard?publish=yes).

> **This repository provides an open, validated machine learning pipeline for estimating business survival probability using public municipal and census data.**

</details>

---

## Research Question & Hypotheses
<details>
<summary>Click to expand</summary>

**Primary Research Question:**  
Can a predictive machine learning model be constructed on the San Diego County Business Listings dataset to reliably estimate business survival probability and identify structural risk factors?

To formally evaluate predictive feasibility against a parametric baseline, the study tested the following:

* **Null Hypothesis (H0):** A predictive parametric logistic regression model cannot be constructed from the research dataset at or above a benchmark performance threshold of an F1-Score of 0.70 (F1-Score < 0.70).
* **Alternative Hypothesis (H1):** A predictive parametric logistic regression model can be constructed from the research dataset achieving an F1-Score of 0.70 or higher (F1-Score ≥ 0.70).

**Resolution:** Standard Logistic Regression achieved an F1-score of only 0.576. We failed to reject the Null Hypothesis (H0). However, the study demonstrates that non-linear ensemble algorithms (specifically LightGBM) easily surpass this threshold (F1 = 0.779), proving that tree-based architectures are required for this highly imbalanced, complex spatial dataset.

</details>

---

## Context & Findings
<details>
<summary>Click to expand</summary>

Prior literature highlights that firm longevity is governed by a complex interaction between internal organizational attributes and external agglomeration economies (e.g., spatial clustering, market density). 

**Key Interpretive Insights (SHAP Analysis):**
1. **Dominance of Business Age:** Model explanations reveal that firm age is the primary factor driving survival predictions. Early-stage closure rates peak sharply in the 5-10 year lifecycle stage before dropping near zero for firms operating >20 years.
2. **Influence of Legal Ownership:** Sole proprietorships consistently reflect elevated failure risk compared to highly capitalized legal entities (Corporations, LLCs).
3. **Secondary Impact of Geography:** Raw spatial metrics (latitude, longitude, population) offer limited predictive contribution once age and ownership structure are accounted for. Location establishes foot traffic, but internal capital dictates resilience.

</details>

---

## Data
<details>
<summary>Click to expand</summary>

**Data Sources:**
- **City of San Diego Active and Inactive Business Listings** (Records from 1926 – Nov 2025)
- **SANDAG 2020 Census Population by ZIP Code**
- **US Census Bureau TIGER/Line Shapefiles (2022/2020)**

**Integrated Analytical Corpus:**
- **Total Validated Records:** 146,481 private-sector establishments.
- Bounding-box coordinate sanitization and spatial joins (GeoPandas) were applied to ensure geospatial accuracy.

**Key Features & Derived Variables:**
* `account_status` (Target Variable: Active vs. Closed)
* `business_age` & `age_segmentation` (Derived)
* `business_density` (Active businesses per 1,000 residents)
* `ownership_type` (Standardized categorical)
* `naics_sector` (Standardized into 18 primary economic sectors)
* `lat`, `lng`, `zip5`, `population`

</details>

---

## Limitations & Delimitations
<details>
<summary>Click to expand</summary>

### Limitations
- **Registry Truncation:** The dataset includes only formally registered businesses, excluding informal or unregistered micro-establishments.
- **Static Census Demographics:** Demographic features rely on static 2020 ZCTA Census baseline counts.
- **Coordinate Boundaries:** Spatial clustering via K-Means relies on mathematical centroids rather than official administrative neighborhood boundaries.

### Delimitations
- Focus is strictly on private enterprise; Public Administration (NAICS 92) and Utilities (NAICS 22) were intentionally excluded.
- Initial duplicate entries and "pending" status records were purged to maintain a strict binary classification scheme.

</details>

---

## Tools and Techniques
<details>
<summary>Click to expand</summary>

- **Core Stack:** Python (pandas, numpy, scikit-learn)
- **Geospatial Pipeline:** GeoPandas, Shapely, Folium, Branca
- **Statistical Testing:** Chi-Square tests of independence, Kruskal-Wallis H-tests, Variance Inflation Factor (VIF).
- **Data Balancing:** SMOTE (Synthetic Minority Over-sampling Technique) applied strictly to the training set.
- **Machine Learning Classifiers:** Logistic Regression, Random Forest, Gradient Boosting, XGBoost, LightGBM (Best Model).
- **Unsupervised Clustering:** K-Prototypes (for mixed data) and K-Means (for spatial coordinates).
- **AI Interpretability:** SHAP (SHapley Additive exPlanations) for global and local feature importance.

</details>

---

## Project Outcomes
<details>
<summary>Click to expand</summary>

**Empirical Results**
* **Model Validation:** Non-linear gradient boosting (LightGBM) effectively captures complex decision boundaries, achieving an 84.4% accuracy, 0.779 F1-score, and 0.909 ROC-AUC.
* **Risk Drivers:** Validated that internal organizational structure (age, legal formation) supersedes geographical location in determining ultimate firm survival.
* **Clustering:** Identified 4 distinct business archetypes (e.g., *Professional Micro-Startups* vs. *High-Density Corporate Hubs*) and 7 distinct geographic business clusters across the county.

**Strategic Action Plan for Stakeholders**
1. **Targeted Micro-Capital:** Support programs should focus heavily on Sole Proprietorships in years 1–5.
2. **Sector-Specific Assistance:** Tailor commercial lending and risk models around volatile sectors (Retail, Construction, Transportation).
3. **Data-Informed Expansion:** Guide retail expansion into high-density, high-population unsupervised clusters identified by the spatial models.

</details>

---

## References
<details>
<summary>Click to expand</summary>

1. City of San Diego. (n.d.). San Diego business listings dataset. City of San Diego Open Data Portal.
2. Ramirez, K. (2025). *San Diego County Active/Closed Business Listing* [Data set]. GitHub. https://github.com/Kenier91/Business-Survival-Site-Selection-Analytics-for-San-Diego-County/tree/main/Data
3. Reyes, J., & Suárez, L. (2022). *The impact of location and road class on firm survival*. Journal of Business Geography. 

</details>
