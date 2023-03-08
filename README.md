# Panda-basic
Basic filtering and modifying dataset using Pandas along with basic plotting using matplotlib and seaborn

```python
import pandas as pd
```


```python
pd.__version__
```


```python
pd.show_versions()
```


```python
# this will open all the options that you can use when reading your file using pandas
pd.read_csv?
```


```python
oo = pd.read_csv(r'A:\Python\Pandas essential\Ex_Files_Pandas_EssT\ExerciseFiles\data\olympics.csv', skiprows=4)

# skiprows ignore the first couple of rows on Excel that do not have any info for our table
# if your data set is not in the first sheet of your csv file, you can use sheet_name = 'your-sheet_name' to import the right worksheet

```


```python
oo.head()
# default rows for head() is 5, you can change it by putting the number of rows you want
```


```python
# alternatively you can use command below to see random rows from your dataset

oo.sample(5)
```

## What if you want to be able to see all the rows of your dataset?

you can use the set_option along with display.max.rows or display.max.columns


```python
oo.shape
```


```python
pd.set_option('display.max_rows', 29216)
# this option is usually good if your rows are less than 500
pd.set_option('display.max_columns', 10)
```


```python
oo.info()

# pay attention to 29216 entires that is consistent along all variables (no missing), also data types that there is one integer
# and everything else is object (character)
```


```python
oo.columns
# for the list of columns
```

# Working with Series


```python
# Let's get an understanding of distribution of observations in each city
oo['City'].value_counts()
```


```python
oo.Athlete
```


```python
#when we want to look at multiple columns in a series we use double brackets
oo[['City', 'Edition', 'Athlete']]

# if you want to create a new dataset using selected columsn df1 = oo[['City', 'Edition', 'Athlete']]
```


```python
df1 = oo[['City', 'Edition', 'Athlete']]
df1.head()
```


```python
type(oo[['City', 'Edition', 'Athlete']])
```


```python
type(oo.City)
```


```python
oo.shape[0]
```


```python
oo.shape[1]
```


```python
oo.head(3)
```


```python
oo.tail(5)
```


```python
oo.Edition.value_counts()
```

# Filtering in Pandas


```python
# what if we want to see only the olympics after 2000?
oo[oo['Edition'] > 1996]
```


```python
# what if we are only interested in medals achieved by certain countries' athlethes?

Countries = ['USA', 'MEX', 'CAN']
oo[oo['NOC'].isin(Countries)]
```


```python
# Look for string variable that contain certain name

oo[oo['Athlete'].str.contains('Thomas')]
```

## Filtering using loc (location) or iloc (integer location)


```python
oo.head()
```


```python
# let's first change the index column
oo1 = oo.set_index('City')
oo1.head()
```


```python
pd.set_option('display.max_rows', 10)
```


```python
oo1.filter(items = ['Edition', 'NOC', 'Gender'])
# the default has axis = 1 which represents the columns of the dataset. If we write axis = 0 we get all the columns
```


```python
oo1.filter(items = ['Edition', 'NOC', 'Gender'], axis = 0)
```


```python
oo1.filter(like = ['Athens'], axis = 0)
```


```python
oo1.loc['Athens']
```


```python
oo1.iloc[1830]
```


```python
oo
```


```python
oo[oo['Edition'] < 1980].sort_values(by='Edition', ascending=False) # ascending false make it higher to lower
```


```python
oo[oo['Edition'] < 1980].sort_values(by=['Edition', 'Sport'], ascending=False)
# this will sort based on edition and sport from high to low 
```


```python
oo[oo['Edition'] < 1980].sort_values(by=['Sport','Edition'], ascending=[False, True])
# here we changed the order. Our sports are from high to low and our edition are from low to high
```


```python
oo.Gender.value_counts(ascending=True,dropna=False)
```


```python
ath=oo.Athlete.sort_values
ath
```


```python
type(oo.Gender=='Men')
```


```python
oom = oo[oo.Gender=='Men']
oom
```


```python
# let's look at all the gold winners
oo[oo.Medal =='Gold']
```


```python
# How about all the all the gold winners who are women
oo[(oo.Medal =='Gold') & (oo.Gender =='Women')]
```


```python
# all the athlete whos names are Florence and won a bronze
oo[(oo.Athlete.str.contains('Florence')) & (oo.Medal == 'Bronze')]
```


```python
oo[oo.Athlete.str.contains('OWENS')]   #REMEMBER IT IS CASE SENSITIVE
```


```python
# Which countries won the most medals?
oo.NOC.value_counts().head(3)
```


```python
# Which countries won the least medals?
oo.NOC.value_counts().tail(3)
```


```python
# What if we are looking for specific athlete
cl = oo[oo.Athlete=='LEWIS, Carl']
cl
```


```python
# how to know what even carl lewis won medal

cl.Event.value_counts()
```

## Question: Which country has won the most men's Gold medals in singles Badminton over the years? Sort the results alphabetically by the Player's Names.



```python
oo.Sport.value_counts()                  
```


```python
oo[oo['NOC'].sort_values(by='Medal')]
```


```python
gbm =oo[(oo.Medal == 'Gold') & (oo.Gender == 'Men') & (oo.Sport == 'Badminton')]
gbm
```


```python
gbm =oo[(oo.Medal == 'Gold') & (oo.Gender == 'Men') & (oo.Sport == 'Badminton') & (oo.Athlete.str.contains('oo'))]
gbm
```


```python
## Now, let's sort them

gbm.sort_values(by=['Athlete'])
```


```python
gbm.NOC.value_counts()
```

## Which three countries have won the most medals in recent years (1984 - 2008)


```python
ry = oo[(oo.Edition >=1984) & (oo.Edition <=2008)]
ry
```


```python
ry.NOC.value_counts()
```


```python
ry.NOC.value_counts().head(3)
```

## Display the male gold medal winners for the 100m Track & Field sprint over the years. List the results starting with the most recent. Show the Olympic City, Edition, Athlete and the country they represent. 


```python
gmh = oo[(oo.Gender == 'Men') & (oo.Medal=='Gold') & (oo.Event=='100m')]
gmh
```


```python
gmh.sort_values('Edition', ascending=False)
```


```python
gmh.sort_values('Edition', ascending=False)[['City', 'Edition', 'Athlete', 'NOC']]
```

# Basic Plotting


```python
import matplotlib.pyplot as plt
%matplotlib inline  
```

## What were the different sports in the first olympics? Plot them using different graphs.


```python
oo
```


```python
fo = oo[oo.Edition == 1896]
fo.head()
```


```python
fo.Sport.value_counts().plot()
```


```python
fo.Sport.value_counts().plot(kind='bar')
```


```python
fo.Sport.value_counts().plot(kind='barh')
```


```python
fo.Sport.value_counts().plot(kind='pie')
```

## Plot colors



```python
fo.Sport.value_counts().plot(kind='barh', color='maroon')
```

## Figure size


```python
fo.Sport.value_counts().plot(figsize=(10,3))
```

## Colormaps


```python
fo.Sport.value_counts().plot(kind='pie', colormap='Pastel1')
```

# Seaborn basic plotting


```python
import seaborn as sns
```

## How many medals have been won by men and women in the history of the Olympics. How many gold, silver, and bronze medals were won for each gender?


```python
sns.countplot(x='Medal', data=oo)
```


```python
sns.countplot(x='Medal', data=oo, hue='Gender')
```


```python
oo.head()
```


```python
c2008 = oo[(oo.NOC == 'CHI') & (oo.Edition == '2008')]
c2008
```


```python
oo[oo.NOC.str.contains('CH')]
```


```python
c2008 = oo[(oo.NOC == 'CHN') & (oo.Edition == 2008)]
c2008
```


```python
c2008.Medal.value_counts().plot()
```


```python
c2008.Gender.value_counts().plot(kind='bar')
```


```python
sns.countplot(x='Medal', data=c2008)
```


```python
sns.countplot(data=oo, x='Gender')
```


```python
sns.countplot(data=oo, x='Gender', palette='bwr')
```


```python
sns.countplot(x='Medal', data=c2008, hue='Gender')
```


```python
sns.countplot(x='Medal', data=c2008, hue='Gender', palette='bwr', order=['Gold', 'Silver', 'Bronze'])
```


```python
oo.head()
```


```python
type(oo.index)
```


```python
oo.index[100]
```

### Set_index()


```python
oo.set_index('Athlete')
```


```python
oo.head()
```


```python
oo.set_index('Athlete', inplace=True)
```


```python
oo.reset_index(inplace=True)
```


```python
ath = oo.set_index('Athlete')
ath
```


```python
ath.reset_index(inplace=True)
```


```python
ath
```


```python
ath.set_index('Athlete', inplace=True)
ath.head()
```


```python
ath.sort_index(inplace=True)
ath.head()
```


```python
ath.sort_index(inplace=True, ascending=False)
ath.head()
```

### loc[...]


```python
oo.set_index('Athlete', inplace=True)
```


```python
oo.loc['BOLT, Usain']
```


```python
oo.reset_index(inplace=True)
```


```python
oo.head()
```


```python
oo[oo.Athlete == 'BOLT, Usain']
```

### iloc[...]


```python
oo.iloc[1700]
```


```python
oo.iloc[[1542, 2390, 6000, 15000]]
```


```python
oo.iloc[1:4]
```


```python
oo.head()
```


```python
oo.Edition.value_counts().plot(kind='barh')
```


```python
oo.Edition.value_counts().sort_index()
```


```python
oo.Edition.value_counts().sort_index().plot()
```


```python
lo = oo[oo.Edition == 2008]
lo
```


```python
noc = pd.read_csv(r'A:\Python\Pandas essential\Ex_Files_Pandas_EssT\ExerciseFiles\data\Summer Olympic medallists 1896 to 2008 - IOC COUNTRY CODES.csv')
noc.head()
```


```python
noc[noc['Country'] != noc['Country.1']]  #these two columns are the same
```


```python
noc.set_index('Int Olympic Committee code', inplace=True)
```


```python
noc.head()
```


```python
medal_2008 = lo.NOC.value_counts()
medal_2008
```


```python
noc['medal_2008'] = medal_2008
noc.head()
```


```python
noc[noc.medal_2008.isnull()]
```


```python
noc.medal_2008.isnull().sum()
```

# Groupby


```python
oo.groupby('Edition')
```


```python
type(oo.groupby('Edition'))
```


```python
list(oo.groupby('Edition'))
```


```python
for group_key, group_value in oo.groupby('Edition'):
    print(group_key)
    print(group_value)
```


```python
oo.groupby('Edition').size()
```


```python
oo.groupby(['Edition', 'NOC', 'Medal']).agg(['min', 'max', 'count'])
```


```python
oo.groupby(['Edition', 'NOC', 'Medal']).agg( 'count')
```


```python
oo.groupby(['Edition', 'NOC', 'Medal']).agg({'Edition': ['min', 'max', 'count']})
```


```python
oo.loc[oo.Athlete == 'LEWIS, Carl'].groupby('Athlete').agg({'Edition' : ['min', 'max', 'count']})
```


```python
oo.head()
```


```python
oo.groupby('Edition').agg({'Medal': ['count']}).plot()
```


```python
oo.groupby('Edition').size().plot()
```


```python
oo.groupby(['Edition', 'NOC']).agg({'Edition': ['min', 'max', 'count']})
```


```python
oo.groupby('NOC').agg({'Edition': ['min', 'max', 'count']})
```


```python
oo.head()
```


```python
usag = oo[(oo.NOC == 'USA') & (oo.Medal == 'Gold')]
usag
```


```python
usag.groupby('Gender').agg({'Medal': ['count']}).plot(kind='barh')
```


```python
usag.groupby(['Edition', 'Gender']).size()
```


```python
usag.groupby(['Edition', 'Gender']).size().unstack('Gender', fill_value=0).plot()
```


```python
oo.groupby(['Athlete', 'Medal']).size()
```


```python
g = oo.groupby(['Athlete', 'Medal']).size().unstack('Medal', fill_value=0)
g
```


```python
g.sort_values(['Gold', 'Silver', 'Bronze'], ascending=False)[['Gold', 'Silver', 'Bronze']].head().plot(kind='barh')
```


```python

```
