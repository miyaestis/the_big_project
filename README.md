# Analysis of EEG Data and Education in Schizophrenia Patients

## Project Overview
This project analyzes EEG data from a sensory task performed by individuals diagnosed with schizophrenia and a control group. The dataset, sourced from [Kaggle](https://www.kaggle.com/datasets/broach/button-tone-sz/data?select=demographic.csv), consists of 81 subjects (32 control group, 49 diagnosed with schizophrenia). The goal of this project was to investigate the relationship between years of education and schizophrenia, as well as explore correlations with age distribution across the groups.

---
## Hypothesis
We hypothesized a **negative correlation** between **years of education** and **schizophrenia diagnosis**, meaning that individuals diagnosed with schizophrenia may have, on average, fewer years of education compared to the control group.

---
## Installation and Setup
### Dependencies
This project requires the following Python libraries:
- `numpy`
- `pandas`
- `matplotlib`

### Installation
Ensure you have the required libraries installed before running the code. You can install them using:
```bash
pip install numpy pandas matplotlib
```

### Dataset
Make sure the **demographic.csv** file is in the correct directory as specified in the code.

---
## Data Preparation and Debugging
- The dataset initially contained **extra spaces** in column names, which caused issues when accessing the data.
- This was corrected by manually inspecting and renaming the column headers.

---
## Step-by-Step Analysis
### 1. Importing Required Libraries
```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
```

### 2. Loading the Dataset
```python
df = pd.read_csv('/Users/miyaestis/Desktop/demographic.csv')
df.head(82)
```
This step loads the dataset and ensures it is correctly structured.

### 3. Plotting the Overall Education Distribution
A bar plot was created to visualize the general distribution of education years across all participants.
```python
education_counts = df['education'].value_counts().sort_index()
plt.bar(education_counts.index, education_counts.values, color='black', alpha=0.85, edgecolor='black')
plt.title("Bar Plot of Years of Education", fontsize=16)
plt.xlabel("Years of Education", fontsize=14)
plt.ylabel("Frequency", fontsize=14)
plt.grid(axis="y", linestyle="--", alpha=0.85)
y_ticks = np.arange(0, education_counts.values.max() + 3, 3)
plt.yticks(y_ticks)
plt.show()
```

### 4. Education Distribution in Patients with Schizophrenia
Filtering participants diagnosed with schizophrenia (`group == 1`) and visualizing their education distribution.
```python
filtered_df = df[df["group"] == 1]
education_counts = filtered_df["education"].value_counts().sort_index()
plt.figure(figsize=(8, 6))
plt.bar(education_counts.index, education_counts.values, width=0.6, color='black')
plt.xlabel("Years of education", fontsize=12)
plt.ylabel("Amount of people", fontsize=12)
plt.title("Amount of patients with schizophrenia as a function of total years of education", fontsize=14)
plt.grid(axis="y", linestyle="--", alpha=0.85)
plt.xticks(education_counts.index, fontsize=10)
plt.show()
```

### 5. Education Distribution in the Control Group
Filtering control group participants (`group == 0`) and plotting their education levels.
```python
filtered_df = df[df["group"] == 0]
education_counts = filtered_df["education"].value_counts().sort_index()
plt.figure(figsize=(8, 6))
plt.bar(education_counts.index, education_counts.values, width=0.6, color='black')
plt.xlabel("Years of education", fontsize=12)
plt.ylabel("Control group", fontsize=12)
plt.grid(axis="y", linestyle="--", alpha=0.85)
plt.xticks(education_counts.index, fontsize=10)
plt.show()
```

### 6. Comparing Age Distribution Between Groups
We calculated the correlation between age and schizophrenia and plotted a boxplot to compare age distributions.
```python
correlation = df['age'].corr(df['group'])
print(f"Correlation between age and schizophrenia: {correlation:.2f}")

plt.figure(figsize=(8, 6))
df.boxplot(column='age', by='group', grid=False, showmeans=True, meanline=True,
           boxprops=dict(color='black'), whiskerprops=dict(color='black'),
           capprops=dict(color='red'), medianprops=dict(color='red'))
plt.title("Age Distribution by Group")
plt.suptitle("")
plt.xlabel("Group (0 = Controls, 1 = Schizophrenia)")
plt.ylabel("Age")
plt.show()
```
#### Interpretation:
- The **boxplot** represents the **interquartile range (IQR)**, showing the middle 50% of the data.
- The **correlation coefficient** quantifies the relationship between age and schizophrenia.

---
## Findings
1. **Education & Schizophrenia**
   - Preliminary visualization suggests that participants diagnosed with schizophrenia tend to have fewer years of education compared to the control group.
2. **Age & Schizophrenia**
   - A correlation of **~0.06** was observed, indicating **almost no relationship** between age and schizophrenia in this dataset.
3. **Boxplot Interpretation**
   - The median age appears similar between both groups, with slight variations in distribution.

---
## Limitations
- The dataset is **large (20.8GB)**, requiring efficient handling.
- The dataset may contain **missing values** or **biases** in data collection.
- The correlation does not imply causation.

---
## Future Work
- Further statistical testing (e.g., **T-tests, ANOVA**) to validate significance.
- Machine learning models to predict schizophrenia based on demographic factors.
- Expanding the dataset to include additional cognitive and neurological variables.

---
## Authors & Credits
- **Project Team**: [Miya Estis Carmel Mantelblit]
- **Dataset Source**: Kaggle ([Link](https://www.kaggle.com/datasets/broach/button-tone-sz/data?select=demographic.csv))
- **Tools Used**: Python, Pandas, Matplotlib





