# Sleep Health & Lifestyle

An Exploratory Data Analysis (EDA) project focused on understanding the relationship between **sleep, lifestyle, stress, physical activity, and health-related factors**.

The project uses Python and popular data analysis and visualization libraries to clean, explore, and analyze a Sleep Health and Lifestyle dataset.

---

## 📌 Project Overview

Sleep quality can be affected by several lifestyle and health-related factors such as:

* Sleep duration
* Stress level
* Physical activity
* Daily steps
* BMI category
* Heart rate
* Blood pressure
* Age
* Gender
* Occupation

The goal of this project is to explore these variables and identify meaningful patterns and relationships within the dataset.

> **Main Question:**
> What relationships can be observed between lifestyle, health indicators, and sleep-related outcomes?

---

## 📊 Dataset

The dataset contains **374 records and 13 original columns**.

### Features

| Feature                   | Description                                 |
| ------------------------- | ------------------------------------------- |
| `person_id`               | Unique identifier for each person           |
| `gender`                  | Gender of the person                        |
| `age`                     | Age in years                                |
| `occupation`              | Person's occupation                         |
| `sleep_duration`          | Average sleep duration in hours             |
| `quality_of_sleep`        | Sleep quality score                         |
| `physical_activity_level` | Physical activity level                     |
| `stress_level`            | Stress level                                |
| `bmi_category`            | BMI classification                          |
| `blood_pressure`          | Blood pressure in Systolic/Diastolic format |
| `heart_rate`              | Heart rate                                  |
| `daily_steps`             | Number of daily steps                       |
| `sleep_disorder`          | Recorded sleep disorder                     |

The dataset includes two recorded sleep disorders:

* **Sleep Apnea — 78 records**
* **Insomnia — 77 records**

## Missing values in `sleep_disorder` were replaced with `"good sleep"` during the analysis.

## 🛠️ Tools & Technologies

* **Python**
* **Pandas** — Data manipulation and analysis
* **NumPy** — Numerical operations
* **Matplotlib** — Data visualization
* **Seaborn** — Statistical visualization
* **Jupyter Notebook**

---

## 🔍 Data Analysis Workflow

The project follows a typical EDA workflow:

```text
Raw Dataset
     ↓
Data Loading
     ↓
Data Inspection
     ↓
Descriptive Statistics
     ↓
Missing Values Analysis
     ↓
Duplicate Analysis
     ↓
Data Cleaning
     ↓
Feature Transformation
     ↓
Exploratory Data Analysis
     ↓
Correlation Analysis
     ↓
Visualization
     ↓
Insights
```

---

## 🧹 Data Cleaning & Preprocessing

### 1. Missing Values

The `sleep_disorder` column contained missing values.

These values were replaced with:

```text
good sleep
```

After this transformation, there were no remaining missing values in the dataset.

### 2. Duplicate Check

Duplicate rows were checked using:

```python
df.duplicated().sum()
```

The result was:

```text
0
```

meaning no completely identical rows were detected.

### 3. Blood Pressure Transformation

The original `blood_pressure` column was stored in the form:

```text
126/83
125/80
140/90
```

It was split into two numerical features:

```text
systolic
diastolic
```

using:

```python
df[["Systolic", "Diastolic"]] = (
    df["Blood Pressure"]
    .str.split("/", expand=True)
    .astype(int)
)
```

This makes blood pressure easier to analyze numerically.

### 4. Column Name Standardization

Column names were converted to lowercase and spaces were replaced with underscores:

```python
df.columns = df.columns.str.lower().str.replace(" ", "_")
```

For example:

```text
Sleep Duration
```

became:

```text
sleep_duration
```

---

## 📈 Descriptive Analysis

The numerical variables were explored using descriptive statistics.

Some key statistics:

| Variable                |    Mean |  Min |   Max |
| ----------------------- | ------: | ---: | ----: |
| Age                     |   42.18 |   27 |    59 |
| Sleep Duration          |    7.13 |  5.8 |   8.5 |
| Quality of Sleep        |    7.31 |    4 |     9 |
| Physical Activity Level |   59.17 |   30 |    90 |
| Stress Level            |    5.39 |    3 |     8 |
| Heart Rate              |   70.17 |   65 |    86 |
| Daily Steps             | 6816.84 | 3000 | 10000 |

These statistics were obtained from the notebook's `describe()` analysis.

---

## 👥 Categorical Analysis

### Gender Distribution

The dataset contains:

* **189 Male**
* **185 Female**

### Occupation Distribution

The most common occupations include:

* Nurse — 73
* Doctor — 71
* Engineer — 63
* Lawyer — 47
* Teacher — 40
* Accountant — 37
* Salesperson — 32

---

## 😴 Sleep Analysis

The average sleep duration in the dataset is approximately:

**7.13 hours**

with values ranging from **5.8 to 8.5 hours**.

The analysis also compares sleep duration across different groups.

For example:

### Sleep Duration by Gender

| Gender | Average Sleep Duration |
| ------ | ---------------------: |
| Female |             7.23 hours |
| Male   |             7.04 hours |

### Sleep Duration by BMI Category

| BMI Category  | Average Sleep Duration |
| ------------- | ---------------------: |
| Normal        |             7.39 hours |
| Normal Weight |             7.33 hours |
| Obese         |             6.96 hours |
| Overweight    |             6.77 hours |

---

## 📊 Visualizations

The project uses several visualization techniques, including:

### Box Plot

Used to inspect the distribution of sleep duration and identify potential outliers.

```python
sns.boxplot(x=df["sleep_duration"])
```

### Scatter Plot

Used to explore the relationship between stress level and sleep duration.

```python
sns.scatterplot(
    x="stress_level",
    y="sleep_duration",
    data=df
)
```

### Correlation Heatmap

A correlation matrix was calculated for numerical variables to explore relationships between features.

Some notable correlations found in the analysis include:

* `sleep_duration` ↔ `quality_of_sleep`: **0.883**
* `stress_level` ↔ `quality_of_sleep`: **-0.899**
* `stress_level` ↔ `sleep_duration`: **-0.811**
* `physical_activity_level` ↔ `daily_steps`: **0.773**
* `systolic` ↔ `diastolic`: **0.973**

---

## 💡 Key Observations

Based on the exploratory analysis:

1. **Sleep duration and sleep quality show a strong positive correlation**, meaning higher sleep duration tends to be associated with higher reported sleep quality in this dataset.

2. **Stress level has a strong negative correlation with sleep quality**, indicating that higher stress levels tend to occur alongside lower sleep quality.

3. **Stress level also shows a strong negative correlation with sleep duration.**

4. **Physical activity level is strongly associated with daily steps**, which is expected because both variables represent aspects of physical activity.

5. **Blood pressure components are highly correlated**, with systolic and diastolic blood pressure showing a strong positive relationship.

6. Average sleep duration differs across BMI categories, with the dataset showing lower average sleep duration for the Overweight and Obese groups compared with the Normal categories.

These observations describe patterns in this dataset and should not be interpreted as medical or causal conclusions.

---

## 📁 Project Structure

```text
DataAnalysis_Python-Sleep_Health_and_Lifestyle-/
│
├── Sleep_Health_and_Lifestyle_Dataset.csv
├── DA_sleep_health.ipynb
└── README.md
```

---

### Install the required libraries

```bash
pip install pandas numpy matplotlib seaborn jupyter
```
