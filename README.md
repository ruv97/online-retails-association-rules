# Online Retail Association Rules

This project applies market basket analysis and association rule mining to discover purchasing patterns in online retail transactions. By identifying which items are frequently bought together, retailers can optimize bundling strategies, personalized recommendations, and inventory management.

## Table of Contents

- [Project Overview](#project-overview)
- [Objectives](#objectives)
- [Dataset](#dataset)
- [Methodology](#methodology)
- [Key Results](#key-results)
- [Recommendations](#recommendations)
- [Technical Stack](#technical-stack)

## Project Overview

This analysis focuses on discovering strong association rules from online retail transaction data covering international customers. The project uses the Apriori algorithm to identify meaningful product co-purchase patterns that can drive strategic business decisions.

## Objectives

The primary objectives of this analysis are:

1. **Product Bundling**: Understand which items are frequently co-purchased to create strategic product bundles. Online retailers with heavy-buying customers exhibit different structural patterns that have important strategic value.

2. **Cross-Sell Recommendations**: Identify items that exhibit strong positive cross-correlations to enable dynamic product recommendations (e.g., "Frequently bought together") on product pages, facilitating effortless cross-selling.

3. **Personalized Marketing**: Enable highly personalized, volume-tiered email promotions tailored to specific operational niches of wholesale customers by identifying their unique purchasing patterns.

## Dataset

### Data Source
- **Size**: 541,909 transaction records covering international transactions
- **File**: `Online_Retail.csv`

### Data Schema
- `InvoiceNo`: Transaction identifier (character)
- `StockCode`: Product code (character)
- `Description`: Product description (character)
- `Quantity`: Units purchased (integer)
- `InvoiceDate`: Transaction date and time (datetime)
- `UnitPrice`: Price per unit (numeric)
- `CustomerID`: Customer identifier (character)
- `Country`: Country of transaction (character)

### Data Preprocessing

The raw data was cleaned using the following steps:

- **Geographic Filtering**: Filtered to include only transactions from the United Kingdom
- **Transaction Removal**: Removed cancelled transactions (identified by invoice numbers starting with 'C')
- **Data Validation**: 
  - Removed non-product codes (POST, DOT, M, BANK CHARGES, PADS)
  - Removed records with missing customer IDs or product descriptions
  - Filtered for positive quantities and unit prices
- **Text Cleaning**: Trimmed whitespace from product descriptions
- **Aggregation**: Aggregated transactions into basket format grouped by invoice number

## Methodology

### Rule Mining Process

The analysis employs the **Apriori algorithm** to discover association rules through iterative exploration cycles:

#### Cycle 1 (Exploratory)
- **Support Threshold**: 0.005 (items appearing in at least 0.5% of baskets)
- **Confidence Threshold**: 0.5 (50% predictive reliability)
- **Purpose**: Broad exploration to identify initial patterns and trends

#### Cycle 2 (Refinement)
- **Support Threshold**: 0.01 (items appearing in at least 1% of baskets)
- **Confidence Threshold**: 0.6 (60% predictive reliability)
- **Purpose**: Reduce noise and prioritize stronger relationships with higher operational certainty

### Rule Quality Assurance

- **Redundancy Pruning**: Rules that are subsets of broader, more impactful rules with lower lift are automatically pruned to ensure distinct, actionable insights

### Required Libraries

```r
library(tidyverse)      # Data manipulation and visualization
library(arules)         # Association rule mining
library(arulesViz)      # Rule visualization
```

## Key Results

The analysis produces association rules evaluated on three key metrics:

### Evaluation Metrics

- **Support**: The absolute popularity of the rule (proportion of transactions containing both items)
- **Confidence**: The predictive reliability of the rule (conditional probability of consequent given antecedent)
- **Lift**: The strength of the rule over random coincidence (values > 1 indicate strong positive dependency)

### Top Rules

The refined Cycle 2 analysis discovered high-yield association rules with strong lift values, surfacing tight, actionable insights into product co-purchase patterns.

Output file: `discovered_association_rules.csv`

## Recommendations

Based on the high-yield rules uncovered, the retailer should implement the following strategic changes:

### 1. Strategic Virtual Bundling (Cross-Category Pairs)
Create themed product bundles containing highly correlated items (e.g., "Regency High-Tea Set" or "Gardener's Comfort Set"). Offer these bundles at a discount to incentivize larger basket sizes and increase average order value.

### 2. Dynamic Recommendations and UI Design
Implement hard-coded dynamic recommendation blocks on product pages. When a customer adds a high-confidence antecedent product (e.g., GREEN REGENCY TEACUP) to their cart, display an interstitial recommendation for the associated consequent product, driving impulse purchases.

### 3. Inventory Allocation Syncing
Tie warehouse inventory alerts together for coupled items. Since these products sell in tandem, coordinate stock management to prevent out-of-stock scenarios that could disrupt the entire bundle (e.g., if ALARM CLOCK BATTERY runs out, customers interested in the associated product may abandon their purchase).

## Technical Stack

- **Language**: R
- **Data Analysis**: tidyverse, arules, arulesViz
- **Output Format**: CSV (transaction and rule data)
- **Documentation**: R Markdown

## Files

- `Assignment-1.Rmd`: Complete R Markdown analysis with code and output
- `market_basket_transactions.csv`: Aggregated basket format transaction data
- `discovered_association_rules.csv`: Final pruned association rules with metrics
- `Online_Retail.csv`: Raw transaction data (not included in repo)

---

**Analysis Date**: 2026-07-03  
**Student ID**: 24440622
