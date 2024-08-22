<h1 align="center">Ex. 1   Data Cleaning and Outlier Detection & Removal</h1>


## AIM
### To read the given data and perform data cleaning and save the cleaned data to a file.

## Explanation
### Data cleaning is the process of preparing data for analysis by removing or modifying data that is incorrect ,incompleted , irrelevant , duplicated or improperly formatted. Data cleaning is not simply about erasing data ,but rather finding a way to maximize datasets accuracy without necessarily deleting the information.

## Algorithm
### STEP 1
#### Read the given Data

### STEP 2
#### Get the information about the data

### STEP 3 
#### Remove the null values from the data

### STEP 4
#### Save the Clean data to the file

### STEP 5
#### Remove outliers using IQR

### STEP 6
#### Use zscore of to remove outliers

## Coding 

<h3 align="center">Data Cleaning</h3>

```py
import pandas as pd
df=pd.read_csv("SAMPLEIDS.csv")
df
```
![image](https://github.com/DHINESH-SEC/exno1/assets/118351569/dfb891f0-1ff6-4086-be44-00b49cccf68f)

```py
df.isnull().sum()
```
![image](https://github.com/DHINESH-SEC/exno1/assets/118351569/1e365842-4e54-4d99-ac19-787632ade990)


```py
df.isnull().any()
```
![image](https://github.com/DHINESH-SEC/exno1/assets/118351569/9c2b7469-5387-4371-af5a-f3caf3177983)

```py
df.dropna()
```
![image](https://github.com/DHINESH-SEC/exno1/assets/118351569/b93072ae-2712-4890-a9bc-5c0373f72a1e)

```py
df.fillna(0)
```
![image](https://github.com/DHINESH-SEC/exno1/assets/118351569/0db06bf2-9c0e-4feb-8c4e-3b24eec02d94)

```py
df.fillna(method = 'ffill')
```
![image](https://github.com/DHINESH-SEC/exno1/assets/118351569/00129275-aa44-426f-b039-37e840af5144)

```py
df.fillna(method = 'bfill')
```
![image](https://github.com/DHINESH-SEC/exno1/assets/118351569/e00a969f-9084-4af1-9d6a-aad539592449)

```py
df_dropped = df.dropna()
df_dropped
```

![image](https://github.com/DHINESH-SEC/exno1/assets/118351569/3d6b105d-83dc-46cd-9cc6-5a8ab32542a6)

```py
df.fillna({'GENDER':'MALE','NAME':'SRI','ADDRESS':'POONAMALEE','M1':98,'M2':87,'M3':76,'M4':92,'TOTAL':305,'AVG':89.999999})
```
![image](https://github.com/DHINESH-SEC/exno1/assets/118351569/9f913d9b-975a-4b3f-87ff-f4491bdebe83)


<hr><hr>

<h3 align="center">IQR(Inter Quartile Range)</h3>

```py
import pandas as pd
```
```py
ir=pd.read_csv('iris.csv')
ir
```
![image](https://github.com/DHINESH-SEC/exno1/assets/118351569/f6f3cc2e-76cb-4f8f-9239-0ddf27fc1190)

```py
ir.describe()
```
![image](https://github.com/DHINESH-SEC/exno1/assets/118351569/51edfdf6-d999-4cc4-ac15-04bc9594df82)

```py
sns.boxplot(x='sepal_width',data=ir)
```
![image](https://github.com/DHINESH-SEC/exno1/assets/118351569/b68ee748-f275-44fe-8cc8-6f19b3e4a386)

```py
c1=ir.sepal_width.quantile(0.25)
c3=ir.sepal_width.quantile(0.75)
iq=c3-c1
print(c3)
```
![image](https://github.com/DHINESH-SEC/exno1/assets/118351569/69d60917-d227-4367-b0ef-ff7ce6e959d8)

```py

rid=ir[((ir.sepal_width<(c1-1.5*iq))|(ir.sepal_width>(c3+1.5*iq)))]
rid['sepal_width']
```
![image](https://github.com/DHINESH-SEC/exno1/assets/118351569/57c049f2-3948-4a40-99b2-af0c54f9395d)

```py
delid=ir[~((ir.sepal_width<(c1-1.5*iq))|(ir.sepal_width>(c3+1.5*iq)))]
delid
```
![image](https://github.com/DHINESH-SEC/exno1/assets/118351569/a1e4026a-3a97-41c7-81c9-92b4ca4997fa)

```py
sns.boxplot(x='sepal_width',data=delid)
```
![image](https://github.com/DHINESH-SEC/exno1/assets/118351569/1e19ac51-2803-4a07-9e0b-d7c2b7583882)

<hr><hr>

<h3 align="center">Z-Score</h3>

```py
import matplotlib.pyplot as plt
import pandas as pd
import numpy as np
import scipy.stats as stats
```
```py
dataset=pd.read_csv("heights.csv")
dataset
```
![image](https://github.com/DHINESH-SEC/exno1/assets/118351569/39c53e03-1ea4-4852-b611-cfd529f2596b)

```py
df = pd.read_csv("heights.csv")
q1 = df['height'].quantile(0.25)
q2 = df['height'].quantile(0.5)
q3 = df['height'].quantile(0.75)
```

```py
iqr = q3-q1
iqr
```
![image](https://github.com/DHINESH-SEC/exno1/assets/118351569/2d26a119-fec1-4349-a5d8-de847121ab75)

```py
low = q1 - 1.5*iqr
low
```
![image](https://github.com/DHINESH-SEC/exno1/assets/118351569/79354921-d9ba-439f-877f-592a0a4ce18e)

```py
high = q3 + 1.5*iqr
high
```
![image](https://github.com/DHINESH-SEC/exno1/assets/118351569/cc3cb025-3fef-4ce6-aa06-4f955c68c37b)


```py
df1 = df[((df['height'] >=low)& (df['height'] <=high))]
df1
```
![image](https://github.com/DHINESH-SEC/exno1/assets/118351569/98644856-3b03-4f58-b361-75be46820c24)

```py
z = np.abs(stats.zscore(df['height']))
z
```
![image](https://github.com/DHINESH-SEC/exno1/assets/118351569/fa7b418c-9efb-4118-9a21-7f271d0fb1d5)

```py
df1 = df[z<3]
df1
```
![image](https://github.com/DHINESH-SEC/exno1/assets/118351569/08be1792-3872-4f44-922f-ff50c606b79e)

## Result
Thus we have cleaned the data and removed the outliers by detection using IQR and Z-score method.
