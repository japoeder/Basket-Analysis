# Basket Analysis

## Introduction

The Instacart Market Basket Analysis is focused on understanding customer purchasing patterns using a dataset containing 3 million grocery orders from over 200,000 Instacart users. The dataset encompasses a variety of files that outline various aspects such as order details, product information, and the order in which products were added to the cart. A significant feature of this dataset is its insight into customer behavior, particularly with regards to product reordering patterns.

## Objectives

- Evaluating the distribution of orders across different days of the week, suggesting that weekends tend to have higher order volumes.
- Analyzing the times of day when orders are typically placed, with a focus on day time as the peak period.
- Assessing the reorder percentage of different product categories, highlighting that day-to-day food items have higher reorder rates.
- Determining popular aisles and departments, which can influence store layout optimization.
- Identifying top products, many of which are organic, suggesting a trend in consumer preference for organic items.

## Project Structure
```
.
├── _plts/                            : Data visualization 
├── _util/                            : Various project utilities 
├── 1) EDA.ipynb                      : EDA to analyze customer purchase pattern
├── 2) Segmentation Analysis.ipynb    : Aisle driven customer segmentation
├── 3) Feature Engineering.ipynb      : Feature engineering for ML
├── 4) Finalize DataPrep.ipynb        : Clean up data for modeling
├── 5) Basket Analysis.ipynb          : Final basket analysis
└── README.md                         : Project Report 
```

## Datasets

#### aisles.csv

*134* distinct aisles commonly observed in retail grocers including, but not limited to:
- prepared soups salads
- specialty cheeses
- energy granola bars
- instant foods
- marinades meat preparation

#### departments.csv

*21* unique departments commonly observed in retail grocers including but not limited to:
- frozen
- other
- bakery
- produce
- alcohol

#### orders.csv

Order level data with various dimensionality for product, department, etc. There are total 3421083 orders made by total 206209 users.

#### products.csv

Data on 49688 products and relevant dimensionality including aisle and department. Commonly observed products in the set include:
- Banana
- Bag of Organic Bananas
- Organic Strawberries
- Organic Baby Spinach
- Large Lemon 

#### order_products_train.csv
Which products were ordered and in what order they're added to the cart, as well as reorder status. 131209 orders across 39123 products.

#### order_products_prior.csv
Which products were ordered and in what order they're added to the cart, as well as reorder status. 3214874 orders across 49677 products.



## EDA Highlights

<br>

<p align="center">
  <img width="700" height="200" src="https://github.com/japoeder/Basket-Analysis/blob/master/_plts/high_vol_products_by_dow.png?raw=true">
</p>

- 0 and 1 appear to represent Saturday and Sunday, respectively, which is consistent with intuition.

<p align="center">
  <img width="700" height="200" src="https://github.com/japoeder/Basket-Analysis/blob/master/_plts/high_vol_prod_x_dow.png?raw=true">
</p>

- Nothing earth shatteringly different here as compared to above when adding top product dimension.

<p align="center">
  <img width="700" height="200" src="https://github.com/japoeder/Basket-Analysis/blob/master/_plts/orders_by_dow_and_hour_of_day.png?raw=true">
</p>

- Time of day consistent with intuition as well, with the the bulk of shopping done from 9am to 4pm (highest on weekends)

<p align="center">
  <img width="700" height="200" src="https://github.com/japoeder/Basket-Analysis/blob/master/_plts/order_count_distribution.png?raw=true">
</p>

- Orders per customer ranges from 0 to 100, probably truncated at max.
- The training data shows reorder percent ~59.86%, while the prior set indicates ~58.97%

<p align="center">
  <img width="700" height="200" src="https://github.com/japoeder/Basket-Analysis/blob/master/_plts/cart_item_count_distribution.png?raw=true">
</p>

- Frequency distribution of cart item count is highly right skewed, but comports with intuition.  Most carts can pass through the 20 item or less aisle.

<p align="center">
  <img width="700" height="200" src="https://github.com/japoeder/Basket-Analysis/blob/master/_plts/days_since_prior_order_dist.png?raw=true">
</p>

- Purchase cycle surfaces in 'Days Since Prior Order' graph with bumps at 7, 14, 21 and 30.

<p align="center">
  <img width="700" height="200" src="https://github.com/japoeder/Basket-Analysis/blob/master/_plts/Order Counts x Aisle.png?raw=true">
</p>

- Pretty consistent reorder consistency across aisles.  Drops off a little with high order count categories like fruits and vegetables, but this seems to make sense given how particular people seem to be when picking these items for themselves.

<p align="center">
  <img width="350" height="150" src="https://github.com/japoeder/Basket-Analysis/blob/master/_plts/highest_20_aisles_reorder_ratio.png?raw=true">
  <img width="350" height="150" src="https://github.com/japoeder/Basket-Analysis/blob/master/_plts/lowest_20_aisles_reorder_ratio.png?raw=true">
</p>

- Reorder percentage of day-to-day food items is high and for other products such as vitamins, first-aids, beauty products, etc. reorder percentage is low. Intuitive given purchase cycle.

<p align="center">
  <img width="700" height="200" src="https://github.com/japoeder/Basket-Analysis/blob/master/_plts/Department Order & Reorder Frequency.png?raw=true">
</p>

- Popular departments may want to be organized together, but in some stores they are organized so you have to pass through departments where the store wants to increase conversion.  This data can be used to support multiple strategies.

<p align="center">
  <img width="700" height="200" src="https://github.com/japoeder/Basket-Analysis/blob/master/_plts/Top Products.png?raw=true">
</p>

- Several organic items in the top selling products.

<p align="center">
  <img width="350" height="150" src="https://github.com/japoeder/Basket-Analysis/blob/master/_plts/Organic vs Inorganic Counts.png?raw=true">
  <img width="350" height="150" src="https://github.com/japoeder/Basket-Analysis/blob/master/_plts/Organic vs Inorganic Reorders.png?raw=true">
</p>

- This holds even though the number of organic products is relatively low.  Average reorder percentage is high, driving sales performance, which also tells us there should be more organic product options.

<p align="center">
  <img width="700" height="200" src="https://github.com/japoeder/Basket-Analysis/blob/master/_plts/Cart Add + Ordered x Reorder Ratio.png?raw=true">
</p>

- Plotting cart add and mean reorder ratio shows an unusual relationship. There's a concave upward relationship between 0 and 100 cart add + ordered, then the relationship becomes erratic.  Assuming most volume is done in the earlier part of the range, the relationship is generally intuitive.

<p align="center">
  <img width="700" height="200" src="https://github.com/japoeder/Basket-Analysis/blob/master/_plts/reorder_pct_x_total_orders.png?raw=true">
</p>

- There appears to be some sort of ceiling effect. I think the plot makes sense - the more orders a product has the more likely it is to be reordered.

<p align="center">
  <img width="700" height="200" src="https://github.com/japoeder/Basket-Analysis/blob/master/_plts/unique_cust_x_prod.png?raw=true">
</p>

- Cumulative total users per product vs products is interesting - 85% of customers buy ~10,000 products out of 49,688. Shelf utilization or placement optimization initiatives should consider this as well as pricing, revenue, and margin factors.

## Segmentation

<p align="center">
  <img width="500" height="200" src="https://github.com/japoeder/Basket-Analysis/blob/master/_plts/elbow.png?raw=true">
</p>


<p align="center">
  <img width="500" height="200" src="https://github.com/japoeder/Basket-Analysis/blob/master/_plts/clustering.png?raw=true">
</p>


## Basket Analysis Results

