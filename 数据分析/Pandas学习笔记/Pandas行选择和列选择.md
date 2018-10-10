
# Pandas行选择和列选择

本文的数据来源：[https://github.com/fivethirtyeight/data/tree/master/fandango](https://github.com/fivethirtyeight/data/tree/master/fandango)


```python
import pandas as pd

fandango = pd.read_csv('fandango_score_comparison.csv')
```


```python
fandango.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 146 entries, 0 to 145
    Data columns (total 22 columns):
    FILM                          146 non-null object
    RottenTomatoes                146 non-null int64
    RottenTomatoes_User           146 non-null int64
    Metacritic                    146 non-null int64
    Metacritic_User               146 non-null float64
    IMDB                          146 non-null float64
    Fandango_Stars                146 non-null float64
    Fandango_Ratingvalue          146 non-null float64
    RT_norm                       146 non-null float64
    RT_user_norm                  146 non-null float64
    Metacritic_norm               146 non-null float64
    Metacritic_user_nom           146 non-null float64
    IMDB_norm                     146 non-null float64
    RT_norm_round                 146 non-null float64
    RT_user_norm_round            146 non-null float64
    Metacritic_norm_round         146 non-null float64
    Metacritic_user_norm_round    146 non-null float64
    IMDB_norm_round               146 non-null float64
    Metacritic_user_vote_count    146 non-null int64
    IMDB_user_vote_count          146 non-null int64
    Fandango_votes                146 non-null int64
    Fandango_Difference           146 non-null float64
    dtypes: float64(15), int64(6), object(1)
    memory usage: 25.2+ KB
    

## 行选择
Pandas进行行选择一般有三种方法：

- 连续多行的选择用类似于python的列表切片
- 按照指定的索引选择一行或多行，使用`loc[]`方法
- 按照指定的位置选择一行多多行，使用`iloc[]`方法

### 第一种


```python
df1 = fandango[1:3]
df1
```



<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>FILM</th>
      <th>RottenTomatoes</th>
      <th>RottenTomatoes_User</th>
      <th>Metacritic</th>
      <th>Metacritic_User</th>
      <th>IMDB</th>
      <th>Fandango_Stars</th>
      <th>Fandango_Ratingvalue</th>
      <th>RT_norm</th>
      <th>RT_user_norm</th>
      <th>...</th>
      <th>IMDB_norm</th>
      <th>RT_norm_round</th>
      <th>RT_user_norm_round</th>
      <th>Metacritic_norm_round</th>
      <th>Metacritic_user_norm_round</th>
      <th>IMDB_norm_round</th>
      <th>Metacritic_user_vote_count</th>
      <th>IMDB_user_vote_count</th>
      <th>Fandango_votes</th>
      <th>Fandango_Difference</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>Cinderella (2015)</td>
      <td>85</td>
      <td>80</td>
      <td>67</td>
      <td>7.5</td>
      <td>7.1</td>
      <td>5.0</td>
      <td>4.5</td>
      <td>4.25</td>
      <td>4.0</td>
      <td>...</td>
      <td>3.55</td>
      <td>4.5</td>
      <td>4.0</td>
      <td>3.5</td>
      <td>4.0</td>
      <td>3.5</td>
      <td>249</td>
      <td>65709</td>
      <td>12640</td>
      <td>0.5</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Ant-Man (2015)</td>
      <td>80</td>
      <td>90</td>
      <td>64</td>
      <td>8.1</td>
      <td>7.8</td>
      <td>5.0</td>
      <td>4.5</td>
      <td>4.00</td>
      <td>4.5</td>
      <td>...</td>
      <td>3.90</td>
      <td>4.0</td>
      <td>4.5</td>
      <td>3.0</td>
      <td>4.0</td>
      <td>4.0</td>
      <td>627</td>
      <td>103660</td>
      <td>12055</td>
      <td>0.5</td>
    </tr>
  </tbody>
</table>
<p>2 rows × 22 columns</p>
</div>



从结果可以看到，和python的列表切片一样，索引号从0开始，选择了索引号1和2的数据（不包括3）

### 第二种
通过指定列名选择多列。


```python
df2 = fandango.loc[1]
df2
```




    FILM                          Cinderella (2015)
    RottenTomatoes                               85
    RottenTomatoes_User                          80
    Metacritic                                   67
    Metacritic_User                             7.5
    IMDB                                        7.1
    Fandango_Stars                                5
    Fandango_Ratingvalue                        4.5
    RT_norm                                    4.25
    RT_user_norm                                  4
    Metacritic_norm                            3.35
    Metacritic_user_nom                        3.75
    IMDB_norm                                  3.55
    RT_norm_round                               4.5
    RT_user_norm_round                            4
    Metacritic_norm_round                       3.5
    Metacritic_user_norm_round                    4
    IMDB_norm_round                             3.5
    Metacritic_user_vote_count                  249
    IMDB_user_vote_count                      65709
    Fandango_votes                            12640
    Fandango_Difference                         0.5
    Name: 1, dtype: object




```python
df3 = fandango.loc[1:3]
df3
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>FILM</th>
      <th>RottenTomatoes</th>
      <th>RottenTomatoes_User</th>
      <th>Metacritic</th>
      <th>Metacritic_User</th>
      <th>IMDB</th>
      <th>Fandango_Stars</th>
      <th>Fandango_Ratingvalue</th>
      <th>RT_norm</th>
      <th>RT_user_norm</th>
      <th>...</th>
      <th>IMDB_norm</th>
      <th>RT_norm_round</th>
      <th>RT_user_norm_round</th>
      <th>Metacritic_norm_round</th>
      <th>Metacritic_user_norm_round</th>
      <th>IMDB_norm_round</th>
      <th>Metacritic_user_vote_count</th>
      <th>IMDB_user_vote_count</th>
      <th>Fandango_votes</th>
      <th>Fandango_Difference</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>Cinderella (2015)</td>
      <td>85</td>
      <td>80</td>
      <td>67</td>
      <td>7.5</td>
      <td>7.1</td>
      <td>5.0</td>
      <td>4.5</td>
      <td>4.25</td>
      <td>4.0</td>
      <td>...</td>
      <td>3.55</td>
      <td>4.5</td>
      <td>4.0</td>
      <td>3.5</td>
      <td>4.0</td>
      <td>3.5</td>
      <td>249</td>
      <td>65709</td>
      <td>12640</td>
      <td>0.5</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Ant-Man (2015)</td>
      <td>80</td>
      <td>90</td>
      <td>64</td>
      <td>8.1</td>
      <td>7.8</td>
      <td>5.0</td>
      <td>4.5</td>
      <td>4.00</td>
      <td>4.5</td>
      <td>...</td>
      <td>3.90</td>
      <td>4.0</td>
      <td>4.5</td>
      <td>3.0</td>
      <td>4.0</td>
      <td>4.0</td>
      <td>627</td>
      <td>103660</td>
      <td>12055</td>
      <td>0.5</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Do You Believe? (2015)</td>
      <td>18</td>
      <td>84</td>
      <td>22</td>
      <td>4.7</td>
      <td>5.4</td>
      <td>5.0</td>
      <td>4.5</td>
      <td>0.90</td>
      <td>4.2</td>
      <td>...</td>
      <td>2.70</td>
      <td>1.0</td>
      <td>4.0</td>
      <td>1.0</td>
      <td>2.5</td>
      <td>2.5</td>
      <td>31</td>
      <td>3136</td>
      <td>1793</td>
      <td>0.5</td>
    </tr>
  </tbody>
</table>
<p>3 rows × 22 columns</p>
</div>



可以看到，df2是一个Series，选择了索引号为1的那一行数据，注意df3，它与第一种的列表索引最大的不同是包含了索引号为3的那一行数据。


```python
df4 = fandango.loc[[1,3]]
df4
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>FILM</th>
      <th>RottenTomatoes</th>
      <th>RottenTomatoes_User</th>
      <th>Metacritic</th>
      <th>Metacritic_User</th>
      <th>IMDB</th>
      <th>Fandango_Stars</th>
      <th>Fandango_Ratingvalue</th>
      <th>RT_norm</th>
      <th>RT_user_norm</th>
      <th>...</th>
      <th>IMDB_norm</th>
      <th>RT_norm_round</th>
      <th>RT_user_norm_round</th>
      <th>Metacritic_norm_round</th>
      <th>Metacritic_user_norm_round</th>
      <th>IMDB_norm_round</th>
      <th>Metacritic_user_vote_count</th>
      <th>IMDB_user_vote_count</th>
      <th>Fandango_votes</th>
      <th>Fandango_Difference</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>Cinderella (2015)</td>
      <td>85</td>
      <td>80</td>
      <td>67</td>
      <td>7.5</td>
      <td>7.1</td>
      <td>5.0</td>
      <td>4.5</td>
      <td>4.25</td>
      <td>4.0</td>
      <td>...</td>
      <td>3.55</td>
      <td>4.5</td>
      <td>4.0</td>
      <td>3.5</td>
      <td>4.0</td>
      <td>3.5</td>
      <td>249</td>
      <td>65709</td>
      <td>12640</td>
      <td>0.5</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Do You Believe? (2015)</td>
      <td>18</td>
      <td>84</td>
      <td>22</td>
      <td>4.7</td>
      <td>5.4</td>
      <td>5.0</td>
      <td>4.5</td>
      <td>0.90</td>
      <td>4.2</td>
      <td>...</td>
      <td>2.70</td>
      <td>1.0</td>
      <td>4.0</td>
      <td>1.0</td>
      <td>2.5</td>
      <td>2.5</td>
      <td>31</td>
      <td>3136</td>
      <td>1793</td>
      <td>0.5</td>
    </tr>
  </tbody>
</table>
<p>2 rows × 22 columns</p>
</div>



这里按照索引号选择不连续的行。

### 第三种
在上面的数据中，使用`iloc[]`和`loc[]`的效果是一样的，因为索引号都是从0开始并且连续不断，现在删除索引号为1和2的这两行。


```python
fandango_drop = fandango.drop([1,2], axis=0)
```

此时如果仍然用`loc[]`来索引行号为2的那一行，就会出错，这时候可以使用`iloc[]`来进行选择。


```python
df5 = fandango_drop.iloc[2]
df5
```




    FILM                          Hot Tub Time Machine 2 (2015)
    RottenTomatoes                                           14
    RottenTomatoes_User                                      28
    Metacritic                                               29
    Metacritic_User                                         3.4
    IMDB                                                    5.1
    Fandango_Stars                                          3.5
    Fandango_Ratingvalue                                      3
    RT_norm                                                 0.7
    RT_user_norm                                            1.4
    Metacritic_norm                                        1.45
    Metacritic_user_nom                                     1.7
    IMDB_norm                                              2.55
    RT_norm_round                                           0.5
    RT_user_norm_round                                      1.5
    Metacritic_norm_round                                   1.5
    Metacritic_user_norm_round                              1.5
    IMDB_norm_round                                         2.5
    Metacritic_user_vote_count                               88
    IMDB_user_vote_count                                  19560
    Fandango_votes                                         1021
    Fandango_Difference                                     0.5
    Name: 4, dtype: object



看到了吧，`iloc[2]`的意思是选择第三行的数据，也就是索引号为4的那一行数据，因为`iloc[]`的计算也是从0开始的，所以`iloc[]`适用于数据进行了筛选后造成索引号与原来不一致的情况

`loc[]`与`iloc[]`方法之间还有一个巨大的差别，那就是`loc[]`里的参数是对应的索引值即可，所以参数可以是整数，也可以是字符串。而`iloc[]`里的参数表示的是第几行的数据，所以只能是整数。

## 列选择
列选择比较简单，只要直接把列名传递过去即可，如果有多列的数据，要单独指出列名或列的索引号。

### 第一种
选择单列（电影名称）。


```python
df6 = fandango['FILM']
df6
```




    0                      Avengers: Age of Ultron (2015)
    1                                   Cinderella (2015)
    2                                      Ant-Man (2015)
    3                              Do You Believe? (2015)
    4                       Hot Tub Time Machine 2 (2015)
    5                            The Water Diviner (2015)
    6                               Irrational Man (2015)
    7                                     Top Five (2014)
    8                        Shaun the Sheep Movie (2015)
    9                                 Love & Mercy (2015)
    10                  Far From The Madding Crowd (2015)
    11                                   Black Sea (2015)
    12                                   Leviathan (2014)
    13                                    Unbroken (2014)
    14                          The Imitation Game (2014)
    15                                     Taken 3 (2015)
    16                                       Ted 2 (2015)
    17                                    Southpaw (2015)
    18     Night at the Museum: Secret of the Tomb (2014)
    19                                      Pixels (2015)
    20                              McFarland, USA (2015)
    21                        Insidious: Chapter 3 (2015)
    22                     The Man From U.N.C.L.E. (2015)
    23                               Run All Night (2015)
    24                                  Trainwreck (2015)
    25                                       Selma (2014)
    26                                  Ex Machina (2015)
    27                                 Still Alice (2015)
    28                                  Wild Tales (2014)
    29                         The End of the Tour (2015)
                                ...                      
    116                       Clouds of Sils Maria (2015)
    117                         Testament of Youth (2015)
    118                      Infinitely Polar Bear (2015)
    119                                    Phoenix (2015)
    120                               The Wolfpack (2015)
    121             The Stanford Prison Experiment (2015)
    122                                  Tangerine (2015)
    123                             Magic Mike XXL (2015)
    124                                       Home (2015)
    125                         The Wedding Ringer (2015)
    126                              Woman in Gold (2015)
    127                        The Last Five Years (2015)
    128       Mission: Impossible â€“ Rogue Nation (2015)
    129                                        Amy (2015)
    130                             Jurassic World (2015)
    131                                    Minions (2015)
    132                                        Max (2015)
    133                     Paul Blart: Mall Cop 2 (2015)
    134                           The Longest Ride (2015)
    135                         The Lazarus Effect (2015)
    136        The Woman In Black 2 Angel of Death (2015)
    137                              Danny Collins (2015)
    138                                Spare Parts (2015)
    139                                     Serena (2015)
    140                                 Inside Out (2015)
    141                                 Mr. Holmes (2015)
    142                                        '71 (2015)
    143                        Two Days, One Night (2014)
    144         Gett: The Trial of Viviane Amsalem (2015)
    145                Kumiko, The Treasure Hunter (2015)
    Name: FILM, Length: 146, dtype: object



### 第二种



```python
df7 = fandango[['FILM','Metacritic']]
df7
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>FILM</th>
      <th>Metacritic</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Avengers: Age of Ultron (2015)</td>
      <td>66</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Cinderella (2015)</td>
      <td>67</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Ant-Man (2015)</td>
      <td>64</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Do You Believe? (2015)</td>
      <td>22</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Hot Tub Time Machine 2 (2015)</td>
      <td>29</td>
    </tr>
    <tr>
      <th>5</th>
      <td>The Water Diviner (2015)</td>
      <td>50</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Irrational Man (2015)</td>
      <td>53</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Top Five (2014)</td>
      <td>81</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Shaun the Sheep Movie (2015)</td>
      <td>81</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Love &amp; Mercy (2015)</td>
      <td>80</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Far From The Madding Crowd (2015)</td>
      <td>71</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Black Sea (2015)</td>
      <td>62</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Leviathan (2014)</td>
      <td>92</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Unbroken (2014)</td>
      <td>59</td>
    </tr>
    <tr>
      <th>14</th>
      <td>The Imitation Game (2014)</td>
      <td>73</td>
    </tr>
    <tr>
      <th>15</th>
      <td>Taken 3 (2015)</td>
      <td>26</td>
    </tr>
    <tr>
      <th>16</th>
      <td>Ted 2 (2015)</td>
      <td>48</td>
    </tr>
    <tr>
      <th>17</th>
      <td>Southpaw (2015)</td>
      <td>57</td>
    </tr>
    <tr>
      <th>18</th>
      <td>Night at the Museum: Secret of the Tomb (2014)</td>
      <td>47</td>
    </tr>
    <tr>
      <th>19</th>
      <td>Pixels (2015)</td>
      <td>27</td>
    </tr>
    <tr>
      <th>20</th>
      <td>McFarland, USA (2015)</td>
      <td>60</td>
    </tr>
    <tr>
      <th>21</th>
      <td>Insidious: Chapter 3 (2015)</td>
      <td>52</td>
    </tr>
    <tr>
      <th>22</th>
      <td>The Man From U.N.C.L.E. (2015)</td>
      <td>55</td>
    </tr>
    <tr>
      <th>23</th>
      <td>Run All Night (2015)</td>
      <td>59</td>
    </tr>
    <tr>
      <th>24</th>
      <td>Trainwreck (2015)</td>
      <td>75</td>
    </tr>
    <tr>
      <th>25</th>
      <td>Selma (2014)</td>
      <td>89</td>
    </tr>
    <tr>
      <th>26</th>
      <td>Ex Machina (2015)</td>
      <td>78</td>
    </tr>
    <tr>
      <th>27</th>
      <td>Still Alice (2015)</td>
      <td>72</td>
    </tr>
    <tr>
      <th>28</th>
      <td>Wild Tales (2014)</td>
      <td>77</td>
    </tr>
    <tr>
      <th>29</th>
      <td>The End of the Tour (2015)</td>
      <td>84</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>116</th>
      <td>Clouds of Sils Maria (2015)</td>
      <td>78</td>
    </tr>
    <tr>
      <th>117</th>
      <td>Testament of Youth (2015)</td>
      <td>77</td>
    </tr>
    <tr>
      <th>118</th>
      <td>Infinitely Polar Bear (2015)</td>
      <td>64</td>
    </tr>
    <tr>
      <th>119</th>
      <td>Phoenix (2015)</td>
      <td>91</td>
    </tr>
    <tr>
      <th>120</th>
      <td>The Wolfpack (2015)</td>
      <td>75</td>
    </tr>
    <tr>
      <th>121</th>
      <td>The Stanford Prison Experiment (2015)</td>
      <td>68</td>
    </tr>
    <tr>
      <th>122</th>
      <td>Tangerine (2015)</td>
      <td>86</td>
    </tr>
    <tr>
      <th>123</th>
      <td>Magic Mike XXL (2015)</td>
      <td>60</td>
    </tr>
    <tr>
      <th>124</th>
      <td>Home (2015)</td>
      <td>55</td>
    </tr>
    <tr>
      <th>125</th>
      <td>The Wedding Ringer (2015)</td>
      <td>35</td>
    </tr>
    <tr>
      <th>126</th>
      <td>Woman in Gold (2015)</td>
      <td>51</td>
    </tr>
    <tr>
      <th>127</th>
      <td>The Last Five Years (2015)</td>
      <td>60</td>
    </tr>
    <tr>
      <th>128</th>
      <td>Mission: Impossible â€“ Rogue Nation (2015)</td>
      <td>75</td>
    </tr>
    <tr>
      <th>129</th>
      <td>Amy (2015)</td>
      <td>85</td>
    </tr>
    <tr>
      <th>130</th>
      <td>Jurassic World (2015)</td>
      <td>59</td>
    </tr>
    <tr>
      <th>131</th>
      <td>Minions (2015)</td>
      <td>56</td>
    </tr>
    <tr>
      <th>132</th>
      <td>Max (2015)</td>
      <td>47</td>
    </tr>
    <tr>
      <th>133</th>
      <td>Paul Blart: Mall Cop 2 (2015)</td>
      <td>13</td>
    </tr>
    <tr>
      <th>134</th>
      <td>The Longest Ride (2015)</td>
      <td>33</td>
    </tr>
    <tr>
      <th>135</th>
      <td>The Lazarus Effect (2015)</td>
      <td>31</td>
    </tr>
    <tr>
      <th>136</th>
      <td>The Woman In Black 2 Angel of Death (2015)</td>
      <td>42</td>
    </tr>
    <tr>
      <th>137</th>
      <td>Danny Collins (2015)</td>
      <td>58</td>
    </tr>
    <tr>
      <th>138</th>
      <td>Spare Parts (2015)</td>
      <td>50</td>
    </tr>
    <tr>
      <th>139</th>
      <td>Serena (2015)</td>
      <td>36</td>
    </tr>
    <tr>
      <th>140</th>
      <td>Inside Out (2015)</td>
      <td>94</td>
    </tr>
    <tr>
      <th>141</th>
      <td>Mr. Holmes (2015)</td>
      <td>67</td>
    </tr>
    <tr>
      <th>142</th>
      <td>'71 (2015)</td>
      <td>83</td>
    </tr>
    <tr>
      <th>143</th>
      <td>Two Days, One Night (2014)</td>
      <td>89</td>
    </tr>
    <tr>
      <th>144</th>
      <td>Gett: The Trial of Viviane Amsalem (2015)</td>
      <td>90</td>
    </tr>
    <tr>
      <th>145</th>
      <td>Kumiko, The Treasure Hunter (2015)</td>
      <td>68</td>
    </tr>
  </tbody>
</table>
<p>146 rows × 2 columns</p>
</div>


