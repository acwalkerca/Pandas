

```python
import pandas as pd
import numpy as np
```


```python
file = "purchase_data.json"
file_df = pd.read_json(file)
file_df.head()

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
#Player Count - COMPLETE

total_players = file_df["SN"].value_counts()

col_name = ["Total Players"]

total_players_df = pd.DataFrame([[total_players.count()]], columns=col_name)
total_players_df
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
#Purchasing Analysis (Total) - COMPLETE

#number of unique items
unique_items = file_df["Item Name"].value_counts()

#average price
average_price = file_df["Price"].mean()

#total purchases
total_purchases = len(file_df)

#total revenue
total_revenue = file_df["Price"].sum()

col_names = ["Number of Unique Items", "Average Price", "Number of Purchases", "Total Revenue"]

purchasing_analysis_total_df = pd.DataFrame([[unique_items.count(), average_price, total_purchases, total_revenue]], columns=col_names)

purchasing_analysis_total_df["Average Price"] = purchasing_analysis_total_df["Average Price"].map("${:.2f}".format)
purchasing_analysis_total_df["Total Revenue"] = purchasing_analysis_total_df["Total Revenue"].map("${:,.2f}".format)
purchasing_analysis_total_df
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
      <td>179</td>
      <td>$2.93</td>
      <td>780</td>
      <td>$2,286.33</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Gender Demographics - COMPLETE

#count players
player_count = file_df["Gender"].value_counts()

#percentage players
percentage_players = (player_count/total_purchases)*100


player_count_table = pd.DataFrame({"Percentage of Players": percentage_players.round(2), "Total Count": player_count})
player_count_table
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
      <th>Percentage of Players</th>
      <th>Total Count</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Male</th>
      <td>81.15</td>
      <td>633</td>
    </tr>
    <tr>
      <th>Female</th>
      <td>17.44</td>
      <td>136</td>
    </tr>
    <tr>
      <th>Other / Non-Disclosed</th>
      <td>1.41</td>
      <td>11</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Purchasing Analysis (Gender) - COMPLETE

gender_data = file_df.groupby(["Gender"])

gender_purchases = gender_data["Item ID"].count()
gender_avg_price = gender_data["Price"].mean()
gender_revenue = gender_data["Price"].sum()

purchasing_analysis_table = pd.DataFrame({"Purchase Count": gender_purchases, "Average Purchase Price" : gender_avg_price, "Total Purchase Value" : gender_revenue})

purchasing_analysis_table["Average Purchase Price"]=purchasing_analysis_table["Average Purchase Price"].map("${:.2f}".format)
purchasing_analysis_table["Total Purchase Value"]=purchasing_analysis_table["Total Purchase Value"].map("${:.2f}".format)
purchasing_analysis_table
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
      <th>Gender</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Female</th>
      <td>136</td>
      <td>$2.82</td>
      <td>$382.91</td>
    </tr>
    <tr>
      <th>Male</th>
      <td>633</td>
      <td>$2.95</td>
      <td>$1867.68</td>
    </tr>
    <tr>
      <th>Other / Non-Disclosed</th>
      <td>11</td>
      <td>$3.25</td>
      <td>$35.74</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Age Demographics - COMPLETE

bins = [0,10,15,20,25,30,35,40,50]
bin_labels = ["<10", "10-14", "15-19", "20-24", "25-39", "30-34", "35-39", "40+"]

file_df["Age Group"] = pd.cut(file_df["Age"], bins, labels = bin_labels)

age_group = file_df.groupby("Age Group")
age_percentage = (age_group["Age"].count()/total_players.count())*100

age_demographics_table = pd.DataFrame({"Percentage of Players" : age_percentage.round(2), "Total Count" : age_group["Age"].count()})
age_demographics_table
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
      <th>Percentage of Players</th>
      <th>Total Count</th>
    </tr>
    <tr>
      <th>Age Group</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>&lt;10</th>
      <td>5.58</td>
      <td>32</td>
    </tr>
    <tr>
      <th>10-14</th>
      <td>13.61</td>
      <td>78</td>
    </tr>
    <tr>
      <th>15-19</th>
      <td>32.11</td>
      <td>184</td>
    </tr>
    <tr>
      <th>20-24</th>
      <td>53.23</td>
      <td>305</td>
    </tr>
    <tr>
      <th>25-39</th>
      <td>13.26</td>
      <td>76</td>
    </tr>
    <tr>
      <th>30-34</th>
      <td>10.12</td>
      <td>58</td>
    </tr>
    <tr>
      <th>35-39</th>
      <td>7.68</td>
      <td>44</td>
    </tr>
    <tr>
      <th>40+</th>
      <td>0.52</td>
      <td>3</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Top Spenders - COMPLETE

spender_total = file_df.groupby(['SN'])
spender_sum = pd.DataFrame(spender_total.sum()["Price"])

top_spenders = spender_sum.sort_values("Price", ascending=False)

spender_count = file_df.groupby(['SN']).count()
spender_items = pd.DataFrame(spender_count)

merge_table = pd.merge(top_spenders, spender_count, on="SN")

reduced_merge = merge_table.loc[:, ["Price_x", "Age"]]

spender_average = pd.DataFrame({"Average Purchase Price" : merge_table["Price_x"]/merge_table["Age"]}).round(2)

total_merge = pd.merge(reduced_merge, spender_average, on="SN")

top_spender_df = total_merge.rename(columns={"Price_x" : "Total Purchase Value", "Age" : "Purchase Count"})

top_spender_df["Average Purchase Price"]=top_spender_df["Average Purchase Price"].map("${:.2f}".format)
top_spender_df["Total Purchase Value"]=top_spender_df["Total Purchase Value"].map("${:.2f}".format)

organized_top_spender = top_spender_df[["Purchase Count", "Average Purchase Price", "Total Purchase Value"]]
organized_top_spender.head()
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
#Most Popular Items - COMPLETE

item_count = file_df.groupby(["Item ID", "Item Name"])
item_total = pd.DataFrame(item_count.count())

top_items = item_total.sort_values("Age", ascending=False)

reduced_table = top_items.loc[: , ["Age"]]

reduced_table = reduced_table.rename(columns={"Age" : "Purchase Count"})

item_totals = file_df.groupby(["Item ID", "Item Name"])
item_count = pd.DataFrame(item_totals.mean())
reduced_item_count = item_count.loc[ : , ["Price"]]

merge_count = pd.merge(reduced_table, reduced_item_count, on=['Item ID','Item Name'])

total_price = pd.DataFrame({"Total Purchase Value" : merge_count["Purchase Count"]*merge_count["Price"]})

most_popular_items = pd.merge(merge_count, total_price, on=['Item ID','Item Name'])

most_popular_items_final = most_popular_items.copy()

most_popular_items_final["Price"]=most_popular_items_final["Price"].map("${:.2f}".format)
most_popular_items_final["Total Purchase Value"]=most_popular_items_final["Total Purchase Value"].map("${:.2f}".format)
most_popular_items_final.head()
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
      <th>Purchase Count</th>
      <th>Price</th>
      <th>Total Purchase Value</th>
    </tr>
    <tr>
      <th>Item ID</th>
      <th>Item Name</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>39</th>
      <th>Betrayal, Whisper of Grieving Widows</th>
      <td>11</td>
      <td>$2.35</td>
      <td>$25.85</td>
    </tr>
    <tr>
      <th>84</th>
      <th>Arcane Gem</th>
      <td>11</td>
      <td>$2.23</td>
      <td>$24.53</td>
    </tr>
    <tr>
      <th>31</th>
      <th>Trickster</th>
      <td>9</td>
      <td>$2.07</td>
      <td>$18.63</td>
    </tr>
    <tr>
      <th>175</th>
      <th>Woeful Adamantite Claymore</th>
      <td>9</td>
      <td>$1.24</td>
      <td>$11.16</td>
    </tr>
    <tr>
      <th>13</th>
      <th>Serenity</th>
      <td>9</td>
      <td>$1.49</td>
      <td>$13.41</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Most Profitable Items - COMPLETE

most_profitable_items = most_popular_items.sort_values("Total Purchase Value", ascending=False)

most_profitable_items["Price"]=most_profitable_items["Price"].map("${:.2f}".format)
most_profitable_items["Total Purchase Value"]=most_profitable_items["Total Purchase Value"].map("${:.2f}".format)
most_profitable_items.head()
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
      <th>Purchase Count</th>
      <th>Price</th>
      <th>Total Purchase Value</th>
    </tr>
    <tr>
      <th>Item ID</th>
      <th>Item Name</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>34</th>
      <th>Retribution Axe</th>
      <td>9</td>
      <td>$4.14</td>
      <td>$37.26</td>
    </tr>
    <tr>
      <th>115</th>
      <th>Spectral Diamond Doomblade</th>
      <td>7</td>
      <td>$4.25</td>
      <td>$29.75</td>
    </tr>
    <tr>
      <th>32</th>
      <th>Orenmir</th>
      <td>6</td>
      <td>$4.95</td>
      <td>$29.70</td>
    </tr>
    <tr>
      <th>103</th>
      <th>Singed Scalpel</th>
      <td>6</td>
      <td>$4.87</td>
      <td>$29.22</td>
    </tr>
    <tr>
      <th>107</th>
      <th>Splitter, Foe Of Subtlety</th>
      <td>8</td>
      <td>$3.61</td>
      <td>$28.88</td>
    </tr>
  </tbody>
</table>
</div>


