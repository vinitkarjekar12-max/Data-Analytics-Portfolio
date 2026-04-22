```python
## Import Libraries
import numpy as np
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt
```


```python
## Import Dataset
df=pd.read_csv(r"C:\Users\-----\Desktop\SkyCity Auckland Restraurant\SkyCity Auckland Restaurants & Bars (1).csv")
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
      <th>CuisineType</th>
      <th>RestaurantID</th>
      <th>RestaurantName</th>
      <th>Segment</th>
      <th>Subregion</th>
      <th>GrowthFactor</th>
      <th>AOV</th>
      <th>MonthlyOrders</th>
      <th>InStoreOrders</th>
      <th>InStoreRevenue</th>
      <th>...</th>
      <th>DeliveryCostPerOrder</th>
      <th>SD_DeliveryTotalCost</th>
      <th>InStoreNetProfit</th>
      <th>UberEatsNetProfit</th>
      <th>DoorDashNetProfit</th>
      <th>SelfDeliveryNetProfit</th>
      <th>InStoreShare</th>
      <th>UE_share</th>
      <th>DD_share</th>
      <th>SD_share</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Burgers</td>
      <td>25731</td>
      <td>Urban Burgers House</td>
      <td>Cafe</td>
      <td>North Shore</td>
      <td>1.03</td>
      <td>43.97</td>
      <td>668</td>
      <td>197</td>
      <td>8662.09</td>
      <td>...</td>
      <td>3.25</td>
      <td>458.25</td>
      <td>3682.14</td>
      <td>1352.45</td>
      <td>752.78</td>
      <td>2177.19</td>
      <td>0.42</td>
      <td>0.45</td>
      <td>0.25</td>
      <td>0.3</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Burgers</td>
      <td>25123</td>
      <td>Urban Burgers Diner</td>
      <td>QSR</td>
      <td>South Auckland</td>
      <td>1.05</td>
      <td>40.45</td>
      <td>1388</td>
      <td>259</td>
      <td>10476.55</td>
      <td>...</td>
      <td>4.72</td>
      <td>1600.08</td>
      <td>3605.72</td>
      <td>1318.61</td>
      <td>731.99</td>
      <td>3119.38</td>
      <td>0.23</td>
      <td>0.45</td>
      <td>0.25</td>
      <td>0.3</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Burgers</td>
      <td>25177</td>
      <td>King Burgers Eatery</td>
      <td>Cafe</td>
      <td>West Auckland</td>
      <td>1.04</td>
      <td>40.03</td>
      <td>1717</td>
      <td>524</td>
      <td>20975.72</td>
      <td>...</td>
      <td>3.25</td>
      <td>1163.50</td>
      <td>7810.95</td>
      <td>1555.90</td>
      <td>863.42</td>
      <td>4172.99</td>
      <td>0.44</td>
      <td>0.45</td>
      <td>0.25</td>
      <td>0.3</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Burgers</td>
      <td>25540</td>
      <td>Classic Burgers Tavern</td>
      <td>QSR</td>
      <td>North Shore</td>
      <td>1.03</td>
      <td>36.28</td>
      <td>1083</td>
      <td>216</td>
      <td>7836.48</td>
      <td>...</td>
      <td>0.89</td>
      <td>231.40</td>
      <td>2546.02</td>
      <td>-72.25</td>
      <td>-40.20</td>
      <td>2833.26</td>
      <td>0.25</td>
      <td>0.45</td>
      <td>0.25</td>
      <td>0.3</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Burgers</td>
      <td>25258</td>
      <td>Lucky Burgers Bistro</td>
      <td>Cafe</td>
      <td>South Auckland</td>
      <td>1.05</td>
      <td>34.34</td>
      <td>1230</td>
      <td>261</td>
      <td>8962.74</td>
      <td>...</td>
      <td>2.66</td>
      <td>774.06</td>
      <td>3093.09</td>
      <td>226.17</td>
      <td>125.53</td>
      <td>2674.56</td>
      <td>0.27</td>
      <td>0.45</td>
      <td>0.25</td>
      <td>0.3</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 30 columns</p>
</div>




```python
df['CommissionRate']
```




    0       0.28
    1       0.28
    2       0.30
    3       0.33
    4       0.33
            ... 
    1691    0.30
    1692    0.30
    1693    0.32
    1694    0.28
    1695    0.28
    Name: CommissionRate, Length: 1696, dtype: float64


Problem Statement
Despite having access to detailed cost and profit data, restaurant operators often lack:

• A side-by-side comparison of channel profitability
• Visibility into commission drag vs delivery cost
• Understanding of which channels erode margins despite high revenue
• Evidence to guide channel prioritization or renegotiation strategies

```python
# A side-by-side comparison of channel profitability
# All channels net profit totals
InStoreNetProfit_Total=df['InStoreNetProfit'].sum()
UberEatsNetProfit_Total=df['UberEatsNetProfit'].sum().round(2)
DoorDashNetProfit_Total=df['DoorDashNetProfit'].sum()
SelfDeliveryNetProfit_Total=df['SelfDeliveryNetProfit'].sum().round(2)

# Combined all channels net profit overall total
Total_NetProfit=df[['InStoreNetProfit','UberEatsNetProfit','DoorDashNetProfit','SelfDeliveryNetProfit']].sum().sum()

# Calculation of net profit contribution
InStore_Profit_Contribution = (InStoreNetProfit_Total/Total_NetProfit) * 100
DoorDash_Profit_Contribution = (DoorDashNetProfit_Total/Total_NetProfit) * 100
SelfDelivery_Profit_Contribution = (SelfDeliveryNetProfit_Total/Total_NetProfit) * 100
UberEats_Profit_Contribution = (UberEatsNetProfit_Total/Total_NetProfit) * 100

# Print the total profit amount 
print("InStore Net Profit : ",InStoreNetProfit_Total)
print("Uber Eats Net Profit : ",UberEatsNetProfit_Total)
print("Door Dash Net Profit : ",DoorDashNetProfit_Total)
print("Self Delivery Net Profit : ",SelfDeliveryNetProfit_Total)

# Sequence of channels and net profit
net_profitability= pd.DataFrame({ 'Channel': ['In Store','Uber Eats','Door Dash','Self Delivery'],
                                 'Net Profit':[InStoreNetProfit_Total,UberEatsNetProfit_Total,DoorDashNetProfit_Total,SelfDeliveryNetProfit_Total],
                                 'Profit Contribution' : [InStore_Profit_Contribution,DoorDash_Profit_Contribution,
                                                          SelfDelivery_Profit_Contribution,UberEats_Profit_Contribution]
                                })
net_profitability
```

    InStore Net Profit :  3828417.36
    Uber Eats Net Profit :  258488.08
    Door Dash Net Profit :  151122.25
    Self Delivery Net Profit :  3628278.44
    




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
      <th>Channel</th>
      <th>Net Profit</th>
      <th>Profit Contribution</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>In Store</td>
      <td>3828417.36</td>
      <td>48.668553</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Uber Eats</td>
      <td>258488.08</td>
      <td>1.921134</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Door Dash</td>
      <td>151122.25</td>
      <td>46.124297</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Self Delivery</td>
      <td>3628278.44</td>
      <td>3.286016</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.columns
```




    Index(['CuisineType', 'RestaurantID', 'RestaurantName', 'Segment', 'Subregion',
           'GrowthFactor', 'AOV', 'MonthlyOrders', 'InStoreOrders',
           'InStoreRevenue', 'UberEatsOrders', 'DoorDashOrders',
           'SelfDeliveryOrders', 'UberEatsRevenue', 'DoorDashRevenue',
           'SelfDeliveryRevenue', 'COGSRate', 'OPEXRate', 'CommissionRate',
           'DeliveryRadiusKM', 'DeliveryCostPerOrder', 'SD_DeliveryTotalCost',
           'InStoreNetProfit', 'UberEatsNetProfit', 'DoorDashNetProfit',
           'SelfDeliveryNetProfit', 'InStoreShare', 'UE_share', 'DD_share',
           'SD_share'],
          dtype='object')




```python
# Understanding of which channels erode margins despite high revenue
margin_calculate=df[['InStoreRevenue','UberEatsRevenue','DoorDashRevenue','SelfDeliveryRevenue','InStoreNetProfit', 'UberEatsNetProfit', 
                     'DoorDashNetProfit','SelfDeliveryNetProfit']].sum()

# Calculate Total Revenue and Net Profit from all 4 channels
total_revenue=df[['InStoreRevenue','UberEatsRevenue','DoorDashRevenue','SelfDeliveryRevenue']].sum().sum()
total_NetProfit=df[['InStoreNetProfit','UberEatsNetProfit','DoorDashNetProfit','SelfDeliveryNetProfit']].sum().sum()

# Calculating channelwise data
result = pd.DataFrame({'Channel' : ['InStore','Uber Eats','Door Dash','Self Delivery'],
                       'Revenue': [
                           margin_calculate['InStoreRevenue'], 
                           margin_calculate['UberEatsRevenue'],
                           margin_calculate['DoorDashRevenue'],
                           margin_calculate['SelfDeliveryRevenue']],
                        'Net Profit':[
                           margin_calculate['InStoreNetProfit'], 
                           margin_calculate['UberEatsNetProfit'],
                           margin_calculate['DoorDashNetProfit'],
                           margin_calculate['SelfDeliveryNetProfit']]})
result['Profit_Margin_%']=((result['Net Profit']/result['Revenue'])*100).round(2)
result['Revenue Contribution']=((result['Revenue']/total_revenue)*100).round(2)
result['Profit Contribution']=((result['Net Profit']/total_NetProfit)*100).round(2)
result
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
      <th>Channel</th>
      <th>Revenue</th>
      <th>Net Profit</th>
      <th>Profit_Margin_%</th>
      <th>Revenue Contribution</th>
      <th>Profit Contribution</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>InStore</td>
      <td>14284378.07</td>
      <td>3828417.36</td>
      <td>26.80</td>
      <td>18.37</td>
      <td>48.67</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Uber Eats</td>
      <td>30816371.49</td>
      <td>258488.08</td>
      <td>0.84</td>
      <td>39.64</td>
      <td>3.29</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Door Dash</td>
      <td>16789380.95</td>
      <td>151122.25</td>
      <td>0.90</td>
      <td>21.60</td>
      <td>1.92</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Self Delivery</td>
      <td>15849176.29</td>
      <td>3628278.44</td>
      <td>22.89</td>
      <td>20.39</td>
      <td>46.12</td>
    </tr>
  </tbody>
</table>
</div>


# UberEats and DoorDash are majorly damaging compamy's eco-system with earning 0.84 and 0.90 profit margin respectively.
# UberEats and DoorDash are combinely contributing 61.12% in total revenue but combine profit contrinution is only 5.21%• Evidence to guide channel prioritization or renegotiation strategies
# As per analysis, company should focus more on profit driven channels i.e. Instore and Self Delivery which are combinely contributing 94.79% overall company's profitPrimary Objectives
• Compare net profitability across In-Store, Uber Eats, DoorDash, and Self-Delivery
• Quantify margin erosion due to commissions and delivery costs
• Identify the most cost-efficient channel per restaurant type

```python
# Quantify margin erosion due to commissions and delivery costs

df['Commission Amount']=df['UberEatsRevenue']*df['CommissionRate']   # Actual commission amount of Uber Eats
total_commission=df['Commission Amount'].sum().round(2)   # Total commission amount of Uber Eats

delivery_cost=df['SD_DeliveryTotalCost'].sum()   # Total delivery cost

total_revenue=df[['InStoreRevenue','UberEatsRevenue','DoorDashRevenue','SelfDeliveryRevenue']].sum().sum()    # All chanels revenue

# Commission impact
commission_impact = ((total_commission/total_revenue)*100).round(2)
delivery_impact = ((delivery_cost/total_revenue)*100).round(2)

## Print statement
print("Total Commission Amount : ",total_commission)
print("Total Delivery Cost : ",delivery_cost)
print("Commission Impact : ",commission_impact)
print("Delivery Charges Impact : ",delivery_impact)
```

    Total Commission Amount :  9253981.25
    Total Delivery Cost :  1281809.47
    Commission Impact :  11.9
    Delivery Charges Impact :  1.65
    


```python
# Impack of Commission and Delivery on revenue
erosion_df=pd.DataFrame({ 'Metric':['Commission','Delivery'],
                         'Amount' :[total_commission,delivery_cost],
                         'Impact on Revenue':[commission_impact,delivery_impact]
                        })
erosion_df
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
      <th>Metric</th>
      <th>Amount</th>
      <th>Impact on Revenue</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Commission</td>
      <td>9253981.25</td>
      <td>11.90</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Delivery</td>
      <td>1281809.47</td>
      <td>1.65</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Identify the most cost-efficient channel per restaurant type
channel_group=df.groupby('Segment').sum(numeric_only=True)

# Margin calculations
channel_group['DoorDash_Margin']=(channel_group['DoorDashNetProfit']/channel_group['DoorDashRevenue'])*100
channel_group['InStore_Margin']=(channel_group['InStoreNetProfit']/channel_group['InStoreRevenue'])*100
channel_group['UberEats_Margin']=(channel_group['UberEatsNetProfit']/channel_group['UberEatsRevenue'])*100
channel_group['SelfDelivery_Margin']=(channel_group['SelfDeliveryNetProfit']/channel_group['SelfDeliveryRevenue'])*100

all_combined=channel_group[['DoorDash_Margin','InStore_Margin','UberEats_Margin','SelfDelivery_Margin']].reset_index()
all_combined
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
      <th>Segment</th>
      <th>DoorDash_Margin</th>
      <th>InStore_Margin</th>
      <th>UberEats_Margin</th>
      <th>SelfDelivery_Margin</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Cafe</td>
      <td>6.119366</td>
      <td>36.304756</td>
      <td>6.091435</td>
      <td>28.359178</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Full-service</td>
      <td>-17.458836</td>
      <td>12.414319</td>
      <td>-17.464645</td>
      <td>4.079558</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Ghost Kitchen</td>
      <td>15.123940</td>
      <td>45.252319</td>
      <td>15.102434</td>
      <td>37.018862</td>
    </tr>
    <tr>
      <th>3</th>
      <td>QSR</td>
      <td>5.848353</td>
      <td>35.984436</td>
      <td>5.847859</td>
      <td>28.098293</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Segment average
segment_avg=df.groupby('Segment')[['DoorDashRevenue','InStoreRevenue','UberEatsRevenue','SelfDeliveryRevenue']].mean().round(1)
segment_avg
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
      <th>DoorDashRevenue</th>
      <th>InStoreRevenue</th>
      <th>UberEatsRevenue</th>
      <th>SelfDeliveryRevenue</th>
    </tr>
    <tr>
      <th>Segment</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Cafe</th>
      <td>9963.2</td>
      <td>8612.3</td>
      <td>18268.2</td>
      <td>9282.4</td>
    </tr>
    <tr>
      <th>Full-service</th>
      <td>9768.9</td>
      <td>12877.8</td>
      <td>18047.4</td>
      <td>9283.5</td>
    </tr>
    <tr>
      <th>Ghost Kitchen</th>
      <td>10110.5</td>
      <td>2537.1</td>
      <td>18411.4</td>
      <td>9706.7</td>
    </tr>
    <tr>
      <th>QSR</th>
      <td>9872.3</td>
      <td>6672.6</td>
      <td>18093.4</td>
      <td>9323.2</td>
    </tr>
  </tbody>
</table>
</div>


# All InStore and SelfDelivery channels are profitable.
# Full-service segment having negative profit margin in DoorDash and UberEats channels, except this all channels are profitable in all segments.
# Need to prioratize Full-service segment for auditing errors and margins to come to break even from negative
# Ghost Kitchen is having positive and healthy profit margin in all channels, needs to focus more skus to increase sales and acquire new consumers
# Cafe and QSR is having low net profit margin with UberEats and DoorDash which needs to stretch at least 10-12% by optimizing pricing
# Need to focus on increasing revenue for Ghost Kitchen InStore performance as average monthly orders are performing very bad
# All segments of UberEats is having best revenue performance but nothing is earning from UberEats which needs to come at break-out
either reprice all sku in UberEats or send promotional coupon with all UberEats orders to promote online orders shifts to InStore or SelfDelivery orders which can lead to save money in commissions and give more discount to InStore and SelfDelivery orders
# InStore orders in Full-service segment is giving good performance so it needs to promote more ad campaigns to increase Full-service segment orders Primary Objectives
• Compare net profitability across In-Store, Uber Eats, DoorDash, and Self-Delivery
• Quantify margin erosion due to commissions and delivery costs
• Identify the most cost-efficient channel per restaurant type

```python
# Compare net profitability across In-Store, Uber Eats, DoorDash, and Self-Delivery
# A side-by-side comparison of channel profitability
# All channels net profit totals
InStoreNetProfit_Total=df['InStoreNetProfit'].sum()
UberEatsNetProfit_Total=df['UberEatsNetProfit'].sum().round(2)
DoorDashNetProfit_Total=df['DoorDashNetProfit'].sum()
SelfDeliveryNetProfit_Total=df['SelfDeliveryNetProfit'].sum().round(2)

# Combined all channels net profit overall total
Total_NetProfit=df[['InStoreNetProfit','UberEatsNetProfit','DoorDashNetProfit','SelfDeliveryNetProfit']].sum().sum().round(2)

# Calculation of net profit contribution
InStore_Profit_Contribution = ((InStoreNetProfit_Total/Total_NetProfit) * 100).round(2)
DoorDash_Profit_Contribution = ((DoorDashNetProfit_Total/Total_NetProfit) * 100).round(2)
SelfDelivery_Profit_Contribution = ((SelfDeliveryNetProfit_Total/Total_NetProfit) * 100).round(2)
UberEats_Profit_Contribution = ((UberEatsNetProfit_Total/Total_NetProfit) * 100).round(2)

# Print the total profit amount 
print("InStore Net Profit : ",InStoreNetProfit_Total)
print("Uber Eats Net Profit : ",UberEatsNetProfit_Total)
print("Door Dash Net Profit : ",DoorDashNetProfit_Total)
print("Self Delivery Net Profit : ",SelfDeliveryNetProfit_Total)

# Sequence of channels and net profit
net_profitability= pd.DataFrame({ 'Channel': ['In Store','Uber Eats','Door Dash','Self Delivery'],
                                 'Net Profit':[InStoreNetProfit_Total,UberEatsNetProfit_Total,DoorDashNetProfit_Total,SelfDeliveryNetProfit_Total],
                                 'Profit Contribution' : [InStore_Profit_Contribution,UberEats_Profit_Contribution,DoorDash_Profit_Contribution,
                                                          SelfDelivery_Profit_Contribution]
                                })
net_profitability
```

    InStore Net Profit :  3828417.36
    Uber Eats Net Profit :  258488.08
    Door Dash Net Profit :  151122.25
    Self Delivery Net Profit :  3628278.44
    




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
      <th>Channel</th>
      <th>Net Profit</th>
      <th>Profit Contribution</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>In Store</td>
      <td>3828417.36</td>
      <td>48.67</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Uber Eats</td>
      <td>258488.08</td>
      <td>3.29</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Door Dash</td>
      <td>151122.25</td>
      <td>1.92</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Self Delivery</td>
      <td>3628278.44</td>
      <td>46.12</td>
    </tr>
  </tbody>
</table>
</div>


Secondary Objectives
• Support data-driven channel prioritization
• Provide financial evidence for aggregator negotiations
• Highlight self-delivery ROI thresholds

```python
# Support data-driven channel prioritization

Channels= ['InStore','UberEats','DoorDash','SelfDelivery']
# Total orders, revenue and net profit channel wise
InStore_Total=df[['InStoreOrders','InStoreRevenue','InStoreNetProfit']].sum().round()
UberEats_Total=df[['UberEatsOrders','UberEatsRevenue','UberEatsNetProfit']].sum().round()
DoorDash_Total=df[['DoorDashOrders','DoorDashRevenue','DoorDashNetProfit']].sum().round()
SelfDelivery_Total=df[['SelfDeliveryOrders','SelfDeliveryRevenue','SelfDeliveryNetProfit']].sum().round()

# Segment Cost
InStoreCost=InStore_Total['InStoreRevenue']-InStore_Total['InStoreNetProfit']
UberEatsCost=UberEats_Total['UberEatsRevenue']-UberEats_Total['UberEatsNetProfit']
DoorDashCost=DoorDash_Total['DoorDashRevenue']-DoorDash_Total['DoorDashNetProfit']
SelfDeliveryCost=SelfDelivery_Total['SelfDeliveryRevenue']-SelfDelivery_Total['SelfDeliveryNetProfit']

All_total=pd.DataFrame({'Channels': Channels, 
                        'Orders' : [InStore_Total['InStoreOrders'],UberEats_Total['UberEatsOrders'],
                        DoorDash_Total['DoorDashOrders'],SelfDelivery_Total['SelfDeliveryOrders']],
                         'Cost' : [InStoreCost,UberEatsCost,DoorDashCost,SelfDeliveryCost],
                        'Revenue' : [InStore_Total['InStoreRevenue'],UberEats_Total['UberEatsRevenue'],
                        DoorDash_Total['DoorDashRevenue'],SelfDelivery_Total['SelfDeliveryRevenue']],
                        'Net Profit' : [InStore_Total['InStoreNetProfit'],UberEats_Total['UberEatsNetProfit'],
                        DoorDash_Total['DoorDashNetProfit'],SelfDelivery_Total['SelfDeliveryNetProfit']]
                       })
All_total
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
      <th>Channels</th>
      <th>Orders</th>
      <th>Cost</th>
      <th>Revenue</th>
      <th>Net Profit</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>InStore</td>
      <td>371391.0</td>
      <td>10455961.0</td>
      <td>14284378.0</td>
      <td>3828417.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>UberEats</td>
      <td>800353.0</td>
      <td>30557883.0</td>
      <td>30816371.0</td>
      <td>258488.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>DoorDash</td>
      <td>436135.0</td>
      <td>16638259.0</td>
      <td>16789381.0</td>
      <td>151122.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>SelfDelivery</td>
      <td>411255.0</td>
      <td>12220898.0</td>
      <td>15849176.0</td>
      <td>3628278.0</td>
    </tr>
  </tbody>
</table>
</div>


• Support data-driven channel prioritization
--> As per data In-Store and Self-Delivery is the prirotize channel for net profit and UberEats and DoorDash have strong online presence that will work for advertising purpose to reach new customers and introduce inventory to customer and showcase your offers and offline presence through these 2 platforms 

• Provide financial evidence for aggregator negotiations
--> Uber Eats and DoorDash revenue combinely contributing near to 61% of total revenue with but profit contribution is only near to 6% which is a clear red flag for company to make a bold decision on these 2 platforms or ne 

• Highlight self-delivery ROI thresholds

```python
df.columns
```




    Index(['CuisineType', 'RestaurantID', 'RestaurantName', 'Segment', 'Subregion',
           'GrowthFactor', 'AOV', 'MonthlyOrders', 'InStoreOrders',
           'InStoreRevenue', 'UberEatsOrders', 'DoorDashOrders',
           'SelfDeliveryOrders', 'UberEatsRevenue', 'DoorDashRevenue',
           'SelfDeliveryRevenue', 'COGSRate', 'OPEXRate', 'CommissionRate',
           'DeliveryRadiusKM', 'DeliveryCostPerOrder', 'SD_DeliveryTotalCost',
           'InStoreNetProfit', 'UberEatsNetProfit', 'DoorDashNetProfit',
           'SelfDeliveryNetProfit', 'InStoreShare', 'UE_share', 'DD_share',
           'SD_share', 'Commission Amount'],
          dtype='object')




```python
# Highlight self-delivery ROI thresholds
roi_threshold=df.groupby('RestaurantName')[['SelfDeliveryNetProfit','SD_DeliveryTotalCost']].sum().round(2)
roi_threshold.sort_values(by='SelfDeliveryNetProfit', ascending=False)

roi_threshold['SD_ROI']=(roi_threshold['SelfDeliveryNetProfit']/roi_threshold['SD_DeliveryTotalCost']).round(2)

# IF-elif-else statement
def roi_category (x) :
    if x < 0:
        return "Loss"
    elif x < 2:
        return "Low ROI"
    elif x < 4:
        return "Moderate ROI"
    else :
        return "High ROI"

# Apply category to threshold
roi_threshold['ROI_Category_Status']=roi_threshold['SD_ROI'].apply(roi_category)
high_ROI_line=roi_threshold[roi_threshold['ROI_Category_Status']=='High ROI']


sd_netprofit_total=roi_threshold['SelfDeliveryNetProfit'].sum().round(2)
ROI_Contribution_Restraurents=roi_threshold.groupby('ROI_Category_Status')['SelfDeliveryNetProfit'].sum().reset_index()
ROI_Contribution_Restraurents['ROI_Contrinution']=((ROI_Contribution_Restraurents['SelfDeliveryNetProfit']/sd_netprofit_total)*100).round(2)
ROI_Contribution_Restraurents
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
      <th>ROI_Category_Status</th>
      <th>SelfDeliveryNetProfit</th>
      <th>ROI_Contrinution</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>High ROI</td>
      <td>486554.18</td>
      <td>13.41</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Loss</td>
      <td>-361.74</td>
      <td>-0.01</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Low ROI</td>
      <td>307584.92</td>
      <td>8.48</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Moderate ROI</td>
      <td>2834501.08</td>
      <td>78.12</td>
    </tr>
  </tbody>
</table>
</div>


# Moderate ROI category restaurants are contributing 78% and High ROI is contributing 13.41%
# High ROI restaurants have premium pricing but limited buyers in other side Moderate ROI restaurants have more buyers and ROI between 2-4

```python
roi_threshold['ROI_Category_Status']=roi_threshold['SD_ROI'].apply(roi_category)
roi_threshold
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
      <th>SelfDeliveryNetProfit</th>
      <th>SD_DeliveryTotalCost</th>
      <th>SD_ROI</th>
      <th>ROI_Category_Status</th>
    </tr>
    <tr>
      <th>RestaurantName</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Bombay Bistro</th>
      <td>2703.48</td>
      <td>2901.00</td>
      <td>0.93</td>
      <td>Low ROI</td>
    </tr>
    <tr>
      <th>Bombay Cafe</th>
      <td>9023.48</td>
      <td>4853.72</td>
      <td>1.86</td>
      <td>Low ROI</td>
    </tr>
    <tr>
      <th>Bombay Corner</th>
      <td>17519.71</td>
      <td>6123.77</td>
      <td>2.86</td>
      <td>Moderate ROI</td>
    </tr>
    <tr>
      <th>Bombay Diner</th>
      <td>17766.54</td>
      <td>7127.63</td>
      <td>2.49</td>
      <td>Moderate ROI</td>
    </tr>
    <tr>
      <th>Bombay Eatery</th>
      <td>15034.71</td>
      <td>3133.09</td>
      <td>4.80</td>
      <td>High ROI</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>Urban Pizza Eatery</th>
      <td>18125.86</td>
      <td>2926.45</td>
      <td>6.19</td>
      <td>High ROI</td>
    </tr>
    <tr>
      <th>Urban Pizza Grill</th>
      <td>36584.09</td>
      <td>10424.02</td>
      <td>3.51</td>
      <td>Moderate ROI</td>
    </tr>
    <tr>
      <th>Urban Pizza House</th>
      <td>30769.79</td>
      <td>9788.88</td>
      <td>3.14</td>
      <td>Moderate ROI</td>
    </tr>
    <tr>
      <th>Urban Pizza Kitchen</th>
      <td>27235.24</td>
      <td>9871.83</td>
      <td>2.76</td>
      <td>Moderate ROI</td>
    </tr>
    <tr>
      <th>Urban Pizza Tavern</th>
      <td>17907.76</td>
      <td>6448.76</td>
      <td>2.78</td>
      <td>Moderate ROI</td>
    </tr>
  </tbody>
</table>
<p>256 rows × 4 columns</p>
</div>




```python
high_ROI_line=roi_threshold[roi_threshold['ROI_Category_Status']=='High ROI']
high_ROI_line.head(10)
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
      <th>SelfDeliveryNetProfit</th>
      <th>SD_DeliveryTotalCost</th>
      <th>SD_ROI</th>
      <th>ROI_Category_Status</th>
    </tr>
    <tr>
      <th>RestaurantName</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Bombay Eatery</th>
      <td>15034.71</td>
      <td>3133.09</td>
      <td>4.80</td>
      <td>High ROI</td>
    </tr>
    <tr>
      <th>Classic Chicken Dishes Cafe</th>
      <td>8821.99</td>
      <td>2101.33</td>
      <td>4.20</td>
      <td>High ROI</td>
    </tr>
    <tr>
      <th>Classic Pizza Corner</th>
      <td>19736.65</td>
      <td>3394.56</td>
      <td>5.81</td>
      <td>High ROI</td>
    </tr>
    <tr>
      <th>Curry Diner</th>
      <td>15654.11</td>
      <td>3859.88</td>
      <td>4.06</td>
      <td>High ROI</td>
    </tr>
    <tr>
      <th>Dragon Diner</th>
      <td>14272.51</td>
      <td>3239.95</td>
      <td>4.41</td>
      <td>High ROI</td>
    </tr>
    <tr>
      <th>Dragon Tavern</th>
      <td>16667.07</td>
      <td>3220.99</td>
      <td>5.17</td>
      <td>High ROI</td>
    </tr>
    <tr>
      <th>Greek Kitchen</th>
      <td>5802.29</td>
      <td>1104.67</td>
      <td>5.25</td>
      <td>High ROI</td>
    </tr>
    <tr>
      <th>King Burgers Kitchen</th>
      <td>12817.47</td>
      <td>2622.14</td>
      <td>4.89</td>
      <td>High ROI</td>
    </tr>
    <tr>
      <th>King Pizza Bistro</th>
      <td>21708.53</td>
      <td>4117.48</td>
      <td>5.27</td>
      <td>High ROI</td>
    </tr>
    <tr>
      <th>King Pizza Eatery</th>
      <td>30318.45</td>
      <td>6907.51</td>
      <td>4.39</td>
      <td>High ROI</td>
    </tr>
  </tbody>
</table>
</div>


# Overall observations is showing 'Moderate ROI' (ROI < 4) is contributing 78.12% in Self Delivery Net Profit

```python
# Uber Eats and Door Dash channels revenue
revenue_total=df['UberEatsRevenue'].sum()+df['DoorDashRevenue'].sum().round(2)

# Uber Eats and Door Dash channels orders
orders_total=df['UberEatsOrders'].sum()+df['DoorDashOrders'].sum()

# Uber Eats and Door Dash commissions
uber_commission=(df['UberEatsRevenue']*df['CommissionRate']).sum().round(2)
doordash_commission=(df['DoorDashRevenue']*df['CommissionRate']).sum().round(2)

# Print statements
print("Combined Revenue of UberEats & DoorDash :",revenue_total)
print("Combined Orders of UberEats & DoorDash :",orders_total)
print("Uber Eats Commission Paid :",uber_commission)
print("Door Dash Commission Paid :",doordash_commission)

```

    Combined Revenue of UberEats & DoorDash : 47605752.44
    Combined Orders of UberEats & DoorDash : 1236488
    Uber Eats Commission Paid : 9253981.25
    Door Dash Commission Paid : 5040940.77
    


```python
df['CommissionRate'].unique()
```




    array([0.28, 0.3 , 0.33, 0.29, 0.31, 0.27, 0.32])




```python
# Commision amount calculations
df['uber_commission']=df['UberEatsRevenue']*df['CommissionRate']
df['doordash_commission']=df['DoorDashRevenue']*df['CommissionRate']

# New Uber Eats ana Door Dash commission calculations
df['new_uber_commission']=df['UberEatsRevenue']*(df['CommissionRate']-0.05)
df['new_doordash_commission']=df['DoorDashRevenue']*(df['CommissionRate']-0.05)
df['Total_Commission']=df['uber_commission']+df['doordash_commission']

#Combined total of commissions
commission_total=(df['uber_commission'].sum()+df['doordash_commission'].sum()).round(2)


CommissionRate_diff=df.groupby('CommissionRate')[['uber_commission','doordash_commission','Total_Commission','new_uber_commission','new_doordash_commission']].sum().round(2)
CommissionRate_diff['Commission_Percent']=((CommissionRate_diff['Total_Commission']/commission_total)*100).round(2)
CommissionRate_diff=CommissionRate_diff.reset_index()
CommissionRate_diff['New Commission Rate']=CommissionRate_diff['CommissionRate'] - 0.05
CommissionRate_diff
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
      <th>CommissionRate</th>
      <th>uber_commission</th>
      <th>doordash_commission</th>
      <th>Total_Commission</th>
      <th>new_uber_commission</th>
      <th>new_doordash_commission</th>
      <th>Commission_Percent</th>
      <th>New Commission Rate</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0.27</td>
      <td>772033.57</td>
      <td>423689.03</td>
      <td>1195722.59</td>
      <td>629064.39</td>
      <td>345228.10</td>
      <td>8.36</td>
      <td>0.22</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0.28</td>
      <td>1415282.21</td>
      <td>773521.27</td>
      <td>2188803.48</td>
      <td>1162553.25</td>
      <td>635392.47</td>
      <td>15.31</td>
      <td>0.23</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0.29</td>
      <td>1259686.48</td>
      <td>686514.97</td>
      <td>1946201.45</td>
      <td>1042499.15</td>
      <td>568150.32</td>
      <td>13.61</td>
      <td>0.24</td>
    </tr>
    <tr>
      <th>3</th>
      <td>0.30</td>
      <td>1508787.80</td>
      <td>818668.41</td>
      <td>2327456.21</td>
      <td>1257323.17</td>
      <td>682223.68</td>
      <td>16.28</td>
      <td>0.25</td>
    </tr>
    <tr>
      <th>4</th>
      <td>0.31</td>
      <td>1768465.83</td>
      <td>963494.25</td>
      <td>2731960.08</td>
      <td>1483229.41</td>
      <td>808091.95</td>
      <td>19.11</td>
      <td>0.26</td>
    </tr>
    <tr>
      <th>5</th>
      <td>0.32</td>
      <td>1676996.86</td>
      <td>913713.61</td>
      <td>2590710.47</td>
      <td>1414966.10</td>
      <td>770945.86</td>
      <td>18.12</td>
      <td>0.27</td>
    </tr>
    <tr>
      <th>6</th>
      <td>0.33</td>
      <td>852728.50</td>
      <td>461339.23</td>
      <td>1314067.73</td>
      <td>723527.21</td>
      <td>391439.34</td>
      <td>9.19</td>
      <td>0.28</td>
    </tr>
  </tbody>
</table>
</div>


# Commission rate of 30% and above bracket are taking commissions over 62% which is clearly indicating these 2 platforms are heavily impacting on company's profit margin.
# Big Red flag over commission rates and on immediate basis company need to negotiate over commission rates to drop 10%
# If successful negotiation happens then net profit 

```python
# New commission rates
df['New Commission Rates']=df['CommissionRate']-0.05

# Commision amount calculations
df['uber_commission']=df['UberEatsRevenue']*df['CommissionRate']
df['doordash_commission']=df['DoorDashRevenue']*df['CommissionRate']
df['Revised_UberEats_Commission']=(df['UberEatsRevenue']*df['New Commission Rates']).round(2)
df['Revised_DoorDash_Commission']=(df['DoorDashRevenue']*df['New Commission Rates']).round(2)
df['Revised_Commission']=(df['Revised_UberEats_Commission']+df['Revised_DoorDash_Commission']).round(2)

# Old Net profit for UberEats and DoorDash
uber_eats_net_profit=df['UberEatsNetProfit'].sum().round(2)
door_dash_net_profit=df['DoorDashNetProfit'].sum().round(2)
combined_net_profit=uber_eats_net_profit+door_dash_net_profit

# Uber Eats old, revised commissions and difference
ubereats_total_commission=df['uber_commission'].sum().round(2)
ubereats_revised_commission=df['Revised_UberEats_Commission'].sum().round(2)
ubereats_commission_difference=ubereats_total_commission-ubereats_revised_commission

# Door Dash old, revised commissions and difference
doordash_total_commission=df['doordash_commission'].sum().round(2)
doordash_revised_commission=df['Revised_DoorDash_Commission'].sum().round(2)
doordash_commission_difference=(doordash_total_commission-doordash_revised_commission).round(2)

# Difference between old and new revised net profits
uber_eats_revised_net_profit= (uber_eats_net_profit+ubereats_commission_difference).round(2)
door_dash_revised_net_profit= door_dash_net_profit+doordash_commission_difference
total_revised_net_profit=combined_net_profit+ubereats_commission_difference+doordash_commission_difference

# Print Statements
print("Uber Eats Total Commission Paid :",ubereats_total_commission)
print("Uber Eats Revised Commission Should be Paid :",ubereats_revised_commission)
print("Differe Between Old & New Commission is :",(ubereats_commission_difference).round(2))
print("Door Dash Total Commission Paid :",doordash_total_commission)
print("Door Dash Revised Commission Should be Paid :",doordash_revised_commission)
print("Differe Between Old & New Commission is :",doordash_commission_difference)
print("Uber Eats Actual Net Profit :",uber_eats_net_profit)
print("Door Dash Actual Net Profit :",door_dash_net_profit)
print("Uber Eats Net Profit After Revised Commission :",uber_eats_revised_net_profit)
print("Door Dash Net Profit After Revised Commission :",door_dash_revised_net_profit)
print("Total Combined Net Profit Contribution From Both Platforms :",(total_revised_net_profit).round(2))
```

    Uber Eats Total Commission Paid : 9253981.25
    Uber Eats Revised Commission Should be Paid : 7713162.77
    Differe Between Old & New Commission is : 1540818.48
    Door Dash Total Commission Paid : 5040940.77
    Door Dash Revised Commission Should be Paid : 4201471.72
    Differe Between Old & New Commission is : 839469.05
    Uber Eats Actual Net Profit : 258488.08
    Door Dash Actual Net Profit : 151122.25
    Uber Eats Net Profit After Revised Commission : 1799306.56
    Door Dash Net Profit After Revised Commission : 990591.3
    Total Combined Net Profit Contribution From Both Platforms : 2789897.86
    


```python
# New commission rate calculations
df['New Commission Rates']=df['CommissionRate']-0.03

# Old commission rates
df['uber_commission']=df['UberEatsRevenue']*df['CommissionRate']
df['doordash_commission']=df['DoorDashRevenue']*df['CommissionRate']

# Apply new commission rates
df['Revised_UberEats_Commission']=(df['UberEatsRevenue']*df['New Commission Rates']).round(2)
df['Revised_DoorDash_Commission']=(df['DoorDashRevenue']*df['New Commission Rates']).round(2)

# Revised net profit for UberEats and DoorDash
df['UberEats_Revised_Net_Profit']=((df['uber_commission']-df['Revised_UberEats_Commission'])+df['UberEatsNetProfit']).round(2)
df['DoorDash_Revised_Net_Profit']=((df['doordash_commission']-df['Revised_DoorDash_Commission'])+df['DoorDashNetProfit']).round(2)

# Net profit columns
df[['UberEatsNetProfit','UberEats_Revised_Net_Profit','DoorDashNetProfit','DoorDash_Revised_Net_Profit']]

# Channels wise revised net profit calculations
Uber_Eats_Net_Profit=df['UberEats_Revised_Net_Profit'].sum().round(2)
DoorDash_Net_Profit=df['DoorDash_Revised_Net_Profit'].sum().round(2)
In_Store_Net_Profit=df['InStoreNetProfit'].sum().round(2)
Self_Delivery_Net_Profit=df['SelfDeliveryNetProfit'].sum().round(2)

# Overall combine net profit 
Total_NetProfit=(Uber_Eats_Net_Profit+DoorDash_Net_Profit+In_Store_Net_Profit+Self_Delivery_Net_Profit)

# Revised net profit contributions 
Uber_Eats_Net_Profit_Contribution=((Uber_Eats_Net_Profit/Total_NetProfit)*100).round(2)
DoorDash_Net_Profit_Contribution=((DoorDash_Net_Profit/Total_NetProfit)*100).round(2)
In_Store_Net_Profit_Contribution=((In_Store_Net_Profit/Total_NetProfit)*100).round(2)
Self_Delivery_Net_Profit_Contribution=((Self_Delivery_Net_Profit/Total_NetProfit)*100).round(2)

# New revised net profit and contribution
new_net_profit=pd.DataFrame({'Channel': ['InStore','Self Delivery','Uber Eats','Door Dash'],
                             'Net Profit':
                             [In_Store_Net_Profit,Self_Delivery_Net_Profit,Uber_Eats_Net_Profit,DoorDash_Net_Profit
                             ],
                             'Profit Contribution':
                             [In_Store_Net_Profit_Contribution,Self_Delivery_Net_Profit_Contribution,Uber_Eats_Net_Profit_Contribution,DoorDash_Net_Profit_Contribution
                             ]
                            })
new_net_profit       
                                 
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
      <th>Channel</th>
      <th>Net Profit</th>
      <th>Profit Contribution</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>InStore</td>
      <td>3828417.36</td>
      <td>41.19</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Self Delivery</td>
      <td>3628278.44</td>
      <td>39.04</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Uber Eats</td>
      <td>1182979.08</td>
      <td>12.73</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Door Dash</td>
      <td>654803.68</td>
      <td>7.05</td>
    </tr>
  </tbody>
</table>
</div>


# By negotiating with UberEats & DoorDash for reducing commissions by 5% can increase profit share from 6% to 27% and by 3% commission reduce can increase profit share from 6% to 20% which is absolutely game changer for company's future
# Reason to negotiate is to company's getting 26679 daily orders from UberEats and 14538 from DoorDash ehich is practically too high and both companies must have to listen our sides as both are getting orders and business in huge volume and they let not go any vendor like us if we decided to cool down operations from their platforms 

```python
# Monthly e-commerce channels orders
monthly_ubereats_orders=df['UberEatsOrders'].sum()
monthly_doordash_orders=df['DoorDashOrders'].sum()

# Monthly e-commerce channels per day orders
Daily_avg_UberEats=(monthly_ubereats_orders/30).round(2)
Daily_avg_DoorDash=(monthly_doordash_orders/30).round(2)

# Print statement
print("Avg Daily Uber Eats Orders:",Daily_avg_UberEats)
print("Avg Daily Door Dash Orders:",Daily_avg_DoorDash)
```

    Avg Daily Uber Eats Orders: 26678.43
    Avg Daily Door Dash Orders: 14537.83
    


```python
# All channels monthly order totals
instore_monthly_orders=df['InStoreOrders'].sum()
selfdelivery_monthly_orders=df['SelfDeliveryOrders'].sum()
ubereats_monthly_orders=df['UberEatsOrders'].sum()
doordash_monthly_orders=df['DoorDashOrders'].sum()

# All channels monthly revenue totals
instore_monthly_revenue=df['InStoreRevenue'].sum()
selfdelivery_monthly_revenue=df['SelfDeliveryRevenue'].sum()
ubereats_monthly_revenue=df['UberEatsRevenue'].sum()
doordash_monthly_revenue=df['DoorDashRevenue'].sum()

# All channels monthly average order value (AOV)
instore_aov=(instore_monthly_revenue/instore_monthly_orders).round(2)
selfdelivery_aov=(selfdelivery_monthly_revenue/selfdelivery_monthly_orders).round(2)
ubereats_aov=(ubereats_monthly_revenue/ubereats_monthly_orders).round(2)
doordash_aov=(doordash_monthly_revenue/doordash_monthly_orders).round(2)

# Arrange in proper sequence
avg_order_value=pd.DataFrame({'Channel' :['In-Store','Self Delivery','Uber Eats','Door Dash'],
                              'AVg Order Value':[instore_aov,selfdelivery_aov,ubereats_aov,doordash_aov]
                             })
avg_order_value
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
      <th>Channel</th>
      <th>AVg Order Value</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>In-Store</td>
      <td>38.46</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Self Delivery</td>
      <td>38.54</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Uber Eats</td>
      <td>38.50</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Door Dash</td>
      <td>38.50</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Find outliers
def detect_outliers_iqr (df, column ):
    Q1=df[column].quantile(0.25)
    Q3=df[column].quantile(0.75)
    IQR=Q3-Q1
    lower=(Q1-1.5*IQR).round(2)
    upper=(Q3+1.5*IQR).round(2)
    outliers=df[(df[column]<lower) | (df[column]>upper)]
    return outliers, lower, upper
aov_outliers, aov_low, aov_high = detect_outliers_iqr(df, 'SelfDeliveryOrders')

# Print statement
print("AOV Outliers:", aov_outliers)
print("Lower Bound:", aov_low)
print("Upper Bound:", aov_high)
```

    AOV Outliers:      CuisineType  RestaurantID        RestaurantName       Segment  \
    1364       Pizza         25449     King Pizza Tavern          Cafe   
    1369       Pizza         25392    Urban Pizza Corner           QSR   
    1371       Pizza         25025       Top Pizza Grill  Full-service   
    1375       Pizza         25369    Lucky Pizza Bistro          Cafe   
    1376       Pizza         26111   Urban Pizza Kitchen           QSR   
    ...          ...           ...                   ...           ...   
    1566       Pizza         25423  Classic Pizza Corner          Cafe   
    1567       Pizza         26524    Lucky Pizza Bistro          Cafe   
    1570       Pizza         25304  Classic Pizza Bistro  Full-service   
    1571       Pizza         26450      Top Pizza Bistro           QSR   
    1573       Pizza         26651     Urban Pizza Grill           QSR   
    
               Subregion  GrowthFactor    AOV  MonthlyOrders  InStoreOrders  \
    1364             CBD          0.99  33.24           1773            469   
    1369  South Auckland          1.05  46.88           1499            270   
    1371     North Shore          1.03  31.92           1930            510   
    1375  South Auckland          1.05  38.81           1624            355   
    1376     North Shore          1.03  42.32           1855            346   
    ...              ...           ...    ...            ...            ...   
    1566  South Auckland          1.05  35.31           1929            580   
    1567  South Auckland          1.05  45.79           1801            436   
    1570   West Auckland          1.04  41.88           2154            708   
    1571     North Shore          1.03  40.75           1759            293   
    1573     North Shore          1.03  43.80           1694            380   
    
          InStoreRevenue  ...  doordash_commission  new_uber_commission  \
    1364        15589.56  ...            2776.2048            4092.5088   
    1369        12657.60  ...            3459.7440            5039.6000   
    1371        16279.20  ...            2719.5840            3966.0600   
    1375        13777.55  ...            3253.0542            4824.8592   
    1376        14642.72  ...            3450.7728            4915.8912   
    ...              ...  ...                  ...                  ...   
    1566        20479.80  ...            2955.4470            4333.2432   
    1567        19964.44  ...            3875.2077            5690.7812   
    1570        29651.04  ...            3752.0292            5509.7328   
    1571        11939.75  ...            3940.1175            5853.3300   
    1573        16644.00  ...            3340.6260            4835.5200   
    
          new_doordash_commission  Total_Commission  New Commission Rates  \
    1364                2342.4228         7626.5856                  0.29   
    1369                2883.1200         9507.2640                  0.27   
    1371                2266.3200         7478.8560                  0.27   
    1375                2760.1672         8939.4954                  0.30   
    1376                2811.7408         9483.9120                  0.24   
    ...                       ...               ...                   ...   
    1566                2478.7620         8122.0062                  0.28   
    1567                3250.1742        10660.3699                  0.28   
    1570                3146.8632        10321.3260                  0.28   
    1571                3343.1300        10838.6850                  0.30   
    1573                2764.6560         9183.5460                  0.26   
    
          Revised_UberEats_Commission  Revised_DoorDash_Commission  \
    1364                      4395.66                      2515.94   
    1369                      5442.77                      3113.77   
    1371                      4283.34                      2447.63   
    1375                      5169.49                      2957.32   
    1376                      5362.79                      3067.35   
    ...                           ...                          ...   
    1566                      4666.57                      2669.44   
    1567                      6128.53                      3500.19   
    1570                      5933.56                      3388.93   
    1571                      6271.43                      3581.93   
    1573                      5238.48                      2995.04   
    
          Revised_Commission  UberEats_Revised_Net_Profit  \
    1364             6434.93                      2225.43   
    1369             7922.72                      1932.43   
    1371             6232.38                     -3094.13   
    1375             7585.03                      1526.43   
    1376             7727.63                      3078.98   
    ...                  ...                          ...   
    1566             6812.00                      1571.85   
    1567             8940.95                      2828.19   
    1570             8656.59                     -2367.08   
    1571             9196.46                      1709.67   
    1573             7600.18                      1454.50   
    
          DoorDash_Revised_Net_Profit  
    1364                      1273.76  
    1369                      1105.52  
    1371                     -1768.09  
    1375                       873.22  
    1376                      1761.08  
    ...                           ...  
    1566                       899.15  
    1567                      1615.26  
    1570                     -1351.95  
    1571                       976.48  
    1573                       831.60  
    
    [62 rows x 42 columns]
    Lower Bound: -94.38
    Upper Bound: 546.62
    
# As per observations, there are no major outliers are visible with all important columns
# All orders and revenue lies with some amount of range 

```python
# Correlation
num_df=df.select_dtypes(include=['number'])
corr_metric=num_df.corr().round(2)
corr_metric
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
      <th>RestaurantID</th>
      <th>GrowthFactor</th>
      <th>AOV</th>
      <th>MonthlyOrders</th>
      <th>InStoreOrders</th>
      <th>InStoreRevenue</th>
      <th>UberEatsOrders</th>
      <th>DoorDashOrders</th>
      <th>SelfDeliveryOrders</th>
      <th>UberEatsRevenue</th>
      <th>...</th>
      <th>doordash_commission</th>
      <th>new_uber_commission</th>
      <th>new_doordash_commission</th>
      <th>Total_Commission</th>
      <th>New Commission Rates</th>
      <th>Revised_UberEats_Commission</th>
      <th>Revised_DoorDash_Commission</th>
      <th>Revised_Commission</th>
      <th>UberEats_Revised_Net_Profit</th>
      <th>DoorDash_Revised_Net_Profit</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>RestaurantID</th>
      <td>1.00</td>
      <td>-0.00</td>
      <td>-0.01</td>
      <td>0.02</td>
      <td>0.02</td>
      <td>0.02</td>
      <td>0.01</td>
      <td>0.02</td>
      <td>0.01</td>
      <td>0.01</td>
      <td>...</td>
      <td>0.01</td>
      <td>-0.00</td>
      <td>0.01</td>
      <td>0.00</td>
      <td>-0.04</td>
      <td>-0.00</td>
      <td>0.01</td>
      <td>0.00</td>
      <td>-0.02</td>
      <td>-0.02</td>
    </tr>
    <tr>
      <th>GrowthFactor</th>
      <td>-0.00</td>
      <td>1.00</td>
      <td>0.21</td>
      <td>0.04</td>
      <td>0.02</td>
      <td>0.06</td>
      <td>0.04</td>
      <td>0.03</td>
      <td>0.04</td>
      <td>0.11</td>
      <td>...</td>
      <td>0.09</td>
      <td>0.10</td>
      <td>0.09</td>
      <td>0.10</td>
      <td>-0.03</td>
      <td>0.10</td>
      <td>0.09</td>
      <td>0.10</td>
      <td>0.03</td>
      <td>0.03</td>
    </tr>
    <tr>
      <th>AOV</th>
      <td>-0.01</td>
      <td>0.21</td>
      <td>1.00</td>
      <td>-0.01</td>
      <td>-0.02</td>
      <td>0.15</td>
      <td>-0.01</td>
      <td>-0.01</td>
      <td>0.01</td>
      <td>0.29</td>
      <td>...</td>
      <td>0.28</td>
      <td>0.28</td>
      <td>0.28</td>
      <td>0.29</td>
      <td>-0.05</td>
      <td>0.28</td>
      <td>0.28</td>
      <td>0.28</td>
      <td>0.10</td>
      <td>0.10</td>
    </tr>
    <tr>
      <th>MonthlyOrders</th>
      <td>0.02</td>
      <td>0.04</td>
      <td>-0.01</td>
      <td>1.00</td>
      <td>0.74</td>
      <td>0.72</td>
      <td>0.83</td>
      <td>0.82</td>
      <td>0.72</td>
      <td>0.79</td>
      <td>...</td>
      <td>0.76</td>
      <td>0.77</td>
      <td>0.76</td>
      <td>0.78</td>
      <td>0.01</td>
      <td>0.77</td>
      <td>0.76</td>
      <td>0.77</td>
      <td>-0.09</td>
      <td>-0.09</td>
    </tr>
    <tr>
      <th>InStoreOrders</th>
      <td>0.02</td>
      <td>0.02</td>
      <td>-0.02</td>
      <td>0.74</td>
      <td>1.00</td>
      <td>0.98</td>
      <td>0.34</td>
      <td>0.28</td>
      <td>0.58</td>
      <td>0.32</td>
      <td>...</td>
      <td>0.25</td>
      <td>0.31</td>
      <td>0.25</td>
      <td>0.29</td>
      <td>-0.02</td>
      <td>0.31</td>
      <td>0.25</td>
      <td>0.29</td>
      <td>-0.46</td>
      <td>-0.47</td>
    </tr>
    <tr>
      <th>InStoreRevenue</th>
      <td>0.02</td>
      <td>0.06</td>
      <td>0.15</td>
      <td>0.72</td>
      <td>0.98</td>
      <td>1.00</td>
      <td>0.34</td>
      <td>0.27</td>
      <td>0.57</td>
      <td>0.37</td>
      <td>...</td>
      <td>0.30</td>
      <td>0.35</td>
      <td>0.29</td>
      <td>0.34</td>
      <td>-0.03</td>
      <td>0.35</td>
      <td>0.29</td>
      <td>0.33</td>
      <td>-0.44</td>
      <td>-0.44</td>
    </tr>
    <tr>
      <th>UberEatsOrders</th>
      <td>0.01</td>
      <td>0.04</td>
      <td>-0.01</td>
      <td>0.83</td>
      <td>0.34</td>
      <td>0.34</td>
      <td>1.00</td>
      <td>0.95</td>
      <td>0.31</td>
      <td>0.95</td>
      <td>...</td>
      <td>0.89</td>
      <td>0.93</td>
      <td>0.89</td>
      <td>0.93</td>
      <td>0.02</td>
      <td>0.93</td>
      <td>0.89</td>
      <td>0.93</td>
      <td>0.09</td>
      <td>0.09</td>
    </tr>
    <tr>
      <th>DoorDashOrders</th>
      <td>0.02</td>
      <td>0.03</td>
      <td>-0.01</td>
      <td>0.82</td>
      <td>0.28</td>
      <td>0.27</td>
      <td>0.95</td>
      <td>1.00</td>
      <td>0.36</td>
      <td>0.90</td>
      <td>...</td>
      <td>0.93</td>
      <td>0.88</td>
      <td>0.93</td>
      <td>0.91</td>
      <td>0.01</td>
      <td>0.89</td>
      <td>0.93</td>
      <td>0.91</td>
      <td>0.10</td>
      <td>0.10</td>
    </tr>
    <tr>
      <th>SelfDeliveryOrders</th>
      <td>0.01</td>
      <td>0.04</td>
      <td>0.01</td>
      <td>0.72</td>
      <td>0.58</td>
      <td>0.57</td>
      <td>0.31</td>
      <td>0.36</td>
      <td>1.00</td>
      <td>0.30</td>
      <td>...</td>
      <td>0.35</td>
      <td>0.29</td>
      <td>0.34</td>
      <td>0.31</td>
      <td>0.02</td>
      <td>0.29</td>
      <td>0.35</td>
      <td>0.31</td>
      <td>0.05</td>
      <td>0.06</td>
    </tr>
    <tr>
      <th>UberEatsRevenue</th>
      <td>0.01</td>
      <td>0.11</td>
      <td>0.29</td>
      <td>0.79</td>
      <td>0.32</td>
      <td>0.37</td>
      <td>0.95</td>
      <td>0.90</td>
      <td>0.30</td>
      <td>1.00</td>
      <td>...</td>
      <td>0.94</td>
      <td>0.98</td>
      <td>0.94</td>
      <td>0.98</td>
      <td>0.00</td>
      <td>0.98</td>
      <td>0.94</td>
      <td>0.98</td>
      <td>0.12</td>
      <td>0.12</td>
    </tr>
    <tr>
      <th>DoorDashRevenue</th>
      <td>0.02</td>
      <td>0.10</td>
      <td>0.29</td>
      <td>0.77</td>
      <td>0.26</td>
      <td>0.31</td>
      <td>0.90</td>
      <td>0.95</td>
      <td>0.35</td>
      <td>0.96</td>
      <td>...</td>
      <td>0.99</td>
      <td>0.94</td>
      <td>0.98</td>
      <td>0.97</td>
      <td>-0.00</td>
      <td>0.94</td>
      <td>0.98</td>
      <td>0.96</td>
      <td>0.13</td>
      <td>0.14</td>
    </tr>
    <tr>
      <th>SelfDeliveryRevenue</th>
      <td>0.01</td>
      <td>0.09</td>
      <td>0.22</td>
      <td>0.69</td>
      <td>0.56</td>
      <td>0.59</td>
      <td>0.30</td>
      <td>0.35</td>
      <td>0.97</td>
      <td>0.35</td>
      <td>...</td>
      <td>0.40</td>
      <td>0.34</td>
      <td>0.40</td>
      <td>0.37</td>
      <td>0.00</td>
      <td>0.35</td>
      <td>0.40</td>
      <td>0.37</td>
      <td>0.08</td>
      <td>0.08</td>
    </tr>
    <tr>
      <th>COGSRate</th>
      <td>0.01</td>
      <td>-0.03</td>
      <td>-0.05</td>
      <td>0.14</td>
      <td>0.38</td>
      <td>0.37</td>
      <td>0.02</td>
      <td>0.01</td>
      <td>-0.01</td>
      <td>-0.00</td>
      <td>...</td>
      <td>-0.01</td>
      <td>-0.01</td>
      <td>-0.01</td>
      <td>-0.01</td>
      <td>-0.02</td>
      <td>-0.01</td>
      <td>-0.01</td>
      <td>-0.01</td>
      <td>-0.79</td>
      <td>-0.79</td>
    </tr>
    <tr>
      <th>OPEXRate</th>
      <td>0.02</td>
      <td>-0.02</td>
      <td>-0.05</td>
      <td>0.17</td>
      <td>0.49</td>
      <td>0.48</td>
      <td>0.00</td>
      <td>-0.01</td>
      <td>-0.01</td>
      <td>-0.01</td>
      <td>...</td>
      <td>-0.04</td>
      <td>-0.02</td>
      <td>-0.04</td>
      <td>-0.03</td>
      <td>-0.03</td>
      <td>-0.02</td>
      <td>-0.04</td>
      <td>-0.03</td>
      <td>-0.84</td>
      <td>-0.84</td>
    </tr>
    <tr>
      <th>CommissionRate</th>
      <td>-0.04</td>
      <td>-0.03</td>
      <td>-0.05</td>
      <td>0.01</td>
      <td>-0.02</td>
      <td>-0.03</td>
      <td>0.02</td>
      <td>0.01</td>
      <td>0.02</td>
      <td>0.00</td>
      <td>...</td>
      <td>0.15</td>
      <td>0.19</td>
      <td>0.18</td>
      <td>0.16</td>
      <td>1.00</td>
      <td>0.17</td>
      <td>0.17</td>
      <td>0.19</td>
      <td>-0.11</td>
      <td>-0.10</td>
    </tr>
    <tr>
      <th>DeliveryRadiusKM</th>
      <td>0.00</td>
      <td>-0.01</td>
      <td>-0.04</td>
      <td>-0.01</td>
      <td>-0.00</td>
      <td>-0.01</td>
      <td>-0.02</td>
      <td>-0.02</td>
      <td>-0.00</td>
      <td>-0.03</td>
      <td>...</td>
      <td>-0.04</td>
      <td>-0.03</td>
      <td>-0.04</td>
      <td>-0.03</td>
      <td>0.01</td>
      <td>-0.03</td>
      <td>-0.04</td>
      <td>-0.03</td>
      <td>-0.00</td>
      <td>-0.00</td>
    </tr>
    <tr>
      <th>DeliveryCostPerOrder</th>
      <td>0.00</td>
      <td>-0.01</td>
      <td>-0.04</td>
      <td>-0.01</td>
      <td>-0.00</td>
      <td>-0.01</td>
      <td>-0.02</td>
      <td>-0.02</td>
      <td>-0.00</td>
      <td>-0.03</td>
      <td>...</td>
      <td>-0.04</td>
      <td>-0.03</td>
      <td>-0.04</td>
      <td>-0.03</td>
      <td>0.01</td>
      <td>-0.03</td>
      <td>-0.04</td>
      <td>-0.03</td>
      <td>-0.00</td>
      <td>-0.00</td>
    </tr>
    <tr>
      <th>SD_DeliveryTotalCost</th>
      <td>0.01</td>
      <td>0.03</td>
      <td>-0.01</td>
      <td>0.53</td>
      <td>0.44</td>
      <td>0.43</td>
      <td>0.22</td>
      <td>0.26</td>
      <td>0.75</td>
      <td>0.20</td>
      <td>...</td>
      <td>0.24</td>
      <td>0.20</td>
      <td>0.24</td>
      <td>0.22</td>
      <td>0.01</td>
      <td>0.20</td>
      <td>0.24</td>
      <td>0.21</td>
      <td>0.03</td>
      <td>0.03</td>
    </tr>
    <tr>
      <th>InStoreNetProfit</th>
      <td>-0.01</td>
      <td>0.07</td>
      <td>0.18</td>
      <td>0.59</td>
      <td>0.62</td>
      <td>0.66</td>
      <td>0.32</td>
      <td>0.26</td>
      <td>0.58</td>
      <td>0.37</td>
      <td>...</td>
      <td>0.31</td>
      <td>0.36</td>
      <td>0.31</td>
      <td>0.35</td>
      <td>0.01</td>
      <td>0.36</td>
      <td>0.31</td>
      <td>0.34</td>
      <td>0.26</td>
      <td>0.25</td>
    </tr>
    <tr>
      <th>UberEatsNetProfit</th>
      <td>-0.02</td>
      <td>0.02</td>
      <td>0.07</td>
      <td>-0.16</td>
      <td>-0.49</td>
      <td>-0.47</td>
      <td>0.01</td>
      <td>0.02</td>
      <td>0.03</td>
      <td>0.04</td>
      <td>...</td>
      <td>0.03</td>
      <td>0.01</td>
      <td>0.03</td>
      <td>0.02</td>
      <td>-0.11</td>
      <td>0.02</td>
      <td>0.03</td>
      <td>0.02</td>
      <td>1.00</td>
      <td>0.99</td>
    </tr>
    <tr>
      <th>DoorDashNetProfit</th>
      <td>-0.02</td>
      <td>0.02</td>
      <td>0.08</td>
      <td>-0.16</td>
      <td>-0.49</td>
      <td>-0.47</td>
      <td>0.01</td>
      <td>0.02</td>
      <td>0.03</td>
      <td>0.04</td>
      <td>...</td>
      <td>0.03</td>
      <td>0.02</td>
      <td>0.03</td>
      <td>0.02</td>
      <td>-0.10</td>
      <td>0.02</td>
      <td>0.03</td>
      <td>0.02</td>
      <td>0.99</td>
      <td>1.00</td>
    </tr>
    <tr>
      <th>SelfDeliveryNetProfit</th>
      <td>-0.02</td>
      <td>0.08</td>
      <td>0.23</td>
      <td>0.33</td>
      <td>0.00</td>
      <td>0.04</td>
      <td>0.20</td>
      <td>0.23</td>
      <td>0.64</td>
      <td>0.26</td>
      <td>...</td>
      <td>0.31</td>
      <td>0.27</td>
      <td>0.31</td>
      <td>0.28</td>
      <td>0.04</td>
      <td>0.27</td>
      <td>0.31</td>
      <td>0.28</td>
      <td>0.65</td>
      <td>0.66</td>
    </tr>
    <tr>
      <th>InStoreShare</th>
      <td>0.02</td>
      <td>-0.01</td>
      <td>-0.01</td>
      <td>0.30</td>
      <td>0.83</td>
      <td>0.82</td>
      <td>-0.11</td>
      <td>-0.19</td>
      <td>0.29</td>
      <td>-0.11</td>
      <td>...</td>
      <td>-0.18</td>
      <td>-0.11</td>
      <td>-0.18</td>
      <td>-0.14</td>
      <td>-0.02</td>
      <td>-0.11</td>
      <td>-0.18</td>
      <td>-0.14</td>
      <td>-0.56</td>
      <td>-0.56</td>
    </tr>
    <tr>
      <th>UE_share</th>
      <td>-0.01</td>
      <td>0.00</td>
      <td>-0.00</td>
      <td>-0.13</td>
      <td>-0.27</td>
      <td>-0.27</td>
      <td>0.34</td>
      <td>0.21</td>
      <td>-0.72</td>
      <td>0.32</td>
      <td>...</td>
      <td>0.19</td>
      <td>0.32</td>
      <td>0.19</td>
      <td>0.28</td>
      <td>-0.00</td>
      <td>0.32</td>
      <td>0.19</td>
      <td>0.28</td>
      <td>0.01</td>
      <td>-0.00</td>
    </tr>
    <tr>
      <th>DD_share</th>
      <td>0.02</td>
      <td>-0.03</td>
      <td>-0.02</td>
      <td>-0.20</td>
      <td>-0.46</td>
      <td>-0.46</td>
      <td>0.22</td>
      <td>0.32</td>
      <td>-0.64</td>
      <td>0.21</td>
      <td>...</td>
      <td>0.29</td>
      <td>0.20</td>
      <td>0.28</td>
      <td>0.23</td>
      <td>-0.03</td>
      <td>0.20</td>
      <td>0.29</td>
      <td>0.23</td>
      <td>0.03</td>
      <td>0.04</td>
    </tr>
    <tr>
      <th>SD_share</th>
      <td>-0.00</td>
      <td>0.01</td>
      <td>0.01</td>
      <td>0.17</td>
      <td>0.36</td>
      <td>0.36</td>
      <td>-0.33</td>
      <td>-0.26</td>
      <td>0.75</td>
      <td>-0.31</td>
      <td>...</td>
      <td>-0.24</td>
      <td>-0.30</td>
      <td>-0.24</td>
      <td>-0.28</td>
      <td>0.01</td>
      <td>-0.30</td>
      <td>-0.24</td>
      <td>-0.28</td>
      <td>-0.02</td>
      <td>-0.01</td>
    </tr>
    <tr>
      <th>Commission Amount</th>
      <td>-0.00</td>
      <td>0.10</td>
      <td>0.28</td>
      <td>0.78</td>
      <td>0.31</td>
      <td>0.35</td>
      <td>0.94</td>
      <td>0.89</td>
      <td>0.29</td>
      <td>0.99</td>
      <td>...</td>
      <td>0.96</td>
      <td>1.00</td>
      <td>0.96</td>
      <td>0.99</td>
      <td>0.16</td>
      <td>1.00</td>
      <td>0.96</td>
      <td>0.99</td>
      <td>0.11</td>
      <td>0.10</td>
    </tr>
    <tr>
      <th>uber_commission</th>
      <td>-0.00</td>
      <td>0.10</td>
      <td>0.28</td>
      <td>0.78</td>
      <td>0.31</td>
      <td>0.35</td>
      <td>0.94</td>
      <td>0.89</td>
      <td>0.29</td>
      <td>0.99</td>
      <td>...</td>
      <td>0.96</td>
      <td>1.00</td>
      <td>0.96</td>
      <td>0.99</td>
      <td>0.16</td>
      <td>1.00</td>
      <td>0.96</td>
      <td>0.99</td>
      <td>0.11</td>
      <td>0.10</td>
    </tr>
    <tr>
      <th>doordash_commission</th>
      <td>0.01</td>
      <td>0.09</td>
      <td>0.28</td>
      <td>0.76</td>
      <td>0.25</td>
      <td>0.30</td>
      <td>0.89</td>
      <td>0.93</td>
      <td>0.35</td>
      <td>0.94</td>
      <td>...</td>
      <td>1.00</td>
      <td>0.96</td>
      <td>1.00</td>
      <td>0.98</td>
      <td>0.15</td>
      <td>0.96</td>
      <td>1.00</td>
      <td>0.98</td>
      <td>0.11</td>
      <td>0.12</td>
    </tr>
    <tr>
      <th>new_uber_commission</th>
      <td>-0.00</td>
      <td>0.10</td>
      <td>0.28</td>
      <td>0.77</td>
      <td>0.31</td>
      <td>0.35</td>
      <td>0.93</td>
      <td>0.88</td>
      <td>0.29</td>
      <td>0.98</td>
      <td>...</td>
      <td>0.96</td>
      <td>1.00</td>
      <td>0.96</td>
      <td>0.99</td>
      <td>0.19</td>
      <td>1.00</td>
      <td>0.96</td>
      <td>0.99</td>
      <td>0.10</td>
      <td>0.10</td>
    </tr>
    <tr>
      <th>new_doordash_commission</th>
      <td>0.01</td>
      <td>0.09</td>
      <td>0.28</td>
      <td>0.76</td>
      <td>0.25</td>
      <td>0.29</td>
      <td>0.89</td>
      <td>0.93</td>
      <td>0.34</td>
      <td>0.94</td>
      <td>...</td>
      <td>1.00</td>
      <td>0.96</td>
      <td>1.00</td>
      <td>0.98</td>
      <td>0.18</td>
      <td>0.96</td>
      <td>1.00</td>
      <td>0.98</td>
      <td>0.11</td>
      <td>0.11</td>
    </tr>
    <tr>
      <th>Total_Commission</th>
      <td>0.00</td>
      <td>0.10</td>
      <td>0.29</td>
      <td>0.78</td>
      <td>0.29</td>
      <td>0.34</td>
      <td>0.93</td>
      <td>0.91</td>
      <td>0.31</td>
      <td>0.98</td>
      <td>...</td>
      <td>0.98</td>
      <td>0.99</td>
      <td>0.98</td>
      <td>1.00</td>
      <td>0.16</td>
      <td>0.99</td>
      <td>0.98</td>
      <td>1.00</td>
      <td>0.11</td>
      <td>0.11</td>
    </tr>
    <tr>
      <th>New Commission Rates</th>
      <td>-0.04</td>
      <td>-0.03</td>
      <td>-0.05</td>
      <td>0.01</td>
      <td>-0.02</td>
      <td>-0.03</td>
      <td>0.02</td>
      <td>0.01</td>
      <td>0.02</td>
      <td>0.00</td>
      <td>...</td>
      <td>0.15</td>
      <td>0.19</td>
      <td>0.18</td>
      <td>0.16</td>
      <td>1.00</td>
      <td>0.17</td>
      <td>0.17</td>
      <td>0.19</td>
      <td>-0.11</td>
      <td>-0.10</td>
    </tr>
    <tr>
      <th>Revised_UberEats_Commission</th>
      <td>-0.00</td>
      <td>0.10</td>
      <td>0.28</td>
      <td>0.77</td>
      <td>0.31</td>
      <td>0.35</td>
      <td>0.93</td>
      <td>0.89</td>
      <td>0.29</td>
      <td>0.98</td>
      <td>...</td>
      <td>0.96</td>
      <td>1.00</td>
      <td>0.96</td>
      <td>0.99</td>
      <td>0.17</td>
      <td>1.00</td>
      <td>0.96</td>
      <td>0.99</td>
      <td>0.10</td>
      <td>0.10</td>
    </tr>
    <tr>
      <th>Revised_DoorDash_Commission</th>
      <td>0.01</td>
      <td>0.09</td>
      <td>0.28</td>
      <td>0.76</td>
      <td>0.25</td>
      <td>0.29</td>
      <td>0.89</td>
      <td>0.93</td>
      <td>0.35</td>
      <td>0.94</td>
      <td>...</td>
      <td>1.00</td>
      <td>0.96</td>
      <td>1.00</td>
      <td>0.98</td>
      <td>0.17</td>
      <td>0.96</td>
      <td>1.00</td>
      <td>0.98</td>
      <td>0.11</td>
      <td>0.12</td>
    </tr>
    <tr>
      <th>Revised_Commission</th>
      <td>0.00</td>
      <td>0.10</td>
      <td>0.28</td>
      <td>0.77</td>
      <td>0.29</td>
      <td>0.33</td>
      <td>0.93</td>
      <td>0.91</td>
      <td>0.31</td>
      <td>0.98</td>
      <td>...</td>
      <td>0.98</td>
      <td>0.99</td>
      <td>0.98</td>
      <td>1.00</td>
      <td>0.19</td>
      <td>0.99</td>
      <td>0.98</td>
      <td>1.00</td>
      <td>0.11</td>
      <td>0.10</td>
    </tr>
    <tr>
      <th>UberEats_Revised_Net_Profit</th>
      <td>-0.02</td>
      <td>0.03</td>
      <td>0.10</td>
      <td>-0.09</td>
      <td>-0.46</td>
      <td>-0.44</td>
      <td>0.09</td>
      <td>0.10</td>
      <td>0.05</td>
      <td>0.12</td>
      <td>...</td>
      <td>0.11</td>
      <td>0.10</td>
      <td>0.11</td>
      <td>0.11</td>
      <td>-0.11</td>
      <td>0.10</td>
      <td>0.11</td>
      <td>0.11</td>
      <td>1.00</td>
      <td>0.99</td>
    </tr>
    <tr>
      <th>DoorDash_Revised_Net_Profit</th>
      <td>-0.02</td>
      <td>0.03</td>
      <td>0.10</td>
      <td>-0.09</td>
      <td>-0.47</td>
      <td>-0.44</td>
      <td>0.09</td>
      <td>0.10</td>
      <td>0.06</td>
      <td>0.12</td>
      <td>...</td>
      <td>0.12</td>
      <td>0.10</td>
      <td>0.11</td>
      <td>0.11</td>
      <td>-0.10</td>
      <td>0.10</td>
      <td>0.12</td>
      <td>0.10</td>
      <td>0.99</td>
      <td>1.00</td>
    </tr>
  </tbody>
</table>
<p>38 rows × 38 columns</p>
</div>




```python
plt.figure(figsize=(8,6))
sns.heatmap(corr_matrix_colmn, annot=True, cmap='coolwarm', fmt='.2f', linewidths=0.5, center=0)
plt.title('Correlation Heatmap', fontsize=15)
plt.show()
```


    
![png](output_38_0.png)
    



```python
# Correlation 
colmn=[ 'AOV', 'MonthlyOrders','InStoreNetProfit','UberEatsNetProfit', 'DoorDashNetProfit',
       'SelfDeliveryNetProfit',]
corr_matrix_colmn=df[colmn].corr()
corr_matrix_colmn.round(2)
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
      <th>AOV</th>
      <th>MonthlyOrders</th>
      <th>InStoreNetProfit</th>
      <th>UberEatsNetProfit</th>
      <th>DoorDashNetProfit</th>
      <th>SelfDeliveryNetProfit</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>AOV</th>
      <td>1.00</td>
      <td>-0.01</td>
      <td>0.18</td>
      <td>0.07</td>
      <td>0.08</td>
      <td>0.23</td>
    </tr>
    <tr>
      <th>MonthlyOrders</th>
      <td>-0.01</td>
      <td>1.00</td>
      <td>0.59</td>
      <td>-0.16</td>
      <td>-0.16</td>
      <td>0.33</td>
    </tr>
    <tr>
      <th>InStoreNetProfit</th>
      <td>0.18</td>
      <td>0.59</td>
      <td>1.00</td>
      <td>0.23</td>
      <td>0.23</td>
      <td>0.58</td>
    </tr>
    <tr>
      <th>UberEatsNetProfit</th>
      <td>0.07</td>
      <td>-0.16</td>
      <td>0.23</td>
      <td>1.00</td>
      <td>0.99</td>
      <td>0.64</td>
    </tr>
    <tr>
      <th>DoorDashNetProfit</th>
      <td>0.08</td>
      <td>-0.16</td>
      <td>0.23</td>
      <td>0.99</td>
      <td>1.00</td>
      <td>0.64</td>
    </tr>
    <tr>
      <th>SelfDeliveryNetProfit</th>
      <td>0.23</td>
      <td>0.33</td>
      <td>0.58</td>
      <td>0.64</td>
      <td>0.64</td>
      <td>1.00</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Correlation 
colmn=[ 'AOV', 'MonthlyOrders','InStoreRevenue','UberEatsRevenue', 'DoorDashRevenue',
       'SelfDeliveryRevenue',]
corr_matrix_colmn=df[colmn].corr()
corr_matrix_colmn.round(2)
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
      <th>AOV</th>
      <th>MonthlyOrders</th>
      <th>InStoreRevenue</th>
      <th>UberEatsRevenue</th>
      <th>DoorDashRevenue</th>
      <th>SelfDeliveryRevenue</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>AOV</th>
      <td>1.00</td>
      <td>-0.01</td>
      <td>0.15</td>
      <td>0.29</td>
      <td>0.29</td>
      <td>0.22</td>
    </tr>
    <tr>
      <th>MonthlyOrders</th>
      <td>-0.01</td>
      <td>1.00</td>
      <td>0.72</td>
      <td>0.79</td>
      <td>0.77</td>
      <td>0.69</td>
    </tr>
    <tr>
      <th>InStoreRevenue</th>
      <td>0.15</td>
      <td>0.72</td>
      <td>1.00</td>
      <td>0.37</td>
      <td>0.31</td>
      <td>0.59</td>
    </tr>
    <tr>
      <th>UberEatsRevenue</th>
      <td>0.29</td>
      <td>0.79</td>
      <td>0.37</td>
      <td>1.00</td>
      <td>0.96</td>
      <td>0.35</td>
    </tr>
    <tr>
      <th>DoorDashRevenue</th>
      <td>0.29</td>
      <td>0.77</td>
      <td>0.31</td>
      <td>0.96</td>
      <td>1.00</td>
      <td>0.40</td>
    </tr>
    <tr>
      <th>SelfDeliveryRevenue</th>
      <td>0.22</td>
      <td>0.69</td>
      <td>0.59</td>
      <td>0.35</td>
      <td>0.40</td>
      <td>1.00</td>
    </tr>
  </tbody>
</table>
</div>




```python
plt.figure(figsize=(8,6))
sns.heatmap(corr_matrix_colmn, annot=True, cmap='coolwarm', fmt='.2f', linewidths=0.5, center=0)
plt.title('Correlation Heatmap', fontsize=15)
plt.show()
```


    
![png](output_41_0.png)
    



```python
df.columns
```




    Index(['CuisineType', 'RestaurantID', 'RestaurantName', 'Segment', 'Subregion',
           'GrowthFactor', 'AOV', 'MonthlyOrders', 'InStoreOrders',
           'InStoreRevenue', 'UberEatsOrders', 'DoorDashOrders',
           'SelfDeliveryOrders', 'UberEatsRevenue', 'DoorDashRevenue',
           'SelfDeliveryRevenue', 'COGSRate', 'OPEXRate', 'CommissionRate',
           'DeliveryRadiusKM', 'DeliveryCostPerOrder', 'SD_DeliveryTotalCost',
           'InStoreNetProfit', 'UberEatsNetProfit', 'DoorDashNetProfit',
           'SelfDeliveryNetProfit', 'InStoreShare', 'UE_share', 'DD_share',
           'SD_share', 'Commission Amount', 'uber_commission',
           'doordash_commission', 'new_uber_commission', 'new_doordash_commission',
           'Total_Commission', 'New Commission Rates',
           'Revised_UberEats_Commission', 'Revised_DoorDash_Commission',
           'Revised_Commission', 'UberEats_Revised_Net_Profit',
           'DoorDash_Revised_Net_Profit'],
          dtype='object')




```python
# Correlation
colmn=[ 'AOV','InStoreRevenue','UberEatsRevenue', 'DoorDashRevenue',
       'SelfDeliveryRevenue',]
corr_matrix_colmn=df[colmn].corr()
corr_matrix_colmn.round(2)
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
      <th>AOV</th>
      <th>InStoreRevenue</th>
      <th>UberEatsRevenue</th>
      <th>DoorDashRevenue</th>
      <th>SelfDeliveryRevenue</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>AOV</th>
      <td>1.00</td>
      <td>0.15</td>
      <td>0.29</td>
      <td>0.29</td>
      <td>0.22</td>
    </tr>
    <tr>
      <th>InStoreRevenue</th>
      <td>0.15</td>
      <td>1.00</td>
      <td>0.37</td>
      <td>0.31</td>
      <td>0.59</td>
    </tr>
    <tr>
      <th>UberEatsRevenue</th>
      <td>0.29</td>
      <td>0.37</td>
      <td>1.00</td>
      <td>0.96</td>
      <td>0.35</td>
    </tr>
    <tr>
      <th>DoorDashRevenue</th>
      <td>0.29</td>
      <td>0.31</td>
      <td>0.96</td>
      <td>1.00</td>
      <td>0.40</td>
    </tr>
    <tr>
      <th>SelfDeliveryRevenue</th>
      <td>0.22</td>
      <td>0.59</td>
      <td>0.35</td>
      <td>0.40</td>
      <td>1.00</td>
    </tr>
  </tbody>
</table>
</div>


# As monthly orders are increasing, the net profit for Uber Eats and Door Dash is showing negative correlation -0.16 that means company is doing loss making business and if they continue with these 2 platforms then loss will increase with time
# While there is an opportunity showing in SelfDelivery as increase in SelfDelivery AOV will increase Net Profit for SelfDelivery orders
# Company need to work on strategy to push customers to buy more in single purchase by giving more discount on higher purse items or giving free delivery above specific amount, this types of strategies company have to introduce to increase AOV for self delivery
# Instore and Self Delivery revenue is supporting each other as store's revenue increase or customers are stepping in when Self Delivery orders are increasing


```python

```
