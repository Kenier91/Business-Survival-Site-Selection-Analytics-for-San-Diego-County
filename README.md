# Strategic Location and Survival Dynamics of Businesses in San Diego County

### A Comparative Machine Learning and Geospatial Approach

**Author:** Kenier Ramirez, M.Sc. in Data Analytics  
**ORCID:** [0009-0001-9900-2473](https://orcid.org/0009-0001-9900-2473)

**Project Repository:** [GitHub – Business Survival and Site Selection Analytics for San Diego County](https://github.com/Kenier91/Business-Survival-Site-Selection-Analytics-for-San-Diego-County)

---

## Table of Contents

1. [Executive Summary](#executive-summary)
2. [Project Overview](#project-overview)
3. [Business Status Predictive Model](#business-status-predictive-model)
4. [Research Question and Hypotheses](#research-question-and-hypotheses)
5. [Data and Analytical Sample](#data-and-analytical-sample)
6. [Context and Key Findings](#context-and-key-findings)
7. [Limitations and Delimitations](#limitations-and-delimitations)
8. [Tools and Analytical Techniques](#tools-and-analytical-techniques)
9. [Repository Structure](#repository-structure)
10. [How to Download and Run the Predictive Model](#how-to-download-and-run-the-predictive-model)
11. [Project Outcomes](#project-outcomes)
12. [References](#references)

---

## 1. Executive Summary

<details>
<summary>Click to expand</summary>

This project presents a data-driven analytical framework for examining recorded business status and the structural, demographic, and spatial characteristics associated with business operations in San Diego County.

The research integrates municipal business registry records, census population data, and geographic information to evaluate statistical relationships, compare predictive machine-learning classifiers, interpret model predictions, and identify descriptive business and spatial clusters.

The project includes:

- A cleaned analytical dataset containing **140,737 business establishments**.
- A supervised-modeling dataset containing **137,814 observations** after excluding 2,923 records without valid geographic coordinates.
- Five predictive classification models.
- SHAP-based model interpretation.
- K-Prototypes and spatial K-Means clustering.
- An interactive dashboard and supplementary visualizations.
- A reproducible Python analysis notebook and serialized model artifacts.

### Key predictive results

LightGBM achieved the strongest overall performance on the unaltered holdout test set:

| Metric | LightGBM |
|---|---:|
| Accuracy | 0.835679 |
| Precision | 0.827757 |
| Recall | 0.760220 |
| F1-score | 0.792553 |
| ROC-AUC | 0.911295 |

The results indicate that tree-based ensemble classifiers performed better than the Logistic Regression baseline on this dataset.

**Important interpretation:** The model classifies recorded active versus closed/cancelled business status. It does not estimate time-to-event survival, closure dates, or an individual business's probability of surviving a specified number of future years.

</details>

---

## 2. Project Overview

<details>
<summary>Click to expand</summary>

Business registries contain useful information about business characteristics, industry classifications, ownership structures, and geographic distribution. However, these records are not always incorporated into predictive decision-support systems.

This project applies statistical analysis, machine learning, model interpretation, and geospatial analytics to examine recorded business status across San Diego County.

The study compares a Logistic Regression baseline against four tree-based ensemble classifiers:

- Random Forest
- Gradient Boosting
- XGBoost
- LightGBM

SHAP is used to examine the contribution of model features to predictions. Unsupervised clustering methods are used to describe business profiles and geographic concentrations.

Potential applications include:

- Commercial site assessment and geographic expansion.
- Retail and franchise market research.
- Real estate and development planning.
- Business support and economic development research.
- Investment and lending decision support.

The project is intended as an analytical decision-support resource, not as a substitute for professional financial, legal, or investment advice.

</details>

---

## 3. Business Status Predictive Model

<details>
<summary>Click to expand</summary>

### A reproducible machine-learning classification tool

The repository includes a prediction notebook and serialized model artifacts that allow users to execute predictions using the trained LightGBM model and its corresponding preprocessing pipeline.

### Required files

The following files are located in the `Model` folder:

| File | Purpose |
|---|---|
| `predict_business_survival.ipynb` | Notebook used to load the trained model, prepare prediction inputs, and execute predictions. |
| `best_survival_model.pkl` | Serialized trained LightGBM model. |
| `preprocessor.pkl` | Serialized preprocessing pipeline required to transform input features into the format expected by the model. |

**Important:** The model and preprocessor should be used together. The preprocessing pipeline must be applied to prediction inputs before they are passed to the trained model.

The notebook is the recommended starting point for users who want to execute new predictions.

</details>

---

## 4. Research Question and Hypotheses

<details>
<summary>Click to expand</summary>

### Primary research question

Can predictive machine-learning models constructed from the San Diego County business-listing data classify recorded business status and identify structural and geographic characteristics associated with that status?

### Prespecified Logistic Regression benchmark

The study established an F1-score benchmark of 0.70 for the Logistic Regression baseline.

- **Null Hypothesis (H0):** Logistic Regression does not attain an F1-score of 0.70.
- **Alternative Hypothesis (H1):** Logistic Regression attains an F1-score of at least 0.70.

Logistic Regression achieved an F1-score of **0.587087**, below the prespecified benchmark.

This is a benchmark-based model-performance criterion, not a conventional hypothesis test about a population parameter. The ensemble classifiers were compared using the same holdout test partition.

</details>

---

## 5. Data and Analytical Sample

<details>
<summary>Click to expand</summary>

### Data sources

The research integrates the following public data sources:

1. **City of San Diego Active and Inactive Business Listings:** Municipal business tax certificate records reported for 1926–2025.
2. **SANDAG 2020 Census Population by ZIP Code:** Demographic population baseline counts.
3. **U.S. Census Bureau TIGER/Line Shapefiles:** Geographic boundaries for San Diego County and ZIP Code Tabulation Areas.

### Dataset counts

The following counts are distinguished throughout the study:

| Dataset stage | Number of records |
|---|---:|
| Initial integrated business records | 158,330 |
| Final cleaned analytical dataset | 140,737 |
| Records excluded from supervised modeling due to invalid geographic coordinates | 2,923 |
| Supervised-modeling dataset | 137,814 |
| Training partition before SMOTE | 110,251 |
| Holdout test partition | 27,563 |
| Training partition after SMOTE | 139,996 |

The original cleaned dataset contains observed business records. It is not the SMOTE-balanced training dataset.

SMOTE was applied only to the training partition. The holdout test set was not oversampled.

### Principal analytical features

The research includes business age, age segmentation, ownership type, NAICS industry sector, geographic coordinates, ZIP/ZCTA information, population, and business density.

</details>

---

## 6. Context and Key Findings

<details>
<summary>Click to expand</summary>

### Predictive model comparison

Five classification models were evaluated using the same unaltered holdout test set.

| Model | Accuracy | Precision | Recall | F1-score | ROC-AUC |
|---|---:|---:|---:|---:|---:|
| LightGBM | 0.835679 | 0.827757 | 0.760220 | 0.792553 | 0.911295 |
| XGBoost | 0.834613 | 0.829190 | 0.754970 | 0.790341 | 0.908955 |
| Gradient Boosting | 0.834506 | 0.827840 | 0.756519 | 0.790574 | 0.904714 |
| Random Forest | 0.811549 | 0.789672 | 0.740942 | 0.764531 | 0.884499 |
| Logistic Regression | 0.661834 | 0.592019 | 0.582236 | 0.587087 | 0.683970 |

LightGBM achieved the highest accuracy, recall, F1-score, and ROC-AUC. XGBoost achieved the highest precision.

### SHAP interpretation

SHAP analysis identified business age as the strongest contributor to LightGBM predictions. Ownership indicators were also important, followed by selected business-density, geographic, and industry features.

SHAP values explain how features contribute to model predictions. They do not establish causal effects.

### Unsupervised clustering

The study applied:

- **K-Prototypes (k = 4):** Descriptive segmentation of business profiles using mixed numerical and categorical features.
- **Spatial K-Means (k = 7):** Geographic segmentation based on business coordinates.

These methods provide descriptive summaries of business characteristics and spatial concentrations. Cluster membership should not be interpreted as evidence that a particular location or business characteristic causes closure.

</details>

---

## 7. Limitations and Delimitations

<details>
<summary>Click to expand</summary>

### Limitations

- **Registry coverage:** The dataset represents businesses included in the municipal registry and may exclude informal or unregistered establishments.
- **Static demographic baseline:** Population features rely on 2020 ZIP/ZCTA population data and do not capture subsequent demographic changes.
- **Recorded status rather than event histories:** Active and closed/cancelled status records do not provide complete event timing for every establishment. The present study does not estimate time-to-event survival or hazard rates.
- **Geographic exclusions:** A total of 2,923 records without valid geographic coordinates were excluded from supervised modeling.
- **Spatial representation:** Spatial K-Means uses latitude and longitude coordinates and does not enforce administrative, zoning, or road-network boundaries.
- **Model generalizability:** Performance is evaluated on one holdout partition and may not generalize to other jurisdictions, time periods, or registry systems.
- **Observational interpretation:** Statistical associations and SHAP contributions do not establish causal relationships.

### Future research

A formal time-to-event survival analysis is a potential future extension. Such a study would require reliable opening dates, verified closure dates, censoring dates, and repeated business-status observations. Kaplan–Meier, log-rank, Cox proportional-hazards, or suitable parametric survival methods could then be considered.

</details>

---

## 8. Tools and Analytical Techniques

<details>
<summary>Click to expand</summary>

### Core technologies

- **Python:** Primary programming language.
- **Pandas and NumPy:** Data manipulation and numerical analysis.
- **Scikit-learn:** Machine-learning workflows and model evaluation.
- **GeoPandas and Shapely:** Geographic data processing and spatial joins.
- **XGBoost and LightGBM:** Gradient-boosting classification algorithms.
- **SHAP:** Model interpretability.
- **K-Prototypes:** Clustering of mixed numerical and categorical data.
- **K-Means:** Spatial clustering.

### Statistical and analytical procedures

The study includes chi-square tests of independence, normality diagnostics, Q–Q plots, Levene's test, Kruskal–Wallis tests, pairwise post-hoc comparisons, and Spearman rank correlation, as documented in the manuscript and analysis outputs.

SMOTE was applied exclusively to the training partition to address class imbalance.

</details>

---

## 9. Repository Structure

The repository is organized into folders containing the data, notebooks, trained model files, reports, and dashboard resources.

| Folder or file | Contents |
|---|---|
| `Data/` | Original cleaned analytical dataset and associated data resources. |
| `Dashboard/` | Interactive dashboard and supplementary visualizations. |
| `Model/` | Prediction notebook, trained LightGBM model, and preprocessing pipeline. |
| `notebooks/` | Statistical, exploratory, and spatial analysis notebook. |
| `Report/` | Supplementary PDF report and PowerPoint presentation containing additional graphs and analyses. |
| `README.md` | Project overview, repository guide, and execution instructions. |

### Principal repository files

- `Model/predict_business_survival.ipynb`
- `Model/best_survival_model.pkl`
- `Model/preprocessor.pkl`
- `notebooks/San_Diego_Business_Survival_Analysis.ipynb`
- `Report/Predictive Modeling and Spatial Analysis.pptx`
- `Report/Predictive Modeling and Spatial Analysis.pdf`

The original cleaned analytical dataset is available in the `Data` folder. It contains 140,737 observed establishments and should not be confused with the SMOTE-balanced training partition.

---

## 10. How to Download and Run the Predictive Model

The predictive model can be run directly in **Google Colab** without installing Python or additional packages on your computer.

### Step 1. Download the Required Files

Open the [GitHub repository](https://github.com/Kenier91/Business-Survival-Site-Selection-Analytics-for-San-Diego-County) and navigate to the `Model` folder.

Download these three files:

1. `predict_business_survival.ipynb`
2. `best_survival_model.pkl`
3. `preprocessor.pkl`

### Step 2. Open the Notebook in Google Colab

1. Visit [Google Colab](https://colab.research.google.com/).
2. Select **File → Upload notebook**.
3. Upload `predict_business_survival.ipynb`.

### Step 3. Upload the Model Files

In Google Colab, open the **Files** panel on the left and upload:

- `best_survival_model.pkl`
- `preprocessor.pkl`

### Step 4. Run the Notebook

Execute the notebook cells in order, or select **Runtime → Run all**.

The notebook will load the trained LightGBM model and its preprocessing pipeline and display an interactive prediction interface.

### Step 5. Enter Business Information

Complete the following fields:

- Business Age
- Population
- Latitude
- Longitude
- Business Density
- Ownership Type
- NAICS Sector
- City

Click **Predict** to generate the results.

### Understanding the Prediction

The notebook displays two model-estimated probabilities:

- **Failure:** Corresponds to the Closed/Cancelled classification.
- **Success:** Corresponds to the Active classification.

These results represent predicted recorded business-status classifications. They are not estimates of how many years a business will remain open or its probability of surviving a specific future period.

**Important:** Always use `best_survival_model.pkl` and `preprocessor.pkl` together. The model was developed using San Diego County business registry data, and applying it to other geographic areas requires additional validation.

---

## 11. Project Outcomes

<details>
<summary>Click to expand</summary>

The project provides an integrated analytical workflow combining statistical testing, supervised classification, model interpretation, and geospatial clustering.

The principal outcomes include:

1. A cleaned analytical dataset of 140,737 establishments.
2. A supervised classification workflow using five machine-learning algorithms.
3. A LightGBM model with a holdout ROC-AUC of 0.911295 and F1-score of 0.792553.
4. SHAP-based interpretation of the features contributing to model predictions.
5. Four K-Prototypes business-profile clusters.
6. Seven spatial K-Means clusters.
7. An interactive dashboard and supplementary analytical visualizations.
8. Reproducible notebooks and serialized model artifacts.

The project is intended to support further research and informed decision-making by providing an accessible analytical framework for examining business registry data.

</details>

---

## 12. References

1. City of San Diego. (n.d.). *San Diego business listings dataset*. City of San Diego Open Data Portal. https://data.sandiego.gov/datasets/business-listings

2. Ramirez, K. (2025). *San Diego County Active/Closed Business Listing* [Data set]. GitHub. https://github.com/Kenier91/Business-Survival-Site-Selection-Analytics-for-San-Diego-County/tree/main/Data

3. SANDAG. (n.d.). *2020 Census population by ZIP code dataset*. San Diego Association of Governments Open Data Portal. https://opendata.sandag.org/Census/2020-Census-Population-by-ZIP-Code/26f5-2x9a/about_data

4. U.S. Census Bureau. (n.d.). *TIGER/Line shapefiles*. https://www.census.gov/geographies/mapping-files/time-series/geo/tiger-line-file.html

---

**For research methodology, detailed statistical results, model evaluation, and interpretation, consult the accompanying preprint:**

*Strategic Location and Survival Dynamics of Businesses in San Diego County: A Comparative Machine Learning and Geospatial Approach.*



