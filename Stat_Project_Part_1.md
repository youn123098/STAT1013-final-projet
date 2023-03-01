---
jupyter:
  colab:
  kernelspec:
    display_name: Python 3
    name: python3
  language_info:
    name: python
  nbformat: 4
  nbformat_minor: 0

---

<div class="cell markdown" id="CSxD0lQhSTxs">

## Shortsighted dataset background

**Description**:

Dataset describing the proportion of myopia between male and female
university students in Hong Kong.

**Github**:
<https://docs.google.com/spreadsheets/d/e/2PACX-1vQdtfk5TmITafCybyALJzQgNB2nqiRzGTYSL6ynA3VDt0vfnNXSwEKQmqRzTcn2ew/pub?output=xlsx>

**Sample size**: 30

**Feature documentation**:

| Feature                             | Class      | Shape | Dtype   |
|:----------------------------------- |:---------- |:----- |:------- |
| Number of shortsighted students     | Tensor     |       | float64 |
| Name                                | Tensor     |       | string  |
| Sex                                 | Tensor     |       | string  |
| Age                                 | Tensor     |       | float64 |
| Shortsighted                        | ClassLabel |       | float64 |
| Relationship between sex and myopia | Tensor     |       | float64 |
| The main reason for myopia          | Tensor     |       | string  |

</div>

<div class="cell markdown" id="yQK4NAk6UZkr">

## **Hypothesis**

**1. Tell us what your idea is and why you have chosen to pursue this
idea.**

- The proportion of myopia between male and female university students
  in Hong Kong?
- Because in the context of the increasing prevalence of myopia, some
  reseach have found that the problem occurs more often in female than
  in male, but I am not really believe on that and I want to find the
  result by some data. (Reseach from : <https://kkne.ws/YeVKqj>)

**2. What two groups you are comparing:**

- G1: Number of myopia in male university student
- G2: Number of myopia in female university student

**3. What you will be measuring (i.e., what your response variable will
be)**

- Number of shortsighted people

**4. Is your response variable quantitative rather than categorical?**

- Number of shortsighted people is a quantitative variable since that
  dtype is float64 and that can be count.

**5. Make a prediction about what kind of difference you expect to see
between your samples and WHY.**

- We would expect that G2 \> G1 since eyes muscles of Women are more
  fragile than man and there is more room to lengthen the eye axis,
  which is the main cause of shortsighted. (Reseach from :
  <https://kkne.ws/YeVKqj>)

**6. Talk about how you will gather your data**

- I will use questionnaires to collect the data from university
  students because it can reflect the data more realistically.

**7. If you had unlimited resources (time, money, staff, etc.) how would
you collect your data?**

- \(i\) Find more people to do the questionnaires to make the datat
  more objective.
- \(ii\) Look for people of different ages to reflect the overall
  situation on male and female.
- \(iii\) make a good random sampling subset not only find the friends
  around me to be the respondents.
- \(iv\) increase more questions around the topic on the
  questionnaires and make the situation more comprehensive.
- \(v\) ask some more professional people to do a professional
  analysis.

</div>

<div class="cell markdown" id="PnH2CNcKUuoE">

## **Data (The proportion of myopia between male and female university students in Hong Kong?)**

</div>

<div class="cell code" execution_count="1"
colab="{"base_uri":"https://localhost:8080/","height":302}"
id="ZpVNUeB4Uy04" outputId="e2044de6-b579-43db-9b13-403f0d8d6cea">

```python
import pandas as pd

df = pd.read_excel(r'https://docs.google.com/spreadsheets/d/e/2PACX-1vQdtfk5TmITafCybyALJzQgNB2nqiRzGTYSL6ynA3VDt0vfnNXSwEKQmqRzTcn2ew/pub?output=xlsx')
df.head(5)
```

<div class="output execute_result" execution_count="1">

       Number of shortsighted students         Name     Sex   Age  \
    0                              1.0       Qi ran  Female  18.0   
    1                              2.0    Ken Yeung    Male  20.0   
    2                              3.0        Kammy  Female  18.0   
    3                              4.0         Judy  Female  19.0   
    4                              5.0  Li sze Hing  Female  20.0   
    
       Shortsighted (1:yes 2:No)  \
    0                        1.0   
    1                        0.0   
    2                        1.0   
    3                        1.0   
    4                        1.0   
    
       Relationship between sex and myopia (1:yes 0:no) The main reason for myopia  
    0                                               0.0                   Heredity  
    1                                               0.0                   Heredity  
    2                                               1.0                      study  
    3                                               0.0                      study  
    4                                               0.0                  play game  

</div>

</div>

<div class="cell code" execution_count="2"
colab="{"base_uri":"https://localhost:8080/"}"
id="ofy3KDJ_sbf8" outputId="9f765ffe-c439-4ddc-da8b-6e5ee80a428f">

```python
df.info()
```

<div class="output stream stdout">

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 60 entries, 0 to 59
    Data columns (total 7 columns):
     #   Column                                            Non-Null Count  Dtype  
    ---  ------                                            --------------  -----  
     0   Number of shortsighted students                   60 non-null     float64
     1   Name                                              60 non-null     object 
     2   Sex                                               60 non-null     object 
     3   Age                                               60 non-null     float64
     4   Shortsighted (1:yes 2:No)                         60 non-null     float64
     5   Relationship between sex and myopia (1:yes 0:no)  60 non-null     float64
     6   The main reason for myopia                        60 non-null     object 
    dtypes: float64(4), object(3)
    memory usage: 3.4+ KB

</div>

</div>

<div class="cell code" execution_count="3"
colab="{"base_uri":"https://localhost:8080/","height":269}"
id="Gy7r5e1K3Zod" outputId="4482c751-e491-4d09-a971-aefa2ead7d54">

```python
df.describe(include='all').T
```

<div class="output execute_result" execution_count="3">

                                                     count unique     top freq  \
    Number of shortsighted students                   60.0    NaN     NaN  NaN   
    Name                                                60     57  Cheryl    2   
    Sex                                                 60      2  Female   30   
    Age                                               60.0    NaN     NaN  NaN   
    Shortsighted (1:yes 2:No)                         60.0    NaN     NaN  NaN   
    Relationship between sex and myopia (1:yes 0:no)  60.0    NaN     NaN  NaN   
    The main reason for myopia                          60      3   study   25   
    
                                                          mean        std   min  \
    Number of shortsighted students                       30.5  17.464249   1.0   
    Name                                                   NaN        NaN   NaN   
    Sex                                                    NaN        NaN   NaN   
    Age                                                  19.15   1.273258  18.0   
    Shortsighted (1:yes 2:No)                         0.733333   0.445948   0.0   
    Relationship between sex and myopia (1:yes 0:no)  0.266667   0.445948   0.0   
    The main reason for myopia                             NaN        NaN   NaN   
    
                                                        25%   50%    75%   max  
    Number of shortsighted students                   15.75  30.5  45.25  60.0  
    Name                                                NaN   NaN    NaN   NaN  
    Sex                                                 NaN   NaN    NaN   NaN  
    Age                                                18.0  19.0   20.0  23.0  
    Shortsighted (1:yes 2:No)                           0.0   1.0    1.0   1.0  
    Relationship between sex and myopia (1:yes 0:no)    0.0   0.0    1.0   1.0  
    The main reason for myopia                          NaN   NaN    NaN   NaN  

</div>

</div>

<div class="cell markdown" id="P-Bs6WKTU203">

- Tell us what groups you want to compare in the dataset
  - **G1** (Shortsighted (1:yes 2:No) \| sex = male) vs. **G2**
    (Shortsighted (1:yes 2:No) \| sex = female)

</div>

<div class="cell markdown" id="oUWBZaq_U8ko">

- Print first 5 records of each group, respectively.

</div>

<div class="cell code" execution_count="4"
colab="{"base_uri":"https://localhost:8080/"}"
id="REgbCrstVFz3" outputId="12a15c98-f347-4e87-a59c-1b85203f07a4">

```python
## First 5 records of G1 (male)
(df[df['Sex'] == 'Male']['Shortsighted (1:yes 2:No)']).head(5)
```

<div class="output execute_result" execution_count="4">

    1     0.0
    5     1.0
    6     0.0
    13    1.0
    19    1.0
    Name: Shortsighted (1:yes 2:No), dtype: float64

</div>

</div>

<div class="cell code" execution_count="5"
colab="{"base_uri":"https://localhost:8080/"}"
id="GLu08ucgVIV2" outputId="e66daa8b-05b5-42a2-c308-a3401117c975">

```python
## First 5 records of G2 (female)
(df[df['Sex'] == 'Female']['Shortsighted (1:yes 2:No)']).head(5)
```

<div class="output execute_result" execution_count="5">

    0    1.0
    2    1.0
    3    1.0
    4    1.0
    7    0.0
    Name: Shortsighted (1:yes 2:No), dtype: float64

</div>

</div>

<div class="cell code" execution_count="6" id="qjc2IKaT4pRU">

```python
import matplotlib.pyplot as plt
import seaborn as sns
plt.rcParams['figure.figsize'] = [10, 5]
sns.set()
```

</div>

<div class="cell markdown" id="HhSs1uxQaWVj">

**(1)** The actual situation for the proportion of myopia between male
and female in Hong Kong.

</div>

<div class="cell code" execution_count="7"
colab="{"base_uri":"https://localhost:8080/","height":339}"
id="uBKylpb344c7" outputId="583a9b57-dd9a-431f-d76a-1ad759d7600b">

```python
sns.histplot(df, x='Shortsighted (1:yes 2:No)', hue='Sex')
plt.show()
```

<div class="output display_data">

![](da7819f41f8efbd088e794e5450562d8aaa755c2.png)

</div>

</div>

<div class="cell markdown" id="LtcqqmzLXZGf">

-> According to the above data,

- Myopia men are less than myopic women, which is the 2/3 of myopic
  women.
- Men without myopia are 3 times more than women without myopia.
- The number of boys with myopia and no myopia is almost equal.
- The number of girls with myopia and no myopia is very different, and
  the number of myopia one is higher.

</div>

<div class="cell markdown" id="0d-ok12Dahi0">

**(2)** The thoughts of people about the relationship between sex and
myopia.

</div>

<div class="cell code" execution_count="9"
colab="{"base_uri":"https://localhost:8080/","height":339}"
id="efOrZ0kYWfZH" outputId="30d183c1-f939-470a-8f5c-fa1eb54547d8">

```python
sns.violinplot(x=df['Relationship between sex and myopia (1:yes 0:no)'])
plt.show()
```

<div class="output display_data">

![](e73fa24decdd5a26ac98cb61c1a05907cb43aa9a.png)

</div>

</div>

<div class="cell markdown" id="Yna7JgnZbAWh">

-> According to the above data,

- most of the people think that sex and myopia are not related and the
  proportion of shortsighted male and female should be divided
  equally.

</div>

<div class="cell markdown" id="juVn7p6VcEwQ">

**(3)** What age group of respondents?

</div>

<div class="cell code" execution_count="10"
colab="{"base_uri":"https://localhost:8080/","height":339}"
id="dg5I62VO5LJr" outputId="2e59ac66-305b-44fb-915b-4204607e6f7c">

```python
sns.stripplot(data=df, x="Sex", y="Age")
plt.show()
```

<div class="output display_data">

![](aa57b40477af837ae43facc6e0d79d65bb3dec7a.png)

</div>

</div>

<div class="cell markdown" id="cgivSHuKcXVh">

-> According to the above data,

- Most of the respondents are teenagers and university students.

</div>

<div class="cell markdown" id="mWTN4G8Qdl49">

**(4)** The main reason for shortsighted

</div>

<div class="cell code" execution_count="14"
colab="{"base_uri":"https://localhost:8080/","height":339}"
id="CQWb5ihHfMyN" outputId="dbfffe42-1162-481b-8349-5d639729b298">

```python
sns.histplot(data=df, x='The main reason for myopia', bins='auto')
plt.show()
```

<div class="output display_data">

![](27c82bb7ff346f37c9b036edccb1639957bb2671.png)

</div>

</div>

<div class="cell markdown" id="745l6uSLiTFy">

-> According to the above data,

- The main couse is learning, then playing games and the third is
  genetices.

</div>

<div class="cell markdown" id="zEdVFkmCnnc0">

**Result (The proportion of myopia between male and female university
students in Hong Kong?)**

- Although most people think that there is no relationship between
  gender and shortsighted,there is actually a relationship.
- The difference is that boys have higher myopia than girls.
- There is not much difference in the data between boys who are myopic
  and not myopic, female are the opposite.
- **The result matched the hypothesis (e.g. G2 \> G1)**

</div>
