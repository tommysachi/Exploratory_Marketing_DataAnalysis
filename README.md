# Marketing Data Analysis
The Objectives of this EDA are to describe the Customer Profile, the Correlation between Customer Profile and the Products offered by the Market, the Best Market Source and Campaign. So, in the future, the Market will apply or make decision based on historical data analysis. 

**1. Datasets Explanation**

This Market Datasets gathered from July 2012 until June 2014, with the following content as describe below :
- Year of Birth, Education, Marital Status, Income, Kidhome, Teenhome (Number of Children) >> Customer Profile
- Date Customer >> When the Customer joined as member for the first time
- Recency >> Days after the last transaction occured
- Mnt Wines, Fruits, Meat Products, Fish Products, Sweet Product, Gold Products >> Total Spending Amount of each Product Category
- Num Web Purchase, Store Purchase, Catalog Purchase >> Number of how the customer made the transaction
- Num Deal Purchase >> Number of how many times the customer made a transaction with discount
- Num Web Visit Month >> Number of times, the customer visit the Corporate Website during last month
- Accepted Cmp >> To shown whether the customer accept the offer from campaign
- Complain >> Number of times the customer made a complain
- Country >> Country of the customer

**2. Data Preparation**
- Check the Data Type

```python
df.info()
```
![Data Type](https://github.com/tommysachi/Exploratory_Marketing_DataAnalysis/blob/main/Table%20%26%20Visual/Data%20Type.JPG)

- Check the Missing Value and Drop Duplicates

```python
df.drop_duplicates()
```
_There was 24 duplicate datas in Income Column._

![Drop Duplicates](https://github.com/tommysachi/Exploratory_Marketing_DataAnalysis/blob/main/Table%20%26%20Visual/Duplicate%20Data.JPG)


- Investigate the Data Description (Continuous Numerical and Object Type) - Changing the Data Type
```python
df['ID'] = df['ID'].astype('object')
df['Year_Birth'] = df['Year_Birth'].astype('object')
df['Kidhome'] = df['Kidhome'].astype('object')
df['Teenhome'] = df['Teenhome'].astype('object')
df['Recency'] = df['Recency'].astype('object')
df['AcceptedCmp3'] = df['AcceptedCmp3'].astype('object')
df['AcceptedCmp4'] = df['AcceptedCmp4'].astype('object')
df['AcceptedCmp5'] = df['AcceptedCmp5'].astype('object')
df['AcceptedCmp1'] = df['AcceptedCmp1'].astype('object')
df['AcceptedCmp2'] = df['AcceptedCmp2'].astype('object')
df['AcceptedCmp6'] = df['AcceptedCmp6'].astype('object')
df['Complain'] = df['Complain'].astype('object')
```

![Data Description](https://github.com/tommysachi/Exploratory_Marketing_DataAnalysis/blob/main/Table%20%26%20Visual/Transform%20Data%20Type.JPG)

**3. Date and Time Conversion and Extraction**

```python
df['Dt_Customer']=df['Dt_Customer'].astype('datetime64')

df['Dt_Customer'] = pd.to_datetime(df['Dt_Customer'],format='%d/%m/%Y')

date = df['Dt_Customer'].dt

df['Month'] = date.month
df['Month_Name'] = date.month_name()
df['Year'] = date.year
```
_Adding Month Column, Month Name Column, and Year Column._

**4. Grouping**

_Adding Age Column, and Grouping into 4 Categories as well as Income Grouping_

```python
df['Age'] = 2021 - df['Year_Birth']

def AgeGrouping(x):
    if (x >= 25) & (x <= 35):
        return '(25-35)'
    elif (x >= 36) & (x <= 45):
        return '(36-45)'
    elif (x >= 46) & (x <= 55):
        return '(46-55)'
    elif (x > 55):
        return '(>55)'

df['Age_Grouping'] = df['Age'].apply(AgeGrouping)
```

```python
def IncomeGrouping(x):
    if (x>=1500) & (x<=25000):
        return '(1500-25000)'
    elif (x>25000) & (x<=50000):
        return '(25001-50000)'
    elif (x>50000) & (x<=75000):
        return '(50001-75000)'
    elif (x>75000) & (x<=100000):
        return '(75001-100000)'
    else :
        return '(>100000)'

df['Income_Grouping'] = df['Income'].apply(IncomeGrouping)
```
**4. Customer Profile**

_Using pandas Crosstab and Groupby, we analyzed that the Customer Profile from Dataset as shown below._

![By Age](https://github.com/tommysachi/Exploratory_Marketing_DataAnalysis/blob/main/Table%20%26%20Visual/Customer%20Profile%20(Age).JPG)

![By Graduation](https://github.com/tommysachi/Exploratory_Marketing_DataAnalysis/blob/main/Table%20%26%20Visual/Customer%20Profile%20(Graduation%20Status).JPG)

![By Marital](https://github.com/tommysachi/Exploratory_Marketing_DataAnalysis/blob/main/Table%20%26%20Visual/Customer%20Profile%20(Marital%20Status).JPG)

![By Kids](https://github.com/tommysachi/Exploratory_Marketing_DataAnalysis/blob/main/Table%20%26%20Visual/Customer%20Profile%20(Kids).JPG)

![By Teens](https://github.com/tommysachi/Exploratory_Marketing_DataAnalysis/blob/main/Table%20%26%20Visual/Customer%20Profile%20(Teens).JPG)

![By Income](https://github.com/tommysachi/Exploratory_Marketing_DataAnalysis/blob/main/Table%20%26%20Visual/Customer%20Profile%20(Income).JPG)

_From these tables, we can simply analyzed that most of the Customer was a liitle bit older with 68% above 46 years old. Approximately around 50% of the Customer was Bachelor's Graduate and their marital status was Married or even Living Together. Most of them didn't have any kids and teenagers, but still, if they have kid or teen, most of them only have one child. Most of their Income ranging from 25000-75000._

**5. Correlation Between Customer Profile and Products Offered**

```python
df[['MntWines','MntFruits','MntMeatProducts','MntFishProducts','MntSweetProducts','MntGoldProds','Year']].groupby('Year',as_index=0).agg('sum')
```
![Correlation 1](https://github.com/tommysachi/Exploratory_Marketing_DataAnalysis/blob/main/Table%20%26%20Visual/Product%20Category.JPG)

![Correlation 2](https://github.com/tommysachi/Exploratory_Marketing_DataAnalysis/blob/main/Table%20%26%20Visual/Product%20Category%20(Graph).JPG)

_These table and graph shown us how much spending on each Products Category yearly. Wine Products and Meat Products were the most compared with the others._

![Correlation 3](https://github.com/tommysachi/Exploratory_Marketing_DataAnalysis/blob/main/Table%20%26%20Visual/Two%20Major%20Category%20(By%20Age).JPG)

![Correlation 4](https://github.com/tommysachi/Exploratory_Marketing_DataAnalysis/blob/main/Table%20%26%20Visual/Two%20Major%20Category%20(By%20Kids%20and%20Teens).JPG)

![Correlation 5](https://github.com/tommysachi/Exploratory_Marketing_DataAnalysis/blob/main/Table%20%26%20Visual/Two%20Major%20Category%20(By%20Marital%20Status).JPG)

![Correlation 6](https://github.com/tommysachi/Exploratory_Marketing_DataAnalysis/blob/main/Table%20%26%20Visual/Two%20Major%20Category%20(By%20Income).JPG)

_By these two top categories (Wine and Meat), we can see the correlation between them with Customer Profile. Most of them are above 55 years old, don't have any kids, and married, with the Income above 50000-100000._

 **6. Market Source**

 ![Market Source](https://github.com/tommysachi/Exploratory_Marketing_DataAnalysis/blob/main/Table%20%26%20Visual/Market%20Source.JPG)

 _From this we can see that, many of the transactions still closed at the offline stores rather than website_

 ![Number of Web Visit](https://github.com/tommysachi/Exploratory_Marketing_DataAnalysis/blob/main/Table%20%26%20Visual/Web%20Visit.JPG)

 _If the customer visit the website more often, it will resulting on more transactions done. But it was limited until 9 visits last month, above than that there was an error (maybe customer still on consideration stage)._

 ![Campaign](https://github.com/tommysachi/Exploratory_Marketing_DataAnalysis/blob/main/Table%20%26%20Visual/Campaign.JPG)

_Most successful marketing campaign was the 6th, even in every group of age. But in these datasets, we cant actually know the detail of the marketing campaign._

**7. Review and Suggestion**
- This Market should focus on improving their Wine and Meat Products, because of it was their specialty.
- They should do Marketing Campaign 6, because of the succeed with target market based on the Customer Profile that made the most transaction (above 45 years old, did't have kids or maximum 1, was married, and income above 50000)
- They should notice their offline store, because still many transactions made at the stores. But they shouldn't forget to focus on their Website Development and Discount from Online Purchases, as shown from the analysis, the difference between Transactions from Website and Store were not significant, and we were going forward for Industry 4.0 as one of the reason.
