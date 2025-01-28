# the_big_project
The dataset we found https://www.kaggle.com/datasets/broach/button-tone-sz/data?select=demographic.csv was about EEG data findings took from basic sensory task in people who have schizophrenia (total 81 subjects, 32 control group, 49 had schizophrenia). The data set was well structured and very big (20.8 GB). After making a quick search we found a csv file called 'demographic' that included information such as gender, age, education etc. Suddenly we came up with a hypothesis about the negative correlation between the years of education and having the disease.
-Step 1. 
import numpy as np 
import pandas as pd 
import matplotlib.pyplot as plt
Pandas and Matplotlib libraries were necessary for the correlation testing and grafics.
-Step 2. Loading the Dataset
df = pd.read_csv('/Users/miyaestis/Desktop/demographic.csv')
df.head(82)
The dataset is loaded using Pandas and previewed to ensure it is correctly loaded.
-Step 3 Debugging.
At first our code couldn't find the right columns in the table and we're wondering why. Finally one of us realized that mb the problem was in the file itself. Turns out the dataset contained columns with an unnecessary empty space. After fixing we continued coding.
-Step 4. Plotting the Overall Education Distribution
education_counts = df['education'].value_counts().sort_index()
plt.bar(education_counts.index, education_counts.values, color='black', alpha=0.85, edgecolor='black')
plt.title("Bar Plot of Years of Education", fontsize=16)
plt.xlabel("Years of Education", fontsize=14)
plt.ylabel("Frequency", fontsize=14)
plt.grid(axis="y", linestyle="--", alpha=0.85)
y_ticks = np.arange(0, education_counts.values.max() + 3, 3) 
plt.yticks(y_ticks)
plt.show()
We created a bar plot showing the distribution of years of education across all participants.
-Step 5. Analysis for Patients with Schizophrenia
filtered_df = df[df["group"] == 1]
education_counts = filtered_df["education"].value_counts().sort_index()
plt.figure(figsize=(8, 6))
plt.bar(education_counts.index, education_counts.values, width=0.6, color='black')
plt.xlabel("Years of education", fontsize=12)
plt.ylabel("Amount of people", fontsize=12)
plt.title("Amount of patients with schizophrenia as a function of total years of education", fontsize=14)
plt.grid(axis="y", linestyle="--", alpha=0.85)
plt.xticks(education_counts.index, fontsize=10)
Filters the dataset to include only participants with group == 1 (1=schizophrenia, 0=control group).
We created a bar plot to visualize the distribution of years of education for patients with schizophrenia.
-Step 6. Analysis for control group
filtered_df = df[df["group"] ==0]
education_counts = filtered_df["education"].value_counts().sort_index()
plt.figure(figsize=(8, 6))
plt.bar(education_counts.index, education_counts.values, width=0.6, color='black')
plt.xlabel("Years of education", fontsize=12)
plt.ylabel("Control group", fontsize=12)
plt.grid(axis="y", linestyle="--", alpha=0.85)
plt.xticks(education_counts.index, fontsize=10)
-Step 7. Comparing age distribution between groups.
correlation = df['age'].corr(df['group'])
print(f"Correlation between age and schizophrenia: {correlation:.2f}")
plt.figure(figsize=(8, 6))
df.boxplot(column='age', by='group', grid=False, showmeans=True, meanline=True,  boxprops=dict(color='black'),
           whiskerprops=dict(color='black'),
           capprops=dict(color='red'),
           medianprops=dict(color='red'))
plt.title("Age Distribution by Group")
plt.suptitle("")  
plt.xlabel("Group (0 = Controls, 1 = Schizophrenia)")
plt.ylabel("Age")
plt.show()
The boxplot represents the interquartile range (IQR), which contains the middle 50% of the data.
*Ensure the dataset exists at the specified path and it's clean.
