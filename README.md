# Retail-Strategy-and-Analytics

## QVI Chip Category Analysis

Retail analytics project examining customer purchasing behaviour for the chips category, using transaction and loyalty data. The goal is to identify which customer segments drive sales, understand what's behind those numbers, and provide targeting recommendations.

## Overview

This project cleans, merges, and analyses two datasets — store transaction data and customer loyalty/segmentation data — to answer:

- Which customer segments generate the most total sales?
- Which segments are the most valuable on a per-customer basis?
- Does pack size preference vary by segment?
- Does brand preference vary by segment?
- Who should be prioritised for targeted marketing?

## Data

| File | Description |
|------------------------------------|------------------------------------|
| `QVI_transaction_data.xlsx` | Raw transaction-level data: date, store, loyalty card, product, quantity, and sales value |
| `QVI_purchase_behaviour.csv` | Customer-level data: loyalty card number, lifestage, and premium customer tier |

## Project Structure

```         
├── QVI_category_analysis.ipynb          # Main analysis notebook
├── QVI_transaction_data.xlsx            # Raw transaction data (input)
├── QVI_purchase_behaviour.csv           # Raw customer data (input)
├── QVI_transaction_data_clean.csv       # Cleaned transaction data (output)
├── QVI_merged_data.csv                  # Cleaned, merged, analysis-ready dataset (output)
├── sales_by_segment.csv                 # Total sales by lifestage x premium segment
├── segment_summary_avg_spend_units.csv  # Avg spend/units per customer by segment
├── pack_size_by_segment.csv             # Avg pack size by segment
├── older_families_brand_affinity.csv    # Brand affinity index, Older Families
├── young_families_brand_affinity.csv    # Brand affinity index, Young Families
├── sales_by_segment.png                 # Chart: total sales by segment
├── avg_spend_per_customer.png           # Chart: avg spend per customer by segment
├── older_families_brand_affinity.png    # Chart: brand affinity, Older Families
└── README.md
```

## Setup

``` bash
pip install pandas numpy matplotlib seaborn openpyxl
```

Open `QVI_category_analysis.ipynb` in Jupyter Notebook or JupyterLab and run all cells in order.

## Methodology

### 1. Data Cleaning — Transactions

- Removed a loyalty card with two 200-packet, \$650 transactions — a commercial/bulk buyer, not a representative household shopper
- Converted `DATE` from Excel serial number to proper datetime
- Confirmed the only missing calendar date (25 Dec) is a store-closure day, not a data error
- Removed non-chip products (salsa/dip jars) identified via product naming and pack-size patterns, while retaining genuine chip flavour variants
- Extracted `PACK_SIZE` from product names
- Extracted and standardised `BRAND` from product names, consolidating naming inconsistencies (e.g. "Dorito"/"Doritos", "WW"/"Woolworths", "NCC"/"Natural Chip Co")

### 2. Data Cleaning — Customers

- Verified no nulls and no duplicate loyalty cards
- Confirmed 7 lifestage categories and 3 premium customer tiers, consistently labelled

### 3. Merge

- Left-joined transactions to customers on `LYLTY_CARD_NBR`
- Verified row count was preserved and no nulls were introduced, confirming a clean 1:1 match

### 4. Analysis

- Total sales by lifestage x premium customer segment
- Average spend and units purchased per customer, to separate segment size from segment value
- Average pack size by segment
- Brand affinity analysis (segment purchase share vs. rest-of-population purchase share) to identify genuine brand preferences, rather than segments simply favouring the overall best-selling brand

## Key Findings

- **Highest total sales** come from Older Families/Budget, Young Singles-Couples/Mainstream, and Retirees/Mainstream — but this is driven mainly by large customer counts, not high spend per customer.
- **Highest value customers**: Older and Young Families spend \~\$32–35 and buy \~8.6–9.3 units per customer — nearly double that of Young Singles/Couples (\~\$15–19, \~4.3–4.6 units).
- **Pack size** is not a meaningful differentiator between segments (\~173–178g average across all groups).
- **Brand preference is a meaningful differentiator**: Families (Older and Young) consistently favour value/everyday brands (Woolworths, Red Rock Deli, Sunbites, CCs, Natural Chip Co) and under-index on premium/mainstream leaders (Kettle, Pringles, Doritos, Tostitos).

## Recommendation

Prioritise **Families** (Older and Young) for targeted marketing, promoting value-oriented, everyday snack brands that already align with their purchasing behaviour. Treat **Young Singles/Couples** as a high-volume but lower-value segment, better suited to lower-cost engagement (e.g. loyalty app promotions) than premium campaign investment.

# Trial Store Performance Assessment Report
This report evaluates the performance of the trial stores by comparing each trial location
with a carefully selected control store. The objective is to determine whether the in-store trial
had a measurable impact on sales performance during the trial period and to provide
evidence-based recommendations for future implementation.

## Methodology

To ensure a fair comparison, a suitable control store was identified for each trial store using
historical pre-trial performance. Control stores were selected based on the following criteria:
Similarity in monthly sales trends, measured using the Pearson correlation coefficient.
Similarity in sales magnitude, measured using Euclidean distance.

A combined similarity score derived from both correlation and magnitude similarity to
identify the most appropriate control store.
Once the control stores were selected, their sales were scaled to match the pre-trial
performance of the corresponding trial stores. This adjustment ensured that any observed
differences during the trial period reflected the impact of the trial rather than underlying
differences in store size or historical performance.
The effectiveness of each trial was assessed by:
Comparing monthly sales between the trial and scaled control stores.
Calculating percentage uplift during the trial period.
Measuring normal pre-trial variation using the standard deviation of historical
differences.
Assessing statistical significance to determine whether observed changes exceeded
normal business variation.

## Results

**Trial Store 77**
Selected Control Store: Store 233
Insert monthly sales comparison chart here.
7/2/26, 6:22 PM Untitled
file:///C:/Users/USER/Downloads/Untitled.html 1/20
The pre-trial analysis identified Store 233 as the most appropriate control store due to its
high similarity in both sales pattern and sales magnitude. During the trial period, Store 77
recorded substantial improvements in sales, particularly in March and April 2019. Statistical
analysis indicated that these increases exceeded normal pre-trial variation, suggesting that
the trial had a positive and statistically significant impact on store performance.
## Recommendation
The trial at Store 77 was successful. Consider extending similar initiatives
to comparable stores.

**Trial Store 86**
Selected Control Store: Store 155
Insert monthly sales comparison chart here.
Store 155 was selected as the control store based on the highest combined similarity score.
The performance of Store 86 was evaluated by comparing its trial-period sales with the
scaled control store and assessing whether any observed uplift was statistically significant.
## Recommendation
Based on the analysis results, determine whether the trial delivered a
significant improvement in performance and recommend continuation or further
investigation accordingly.

**Trial Store 88**
Selected Control Store: Store 125
Insert monthly sales comparison chart here.
Store 125 was identified as the best available control store for Store 88. Although it provided
the highest combined similarity score, the similarity was lower than that observed for the
other trial stores. Consequently, the findings for Store 88 should be interpreted with
appropriate caution while assessing the effectiveness of the trial.
## Recommendation
Base the recommendation on the observed trial performance while
acknowledging the relatively lower similarity between the trial and control stores.

# Overall Conclusion
The analysis compared each trial store with a carefully selected control store using historical
sales performance. Statistical testing was used to distinguish genuine trial effects from
normal business variation. The findings provide evidence-based recommendations regarding
the effectiveness of the trial at each location and support informed decision-making on
whether the initiative should be expanded to additional stores.

