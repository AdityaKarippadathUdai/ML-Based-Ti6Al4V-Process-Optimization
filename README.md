# 🧪 ML-Based Ti6Al4V Process Optimization

<p align="center">

![Python](https://img.shields.io/badge/Python-3.10%2B-3776AB?style=for-the-badge\&logo=python\&logoColor=white)![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-F37626?style=for-the-badge\&logo=jupyter\&logoColor=white)![Pandas](https://img.shields.io/badge/Pandas-Data%20Analysis-150458?style=for-the-badge\&logo=pandas\&logoColor=white)![NumPy](https://img.shields.io/badge/NumPy-Numerical%20Computing-013243?style=for-the-badge\&logo=numpy\&logoColor=white)
![Matplotlib](https://img.shields.io/badge/Matplotlib-Visualization-11557C?style=for-the-badge\&logo=matplotlib\&logoColor=white)![Material Science](https://img.shields.io/badge/Material-Science-8A2BE2?style=for-the-badge)![Machine Learning](https://img.shields.io/badge/Machine-Learning-FF6F00?style=for-the-badge)

</p>

<p align="center">
  <img src="https://img.shields.io/badge/Alloy-Ti--6Al--4V-1f6feb?style=flat-square" />
  <img src="https://img.shields.io/badge/Process-LPBF-0b7285?style=flat-square" />
  <img src="https://img.shields.io/badge/Analysis-EDA-success?style=flat-square" />
</p>

> 🧬 **Machine Learning Assisted Prediction and Optimization of Mechanical Properties for Laser Powder Bed Fusion of Ti6Al4V Alloy**

A data-driven research project focused on exploring and eventually developing machine-learning models for predicting and optimizing the mechanical properties of **Ti6Al4V alloy manufactured using Laser Powder Bed Fusion (LPBF)**.

---

## 🧭 Project Overview

Laser Powder Bed Fusion (LPBF) is an additive manufacturing process in which metallic powder is selectively melted layer by layer using a high-energy laser.

The final mechanical properties of an LPBF-produced component depend strongly on the selected processing parameters.

This project investigates the relationship between:

```text
LPBF Process Parameters
        │
        ▼
┌──────────────────────────┐
│   Laser / Powder Setup   │
│                          │
│ • Powder Size            │
│ • Laser Spot             │
│ • Laser Power            │
│ • Scanning Speed         │
│ • Hatch Distance         │
│ • Layer Thickness        │
└────────────┬─────────────┘
             │
             ▼
      Material Response
             │
             ▼
┌──────────────────────────┐
│ Mechanical Properties    │
│                          │
│ • UTS                    │
│ • Yield Strength         │
│ • Elongation             │
└──────────────────────────┘
```

The current notebook focuses primarily on **data exploration and statistical understanding of the dataset**, providing the foundation for subsequent machine-learning modeling and process optimization.

---

# 🎯 Objectives

The major objectives of this project are:

* 🔍 Explore the available Ti6Al4V LPBF experimental dataset.
* 🧹 Assess dataset quality and consistency.
* 📊 Understand the distribution of process parameters.
* 📈 Analyze the distribution of mechanical properties.
* 🧮 Calculate descriptive statistics.
* 🔎 Identify missing values and duplicate observations.
* 🧩 Investigate reference/source groups within the dataset.
* ⚠️ Identify potential identifier columns and avoid accidental data leakage.
* 📉 Detect potential outliers and unusual observations.
* 🔗 Study relationships between LPBF parameters and mechanical properties.
* 🤖 Prepare the dataset for machine-learning models.
* ⚙️ Eventually identify process-parameter combinations associated with desired mechanical properties.

---

# 🧪 Material and Manufacturing Process

## Ti6Al4V

The material investigated in this project is **Ti6Al4V**, a titanium alloy widely used in applications where high strength-to-weight ratio, corrosion resistance, and mechanical performance are important.

Typical application areas include:

* ✈️ Aerospace
* 🚀 Space systems
* 🦴 Biomedical implants
* 🏎️ High-performance engineering
* ⚙️ Advanced manufacturing

---

## 🔥 Laser Powder Bed Fusion

LPBF builds components by selectively melting metallic powder using a laser.

A simplified process can be represented as:

```text
Metal Powder
     │
     ▼
 ┌─────────┐
 │ Powder  │
 │ Layer   │
 └────┬────┘
      │
      ▼
 ┌─────────┐
 │  Laser  │
 │ Scanning│
 └────┬────┘
      │
      ▼
 Melt Pool Formation
      │
      ▼
 Solidified Layer
      │
      ▼
 Next Powder Layer
      │
      ▼
 Final Ti6Al4V Part
```

Changes in laser power, scanning speed, hatch distance, layer thickness, and other parameters can influence melt-pool behavior and therefore the resulting mechanical properties.

---

# 📂 Dataset

The project uses the Excel dataset:

```text
1-s2.0-S2214860424003877-mmc1.xlsx
```

The dataset contains experimental observations related to **Ti6Al4V manufactured using LPBF**.

The notebook loads the dataset using:

```python
pd.read_excel()
```

Example:

```python
FILE_PATH = "/content/1-s2.0-S2214860424003877-mmc1.xlsx"

df = pd.read_excel(FILE_PATH)
```

> 📌 **Important:** The dataset file must be available at the path specified by `FILE_PATH`, or the path should be modified according to the local environment.

---

# 🧱 Dataset Variables

The current analysis separates variables into three major groups.

## ⚙️ Process Parameters

The following parameters are treated as manufacturing/process features:

| Parameter       | Unit | Description                              |
| --------------- | ---: | ---------------------------------------- |
| Powder Size     |   μm | Particle/powder size                     |
| Laser Spot      |   μm | Laser spot size                          |
| Laser Power     |    W | Laser energy input parameter             |
| Scanning Speed  | mm/s | Speed at which the laser scans           |
| Hatch Distance  |   μm | Distance between adjacent scan tracks    |
| Layer Thickness |   μm | Thickness of each deposited powder layer |

These variables represent the primary LPBF processing conditions investigated by the project.

---

## 📐 Geometry Variables

The dataset also contains specimen geometry information:

| Variable     | Unit |
| ------------ | ---: |
| Gauge Area   |  mm² |
| Gauge Length |   mm |

These variables describe characteristics of the mechanical-test specimen.

They should be handled carefully during machine-learning modeling because their relevance depends on the specific prediction task and experimental design.

---

## 💪 Mechanical Property Targets

The primary target variables are:

| Property | Unit | Meaning                   |
| -------- | ---: | ------------------------- |
| UTS      |  MPa | Ultimate Tensile Strength |
| YS       |  MPa | Yield Strength            |
| EF       |    % | Elongation at Fracture    |

The machine-learning stage can eventually investigate these properties individually or through a multi-output prediction framework.

---

# 🔎 Current Notebook — Exploratory Data Analysis

The current Jupyter notebook performs the initial **Exploratory Data Analysis (EDA)**.

The analysis includes:

### 1. 📦 Library Import

The notebook imports:

* NumPy
* Pandas
* Matplotlib

These libraries provide the basic functionality required for numerical analysis, data manipulation, and visualization.

---

### 2. 📥 Dataset Loading

The Excel dataset is loaded into a Pandas DataFrame.

The notebook also reports:

* Number of rows
* Number of columns
* Dataset shape

---

### 3. 👀 Dataset Inspection

The notebook displays:

* First rows
* Last rows
* Dataset information
* Column names
* Data types

This provides an initial understanding of the dataset structure.

---

### 4. 🕳️ Missing-Value Analysis

The notebook checks for missing values using:

```python
df.isnull().sum()
```

It also calculates the percentage of missing values for every column.

This helps determine whether preprocessing or imputation will be required before machine-learning modeling.

---

### 5. ♻️ Duplicate Analysis

Duplicate rows are identified using:

```python
df.duplicated().sum()
```

Duplicate observations can potentially affect statistical analysis and model training, so they need to be investigated before preprocessing.

---

### 6. 🔢 Unique-Value Analysis

The notebook calculates the number of unique values in each column.

This is particularly useful for identifying:

* Continuous variables
* Categorical variables
* Identifiers
* Potentially constant columns

---

# ⚠️ Alloy Identifier Investigation

One important part of the current notebook is the investigation of the `Alloy` column.

The notebook checks:

```python
df["Alloy"].nunique()
```

and compares the number of unique values with the number of rows.

If every row has a unique `Alloy` value, the column may represent an **identifier rather than a meaningful predictive feature**.

This is important because including an identifier in a machine-learning model can introduce misleading patterns or data leakage.

> ⚠️ The column should not automatically be used as a feature simply because it is numeric. Its experimental meaning must first be established.

---

# 📚 Reference Analysis

The dataset contains a `Reference` column that can be used to investigate the source of experimental observations.

The notebook calculates:

```python
df["Reference"].nunique()
```

and determines the number of samples associated with each reference.

This allows the dataset to be examined in terms of experimental source distribution.

---

## 📊 Samples per Reference

A histogram is generated to visualize how many observations belong to each reference.

This is useful because datasets assembled from multiple studies may contain differences in:

* Experimental setup
* Material conditions
* Machine configuration
* Measurement methodology
* Specimen geometry
* Processing parameters

These differences should be considered when designing the machine-learning validation strategy.

---

# 📊 Statistical Analysis

The notebook calculates descriptive statistics for numerical variables.

These include:

* Count
* Mean
* Standard deviation
* Minimum
* Maximum
* Median
* Variance
* Skewness

Additional quantiles are calculated at:

```text
1%
5%
25%
50%
75%
95%
99%
```

This provides a more complete understanding of the spread and shape of the numerical variables.

---

# 📈 Data Visualization

The notebook generates several types of visualizations.

## Process Parameter Distributions

Histograms are generated for:

* Powder Size
* Laser Spot
* Laser Power
* Scanning Speed
* Hatch Distance
* Layer Thickness

These plots help identify:

* Central tendency
* Spread
* Skewness
* Potential multimodal distributions
* Extreme observations

---

## Mechanical Property Distributions

Histograms are generated for:

* UTS
* YS
* EF

These visualizations provide an initial understanding of the response variables that the future ML models will predict.

---

## 📦 Boxplots

Boxplots are generated for both process parameters and mechanical properties.

They can help identify:

* Potential outliers
* Interquartile ranges
* Median values
* Distribution spread

However, an observation appearing as an outlier does **not automatically mean that it is an error**.

In experimental materials-science datasets, extreme observations may represent legitimate processing conditions or material behavior.

---
---

# 🤖 Machine Learning Modeling

Following the exploratory data analysis, machine-learning regression models were developed to investigate the relationship between the LPBF input parameters and the resulting mechanical properties of Ti6Al4V.

The eight input variables used for prediction are:

```text
Powder Size
Laser Spot
Laser Power
Scanning Speed
Hatch Distance
Layer Thickness
Gauge Area
Gauge Length
```

The three prediction targets are:

```text
UTS (MPa)
YS (MPa)
EF (%)
```

The dataset contains **173 experimental observations**.

The current modeling stage uses an **80/20 train-test split** with a fixed random state to provide a reproducible baseline comparison.

```text
173 Samples
     │
     ▼
┌─────────────────────┐
│ 8 Input Features    │
└──────────┬──────────┘
           │
           ▼
     Train / Test Split
           │
      ┌────┴────┐
      ▼         ▼
   80% Train  20% Test
      │         │
      ▼         ▼
   ML Models  Evaluation
```

---

# 🧠 Regression Models

Four regression algorithms are currently implemented.

### 1. Gaussian Process Regression (GPR)

Gaussian Process Regression is a non-parametric regression method capable of modeling nonlinear relationships.

In this project, feature standardization is applied before GPR.

GPR is used to predict:

```text
Process Parameters ─────► UTS
Process Parameters ─────► YS
Process Parameters ─────► EF
```

---

### 2. Support Vector Regression (SVR)

Support Vector Regression is used to model nonlinear relationships between LPBF parameters and mechanical properties.

An RBF kernel is used for the current implementation.

The model uses standardized input features.

---

### 3. Random Forest Regression

Random Forest Regression combines multiple decision trees to model nonlinear relationships between the input parameters and mechanical properties.

The current implementation uses:

```text
Number of trees : 300
Random state    : 42
```

Random Forest is particularly useful for examining nonlinear feature relationships and provides feature-importance estimates.

---

### 4. XGBoost Regression

XGBoost is included as an additional machine-learning benchmark.

The current implementation uses gradient-boosted decision trees with parameters including:

```text
n_estimators      = 300
max_depth         = 6
learning_rate     = 0.05
subsample         = 0.8
colsample_bytree  = 0.8
```

XGBoost is not one of the three regression algorithms specifically described in the paper's CIRM methodology; it is included here as an additional model for comparison.

---

# 📊 Model Evaluation

The models are evaluated using three regression metrics.

## R² — Coefficient of Determination

R² measures the proportion of variation in the target variable explained by the model.

Higher values indicate that the model explains more of the observed variation on the evaluation data.

---

## RMSE — Root Mean Squared Error

RMSE measures the magnitude of prediction errors while giving greater weight to larger errors.

```text
RMSE = √(mean((y_actual - y_predicted)²))
```

Lower values indicate smaller prediction errors.

---

## MAE — Mean Absolute Error

MAE measures the average absolute difference between actual and predicted values.

```text
MAE = mean(|y_actual - y_predicted|)
```

Lower values indicate smaller average prediction errors.

---

# 📈 Current Model Results

Using the current 80/20 train-test split, the Random Forest model produced the following R² values:

| Target | Model         |     R² |
| ------ | ------------- | -----: |
| UTS    | Random Forest | 0.7172 |
| YS     | Random Forest | 0.6473 |
| EF     | Random Forest | 0.5653 |

These values represent the current baseline results obtained from the implemented train-test split.

The complete comparison includes:

```text
                 ┌─────────────┐
                 │     GPR     │
                 └──────┬──────┘
                        │
                 ┌──────▼──────┐
                 │     SVR     │
                 └──────┬──────┘
                        │
                 ┌──────▼──────┐
                 │ Random Forest│
                 └──────┬──────┘
                        │
                 ┌──────▼──────┐
                 │   XGBoost   │
                 └──────┬──────┘
                        │
                        ▼
               Model Comparison
                        │
             ┌──────────┼──────────┐
             ▼          ▼          ▼
            UTS        YS          EF
```

The notebook generates comparison tables and plots for R², RMSE, and MAE.

---

# 📊 R² Model Comparison

A grouped bar chart is generated to compare the R² values obtained by:

* GPR
* SVR
* Random Forest
* XGBoost

for:

* UTS
* YS
* EF

This provides a direct visual comparison of model performance across the three mechanical properties.

---

# 📉 RMSE and MAE Comparison

RMSE and MAE plots are also generated to examine prediction error.

The models are therefore evaluated from multiple perspectives rather than using R² alone.

```text
                  Model Evaluation
                         │
          ┌──────────────┼──────────────┐
          ▼              ▼              ▼
         R²             RMSE           MAE
          │              │              │
          ▼              ▼              ▼
      Explained       Prediction      Average
      variance          error          error
```

---

# 🎯 Actual vs Predicted Analysis

Actual-versus-predicted plots are generated for each model and target.

The plots compare:

```text
Actual Experimental Value
          │
          │
          │       •
          │    •
          │  •
          │ •
          └──────────────────►
             Predicted Value
```

A reference diagonal line represents:

```text
Predicted = Actual
```

Points closer to this line indicate smaller prediction differences.

Separate plots are generated for:

```text
GPR
 ├── UTS
 ├── YS
 └── EF

SVR
 ├── UTS
 ├── YS
 └── EF

Random Forest
 ├── UTS
 ├── YS
 └── EF

XGBoost
 ├── UTS
 ├── YS
 └── EF
```

---

# 🔬 XGBoost Feature Importance

XGBoost feature importance is also calculated to investigate the relative contribution of the eight input variables to the predictions.

The analysis considers:

```text
Powder Size
Laser Spot
Laser Power
Scanning Speed
Hatch Distance
Layer Thickness
Gauge Area
Gauge Length
```

Feature-importance plots are generated separately for:

* UTS
* YS
* EF

These plots provide an initial model-based interpretation of which input variables contribute most strongly to the predictions.

Feature importance should not automatically be interpreted as a causal physical relationship. Further analysis is required to distinguish predictive association from physical causation.

## 🧩 GMM-Based Clustering and Modeling

To investigate whether a probabilistic clustering approach could better represent the heterogeneous LPBF processing conditions, a **Gaussian Mixture Model (GMM)** was introduced as an alternative to the K-Means clustering used in the original research methodology.

### Gaussian Mixture Model

GMM is a probabilistic clustering method that represents the dataset as a mixture of Gaussian distributions. Unlike K-Means, which assigns each sample to a single cluster based primarily on distance to a cluster centroid, GMM estimates the probability that each sample belongs to each cluster.

For this project, the eight LPBF input parameters were standardized before applying GMM.

**Number of clusters:**

```text
k = 3
```

The three-cluster configuration was selected to provide a direct comparison with the clustering structure used in the reference study.

### GMM Workflow

```text
Ti6Al4V Dataset
      │
      ▼
Feature Selection
      │
      ▼
Standardization
      │
      ▼
Gaussian Mixture Model
      │
      ├── Cluster 0
      ├── Cluster 1
      └── Cluster 2
      │
      ▼
Cluster-Specific Models
      │
      ├── GPR
      ├── SVR
      └── Random Forest
      │
      ▼
Predictions
      │
      ▼
Performance Evaluation
      │
      ├── R²
      ├── RMSE
      └── MAE
```

### Why GMM Was Investigated

GMM was tested because LPBF process data may contain overlapping groups of processing conditions. GMM can represent clusters using their estimated means and covariance structures and provides **soft cluster assignments** through membership probabilities.

This makes it possible to investigate whether probabilistic clustering can improve the prediction of mechanical properties compared with:

1. Global regression models without clustering.
2. K-Means-based clustering.
3. GMM-based clustering.

### GMM Configuration

The following configuration was used:

| Parameter                  | Value                  |
| -------------------------- | ---------------------- |
| Clustering algorithm       | Gaussian Mixture Model |
| Number of components       | 3                      |
| Covariance type            | Full                   |
| Initialization repetitions | 20                     |
| Random state               | 42                     |
| Feature preprocessing      | StandardScaler         |
| Input features             | 8 LPBF parameters      |

### Cluster-Specific Regression

After clustering, separate regression models were trained within each GMM cluster.

The models investigated were:

* **Gaussian Process Regression (GPR)**
* **Support Vector Regression (SVR)**
* **Random Forest Regression**

The models were trained independently for each mechanical-property target:

* **Ultimate Tensile Strength (UTS)**
* **Yield Strength (YS)**
* **Elongation to Failure (EF)**

The performance of the resulting cluster-specific models was evaluated on the held-out test set using:

* **R²** — coefficient of determination
* **RMSE** — root mean squared error
* **MAE** — mean absolute error

### GMM vs Global Models

The GMM approach is treated as an experimental extension of the baseline modeling pipeline.

The comparison is structured as:

| Approach              | Clustering | Regression               |
| --------------------- | ---------- | ------------------------ |
| Global baseline       | None       | GPR / SVR / RF / XGBoost |
| Reference methodology | K-Means    | GPR / SVR / RF           |
| Proposed experiment   | GMM        | GPR / SVR / RF           |

The objective is to determine whether introducing probabilistic clustering improves prediction performance for the Ti6Al4V mechanical-property targets.

### Important Methodological Note

The reference research paper uses **K-Means clustering with three clusters** as part of its CIRM methodology. The GMM implementation in this project is therefore an **additional experimental approach**, rather than an exact reproduction of the paper's CIRM methodology.

GMM results will be compared using the same evaluation metrics and held-out test data to determine whether the clustering approach provides measurable predictive improvement.

### Current Status

🟢 **Completed**

* GMM implementation
* Three-component clustering
* Feature standardization
* Cluster assignment
* Cluster-specific GPR
* Cluster-specific SVR
* Cluster-specific Random Forest
* R², RMSE and MAE evaluation
* Comparison with global baseline models

🟡 **Next Steps**

* Compare GMM against K-Means
* Hyperparameter tuning
* Cross-validation
* SHAP-based model interpretation
* Investigate cluster characteristics
* Multi-objective optimization using validated models

---

# ⚠️ Current ML Limitations

The current ML results should be considered a **baseline model comparison** rather than final research conclusions.

Important considerations include:

### Dataset Size

The dataset contains only 173 observations. This is relatively small for training complex machine-learning models.

### Train-Test Split

The current results use a single 80/20 train-test split.

Therefore, the reported R², RMSE, and MAE values can depend on the particular samples assigned to the test set.

### Experimental References

The observations originate from multiple experimental references.

Differences between studies may include:

* Experimental equipment
* Processing conditions
* Material conditions
* Specimen geometry
* Measurement procedures

Group-aware validation based on the `Reference` column should therefore be investigated in a later stage.

### Model Comparison

The current comparison is intended to establish a baseline between several regression algorithms.

Hyperparameter optimization and cross-validation have not yet been used to establish final model performance.

---

# 🔬 Relationship to the Research Paper

The research paper uses a **Clustering Integrated Regression Model (CIRM)** involving:

```text
K-Means Clustering
       │
       ▼
 ┌─────┼─────┐
 ▼     ▼     ▼
GPR   SVR    RF
```

The paper reports the use of K-Means clustering followed by GPR, SVR, and Random Forest regression.

The current notebook first implements the regression models independently to establish baseline performance.

XGBoost has additionally been included as an experimental benchmark and is **not part of the paper's reported CIRM regression model set**.

The next stage can therefore investigate whether integrating K-Means clustering with the regression models changes prediction performance.

---

# 🚀 Next Machine-Learning Stage

The planned next stage is to extend the baseline models into the clustering-based framework:

```text
                 Dataset
                    │
                    ▼
             Standardization
                    │
                    ▼
             K-Means Clustering
                    │
             ┌──────┼──────┐
             ▼      ▼      ▼
          Cluster Cluster Cluster
             1      2      3
             │      │      │
             └──────┼──────┘
                    ▼
          ┌─────────────────┐
          │ GPR / SVR / RF  │
          │ per cluster     │
          └────────┬────────┘
                   │
                   ▼
             Model Evaluation
                   │
                   ▼
            UTS / YS / EF
```

Following this, the project can investigate:

* Hyperparameter tuning
* Cross-validation
* SHAP-based model interpretation
* Feature interaction analysis
* Multi-objective optimization
* NSGA-II optimization
* Comparison with experimental observations

The final optimization stage should only be performed after establishing an appropriate validation strategy for the predictive models.

---



# 🛠️ Technologies Used

| Technology                | Purpose                      |
| ------------------------- | ---------------------------- |
| 🐍 Python                 | Core programming language    |
| 📓 Jupyter Notebook       | Interactive analysis         |
| 🐼 Pandas                 | Data manipulation            |
| 🔢 NumPy                  | Numerical computation        |
| 📊 Matplotlib             | Data visualization           |
| 📗 Excel                  | Dataset storage              |
| 🤖 Scikit-learn           | Planned ML modeling          |
| ⚙️ Optimization Libraries | Planned process optimization |

---

# 🚀 Installation

## 1. Clone the Repository

```bash
git clone <YOUR_REPOSITORY_URL>
cd ML-Ti6Al4V-Process-Optimization
```

---

## 2. Create a Virtual Environment

### Linux / macOS

```bash
python3 -m venv venv
source venv/bin/activate
```

### Windows

```powershell
python -m venv venv
venv\Scripts\activate
```

---

## 3. Install Dependencies

```bash
pip install numpy pandas matplotlib openpyxl jupyter
```

For the upcoming machine-learning stage:

```bash
pip install scikit-learn scipy seaborn
```

You can also create a `requirements.txt` file:

```text
numpy
pandas
matplotlib
openpyxl
jupyter
scikit-learn
scipy
seaborn
```

Then install everything using:

```bash
pip install -r requirements.txt
```

---

# ▶️ Running the Notebook

Start Jupyter:

```bash
jupyter notebook
```

or:

```bash
jupyter lab
```

Open:

```text
ML_Based_Ti6Al4V_Process_Optimization.ipynb
```

Make sure the dataset exists at the expected location.

For Google Colab, upload:

```text
1-s2.0-S2214860424003877-mmc1.xlsx
```

and ensure the `FILE_PATH` points to the uploaded file.

---

# 🧠 Planned Machine-Learning Pipeline

The current notebook establishes the EDA foundation.

The complete project can later follow this pipeline:

```text
                    ┌──────────────────┐
                    │   Raw Dataset    │
                    └────────┬─────────┘
                             │
                             ▼
                    ┌──────────────────┐
                    │ Data Exploration │
                    │      (EDA)       │
                    └────────┬─────────┘
                             │
                             ▼
                    ┌──────────────────┐
                    │ Data Cleaning &  │
                    │ Preprocessing    │
                    └────────┬─────────┘
                             │
                             ▼
                    ┌──────────────────┐
                    │ Feature Analysis │
                    │ & Engineering    │
                    └────────┬─────────┘
                             │
                             ▼
                    ┌──────────────────┐
                    │ Train / Test     │
                    │ Split            │
                    └────────┬─────────┘
                             │
                             ▼
              ┌──────────────────────────────┐
              │       ML Regression Models   │
              ├──────────────────────────────┤
              │ • Linear Regression          │
              │ • Random Forest              │
              │ • Gradient Boosting          │
              │ • Extra Trees                │
              │ • Support Vector Regression  │
              │ • XGBoost / other models     │
              └──────────────┬───────────────┘
                             │
                             ▼
                    ┌──────────────────┐
                    │ Model Evaluation │
                    ├──────────────────┤
                    │ R²               │
                    │ MAE              │
                    │ RMSE             │
                    │ MAPE*            │
                    └────────┬─────────┘
                             │
                             ▼
                    ┌──────────────────┐
                    │ Feature / Model  │
                    │ Interpretation   │
                    └────────┬─────────┘
                             │
                             ▼
                    ┌──────────────────┐
                    │ Multi-objective  │
                    │ Optimization     │
                    └────────┬─────────┘
                             │
                             ▼
                    ┌──────────────────┐
                    │ Optimal Process  │
                    │ Parameters       │
                    └──────────────────┘
```

> * MAPE should be used carefully when target values can approach zero.

---

# 🎯 Future Prediction Tasks

The ML stage can investigate prediction of:

### Ultimate Tensile Strength

```text
Process Parameters ─────► UTS (MPa)
```

### Yield Strength

```text
Process Parameters ─────► YS (MPa)
```

### Elongation

```text
Process Parameters ─────► EF (%)
```

A multi-output model may also eventually be investigated:

```text
             ┌──────► UTS
             │
Process ─────┼──────► YS
Parameters   │
             └──────► EF
```

---

# ⚙️ Process Optimization

After sufficiently validated prediction models are developed, the project can investigate process optimization.

The goal is to identify parameter combinations that satisfy a desired mechanical-property objective.

For example:

```text
                    LPBF Parameters
                          │
        ┌─────────────────┼─────────────────┐
        ▼                 ▼                 ▼
   Laser Power      Scan Speed       Hatch Distance
        │                 │                 │
        └─────────────────┼─────────────────┘
                          ▼
                 ML Prediction Model
                          │
              ┌───────────┼───────────┐
              ▼           ▼           ▼
             UTS          YS          EF
              │           │           │
              └───────────┼───────────┘
                          ▼
                  Optimization Stage
                          │
                          ▼
                Recommended Parameter
                    Combinations
```

Optimization should be performed only after appropriate validation of the predictive models and consideration of the physical meaning and experimental limits of the process parameters.

---

# ⚠️ Important Data Science Considerations

## 1. Identifier Leakage

Columns such as `Alloy` and `Reference` should be investigated before being used as ML features.

An identifier can allow a model to learn dataset-specific patterns rather than genuine physical relationships.

---

## 2. Experimental Grouping

Because the dataset contains observations from different references, a random train/test split may not always represent the strongest evaluation strategy.

Depending on the research objective, grouped validation based on `Reference` may be worth investigating.

For example:

```text
Reference A ──┐
Reference B ──┤
Reference C ──┼──► Model
Reference D ──┤
Reference E ──┘
```

A later analysis can compare conventional random splitting with group-aware validation.

---

## 3. Outliers

Outliers should not automatically be removed.

Each unusual observation should ideally be investigated based on:

* Experimental validity
* Measurement reliability
* Physical plausibility
* Source/reference
* Processing conditions

---

## 4. Feature Leakage

Only variables that would genuinely be available for the intended prediction scenario should be used as model inputs.

This is particularly important when geometry or experimentally measured properties are included in the dataset.

---

# 📌 Current Project Status

### 🟢 Completed

* [x] Dataset loading
* [x] Dataset shape inspection
* [x] First/last-row inspection
* [x] Column inspection
* [x] Data-type inspection
* [x] Missing-value analysis
* [x] Missing-value percentage calculation
* [x] Duplicate-row analysis
* [x] Unique-value analysis
* [x] Alloy identifier investigation
* [x] Reference analysis
* [x] Samples-per-reference analysis
* [x] Numerical-column identification
* [x] Descriptive statistics
* [x] Additional statistics
* [x] Quantile analysis
* [x] Process-parameter definition
* [x] Target-variable definition
* [x] Process-parameter distributions
* [x] Target distributions
* [x] Process-parameter boxplots
* [x] Target boxplots

### 🟡 In Progress

* [ ] Correlation analysis
* [ ] Feature relationship analysis
* [ ] Outlier investigation
* [ ] Feature engineering
* [ ] Data preprocessing
* [ ] Experimental-group analysis

### 🔵 Planned

* [ ] Train/test strategy
* [ ] Regression models
* [ ] Hyperparameter tuning
* [ ] Cross-validation
* [ ] Model comparison
* [ ] Feature importance
* [ ] Model interpretation
* [ ] Prediction analysis
* [ ] Process optimization
* [ ] Multi-objective optimization

---

# 📊 Expected Outputs

The project is expected to produce:

### Data Analysis

* Dataset statistics
* Missing-value reports
* Duplicate analysis
* Feature distributions
* Target distributions
* Outlier analysis
* Correlation analysis

### Machine Learning

* Trained regression models
* Prediction results
* Evaluation metrics
* Feature importance
* Model interpretation

### Optimization

* Candidate process-parameter combinations
* Predicted mechanical properties
* Optimization results
* Experimental recommendations for further validation

---

# 🔬 Research Workflow

The overall research workflow is:

```text
📚 Literature / Dataset
          │
          ▼
📥 Data Collection
          │
          ▼
🔍 Exploratory Data Analysis
          │
          ▼
🧹 Data Cleaning
          │
          ▼
⚙️ Feature Engineering
          │
          ▼
🤖 Machine Learning
          │
          ▼
📊 Model Evaluation
          │
          ▼
🔎 Model Interpretation
          │
          ▼
⚙️ Process Optimization
          │
          ▼
🧪 Experimental Validation
```

---

# 📚 Scientific Context

This project is based on research concerning **machine-learning-assisted prediction and optimization of mechanical properties for Ti6Al4V manufactured using Laser Powder Bed Fusion**.

The dataset should be interpreted in the context of additive-manufacturing experiments rather than as a generic tabular machine-learning dataset.

Particular attention should therefore be given to:

* Manufacturing physics
* Experimental grouping
* Process parameter ranges
* Material conditions
* Measurement methods
* Dataset heterogeneity
* Model generalization

---

# 🤝 Contribution

Contributions and improvements are welcome.

Possible contribution areas include:

* Improved EDA
* Feature engineering
* Machine-learning models
* Model interpretation
* Optimization algorithms
* Visualization
* Statistical validation
* Experimental analysis

A typical workflow is:

```bash
git checkout -b feature/new-analysis
```

Make your changes, test the notebook, and submit a pull request.

---

# 📜 License

This project is distributed under the license included in the repository.

See:

```text
LICENSE
```

for the complete license terms.

---

# ⭐ Acknowledgements

This project makes use of publicly available experimental data and research concerning **Ti6Al4V Laser Powder Bed Fusion** and machine-learning-assisted materials-property prediction.

The original scientific publication and supplementary dataset should be properly cited when this work is used in academic research.

---

# 🧪 Research Note

> **This repository is intended for research and educational purposes.**

Machine-learning predictions should not be treated as a replacement for physical experiments or engineering validation.

Predicted optimal LPBF parameters should be experimentally validated before being used in real manufacturing applications.

---

<p align="center">

### 🧬 Ti6Al4V + 🔥 LPBF + 🤖 Machine Learning + ⚙️ Optimization

**Turning additive-manufacturing data into actionable process insights.**

⭐ Star the repository if you find the project useful!

</p>
