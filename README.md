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
