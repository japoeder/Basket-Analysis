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

Customer segmentation is a strategic approach to divide a customer base into distinct groups that share similar characteristics, allowing for targeted marketing strategies and personalized customer experiences. By understanding the purchase behaviors and product preferences of these groups, businesses can tailor their offerings to meet the specific needs and desires of each segment.

To handle the complexity of thousands of products and customers, product categories, represented by aisles, serve as a practical proxy for detailed segmentation. This categorization simplifies the segmentation process without losing the granularity needed for effective personalization.

The refined segmentation strategy leveraged here can enable a companto to engage with their customers more effectively, crafting marketing campaigns and product development that resonate with the distinct purchasing patterns identified through this data-driven approach.

<p align="center">
  <img width="500" height="200" src="https://github.com/japoeder/Basket-Analysis/blob/master/_plts/elbow.png?raw=true">
</p>

The Elbow Method is a technique used to determine the appropriate number of clusters by plotting the explained variance against the number of clusters and identifying the point where the increase in variance explained by additional clusters diminishes, often referred to as the "elbow." In this analysis, five clusters were identified as optimal, suggesting a clear distinction among different customer purchasing behaviors.

<p align="center">
  <img width="500" height="200" src="https://github.com/japoeder/Basket-Analysis/blob/master/_plts/clustering.png?raw=true">
</p>

Principal Component Analysis (PCA) is leveraged to condense the high-dimensional data into a more manageable form, addressing the challenge that KMeans clustering faces in higher-dimensional spaces. By transforming the data into 10 principal components, the most significant variance is captured, facilitating more accurate clustering.

Finally, the clustering results into 5 neat clusters and after checking most frequent products in them, we can conclude following:

- Cluster 1 includes 55356 consumers who exhibit preferences for fresh vegetables followed by fruits.
- Cluster 2 includes 5369 consumers who exhibit preferences for water seltzer sparkling water aisle.
- Cluster 3 includes 38887 consumers who exhibit preferences for fruits followed and fresh vegetables.
- Cluster 4 includes 98639 consumers who don't exhibit clear preferences for any category. Their average orders are relatively low, so either they don't use Instacart regularly or they are new. 
- Cluster 5 includes 7958 consumers  who exhibit preferences for packaged produce and fresh fruits.

## Basket Analysis Results

Market Basket Analysis (MBA) is a data mining technique used to uncover associations between items within large datasets, commonly used in retail to discover frequent item sets or combinations of items purchased together. It’s most famously applied in the context of shopping transactions to identify patterns of products that frequently co-occur in shopping baskets, but its applications extend to any domain where understanding item association is beneficial, such as content recommendation, cross-selling strategies, and inventory management.

### Key Concepts

- **Association Rules**: The core of MBA revolves around finding association rules, which are implication expressions of the form *X* ⇒ *Y*, where *X* and *Y* are disjoint item sets. The rule suggests that when items in *X* are purchased, items in *Y* are also likely to be purchased.
- **Support**: This metric measures the proportion of transactions in the dataset that contain a specific item set. It helps in identifying the most common item combinations.
- **Confidence**: Confidence measures how often items in *Y* are purchased when items in *X* are purchased, providing insight into the reliability of the inference made by a rule.
- **Lift**: Lift indicates the strength of a rule over the random co-occurrence of *X* and *Y*, with a lift value greater than 1 suggesting a strong rule.

### Process Overview

1. **Data Collection and Preparation**: The first step involves collecting transaction data and organizing it in a format suitable for analysis, typically a transaction-item matrix.

2. **Frequency Analysis**: Identifying frequent individual items or item sets that meet a minimum support threshold.

3. **Rule Generation**: Generating association rules from the frequent item sets. This involves calculating metrics like support, confidence, and lift to evaluate the strength and usefulness of the rules.

4. **Rule Pruning and Selection**: Filtering out rules that do not meet the minimum criteria for the metrics of interest, leaving only the most potentially valuable associations.

### Applications

- **Cross-Selling and Upselling**: Identifying products to promote together based on their likelihood of being purchased together.
- **Store Layout Optimization**: Organizing shelves and aisles in a way that maximizes cross-category purchases.
- **Targeted Marketing**: Developing promotions and offers for specific customer segments based on their buying patterns.
- **Inventory Management**: Understanding product affinities can help in optimizing stock levels and reducing inventory costs.
- **Product Bundling**: Creating product bundles that are likely to be purchased together, enhancing value for customers and increasing sales.

### Tools and Techniques

Market Basket Analysis can be performed using various statistical software and programming languages equipped with data mining capabilities, such as R (using the `arules` package) and Python (using libraries like `mlxtend`).

### Challenges

- **Data Volume and Quality**: MBA requires access to large transactional datasets, and the quality of insights is directly related to the quality of the underlying data.
- **Computational Complexity**: As the number of items in the dataset grows, the computational complexity of finding frequent item sets and generating rules increases exponentially.
- **Dynamic Patterns**: Consumer behavior and item associations can change over time, necessitating regular updates to the analysis to keep insights current.

By leveraging the Mlxtend Python library's Apriori algorithm, I identified significant associations among the top 100 most frequently purchased products, yielding 28 pairs of products (or 56 rules) with a lift greater than 1. This analysis highlights the top 10 product pairs with the highest lift, demonstrating the powerful insights Market Basket Analysis can provide in understanding and influencing consumer purchasing decisions.

| Product A  | Product B | Lift |
| ------------- | ------------- | ---- |
| Organic Yellow Onion  | Organic Garlic  | 3.70 |
| Limes | Large Lemon | 2.66 |
| Organic Lemon | Organic Hass Avocado  | 2.36 |
| Organic Raspberries | Organic Strawberries  | 1.95 |
| Organic Avocado | Large Lemon  | 1.88 |
| Organic Strawberries | Organic Blueberries  | 1.87 |
| Limes | Organic Avocado  | 1.85 |
| Organic Hass Avocado | Organic Raspberries  | 1.84 |
| Organic Large Extra Fancy Fuji Apple | Bag of Organic Bananas  | 1.71 |
| Banana | Organic Fuji Apple  | 1.67 |