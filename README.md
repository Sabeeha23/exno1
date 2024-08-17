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
                            Data Cleaning
```
import pandas as pd
df=pd.read_csv('/content/SAMPLEIDS.csv')
df
```
![alt text](<Screenshot 2024-08-17 110103.png>)


```
df.isnull().sum()
```
![alt text](<Screenshot 2024-08-17 110650.png>)


```
df.isnull().any()
```
![alt text](<Screenshot 2024-08-17 110659.png>)

```
df.dropna()
```
![alt text](<Screenshot 2024-08-17 110713.png>)

```
df.fillna(0)
```
![alt text](<Screenshot 2024-08-17 110724.png>)


```
df.fillna(method = 'ffill')
```

![alt text](<Screenshot 2024-08-17 110743.png>)

```
df.fillna(method = 'bfill')
```
![alt text](<Screenshot 2024-08-17 110756.png>)


```
df_dropped = df.dropna()
df_dropped
```
![alt text](<Screenshot 2024-08-17 110807.png>)

```
df.fillna({'GENDER':'FEMALE','NAME':'SABEEHA','ADDRESS':'CHITTOOR','M1':98,'M2':87,'M3':76,'M4':92,'TOTAL':305,'AVG':89.999999})
```
![alt text](<Screenshot 2024-08-17 110830.png>)


                         IQR(Inter Quartile Range)
```
import pandas as pd
```
```
ir = pd.read_csv('/content/iris.csv')
ir
```

![alt text](<Screenshot 2024-08-17 110846.png>)

```
ir.describe()
```
![alt text](<Screenshot 2024-08-17 110853.png>)

```
import seaborn as sns
sns.boxplot(x='sepal_width',data=ir)
```
![alt text](<Screenshot 2024-08-17 110901.png>)

```
c1=ir.sepal_width.quantile(0.25)
c3=ir.sepal_width.quantile(0.75)
iq = c3-c1
print(c3)
```
![alt text](<Screenshot 2024-08-17 110908.png>)

```
rid = ir[((ir.sepal_width < (c1 - 1.5 * iq)) | (ir.sepal_width > (c3 + 1.5 * iq)))]
rid['sepal_width']
```
![alt text](<Screenshot 2024-08-17 110913.png>)

```
delid =ir[~((ir.sepal_width < (c1 - 1.5 * iq)) | (ir.sepal_width > (c3 + 1.5 * iq)))]
delid
```
![alt text](<Screenshot 2024-08-17 110920.png>)

```
sns.boxplot(x='sepal_width', data=delid)
```
![alt text](<Screenshot 2024-08-17 110928.png>)

                                 Z- Score
```
import matplotlib.pyplot as plt
import pandas as pd
import numpy as np
import scipy.stats as stats
```

```
dataset = pd.read_csv('/content/heights.csv')
dataset
```
![alt text](<Screenshot 2024-08-17 110936.png>)

```
df = pd.read_csv('/content/heights.csv')
q1 = df['height'].quantile(0.25)
q2 = df['height'].quantile(0.5)
q3 = df['height'].quantile(0.75)
```

```
iqr = q3 - q1
iqr
```
![alt text](<Screenshot 2024-08-17 110946.png>)
```
low = q1 - 1.5 * iqr
low
```
![alt text](<Screenshot 2024-08-17 110951.png>)
```
high = q3 + 1.5 * iqr
high
```
![alt text](<Screenshot 2024-08-17 110956.png>)
```
df1 = df[(df['height'] >= low) & (df['height'] <= high)]
df1
```
![alt text](<Screenshot 2024-08-17 111002.png>)
```
z = np.abs(stats.zscore(df['height']))
z
```
![alt text](<Screenshot 2024-08-17 111029.png>)
```
df1 = df[(z < 3)]
df1
```
![alt text](<Screenshot 2024-08-17 111036.png>)

# Result
Thus we have cleaned the data and removed the outliners by 
detection using  IQR and Z-Score method.

