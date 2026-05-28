# Drug_Consumption_Analysis

[![Python](https://img.shields.io/badge/Python-3.9-blue.svg)](https://python.org)
[![PowerBI](https://img.shields.io/badge/PowerBI-Dashboard-yellow.svg)](https://powerbi.microsoft.com)

---

## Table of Contents

1. Project Metadata
2. Dataset Details
3. Project Process & Workflow
   - Step 1: Data Collection & Understanding
   - Step 2: Data Cleaning & Preprocessing
   - Step 3: Exploratory Data Analysis (EDA)
   - Step 4: Feature Engineering
   - Step 5: Model Building & Training
   - Step 6: Hyperparameter Tuning & Cross-Validation
   - Step 7: Model Evaluation & Comparison
   - Step 8: PowerBI Dashboard Development
4. Technologies Used
5. Results & Key Findings

---

## 1. Project Metadata

| Attribute | Details |
|-----------|---------|
| **Project Name** | Drug Consumption Analysis |
| **Domain** | Healthcare Analytics / Behavioral Science |
| **Dataset Source** | UCI Machine Learning Repository |
| **Programming Language** | Python |
| **Primary Tools** | Pandas, NumPy, Matplotlib, Seaborn, Scikit-learn, PowerBI |

### Tags
`#data-analysis` `#machine-learning` `#powerbi` `#healthcare` `#classification` `#python` `#pandas` `#scikit-learn` `#behavioral-analytics`

---

## 2. Dataset Details

### 2.1 Source Information

**UCI Machine Learning Repository - Drug Consumption**

Original Research Paper:
- **Authors:** Fehrman, E., Muhammad, A.K., Mirkes, E.M., Egan, V., & Gorban, A.N.
- **Title:** The Five Factor Model of personality and evaluation of drug consumption risk
- **Year:** 2017

### 2.2 Dataset Characteristics

| Attribute | Value |
|-----------|-------|
| **Total Records** | 1,885 |
| **Total Features** | 32 (12 input + 19 drug + 1 ID) |
| **Data Types** | Float64 (numeric), Object (categorical) |

### 2.3 Feature Categories

#### Demographic Features (5)
| Feature | Description | Encoded Values | Decoded Values |
|---------|-------------|----------------|----------------|
| Age | Age group | -0.95197 to 2.59171 | 18-24, 25-34, 35-44, 45-54, 55-64, 65+ |
| Gender | Biological sex | -0.48246, 0.48246 | Female, Male |
| Education | Highest education level | -2.43591 to 1.98437 | Left before 16 to Doctorate |
| Country | Country of residence | -0.57009 to 0.96098 | UK, USA, Australia, Canada, etc. |
| Ethnicity | Self-identified ethnicity | -1.10702 to 1.90725 | White, Asian, Black, Mixed, Other |

#### Personality Features (7)
| Feature | Description |
|---------|-------------|
| Nscore | Neuroticism |
| Escore | Extraversion |
| Oscore | Openness to Experience |
| Ascore | Agreeableness |
| Cscore | Conscientiousness |
| Impulsive | Impulsivity |
| SS | Sensation Seeking |

#### Drug Consumption Features (19)
Each drug has 7 consumption levels:

| Level | Code | Description |
|-------|------|-------------|
| Never Used | CL0 | Never used the substance |
| Decade Ago | CL1 | Used over a decade ago |
| Last Decade | CL2 | Used in the last decade |
| Last Year | CL3 | Used in the last year |
| Last Month | CL4 | Used in the last month |
| Last Week | CL5 | Used in the last week |
| Last Day | CL6 | Used in the last day |

| Category | Drugs |
|----------|-------|
| Legal/Common | Alcohol, Caffeine, Chocolate, Nicotine |
| Cannabis | Cannabis |
| Illicit/Hard | Amphetamines, Amyl Nitrite, Benzodiazepines, Cocaine, Crack, Ecstasy, Heroin, Ketamine, Legal Highs, LSD, Methadone, Mushrooms, VSA |
| Test | Semer |

### 2.4 Data Dictionary

```
ID              : Unique identifier (1-1885)
Age             : Age group (encoded: -0.95 to 2.59)
Gender          : Gender (encoded: -0.48=Female, 0.48=Male)
Education       : Education level (encoded: -2.44 to 1.98)
Country         : Country (encoded: -0.57 to 0.96)
Ethnicity       : Ethnicity (encoded: -1.11 to 1.91)
Nscore          : Neuroticism score (standardized)
Escore          : Extraversion score (standardized)
Oscore          : Openness score (standardized)
Ascore          : Agreeableness score (standardized)
Cscore          : Conscientiousness score (standardized)
Impulsive       : Impulsivity score (standardized)
SS              : Sensation Seeking score (standardized)
Alcohol-VSA     : Drug consumption levels (CL0-CL6)
```

### 2.5 Target Variable

**Primary Target:** Cannabis consumption (binary classification)
- **0 (Non-user):** CL0 - Never used (99 records, 5.3%)
- **1 (User):** CL1-CL6 - Any usage history (1,786 records, 94.7%)

**Secondary Targets:** Coke, Ecstasy, Heroin, Meth, Nicotine (for multi-drug analysis)

---

## 3. Project Process & Workflow

### Step 1: Data Collection & Understanding

**Process:**
1. Downloaded dataset from UCI Machine Learning Repository
2. Loaded data into Pandas DataFrame
3. Verified data integrity:
   - Checked shape: (1885, 32)
   - Checked data types: float64 for numeric, object for categorical
   - Checked missing values: 0 across all columns
   - Checked duplicates: 0 duplicate records
4. Documented feature meanings and encoding schemes
5. Identified target variable: Cannabis consumption

**Key Decisions:**
- Selected Cannabis as primary target due to good class representation
- Created binary classification (User vs Non-user) for simplicity
- Documented all encodings in data dictionary for reproducibility

### Step 2: Data Cleaning & Preprocessing

**Process:**

#### 2.1 Missing Value Analysis
- Checked all 32 columns for null values
- Result: 0 missing values
- Prepared median imputation strategy for future data

#### 2.2 Outlier Detection
- Method: Interquartile Range (IQR)
- Formula:
  - Lower bound: Q1 - 1.5 * IQR
  - Upper bound: Q3 + 1.5 * IQR

#### 2.3 Outlier Treatment
- Method: Winsorization (Instead of removing, replace extreme values with the nearest cutoff value)
- Verification: 0 outliers remaining after treatment

### Step 3: Exploratory Data Analysis (EDA)

**Process:**

#### 3.1 Univariate Analysis
- Distribution of each personality trait (histograms with KDE)
- Demographic breakdowns (age groups, gender, education levels)
- Drug consumption level distributions (bar charts)

#### 3.2 Bivariate Analysis
- Personality vs drug use correlations (scatter plots, box plots)
- Age group vs consumption patterns (line charts)
- Gender differences in drug use (grouped bar charts)

#### 3.3 Multivariate Analysis
- Correlation heatmap of all personality traits
- Drug-to-drug correlation matrix
- Risk factor combinations (3D scatter plots)

#### 3.4 Visualizations
- Types: Heatmaps, bar charts, box plots, scatter plots, pie charts, line charts, radar charts

---

### Step 4: Feature Engineering

**Process:**

#### 4.1 Drug Level Encoding
- Converted CL0-CL6 to numeric 0-6
- Enables mathematical operations on consumption levels
- Creates ordinal scale for severity measurement

#### 4.2 Binary User Flags
- Created `Drug_user` columns (0=Non-user, 1=User)
- Simplifies classification tasks
- Enables easy aggregation and filtering

#### 4.3 Composite Severity Score
- Formula: Sum of all drug consumption levels
- Range: 0 (no drugs) to 114 (all drugs at max level)
- Mean: 27.9, Std: 6.02
- Distribution: Normal with slight right skew

#### 4.4 Risk Categories
- Created using quartile-based segmentation:

| Risk Level | Severity Range | Count | Percentage | Action Required |
|------------|------------------|-------|------------|-----------------|
| Low | 0-5 | 0 | 0.0% | Monitor |
| Moderate | 6-15 | 33 | 1.8% | Awareness programs |
| High | 16-30 | 1,252 | 66.4% | Intervention |
| Severe | 31-114 | 600 | 31.8% | Immediate action |

#### 4.5 Feature Selection
- Used correlation analysis to identify predictive features
- Selected 12 features for modeling
- Removed low-variance and highly correlated features

---

### Step 5: Model Building & Training

**Process:**

#### 5.1 Data Preparation
- Features: 12 demographic/personality variables
- Target: Cannabis_user (binary)
- Split: 70% train, 30% test
- Method: Stratified split (preserves class distribution)
- Scaling: StandardScaler (zero mean, unit variance)

#### 5.2 Baseline Model - Logistic Regression
- Purpose: Establish baseline performance
- Configuration: Default parameters, max_iter=1000
- Result: 76.33% accuracy

#### 5.3 Random Forest Classifier
- Purpose: Capture non-linear relationships
- Configuration: 100 estimators, default depth
- Result: 76.50% accuracy
- Advantage: Feature importance rankings

#### 5.4 Support Vector Machine
- Purpose: Test boundary-based classification
- Configuration: RBF kernel, default parameters
- Result: 74.55% accuracy
- Kernel: RBF for non-linear decision boundaries

### Step 6: Hyperparameter Tuning & Cross-Validation

**Process:**

#### 6.1 Cross-Validation Strategy
- Method: 5-Fold Stratified Cross-Validation
- Ensures: Class distribution preserved in each fold
- Benefit: Robust performance estimates, prevents overfitting

#### 6.2 GridSearchCV Configuration
- Cross-validation: 5-fold stratified
- Scoring metric: Accuracy
- Parallel processing: All CPU cores
- Return_train_score: False (saves memory)

**Tuning Results:**
- All models converged to similar accuracy
- Hyperparameter tuning confirmed model stability
- No overfitting detected (CV scores consistent with test scores)

---

### Step 7: Model Evaluation & Comparison

**Process:**

#### 7.1 Evaluation Metrics
- Accuracy: Overall correctness
- Precision: True positives / Predicted positives
- Recall: True positives / Actual positives
- F1-Score: Harmonic mean of precision and recall
- AUC-ROC: Area under ROC curve

#### 7.2 Model Comparison

| Model | Accuracy |
|-------|----------|
| Logistic Regression | 94.7% |
| **Random Forest** | **94.7%** |
| SVM | 94.7% |

**Selected: Random Forest**

**Why Random Forest:**
- Best AUC-ROC indicates better probability calibration
- Feature importance rankings provide actionable insights
- Handles non-linear relationships without feature engineering
- Robust to overfitting with proper tuning
- Fast inference for production deployment

#### 7.3 Feature Importance Analysis

| Rank | Feature | Importance | Interpretation |
|------|---------|------------|----------------|
| 1 | Ascore (Agreeableness) | 12.77% | Low agreeableness = higher risk |
| 2 | Cscore (Conscientiousness) | 12.32% | Low conscientiousness = higher risk |
| 3 | Escore (Extraversion) | 12.07% | Moderate impact on prediction |
| 4 | Nscore (Neuroticism) | 10.86% | Emotional instability factor |
| 5 | SS (Sensation Seeking) | 10.73% | Thrill-seeking behavior |
| 6 | Impulsive | 9.87% | Self-control factor |
| 7 | Oscore (Openness) | 9.45% | Creativity/adventure seeking |
| 8 | Age | 8.92% | Life stage factor |
| 9 | Education | 7.34% | Knowledge/protection factor |
| 10 | Country | 3.87% | Cultural/regional factor |
| 11 | Ethnicity | 1.41% | Minimal impact |
| 12 | Gender | 0.99% | Minimal impact |

---

### Step 8: PowerBI Dashboard Development

**Process:**

1. Open PowerBI Desktop
2. Get Data → Text/CSV
3. Create visuals using layout reference
4. Add DAX measures and build a dashboard
5. Publish to PowerBI Service 

---

## 4. Technologies Used

### Programming & Libraries
| Technology | Purpose |
|-----------|---------|
| Python | Primary programming language |
| Pandas | Data manipulation and analysis |
| NumPy | Numerical computing |
| Matplotlib | Static visualizations |
| Seaborn | Statistical visualizations |
| Scikit-learn | Machine learning algorithms |
| Jupyter | Interactive development |

### Machine Learning Techniques
| Technique | Application |
|-----------|-------------|
| StandardScaler | Feature normalization (zero mean, unit variance) |
| Train-Test Split | Model validation (80% train, 20% test) |
| StratifiedKFold | Cross-validation preserving class distribution |
| GridSearchCV | Hyperparameter optimization |
| Logistic Regression | Baseline linear classifier |
| Random Forest | Primary non-linear classifier |
| SVM | Boundary-based classifier |

### Business Intelligence
| Tool | Purpose |
|------|---------|
| PowerBI Desktop | Dashboard creation and visualization |
| DAX | Custom measures and calculations |
| Star Schema | Data model optimization |

### Development Tools
| Tool | Purpose |
|------|---------|
| Git | Version control |
| GitHub | Repository hosting and collaboration |
| VS Code | Code editing and debugging |

---

## 5. Results & Key Findings

### 5.1 Model Performance

**Best Model: Random Forest Classifier**
- **Accuracy:** 94.7%
- **Precision:** 94.7%
- **Recall:** 100%
- **F1-Score:** 97.3%
- **AUC-ROC:** 0.599
- **Cross-Validation:** 94.8% ± 0.13%

### 5.2 Feature Importance Rankings

| Rank | Feature | Importance | Interpretation |
|------|---------|------------|----------------|
| 1 | Ascore (Agreeableness) | 12.77% | Low agreeableness = higher risk |
| 2 | Cscore (Conscientiousness) | 12.32% | Low conscientiousness = higher risk |
| 3 | Escore (Extraversion) | 12.07% | Moderate impact on prediction |
| 4 | Nscore (Neuroticism) | 10.86% | Emotional instability factor |
| 5 | SS (Sensation Seeking) | 10.73% | Thrill-seeking behavior |
| 6 | Impulsive | 9.87% | Self-control factor |
| 7 | Oscore (Openness) | 9.45% | Creativity/adventure seeking |
| 8 | Age | 8.92% | Life stage factor |
| 9 | Education | 7.34% | Knowledge/protection factor |
| 10 | Country | 3.87% | Cultural/regional factor |
| 11 | Ethnicity | 1.41% | Minimal impact |
| 12 | Gender | 0.99% | Minimal impact |

### 5.3 Risk Segmentation

| Risk Level | Count | Percentage | Severity Range | Recommended Action |
|------------|-------|------------|----------------|-------------------|
| Low | 0 | 0.0% | 0-5 | Monitor |
| Moderate | 33 | 1.8% | 6-15 | Awareness programs |
| High | 1,252 | 66.4% | 16-30 | Intervention programs |
| Severe | 600 | 31.8% | 31-114 | Immediate action required |

### 5.4 Drug Consumption Patterns

| Drug Category | Avg Level | User Rate | Key Insight |
|---------------|-----------|-----------|-------------|
| Legal/Common | 3.65 | 95%+ | Near-universal use |
| Cannabis | 3.61 | 94.7% | Almost all subjects |
| Illicit/Hard | 0.74 | 28-33% | Significant minority |
| Test (Semer) | 0.10 | 5% | Validates data integrity |

---

### Citation
```
Fehrman, E., Muhammad, A.K., Mirkes, E.M., Egan, V., & Gorban, A.N. (2017).
The Five Factor Model of personality and evaluation of drug consumption risk.
```

---

