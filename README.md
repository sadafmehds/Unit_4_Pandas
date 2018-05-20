

```python
import os
import pandas as pd
import numpy as np
import json
from pprint import pprint
#import sys
#print(sys.version)

json_path = os.path.join('Resources/purchase_data.json')
with open(json_path) as json_data:
    data=json.load(json_data)
    json_data.close()
    #pprint(data)

```


```python
game_data=pd.DataFrame(data)
game_data.head()
```




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
      <th>Age</th>
      <th>Gender</th>
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Price</th>
      <th>SN</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>38</td>
      <td>Male</td>
      <td>165</td>
      <td>Bone Crushing Silver Skewer</td>
      <td>3.37</td>
      <td>Aelalis34</td>
    </tr>
    <tr>
      <th>1</th>
      <td>21</td>
      <td>Male</td>
      <td>119</td>
      <td>Stormbringer, Dark Blade of Ending Misery</td>
      <td>2.32</td>
      <td>Eolo46</td>
    </tr>
    <tr>
      <th>2</th>
      <td>34</td>
      <td>Male</td>
      <td>174</td>
      <td>Primitive Blade</td>
      <td>2.46</td>
      <td>Assastnya25</td>
    </tr>
    <tr>
      <th>3</th>
      <td>21</td>
      <td>Male</td>
      <td>92</td>
      <td>Final Critic</td>
      <td>1.36</td>
      <td>Pheusrical25</td>
    </tr>
    <tr>
      <th>4</th>
      <td>23</td>
      <td>Male</td>
      <td>63</td>
      <td>Stormfury Mace</td>
      <td>1.27</td>
      <td>Aela59</td>
    </tr>
  </tbody>
</table>
</div>




```python
#PLAYER COUNT
```


```python
#Total number of players
players=game_data["SN"].value_counts()
total_players=len(players)
total_players

    #long code practice
# player_ids_unique=[]
# for i in game_data["SN"]:
#     if i not in player_ids_unique:
#         player_ids_unique.append(i)
# number_of_players=len(player_ids_unique)
# print(number_of_players)
```




    573




```python
tot_players=pd.DataFrame({"Total Players":[total_players]})
tot_players

```




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
      <th>Total Players</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>573</td>
    </tr>
  </tbody>
</table>
</div>




```python
#PURCHASING ANALYSIS (TOTAL)

```


```python
## Number of Unique Items

# unique_items=[]
# for i in game_data["Item ID"]:
#     if i not in unique_items:
#         unique_items.append(i)
# number_of_unique_items=len(unique_items)
# print(number_of_unique_items)

unique_items=game_data["Item ID"].value_counts()
number_of_unique_items=len(unique_items)
number_of_unique_items
    
```




    183




```python
# Average Purchase Price
avg_purchase_price=round(game_data["Price"].mean(),2)
avg_purchase_price

```




    2.93




```python
# Total Number of Purchases
total_purchases=len(game_data)
total_purchases
```




    780




```python
# Total Revenue
total_revenue=game_data["Price"].sum()
total_revenue
```




    2286.33




```python
purchasing_analysis_total=pd.DataFrame({"Number of Unique Items":[number_of_unique_items],"Average Price":[avg_purchase_price],"Number of Purchases":[total_purchases],"Total Revenue":[total_revenue]})
purchasing_analysis_total[["Number of Unique Items","Number of Purchases","Average Price","Total Revenue"]]
purchasing_analysis_total["Average Price"]=purchasing_analysis_total["Average Price"].map("${:.2f}".format)
purchasing_analysis_total["Total Revenue"]=purchasing_analysis_total["Total Revenue"].map("${:.2f}".format)

#how do you do two formats per column ($ and , together?)
purchasing_analysis_total[["Number of Unique Items","Average Price","Number of Purchases","Total Revenue"]]
```




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
      <th>Number of Unique Items</th>
      <th>Average Price</th>
      <th>Number of Purchases</th>
      <th>Total Revenue</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>183</td>
      <td>$2.93</td>
      <td>780</td>
      <td>$2286.33</td>
    </tr>
  </tbody>
</table>
</div>




```python
#GENDER DEMOGRAPHICS

```


```python
# Percentage and Count of Male Players
#Male count
males_only_dataframe=game_data.loc[game_data["Gender"]=="Male"]
unique_males=males_only_dataframe["SN"].value_counts()
unique_males_count=len(unique_males)
unique_males_count
#Male percentage
male_percentage=round((unique_males_count/total_players)*100,2)
male_percentage
```




    81.15




```python
# Percentage and Count of Female Players
#female count
females_only_dataframe=game_data.loc[game_data["Gender"]=="Female"]
unique_females=females_only_dataframe["SN"].value_counts()
unique_females_count=len(unique_females)
unique_females_count
#female percentage
female_percentage=round((unique_females_count/total_players)*100,2)
female_percentage

```




    17.45




```python
# Percentage and Count of Other / Non-Disclosed
#count of other/non-disclosed
m_o_dataframe=game_data.loc[game_data["Gender"]!="Female"]
other_dataframe=m_o_dataframe.loc[m_o_dataframe["Gender"]!="Male"]
other_dataframe

other_nd_count=total_players-(unique_males_count+unique_females_count)
other_nd_count
#Percentage other/non-disclosed
percentage_other_nd=round((other_nd_count/total_players)*100,2)
percentage_other_nd

```




    1.4




```python
gender_demo_df=pd.DataFrame({"Player Count":[unique_males_count,unique_females_count,other_nd_count],"Percentage Purchase":[male_percentage,female_percentage,percentage_other_nd]})
gender_demo_df.index=["Male","Female","Other"]
gender_demo_df=gender_demo_df[["Player Count","Percentage Purchase"]]
gender_demo_df["Percentage Purchase"]=gender_demo_df["Percentage Purchase"].map("%{:.2f}".format)
gender_demo_df
```




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
      <th>Player Count</th>
      <th>Percentage Purchase</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Male</th>
      <td>465</td>
      <td>%81.15</td>
    </tr>
    <tr>
      <th>Female</th>
      <td>100</td>
      <td>%17.45</td>
    </tr>
    <tr>
      <th>Other</th>
      <td>8</td>
      <td>%1.40</td>
    </tr>
  </tbody>
</table>
</div>




```python
#PURCHASING ANALYSIS(BY GENDER)




```


```python
# Purchase Count by Gender
#Male purchase count
male_purchases=len(males_only_dataframe)
male_purchases

#Female purchase count
female_purchases=len(females_only_dataframe)
female_purchases

#other purchase count
other_purchases=len(other_dataframe)
other_purchases
```




    11




```python
# Average Purchase Price by Gender
#average male purchase price
avg_male_price=round(males_only_dataframe["Price"].sum()/male_purchases,2)
avg_male_price
#average female purchase price
avg_female_price=round(females_only_dataframe["Price"].sum()/female_purchases,2)
avg_female_price

#average other purchase price
avg_other_price=round(other_dataframe["Price"].sum()/other_purchases,2)
avg_other_price
```




    3.25




```python
# Total Purchase Value by Gender
#male
total_m_value=round(males_only_dataframe["Price"].sum(),2)
total_m_value

#female
total_f_value=round(females_only_dataframe["Price"].sum(),2)
total_f_value

#other
total_o_value=round(other_dataframe["Price"].sum(),2)
total_o_value
```




    35.74




```python
# Normalized Totals by Gender
totals=[total_m_value,total_f_value,total_o_value]
totals_dataframe=pd.DataFrame(totals)
totals_dataframe.head()

totals_dataframe[0].mean()
totals_dataframe[0].std()
#Male
#Female
```




    973.0598752903134




```python
gendered_purch_analysis=pd.DataFrame({"Gender":["Male","Female","Other/Non-Disclosed"],"Purchase Count":[male_purchases,female_purchases,other_purchases],
                                     "Average Purchase Price":[avg_male_price,avg_female_price,avg_other_price],
                                     "Total Purchase Value":[total_m_value,total_f_value,total_o_value]
                                    
                                    })
gendered_purch_analysis=gendered_purch_analysis[["Gender","Purchase Count","Average Purchase Price","Total Purchase Value"]]


#gendered_purch_analysis
```


```python

unique_counts=[unique_males_count,unique_females_count,other_nd_count]
normal=((gendered_purch_analysis["Total Purchase Value"])/(unique_counts))


gendered_purch_analysis["Normalized Totals"]=normal

gendered_purch_analysis["Average Purchase Price"]=gendered_purch_analysis["Average Purchase Price"].map("${:.2f}".format)
gendered_purch_analysis["Total Purchase Value"]=gendered_purch_analysis["Total Purchase Value"].map("${:.2f}".format)
gendered_purch_analysis["Normalized Totals"]=gendered_purch_analysis["Normalized Totals"].map("${:.2f}".format)

gendered_purch_analysis.head()

```




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
      <th>Gender</th>
      <th>Purchase Count</th>
      <th>Average Purchase Price</th>
      <th>Total Purchase Value</th>
      <th>Normalized Totals</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Male</td>
      <td>633</td>
      <td>$2.95</td>
      <td>$1867.68</td>
      <td>$4.02</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Female</td>
      <td>136</td>
      <td>$2.82</td>
      <td>$382.91</td>
      <td>$3.83</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Other/Non-Disclosed</td>
      <td>11</td>
      <td>$3.25</td>
      <td>$35.74</td>
      <td>$4.47</td>
    </tr>
  </tbody>
</table>
</div>




```python
##AGE DEMOGRAPHICS

 




```


```python
bins=[0,9,14,19,24,29,34,39,44,49] #bin's boolean is by default right==True which means intervals are (a,b],(b,c],(c,d] and si on
group_names=["<10","10-14","15-19","20-24",
            "25-29","30-34","35-39","40-44","44+"
            ]
game_data["Player Age Group"]=pd.cut(game_data["Age"],bins,labels=group_names)
game_data.head()
```




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
      <th>Age</th>
      <th>Gender</th>
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Price</th>
      <th>SN</th>
      <th>Player Age Group</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>38</td>
      <td>Male</td>
      <td>165</td>
      <td>Bone Crushing Silver Skewer</td>
      <td>3.37</td>
      <td>Aelalis34</td>
      <td>35-39</td>
    </tr>
    <tr>
      <th>1</th>
      <td>21</td>
      <td>Male</td>
      <td>119</td>
      <td>Stormbringer, Dark Blade of Ending Misery</td>
      <td>2.32</td>
      <td>Eolo46</td>
      <td>20-24</td>
    </tr>
    <tr>
      <th>2</th>
      <td>34</td>
      <td>Male</td>
      <td>174</td>
      <td>Primitive Blade</td>
      <td>2.46</td>
      <td>Assastnya25</td>
      <td>30-34</td>
    </tr>
    <tr>
      <th>3</th>
      <td>21</td>
      <td>Male</td>
      <td>92</td>
      <td>Final Critic</td>
      <td>1.36</td>
      <td>Pheusrical25</td>
      <td>20-24</td>
    </tr>
    <tr>
      <th>4</th>
      <td>23</td>
      <td>Male</td>
      <td>63</td>
      <td>Stormfury Mace</td>
      <td>1.27</td>
      <td>Aela59</td>
      <td>20-24</td>
    </tr>
  </tbody>
</table>
</div>




```python
game_data_grouped=game_data.groupby("Player Age Group")

purch_count_age=game_data_grouped[["Item ID"]].count()

purch_count_age=purch_count_age.rename(columns={"Item ID":"Purchase Count"})



```


```python
#Average Purchase Price


avg_purch_price=game_data_grouped[["Price"]].mean()


purch_count_age["Average Purchase Price"]=round(avg_purch_price,2)
purch_count_age_df=pd.DataFrame(purch_count_age)
```


```python
#Total Purchase Value
total_purch_val=game_data_grouped[["Price"]].sum()


purch_count_age_df["Total Purchase Value"]=total_purch_val

```


```python
organized_table=purch_count_age_df[["Purchase Count","Average Purchase Price","Total Purchase Value"]]

organized_table.head()
```




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
      <th>Purchase Count</th>
      <th>Average Purchase Price</th>
      <th>Total Purchase Value</th>
    </tr>
    <tr>
      <th>Player Age Group</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>&lt;10</th>
      <td>28</td>
      <td>2.98</td>
      <td>83.46</td>
    </tr>
    <tr>
      <th>10-14</th>
      <td>35</td>
      <td>2.77</td>
      <td>96.95</td>
    </tr>
    <tr>
      <th>15-19</th>
      <td>133</td>
      <td>2.91</td>
      <td>386.42</td>
    </tr>
    <tr>
      <th>20-24</th>
      <td>336</td>
      <td>2.91</td>
      <td>978.77</td>
    </tr>
    <tr>
      <th>25-29</th>
      <td>125</td>
      <td>2.96</td>
      <td>370.33</td>
    </tr>
  </tbody>
</table>
</div>




```python



#unique players in age group
# uniques=game_data.groupby(["SN","Player Age Group"])["Player Age Group"].agg(['count'])
# uniques


#tried the above and the following to get the unique player count from each age group, I get close but
#cannot get the actual wanted way to report
#once the unique number of players from each age group is down:
#normalized values for the above table are easy to evaluae: Total Purchase Value/Unique players from each age group
x=game_data_grouped["SN"].value_counts()
x

#Normalized Totals
#unique players in each age group
#percent player in each age group



```




    Player Age Group  SN            
    <10               Lisistaya47       3
                      Eosurdru76        2
                      Iladarla40        2
                      Ingatcil75        2
                      Lassjask63        2
                      Liri91            2
                      Lisirra55         2
                      Yarithsurgue62    2
                      Eullydru35        1
                      Frichjaskan98     1
                      Heosurnuru52      1
                      Ilophos58         1
                      Jiskosiala43      1
                      Reulae52          1
                      Saralp86          1
                      Silinu63          1
                      Sundastnya66      1
                      Tyaenasti87       1
                      Undjasksya56      1
    10-14             Qarwen67          4
                      Lirtosia72        3
                      Chanosiast43      2
                      Deural48          2
                      Eoralphos86       2
                      Ethrusuard41      2
                      Lirtossa78        2
                      Sondossa55        2
                      Streural92        2
                      Aeral97           1
                      Aillycal84        1
                                       ..
    35-39             Seosri62          2
                      Tyisriphos58      2
                      Airal46           1
                      Chanassa48        1
                      Cosadar58         1
                      Filon68           1
                      Filrion59         1
                      Hala31            1
                      Inguard95         1
                      Iskistasda86      1
                      Isri59            1
                      Lirtossan50       1
                      Phyali88          1
                      Ralasti48         1
                      Saena74           1
                      Tridaira71        1
                      Wailin72          1
                      Yaristi64         1
                      Yasrisu92         1
    40-44             Yasriphos60       3
                      Chanosiaya39      2
                      Indcil77          2
                      Sundast29         2
                      Yaralnura48       2
                      Chamadar27        1
                      Lisista27         1
                      Raesurdil91       1
                      Saelollop56       1
                      Yarmol79          1
    44+               Marassaya49       1
    Name: SN, Length: 573, dtype: int64




```python
##TOP SPENDERS:
# SN
# Purchase Count
# Average Purchase Price
# Total Purchase Value

```


```python


top_spenders=game_data.groupby('SN')['Price'].agg(['sum','count']).sort_values('sum',ascending=False)
top_spenders=top_spenders.rename(columns={"sum":"Total Purchase Value","count":"Purchase Count"})

top_spenders_df=pd.DataFrame(top_spenders)
avg_purch_val=round(top_spenders_df["Total Purchase Value"]/top_spenders_df["Purchase Count"],2)
top_spenders_df["Average Purchase Price"]=avg_purch_val


reordered_table=top_spenders_df[["Purchase Count","Average Purchase Price","Total Purchase Value"]]

reordered_table["Average Purchase Price"]=reordered_table['Average Purchase Price'].map("${:.2f}".format)
reordered_table["Total Purchase Value"]=reordered_table['Total Purchase Value'].map("${:.2f}".format)

reordered_table.head(5)


```




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
      <th>Purchase Count</th>
      <th>Average Purchase Price</th>
      <th>Total Purchase Value</th>
    </tr>
    <tr>
      <th>SN</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Undirrala66</th>
      <td>5</td>
      <td>$3.41</td>
      <td>$17.06</td>
    </tr>
    <tr>
      <th>Saedue76</th>
      <td>4</td>
      <td>$3.39</td>
      <td>$13.56</td>
    </tr>
    <tr>
      <th>Mindimnya67</th>
      <td>4</td>
      <td>$3.18</td>
      <td>$12.74</td>
    </tr>
    <tr>
      <th>Haellysu29</th>
      <td>3</td>
      <td>$4.24</td>
      <td>$12.73</td>
    </tr>
    <tr>
      <th>Eoda93</th>
      <td>3</td>
      <td>$3.86</td>
      <td>$11.58</td>
    </tr>
  </tbody>
</table>
</div>




```python
##MOST POPULAR ITEMS:
# Item ID
# Item Name
# Purchase Count
# Item Price
# Total Purchase Value
```


```python

popular_items=game_data.groupby(['Item ID','Item Name','Price'])['Price'].agg(['sum','count']).sort_values('count',ascending=False)

popular_items_df=pd.DataFrame(popular_items)

popular_items_df_renamed=popular_items_df.rename(columns={"Price":"Item Price","count":"Purchase Count","Price":"Item Price","sum":"Total Purchase Value"})
popular_items_df_renamed[["Purchase Count","Total Purchase Value"]]


#price column is an index column, couldn't reset it so that I could format...
#popular_items_df_renamed['Price']=popular_items_df_renamed['Price'].map('${:.2}'.format)

popular_items_df_renamed.head(5)

```




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
      <th></th>
      <th></th>
      <th>Total Purchase Value</th>
      <th>Purchase Count</th>
    </tr>
    <tr>
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Price</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>39</th>
      <th>Betrayal, Whisper of Grieving Widows</th>
      <th>2.35</th>
      <td>25.85</td>
      <td>11</td>
    </tr>
    <tr>
      <th>84</th>
      <th>Arcane Gem</th>
      <th>2.23</th>
      <td>24.53</td>
      <td>11</td>
    </tr>
    <tr>
      <th>31</th>
      <th>Trickster</th>
      <th>2.07</th>
      <td>18.63</td>
      <td>9</td>
    </tr>
    <tr>
      <th>175</th>
      <th>Woeful Adamantite Claymore</th>
      <th>1.24</th>
      <td>11.16</td>
      <td>9</td>
    </tr>
    <tr>
      <th>13</th>
      <th>Serenity</th>
      <th>1.49</th>
      <td>13.41</td>
      <td>9</td>
    </tr>
  </tbody>
</table>
</div>




```python
##MOST PROFITABLE ITEMS

# Item ID
# Item Name
# Purchase Count
# Item Price
# Total Purchase Value
```


```python

profitable_items=game_data.groupby(['Item ID','Item Name','Price'])['Price'].agg(['sum','count']).sort_values('sum',ascending=False)

profitable_items_df=pd.DataFrame(profitable_items)

profitable_items_df_renamed=profitable_items_df.rename(columns={"Price":"Item Price","count":"Purchase Count","Price":"Item Price","sum":"Total Purchase Value"})
profitable_items_df_renamed[["Purchase Count","Total Purchase Value"]]

# profitable_items_df_renamed['Price']=profitable_items_df_renamed.reset_index
profitable_items_df_renamed.head(5)
```




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
      <th></th>
      <th></th>
      <th>Total Purchase Value</th>
      <th>Purchase Count</th>
    </tr>
    <tr>
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Price</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>34</th>
      <th>Retribution Axe</th>
      <th>4.14</th>
      <td>37.26</td>
      <td>9</td>
    </tr>
    <tr>
      <th>115</th>
      <th>Spectral Diamond Doomblade</th>
      <th>4.25</th>
      <td>29.75</td>
      <td>7</td>
    </tr>
    <tr>
      <th>32</th>
      <th>Orenmir</th>
      <th>4.95</th>
      <td>29.70</td>
      <td>6</td>
    </tr>
    <tr>
      <th>103</th>
      <th>Singed Scalpel</th>
      <th>4.87</th>
      <td>29.22</td>
      <td>6</td>
    </tr>
    <tr>
      <th>107</th>
      <th>Splitter, Foe Of Subtlety</th>
      <th>3.61</th>
      <td>28.88</td>
      <td>8</td>
    </tr>
  </tbody>
</table>
</div>


