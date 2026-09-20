# 🧪 ML-Based Ti6Al4V Process Optimization

<p align="center">

![Python](https://img.shields.io/badge/Python-3.10%2B-3776AB?style=for-the-badge\&logo=python\&logoColor=white)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-F37626?style=for-the-badge\&logo=jupyter\&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-Data%20Analysis-150458?style=for-the-badge\&logo=pandas\&logoColor=white)
![NumPy](https://img.shields.io/badge/NumPy-Numerical%20Computing-013243?style=for-the-badge\&logo=numpy\&logoColor=white)
![Matplotlib](https://img.shields.io/badge/Matplotlib-Visualization-11557C?style=for-the-badge\&logo=matplotlib\&logoColor=white)
![Material Science](https://img.shields.io/badge/Material-Science-8A2BE2?style=for-the-badge)
![Machine Learning](https://img.shields.io/badge/Machine-Learning-FF6F00?style=for-the-badge)

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

A histogram is generated to visu
