# Drug_Consumption_Analysis

[![Python](https://img.shields.io/badge/Python-3.9-blue.svg)](https://python.org)
[![Pandas](https://img.shields.io/badge/Pandas-1.3-green.svg)](https://pandas.pydata.org)
[![Scikit-Learn](https://img.shields.io/badge/Scikit--Learn-1.0-orange.svg)](https://scikit-learn.org)
[![PowerBI](https://img.shields.io/badge/PowerBI-Dashboard-yellow.svg)](https://powerbi.microsoft.com)

## Project Overview

This project analyzes drug consumption patterns across **1,885 subjects** from the UCI Machine Learning Repository to identify personality-driven risk factors and build predictive models for targeted intervention programs.

**Business Problem:** Identify high-risk individuals based on personality traits and demographics to enable resource-efficient intervention programs.

**Success Metric:** Prediction accuracy for drug use classification with interpretable feature importance.

---

## Key Results

| Metric | Value |
|--------|-------|
| **Dataset Size** | 1,885 records × 32 features |
| **Models Trained** | Logistic Regression, Random Forest, SVM |
| **Best Accuracy** | **94.7%** (Random Forest) |

---

## Project Structure

```
drug-consumption-analysis/
├── data/
│   ├── drug_consumption_cleaned.csv          # Cleaned dataset with engineered features
│   ├── PowerBI_MASTER_FLAT.csv               # Flat table for quick PowerBI import
│   ├── PowerBI_DIM_PERSON.csv                # Dimension: demographics & personality
│   ├── PowerBI_DIM_DRUG.csv                  # Dimension: drug reference data
│   └── PowerBI_FACT_DRUG_CONSUMPTION.csv     # Fact: transaction-level drug use
├── notebooks/
│   └── 01_drug_consumption_analysis.ipynb    # Complete analysis workflow
├── models/
│   ├── best_model.pkl                        # Production-ready Random Forest
│   └── scaler.pkl                            # StandardScaler for inference
├── dashboards/
│   └── PowerBI_Dashboard_Layout.png          # Dashboard mockup & layout guide
├── assets/
│   ├── eda_visualizations.png                # 4-panel EDA overview
│   ├── eda_demographics.png                  # Demographic distributions
│   ├── eda_relationships.png                 # Feature relationships
│   ├── model_performance.png                 # ML comparison dashboard
│   ├── correlation_heatmap.png                 # Personality correlations
│   ├── drug_distribution.png                 # Drug use distribution
│   └── feature_importance.png                # Top predictive features
└── README.md                                   # This file
```

---

## Techniques Used

### 1. Data Engineering
- **Outlier Detection:** IQR method with Winsorization (1st/99th percentiles)
- **Feature Engineering:** Drug severity score, risk categories, binary user flags
- **Automation:** Reusable preprocessing pipeline function

### 2. Exploratory Data Analysis
- **17+ Visualizations:** Correlation heatmaps, distributions, boxplots, scatter plots
- **Behavioral Patterns:** Sensation Seeking vs drug use, age trends, gender analysis
- **Risk Segmentation:** Composite severity scoring with quartile-based categories

### 3. Machine Learning
- **Models:** Logistic Regression, Random Forest, SVM
- **Validation:** 5-fold stratified cross-validation
- **Tuning:** GridSearchCV hyperparameter optimization
- **Metrics:** Accuracy, Precision, Recall, F1-Score, AUC-ROC

### 4. Business Intelligence
- **Dashboard:** PowerBI with star schema architecture
- **Schema:** DIM_PERSON, DIM_DRUG, FACT_DRUG_CONSUMPTION
- **DAX Measures:** Custom KPIs for risk percentages and user rates
- **Interactivity:** Slicers, drill-through, cross-filtering

---

## Quick Start

### Prerequisites
```bash
pip install pandas numpy matplotlib seaborn scikit-learn
```

### Run Analysis
```bash
# Clone repository
git clone https://github.com/yourusername/drug-consumption-analysis.git
cd drug-consumption-analysis

# Launch Jupyter notebook
jupyter notebook notebooks/01_drug_consumption_analysis.ipynb
```

### Load Pre-trained Model
```python
import pickle

# Load model and scaler
with open('models/best_model.pkl', 'rb') as f:
    model = pickle.load(f)

with open('models/scaler.pkl', 'rb') as f:
    scaler = pickle.load(f)

# Make predictions on new data
# X_new_scaled = scaler.transform(X_new)
# predictions = model.predict(X_new_scaled)
```

---

## PowerBI Dashboard

The dashboard includes 4 interactive pages:

1. **Executive Summary** - 4 KPI cards + 4 main charts
2. **Demographic Analysis** - Heatmaps, distributions, country comparisons
3. **Drug Deep Dive** - Interactive slicers, trend analysis
4. **ML Predictions** - Model accuracy gauges, feature importance table

**Import Instructions:**
1. Open PowerBI Desktop
2. Get Data → Text/CSV → select `data/PowerBI_MASTER_FLAT.csv`
3. Create relationships using the star schema guide
4. Add DAX measures from the setup documentation

![Dashboard Preview](dashboards/PowerBI_Dashboard_Layout.png)

---

## Business Impact

### Risk Segmentation Strategy
- **Severe Risk (31.8%):** Immediate intervention priority
- **High Risk (66.4%):** Secondary intervention target
- **Resource Allocation:** Focus on cannabis/nicotine programs (94.7% usage)

### Personality-Driven Targeting
- **Low Agreeableness + High Sensation Seeking:** Highest risk profile
- **Age 18-24:** Highest consumption rates, early intervention opportunity
- **Gender:** Minimal variation, universal program applicability

---

## Visualizations

### EDA Overview
![EDA Visualizations](assets/eda_visualizations.png)

### Model Performance
![Model Performance](assets/model_performance.png)

### Feature Importance
![Feature Importance](assets/feature_importance.png)

---

## Contact

**Your Name** - Data Analyst
- LinkedIn: [your-linkedin-url]
- Email: your.email@example.com
- Portfolio: [your-portfolio-website]

**Project Link:** https://github.com/yourusername/drug-consumption-analysis
