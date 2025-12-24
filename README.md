# Project: Business Survival & Site Selection Analytics for San Diego County
### Predictive Modeling and Spatial Analysis Using Public Business Registry and Census Data

## Table of Contents
1. [Executive Summary](#Executive-Summary)
2. [Project Overview](#project-overview)
3. [Business Survival Predictive Model for San Diego County](#Business-Survival-Predictive-Model-for-San-Diego-County)
4. [Research Question & Hypotheses](#research-question--hypotheses)
5. [Context](#context)
6. [Data](#data)
7. [Limitations](#limitations)
8. [Delimitations](#delimitations)
9. [Data Gathering and Cleaning](#data-gathering-and-cleaning)
10. [Tools and Techniques](#tools-and-techniques)
11. [Project Outcomes](#project-outcomes)
12. [References](#references)

---

## Executive Summary 
<details>
<summary>Click to expand</summary>

**Project Focus:** Predictive Modeling & Spatial Intelligence for Investment, Development, and Site Selection in San Diego County.

This project delivers a validated, data-driven decision-support system for assessing business survival risk and location stability across San Diego County.

Using 146,000+ registered businesses, public census data, spatial analytics, and predictive modeling, the analysis identifies where businesses are more likely to survive or fail, and which factors most strongly influence longevity.

The results are designed to support:

* Site selection

* Real estate and housing development

* Infrastructure and healthcare facility planning

* Franchise and retail expansion

* Investment and lending risk assessment

The project is fully reproducible, well-documented, and includes an interactive executive dashboard suitable for non-technical stakeholders.

🔗 Interactive Dashboard (Tableau Public)
https://public.tableau.com/app/profile/kenier.ramirez6937/viz/SanDiegoCountyBusinessesAnalysis/MainDashboard?publish=yes

🔗 Source Code & Data
This GitHub repository

**This project uses only public data and does not involve human subjects research (IRB exempt).**


### Primary Users

* Real estate & housing developers

* Infrastructure & healthcare facility planners

* Franchise and retail expansion teams

* Investors, lenders, and site selection analysts


### Key Outputs

* Business survival probability scores across geography, industry, and business characteristics

* Closure and survival rates by ZIP code, city, NAICS sector, and ownership type

* Spatial risk maps and business clustering analysis

* Interactive executive dashboard (non-technical friendly)


### Business Use Cases

* Real Estate & Housing Development:
Identify ZIP codes and corridors with historically higher business survival to reduce vacancy and development risk.

* Healthcare & Infrastructure Planning:
Evaluate long-term economic stability and demand signals when selecting facility locations.

* Franchise & Retail Expansion:
Compare closure rates by industry and geography to optimize market entry decisions.

* Investment & Lending:
Assess geographic and sector-level exposure to business failure risk.

</details>

---

## Project Overview
<details>
<summary>Click to expand</summary>

**Project Topic:** Predicting Business Survival in San Diego County Using Public Business Registry Data.

This project applies statistical modeling, machine learning, and spatial analysis to evaluate survival outcomes of registered businesses in San Diego County. The study assesses the feasibility of building an accurate predictive model, identifies key predictors of longevity, and translates results into actionable insights for expansion, investment, and development decisions.

**IRB Status:** Exempt (no human subjects)

**Note:** This repository includes a complementary predictive modeling tool intended for entrepreneurs, analysts, and investors evaluating business expansion in San Diego County

</details>

---

## Business Survival Predictive Model for San Diego County  
<details>
<summary>Click to expand</summary>

**A Reproducible Decision-Support Tool**

### Required Files 
To run the model locally, the following files are required:
1. `best_survival_model.pkl`
2. `preprocessor.pkl`
3. `predict_business_survival.ipynb`
    * Files are Located under /Model

### Additional Resources
- **Project Report and Presentation:** Located under /Report
- **Interactive Dashboard (Tableau Public):**  
  https://public.tableau.com/app/profile/kenier.ramirez6937/viz/SanDiegoCountyBusinessesAnalysis/MainDashboard?publish=yes

> **This repository provides an open, validated predictive model for estimating business survival probability using public San Diego County data.**

</details>

---

## Research Question & Hypotheses
<details>
<summary>Click to expand</summary>

**Research Question:**  
Can a logistic regression–based predictive model be constructed using San Diego County business registry data?

**Hypotheses:**
- **Null Hypothesis (H₀):** A predictive logistic regression model cannot be constructed from the research dataset.
- **Alternate Hypothesis (H₁):** A predictive logistic regression model can be constructed from the research dataset with a model accuracy of 70% or higher.

</details>

---

## Context
<details>
<summary>Click to expand</summary>

Business survival is influenced by multiple factors, including geographic location, industry sector, firm age, ownership type, and local business clustering. Prior research (Reyes & Suárez, 2022) demonstrates that spatial and economic characteristics, such as proximity to major transportation routes and local business density, significantly influence firm longevity.

This project applies logistic regression, ensemble models, and spatial analytics to identify statistically significant predictors of survival and closure, supporting evidence-based development and investment decisions in San Diego County.

</details>

---

## Data
<details>
<summary>Click to expand</summary>

**Data Sources:**
- **Active/Inactive San Diego Registered Business Listings** (City of San Diego, n.d.)
- **2020 Census Population by ZIP Code** (SANDAG, n.d.)

**Integrated Dataset:**
- **Total Records:** 146,481 registered businesses
- **Time Span:** 1926 – November 3, 2025

Active and inactive listings were merged into a single dataset. ZIP codes were standardized and joined with population data. Latitude and longitude were validated using a San Diego County boundary shapefile.


**Key Variables:**

| Variable | Description / Purpose | Data Type | Type (IV/DV) |
|----------|----------------------|----------|---------------|
| account_status | Indicates if a business is active or inactive | Categorical | DV |
| date_business_start | Date when the business start operations | Continuous | IV |
| ownership_type | Type of ownership (e.g., sole proprietorship, corporation) | Categorical | IV |
| naics_sector | High-level NAICS code representing the industry sector | Categorical | IV |
| naics_description | Full textual description of the NAICS sector | Categorical | IV |
| naics_code | Detailed 2–6 digit NAICS code for the specific industry | Categorical | IV |
| address_city | City of the business location | Categorical | IV |
| address_state | State of the business location (San Diego, CA) | Categorical | IV |
| zip5 | ZIP code of the business location | Categorical | IV |
| lat | Latitude coordinate for geospatial mapping | Continuous | IV |
| lng | Longitude coordinate for geospatial mapping | Continuous | IV |
| population | Number of persons in that ZIP code | Continuous | IV |


**Derived Variables:**
- **Business age:** Years since business start operations.
- **Business group:** Categorized by business lifecycle stage.
- **Active/Closed Rate:** Proportion of active vs. closed businesses.
- **Business density:** Number of businesses per 1000 residents.

</details>

---

## Limitations
<details>
<summary>Click to expand</summary>

- Potential imprecision in geospatial coordinates.
- Only registered businesses included.
- Population data limited to 2020 Census.
- No financial or employment-level variables.

</details>

---

## Delimitations
<details>
<summary>Click to expand</summary>

- Focus exclusively on registered businesses within San Diego County.
- Variables selected specifically for predictive modeling relevance.
- Records in sectors 22 (“Utilities”) and 92 (“Public Administration”) are removed to ensure that the analysis remained focused on private-sector business activity.
- Outliers in `date_business_start` are retained as delimitations of the study to preserve potentially meaningful cases of long-standing businesses.

</details>

---

## Data Gathering and Cleaning
<details>
<summary>Click to expand</summary>

- Public CSV data compiled from City of San Diego and SANDAG.
- Data cleaning includes encoding categorical variables, imputing missing values where appropriate, and validating geospatial coordinates.
- Derived variables calculated for business age, life cycle group, active/closed rate, and business density.
- Data sparsity is less than 10%.

</details>

---

## Tools and Techniques
<details>
<summary>Click to expand</summary>

- **Programming Language:** Python
- **Statistical Tests:** Shapiro-Wilk, Levene (for assumption checking; not required for logistic regression)
- **Handling Imbalanced Classes:** SMOTE applied to training data
- **Modeling Approach:** Logistic Regression, Random Forest, Gradient Boosting, XGBoost, LightGBM
- **Evaluation:** Cross-validation, holdout test set (20%)
- **Interpretability:** SHAP analysis for feature importance
- **Clustering:** Unsupervised segmentation to uncover meaningful data patterns
- **Visualization:** Univariate and bivariate plots, tables, interactive dashboards

</details>

---

## Project Outcomes
<details>
<summary>Click to expand</summary>

**Key Results**

* Validated predictive survival model.

* Identification of strongest survival and closure drivers.

* Spatial clustering of high-risk and high-stability zones.


**Practical Impact**

* Entrepreneurs identify high-risk ventures earlier.

* Investors prioritize resilient locations and sectors.

* Developers assess long-term stability beyond surface metrics.

</details>

---

## References
<details>
<summary>Click to expand</summary>

- City of San Diego. (n.d.). *San Diego Business Listings*. City of San Diego Open Data Portal.  
- San Diego Association of Governments (SANDAG). (n.d.). *2020 Census Population by ZIP Code*. SANDAG Open Data Portal.  
- Reyes, J., & Suárez, L. (2022). *The impact of location and road class on firm survival*. Journal of Business Geography.  
- Society of Actuaries. (2019). *Standard practices in multivariate statistical and predictive modeling*.  
- Nemade, S., Bharadi, P., Alegavi, S., & Marakarkandy, B. (2023). *SMOTE in predictive modeling*.  
- Wang, H., & Guedes, R. (2024). *Logistic regression for SME failure prediction*.  
- García-Vidal, J., et al. (2025). *Determinants of business closure intention*.  
- Ramirez, K. (2025). *San Diego County Business Listing Dataset*.  

</details>
