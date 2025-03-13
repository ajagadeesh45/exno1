# Exno:1
Data Cleaning Process

# AIM
To read the given data and perform data cleaning and save the cleaned data to a file.

# Explanation
Data cleaning is the process of preparing data for analysis by removing or modifying data that is incorrect ,incompleted , irrelevant , duplicated or improperly formatted. Data cleaning is not simply about erasing data ,but rather finding a way to maximize datasets accuracy without necessarily deleting the information.

# Algorithm
STEP 1: Read the given Data

STEP 2: Get the information about the data

STEP 3: Remove the null values from the data

STEP 4: Save the Clean data to the file

STEP 5: Remove outliers using IQR

STEP 6: Use zscore of to remove outliers

# Coding and Output
# READ CSV FILE HERE
``` py
import numpy as np
import pandas as pd
from google.colab import drive
drive.mount('/content/drive')
```
![image](https://github.com/user-attachments/assets/6b9f2ae2-35f8-4203-afe6-631d73380df1)
``` py
!ls "/content/drive/My Drive/data science"
```
![image](https://github.com/user-attachments/assets/0d0c3324-a5b5-4d6c-a7fc-a3eefb654ba5)
``` py
file_path = "/content/drive/My Drive/data science/Data_set.csv"
df=pd.read_csv(file_path)
df
```
![image](https://github.com/user-attachments/assets/225b0fb4-c83b-4ee2-b28f-fa011237071d)

# DISPLAY THE INFORMATION ABOUT CSV AND RUN THE BASIC DATA ANALYSIS FUNCTIONS
``` py
df.info()
```
![image](https://github.com/user-attachments/assets/7a816605-fac1-4e30-8ab9-a1fc3d0d8e05)
```py
df.head()
```
![image](https://github.com/user-attachments/assets/64e2f69c-c32a-47a1-90f1-04a08f328f3a)
``` py
df.tail()
```
![image](https://github.com/user-attachments/assets/bb1a0a8c-4423-4381-a5ec-e676f9808927)
``` py
df.describe()
```
![image](https://github.com/user-attachments/assets/bd84ff24-44ec-487c-a5c1-5abb0de7da7d)
# CHECK OUT NULL VALUES IN DATA SET USING FUNCTION
``` py
df.isnull()
df
```
![image](https://github.com/user-attachments/assets/dad0ecfa-c35b-4a54-92e0-ab53db75edcc)

# DISPLAY THE SUM ON NULL VALUES IN EACH ROWS

``` py
df.isnull().sum()
py
```
![image](https://github.com/user-attachments/assets/3d02014d-7533-4278-a3b0-b2954efcafa7)
# DROP NULL VALUES
``` py
df = df.dropna()
df
```
![image](https://github.com/user-attachments/assets/9cf6386a-f209-4457-a0e8-fb485dde2e8b)

# FILL NULL VALUES WITH CONSTANT VALUE "O"
``` py
df.fillna(0, inplace=True)
df
```
![image](https://github.com/user-attachments/assets/7e2e0efb-a2c8-4d34-89ff-ca14a1b8eb23)


# FILL NULL VALUES WITH ffill or bfill METHOD
``` py
df.ffill(inplace=True)
df.bfill(inplace=True)
df
```
![image](https://github.com/user-attachments/assets/20fc0f3c-44ce-46d9-9921-6e9e240d0a0e)


# CALCULATE MEAN VALUE OF A COLUMN AND FILL IT WITH NULL VALUES
``` py
column_name=['rating','watchers']
mean_value = df[column_name].mean()
df[column_name].fillna(mean_value, inplace=True)
df
```
![image](https://github.com/user-attachments/assets/4a23beb8-ad71-4fdc-9832-7d2f59a6a10e)

# DROP NULL VALUES
``` py
df.dropna(inplace=True)
df
```
![image](https://github.com/user-attachments/assets/196a5eb9-ea4d-4514-8533-82607b6c3ac2)

``` py
import pandas as pd
import seaborn as sns
import numpy as np
```
``` py
age=[1,3,28,27,25,92,30,39,40,50,26,24,29,94]
af=pd.DataFrame(age)
af
```
![image](https://github.com/user-attachments/assets/dad75cdb-2347-46f9-a567-49f60fd786af)


# USE BOXPLOT FUNCTION HERE TO DETECT OUTLIER
``` py
sns.boxplot(data=af)
```
![image](https://github.com/user-attachments/assets/3577c1ec-0da9-49d4-b634-bceb8c078ae8)

# PERFORM IQR METHOD AND DETECT OUTLIER VALUES
``` py
Q1 = np.percentile(age, 25)  # First quartile (25th percentile)
Q3 = np.percentile(age, 75)  # Third quartile (75th percentile)
IQR = Q3 - Q1
lower_bound = Q1 - (1.5 * IQR)
upper_bound = Q3 + (1.5 * IQR)
```
``` py
lower_bound=Q1 - 1.5*IQR
upper_bound=Q3 + 1.5*IQR
```
``` py
lower_bound
```

![image](https://github.com/user-attachments/assets/38ffa924-be61-477e-91e2-b848ae724338)
```py
upper_bound
```
![image](https://github.com/user-attachments/assets/81e12814-99d1-43fa-93a7-de6340790fac)
# REMOVE OUTLIERS
``` py
outliers=[x for x in age if x<lower_bound or x>upper_bound]
outliers
```
![image](https://github.com/user-attachments/assets/2c4bb874-66c6-4e56-9be5-ce32a1c629a5)
```py
af=af[((af>=lower_bound)&(af<=upper_bound))]
af
```

![image](https://github.com/user-attachments/assets/e89d3eab-5603-4d7d-86a5-6626017b5584)
```py
af.dropna()
```

![image](https://github.com/user-attachments/assets/8e11b0be-21d5-45cd-ba0b-ba6f082710f5)
# USE BOXPLOT FUNCTION HERE TO CHECK OUTLIER IS REMOVED
```py
sns.boxplot(data=af)
```

![image](https://github.com/user-attachments/assets/91a03c3d-dbf5-4d38-a605-ce3b8d630633)

```py
from scipy import stats
import matplotlib.pyplot as plt
```
```py
data=[1,12,15,18,21,24,27,30,33,36,39,42,45,48,51,54,57,60,63,66,69,72,75,78,81,84,87,90,93,96,99,158]
df=pd.DataFrame(data, columns=['Data'])
df
```

![image](https://github.com/user-attachments/assets/63f53592-361a-4171-8013-560468cf0180)


# USE BOXPLOT FUNCTION HERE TO DETECT OUTLIER
```py
sns.boxplot(data=df, y='Data')
plt.show()
```

![image](https://github.com/user-attachments/assets/68298aba-738c-4bc3-955a-830d484d97c1)
# PERFORM Z SCORE METHOD AND DETECT OUTLIER VALUES
``` py
z_scores = stats.zscore(df['Data'])
outliers_z=df[(z_scores > 3) | (z_scores < -3)]
outliers_z
```
![image](https://github.com/user-attachments/assets/f03813ff-ab56-48a1-9ede-14900b13b471)

# REMOVE OUTLIERS
``` py
threshold = 3
df_clean = df[(z_scores < threshold) & (z_scores > -threshold)]
```

# USE BOXPLOT FUNCTION HERE TO CHECK OUTLIER IS REMOVED
``` py
sns.boxplot(data=df_clean, y='Data')
```
![image](https://github.com/user-attachments/assets/73b7ff2e-625f-45cb-8bd5-3a7a2bdd7b00)









# Result
         Thus, We have read the given data, performed data cleaning, and saved the cleaned data to a file.
           
         
