---
jupyter:
  kernelspec:
    display_name: Python 3 (ipykernel)
    language: python
    name: python3
  language_info:
    codemirror_mode:
      name: ipython
      version: 3
    file_extension: .py
    mimetype: text/x-python
    name: python
    nbconvert_exporter: python
    pygments_lexer: ipython3
    version: 3.11.2
  nbformat: 4
  nbformat_minor: 5
---

::: {#08520e13 .cell .markdown}
# FIFA PLAYERS DATA ANALYSIS

The primary objective is to unearth insightful trends, attributes, and
demographic nuances embedded within the dataset. The profound
revelations extracted from this analysis not only underscore a profound
grasp of the data\'s intricacies but also underscore the potential to
refine decision-making across areas encompassing team formation, player
recruitment, and tactical strategy. Implicit in the project is a
compelling problem statement: How can data-driven insights be
effectively harnessed to decode the multifaceted dimensions of player
performance, consequently empowering astute choices that can sway the
balance between triumph and defeat on the football field.
:::

::: {#c95d04c7 .cell .markdown}
## IMPORTING REQUIRED LIBRARIES
:::

::: {#cd0109a5 .cell .code execution_count="1"}
``` python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import datetime as dt
import seaborn as sns
```
:::

::: {#44a37cfa .cell .markdown}
## SNEAKING IN THE DATA
:::

::: {#cb8301cb .cell .code execution_count="2"}
``` python
fdf=pd.read_csv('fifa21_raw_data.csv')
fdf
```

::: {.output .stream .stderr}
    C:\Users\91965\AppData\Local\Temp\ipykernel_15712\1923156327.py:1: DtypeWarning: Columns (76) have mixed types. Specify dtype option on import or set low_memory=False.
      fdf=pd.read_csv('fifa21_raw_data.csv')
:::

::: {.output .execute_result execution_count="2"}
```{=html}
<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>photoUrl</th>
      <th>LongName</th>
      <th>playerUrl</th>
      <th>Nationality</th>
      <th>Positions</th>
      <th>Name</th>
      <th>Age</th>
      <th>↓OVA</th>
      <th>POT</th>
      <th>Team &amp; Contract</th>
      <th>...</th>
      <th>A/W</th>
      <th>D/W</th>
      <th>IR</th>
      <th>PAC</th>
      <th>SHO</th>
      <th>PAS</th>
      <th>DRI</th>
      <th>DEF</th>
      <th>PHY</th>
      <th>Hits</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>https://cdn.sofifa.com/players/158/023/21_60.png</td>
      <td>Lionel Messi</td>
      <td>http://sofifa.com/player/158023/lionel-messi/2...</td>
      <td>Argentina</td>
      <td>RW ST CF</td>
      <td>L. Messi</td>
      <td>33</td>
      <td>93</td>
      <td>93</td>
      <td>\n\n\n\nFC Barcelona\n2004 ~ 2021\n\n</td>
      <td>...</td>
      <td>Medium</td>
      <td>Low</td>
      <td>5 ★</td>
      <td>85</td>
      <td>92</td>
      <td>91</td>
      <td>95</td>
      <td>38</td>
      <td>65</td>
      <td>\n372</td>
    </tr>
    <tr>
      <th>1</th>
      <td>https://cdn.sofifa.com/players/020/801/21_60.png</td>
      <td>C. Ronaldo dos Santos Aveiro</td>
      <td>http://sofifa.com/player/20801/c-ronaldo-dos-s...</td>
      <td>Portugal</td>
      <td>ST LW</td>
      <td>Cristiano Ronaldo</td>
      <td>35</td>
      <td>92</td>
      <td>92</td>
      <td>\n\n\n\nJuventus\n2018 ~ 2022\n\n</td>
      <td>...</td>
      <td>High</td>
      <td>Low</td>
      <td>5 ★</td>
      <td>89</td>
      <td>93</td>
      <td>81</td>
      <td>89</td>
      <td>35</td>
      <td>77</td>
      <td>\n344</td>
    </tr>
    <tr>
      <th>2</th>
      <td>https://cdn.sofifa.com/players/200/389/21_60.png</td>
      <td>Jan Oblak</td>
      <td>http://sofifa.com/player/200389/jan-oblak/210005/</td>
      <td>Slovenia</td>
      <td>GK</td>
      <td>J. Oblak</td>
      <td>27</td>
      <td>91</td>
      <td>93</td>
      <td>\n\n\n\nAtlético Madrid\n2014 ~ 2023\n\n</td>
      <td>...</td>
      <td>Medium</td>
      <td>Medium</td>
      <td>3 ★</td>
      <td>87</td>
      <td>92</td>
      <td>78</td>
      <td>90</td>
      <td>52</td>
      <td>90</td>
      <td>\n86</td>
    </tr>
    <tr>
      <th>3</th>
      <td>https://cdn.sofifa.com/players/192/985/21_60.png</td>
      <td>Kevin De Bruyne</td>
      <td>http://sofifa.com/player/192985/kevin-de-bruyn...</td>
      <td>Belgium</td>
      <td>CAM CM</td>
      <td>K. De Bruyne</td>
      <td>29</td>
      <td>91</td>
      <td>91</td>
      <td>\n\n\n\nManchester City\n2015 ~ 2023\n\n</td>
      <td>...</td>
      <td>High</td>
      <td>High</td>
      <td>4 ★</td>
      <td>76</td>
      <td>86</td>
      <td>93</td>
      <td>88</td>
      <td>64</td>
      <td>78</td>
      <td>\n163</td>
    </tr>
    <tr>
      <th>4</th>
      <td>https://cdn.sofifa.com/players/190/871/21_60.png</td>
      <td>Neymar da Silva Santos Jr.</td>
      <td>http://sofifa.com/player/190871/neymar-da-silv...</td>
      <td>Brazil</td>
      <td>LW CAM</td>
      <td>Neymar Jr</td>
      <td>28</td>
      <td>91</td>
      <td>91</td>
      <td>\n\n\n\nParis Saint-Germain\n2017 ~ 2022\n\n</td>
      <td>...</td>
      <td>High</td>
      <td>Medium</td>
      <td>5 ★</td>
      <td>91</td>
      <td>85</td>
      <td>86</td>
      <td>94</td>
      <td>36</td>
      <td>59</td>
      <td>\n273</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>18974</th>
      <td>https://cdn.sofifa.com/players/257/710/21_60.png</td>
      <td>Mengxuan Zhang</td>
      <td>http://sofifa.com/player/257710/mengxuan-zhang...</td>
      <td>China PR</td>
      <td>CB</td>
      <td>Zhang Mengxuan</td>
      <td>21</td>
      <td>47</td>
      <td>52</td>
      <td>\n\n\n\nChongqing Dangdai Lifan FC SWM Team\n2...</td>
      <td>...</td>
      <td>Low</td>
      <td>Low</td>
      <td>1 ★</td>
      <td>58</td>
      <td>23</td>
      <td>26</td>
      <td>27</td>
      <td>50</td>
      <td>48</td>
      <td>2</td>
    </tr>
    <tr>
      <th>18975</th>
      <td>https://cdn.sofifa.com/players/258/736/21_60.png</td>
      <td>Vani Da Silva</td>
      <td>http://sofifa.com/player/258736/vani-da-silva/...</td>
      <td>England</td>
      <td>ST</td>
      <td>V. Da Silva</td>
      <td>17</td>
      <td>47</td>
      <td>67</td>
      <td>\n\n\n\nOldham Athletic\n2020 ~ 2021\n\n</td>
      <td>...</td>
      <td>Medium</td>
      <td>Medium</td>
      <td>1 ★</td>
      <td>70</td>
      <td>46</td>
      <td>40</td>
      <td>53</td>
      <td>16</td>
      <td>40</td>
      <td>3</td>
    </tr>
    <tr>
      <th>18976</th>
      <td>https://cdn.sofifa.com/players/247/223/21_60.png</td>
      <td>Ao Xia</td>
      <td>http://sofifa.com/player/247223/ao-xia/210005/</td>
      <td>China PR</td>
      <td>CB</td>
      <td>Xia Ao</td>
      <td>21</td>
      <td>47</td>
      <td>55</td>
      <td>\n\n\n\nWuhan Zall\n2018 ~ 2022\n\n</td>
      <td>...</td>
      <td>Medium</td>
      <td>Medium</td>
      <td>1 ★</td>
      <td>64</td>
      <td>28</td>
      <td>26</td>
      <td>38</td>
      <td>48</td>
      <td>51</td>
      <td>3</td>
    </tr>
    <tr>
      <th>18977</th>
      <td>https://cdn.sofifa.com/players/258/760/21_60.png</td>
      <td>Ben Hough</td>
      <td>http://sofifa.com/player/258760/ben-hough/210005/</td>
      <td>England</td>
      <td>CM</td>
      <td>B. Hough</td>
      <td>17</td>
      <td>47</td>
      <td>67</td>
      <td>\n\n\n\nOldham Athletic\n2020 ~ 2021\n\n</td>
      <td>...</td>
      <td>Medium</td>
      <td>Medium</td>
      <td>1 ★</td>
      <td>64</td>
      <td>40</td>
      <td>48</td>
      <td>49</td>
      <td>35</td>
      <td>45</td>
      <td>5</td>
    </tr>
    <tr>
      <th>18978</th>
      <td>https://cdn.sofifa.com/players/255/958/21_60.png</td>
      <td>Mateo Flores</td>
      <td>http://sofifa.com/player/255958/mateo-flores/2...</td>
      <td>Bolivia</td>
      <td>CDM</td>
      <td>M. Flores</td>
      <td>19</td>
      <td>47</td>
      <td>63</td>
      <td>\n\n\n\nClub Bolívar\n2020 ~ 2024\n\n</td>
      <td>...</td>
      <td>Medium</td>
      <td>Medium</td>
      <td>1 ★</td>
      <td>57</td>
      <td>32</td>
      <td>43</td>
      <td>48</td>
      <td>44</td>
      <td>49</td>
      <td>2</td>
    </tr>
  </tbody>
</table>
<p>18979 rows × 77 columns</p>
</div>
```
:::
:::

::: {#76be15b5 .cell .markdown}
### GETTING THE DATA TYPES
:::

::: {#cd67b2f8 .cell .code execution_count="3"}
``` python
fdf.info()
```

::: {.output .stream .stdout}
    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 18979 entries, 0 to 18978
    Data columns (total 77 columns):
     #   Column            Non-Null Count  Dtype 
    ---  ------            --------------  ----- 
     0   photoUrl          18979 non-null  object
     1   LongName          18979 non-null  object
     2   playerUrl         18979 non-null  object
     3   Nationality       18979 non-null  object
     4   Positions         18979 non-null  object
     5   Name              18979 non-null  object
     6   Age               18979 non-null  int64 
     7   ↓OVA              18979 non-null  int64 
     8   POT               18979 non-null  int64 
     9   Team & Contract   18979 non-null  object
     10  ID                18979 non-null  int64 
     11  Height            18979 non-null  object
     12  Weight            18979 non-null  object
     13  foot              18979 non-null  object
     14  BOV               18979 non-null  int64 
     15  BP                18979 non-null  object
     16  Growth            18979 non-null  int64 
     17  Joined            18979 non-null  object
     18  Loan Date End     1013 non-null   object
     19  Value             18979 non-null  object
     20  Wage              18979 non-null  object
     21  Release Clause    18979 non-null  object
     22  Attacking         18979 non-null  int64 
     23  Crossing          18979 non-null  int64 
     24  Finishing         18979 non-null  int64 
     25  Heading Accuracy  18979 non-null  int64 
     26  Short Passing     18979 non-null  int64 
     27  Volleys           18979 non-null  int64 
     28  Skill             18979 non-null  int64 
     29  Dribbling         18979 non-null  int64 
     30  Curve             18979 non-null  int64 
     31  FK Accuracy       18979 non-null  int64 
     32  Long Passing      18979 non-null  int64 
     33  Ball Control      18979 non-null  int64 
     34  Movement          18979 non-null  int64 
     35  Acceleration      18979 non-null  int64 
     36  Sprint Speed      18979 non-null  int64 
     37  Agility           18979 non-null  int64 
     38  Reactions         18979 non-null  int64 
     39  Balance           18979 non-null  int64 
     40  Power             18979 non-null  int64 
     41  Shot Power        18979 non-null  int64 
     42  Jumping           18979 non-null  int64 
     43  Stamina           18979 non-null  int64 
     44  Strength          18979 non-null  int64 
     45  Long Shots        18979 non-null  int64 
     46  Mentality         18979 non-null  int64 
     47  Aggression        18979 non-null  int64 
     48  Interceptions     18979 non-null  int64 
     49  Positioning       18979 non-null  int64 
     50  Vision            18979 non-null  int64 
     51  Penalties         18979 non-null  int64 
     52  Composure         18979 non-null  int64 
     53  Defending         18979 non-null  int64 
     54  Marking           18979 non-null  int64 
     55  Standing Tackle   18979 non-null  int64 
     56  Sliding Tackle    18979 non-null  int64 
     57  Goalkeeping       18979 non-null  int64 
     58  GK Diving         18979 non-null  int64 
     59  GK Handling       18979 non-null  int64 
     60  GK Kicking        18979 non-null  int64 
     61  GK Positioning    18979 non-null  int64 
     62  GK Reflexes       18979 non-null  int64 
     63  Total Stats       18979 non-null  int64 
     64  Base Stats        18979 non-null  int64 
     65  W/F               18979 non-null  object
     66  SM                18979 non-null  object
     67  A/W               18979 non-null  object
     68  D/W               18979 non-null  object
     69  IR                18979 non-null  object
     70  PAC               18979 non-null  int64 
     71  SHO               18979 non-null  int64 
     72  PAS               18979 non-null  int64 
     73  DRI               18979 non-null  int64 
     74  DEF               18979 non-null  int64 
     75  PHY               18979 non-null  int64 
     76  Hits              18979 non-null  object
    dtypes: int64(55), object(22)
    memory usage: 11.1+ MB
:::
:::

::: {#118ab9fd .cell .code execution_count="4"}
``` python
fdf.shape
```

::: {.output .execute_result execution_count="4"}
    (18979, 77)
:::
:::

::: {#265cab50 .cell .markdown}
### NUMBER OF NATIONS IN THE DATA
:::

::: {#7c4132b8 .cell .code execution_count="5"}
``` python
fdf.Nationality.unique().shape
```

::: {.output .execute_result execution_count="5"}
    (164,)
:::
:::

::: {#e2cdbbc4 .cell .code execution_count="6"}
``` python
fdf.Nationality.unique()
```

::: {.output .execute_result execution_count="6"}
    array(['Argentina', 'Portugal', 'Slovenia', 'Belgium', 'Brazil', 'Poland',
           'France', 'Egypt', 'Senegal', 'Netherlands', 'Germany', 'Spain',
           'England', 'Scotland', 'Korea Republic', 'Costa Rica', 'Italy',
           'Gabon', 'Croatia', 'Uruguay', 'Switzerland', 'Slovakia', 'Serbia',
           'Morocco', 'Algeria', 'Denmark', 'Hungary', 'Bosnia Herzegovina',
           'Norway', 'Nigeria', 'Cameroon', 'Ghana', 'Mexico', 'Austria',
           'Colombia', 'Albania', 'Chile', 'Ivory Coast', 'Greece', 'Finland',
           'Wales', 'Sweden', 'Czech Republic', 'Togo', 'Russia', 'Canada',
           'United States', 'Guinea', 'Venezuela', 'Montenegro', 'Israel',
           'Republic of Ireland', 'Ukraine', 'Ecuador', 'Turkey', 'Jamaica',
           'Australia', 'DR Congo', 'Armenia', 'China PR', 'Northern Ireland',
           'North Macedonia', 'Kosovo', 'Mali', 'Peru',
           'Central African Republic', 'Iceland', 'Burkina Faso', 'Paraguay',
           'Japan', 'Romania', 'New Zealand', 'Angola', 'Tunisia', 'Iran',
           'Syria', 'Dominican Republic', 'Cape Verde', 'Kenya', 'Georgia',
           'Zambia', 'Panama', 'Equatorial Guinea', 'Tanzania', 'Zimbabwe',
           'Congo', 'Moldova', 'South Africa', 'Guinea Bissau', 'Mozambique',
           'Honduras', 'Iraq', 'Cuba', 'Cyprus', 'Lithuania', 'Estonia',
           'Madagascar', 'Benin', 'Curacao', 'Saudi Arabia', 'Gambia',
           'Uzbekistan', 'Chad', 'Libya', 'Philippines', 'Sierra Leone',
           'Liberia', 'Bulgaria', 'Comoros', 'Saint Kitts and Nevis',
           'United Arab Emirates', 'Namibia', 'Luxembourg',
           'Trinidad & Tobago', 'Bermuda', 'Thailand', 'Burundi',
           'New Caledonia', 'Puerto Rico', 'Bolivia', 'Kazakhstan',
           'Antigua & Barbuda', 'Latvia', 'Malawi', 'Montserrat',
           'São Tomé & Príncipe', 'Mauritania', 'Jordan', 'Eritrea',
           'El Salvador', 'Aruba', 'Uganda', 'Chinese Taipei', 'Azerbaijan',
           'Afghanistan', 'Faroe Islands', 'Haiti', 'Sudan', 'Grenada',
           'Lebanon', 'Guam', 'Palestine', 'Belarus', 'Guyana', 'Rwanda',
           'Saint Lucia', 'Papua New Guinea', 'Liechtenstein', 'India',
           'Ethiopia', 'Belize', 'Andorra', 'Guatemala', 'Malta', 'Niger',
           'Korea DPR', 'Barbados', 'Macau', 'South Sudan', 'Singapore',
           'Hong Kong', 'Nicaragua', 'Malaysia', 'Indonesia'], dtype=object)
:::
:::

::: {#f659cbdc .cell .markdown}
### AGE & HEIGHT OF PLAYERS IN SORTED MANNER {#age--height-of-players-in-sorted-manner}
:::

::: {#e58304f0 .cell .code execution_count="7"}
``` python
a=fdf.Age.unique()
a.sort()
print(a)

```

::: {.output .stream .stdout}
    [16 17 18 19 20 21 22 23 24 25 26 27 28 29 30 31 32 33 34 35 36 37 38 39
     40 41 42 43 53]
:::
:::

::: {#975eabfe .cell .code execution_count="8"}
``` python
h=fdf.Height.unique()
h.sort()
print(h)
```

::: {.output .stream .stdout}
    ['5\'1"' '5\'10"' '5\'11"' '5\'2"' '5\'3"' '5\'4"' '5\'5"' '5\'6"' '5\'7"'
     '5\'8"' '5\'9"' '6\'0"' '6\'1"' '6\'2"' '6\'3"' '6\'4"' '6\'5"' '6\'6"'
     '6\'7"' '6\'8"' '6\'9"']
:::
:::

::: {#5bc8520a .cell .markdown}
### REMOVING DUPLICATES
:::

::: {#0afaab8c .cell .code execution_count="9"}
``` python
fdf.drop_duplicates
```

::: {.output .execute_result execution_count="9"}
    <bound method DataFrame.drop_duplicates of                                                photoUrl  \
    0      https://cdn.sofifa.com/players/158/023/21_60.png   
    1      https://cdn.sofifa.com/players/020/801/21_60.png   
    2      https://cdn.sofifa.com/players/200/389/21_60.png   
    3      https://cdn.sofifa.com/players/192/985/21_60.png   
    4      https://cdn.sofifa.com/players/190/871/21_60.png   
    ...                                                 ...   
    18974  https://cdn.sofifa.com/players/257/710/21_60.png   
    18975  https://cdn.sofifa.com/players/258/736/21_60.png   
    18976  https://cdn.sofifa.com/players/247/223/21_60.png   
    18977  https://cdn.sofifa.com/players/258/760/21_60.png   
    18978  https://cdn.sofifa.com/players/255/958/21_60.png   

                               LongName  \
    0                      Lionel Messi   
    1      C. Ronaldo dos Santos Aveiro   
    2                         Jan Oblak   
    3                   Kevin De Bruyne   
    4        Neymar da Silva Santos Jr.   
    ...                             ...   
    18974                Mengxuan Zhang   
    18975                 Vani Da Silva   
    18976                        Ao Xia   
    18977                     Ben Hough   
    18978                  Mateo Flores   

                                                   playerUrl Nationality  \
    0      http://sofifa.com/player/158023/lionel-messi/2...   Argentina   
    1      http://sofifa.com/player/20801/c-ronaldo-dos-s...    Portugal   
    2      http://sofifa.com/player/200389/jan-oblak/210005/    Slovenia   
    3      http://sofifa.com/player/192985/kevin-de-bruyn...     Belgium   
    4      http://sofifa.com/player/190871/neymar-da-silv...      Brazil   
    ...                                                  ...         ...   
    18974  http://sofifa.com/player/257710/mengxuan-zhang...    China PR   
    18975  http://sofifa.com/player/258736/vani-da-silva/...     England   
    18976     http://sofifa.com/player/247223/ao-xia/210005/    China PR   
    18977  http://sofifa.com/player/258760/ben-hough/210005/     England   
    18978  http://sofifa.com/player/255958/mateo-flores/2...     Bolivia   

          Positions               Name  Age  ↓OVA  POT  \
    0      RW ST CF           L. Messi   33    93   93   
    1         ST LW  Cristiano Ronaldo   35    92   92   
    2            GK           J. Oblak   27    91   93   
    3        CAM CM       K. De Bruyne   29    91   91   
    4        LW CAM          Neymar Jr   28    91   91   
    ...         ...                ...  ...   ...  ...   
    18974        CB     Zhang Mengxuan   21    47   52   
    18975        ST        V. Da Silva   17    47   67   
    18976        CB             Xia Ao   21    47   55   
    18977        CM           B. Hough   17    47   67   
    18978       CDM          M. Flores   19    47   63   

                                             Team & Contract  ...     A/W     D/W  \
    0                  \n\n\n\nFC Barcelona\n2004 ~ 2021\n\n  ...  Medium     Low   
    1                      \n\n\n\nJuventus\n2018 ~ 2022\n\n  ...    High     Low   
    2               \n\n\n\nAtlético Madrid\n2014 ~ 2023\n\n  ...  Medium  Medium   
    3               \n\n\n\nManchester City\n2015 ~ 2023\n\n  ...    High    High   
    4           \n\n\n\nParis Saint-Germain\n2017 ~ 2022\n\n  ...    High  Medium   
    ...                                                  ...  ...     ...     ...   
    18974  \n\n\n\nChongqing Dangdai Lifan FC SWM Team\n2...  ...     Low     Low   
    18975           \n\n\n\nOldham Athletic\n2020 ~ 2021\n\n  ...  Medium  Medium   
    18976                \n\n\n\nWuhan Zall\n2018 ~ 2022\n\n  ...  Medium  Medium   
    18977           \n\n\n\nOldham Athletic\n2020 ~ 2021\n\n  ...  Medium  Medium   
    18978              \n\n\n\nClub Bolívar\n2020 ~ 2024\n\n  ...  Medium  Medium   

            IR PAC  SHO PAS  DRI DEF PHY   Hits  
    0      5 ★  85   92  91   95  38  65  \n372  
    1      5 ★  89   93  81   89  35  77  \n344  
    2      3 ★  87   92  78   90  52  90   \n86  
    3      4 ★  76   86  93   88  64  78  \n163  
    4      5 ★  91   85  86   94  36  59  \n273  
    ...    ...  ..  ...  ..  ...  ..  ..    ...  
    18974  1 ★  58   23  26   27  50  48      2  
    18975  1 ★  70   46  40   53  16  40      3  
    18976  1 ★  64   28  26   38  48  51      3  
    18977  1 ★  64   40  48   49  35  45      5  
    18978  1 ★  57   32  43   48  44  49      2  

    [18979 rows x 77 columns]>
:::
:::

::: {#cc2052a4 .cell .code execution_count="10"}
``` python
fdf
```

::: {.output .execute_result execution_count="10"}
```{=html}
<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>photoUrl</th>
      <th>LongName</th>
      <th>playerUrl</th>
      <th>Nationality</th>
      <th>Positions</th>
      <th>Name</th>
      <th>Age</th>
      <th>↓OVA</th>
      <th>POT</th>
      <th>Team &amp; Contract</th>
      <th>...</th>
      <th>A/W</th>
      <th>D/W</th>
      <th>IR</th>
      <th>PAC</th>
      <th>SHO</th>
      <th>PAS</th>
      <th>DRI</th>
      <th>DEF</th>
      <th>PHY</th>
      <th>Hits</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>https://cdn.sofifa.com/players/158/023/21_60.png</td>
      <td>Lionel Messi</td>
      <td>http://sofifa.com/player/158023/lionel-messi/2...</td>
      <td>Argentina</td>
      <td>RW ST CF</td>
      <td>L. Messi</td>
      <td>33</td>
      <td>93</td>
      <td>93</td>
      <td>\n\n\n\nFC Barcelona\n2004 ~ 2021\n\n</td>
      <td>...</td>
      <td>Medium</td>
      <td>Low</td>
      <td>5 ★</td>
      <td>85</td>
      <td>92</td>
      <td>91</td>
      <td>95</td>
      <td>38</td>
      <td>65</td>
      <td>\n372</td>
    </tr>
    <tr>
      <th>1</th>
      <td>https://cdn.sofifa.com/players/020/801/21_60.png</td>
      <td>C. Ronaldo dos Santos Aveiro</td>
      <td>http://sofifa.com/player/20801/c-ronaldo-dos-s...</td>
      <td>Portugal</td>
      <td>ST LW</td>
      <td>Cristiano Ronaldo</td>
      <td>35</td>
      <td>92</td>
      <td>92</td>
      <td>\n\n\n\nJuventus\n2018 ~ 2022\n\n</td>
      <td>...</td>
      <td>High</td>
      <td>Low</td>
      <td>5 ★</td>
      <td>89</td>
      <td>93</td>
      <td>81</td>
      <td>89</td>
      <td>35</td>
      <td>77</td>
      <td>\n344</td>
    </tr>
    <tr>
      <th>2</th>
      <td>https://cdn.sofifa.com/players/200/389/21_60.png</td>
      <td>Jan Oblak</td>
      <td>http://sofifa.com/player/200389/jan-oblak/210005/</td>
      <td>Slovenia</td>
      <td>GK</td>
      <td>J. Oblak</td>
      <td>27</td>
      <td>91</td>
      <td>93</td>
      <td>\n\n\n\nAtlético Madrid\n2014 ~ 2023\n\n</td>
      <td>...</td>
      <td>Medium</td>
      <td>Medium</td>
      <td>3 ★</td>
      <td>87</td>
      <td>92</td>
      <td>78</td>
      <td>90</td>
      <td>52</td>
      <td>90</td>
      <td>\n86</td>
    </tr>
    <tr>
      <th>3</th>
      <td>https://cdn.sofifa.com/players/192/985/21_60.png</td>
      <td>Kevin De Bruyne</td>
      <td>http://sofifa.com/player/192985/kevin-de-bruyn...</td>
      <td>Belgium</td>
      <td>CAM CM</td>
      <td>K. De Bruyne</td>
      <td>29</td>
      <td>91</td>
      <td>91</td>
      <td>\n\n\n\nManchester City\n2015 ~ 2023\n\n</td>
      <td>...</td>
      <td>High</td>
      <td>High</td>
      <td>4 ★</td>
      <td>76</td>
      <td>86</td>
      <td>93</td>
      <td>88</td>
      <td>64</td>
      <td>78</td>
      <td>\n163</td>
    </tr>
    <tr>
      <th>4</th>
      <td>https://cdn.sofifa.com/players/190/871/21_60.png</td>
      <td>Neymar da Silva Santos Jr.</td>
      <td>http://sofifa.com/player/190871/neymar-da-silv...</td>
      <td>Brazil</td>
      <td>LW CAM</td>
      <td>Neymar Jr</td>
      <td>28</td>
      <td>91</td>
      <td>91</td>
      <td>\n\n\n\nParis Saint-Germain\n2017 ~ 2022\n\n</td>
      <td>...</td>
      <td>High</td>
      <td>Medium</td>
      <td>5 ★</td>
      <td>91</td>
      <td>85</td>
      <td>86</td>
      <td>94</td>
      <td>36</td>
      <td>59</td>
      <td>\n273</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>18974</th>
      <td>https://cdn.sofifa.com/players/257/710/21_60.png</td>
      <td>Mengxuan Zhang</td>
      <td>http://sofifa.com/player/257710/mengxuan-zhang...</td>
      <td>China PR</td>
      <td>CB</td>
      <td>Zhang Mengxuan</td>
      <td>21</td>
      <td>47</td>
      <td>52</td>
      <td>\n\n\n\nChongqing Dangdai Lifan FC SWM Team\n2...</td>
      <td>...</td>
      <td>Low</td>
      <td>Low</td>
      <td>1 ★</td>
      <td>58</td>
      <td>23</td>
      <td>26</td>
      <td>27</td>
      <td>50</td>
      <td>48</td>
      <td>2</td>
    </tr>
    <tr>
      <th>18975</th>
      <td>https://cdn.sofifa.com/players/258/736/21_60.png</td>
      <td>Vani Da Silva</td>
      <td>http://sofifa.com/player/258736/vani-da-silva/...</td>
      <td>England</td>
      <td>ST</td>
      <td>V. Da Silva</td>
      <td>17</td>
      <td>47</td>
      <td>67</td>
      <td>\n\n\n\nOldham Athletic\n2020 ~ 2021\n\n</td>
      <td>...</td>
      <td>Medium</td>
      <td>Medium</td>
      <td>1 ★</td>
      <td>70</td>
      <td>46</td>
      <td>40</td>
      <td>53</td>
      <td>16</td>
      <td>40</td>
      <td>3</td>
    </tr>
    <tr>
      <th>18976</th>
      <td>https://cdn.sofifa.com/players/247/223/21_60.png</td>
      <td>Ao Xia</td>
      <td>http://sofifa.com/player/247223/ao-xia/210005/</td>
      <td>China PR</td>
      <td>CB</td>
      <td>Xia Ao</td>
      <td>21</td>
      <td>47</td>
      <td>55</td>
      <td>\n\n\n\nWuhan Zall\n2018 ~ 2022\n\n</td>
      <td>...</td>
      <td>Medium</td>
      <td>Medium</td>
      <td>1 ★</td>
      <td>64</td>
      <td>28</td>
      <td>26</td>
      <td>38</td>
      <td>48</td>
      <td>51</td>
      <td>3</td>
    </tr>
    <tr>
      <th>18977</th>
      <td>https://cdn.sofifa.com/players/258/760/21_60.png</td>
      <td>Ben Hough</td>
      <td>http://sofifa.com/player/258760/ben-hough/210005/</td>
      <td>England</td>
      <td>CM</td>
      <td>B. Hough</td>
      <td>17</td>
      <td>47</td>
      <td>67</td>
      <td>\n\n\n\nOldham Athletic\n2020 ~ 2021\n\n</td>
      <td>...</td>
      <td>Medium</td>
      <td>Medium</td>
      <td>1 ★</td>
      <td>64</td>
      <td>40</td>
      <td>48</td>
      <td>49</td>
      <td>35</td>
      <td>45</td>
      <td>5</td>
    </tr>
    <tr>
      <th>18978</th>
      <td>https://cdn.sofifa.com/players/255/958/21_60.png</td>
      <td>Mateo Flores</td>
      <td>http://sofifa.com/player/255958/mateo-flores/2...</td>
      <td>Bolivia</td>
      <td>CDM</td>
      <td>M. Flores</td>
      <td>19</td>
      <td>47</td>
      <td>63</td>
      <td>\n\n\n\nClub Bolívar\n2020 ~ 2024\n\n</td>
      <td>...</td>
      <td>Medium</td>
      <td>Medium</td>
      <td>1 ★</td>
      <td>57</td>
      <td>32</td>
      <td>43</td>
      <td>48</td>
      <td>44</td>
      <td>49</td>
      <td>2</td>
    </tr>
  </tbody>
</table>
<p>18979 rows × 77 columns</p>
</div>
```
:::
:::

::: {#d486b64d .cell .markdown}
### REMOVING UNNECESSARY COLUMNS
:::

::: {#392cf3bb .cell .code execution_count="11"}
``` python
fdf.drop(columns=['photoUrl','playerUrl'],inplace=True)

fdf.head()
```

::: {.output .execute_result execution_count="11"}
```{=html}
<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>LongName</th>
      <th>Nationality</th>
      <th>Positions</th>
      <th>Name</th>
      <th>Age</th>
      <th>↓OVA</th>
      <th>POT</th>
      <th>Team &amp; Contract</th>
      <th>ID</th>
      <th>Height</th>
      <th>...</th>
      <th>A/W</th>
      <th>D/W</th>
      <th>IR</th>
      <th>PAC</th>
      <th>SHO</th>
      <th>PAS</th>
      <th>DRI</th>
      <th>DEF</th>
      <th>PHY</th>
      <th>Hits</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Lionel Messi</td>
      <td>Argentina</td>
      <td>RW ST CF</td>
      <td>L. Messi</td>
      <td>33</td>
      <td>93</td>
      <td>93</td>
      <td>\n\n\n\nFC Barcelona\n2004 ~ 2021\n\n</td>
      <td>158023</td>
      <td>5'7"</td>
      <td>...</td>
      <td>Medium</td>
      <td>Low</td>
      <td>5 ★</td>
      <td>85</td>
      <td>92</td>
      <td>91</td>
      <td>95</td>
      <td>38</td>
      <td>65</td>
      <td>\n372</td>
    </tr>
    <tr>
      <th>1</th>
      <td>C. Ronaldo dos Santos Aveiro</td>
      <td>Portugal</td>
      <td>ST LW</td>
      <td>Cristiano Ronaldo</td>
      <td>35</td>
      <td>92</td>
      <td>92</td>
      <td>\n\n\n\nJuventus\n2018 ~ 2022\n\n</td>
      <td>20801</td>
      <td>6'2"</td>
      <td>...</td>
      <td>High</td>
      <td>Low</td>
      <td>5 ★</td>
      <td>89</td>
      <td>93</td>
      <td>81</td>
      <td>89</td>
      <td>35</td>
      <td>77</td>
      <td>\n344</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Jan Oblak</td>
      <td>Slovenia</td>
      <td>GK</td>
      <td>J. Oblak</td>
      <td>27</td>
      <td>91</td>
      <td>93</td>
      <td>\n\n\n\nAtlético Madrid\n2014 ~ 2023\n\n</td>
      <td>200389</td>
      <td>6'2"</td>
      <td>...</td>
      <td>Medium</td>
      <td>Medium</td>
      <td>3 ★</td>
      <td>87</td>
      <td>92</td>
      <td>78</td>
      <td>90</td>
      <td>52</td>
      <td>90</td>
      <td>\n86</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Kevin De Bruyne</td>
      <td>Belgium</td>
      <td>CAM CM</td>
      <td>K. De Bruyne</td>
      <td>29</td>
      <td>91</td>
      <td>91</td>
      <td>\n\n\n\nManchester City\n2015 ~ 2023\n\n</td>
      <td>192985</td>
      <td>5'11"</td>
      <td>...</td>
      <td>High</td>
      <td>High</td>
      <td>4 ★</td>
      <td>76</td>
      <td>86</td>
      <td>93</td>
      <td>88</td>
      <td>64</td>
      <td>78</td>
      <td>\n163</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Neymar da Silva Santos Jr.</td>
      <td>Brazil</td>
      <td>LW CAM</td>
      <td>Neymar Jr</td>
      <td>28</td>
      <td>91</td>
      <td>91</td>
      <td>\n\n\n\nParis Saint-Germain\n2017 ~ 2022\n\n</td>
      <td>190871</td>
      <td>5'9"</td>
      <td>...</td>
      <td>High</td>
      <td>Medium</td>
      <td>5 ★</td>
      <td>91</td>
      <td>85</td>
      <td>86</td>
      <td>94</td>
      <td>36</td>
      <td>59</td>
      <td>\n273</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 75 columns</p>
</div>
```
:::
:::

::: {#b5562e91 .cell .markdown}
### CHANGING THE DATA TYPE
:::

::: {#63c7e87a .cell .code execution_count="12"}
``` python
fdf['Joined'] = pd.to_datetime(fdf['Joined'])
fdf['Loan Date End'] = pd.to_datetime(fdf['Loan Date End'])
```
:::

::: {#732763f1 .cell .code execution_count="13"}
``` python
fdf.info()
```

::: {.output .stream .stdout}
    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 18979 entries, 0 to 18978
    Data columns (total 75 columns):
     #   Column            Non-Null Count  Dtype         
    ---  ------            --------------  -----         
     0   LongName          18979 non-null  object        
     1   Nationality       18979 non-null  object        
     2   Positions         18979 non-null  object        
     3   Name              18979 non-null  object        
     4   Age               18979 non-null  int64         
     5   ↓OVA              18979 non-null  int64         
     6   POT               18979 non-null  int64         
     7   Team & Contract   18979 non-null  object        
     8   ID                18979 non-null  int64         
     9   Height            18979 non-null  object        
     10  Weight            18979 non-null  object        
     11  foot              18979 non-null  object        
     12  BOV               18979 non-null  int64         
     13  BP                18979 non-null  object        
     14  Growth            18979 non-null  int64         
     15  Joined            18979 non-null  datetime64[ns]
     16  Loan Date End     1013 non-null   datetime64[ns]
     17  Value             18979 non-null  object        
     18  Wage              18979 non-null  object        
     19  Release Clause    18979 non-null  object        
     20  Attacking         18979 non-null  int64         
     21  Crossing          18979 non-null  int64         
     22  Finishing         18979 non-null  int64         
     23  Heading Accuracy  18979 non-null  int64         
     24  Short Passing     18979 non-null  int64         
     25  Volleys           18979 non-null  int64         
     26  Skill             18979 non-null  int64         
     27  Dribbling         18979 non-null  int64         
     28  Curve             18979 non-null  int64         
     29  FK Accuracy       18979 non-null  int64         
     30  Long Passing      18979 non-null  int64         
     31  Ball Control      18979 non-null  int64         
     32  Movement          18979 non-null  int64         
     33  Acceleration      18979 non-null  int64         
     34  Sprint Speed      18979 non-null  int64         
     35  Agility           18979 non-null  int64         
     36  Reactions         18979 non-null  int64         
     37  Balance           18979 non-null  int64         
     38  Power             18979 non-null  int64         
     39  Shot Power        18979 non-null  int64         
     40  Jumping           18979 non-null  int64         
     41  Stamina           18979 non-null  int64         
     42  Strength          18979 non-null  int64         
     43  Long Shots        18979 non-null  int64         
     44  Mentality         18979 non-null  int64         
     45  Aggression        18979 non-null  int64         
     46  Interceptions     18979 non-null  int64         
     47  Positioning       18979 non-null  int64         
     48  Vision            18979 non-null  int64         
     49  Penalties         18979 non-null  int64         
     50  Composure         18979 non-null  int64         
     51  Defending         18979 non-null  int64         
     52  Marking           18979 non-null  int64         
     53  Standing Tackle   18979 non-null  int64         
     54  Sliding Tackle    18979 non-null  int64         
     55  Goalkeeping       18979 non-null  int64         
     56  GK Diving         18979 non-null  int64         
     57  GK Handling       18979 non-null  int64         
     58  GK Kicking        18979 non-null  int64         
     59  GK Positioning    18979 non-null  int64         
     60  GK Reflexes       18979 non-null  int64         
     61  Total Stats       18979 non-null  int64         
     62  Base Stats        18979 non-null  int64         
     63  W/F               18979 non-null  object        
     64  SM                18979 non-null  object        
     65  A/W               18979 non-null  object        
     66  D/W               18979 non-null  object        
     67  IR                18979 non-null  object        
     68  PAC               18979 non-null  int64         
     69  SHO               18979 non-null  int64         
     70  PAS               18979 non-null  int64         
     71  DRI               18979 non-null  int64         
     72  DEF               18979 non-null  int64         
     73  PHY               18979 non-null  int64         
     74  Hits              18979 non-null  object        
    dtypes: datetime64[ns](2), int64(55), object(18)
    memory usage: 10.9+ MB
:::
:::

::: {#2dde8b8b .cell .markdown}
### CLEANING THE DATA
:::

::: {#9e398a6b .cell .code execution_count="42"}
``` python
def cleaning(val):
  if isinstance(val,str):
    if val.find('\n'):
      return val.replace('\n','')
    else:
      return val
  else:
    return val
```
:::

::: {#32a7a28b .cell .code execution_count="43"}
``` python
fdf['Team & Contract']=fdf['Team & Contract'].apply(cleaning)
fdf['Hits']=fdf['Hits'].apply(cleaning)
```
:::

::: {#a5986353 .cell .code execution_count="44"}
``` python
fdf
```

::: {.output .execute_result execution_count="44"}
```{=html}
<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>LongName</th>
      <th>Nationality</th>
      <th>Positions</th>
      <th>Name</th>
      <th>Age</th>
      <th>OVA</th>
      <th>POT</th>
      <th>Team &amp; Contract</th>
      <th>ID</th>
      <th>Height</th>
      <th>...</th>
      <th>PAC</th>
      <th>SHO</th>
      <th>PAS</th>
      <th>DRI</th>
      <th>DEF</th>
      <th>PHY</th>
      <th>Hits</th>
      <th>Day</th>
      <th>Month</th>
      <th>Year</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Lionel Messi</td>
      <td>Argentina</td>
      <td>RW ST CF</td>
      <td>L. Messi</td>
      <td>33</td>
      <td>93</td>
      <td>93</td>
      <td>FC Barcelona2004 ~ 2021</td>
      <td>158023</td>
      <td>170.18</td>
      <td>...</td>
      <td>85</td>
      <td>92</td>
      <td>91</td>
      <td>95</td>
      <td>38</td>
      <td>65</td>
      <td>372.0</td>
      <td>1</td>
      <td>7</td>
      <td>2004</td>
    </tr>
    <tr>
      <th>1</th>
      <td>C. Ronaldo dos Santos Aveiro</td>
      <td>Portugal</td>
      <td>ST LW</td>
      <td>Cristiano Ronaldo</td>
      <td>35</td>
      <td>92</td>
      <td>92</td>
      <td>Juventus2018 ~ 2022</td>
      <td>20801</td>
      <td>187.96</td>
      <td>...</td>
      <td>89</td>
      <td>93</td>
      <td>81</td>
      <td>89</td>
      <td>35</td>
      <td>77</td>
      <td>344.0</td>
      <td>10</td>
      <td>7</td>
      <td>2018</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Jan Oblak</td>
      <td>Slovenia</td>
      <td>GK</td>
      <td>J. Oblak</td>
      <td>27</td>
      <td>91</td>
      <td>93</td>
      <td>Atlético Madrid2014 ~ 2023</td>
      <td>200389</td>
      <td>187.96</td>
      <td>...</td>
      <td>87</td>
      <td>92</td>
      <td>78</td>
      <td>90</td>
      <td>52</td>
      <td>90</td>
      <td>86.0</td>
      <td>16</td>
      <td>7</td>
      <td>2014</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Kevin De Bruyne</td>
      <td>Belgium</td>
      <td>CAM CM</td>
      <td>K. De Bruyne</td>
      <td>29</td>
      <td>91</td>
      <td>91</td>
      <td>Manchester City2015 ~ 2023</td>
      <td>192985</td>
      <td>180.34</td>
      <td>...</td>
      <td>76</td>
      <td>86</td>
      <td>93</td>
      <td>88</td>
      <td>64</td>
      <td>78</td>
      <td>163.0</td>
      <td>30</td>
      <td>8</td>
      <td>2015</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Neymar da Silva Santos Jr.</td>
      <td>Brazil</td>
      <td>LW CAM</td>
      <td>Neymar Jr</td>
      <td>28</td>
      <td>91</td>
      <td>91</td>
      <td>Paris Saint-Germain2017 ~ 2022</td>
      <td>190871</td>
      <td>175.26</td>
      <td>...</td>
      <td>91</td>
      <td>85</td>
      <td>86</td>
      <td>94</td>
      <td>36</td>
      <td>59</td>
      <td>273.0</td>
      <td>3</td>
      <td>8</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>18974</th>
      <td>Mengxuan Zhang</td>
      <td>China PR</td>
      <td>CB</td>
      <td>Zhang Mengxuan</td>
      <td>21</td>
      <td>47</td>
      <td>52</td>
      <td>Chongqing Dangdai Lifan FC SWM Team2020 ~ 2020</td>
      <td>257710</td>
      <td>177.80</td>
      <td>...</td>
      <td>58</td>
      <td>23</td>
      <td>26</td>
      <td>27</td>
      <td>50</td>
      <td>48</td>
      <td>2.0</td>
      <td>1</td>
      <td>8</td>
      <td>2020</td>
    </tr>
    <tr>
      <th>18975</th>
      <td>Vani Da Silva</td>
      <td>England</td>
      <td>ST</td>
      <td>V. Da Silva</td>
      <td>17</td>
      <td>47</td>
      <td>67</td>
      <td>Oldham Athletic2020 ~ 2021</td>
      <td>258736</td>
      <td>170.18</td>
      <td>...</td>
      <td>70</td>
      <td>46</td>
      <td>40</td>
      <td>53</td>
      <td>16</td>
      <td>40</td>
      <td>3.0</td>
      <td>1</td>
      <td>8</td>
      <td>2020</td>
    </tr>
    <tr>
      <th>18976</th>
      <td>Ao Xia</td>
      <td>China PR</td>
      <td>CB</td>
      <td>Xia Ao</td>
      <td>21</td>
      <td>47</td>
      <td>55</td>
      <td>Wuhan Zall2018 ~ 2022</td>
      <td>247223</td>
      <td>177.80</td>
      <td>...</td>
      <td>64</td>
      <td>28</td>
      <td>26</td>
      <td>38</td>
      <td>48</td>
      <td>51</td>
      <td>3.0</td>
      <td>13</td>
      <td>7</td>
      <td>2018</td>
    </tr>
    <tr>
      <th>18977</th>
      <td>Ben Hough</td>
      <td>England</td>
      <td>CM</td>
      <td>B. Hough</td>
      <td>17</td>
      <td>47</td>
      <td>67</td>
      <td>Oldham Athletic2020 ~ 2021</td>
      <td>258760</td>
      <td>175.26</td>
      <td>...</td>
      <td>64</td>
      <td>40</td>
      <td>48</td>
      <td>49</td>
      <td>35</td>
      <td>45</td>
      <td>5.0</td>
      <td>1</td>
      <td>8</td>
      <td>2020</td>
    </tr>
    <tr>
      <th>18978</th>
      <td>Mateo Flores</td>
      <td>Bolivia</td>
      <td>CDM</td>
      <td>M. Flores</td>
      <td>19</td>
      <td>47</td>
      <td>63</td>
      <td>Club Bolívar2020 ~ 2024</td>
      <td>255958</td>
      <td>175.26</td>
      <td>...</td>
      <td>57</td>
      <td>32</td>
      <td>43</td>
      <td>48</td>
      <td>44</td>
      <td>49</td>
      <td>2.0</td>
      <td>1</td>
      <td>1</td>
      <td>2020</td>
    </tr>
  </tbody>
</table>
<p>18979 rows × 78 columns</p>
</div>
```
:::
:::

::: {#fe9e535b .cell .code execution_count="17"}
``` python
fdf['Day'] =fdf['Joined'].dt.day
fdf['Month'] =fdf['Joined'].dt.month
fdf['Year'] = fdf['Joined'].dt.year
```
:::

::: {#b519db2b .cell .code execution_count="18"}
``` python
fdf.columns.tolist()
```

::: {.output .execute_result execution_count="18"}
    ['LongName',
     'Nationality',
     'Positions',
     'Name',
     'Age',
     '↓OVA',
     'POT',
     'Team & Contract',
     'ID',
     'Height',
     'Weight',
     'foot',
     'BOV',
     'BP',
     'Growth',
     'Joined',
     'Loan Date End',
     'Value',
     'Wage',
     'Release Clause',
     'Attacking',
     'Crossing',
     'Finishing',
     'Heading Accuracy',
     'Short Passing',
     'Volleys',
     'Skill',
     'Dribbling',
     'Curve',
     'FK Accuracy',
     'Long Passing',
     'Ball Control',
     'Movement',
     'Acceleration',
     'Sprint Speed',
     'Agility',
     'Reactions',
     'Balance',
     'Power',
     'Shot Power',
     'Jumping',
     'Stamina',
     'Strength',
     'Long Shots',
     'Mentality',
     'Aggression',
     'Interceptions',
     'Positioning',
     'Vision',
     'Penalties',
     'Composure',
     'Defending',
     'Marking',
     'Standing Tackle',
     'Sliding Tackle',
     'Goalkeeping',
     'GK Diving',
     'GK Handling',
     'GK Kicking',
     'GK Positioning',
     'GK Reflexes',
     'Total Stats',
     'Base Stats',
     'W/F',
     'SM',
     'A/W',
     'D/W',
     'IR',
     'PAC',
     'SHO',
     'PAS',
     'DRI',
     'DEF',
     'PHY',
     'Hits',
     'Day',
     'Month',
     'Year']
:::
:::

::: {#9bb3134d .cell .code execution_count="19"}
``` python
def obj_to_float(val):
    if isinstance(val, str):
        if val.find('cm')!=-1:
            val = val.replace('cm', '')
            return float(val)
        elif val.find("'")!=-1:
            val = val.split("\'")
            h = float(val[0])*(30.48) + float(val[1].replace('"', ''))*(2.54)
            return h
        elif val.find('kg')!=-1:
            val = val.replace('kg', '')
            return float(val)
        elif val.find('lbs')!=-1:
            val = val.replace('lbs', '')
            return float(val)*0.45359237
        elif val.find('K')!= -1:
            val = val.replace('K', '')
            return float(val)*1000
        else:
            return float(val)
    else:
        return val
```
:::

::: {#fdb6552c .cell .code execution_count="20"}
``` python
fdf['Height']=fdf['Height'].apply(obj_to_float)
fdf['Weight']=fdf['Weight'].apply(obj_to_float)
fdf['Hits']=fdf['Hits'].apply(obj_to_float)
```
:::

::: {#80e5cd22 .cell .code execution_count="21"}
``` python
fdf.rename(columns = {'↓OVA':'OVA'},inplace=True)
```
:::

::: {#cac5b851 .cell .code execution_count="22"}
``` python
def money(val):
    if isinstance(val, str):
        if val.find('K')!=-1:
            return float(val.replace('K', '').replace('€', ''))*1000*90.57
        elif val.find('M')!=-1:
            return float(val.replace('M', '').replace('€', ''))*10e6
        elif val.find('€')!=-1:
            return float(val.replace('€', ''))
        else:
            return val
    else:
        return val
```
:::

::: {#12baf8d7 .cell .code execution_count="23"}
``` python
fdf['Value'] =fdf['Value'].apply(money)
fdf['Release Clause'] = fdf['Release Clause'].apply(money)
fdf['Wage'] = fdf['Wage'].apply(money)
```
:::

::: {#76ee1c5c .cell .code execution_count="24"}
``` python
fdf.head()
```

::: {.output .execute_result execution_count="24"}
```{=html}
<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>LongName</th>
      <th>Nationality</th>
      <th>Positions</th>
      <th>Name</th>
      <th>Age</th>
      <th>OVA</th>
      <th>POT</th>
      <th>Team &amp; Contract</th>
      <th>ID</th>
      <th>Height</th>
      <th>...</th>
      <th>PAC</th>
      <th>SHO</th>
      <th>PAS</th>
      <th>DRI</th>
      <th>DEF</th>
      <th>PHY</th>
      <th>Hits</th>
      <th>Day</th>
      <th>Month</th>
      <th>Year</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Lionel Messi</td>
      <td>Argentina</td>
      <td>RW ST CF</td>
      <td>L. Messi</td>
      <td>33</td>
      <td>93</td>
      <td>93</td>
      <td>FC Barcelona\n2004 ~ 2021\n\n</td>
      <td>158023</td>
      <td>170.18</td>
      <td>...</td>
      <td>85</td>
      <td>92</td>
      <td>91</td>
      <td>95</td>
      <td>38</td>
      <td>65</td>
      <td>372.0</td>
      <td>1</td>
      <td>7</td>
      <td>2004</td>
    </tr>
    <tr>
      <th>1</th>
      <td>C. Ronaldo dos Santos Aveiro</td>
      <td>Portugal</td>
      <td>ST LW</td>
      <td>Cristiano Ronaldo</td>
      <td>35</td>
      <td>92</td>
      <td>92</td>
      <td>Juventus\n2018 ~ 2022\n\n</td>
      <td>20801</td>
      <td>187.96</td>
      <td>...</td>
      <td>89</td>
      <td>93</td>
      <td>81</td>
      <td>89</td>
      <td>35</td>
      <td>77</td>
      <td>344.0</td>
      <td>10</td>
      <td>7</td>
      <td>2018</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Jan Oblak</td>
      <td>Slovenia</td>
      <td>GK</td>
      <td>J. Oblak</td>
      <td>27</td>
      <td>91</td>
      <td>93</td>
      <td>Atlético Madrid\n2014 ~ 2023\n\n</td>
      <td>200389</td>
      <td>187.96</td>
      <td>...</td>
      <td>87</td>
      <td>92</td>
      <td>78</td>
      <td>90</td>
      <td>52</td>
      <td>90</td>
      <td>86.0</td>
      <td>16</td>
      <td>7</td>
      <td>2014</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Kevin De Bruyne</td>
      <td>Belgium</td>
      <td>CAM CM</td>
      <td>K. De Bruyne</td>
      <td>29</td>
      <td>91</td>
      <td>91</td>
      <td>Manchester City\n2015 ~ 2023\n\n</td>
      <td>192985</td>
      <td>180.34</td>
      <td>...</td>
      <td>76</td>
      <td>86</td>
      <td>93</td>
      <td>88</td>
      <td>64</td>
      <td>78</td>
      <td>163.0</td>
      <td>30</td>
      <td>8</td>
      <td>2015</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Neymar da Silva Santos Jr.</td>
      <td>Brazil</td>
      <td>LW CAM</td>
      <td>Neymar Jr</td>
      <td>28</td>
      <td>91</td>
      <td>91</td>
      <td>Paris Saint-Germain\n2017 ~ 2022\n\n</td>
      <td>190871</td>
      <td>175.26</td>
      <td>...</td>
      <td>91</td>
      <td>85</td>
      <td>86</td>
      <td>94</td>
      <td>36</td>
      <td>59</td>
      <td>273.0</td>
      <td>3</td>
      <td>8</td>
      <td>2017</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 78 columns</p>
</div>
```
:::
:::

::: {#d98162c8 .cell .markdown}
### ARRANGING & PLOTTING THE DATA {#arranging--plotting-the-data}

OVA stands for OFFENSIVE VALUE ADDED,it is a metric to measure a
player's attacking contribution in numbers its very difficult for
analyst to measure attack of players like a creative midfielder who was
highly dependent on his teammate to score. Therefore, the player was
only awarded the assist if the move ended with a goal. so to overcome
this OVA comes in picture.
:::

::: {#7914c223 .cell .code execution_count="25"}
``` python
fdf['OVA'].min()
```

::: {.output .execute_result execution_count="25"}
    47
:::
:::

::: {#5582890c .cell .markdown}
### TAKING RANGES OF OVA TO PLOT A GRAPH
:::

::: {#98f87359 .cell .code execution_count="26"}
``` python
ova_freq = [fdf.query(f'{i}<OVA <= {i+10}').shape[0] for i in range(40,100,10)]
ova_freq
```

::: {.output .execute_result execution_count="26"}
    [238, 3941, 10264, 4167, 363, 6]
:::
:::

::: {#45176e76 .cell .code execution_count="27"}
``` python
plt.figure(figsize = (10,10))
plt.title("Overall Rating Analysis")
plt.hist(fdf['OVA'], bins =[40,50,60,70,80,90,100], color = 'yellow', edgecolor = 'black')
plt.show()
```

::: {.output .display_data}
![](vertopal_a584e449c25547d2bf750a3376172d90/e229af530555f6ae84cbe3906feb0b86421463ba.png)
:::
:::

::: {#f3b571ad .cell .code execution_count="28"}
``` python
plt.figure(figsize = (20,10))
plt.title("Overall Rating Range")
plt.pie(ova_freq, autopct='%.2f', labels = [f'{i} to {i+10}' for i in range(40,100,10)])
plt.show()
```

::: {.output .display_data}
![](vertopal_a584e449c25547d2bf750a3376172d90/c6cc9fd42140ef38bf25ffc6104dd513cf51cf6d.png)
:::
:::

::: {#5d9639e7 .cell .code execution_count="29"}
``` python
plt.figure(figsize = (10,10))
sns.histplot(fdf['OVA'], bins =[40,50,60,70,80,90,100],color='orange', edgecolor = 'black', kde = True)
plt.show()
```

::: {.output .display_data}
![](vertopal_a584e449c25547d2bf750a3376172d90/c191b9c754f49d84b4eb55e744b73aac4adc5836.png)
:::
:::

::: {#4106e3b4 .cell .code execution_count="30"}
``` python
ova_wage = [fdf.query(f'{i}<OVA <= {i+10}')['Wage'].median() for i in range(40,100,10)]
ova_wage
```

::: {.output .execute_result execution_count="30"}
    [500.0, 950.0, 271710.0, 1449120.0, 7426739.999999999, 23095350.0]
:::
:::

::: {#f5130caa .cell .markdown}
## WAGES OF PLAYERS ACCORDING TO THIER OVA
:::

::: {#cf6c518e .cell .code execution_count="31"}
``` python
plt.bar([40,50,60,70,80,90], ova_wage, width = 10, align = 'edge', edgecolor = 'black')
plt.xticks(np.arange(40,101,10))
plt.show()
```

::: {.output .display_data}
![](vertopal_a584e449c25547d2bf750a3376172d90/87d3125243d9c9736ab78c6aa7e92428de4ee064.png)
:::
:::

::: {#fde5914f .cell .markdown}
## CONTRIBUTUON OF PLAYERS BY TOP NATIONS IN FIFA
:::

::: {#01f11996 .cell .code execution_count="32"}
``` python
Number_of_players= fdf.groupby(['Nationality']).size().sort_values(0,ascending=False)
Number_of_players.head(10)

Number_of_players.head(10).plot(kind='bar',color='c')
 
plt.xlabel("Nationality")
plt.ylabel("Number of players")
plt.title("Nationality of Players")
plt.show()
```

::: {.output .stream .stderr}
    C:\Users\91965\AppData\Local\Temp\ipykernel_15712\1184695446.py:1: FutureWarning: In a future version of pandas all arguments of Series.sort_values will be keyword-only.
      Number_of_players= fdf.groupby(['Nationality']).size().sort_values(0,ascending=False)
:::

::: {.output .display_data}
![](vertopal_a584e449c25547d2bf750a3376172d90/74d189fd4ef0f96dfd6e5322de1ecd57d691c6bd.png)
:::
:::

::: {#5596af72 .cell .code execution_count="33"}
``` python
Age_of_players=fdf.groupby(['Age']).size().sort_values(0,ascending=False)

Age_of_players.plot(kind='bar',color='green')
plt.xlabel("Age")
plt.ylabel("Number of players")
plt.title("Age of Players")
plt.show()
```

::: {.output .stream .stderr}
    C:\Users\91965\AppData\Local\Temp\ipykernel_15712\1226137006.py:1: FutureWarning: In a future version of pandas all arguments of Series.sort_values will be keyword-only.
      Age_of_players=fdf.groupby(['Age']).size().sort_values(0,ascending=False)
:::

::: {.output .display_data}
![](vertopal_a584e449c25547d2bf750a3376172d90/eebed2a516decfd7ad02541aacd45deb8c293e6b.png)
:::
:::
