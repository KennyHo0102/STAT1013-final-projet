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

<div class="cell markdown" id="CRExAPNFofZW">

# CUHK-STAT1013: Practical Assignment Part 1: Sharing Your Idea and Data

</div>

<div class="cell markdown" id="VtJrITDeolyz">

##Project background

**Description:**

Dataset describing the salary for different gender in distinct area

**Github:**
<https://github.com/fxangulo/GenderPayGap/blob/main/sample_salary.xls>

**Sample size:** 690

</div>

<div class="cell markdown" id="MCTMJs3O-NWB">

**Feature documentation:**

</div>

<div class="cell code" execution_count="44"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;}"
id="QN_2Fhj-9_nE" outputId="856ff463-8897-45fb-efe5-e8d90c453988">

``` python
df.info()
```

<div class="output stream stdout">

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 690 entries, 0 to 689
    Data columns (total 7 columns):
     #   Column  Non-Null Count  Dtype 
    ---  ------  --------------  ----- 
     0   SCALE   690 non-null    int64 
     1   TENURE  690 non-null    int64 
     2   ZONE    690 non-null    object
     3   CENTER  690 non-null    object
     4   GENDER  690 non-null    object
     5   TYPE    690 non-null    object
     6   SALARY  690 non-null    int64 
    dtypes: int64(3), object(4)
    memory usage: 37.9+ KB

</div>

</div>

<div class="cell markdown" id="7bYTEY5Hp5W3">

## Hypothesis

-   Tell us what your idea is and why you have chosen to pursue this
    idea.
    -   I am interested in "*Do male still have a higher salary than
        female in the new generation*"
-   What two groups you are comparing:
    -   **G1**: salary of male; **G2**: salary of female
-   What you will be measuring (i.e., what your response variable will
    be)
    -   `salary`
-   Is your response variable quantitative rather than categorical?
    -   `salary` are quantitative data with number
-   Make a prediction about what kind of difference you expect to see
    between your samples and WHY.
    -   I expect that **G1** \> **G2** since [Male have a higher salary
        in the old
        generation](https://www.assemble.inc/blog/how-the-gender-wage-gap-has-changed-over-the-last-40-years).
-   Talk about how you will gather your data
    -   From Excel file:
        [sample_salary.xls](https://github.com/fxangulo/GenderPayGap/blob/main/sample_salary.xls?raw=true)
-   If you had unlimited resources (time, money, staff, etc.) how would
    you collect your data?
    -   \(i\) collect data from both small company and big company if
        the data is not confidential such that we will have both high
        and low salary data.

    -   \(ii\) collect data from more countries so that the data is more
        representative to the world

</div>

<div class="cell markdown" id="CwLMAZ7dwP99">

##dataset

</div>

<div class="cell code" execution_count="31"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;,&quot;height&quot;:206}"
id="AHEw6QvGheNe" outputId="b441e7d4-6fd3-40eb-f1e9-6883aea8775a">

``` python
## load dataset from excel

import pandas as pd

df = pd.read_excel('/content/sample_salary.xls')
df.head(5)
```

<div class="output execute_result" execution_count="31">

       SCALE  TENURE  ZONE         CENTER  GENDER       TYPE  SALARY
    0    145       1  WEST  Emp: 36 to 50  FEMALE  FULL-TIME   17515
    1    145       1  WEST  Emp: 36 to 50  FEMALE  FULL-TIME   16031
    2    145      11  WEST  Emp: 10 to 20  FEMALE  FULL-TIME   21633
    3    145       9  WEST  Emp: 10 to 20  FEMALE  FULL-TIME   20001
    4    145       2  WEST  Emp: 10 to 20  FEMALE  FULL-TIME   19623

</div>

</div>

<div class="cell markdown" id="J0aM5ttIvRr-">

-   Tell us what groups you want to compare in the dataset
    -   **G1** (SALARY \| GENDER = MALE) vs. **G2** (SALARY \| GENDER =
        FEMALE)

</div>

<div class="cell code" execution_count="7"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;}"
id="UuFvPabQyIku" outputId="f12cb161-9bc7-47ca-c341-2d7b78df72db">

``` python
## First 5 records of G1 (male)
(df[df['GENDER'] == 'MALE']['SALARY']).head(5)
```

<div class="output execute_result" execution_count="7">

    17    22182
    20    31194
    56    18783
    57    22848
    58    19083
    Name: SALARY, dtype: int64

</div>

</div>

<div class="cell code" execution_count="8"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;}"
id="7wf7k7GwyUpv" outputId="ea3bcc02-c57d-4291-894a-2bbff084d892">

``` python
## First 5 records of G1 (female)
(df[df['GENDER'] == 'FEMALE']['SALARY']).head(5)
```

<div class="output execute_result" execution_count="8">

    0    17515
    1    16031
    2    21633
    3    20001
    4    19623
    Name: SALARY, dtype: int64

</div>

</div>

<div class="cell markdown" id="wLx6Omde1NuZ">

##Any other data description and visualization you want to add.

</div>

<div class="cell markdown" id="QelEx7EO1Pa6">

import software for data visualisation

</div>

<div class="cell code" execution_count="9" id="v4xA7yOVy8L3">

``` python
import matplotlib.pyplot as plt
import seaborn as sns
plt.rcParams['figure.figsize'] = [10, 5]

sns.set()


```

</div>

<div class="cell markdown" id="uNVj_kmK1lpc">

1.stripplot

</div>

<div class="cell code" execution_count="16"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;,&quot;height&quot;:661}"
id="rgo_k_6J1gZS" outputId="ff7a72e1-b377-4c76-fb66-487869869553">

``` python
sns.stripplot(data=df, x="SALARY", y="GENDER")
plt.show()

sns.stripplot(data=df, y="SALARY", x="GENDER")
plt.show()
```

<div class="output display_data">

![](ee2d604c15a4d87ac0c837e3eada37be42e49c52.png)

</div>

<div class="output display_data">

![](d807c9b1ac451ddf63467cbbec1d8cf414344928.png)

</div>

</div>

<div class="cell markdown" id="q7AnaWzx1qxJ">

2.violinplot

</div>

<div class="cell code" execution_count="14"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;,&quot;height&quot;:339}"
id="YYRFQzr02Qb_" outputId="3bb3f802-6cfb-45cf-e6e5-c4d980bebddb">

``` python
sns.violinplot(data=df, x="SALARY", y="GENDER")
plt.show()
```

<div class="output display_data">

![](460599e813e83574d635dd736d2493df5459987e.png)

</div>

</div>

<div class="cell markdown" id="bSS1wBoi3M_J">

3.boxplot

</div>

<div class="cell code" execution_count="19"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;,&quot;height&quot;:339}"
id="LdYAm9X429_w" outputId="c19b6e38-aa7a-40bd-e0c1-a5154ec12115">

``` python
sns.boxplot(data=df, x='SALARY', y='GENDER')
plt.show()
```

<div class="output display_data">

![](8c89d8278bab7d8058a8e4d0df9b92b585b11aad.png)

</div>

</div>

<div class="cell markdown" id="uhT7WLIq3Qv-">

4.scatterplot including ZONE

</div>

<div class="cell code" execution_count="22"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;,&quot;height&quot;:339}"
id="NQVaAcQ73s3W" outputId="4fc7b50e-240f-49eb-fd5f-6496657f8320">

``` python
sns.scatterplot(data=df, x="SALARY", y="GENDER", hue='ZONE',style='ZONE')
plt.show()
```

<div class="output display_data">

![](c571aa76ad197c14b56195570fbb5ecf81e63c78.png)

</div>

</div>

<div class="cell markdown" id="FMBYxasI4M5C">

5.joint plot with tenure

</div>

<div class="cell code" execution_count="27"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;,&quot;height&quot;:437}"
id="bfENt80Z4Osg" outputId="f13e1278-50bd-4525-dbe9-debdf6c50c17">

``` python
g = sns.jointplot(data=df, x="TENURE", y="SALARY", hue="GENDER", kind="kde")
plt.show()
```

<div class="output display_data">

![](ae2673ef7d738f96caff698c54ca47ff7d74782d.png)

</div>

</div>
