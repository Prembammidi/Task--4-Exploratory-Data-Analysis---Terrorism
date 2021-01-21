# Task--4-Exploratory-Data-Analysis---Terrorism


BAMMIDI PREM KUMAR¶
GRIP THE SPARKS FOUNDATION
TASK4: Exploratory Data Analysis - Terrorism - Perform ‘Exploratory Data Analysis’ on dataset ‘Global Terrorism’
In [2]:
import pandas as pd
import numpy as np
import plotly.offline as py
import plotly.graph_objs as go
import matplotlib.pyplot as plt
import math
import seaborn as sns
In [3]:
ts_df = pd.read_csv("globaltsm.csv", encoding=('ISO-8859-1'),low_memory =False)
In [4]:
ts_df.head()
Out[4]:
eventid	iyear	imonth	iday	approxdate	extended	resolution	country	country_txt	region	...	addnotes	scite1	scite2	scite3	dbsource	INT_LOG	INT_IDEO	INT_MISC	INT_ANY	related
0	197000000001	1970	7	2	NaN	0	NaN	58	Dominican Republic	2	...	NaN	NaN	NaN	NaN	PGIS	0	0	0	0	NaN
1	197000000002	1970	0	0	NaN	0	NaN	130	Mexico	1	...	NaN	NaN	NaN	NaN	PGIS	0	1	1	1	NaN
2	197001000001	1970	1	0	NaN	0	NaN	160	Philippines	5	...	NaN	NaN	NaN	NaN	PGIS	-9	-9	1	1	NaN
3	197001000002	1970	1	0	NaN	0	NaN	78	Greece	8	...	NaN	NaN	NaN	NaN	PGIS	-9	-9	1	1	NaN
4	197001000003	1970	1	0	NaN	0	NaN	101	Japan	4	...	NaN	NaN	NaN	NaN	PGIS	-9	-9	1	1	NaN
5 rows × 135 columns

In [5]:
pd.set_option('display.max_columns', None)
In [7]:
ts_df.shape
Out[7]:
(181691, 135)
In [8]:
ts_df.head()
Out[8]:
eventid	iyear	imonth	iday	approxdate	extended	resolution	country	country_txt	region	region_txt	provstate	city	latitude	longitude	specificity	vicinity	location	summary	crit1	crit2	crit3	doubtterr	alternative	alternative_txt	multiple	success	suicide	attacktype1	attacktype1_txt	attacktype2	attacktype2_txt	attacktype3	attacktype3_txt	targtype1	targtype1_txt	targsubtype1	targsubtype1_txt	corp1	target1	natlty1	natlty1_txt	targtype2	targtype2_txt	targsubtype2	targsubtype2_txt	corp2	target2	natlty2	natlty2_txt	targtype3	targtype3_txt	targsubtype3	targsubtype3_txt	corp3	target3	natlty3	natlty3_txt	gname	gsubname	gname2	gsubname2	gname3	gsubname3	motive	guncertain1	guncertain2	guncertain3	individual	nperps	nperpcap	claimed	claimmode	claimmode_txt	claim2	claimmode2	claimmode2_txt	claim3	claimmode3	claimmode3_txt	compclaim	weaptype1	weaptype1_txt	weapsubtype1	weapsubtype1_txt	weaptype2	weaptype2_txt	weapsubtype2	weapsubtype2_txt	weaptype3	weaptype3_txt	weapsubtype3	weapsubtype3_txt	weaptype4	weaptype4_txt	weapsubtype4	weapsubtype4_txt	weapdetail	nkill	nkillus	nkillter	nwound	nwoundus	nwoundte	property	propextent	propextent_txt	propvalue	propcomment	ishostkid	nhostkid	nhostkidus	nhours	ndays	divert	kidhijcountry	ransom	ransomamt	ransomamtus	ransompaid	ransompaidus	ransomnote	hostkidoutcome	hostkidoutcome_txt	nreleased	addnotes	scite1	scite2	scite3	dbsource	INT_LOG	INT_IDEO	INT_MISC	INT_ANY	related
0	197000000001	1970	7	2	NaN	0	NaN	58	Dominican Republic	2	Central America & Caribbean	NaN	Santo Domingo	18.456792	-69.951164	1.0	0	NaN	NaN	1	1	1	0.0	NaN	NaN	0.0	1	0	1	Assassination	NaN	NaN	NaN	NaN	14	Private Citizens & Property	68.0	Named Civilian	NaN	Julio Guzman	58.0	Dominican Republic	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN	MANO-D	NaN	NaN	NaN	NaN	NaN	NaN	0.0	NaN	NaN	0	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN	13	Unknown	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN	1.0	NaN	NaN	0.0	NaN	NaN	0	NaN	NaN	NaN	NaN	0.0	NaN	NaN	NaN	NaN	NaN	NaN	0.0	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN	PGIS	0	0	0	0	NaN
1	197000000002	1970	0	0	NaN	0	NaN	130	Mexico	1	North America	Federal	Mexico city	19.371887	-99.086624	1.0	0	NaN	NaN	1	1	1	0.0	NaN	NaN	0.0	1	0	6	Hostage Taking (Kidnapping)	NaN	NaN	NaN	NaN	7	Government (Diplomatic)	45.0	Diplomatic Personnel (outside of embassy, cons...	Belgian Ambassador Daughter	Nadine Chaval, daughter	21.0	Belgium	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN	23rd of September Communist League	NaN	NaN	NaN	NaN	NaN	NaN	0.0	NaN	NaN	0	7.0	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN	13	Unknown	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN	0.0	NaN	NaN	0.0	NaN	NaN	0	NaN	NaN	NaN	NaN	1.0	1.0	0.0	NaN	NaN	NaN	Mexico	1.0	800000.0	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN	PGIS	0	1	1	1	NaN
2	197001000001	1970	1	0	NaN	0	NaN	160	Philippines	5	Southeast Asia	Tarlac	Unknown	15.478598	120.599741	4.0	0	NaN	NaN	1	1	1	0.0	NaN	NaN	0.0	1	0	1	Assassination	NaN	NaN	NaN	NaN	10	Journalists & Media	54.0	Radio Journalist/Staff/Facility	Voice of America	Employee	217.0	United States	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN	Unknown	NaN	NaN	NaN	NaN	NaN	NaN	0.0	NaN	NaN	0	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN	13	Unknown	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN	1.0	NaN	NaN	0.0	NaN	NaN	0	NaN	NaN	NaN	NaN	0.0	NaN	NaN	NaN	NaN	NaN	NaN	0.0	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN	PGIS	-9	-9	1	1	NaN
3	197001000002	1970	1	0	NaN	0	NaN	78	Greece	8	Western Europe	Attica	Athens	37.997490	23.762728	1.0	0	NaN	NaN	1	1	1	0.0	NaN	NaN	0.0	1	0	3	Bombing/Explosion	NaN	NaN	NaN	NaN	7	Government (Diplomatic)	46.0	Embassy/Consulate	NaN	U.S. Embassy	217.0	United States	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN	Unknown	NaN	NaN	NaN	NaN	NaN	NaN	0.0	NaN	NaN	0	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN	6	Explosives	16.0	Unknown Explosive Type	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN	Explosive	NaN	NaN	NaN	NaN	NaN	NaN	1	NaN	NaN	NaN	NaN	0.0	NaN	NaN	NaN	NaN	NaN	NaN	0.0	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN	PGIS	-9	-9	1	1	NaN
4	197001000003	1970	1	0	NaN	0	NaN	101	Japan	4	East Asia	Fukouka	Fukouka	33.580412	130.396361	1.0	0	NaN	NaN	1	1	1	-9.0	NaN	NaN	0.0	1	0	7	Facility/Infrastructure Attack	NaN	NaN	NaN	NaN	7	Government (Diplomatic)	46.0	Embassy/Consulate	NaN	U.S. Consulate	217.0	United States	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN	Unknown	NaN	NaN	NaN	NaN	NaN	NaN	0.0	NaN	NaN	0	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN	8	Incendiary	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN	Incendiary	NaN	NaN	NaN	NaN	NaN	NaN	1	NaN	NaN	NaN	NaN	0.0	NaN	NaN	NaN	NaN	NaN	NaN	0.0	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN	NaN	PGIS	-9	-9	1	1	NaN
In [49]:
ts_df.rename(columns={'iyear':'Year','imonth':'Month','extended':'Extended','iday':'Day',
                  'country_txt':'country','provstate':'state','region_txt':'Region',
                  'attacktype1_txt':'AttackType','target1':'Target','nkill':'killed',
                  'nwound':'wounded','summary':'Summary','gname':'Group',
                  'targtype1_txt':'Target_type','weaptype1_txt':'Weapon_type','motive':'Motive'}, inplace=True)
In [50]:
ts_df=ts_df[['Year','Month','Extended','Day','country','state','Region','city',
      'latitude','longitude','AttackType','killed','Target','wounded',
      'Summary','Group','Target_type','Weapon_type','Motive']]
In [23]:
ts_df.columns
Out[23]:
Index(['eventid', 'Year', 'Month', 'Day', 'approxdate', 'Extended',
       'resolution', 'country', 'country', 'region',
       ...
       'addnotes', 'scite1', 'scite2', 'scite3', 'dbsource', 'INT_LOG',
       'INT_IDEO', 'INT_MISC', 'INT_ANY', 'related'],
      dtype='object', length=135)
In [51]:
ts_df.head()
Out[51]:
Year	Month	Extended	Day	country	country	state	Region	city	latitude	longitude	AttackType	killed	Target	wounded	Summary	Group	Target_type	Weapon_type	Motive
0	1970	7	0	2	58	Dominican Republic	NaN	Central America & Caribbean	Santo Domingo	18.456792	-69.951164	Assassination	1.0	Julio Guzman	0.0	NaN	MANO-D	Private Citizens & Property	Unknown	NaN
1	1970	0	0	0	130	Mexico	Federal	North America	Mexico city	19.371887	-99.086624	Hostage Taking (Kidnapping)	0.0	Nadine Chaval, daughter	0.0	NaN	23rd of September Communist League	Government (Diplomatic)	Unknown	NaN
2	1970	1	0	0	160	Philippines	Tarlac	Southeast Asia	Unknown	15.478598	120.599741	Assassination	1.0	Employee	0.0	NaN	Unknown	Journalists & Media	Unknown	NaN
3	1970	1	0	0	78	Greece	Attica	Western Europe	Athens	37.997490	23.762728	Bombing/Explosion	NaN	U.S. Embassy	NaN	NaN	Unknown	Government (Diplomatic)	Explosives	NaN
4	1970	1	0	0	101	Japan	Fukouka	East Asia	Fukouka	33.580412	130.396361	Facility/Infrastructure Attack	NaN	U.S. Consulate	NaN	NaN	Unknown	Government (Diplomatic)	Incendiary	NaN
In [53]:
ts_df.info()
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 181691 entries, 0 to 181690
Data columns (total 20 columns):
 #   Column       Non-Null Count   Dtype  
---  ------       --------------   -----  
 0   Year         181691 non-null  int64  
 1   Month        181691 non-null  int64  
 2   Extended     181691 non-null  int64  
 3   Day          181691 non-null  int64  
 4   country      181691 non-null  int64  
 5   country      181691 non-null  object 
 6   state        181270 non-null  object 
 7   Region       181691 non-null  object 
 8   city         181257 non-null  object 
 9   latitude     177135 non-null  float64
 10  longitude    177134 non-null  float64
 11  AttackType   181691 non-null  object 
 12  killed       171378 non-null  float64
 13  Target       181055 non-null  object 
 14  wounded      165380 non-null  float64
 15  Summary      115562 non-null  object 
 16  Group        181691 non-null  object 
 17  Target_type  181691 non-null  object 
 18  Weapon_type  181691 non-null  object 
 19  Motive       50561 non-null   object 
dtypes: float64(4), int64(5), object(11)
memory usage: 27.7+ MB
In [55]:
ts_df.isnull().sum()
Out[55]:
Year                0
Month               0
Extended            0
Day                 0
country             0
country             0
state             421
Region              0
city              434
latitude         4556
longitude        4557
AttackType          0
killed          10313
Target            636
wounded         16311
Summary         66129
Group               0
Target_type         0
Weapon_type         0
Motive         131130
dtype: int64
In [58]:
plt.figure(figsize=(20,10))
sns.heatmap(ts_df.isnull() ,cbar = False , cmap='viridis')
Out[58]:
<AxesSubplot:>

In [60]:
pd.crosstab(ts_df.Year, ts_df.Region).plot(kind='area',figsize=(15,6))
plt.title('Terrorist activities by region in the year')
plt.ylabel('Number of attacks')
plt.show()

In [8]:
plt.subplots(figsize=(15,6))
sns.countplot('Year',data=ts_df,palette='RdYlGn_r',edgecolor=sns.color_palette("YlOrBr", 10))
plt.xticks(rotation=90)
plt.title('num of terrorist')
plt.show()
---------------------------------------------------------------------------
NameError                                 Traceback (most recent call last)
<ipython-input-8-bd9af0dbbf32> in <module>
----> 1 plt.subplots(figsize=(15,6))
      2 sns.countplot('Year',data=ts_df,palette='RdYlGn_r',edgecolor=sns.color_palette("YlOrBr", 10))
      3 plt.xticks(rotation=90)
      4 plt.title('num of terrorist')
      5 plt.show()

NameError: name 'plt' is not defined
In [7]:
t['city'].value_counts()
---------------------------------------------------------------------------
AttributeError                            Traceback (most recent call last)
<ipython-input-7-b123a2c6dad1> in <module>
----> 1 ts_df=['city'].value_counts()

AttributeError: 'list' object has no attribute 'value_counts'
In [ ]:
