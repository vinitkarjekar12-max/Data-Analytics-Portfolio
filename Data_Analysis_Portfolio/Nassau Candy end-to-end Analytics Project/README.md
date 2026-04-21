```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
```


```python
df=pd.read_csv(r"C:\Users\-----\Downloads\Nassau_Candy_Distributor.csv")
df.head()
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
      <th>Row ID</th>
      <th>Order ID</th>
      <th>Order Date</th>
      <th>Ship Date</th>
      <th>Ship Mode</th>
      <th>Customer ID</th>
      <th>Country/Region</th>
      <th>City</th>
      <th>State/Province</th>
      <th>Postal Code</th>
      <th>Division</th>
      <th>Region</th>
      <th>Product ID</th>
      <th>Product Name</th>
      <th>Sales</th>
      <th>Units</th>
      <th>Gross Profit</th>
      <th>Cost</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>US-2021-103800-CHO-MIL-31000</td>
      <td>03-01-2024</td>
      <td>30-06-2026</td>
      <td>Standard Class</td>
      <td>103800</td>
      <td>United States</td>
      <td>Houston</td>
      <td>Texas</td>
      <td>77095</td>
      <td>Chocolate</td>
      <td>Interior</td>
      <td>CHO-MIL-31000</td>
      <td>Wonka Bar - Milk Chocolate</td>
      <td>6.50</td>
      <td>2</td>
      <td>4.22</td>
      <td>2.28</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>US-2021-112326-CHO-TRI-54000</td>
      <td>04-01-2024</td>
      <td>01-07-2026</td>
      <td>Standard Class</td>
      <td>112326</td>
      <td>United States</td>
      <td>Naperville</td>
      <td>Illinois</td>
      <td>60540</td>
      <td>Chocolate</td>
      <td>Interior</td>
      <td>CHO-TRI-54000</td>
      <td>Wonka Bar - Triple Dazzle Caramel</td>
      <td>7.50</td>
      <td>2</td>
      <td>4.90</td>
      <td>2.60</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>US-2021-112326-CHO-NUT-13000</td>
      <td>04-01-2024</td>
      <td>01-07-2026</td>
      <td>Standard Class</td>
      <td>112326</td>
      <td>United States</td>
      <td>Naperville</td>
      <td>Illinois</td>
      <td>60540</td>
      <td>Chocolate</td>
      <td>Interior</td>
      <td>CHO-NUT-13000</td>
      <td>Wonka Bar - Nutty Crunch Surprise</td>
      <td>10.47</td>
      <td>3</td>
      <td>7.47</td>
      <td>3.00</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>US-2021-112326-CHO-SCR-58000</td>
      <td>04-01-2024</td>
      <td>01-07-2026</td>
      <td>Standard Class</td>
      <td>112326</td>
      <td>United States</td>
      <td>Naperville</td>
      <td>Illinois</td>
      <td>60540</td>
      <td>Chocolate</td>
      <td>Interior</td>
      <td>CHO-SCR-58000</td>
      <td>Wonka Bar -Scrumdiddlyumptious</td>
      <td>10.80</td>
      <td>3</td>
      <td>7.50</td>
      <td>3.30</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>US-2021-141817-CHO-TRI-54000</td>
      <td>05-01-2024</td>
      <td>05-07-2026</td>
      <td>Standard Class</td>
      <td>141817</td>
      <td>United States</td>
      <td>Philadelphia</td>
      <td>Pennsylvania</td>
      <td>19143</td>
      <td>Chocolate</td>
      <td>Atlantic</td>
      <td>CHO-TRI-54000</td>
      <td>Wonka Bar - Triple Dazzle Caramel</td>
      <td>11.25</td>
      <td>3</td>
      <td>7.35</td>
      <td>3.90</td>
    </tr>
  </tbody>
</table>
</div>




```python
df1=pd.read_csv(r"C:\Users\-----\Downloads\Products and Factories Correlation.csv")
df1.head()
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
      <th>Division</th>
      <th>Product Name</th>
      <th>Factory</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Chocolate</td>
      <td>Wonka Bar - Nutty Crunch Surprise</td>
      <td>Lot's O' Nuts</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Chocolate</td>
      <td>Wonka Bar - Fudge Mallows</td>
      <td>Lot's O' Nuts</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Chocolate</td>
      <td>Wonka Bar -Scrumdiddlyumptious</td>
      <td>Lot's O' Nuts</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Chocolate</td>
      <td>Wonka Bar - Milk Chocolate</td>
      <td>Wicked Choccy's</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Chocolate</td>
      <td>Wonka Bar - Triple Dazzle Caramel</td>
      <td>Wicked Choccy's</td>
    </tr>
  </tbody>
</table>
</div>



Data Cleaning & Validation
• Validate cost and sales values
• Remove zero-sales or invalid profit records
• Handle missing unit values
• Standardize product and division labels


```python
df.isnull().sum()
```




    Row ID            0
    Order ID          0
    Order Date        0
    Ship Date         0
    Ship Mode         0
    Customer ID       0
    Country/Region    0
    City              0
    State/Province    0
    Postal Code       0
    Division          0
    Region            0
    Product ID        0
    Product Name      0
    Sales             0
    Units             0
    Gross Profit      0
    Cost              0
    Gross Margin      0
    dtype: int64




```python
df.shape
```




    (10194, 18)




```python
df.describe()
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
      <th>Row ID</th>
      <th>Customer ID</th>
      <th>Sales</th>
      <th>Units</th>
      <th>Gross Profit</th>
      <th>Cost</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>10194.000000</td>
      <td>10194.000000</td>
      <td>10194.000000</td>
      <td>10194.000000</td>
      <td>10194.000000</td>
      <td>10194.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>5097.500000</td>
      <td>134468.961154</td>
      <td>13.908537</td>
      <td>3.791838</td>
      <td>9.166451</td>
      <td>4.742087</td>
    </tr>
    <tr>
      <th>std</th>
      <td>2942.898656</td>
      <td>20231.483007</td>
      <td>11.341020</td>
      <td>2.228317</td>
      <td>6.643740</td>
      <td>5.061647</td>
    </tr>
    <tr>
      <th>min</th>
      <td>1.000000</td>
      <td>100006.000000</td>
      <td>1.250000</td>
      <td>1.000000</td>
      <td>0.250000</td>
      <td>0.600000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>2549.250000</td>
      <td>117212.000000</td>
      <td>7.200000</td>
      <td>2.000000</td>
      <td>4.900000</td>
      <td>2.400000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>5097.500000</td>
      <td>133550.000000</td>
      <td>10.800000</td>
      <td>3.000000</td>
      <td>7.470000</td>
      <td>3.600000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>7645.750000</td>
      <td>152051.000000</td>
      <td>18.000000</td>
      <td>5.000000</td>
      <td>12.250000</td>
      <td>5.700000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>10194.000000</td>
      <td>192314.000000</td>
      <td>260.000000</td>
      <td>14.000000</td>
      <td>130.000000</td>
      <td>130.000000</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 10194 entries, 0 to 10193
    Data columns (total 21 columns):
     #   Column          Non-Null Count  Dtype  
    ---  ------          --------------  -----  
     0   Row ID          10194 non-null  int64  
     1   Order ID        10194 non-null  object 
     2   Order Date      10194 non-null  object 
     3   Ship Date       10194 non-null  object 
     4   Ship Mode       10194 non-null  object 
     5   Customer ID     10194 non-null  int64  
     6   Country/Region  10194 non-null  object 
     7   City            10194 non-null  object 
     8   State/Province  10194 non-null  object 
     9   Postal Code     10194 non-null  object 
     10  Division        10194 non-null  object 
     11  Region          10194 non-null  object 
     12  Product ID      10194 non-null  object 
     13  Product Name    10194 non-null  object 
     14  Sales           10194 non-null  float64
     15  Units           10194 non-null  int64  
     16  Gross Profit    10194 non-null  float64
     17  Cost            10194 non-null  float64
     18  Gross_Margin    10194 non-null  float64
     19  Profit_%        10194 non-null  float64
     20  Profit Status   10194 non-null  object 
    dtypes: float64(5), int64(3), object(13)
    memory usage: 1.6+ MB
    


```python
df.columns
```




    Index(['Row ID', 'Order ID', 'Order Date', 'Ship Date', 'Ship Mode',
           'Customer ID', 'Country/Region', 'City', 'State/Province',
           'Postal Code', 'Division', 'Region', 'Product ID', 'Product Name',
           'Sales', 'Units', 'Gross Profit', 'Cost', 'Profit_%', 'Profit Status',
           'Gross_Margin'],
          dtype='object')




```python

```


```python
df[df['Units']==0]
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
      <th>Row ID</th>
      <th>Order ID</th>
      <th>Order Date</th>
      <th>Ship Date</th>
      <th>Ship Mode</th>
      <th>Customer ID</th>
      <th>Country/Region</th>
      <th>City</th>
      <th>State/Province</th>
      <th>Postal Code</th>
      <th>Division</th>
      <th>Region</th>
      <th>Product ID</th>
      <th>Product Name</th>
      <th>Sales</th>
      <th>Units</th>
      <th>Gross Profit</th>
      <th>Cost</th>
      <th>Gross_Margin</th>
      <th>Profit_%</th>
    </tr>
  </thead>
  <tbody>
  </tbody>
</table>
</div>




```python
df[['Sales','Cost']].isnull().sum()
```




    Sales    0
    Cost     0
    dtype: int64




```python
df['Product Name'].unique()
```




    array(['Wonka Bar - Milk Chocolate', 'Wonka Bar - Triple Dazzle Caramel',
           'Wonka Bar - Nutty Crunch Surprise',
           'Wonka Bar - Scrumdiddlyumptious', 'Wonka Bar - Fudge Mallows',
           'Wonka Gum', 'Kazookles', 'Lickable Wallpaper',
           'Fizzy Lifting Drinks', 'Laffy Taffy', 'Sweet Arts', 'Nerds',
           'Hair Toffee', 'Everlasting Gobstopper', 'Fun Dip'], dtype=object)




```python
df['Division'].unique()
```




    array(['Chocolate', 'Other', 'Sugar'], dtype=object)



## Standardize product and division labels


```python
## Standardize product and division labels
df['Product Name']=df['Product Name'].replace({'SweeTARTS':'Sweet arts'})
df['Product Name']=df['Product Name'].str.strip().str.title()
df['Product Name']=df['Product Name'].replace({'Wonka Bar -Scrumdiddlyumptious':'Wonka Bar - Scrumdiddlyumptious'})
df['City']=df['City'].str.strip().str.title()
df['State/Province']=df['State/Province'].str.strip().str.title()
```

## Standardized the values in ‘Product Name’, ‘Division’, ‘City’, and ‘State/Province’ to ensure consistency and accuracy across the dataset.


```python
df['State/Province'].unique()
```




    array(['Texas', 'Illinois', 'Pennsylvania', 'Kentucky', 'Georgia',
           'California', 'Virginia', 'Delaware', 'South Carolina', 'Ohio',
           'Louisiana', 'Oregon', 'Arizona', 'Arkansas', 'Michigan',
           'Tennessee', 'Florida', 'Ontario', 'Indiana', 'Nevada',
           'South Dakota', 'New York', 'Wisconsin', 'Washington',
           'New Jersey', 'Missouri', 'North Carolina', 'Colorado', 'Alberta',
           'Utah', 'Minnesota', 'Mississippi', 'Iowa', 'New Mexico',
           'Massachusetts', 'Alabama', 'Idaho', 'Montana', 'Maryland',
           'Connecticut', 'New Hampshire', 'British Columbia', 'Quebec',
           'Nova Scotia', 'Oklahoma', 'Nebraska', 'Maine', 'Kansas',
           'Rhode Island', 'Newfoundland And Labrador', 'New Brunswick',
           'Prince Edward Island', 'District Of Columbia', 'Vermont',
           'Manitoba', 'Saskatchewan', 'Wyoming', 'North Dakota',
           'West Virginia'], dtype=object)




```python
df['Order ID'].value_counts()
df['Order ID'].value_counts()[df['Order ID'].value_counts()==1].shape
```




    (7176,)



## Problem Statement
Currently, the organization lacks visibility into:

#1. Which product lines deliver the highest gross margin
#2. Whether high-sales products are actually profitable
#3. How profitability varies across product divisions
#4. Which products represent margin risk


```python
#1 Which product lines deliver the highest gross margin
df=df.groupby('Product Name')[['Units','Cost','Sales','Gross Profit']].sum()
Total_Units=df['Units'].sum()
df['Gross Margin']=((df['Gross Profit']/df['Sales'])*100).round(2)
df['Total Units']=((df['Units']/Total_Units)*100).round(2)
df.sort_values(by='Gross Margin', ascending=False).head(1)
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
      <th>Units</th>
      <th>Cost</th>
      <th>Sales</th>
      <th>Gross Profit</th>
      <th>Gross Margin</th>
      <th>Total Units</th>
    </tr>
    <tr>
      <th>Product Name</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Everlasting Gobstopper</th>
      <td>13</td>
      <td>26.0</td>
      <td>130.0</td>
      <td>104.0</td>
      <td>80.0</td>
      <td>0.03</td>
    </tr>
  </tbody>
</table>
</div>



### Observations: Which product lines deliver the highest gross margin
1. Everlasting Gobstopper (Product Line) has the highest gross margin of 80%, but it has sold only 0.03% units of the overall inventory.
2. As per the highest selling units, Wonka Bar - Nutty Crunch Surprise is the product that delivers a high gross margin. This product contributes 17.48% of the total units sold with a 71.35% gross margin.


```python
#2. Whether high-sales products are actually profitable
## Total of all rows
total_units=df['Units'].sum()
total_cost=df['Cost'].sum()
total_sales=df['Sales'].sum()
total_gross_profit=df['Gross Profit'].sum()

## Top 5 calculations
Overall_Gross_Margin=((df['Gross Profit'].sum()/df['Sales'].sum())*100).round(2)
top_5=df.groupby('Product Name')[['Units','Sales','Gross Profit','Gross Margin']].sum().sort_values(by='Sales', ascending=False).head(5)
df['Total Units %']=(top_5['Units']/total_units)*100
df['Total Sales %']=(top_5['Sales']/total_sales)*100
df['Gross Profit %']=(top_5['Gross Profit']/total_gross_profit)*100
df['Gross Margin']=((df['Gross Profit']/df['Sales'])*100).round(2)
top5_Gross_Margin=((top_5['Gross Profit'].sum()/top_5['Sales'].sum())*100).round(5)

## Top 5 Highest Selling SKUS Calculations
top5_units=top_5['Units'].sum()
top5_sales=top_5['Sales'].sum().round(2)
top5_profit=top_5['Gross Profit'].sum().round(2)
Top_5_Units_Contribution=((top5_units/total_units)*100).round(2)
Top_5_Sales_Contribution=((top5_sales/total_sales)*100).round(2)
Top_5_Profit=((top5_profit/total_gross_profit)*100).round(2)

## Print Statement
print("Top 5 Products Units Sold : ",top5_units)
print("Top 5 Products Units Contribution : ",Top_5_Units_Contribution,"%")
print("Top 5 Products Sales : ",top5_sales)
print("Top 5 Products Sales Contribution : ",Top_5_Sales_Contribution,"%")
print("Top 5 Products Gross Profit : ",top5_profit)
print("Top 5 Products Gross Profit Contribution : ",Top_5_Profit,"%")
print("Gross Margin Average of Top 5 Selling Products : " ,top5_Gross_Margin,"%")
```

#2 Observations: Whether high-sales products are actually profitable
1. Yes, based on the observations, the top 5 highest-selling SKUs contribute 95.06% of the total gross profit and 92.88% of the overall sales.
2. The average gross margin for the top 5 highest-selling SKUs is 67.45%, which is above the 60% margin bracket. This indicates that 96.43% of 
the units and 92.88% of the sales are generated with a 67.45% gross margin, which is a strong indicator of good profitability for the company.

#3. How profitability varies across product divisions


```python
def profit_status (x):
    if x > 60:
        return 'High Profit'
    elif x > 40:
        return 'Mid Profit'
    elif x > 20:
        return 'Low Profit'
    else:
        return 'Very low profit'
```


```python
profitability=df.groupby('Division')[['Sales','Units','Cost','Gross Profit']].sum()
profitability['Profit_%']=((profitability['Gross Profit']/profitability['Sales'])*100).round(2)
profitability['Status']=profitability['Profit_%'].apply(profit_status)
profitability=profitability.sort_values(by='Units', ascending=False)
profitability
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
      <th>Sales</th>
      <th>Units</th>
      <th>Cost</th>
      <th>Gross Profit</th>
      <th>Profit_%</th>
      <th>Status</th>
    </tr>
    <tr>
      <th>Division</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Chocolate</th>
      <td>131692.90</td>
      <td>37275</td>
      <td>42868.28</td>
      <td>88824.62</td>
      <td>67.45</td>
      <td>High Profit</td>
    </tr>
    <tr>
      <th>Other</th>
      <td>9663.25</td>
      <td>1242</td>
      <td>5329.80</td>
      <td>4333.45</td>
      <td>44.84</td>
      <td>Mid Profit</td>
    </tr>
    <tr>
      <th>Sugar</th>
      <td>427.48</td>
      <td>137</td>
      <td>142.75</td>
      <td>284.73</td>
      <td>66.61</td>
      <td>High Profit</td>
    </tr>
  </tbody>
</table>
</div>



### Observations: How profitability varies across product divisions
1. The Chocolate category contributes 95.06% of the total gross profit, which clearly indicates that the Chocolate 
division dominates the company's overall profitability.
2. The Sugar and Other categories contribute 0.30% and 4.64% of the total gross profit, respectively, indicating that 
their impact on overall profitability is relatively small compared to the Chocolate division.


```python
#4. Which products represent margin risk
df=df.groupby('Product Name')[['Units','Cost','Sales','Gross Profit']].sum()
Total_Units=df['Units'].sum()
df['Gross Margin']=((df['Gross Profit']/df['Sales'])*100).round(2)
df['Total Units']=((df['Units']/Total_Units)*100).round(2)
df.sort_values(by='Gross Margin', ascending=True).head(5)
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
      <th>Units</th>
      <th>Cost</th>
      <th>Sales</th>
      <th>Gross Profit</th>
      <th>Gross Margin</th>
      <th>Total Units</th>
    </tr>
    <tr>
      <th>Product Name</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Kazookles</th>
      <td>371</td>
      <td>1113.0</td>
      <td>1205.75</td>
      <td>92.75</td>
      <td>7.69</td>
      <td>0.96</td>
    </tr>
    <tr>
      <th>Fun Dip</th>
      <td>8</td>
      <td>7.2</td>
      <td>12.00</td>
      <td>4.80</td>
      <td>40.00</td>
      <td>0.02</td>
    </tr>
    <tr>
      <th>Nerds</th>
      <td>10</td>
      <td>8.0</td>
      <td>15.00</td>
      <td>7.00</td>
      <td>46.67</td>
      <td>0.03</td>
    </tr>
    <tr>
      <th>Sweet arts</th>
      <td>41</td>
      <td>32.8</td>
      <td>61.50</td>
      <td>28.70</td>
      <td>46.67</td>
      <td>0.11</td>
    </tr>
    <tr>
      <th>Lickable Wallpaper</th>
      <td>393</td>
      <td>3930.0</td>
      <td>7860.00</td>
      <td>3930.00</td>
      <td>50.00</td>
      <td>1.02</td>
    </tr>
  </tbody>
</table>
</div>



## Observations
1. Kazookles is the only product with margin risk with margin of 7.69% with sold over 370 units.
2. Fun Dip, SweeTARTS & Nerds are 3 products with profit margin below 50% except Kazookles 


```python

```

Profitability Metric Calculation
For each product:
## Gross Margin (%)
## Profit per unit
## Total profit contribution


```python
df['Per Unit Sale Price']=df['Sales']/df['Units']
df['Per Unit Cost']=df['Cost']/df['Units']
df['Profit Per Unit']=df['Per Unit Sale Price']-df['Per Unit Cost']
df['Gross Margin % Per Units']=(((df['Per Unit Sale Price']-df['Per Unit Cost'])/df['Per Unit Sale Price'])*100).round(2)
df
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
      <th>Units</th>
      <th>Cost</th>
      <th>Sales</th>
      <th>Gross Profit</th>
      <th>Gross Margin</th>
      <th>Total Units</th>
      <th>Per Unit Sale Price</th>
      <th>Per Unit Cost</th>
      <th>Profit Per Unit</th>
      <th>Gross Margin % Per Units</th>
    </tr>
    <tr>
      <th>Product Name</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Everlasting Gobstopper</th>
      <td>13</td>
      <td>26.00</td>
      <td>130.00</td>
      <td>104.00</td>
      <td>80.00</td>
      <td>0.03</td>
      <td>10.00</td>
      <td>2.00</td>
      <td>8.00</td>
      <td>80.00</td>
    </tr>
    <tr>
      <th>Fizzy Lifting Drinks</th>
      <td>21</td>
      <td>31.50</td>
      <td>78.75</td>
      <td>47.25</td>
      <td>60.00</td>
      <td>0.05</td>
      <td>3.75</td>
      <td>1.50</td>
      <td>2.25</td>
      <td>60.00</td>
    </tr>
    <tr>
      <th>Fun Dip</th>
      <td>8</td>
      <td>7.20</td>
      <td>12.00</td>
      <td>4.80</td>
      <td>40.00</td>
      <td>0.02</td>
      <td>1.50</td>
      <td>0.90</td>
      <td>0.60</td>
      <td>40.00</td>
    </tr>
    <tr>
      <th>Hair Toffee</th>
      <td>17</td>
      <td>17.00</td>
      <td>76.50</td>
      <td>59.50</td>
      <td>77.78</td>
      <td>0.04</td>
      <td>4.50</td>
      <td>1.00</td>
      <td>3.50</td>
      <td>77.78</td>
    </tr>
    <tr>
      <th>Kazookles</th>
      <td>371</td>
      <td>1113.00</td>
      <td>1205.75</td>
      <td>92.75</td>
      <td>7.69</td>
      <td>0.96</td>
      <td>3.25</td>
      <td>3.00</td>
      <td>0.25</td>
      <td>7.69</td>
    </tr>
    <tr>
      <th>Laffy Taffy</th>
      <td>27</td>
      <td>20.25</td>
      <td>53.73</td>
      <td>33.48</td>
      <td>62.31</td>
      <td>0.07</td>
      <td>1.99</td>
      <td>0.75</td>
      <td>1.24</td>
      <td>62.31</td>
    </tr>
    <tr>
      <th>Lickable Wallpaper</th>
      <td>393</td>
      <td>3930.00</td>
      <td>7860.00</td>
      <td>3930.00</td>
      <td>50.00</td>
      <td>1.02</td>
      <td>20.00</td>
      <td>10.00</td>
      <td>10.00</td>
      <td>50.00</td>
    </tr>
    <tr>
      <th>Nerds</th>
      <td>10</td>
      <td>8.00</td>
      <td>15.00</td>
      <td>7.00</td>
      <td>46.67</td>
      <td>0.03</td>
      <td>1.50</td>
      <td>0.80</td>
      <td>0.70</td>
      <td>46.67</td>
    </tr>
    <tr>
      <th>Sweet arts</th>
      <td>41</td>
      <td>32.80</td>
      <td>61.50</td>
      <td>28.70</td>
      <td>46.67</td>
      <td>0.11</td>
      <td>1.50</td>
      <td>0.80</td>
      <td>0.70</td>
      <td>46.67</td>
    </tr>
    <tr>
      <th>Wonka Bar - Fudge Mallows</th>
      <td>6914</td>
      <td>8296.80</td>
      <td>24890.40</td>
      <td>16593.60</td>
      <td>66.67</td>
      <td>17.89</td>
      <td>3.60</td>
      <td>1.20</td>
      <td>2.40</td>
      <td>66.67</td>
    </tr>
    <tr>
      <th>Wonka Bar - Milk Chocolate</th>
      <td>8267</td>
      <td>9424.38</td>
      <td>26867.75</td>
      <td>17443.37</td>
      <td>64.92</td>
      <td>21.39</td>
      <td>3.25</td>
      <td>1.14</td>
      <td>2.11</td>
      <td>64.92</td>
    </tr>
    <tr>
      <th>Wonka Bar - Nutty Crunch Surprise</th>
      <td>6755</td>
      <td>6755.00</td>
      <td>23574.95</td>
      <td>16819.95</td>
      <td>71.35</td>
      <td>17.48</td>
      <td>3.49</td>
      <td>1.00</td>
      <td>2.49</td>
      <td>71.35</td>
    </tr>
    <tr>
      <th>Wonka Bar - Triple Dazzle Caramel</th>
      <td>7596</td>
      <td>9874.80</td>
      <td>28485.00</td>
      <td>18610.20</td>
      <td>65.33</td>
      <td>19.65</td>
      <td>3.75</td>
      <td>1.30</td>
      <td>2.45</td>
      <td>65.33</td>
    </tr>
    <tr>
      <th>Wonka Bar -Scrumdiddlyumptious</th>
      <td>7743</td>
      <td>8517.30</td>
      <td>27874.80</td>
      <td>19357.50</td>
      <td>69.44</td>
      <td>20.03</td>
      <td>3.60</td>
      <td>1.10</td>
      <td>2.50</td>
      <td>69.44</td>
    </tr>
    <tr>
      <th>Wonka Gum</th>
      <td>478</td>
      <td>286.80</td>
      <td>597.50</td>
      <td>310.70</td>
      <td>52.00</td>
      <td>1.24</td>
      <td>1.25</td>
      <td>0.60</td>
      <td>0.65</td>
      <td>52.00</td>
    </tr>
  </tbody>
</table>
</div>



## Total profit contribution


```python
#1. Gross Margin (%)
#1. Profit Per Unit
#3. Total Profit Contribution

df=df.groupby('Product Name')[['Units','Cost','Sales','Gross Profit']].sum()
Total_Units=df['Units'].sum()
Total_Profit=df['Gross Profit'].sum()
df['Gross Margin']=((df['Gross Profit']/df['Sales'])*100).round(2)
df['Units Contribution %']=((df['Units']/Total_Units)*100).round(2)
df['Profit Contribution %']=((df['Gross Profit']/Total_Profit)*100).round(2)
df['Profit Per Unit']=df['Gross Profit']/df['Units']
df.sort_values(by='Gross Margin', ascending=False)
top_profit=df.sort_values(by='Profit Contribution %',ascending=False)
top_profit
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
      <th>Units</th>
      <th>Cost</th>
      <th>Sales</th>
      <th>Gross Profit</th>
      <th>Gross Margin</th>
      <th>Units Contribution %</th>
      <th>Profit Contribution %</th>
      <th>Profit Per Unit</th>
    </tr>
    <tr>
      <th>Product Name</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Wonka Bar -Scrumdiddlyumptious</th>
      <td>7743</td>
      <td>8517.30</td>
      <td>27874.80</td>
      <td>19357.50</td>
      <td>69.44</td>
      <td>20.03</td>
      <td>20.72</td>
      <td>2.50</td>
    </tr>
    <tr>
      <th>Wonka Bar - Triple Dazzle Caramel</th>
      <td>7596</td>
      <td>9874.80</td>
      <td>28485.00</td>
      <td>18610.20</td>
      <td>65.33</td>
      <td>19.65</td>
      <td>19.92</td>
      <td>2.45</td>
    </tr>
    <tr>
      <th>Wonka Bar - Milk Chocolate</th>
      <td>8267</td>
      <td>9424.38</td>
      <td>26867.75</td>
      <td>17443.37</td>
      <td>64.92</td>
      <td>21.39</td>
      <td>18.67</td>
      <td>2.11</td>
    </tr>
    <tr>
      <th>Wonka Bar - Nutty Crunch Surprise</th>
      <td>6755</td>
      <td>6755.00</td>
      <td>23574.95</td>
      <td>16819.95</td>
      <td>71.35</td>
      <td>17.48</td>
      <td>18.00</td>
      <td>2.49</td>
    </tr>
    <tr>
      <th>Wonka Bar - Fudge Mallows</th>
      <td>6914</td>
      <td>8296.80</td>
      <td>24890.40</td>
      <td>16593.60</td>
      <td>66.67</td>
      <td>17.89</td>
      <td>17.76</td>
      <td>2.40</td>
    </tr>
    <tr>
      <th>Lickable Wallpaper</th>
      <td>393</td>
      <td>3930.00</td>
      <td>7860.00</td>
      <td>3930.00</td>
      <td>50.00</td>
      <td>1.02</td>
      <td>4.21</td>
      <td>10.00</td>
    </tr>
    <tr>
      <th>Wonka Gum</th>
      <td>478</td>
      <td>286.80</td>
      <td>597.50</td>
      <td>310.70</td>
      <td>52.00</td>
      <td>1.24</td>
      <td>0.33</td>
      <td>0.65</td>
    </tr>
    <tr>
      <th>Everlasting Gobstopper</th>
      <td>13</td>
      <td>26.00</td>
      <td>130.00</td>
      <td>104.00</td>
      <td>80.00</td>
      <td>0.03</td>
      <td>0.11</td>
      <td>8.00</td>
    </tr>
    <tr>
      <th>Kazookles</th>
      <td>371</td>
      <td>1113.00</td>
      <td>1205.75</td>
      <td>92.75</td>
      <td>7.69</td>
      <td>0.96</td>
      <td>0.10</td>
      <td>0.25</td>
    </tr>
    <tr>
      <th>Hair Toffee</th>
      <td>17</td>
      <td>17.00</td>
      <td>76.50</td>
      <td>59.50</td>
      <td>77.78</td>
      <td>0.04</td>
      <td>0.06</td>
      <td>3.50</td>
    </tr>
    <tr>
      <th>Fizzy Lifting Drinks</th>
      <td>21</td>
      <td>31.50</td>
      <td>78.75</td>
      <td>47.25</td>
      <td>60.00</td>
      <td>0.05</td>
      <td>0.05</td>
      <td>2.25</td>
    </tr>
    <tr>
      <th>Laffy Taffy</th>
      <td>27</td>
      <td>20.25</td>
      <td>53.73</td>
      <td>33.48</td>
      <td>62.31</td>
      <td>0.07</td>
      <td>0.04</td>
      <td>1.24</td>
    </tr>
    <tr>
      <th>Sweet arts</th>
      <td>41</td>
      <td>32.80</td>
      <td>61.50</td>
      <td>28.70</td>
      <td>46.67</td>
      <td>0.11</td>
      <td>0.03</td>
      <td>0.70</td>
    </tr>
    <tr>
      <th>Fun Dip</th>
      <td>8</td>
      <td>7.20</td>
      <td>12.00</td>
      <td>4.80</td>
      <td>40.00</td>
      <td>0.02</td>
      <td>0.01</td>
      <td>0.60</td>
    </tr>
    <tr>
      <th>Nerds</th>
      <td>10</td>
      <td>8.00</td>
      <td>15.00</td>
      <td>7.00</td>
      <td>46.67</td>
      <td>0.03</td>
      <td>0.01</td>
      <td>0.70</td>
    </tr>
  </tbody>
</table>
</div>




```python

```

## Product-Level Profitability Analysis
• Rank products by:
○ Gross profit
○ Gross margin

• Identify:
○ High-profit / high-margin products
○ High-sales / low-margin products
○ Low-sales / low-profit products


```python
## Rank products by:
# Gross profit
ProductWise_Profit = df.groupby('Product Name')['Gross Profit'].sum()
ProductWise_Profit=ProductWise_Profit.sort_values(ascending=False).reset_index()
ProductWise_Profit.index=ProductWise_Profit.index +1
ProductWise_Profit
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
      <th>Product Name</th>
      <th>Gross Profit</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>Wonka Bar -Scrumdiddlyumptious</td>
      <td>19357.50</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Wonka Bar - Triple Dazzle Caramel</td>
      <td>18610.20</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Wonka Bar - Milk Chocolate</td>
      <td>17443.37</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Wonka Bar - Nutty Crunch Surprise</td>
      <td>16819.95</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Wonka Bar - Fudge Mallows</td>
      <td>16593.60</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Lickable Wallpaper</td>
      <td>3930.00</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Wonka Gum</td>
      <td>310.70</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Everlasting Gobstopper</td>
      <td>104.00</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Kazookles</td>
      <td>92.75</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Hair Toffee</td>
      <td>59.50</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Fizzy Lifting Drinks</td>
      <td>47.25</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Laffy Taffy</td>
      <td>33.48</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Sweet arts</td>
      <td>28.70</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Nerds</td>
      <td>7.00</td>
    </tr>
    <tr>
      <th>15</th>
      <td>Fun Dip</td>
      <td>4.80</td>
    </tr>
  </tbody>
</table>
</div>




```python
## Rank products by:
# Gross Margin
ProductWise_Profit = df.groupby('Product Name')[['Sales','Gross Profit']].sum()
ProductWise_Profit['Gross Margin']=((ProductWise_Profit['Gross Profit']/ProductWise_Profit['Sales'])*100).round(2)
ProductWise_Profit=ProductWise_Profit.sort_values(by='Gross Margin',ascending=False).reset_index()
ProductWise_Profit.index=ProductWise_Profit.index +1
ProductWise_Profit
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
      <th>Product Name</th>
      <th>Sales</th>
      <th>Gross Profit</th>
      <th>Gross Margin</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>Everlasting Gobstopper</td>
      <td>130.00</td>
      <td>104.00</td>
      <td>80.00</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Hair Toffee</td>
      <td>76.50</td>
      <td>59.50</td>
      <td>77.78</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Wonka Bar - Nutty Crunch Surprise</td>
      <td>23574.95</td>
      <td>16819.95</td>
      <td>71.35</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Wonka Bar -Scrumdiddlyumptious</td>
      <td>27874.80</td>
      <td>19357.50</td>
      <td>69.44</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Wonka Bar - Fudge Mallows</td>
      <td>24890.40</td>
      <td>16593.60</td>
      <td>66.67</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Wonka Bar - Triple Dazzle Caramel</td>
      <td>28485.00</td>
      <td>18610.20</td>
      <td>65.33</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Wonka Bar - Milk Chocolate</td>
      <td>26867.75</td>
      <td>17443.37</td>
      <td>64.92</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Laffy Taffy</td>
      <td>53.73</td>
      <td>33.48</td>
      <td>62.31</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Fizzy Lifting Drinks</td>
      <td>78.75</td>
      <td>47.25</td>
      <td>60.00</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Wonka Gum</td>
      <td>597.50</td>
      <td>310.70</td>
      <td>52.00</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Lickable Wallpaper</td>
      <td>7860.00</td>
      <td>3930.00</td>
      <td>50.00</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Nerds</td>
      <td>15.00</td>
      <td>7.00</td>
      <td>46.67</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Sweet arts</td>
      <td>61.50</td>
      <td>28.70</td>
      <td>46.67</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Fun Dip</td>
      <td>12.00</td>
      <td>4.80</td>
      <td>40.00</td>
    </tr>
    <tr>
      <th>15</th>
      <td>Kazookles</td>
      <td>1205.75</td>
      <td>92.75</td>
      <td>7.69</td>
    </tr>
  </tbody>
</table>
</div>



• Identify:
○ High-profit / high-margin products
○ High-sales / low-margin products
○ Low-sales / low-profit products


```python
def margin_status (x):
    if x['Profit_%'] > 50 & x['Profit_%'] > 50:
        return 'High Profit'
    elif x['Profit_%'] > 60:
        return 'Medium Profit'
    elif x['Profit_%'] > 40:
        return 'Low Profit'
    else:
        return 'Very Low Profit'
```


```python
## Identify:
# High-profit / high-margin products
# High-sales / low-margin products
# Low-sales / low-profit products
    
product_rnk=df.groupby('Product Name')[['Gross Profit','Sales','Cost']].sum()
product_rnk['Profit_%']=((product_rnk['Gross Profit']/product_rnk['Sales'])*100).round(2)
product_rnk=product_rnk.sort_values(by='Gross Profit',ascending=False).reset_index()
product_rnk['Profit_Status']=product_rnk.apply(margin_status, axis=1)
product_rnk.index=product_rnk.index + 1
product_rnk
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
      <th>Product Name</th>
      <th>Gross Profit</th>
      <th>Sales</th>
      <th>Cost</th>
      <th>Profit_%</th>
      <th>Profit_Status</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>Wonka Bar -Scrumdiddlyumptious</td>
      <td>19357.50</td>
      <td>27874.80</td>
      <td>8517.30</td>
      <td>69.44</td>
      <td>Medium Profit</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Wonka Bar - Triple Dazzle Caramel</td>
      <td>18610.20</td>
      <td>28485.00</td>
      <td>9874.80</td>
      <td>65.33</td>
      <td>Medium Profit</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Wonka Bar - Milk Chocolate</td>
      <td>17443.37</td>
      <td>26867.75</td>
      <td>9424.38</td>
      <td>64.92</td>
      <td>Medium Profit</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Wonka Bar - Nutty Crunch Surprise</td>
      <td>16819.95</td>
      <td>23574.95</td>
      <td>6755.00</td>
      <td>71.35</td>
      <td>Medium Profit</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Wonka Bar - Fudge Mallows</td>
      <td>16593.60</td>
      <td>24890.40</td>
      <td>8296.80</td>
      <td>66.67</td>
      <td>Medium Profit</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Lickable Wallpaper</td>
      <td>3930.00</td>
      <td>7860.00</td>
      <td>3930.00</td>
      <td>50.00</td>
      <td>Low Profit</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Wonka Gum</td>
      <td>310.70</td>
      <td>597.50</td>
      <td>286.80</td>
      <td>52.00</td>
      <td>Low Profit</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Everlasting Gobstopper</td>
      <td>104.00</td>
      <td>130.00</td>
      <td>26.00</td>
      <td>80.00</td>
      <td>Medium Profit</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Kazookles</td>
      <td>92.75</td>
      <td>1205.75</td>
      <td>1113.00</td>
      <td>7.69</td>
      <td>Very Low Profit</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Hair Toffee</td>
      <td>59.50</td>
      <td>76.50</td>
      <td>17.00</td>
      <td>77.78</td>
      <td>Medium Profit</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Fizzy Lifting Drinks</td>
      <td>47.25</td>
      <td>78.75</td>
      <td>31.50</td>
      <td>60.00</td>
      <td>Low Profit</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Laffy Taffy</td>
      <td>33.48</td>
      <td>53.73</td>
      <td>20.25</td>
      <td>62.31</td>
      <td>Medium Profit</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Sweet arts</td>
      <td>28.70</td>
      <td>61.50</td>
      <td>32.80</td>
      <td>46.67</td>
      <td>Low Profit</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Nerds</td>
      <td>7.00</td>
      <td>15.00</td>
      <td>8.00</td>
      <td>46.67</td>
      <td>Low Profit</td>
    </tr>
    <tr>
      <th>15</th>
      <td>Fun Dip</td>
      <td>4.80</td>
      <td>12.00</td>
      <td>7.20</td>
      <td>40.00</td>
      <td>Very Low Profit</td>
    </tr>
  </tbody>
</table>
</div>



--------------------------------------------------------------------------------------------------------------------------------------------------------

### Observations : Which products represent margin risk
1. Kazookles is the only product with a margin risk, having a profit margin of 7.69% while selling over 370 units.
2. Sweetarts and Nerds are the products with a profit margin of 46.67%.

### Profitability Metric Calculation For each product:
1. Gross Margin (%)
2. Profit per unit
3. Total profit contribution


```python
top_profit=df.sort_values(by='Profit Contribution %',ascending=False)
plt.figure()
plt.pie('Profit Contribution %'.index, top_profit['Profit Contribution %'])
plt.xlabel('Profit Contribution %')
plt.ylabel('Product Name')
plt.title('Profit Contribution % Per Product')
plt.show()
```


    ---------------------------------------------------------------------------

    KeyError                                  Traceback (most recent call last)

    ~\AppData\Local\Temp\ipykernel_13888\3829100196.py in ?()
    ----> 1 top_profit=df.sort_values(by='Profit Contribution %',ascending=False)
          2 plt.figure()
          3 plt.pie('Profit Contribution %'.index, top_profit['Profit Contribution %'])
          4 plt.xlabel('Profit Contribution %')
    

    ~\anaconda3\Lib\site-packages\pandas\core\frame.py in ?(self, by, axis, ascending, inplace, kind, na_position, ignore_index, key)
       7185             )
       7186         elif len(by):
       7187             # len(by) == 1
       7188 
    -> 7189             k = self._get_label_or_level_values(by[0], axis=axis)
       7190 
       7191             # need to rewrap column in Series to apply key function
       7192             if key is not None:
    

    ~\anaconda3\Lib\site-packages\pandas\core\generic.py in ?(self, key, axis)
       1907             values = self.xs(key, axis=other_axes[0])._values
       1908         elif self._is_level_reference(key, axis=axis):
       1909             values = self.axes[axis].get_level_values(key)._values
       1910         else:
    -> 1911             raise KeyError(key)
       1912 
       1913         # Check for duplicates
       1914         if values.ndim > 1:
    

    KeyError: 'Profit Contribution %'


## Product-Level Profitability Analysis
Rank products by:
1. Gross profit
2. Gross margin


```python
## Gross Profit Wise Product Rank
df=df.groupby('Product Name')[['Sales','Gross Profit']].sum()
Total_Profit=df['Gross Profit'].sum()
df['Gross Margin']=((df['Gross Profit']/df['Sales'])*100).round(2)
df=df.sort_values(by='Gross Profit', ascending=False).reset_index()
df.index=df.index +1
df
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
      <th>Product Name</th>
      <th>Sales</th>
      <th>Gross Profit</th>
      <th>Gross Margin</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>Wonka Bar -Scrumdiddlyumptious</td>
      <td>27874.80</td>
      <td>19357.50</td>
      <td>69.44</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Wonka Bar - Triple Dazzle Caramel</td>
      <td>28485.00</td>
      <td>18610.20</td>
      <td>65.33</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Wonka Bar - Milk Chocolate</td>
      <td>26867.75</td>
      <td>17443.37</td>
      <td>64.92</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Wonka Bar - Nutty Crunch Surprise</td>
      <td>23574.95</td>
      <td>16819.95</td>
      <td>71.35</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Wonka Bar - Fudge Mallows</td>
      <td>24890.40</td>
      <td>16593.60</td>
      <td>66.67</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Lickable Wallpaper</td>
      <td>7860.00</td>
      <td>3930.00</td>
      <td>50.00</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Wonka Gum</td>
      <td>597.50</td>
      <td>310.70</td>
      <td>52.00</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Everlasting Gobstopper</td>
      <td>130.00</td>
      <td>104.00</td>
      <td>80.00</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Kazookles</td>
      <td>1205.75</td>
      <td>92.75</td>
      <td>7.69</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Hair Toffee</td>
      <td>76.50</td>
      <td>59.50</td>
      <td>77.78</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Fizzy Lifting Drinks</td>
      <td>78.75</td>
      <td>47.25</td>
      <td>60.00</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Laffy Taffy</td>
      <td>53.73</td>
      <td>33.48</td>
      <td>62.31</td>
    </tr>
    <tr>
      <th>13</th>
      <td>SweeTARTS</td>
      <td>61.50</td>
      <td>28.70</td>
      <td>46.67</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Nerds</td>
      <td>15.00</td>
      <td>7.00</td>
      <td>46.67</td>
    </tr>
    <tr>
      <th>15</th>
      <td>Fun Dip</td>
      <td>12.00</td>
      <td>4.80</td>
      <td>40.00</td>
    </tr>
  </tbody>
</table>
</div>




```python
## Gross Margin Wise Product Rank
df=df.groupby('Product Name')[['Sales','Gross Profit']].sum()
Total_Profit=df['Gross Profit'].sum()
df['Gross Margin']=((df['Gross Profit']/df['Sales'])*100).round(2)
df=df.sort_values(by='Gross Margin', ascending=False).reset_index()
df.index=df.index +1
df
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
      <th>Product Name</th>
      <th>Sales</th>
      <th>Gross Profit</th>
      <th>Gross Margin</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>Everlasting Gobstopper</td>
      <td>130.00</td>
      <td>104.00</td>
      <td>80.00</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Hair Toffee</td>
      <td>76.50</td>
      <td>59.50</td>
      <td>77.78</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Wonka Bar - Nutty Crunch Surprise</td>
      <td>23574.95</td>
      <td>16819.95</td>
      <td>71.35</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Wonka Bar -Scrumdiddlyumptious</td>
      <td>27874.80</td>
      <td>19357.50</td>
      <td>69.44</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Wonka Bar - Fudge Mallows</td>
      <td>24890.40</td>
      <td>16593.60</td>
      <td>66.67</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Wonka Bar - Triple Dazzle Caramel</td>
      <td>28485.00</td>
      <td>18610.20</td>
      <td>65.33</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Wonka Bar - Milk Chocolate</td>
      <td>26867.75</td>
      <td>17443.37</td>
      <td>64.92</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Laffy Taffy</td>
      <td>53.73</td>
      <td>33.48</td>
      <td>62.31</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Fizzy Lifting Drinks</td>
      <td>78.75</td>
      <td>47.25</td>
      <td>60.00</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Wonka Gum</td>
      <td>597.50</td>
      <td>310.70</td>
      <td>52.00</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Lickable Wallpaper</td>
      <td>7860.00</td>
      <td>3930.00</td>
      <td>50.00</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Nerds</td>
      <td>15.00</td>
      <td>7.00</td>
      <td>46.67</td>
    </tr>
    <tr>
      <th>13</th>
      <td>SweeTARTS</td>
      <td>61.50</td>
      <td>28.70</td>
      <td>46.67</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Fun Dip</td>
      <td>12.00</td>
      <td>4.80</td>
      <td>40.00</td>
    </tr>
    <tr>
      <th>15</th>
      <td>Kazookles</td>
      <td>1205.75</td>
      <td>92.75</td>
      <td>7.69</td>
    </tr>
  </tbody>
</table>
</div>



## Identify:
1. High-profit / high-margin products
2. High-sales / low-margin products
3. Low-sales / low-profit products


```python
## Def function for getting margin and sales status
def product_status(x):
    if (x['Gross Profit']) > 10000 and (x['Gross Margin'] > 50):
        return "High Profit & High Margin"
    elif (x['Sales'] > 5000) and (x['Gross Margin'] < 60) :
        return "High Sales & Low Margin"
    elif (x['Sales'] < 5000) and (x['Gross Profit'] > 1000) :
        return "Low Sales & Low Profit"
    else :
        return ("Moderate Performance")
```


```python
Performance_Status=df.groupby('Product Name')[['Sales','Gross Profit']].sum()
Performance_Status['Gross Margin']=((Performance_Status['Gross Profit']/Performance_Status['Sales'])*100).round(2)
Performance_Status['product_status']=Performance_Status.apply(product_status, axis=1)
Performance_Status=Performance_Status.sort_values(by='Gross Profit', ascending=False).reset_index()
Performance_Status.index=Performance_Status.index +1
Performance_Status
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
      <th>Product Name</th>
      <th>Sales</th>
      <th>Gross Profit</th>
      <th>Gross Margin</th>
      <th>product_status</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>Wonka Bar -Scrumdiddlyumptious</td>
      <td>27874.80</td>
      <td>19357.50</td>
      <td>69.44</td>
      <td>High Profit &amp; High Margin</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Wonka Bar - Triple Dazzle Caramel</td>
      <td>28485.00</td>
      <td>18610.20</td>
      <td>65.33</td>
      <td>High Profit &amp; High Margin</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Wonka Bar - Milk Chocolate</td>
      <td>26867.75</td>
      <td>17443.37</td>
      <td>64.92</td>
      <td>High Profit &amp; High Margin</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Wonka Bar - Nutty Crunch Surprise</td>
      <td>23574.95</td>
      <td>16819.95</td>
      <td>71.35</td>
      <td>High Profit &amp; High Margin</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Wonka Bar - Fudge Mallows</td>
      <td>24890.40</td>
      <td>16593.60</td>
      <td>66.67</td>
      <td>High Profit &amp; High Margin</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Lickable Wallpaper</td>
      <td>7860.00</td>
      <td>3930.00</td>
      <td>50.00</td>
      <td>High Sales &amp; Low Margin</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Wonka Gum</td>
      <td>597.50</td>
      <td>310.70</td>
      <td>52.00</td>
      <td>Moderate Performance</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Everlasting Gobstopper</td>
      <td>130.00</td>
      <td>104.00</td>
      <td>80.00</td>
      <td>Moderate Performance</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Kazookles</td>
      <td>1205.75</td>
      <td>92.75</td>
      <td>7.69</td>
      <td>Moderate Performance</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Hair Toffee</td>
      <td>76.50</td>
      <td>59.50</td>
      <td>77.78</td>
      <td>Moderate Performance</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Fizzy Lifting Drinks</td>
      <td>78.75</td>
      <td>47.25</td>
      <td>60.00</td>
      <td>Moderate Performance</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Laffy Taffy</td>
      <td>53.73</td>
      <td>33.48</td>
      <td>62.31</td>
      <td>Moderate Performance</td>
    </tr>
    <tr>
      <th>13</th>
      <td>SweeTARTS</td>
      <td>61.50</td>
      <td>28.70</td>
      <td>46.67</td>
      <td>Moderate Performance</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Nerds</td>
      <td>15.00</td>
      <td>7.00</td>
      <td>46.67</td>
      <td>Moderate Performance</td>
    </tr>
    <tr>
      <th>15</th>
      <td>Fun Dip</td>
      <td>12.00</td>
      <td>4.80</td>
      <td>40.00</td>
      <td>Moderate Performance</td>
    </tr>
  </tbody>
</table>
</div>



## Division-Level Performance Analysis
# Aggregate metrics by Division
# Compare:
1. Average margin by division
2. Revenue vs profit imbalance


```python
## 1. Average margin by division
df['Gross Margin']=((df['Gross Profit']/df['Sales'])*100).round(2)
div_margin=df.groupby('Division')['Gross Margin'].mean().round(2)
div_margin
```




    Division
    Chocolate    67.46
    Other        37.67
    Sugar        57.69
    Name: Gross Margin, dtype: float64



## 2. Revenue vs profit imbalance


```python
def revenue_profit_imbalance(x):
    if (x['Sales'] > 20000) and (x['Gross Margin'] < 50):
        return "High Sales With Low Margin"
    elif (x['Sales'] < 10000) and (x['Gross Margin'] > 50):
        return "Low Sales With High Margin"
    elif (x['Sales'] < 2000) and (x['Gross Margin'] < 20):
        return "Low Sales With Low Margin"
    elif (x['Sales'] > 10000) and (x['Gross Margin'] > 50):
        return "High Sales With High Margin"
    else:
        return "Balanced"
```


```python
margin_imbalance=df.groupby('Product Name')[['Sales','Gross Profit']].sum()
margin_imbalance['Gross Margin']=((margin_imbalance['Gross Profit']/margin_imbalance['Sales'])*100).round(2)
margin_imbalance['Imbalance Status']=margin_imbalance.apply(revenue_profit_imbalance, axis=1)
margin_imbalance=margin_imbalance.sort_values(by='Gross Profit', ascending=False).reset_index()
margin_imbalance.index=margin_imbalance.index +1
margin_imbalance
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
      <th>Product Name</th>
      <th>Sales</th>
      <th>Gross Profit</th>
      <th>Gross Margin</th>
      <th>Imbalance Status</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>Wonka Bar -Scrumdiddlyumptious</td>
      <td>27874.80</td>
      <td>19357.50</td>
      <td>69.44</td>
      <td>High Sales With High Margin</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Wonka Bar - Triple Dazzle Caramel</td>
      <td>28485.00</td>
      <td>18610.20</td>
      <td>65.33</td>
      <td>High Sales With High Margin</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Wonka Bar - Milk Chocolate</td>
      <td>26867.75</td>
      <td>17443.37</td>
      <td>64.92</td>
      <td>High Sales With High Margin</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Wonka Bar - Nutty Crunch Surprise</td>
      <td>23574.95</td>
      <td>16819.95</td>
      <td>71.35</td>
      <td>High Sales With High Margin</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Wonka Bar - Fudge Mallows</td>
      <td>24890.40</td>
      <td>16593.60</td>
      <td>66.67</td>
      <td>High Sales With High Margin</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Lickable Wallpaper</td>
      <td>7860.00</td>
      <td>3930.00</td>
      <td>50.00</td>
      <td>Balanced</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Wonka Gum</td>
      <td>597.50</td>
      <td>310.70</td>
      <td>52.00</td>
      <td>Low Sales With High Margin</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Everlasting Gobstopper</td>
      <td>130.00</td>
      <td>104.00</td>
      <td>80.00</td>
      <td>Low Sales With High Margin</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Kazookles</td>
      <td>1205.75</td>
      <td>92.75</td>
      <td>7.69</td>
      <td>Low Sales With Low Margin</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Hair Toffee</td>
      <td>76.50</td>
      <td>59.50</td>
      <td>77.78</td>
      <td>Low Sales With High Margin</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Fizzy Lifting Drinks</td>
      <td>78.75</td>
      <td>47.25</td>
      <td>60.00</td>
      <td>Low Sales With High Margin</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Laffy Taffy</td>
      <td>53.73</td>
      <td>33.48</td>
      <td>62.31</td>
      <td>Low Sales With High Margin</td>
    </tr>
    <tr>
      <th>13</th>
      <td>SweeTARTS</td>
      <td>61.50</td>
      <td>28.70</td>
      <td>46.67</td>
      <td>Balanced</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Nerds</td>
      <td>15.00</td>
      <td>7.00</td>
      <td>46.67</td>
      <td>Balanced</td>
    </tr>
    <tr>
      <th>15</th>
      <td>Fun Dip</td>
      <td>12.00</td>
      <td>4.80</td>
      <td>40.00</td>
      <td>Balanced</td>
    </tr>
  </tbody>
</table>
</div>



## Division-Level Performance Analysis
## Aggregate metrics by Division
# Compare:
# Identify divisions with:
1. Strong financial efficiency
2. Structural margin issues


```python
## Def function for Financial Efficiency
def financial_efficiency(x):
    if (x['Gross Margin']>50):
        return "Strong Financial Efficiency"
    elif (x['Gross Margin']<20):
        return "Weak Financial Efficiency"
    else:
        return "Moderate"
```


```python
total_profit=df['Gross Profit'].sum()
Fin_eff=df.groupby('Division')[['Sales','Gross Profit']].sum()
Fin_eff['Gross Margin']=((Fin_eff['Gross Profit']/Fin_eff['Sales'])*100).round(2)
Fin_eff['Efficiency Status']=Fin_eff.apply(financial_efficiency, axis=1)
Fin_eff['Profit_%']=(Fin_eff['Gross Profit']/total_profit*100).round(2)
Fin_eff=Fin_eff.sort_values(by='Sales', ascending=False).reset_index()
Fin_eff.index=Fin_eff.index +1
Fin_eff
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
      <th>Division</th>
      <th>Sales</th>
      <th>Gross Profit</th>
      <th>Gross Margin</th>
      <th>Efficiency Status</th>
      <th>Profit_%</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>Chocolate</td>
      <td>131692.90</td>
      <td>88824.62</td>
      <td>67.45</td>
      <td>Strong Financial Efficiency</td>
      <td>95.06</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Other</td>
      <td>9663.25</td>
      <td>4333.45</td>
      <td>44.84</td>
      <td>Moderate</td>
      <td>4.64</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Sugar</td>
      <td>427.48</td>
      <td>284.73</td>
      <td>66.61</td>
      <td>Strong Financial Efficiency</td>
      <td>0.30</td>
    </tr>
  </tbody>
</table>
</div>



## ML PROJECT
Profit Concentration (Pareto) Analysis
• Determine % of products contributing:
○ 80% of revenue
○ 80% of profit
• Detect congestion-prone states or regionIdentify over-dependency risks


```python
total_sales=df['Sales'].sum()
total_profit=df['Gross Profit'].sum()
product_category_profit=df.groupby('Product Name')[['Sales','Gross Profit']].sum().reset_index()
product_category_profit=product_category_profit.sort_values(by='Gross Profit', ascending=False)
product_category_profit['Cumulative Sales']=(product_category_profit['Sales']/total_sales*100).cumsum()
product_category_profit['Cumulative Profit']=(product_category_profit['Gross Profit']/total_profit*100).cumsum()
top_products=product_category_profit[product_category_profit['Cumulative Profit']<=80]
top_products
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
      <th>Product Name</th>
      <th>Sales</th>
      <th>Gross Profit</th>
      <th>Cumulative Sales</th>
      <th>Cumulative Profit</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>13</th>
      <td>Wonka Bar -Scrumdiddlyumptious</td>
      <td>27874.80</td>
      <td>19357.50</td>
      <td>19.660098</td>
      <td>20.715882</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Wonka Bar - Triple Dazzle Caramel</td>
      <td>28485.00</td>
      <td>18610.20</td>
      <td>39.750569</td>
      <td>40.632023</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Wonka Bar - Milk Chocolate</td>
      <td>26867.75</td>
      <td>17443.37</td>
      <td>58.700394</td>
      <td>59.299454</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Wonka Bar - Nutty Crunch Surprise</td>
      <td>23574.95</td>
      <td>16819.95</td>
      <td>75.327808</td>
      <td>77.299717</td>
    </tr>
  </tbody>
</table>
</div>




```python
total_sales=df['Sales'].sum()
total_profit=df['Gross Profit'].sum()
product_category_profit=df.groupby('Region')[['Gross Profit','Sales']].sum()
product_category_profit=product_category_profit.sort_values(by='Sales', ascending=False)
product_category_profit['Sales_%']=(product_category_profit['Sales']/total_sales*100).round(2)
product_category_profit['Cumulative Sales']=(product_category_profit['Sales']/total_sales*100).cumsum()
product_category_profit['Cumulative Profit']=(product_category_profit['Gross Profit']/total_profit*100).cumsum()
product_category_profit['Total Sales']=total_sales
top_products=product_category_profit[product_category_profit['Cumulative Profit']<=101]
top_products
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
      <th>Gross Profit</th>
      <th>Sales</th>
      <th>Sales_%</th>
      <th>Cumulative Sales</th>
      <th>Cumulative Profit</th>
      <th>Total Sales</th>
    </tr>
    <tr>
      <th>Region</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Pacific</th>
      <td>30485.94</td>
      <td>46301.53</td>
      <td>32.66</td>
      <td>32.656471</td>
      <td>32.625242</td>
      <td>141783.63</td>
    </tr>
    <tr>
      <th>Atlantic</th>
      <td>26973.70</td>
      <td>41197.24</td>
      <td>29.06</td>
      <td>61.712886</td>
      <td>61.491779</td>
      <td>141783.63</td>
    </tr>
    <tr>
      <th>Interior</th>
      <td>21282.49</td>
      <td>32037.60</td>
      <td>22.60</td>
      <td>84.309007</td>
      <td>84.267734</td>
      <td>141783.63</td>
    </tr>
    <tr>
      <th>Gulf</th>
      <td>14700.67</td>
      <td>22247.26</td>
      <td>15.69</td>
      <td>100.000000</td>
      <td>100.000000</td>
      <td>141783.63</td>
    </tr>
  </tbody>
</table>
</div>




```python
region_sale=df.groupby('Region')['Sales'].sum()
region_sale
```




    Region
    Atlantic    41197.24
    Gulf        22247.26
    Interior    32037.60
    Pacific     46301.53
    Name: Sales, dtype: float64



Cost Structure Diagnostics
• Cost vs sales scatter analysis
• Identify:
○ Cost-heavy, margin-poor products
○ Pricing inefficiencies
• Flag products needing:
○ Repricing
○ Cost renegotiation
○ Discontinuation review


```python
## Cost-heavy, margin-poor products
df=df.groupby('Product Name')[['Gross Profit','Sales']].sum()
df['Gross Margin']=((df['Gross Profit']/df['Sales'])*100).round(2)
cost_heavy_products=df[(df['Gross Margin']<50) & (df['Sales']>1000)]
cost_heavy_products
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
      <th>Gross Profit</th>
      <th>Sales</th>
      <th>Gross Margin</th>
    </tr>
    <tr>
      <th>Product Name</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Kazookles</th>
      <td>92.75</td>
      <td>1205.75</td>
      <td>7.69</td>
    </tr>
  </tbody>
</table>
</div>




```python
df=df.groupby('Product Name')[['Gross Profit','Sales']].sum()
df['Gross Margin']=((df['Gross Profit']/df['Sales'])*100).round(2)
df.sort_values(by='Gross Margin', ascending=False)
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
      <th>Gross Profit</th>
      <th>Sales</th>
      <th>Gross Margin</th>
    </tr>
    <tr>
      <th>Product Name</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Everlasting Gobstopper</th>
      <td>104.00</td>
      <td>130.00</td>
      <td>80.00</td>
    </tr>
    <tr>
      <th>Hair Toffee</th>
      <td>59.50</td>
      <td>76.50</td>
      <td>77.78</td>
    </tr>
    <tr>
      <th>Wonka Bar - Nutty Crunch Surprise</th>
      <td>16819.95</td>
      <td>23574.95</td>
      <td>71.35</td>
    </tr>
    <tr>
      <th>Wonka Bar -Scrumdiddlyumptious</th>
      <td>19357.50</td>
      <td>27874.80</td>
      <td>69.44</td>
    </tr>
    <tr>
      <th>Wonka Bar - Fudge Mallows</th>
      <td>16593.60</td>
      <td>24890.40</td>
      <td>66.67</td>
    </tr>
    <tr>
      <th>Wonka Bar - Triple Dazzle Caramel</th>
      <td>18610.20</td>
      <td>28485.00</td>
      <td>65.33</td>
    </tr>
    <tr>
      <th>Wonka Bar - Milk Chocolate</th>
      <td>17443.37</td>
      <td>26867.75</td>
      <td>64.92</td>
    </tr>
    <tr>
      <th>Laffy Taffy</th>
      <td>33.48</td>
      <td>53.73</td>
      <td>62.31</td>
    </tr>
    <tr>
      <th>Fizzy Lifting Drinks</th>
      <td>47.25</td>
      <td>78.75</td>
      <td>60.00</td>
    </tr>
    <tr>
      <th>Wonka Gum</th>
      <td>310.70</td>
      <td>597.50</td>
      <td>52.00</td>
    </tr>
    <tr>
      <th>Lickable Wallpaper</th>
      <td>3930.00</td>
      <td>7860.00</td>
      <td>50.00</td>
    </tr>
    <tr>
      <th>Nerds</th>
      <td>7.00</td>
      <td>15.00</td>
      <td>46.67</td>
    </tr>
    <tr>
      <th>SweeTARTS</th>
      <td>28.70</td>
      <td>61.50</td>
      <td>46.67</td>
    </tr>
    <tr>
      <th>Fun Dip</th>
      <td>4.80</td>
      <td>12.00</td>
      <td>40.00</td>
    </tr>
    <tr>
      <th>Kazookles</th>
      <td>92.75</td>
      <td>1205.75</td>
      <td>7.69</td>
    </tr>
  </tbody>
</table>
</div>




```python
## Pricing inefficiencies
df['Gross Margin']=((df['Gross Profit']/df['Sales'])*100).round(2)
pricing_issues=df[(df['Sales']>1000) & (df['Gross Margin']<20)]
pricing_issues
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
      <th>Gross Profit</th>
      <th>Sales</th>
      <th>Gross Margin</th>
    </tr>
    <tr>
      <th>Product Name</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Kazookles</th>
      <td>92.75</td>
      <td>1205.75</td>
      <td>7.69</td>
    </tr>
  </tbody>
</table>
</div>




```python
## Find sales greater than median
pricing_issues=df[(df['Sales']>df['Sales'].median()) & (df['Gross Margin'] < 60)]
pricing_issues.sort_values(by='Sales', ascending=False)
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
      <th>Gross Profit</th>
      <th>Sales</th>
      <th>Gross Margin</th>
    </tr>
    <tr>
      <th>Product Name</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Lickable Wallpaper</th>
      <td>3930.00</td>
      <td>7860.00</td>
      <td>50.00</td>
    </tr>
    <tr>
      <th>Kazookles</th>
      <td>92.75</td>
      <td>1205.75</td>
      <td>7.69</td>
    </tr>
  </tbody>
</table>
</div>




```python
total_sales = df['Sales'].sum()
total_profit = df['Gross Profit'].sum()

product_category = df.groupby('Product Name')[['Sales','Gross Profit']].sum().reset_index()

product_category = product_category.sort_values(by='Gross Profit', ascending=False)

product_category['Cumulative Sales'] = product_category['Sales'].cumsum()
product_category['Cumulative Sales %'] = (product_category['Cumulative Sales'] / total_sales * 100).round(2)

product_category['Cumulative Profit'] = product_category['Gross Profit'].cumsum()
product_category['Cumulative Profit %'] = (product_category['Cumulative Profit'] / total_profit * 100).round(2)

top_products = product_category[product_category['Cumulative Profit %'] <= 80]

top_products
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
      <th>Product Name</th>
      <th>Sales</th>
      <th>Gross Profit</th>
      <th>Cumulative Sales</th>
      <th>Cumulative Sales %</th>
      <th>Cumulative Profit</th>
      <th>Cumulative Profit %</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>13</th>
      <td>Wonka Bar -Scrumdiddlyumptious</td>
      <td>27874.80</td>
      <td>19357.50</td>
      <td>27874.80</td>
      <td>19.66</td>
      <td>19357.50</td>
      <td>20.72</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Wonka Bar - Triple Dazzle Caramel</td>
      <td>28485.00</td>
      <td>18610.20</td>
      <td>56359.80</td>
      <td>39.75</td>
      <td>37967.70</td>
      <td>40.63</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Wonka Bar - Milk Chocolate</td>
      <td>26867.75</td>
      <td>17443.37</td>
      <td>83227.55</td>
      <td>58.70</td>
      <td>55411.07</td>
      <td>59.30</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Wonka Bar - Nutty Crunch Surprise</td>
      <td>23574.95</td>
      <td>16819.95</td>
      <td>106802.50</td>
      <td>75.33</td>
      <td>72231.02</td>
      <td>77.30</td>
    </tr>
  </tbody>
</table>
</div>




```python
## Find sales greater than mean for repricing
pricing_issues=df[(df['Sales']>df['Sales'].mean()) & (df['Gross Margin'] < 60)]
pricing_issues.sort_values(by='Sales', ascending=False)
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
      <th>Gross Profit</th>
      <th>Sales</th>
      <th>Gross Margin</th>
    </tr>
    <tr>
      <th>Product Name</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
  </tbody>
</table>
</div>




```python
## Cost renegotiation
df=df.groupby('Product Name')[['Cost','Sales']].sum()
df['Cost Ratio']=(df['Cost']/df['Sales']*100).round(1)
Cost_Renegotiation=df[df['Cost Ratio']>60]
Cost_Renegotiation
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
      <th>Cost</th>
      <th>Sales</th>
      <th>Cost Ratio</th>
    </tr>
    <tr>
      <th>Product Name</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Kazookles</th>
      <td>1113.0</td>
      <td>1205.75</td>
      <td>92.3</td>
    </tr>
  </tbody>
</table>
</div>




```python
## Discontinuation review
discontinue_product=df.groupby('Product Name')[['Sales','Gross Profit']].sum()
discontinue_product=discontinue_product[(discontinue_product['Sales']<1000) & (discontinue_product['Gross Profit'] <1000)]
discontinue_product
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
      <th>Sales</th>
      <th>Gross Profit</th>
    </tr>
    <tr>
      <th>Product Name</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Everlasting Gobstopper</th>
      <td>130.00</td>
      <td>104.00</td>
    </tr>
    <tr>
      <th>Fizzy Lifting Drinks</th>
      <td>78.75</td>
      <td>47.25</td>
    </tr>
    <tr>
      <th>Fun Dip</th>
      <td>12.00</td>
      <td>4.80</td>
    </tr>
    <tr>
      <th>Hair Toffee</th>
      <td>76.50</td>
      <td>59.50</td>
    </tr>
    <tr>
      <th>Laffy Taffy</th>
      <td>53.73</td>
      <td>33.48</td>
    </tr>
    <tr>
      <th>Nerds</th>
      <td>15.00</td>
      <td>7.00</td>
    </tr>
    <tr>
      <th>SweeTARTS</th>
      <td>61.50</td>
      <td>28.70</td>
    </tr>
    <tr>
      <th>Wonka Gum</th>
      <td>597.50</td>
      <td>310.70</td>
    </tr>
  </tbody>
</table>
</div>




```python
## Discontinuation review
df['Gross Margin']=((df['Gross Profit']/df['Sales'])*100).round(2)
discontinued_products=df[((df['Sales']>df['Sales'].median()) & (df['Gross Margin'] <10))]
discontinued_products.groupby('Product Name')[['Sales','Gross Profit']].sum()
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
      <th>Sales</th>
      <th>Gross Profit</th>
    </tr>
    <tr>
      <th>Product Name</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Kazookles</th>
      <td>832.0</td>
      <td>64.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
## City Wise Sales
city_wise=df.groupby('State/Province')['Sales'].sum()
city_wise.sort_values(ascending=False)
```




    State/Province
    California                   27917.40
    New York                     15541.03
    Texas                        13416.09
    Pennsylvania                  8027.03
    Washington                    6921.15
    Illinois                      6898.96
    Ohio                          6768.95
    Florida                       4804.02
    Arizona                       3587.55
    North Carolina                3450.86
    Michigan                      3331.00
    Virginia                      3177.84
    Georgia                       2692.84
    Colorado                      2544.91
    Tennessee                     2383.56
    Indiana                       2002.78
    Wisconsin                     1920.50
    Oregon                        1920.15
    Kentucky                      1880.63
    Massachusetts                 1806.99
    New Jersey                    1578.35
    Maryland                      1476.99
    Delaware                      1323.59
    Minnesota                     1161.46
    Alabama                        995.11
    Connecticut                    980.57
    Arkansas                       891.94
    Missouri                       882.83
    Oklahoma                       877.65
    Utah                           856.41
    Mississippi                    844.18
    Ontario                        814.57
    Rhode Island                   805.76
    Nevada                         759.46
    South Carolina                 601.07
    Quebec                         597.68
    Alberta                        530.32
    Louisiana                      525.21
    New Mexico                     502.71
    Nebraska                       483.53
    New Hampshire                  428.27
    Iowa                           400.37
    British Columbia               290.90
    Kansas                         263.18
    Idaho                          225.25
    Montana                        202.11
    New Brunswick                  172.72
    Vermont                        162.44
    Newfoundland and Labrador      162.00
    South Dakota                   151.34
    District of Columbia           142.25
    Manitoba                       138.25
    Prince Edward Island           130.10
    Maine                          126.48
    North Dakota                   109.66
    Nova Scotia                     87.50
    West Virginia                   63.97
    Saskatchewan                    29.25
    Wyoming                         13.96
    Name: Sales, dtype: float64




```python
## Correlation between Gross Profit and Sales
profit_sales_corr=df[['Gross Profit','Sales']].corr()
profit_sales_corr
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
      <th>Gross Profit</th>
      <th>Sales</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Gross Profit</th>
      <td>1.000000</td>
      <td>0.976404</td>
    </tr>
    <tr>
      <th>Sales</th>
      <td>0.976404</td>
      <td>1.000000</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.corr(numeric_only=True)
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
      <th>Row ID</th>
      <th>Customer ID</th>
      <th>Sales</th>
      <th>Units</th>
      <th>Gross Profit</th>
      <th>Cost</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Row ID</th>
      <td>1.000000</td>
      <td>-0.008749</td>
      <td>0.005513</td>
      <td>0.000502</td>
      <td>0.008031</td>
      <td>0.001812</td>
    </tr>
    <tr>
      <th>Customer ID</th>
      <td>-0.008749</td>
      <td>1.000000</td>
      <td>-0.005401</td>
      <td>-0.011616</td>
      <td>-0.005964</td>
      <td>-0.004274</td>
    </tr>
    <tr>
      <th>Sales</th>
      <td>0.005513</td>
      <td>-0.005401</td>
      <td>1.000000</td>
      <td>0.729347</td>
      <td>0.976404</td>
      <td>0.958986</td>
    </tr>
    <tr>
      <th>Units</th>
      <td>0.000502</td>
      <td>-0.011616</td>
      <td>0.729347</td>
      <td>1.000000</td>
      <td>0.815820</td>
      <td>0.563344</td>
    </tr>
    <tr>
      <th>Gross Profit</th>
      <td>0.008031</td>
      <td>-0.005964</td>
      <td>0.976404</td>
      <td>0.815820</td>
      <td>1.000000</td>
      <td>0.875144</td>
    </tr>
    <tr>
      <th>Cost</th>
      <td>0.001812</td>
      <td>-0.004274</td>
      <td>0.958986</td>
      <td>0.563344</td>
      <td>0.875144</td>
      <td>1.000000</td>
    </tr>
  </tbody>
</table>
</div>




```python
## Merging of 2 Tables
df_merged=pd.merge(df,df1, on='Division', how='left')
df_merged
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
      <th>Row ID</th>
      <th>Order ID</th>
      <th>Order Date</th>
      <th>Ship Date</th>
      <th>Ship Mode</th>
      <th>Customer ID</th>
      <th>Country/Region</th>
      <th>City</th>
      <th>State/Province</th>
      <th>Postal Code</th>
      <th>Division</th>
      <th>Region</th>
      <th>Product ID</th>
      <th>Product Name_x</th>
      <th>Sales</th>
      <th>Units</th>
      <th>Gross Profit</th>
      <th>Cost</th>
      <th>Product Name_y</th>
      <th>Factory</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>US-2021-103800-CHO-MIL-31000</td>
      <td>03-01-2024</td>
      <td>30-06-2026</td>
      <td>Standard Class</td>
      <td>103800</td>
      <td>United States</td>
      <td>Houston</td>
      <td>Texas</td>
      <td>77095</td>
      <td>Chocolate</td>
      <td>Interior</td>
      <td>CHO-MIL-31000</td>
      <td>Wonka Bar - Milk Chocolate</td>
      <td>6.5</td>
      <td>2</td>
      <td>4.22</td>
      <td>2.28</td>
      <td>Wonka Bar - Nutty Crunch Surprise</td>
      <td>Lot's O' Nuts</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>US-2021-103800-CHO-MIL-31000</td>
      <td>03-01-2024</td>
      <td>30-06-2026</td>
      <td>Standard Class</td>
      <td>103800</td>
      <td>United States</td>
      <td>Houston</td>
      <td>Texas</td>
      <td>77095</td>
      <td>Chocolate</td>
      <td>Interior</td>
      <td>CHO-MIL-31000</td>
      <td>Wonka Bar - Milk Chocolate</td>
      <td>6.5</td>
      <td>2</td>
      <td>4.22</td>
      <td>2.28</td>
      <td>Wonka Bar - Fudge Mallows</td>
      <td>Lot's O' Nuts</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1</td>
      <td>US-2021-103800-CHO-MIL-31000</td>
      <td>03-01-2024</td>
      <td>30-06-2026</td>
      <td>Standard Class</td>
      <td>103800</td>
      <td>United States</td>
      <td>Houston</td>
      <td>Texas</td>
      <td>77095</td>
      <td>Chocolate</td>
      <td>Interior</td>
      <td>CHO-MIL-31000</td>
      <td>Wonka Bar - Milk Chocolate</td>
      <td>6.5</td>
      <td>2</td>
      <td>4.22</td>
      <td>2.28</td>
      <td>Wonka Bar -Scrumdiddlyumptious</td>
      <td>Lot's O' Nuts</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1</td>
      <td>US-2021-103800-CHO-MIL-31000</td>
      <td>03-01-2024</td>
      <td>30-06-2026</td>
      <td>Standard Class</td>
      <td>103800</td>
      <td>United States</td>
      <td>Houston</td>
      <td>Texas</td>
      <td>77095</td>
      <td>Chocolate</td>
      <td>Interior</td>
      <td>CHO-MIL-31000</td>
      <td>Wonka Bar - Milk Chocolate</td>
      <td>6.5</td>
      <td>2</td>
      <td>4.22</td>
      <td>2.28</td>
      <td>Wonka Bar - Milk Chocolate</td>
      <td>Wicked Choccy's</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1</td>
      <td>US-2021-103800-CHO-MIL-31000</td>
      <td>03-01-2024</td>
      <td>30-06-2026</td>
      <td>Standard Class</td>
      <td>103800</td>
      <td>United States</td>
      <td>Houston</td>
      <td>Texas</td>
      <td>77095</td>
      <td>Chocolate</td>
      <td>Interior</td>
      <td>CHO-MIL-31000</td>
      <td>Wonka Bar - Milk Chocolate</td>
      <td>6.5</td>
      <td>2</td>
      <td>4.22</td>
      <td>2.28</td>
      <td>Wonka Bar - Triple Dazzle Caramel</td>
      <td>Wicked Choccy's</td>
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
    </tr>
    <tr>
      <th>50695</th>
      <td>10194</td>
      <td>CA-2024-143500-CHO-SCR-58000</td>
      <td>30-12-2025</td>
      <td>26-06-2030</td>
      <td>Standard Class</td>
      <td>143500</td>
      <td>Canada</td>
      <td>Charlottetown</td>
      <td>Prince Edward Island</td>
      <td>C0A</td>
      <td>Chocolate</td>
      <td>Atlantic</td>
      <td>CHO-SCR-58000</td>
      <td>Wonka Bar -Scrumdiddlyumptious</td>
      <td>10.8</td>
      <td>3</td>
      <td>7.50</td>
      <td>3.30</td>
      <td>Wonka Bar - Nutty Crunch Surprise</td>
      <td>Lot's O' Nuts</td>
    </tr>
    <tr>
      <th>50696</th>
      <td>10194</td>
      <td>CA-2024-143500-CHO-SCR-58000</td>
      <td>30-12-2025</td>
      <td>26-06-2030</td>
      <td>Standard Class</td>
      <td>143500</td>
      <td>Canada</td>
      <td>Charlottetown</td>
      <td>Prince Edward Island</td>
      <td>C0A</td>
      <td>Chocolate</td>
      <td>Atlantic</td>
      <td>CHO-SCR-58000</td>
      <td>Wonka Bar -Scrumdiddlyumptious</td>
      <td>10.8</td>
      <td>3</td>
      <td>7.50</td>
      <td>3.30</td>
      <td>Wonka Bar - Fudge Mallows</td>
      <td>Lot's O' Nuts</td>
    </tr>
    <tr>
      <th>50697</th>
      <td>10194</td>
      <td>CA-2024-143500-CHO-SCR-58000</td>
      <td>30-12-2025</td>
      <td>26-06-2030</td>
      <td>Standard Class</td>
      <td>143500</td>
      <td>Canada</td>
      <td>Charlottetown</td>
      <td>Prince Edward Island</td>
      <td>C0A</td>
      <td>Chocolate</td>
      <td>Atlantic</td>
      <td>CHO-SCR-58000</td>
      <td>Wonka Bar -Scrumdiddlyumptious</td>
      <td>10.8</td>
      <td>3</td>
      <td>7.50</td>
      <td>3.30</td>
      <td>Wonka Bar -Scrumdiddlyumptious</td>
      <td>Lot's O' Nuts</td>
    </tr>
    <tr>
      <th>50698</th>
      <td>10194</td>
      <td>CA-2024-143500-CHO-SCR-58000</td>
      <td>30-12-2025</td>
      <td>26-06-2030</td>
      <td>Standard Class</td>
      <td>143500</td>
      <td>Canada</td>
      <td>Charlottetown</td>
      <td>Prince Edward Island</td>
      <td>C0A</td>
      <td>Chocolate</td>
      <td>Atlantic</td>
      <td>CHO-SCR-58000</td>
      <td>Wonka Bar -Scrumdiddlyumptious</td>
      <td>10.8</td>
      <td>3</td>
      <td>7.50</td>
      <td>3.30</td>
      <td>Wonka Bar - Milk Chocolate</td>
      <td>Wicked Choccy's</td>
    </tr>
    <tr>
      <th>50699</th>
      <td>10194</td>
      <td>CA-2024-143500-CHO-SCR-58000</td>
      <td>30-12-2025</td>
      <td>26-06-2030</td>
      <td>Standard Class</td>
      <td>143500</td>
      <td>Canada</td>
      <td>Charlottetown</td>
      <td>Prince Edward Island</td>
      <td>C0A</td>
      <td>Chocolate</td>
      <td>Atlantic</td>
      <td>CHO-SCR-58000</td>
      <td>Wonka Bar -Scrumdiddlyumptious</td>
      <td>10.8</td>
      <td>3</td>
      <td>7.50</td>
      <td>3.30</td>
      <td>Wonka Bar - Triple Dazzle Caramel</td>
      <td>Wicked Choccy's</td>
    </tr>
  </tbody>
</table>
<p>50700 rows × 20 columns</p>
</div>




```python
## Factory Performance
factory_performance=df_merged.groupby('Factory')[['Sales','Gross Profit','Cost']].sum()
total_profit=df_merged['Gross Profit'].sum()
total_sales=df_merged['Sales'].sum()
factory_performance['Sales_%']=(factory_performance['Sales']/total_sales*100).round(2)
factory_performance['Profit_%']=(factory_performance['Gross Profit']/total_sales*100).round(2)
factory_performance['Gross Margin_%']=(factory_performance['Cost']/factory_performance['Sales']*100).round(2)
factory_performance
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
      <th>Sales</th>
      <th>Gross Profit</th>
      <th>Cost</th>
      <th>Sales_%</th>
      <th>Profit_%</th>
      <th>Gross Margin_%</th>
    </tr>
    <tr>
      <th>Factory</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Lot's O' Nuts</th>
      <td>395078.70</td>
      <td>266473.86</td>
      <td>128604.84</td>
      <td>56.47</td>
      <td>38.08</td>
      <td>32.55</td>
    </tr>
    <tr>
      <th>Secret Factory</th>
      <td>19753.98</td>
      <td>8951.63</td>
      <td>10802.35</td>
      <td>2.82</td>
      <td>1.28</td>
      <td>54.68</td>
    </tr>
    <tr>
      <th>Sugar Shack</th>
      <td>11373.17</td>
      <td>5472.37</td>
      <td>5900.80</td>
      <td>1.63</td>
      <td>0.78</td>
      <td>51.88</td>
    </tr>
    <tr>
      <th>The Other Factory</th>
      <td>10090.73</td>
      <td>4618.18</td>
      <td>5472.55</td>
      <td>1.44</td>
      <td>0.66</td>
      <td>54.23</td>
    </tr>
    <tr>
      <th>Wicked Choccy's</th>
      <td>263385.80</td>
      <td>177649.24</td>
      <td>85736.56</td>
      <td>37.64</td>
      <td>25.39</td>
      <td>32.55</td>
    </tr>
  </tbody>
</table>
</div>


