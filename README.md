# python_p2
## Performing The Following functions
* How to fetch random samples from the Dataset?
* isin
* between
* unique
* dropna
* replace
* duplicated
* drop_dupplicates
* astype
* apply
* What is Univariate analysis?
* What is Bivariate analysis?
* Memory Optimization

  ### Importing required python libraries
  
```
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
```
**Read the Adult dataset**
>data=pd.read_csv(r"C:\Users\mahes\Desktop\adult.csv.zip",low_memory=False)

### Let's See The Adult Dataset
>data
>
**Display the first 10 rows of the dataset**
>data.head(10)
>
**Display the last 5 rows of the dataset**
>data.tail(5)

**Find shape of our dataset(No of rows and no of columns)**
>data.shape

**Getting information about our dataset like total no of rows,total no of columns,datatype of each column 
and memory requirement**
>data.info()

**Fetch random samples from the dataset(50%)**
>data1=data.sample(frac=0.50,random_state=111)
>data1

**Check nullvalues in the Dataset**
>data.isnull()

>data.isnull().sum(axis=0) # (Checking null values in columns)

>data.isnull().sum(axis=1) # (Checking null values in rows)

>sns.heatmap(data.isnull()) # (Showing null values in visually using heatmap method)

 **Checking how many ? in the occupation**
 >data.isin(['?']).sum()

>import numpy as np

>data.columns

**Replacing '?' with null using np**
```
data['workclass']=data['workclass'].replace('?',np.nan)
data['occupation']=data['occupation'].replace('?',np.nan)
data['native-country']=data['native-country'].replace('?',np.nan)
data
```
**Checking how many null values in each column**
>data.isnull().sum()

>sns.heatmap(data.isnull()) # (Visually showing null values of the dataset

**Drop All Missing Values**
>per_missing=data.isnull().sum()*100/len(data)

>per_missing

>data.dropna(how='any',inplace=True)
>data

**Let's Check shape of the dataset After removing null values**
>data.shape

**Check for Duplicate data and drop them**
```
dup_dt=data.duplicated().any()
print("Are there any duplicated value:",dup_dt)
data=data.drop_duplicates()
```
**Let's Check shape of the dataset After removing duplicate values**
>data.shape

**Get Overall Statastics  about the dataframe**
>data.describe(include='all')

**Let's check the unique values of the education column of the data**
```
data.columns
data['education'].unique()
data['educational-num'].unique()
```
**Drop the Columns education-num,captain-gain and captain-loss**
```
data.columns
data=data.drop(['educational-num','capital-gain','capital-loss'],axis=1)
data.columns
```
### Univariate Analysis
**What is the distribution of the Age column**
>data['age'].describe()

>data['age'].hist() # Visually showing employee age graph

**Find Total no of persons having age between 17 to 48(inclusive) using Between method**
>sum((data['age']>=17) & (data['age']<=48))

>sum(data['age'].between(17,48))

**Describing the columns of the dataset**
```
data.columns
data['workclass'].describe()
plt.figure(figsize=(10,10))
data['workclass'].hist() # histogram for the workclass column
```
**How many persons having Bachelors or Masters Degree**
```
data.columns
data['education']
flt1=data['education']=='Bachelors'
flt2=data['education']=='Masters'
data[flt1 | flt2]
len(data[flt1 | flt2]) # checking total no of masters and bachelors qualified employees
sum(data['education'].isin(['Bachelors','Masters'])) # checking total no of masters and bachelors qualified employees using sum method
```
**Bivariate Analysis**
>data.columns

>sns.boxplot(x='income',y='age',data=data) # Visually showing relation between age and income column
**Checking income column**
```
data.columns
data['income'].unique()
data['income'].value_counts()
sns.countplot(x='income',data=data) # Visually showing quantity of employee's income >=50k and <=50k
```
**Replace Salary Values['<=50K','>=50K'] with 0 and 1**
```
def salary_data(sal): # Defyning salary_data function
    if sal=='<=50K':
        return 0
    else:
        return 1
data['encoded_income']=data['income'].apply(salary_data) # calling or applying function
data.head(1) # Checking head of the dataset
```
**Which Workclass Getting Highest salary**
>data.groupby("workclass")["encoded_income"].agg("mean").sort_values(ascending=False)

**How Has Better Chance To Get Salary>=50K Male or Female**
>data.groupby("gender")["encoded_income"].agg("mean").sort_values(ascending=False)

**Convert workclass Columns Datatype To Category Datatype**
```
data.info()
data['workclass']=data['workclass'].astype('category')
data.info()
```





