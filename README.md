Categorical Data Imputation using Mode

Overview

This project demonstrates how to handle missing categorical data using mode imputation, specifically by filling missing values with the most frequently occurring category. The dataset used is data_science_job.csv, which contains various features related to job candidates.

What is Mode?

Mode is the most frequent value in a dataset. A dataset can have:

Uni-modal: One mode

Bi-modal: Two modes

Tri-modal: Three modes

Multi-modal: More than one mode

No mode: If all values appear only once

Mode Formula:

Mode = Highest Frequency Term

Steps in Categorical Data Imputation

1. Import Required Libraries

import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns

2. Load the Dataset

df = pd.read_csv('../Data/data_science_job.csv')
df.info()
df.describe()
df.isnull().mean() * 100  # Check missing values percentage

3. Extract Categorical Columns

df1 = df.select_dtypes(exclude=np.number)
df1 = [col for col in df1.columns if 0 < df[col].isnull().mean() * 100 < 5]
print(df1)  # Columns with missing values <5%

4. Determine the Most Frequent Category

most_frequent_value = df['enrolled_university'].mode()[0]
print(most_frequent_value)

5. Visualize Distribution Before Imputation

plt.figure()
ax = plt.subplot(1, 1, 1)
df[df['enrolled_university'] == 'no_enrollment']['training_hours'].value_counts().plot(kind='kde', label='Original Value')
df[df['enrolled_university'].isnull()]['training_hours'].plot(kind='kde', label='Missing Value')
ax.legend()
plt.title('Most Frequent Value Occurrences and Missing Values')
plt.show()

6. Impute Missing Values

df['enrolled_university'].fillna('no_enrollment', inplace=True)

Note: This approach may change in future versions of pandas. To avoid warnings, use:

df['enrolled_university'] = df['enrolled_university'].fillna('no_enrollment')

7. Validate Imputation with Post-Processing Analysis

plt.figure()
ax = plt.subplot(1, 1, 1)
before = df[df['enrolled_university'] == 'no_enrollment']['training_hours']
before.plot(kind='kde', label='Before Imputation')
df[df['enrolled_university'] == 'no_enrollment']['training_hours'].value_counts().plot(kind='kde', label='After Imputation')
ax.legend()
plt.title('Before Imputation & After Imputation')
plt.show()

Conclusion

This project successfully fills missing categorical data using mode imputation and verifies the distributional integrity of the dataset post-imputation.
