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
├── _plts/                                      : Data visualization 
├── 1) EDA
├── 2) D             : EDA to analyze customer purchase pattern
├── Customers Segmentation.ipynb                : Customer Segmentation based on product aisles
├── Market Basket Analysis.ipynb                : Market Basket Analysis to find products association
├── Feature Extraction.ipynb                    : Feature engineering and extraction for a ML model
├── Data Preparation.ipynb                      : Data preparation for modeling
├── ANN Model.ipynb                             : Neural Network model for product reorder prediction
├── XGBoost Model.ipynb                         : XGBoost model for product reorder prediction
├── LICENSE                                     : License
└── README.md                                   : Project Report 
```
<br />