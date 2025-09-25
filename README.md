Cardiovascular Disease Analysis Project
1. Project Overview
This project is an in-depth exploratory data analysis (EDA) of a heart disease dataset. The primary goal is to uncover patterns, correlations, and key insights related to heart disease presence. The analysis uses Python with the Pandas library for data manipulation and is presented as a step-by-step guide that can be easily understood and replicated.
Tools & Technologies:
●	Python: For data cleaning, exploration, and analysis.
●	Pandas: A powerful library for data manipulation and analysis.
●	Jupyter Notebook: The interactive environment used to execute the code.
●	Matplotlib & Seaborn: Libraries for data visualization.
●	Tableau: A business intelligence tool used to create the final dashboard.
2. Dataset Description
The dataset contains 14 key features that describe a patient's health status and a target variable indicating the presence of heart disease.
●	age: Age of the patient in years.
●	sex: Gender of the patient (1 = male, 0 = female).
●	cp: Chest pain type (0-3).
●	trestbps: Resting blood pressure (in mm Hg).
●	chol: Serum cholesterol (in mg/dl).
●	fbs: Fasting blood sugar > 120 mg/dl (1 = true, 0 = false).
●	restecg: Resting electrocardiographic results (0-2).
●	thalach: Maximum heart rate achieved.
●	exang: Exercise-induced angina (1 = yes, 0 = no).
●	oldpeak: ST depression induced by exercise relative to rest.
●	slope: The slope of the peak exercise ST segment.
●	ca: Number of major vessels (0-3) colored by fluoroscopy.
●	thal: Thalassemia (3 = normal, 6 = fixed defect, 7 = reversible defect).
●	target: The target variable (1 = heart disease, 0 = no heart disease).
3. Step-by-Step Data Analysis Guide
Step 1: Import The Libraries And Dataset
This is the foundational step. We import the necessary Python libraries (pandas for data handling, and matplotlib and seaborn for visualization) and then load the dataset from a CSV file into a Pandas DataFrame.
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

df = pd.read_csv('heart.csv')

Step 2: Display Top 5 Rows of The Dataset
This step is crucial for getting a first look at the data structure. It confirms that the dataset was loaded correctly and provides a snapshot of the column names and data types.
df.head()

Step 3: Check The Last 5 Rows of The Dataset
Similar to the previous step, this helps us verify the dataset's integrity by checking the end of the data, which can sometimes reveal issues like missing or trailing values.
df.tail()

Step 4: Find Shape of Our Dataset (Number of Rows And Columns)
This provides a quick summary of the dataset's size. Knowing the total number of rows and columns helps in planning the subsequent analysis and resource requirements.
print(f'Number of Rows: {df.shape[0]}')
print(f'Number of Columns: {df.shape[1]}')

Step 5: Get Information About Our Dataset
The info() function is an essential tool for data validation. It provides a non-null count for each column, the data type of each column (int, float, object), and the total memory usage. This helps us identify potential data cleaning needs, such as converting data types.
df.info()

Step 6: Check Null Values In The Dataset
Checking for null values is a critical data cleaning step. The .isnull().sum() method provides a count of missing values for each column. In a real-world scenario, you would then decide how to handle these (e.g., fill with a mean, or drop the rows).
df.isnull().sum()

Step 7: Check For Duplicate Data and Drop Them
Duplicate rows can skew analysis and lead to inaccurate conclusions. By checking for and dropping duplicates, we ensure that our analysis is based on unique, valid patient records.
df.duplicated().sum()
df.drop_duplicates(inplace=True)
print(f'Shape after dropping duplicates: {df.shape}')

Step 8: Get Overall Statistics About The Dataset
The .describe() method provides a statistical summary of all numerical columns. This includes count, mean, standard deviation, and quartiles, giving us a quick understanding of the data's distribution and potential outliers.
df.describe()

Step 9: Draw Correlation Matrix
A correlation matrix is a powerful visualization for understanding the relationships between variables. We use a heatmap to show the correlation coefficients, where values close to 1 or -1 indicate a strong positive or negative correlation, respectively. This helps identify features that are most predictive of the target variable.
plt.figure(figsize=(12, 10))
sns.heatmap(df.corr(), annot=True, cmap='coolwarm')
plt.title('Correlation Matrix')
plt.show()

Step 10: How Many People Have Heart Disease?
This step provides a foundational metric for the entire project: the distribution of the target variable. We can see the class balance (how many patients have heart disease vs. how many don't).
df['target'].value_counts()

Step 11: Find Count of Male & Female
Understanding the gender composition of the dataset is crucial for demographic analysis. We can see if the patient population is balanced between males and females.
df['sex'].value_counts()

Step 12: Find Gender Distribution According to The Target Variable
This visualization helps us understand how the presence of heart disease differs between genders. By plotting sex against target, we can see if one gender is more susceptible to the disease in this dataset.
sns.countplot(x='sex', hue='target', data=df)
plt.title('Gender Distribution by Target')
plt.xticks(ticks=[0, 1], labels=['Female', 'Male'])
plt.show()

Step 13: Check Age Distribution In The Dataset
Age is a major risk factor for many diseases. A histogram of the age column shows the age range and the most common age groups in the dataset.
sns.histplot(df['age'], kde=True, bins=20)
plt.title('Age Distribution')
plt.show()

Step 14: Check Chest Pain Type
Chest pain is a primary symptom of heart disease. This step provides a count of each type of chest pain, which is helpful context for the next visualization.
df['cp'].value_counts()

Step 15: Show The Chest Pain Distribution As Per Target Variable
This chart directly links chest pain type to the presence of heart disease. It can reveal which types of chest pain are most common in patients with a positive diagnosis.
sns.countplot(x='cp', hue='target', data=df)
plt.title('Chest Pain Distribution by Target')
plt.show()

Step 16: Show Fasting Blood Sugar Distribution According To Target Variable
This step explores another key clinical feature. It shows the distribution of patients with high fasting blood sugar (fbs > 120 mg/dl) and how this relates to the target variable.
sns.countplot(x='fbs', hue='target', data=df)
plt.title('Fasting Blood Sugar by Target')
plt.show()

Step 17: Check Resting Blood Pressure Distribution
A histogram of trestbps helps us understand the typical blood pressure range of the patients in the dataset and identify any unusual readings.
sns.histplot(df['trestbps'], kde=True)
plt.title('Resting Blood Pressure Distribution')
plt.show()

Step 18: Compare Resting Blood Pressure As Per Sex Column
This box plot compares the distribution of resting blood pressure between male and female patients, allowing us to see if there are significant differences.
sns.boxplot(x='sex', y='trestbps', data=df)
plt.title('Resting Blood Pressure by Gender')
plt.xticks(ticks=[0, 1], labels=['Female', 'Male'])
plt.show()

Step 19: Show Distribution of Serum cholesterol
Similar to blood pressure, this histogram provides an overview of the cholesterol levels within the patient population.
sns.histplot(df['chol'], kde=True)
plt.title('Serum Cholesterol Distribution')
plt.show()

Step 20: Plot Continuous Variables
This final step provides a composite visualization of several key continuous variables, including blood pressure, maximum heart rate, and oldpeak. This helps visualize their overall distributions side-by-side.
fig, axes = plt.subplots(1, 3, figsize=(18, 5))
sns.histplot(df['trestbps'], ax=axes[0], kde=True, color='skyblue')
axes[0].set_title('Resting BP Distribution')
sns.histplot(df['thalach'], ax=axes[1], kde=True, color='lightgreen')
axes[1].set_title('Max Heart Rate Distribution')
sns.histplot(df['oldpeak'], ax=axes[2], kde=True, color='salmon')
axes[2].set_title('Oldpeak Distribution')
plt.tight_layout()
plt.show()

4. Final Dashboard & Key Findings
After completing the EDA, a comprehensive dashboard was created in Tableau to visualize the most impactful insights. The dashboard is designed to be intuitive and focused on answering key questions about heart disease.
Key Dashboard Insights:
●	Age is a major factor: The charts clearly show a higher prevalence of heart disease in older age groups.
●	Cholesterol & Blood Pressure are critical: Patients with heart disease tend to have significantly higher cholesterol and blood pressure readings.
●	Chest Pain & Exercise: The type of chest pain and the presence of exercise-induced angina are strong predictors of a heart disease diagnosis.
●	Major Vessels: The number of major vessels (as revealed by fluoroscopy) is a powerful indicator of disease severity and a strong predictor of the outcome.


View the interactive Dashboard here! - https://public.tableau.com/views/CVD_17587379406300/Dashboard1?:language=en-US&:sid=&:redirect=auth&:display_count=n&:origin=viz_share_link
This project demonstrates the full data analysis workflow, from initial data loading and cleaning to advanced visualization, culminating in a clear and actionable final report.

