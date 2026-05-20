# Capstone Project Summary

---

## 1. Problem Statement

**Which customer segments and marketing channels drive the highest revenue and lowest return rates, and what actions should the business take to maximise profitable growth?**

The analysis was conducted for marketing and sales leadership to guide budget allocation across customer acquisition and retention programmes.

---

## 2. Dataset Used

| Attribute | Detail |
|---|---|
| File | `capstone_dataset.csv` |
| Rows | 500 transactions |
| Columns | 13 |
| Date range | January 2025 – January 2026 |
| Unique customers | 472 |
| Customer segments | New, Returning, VIP |
| Marketing channels | Paid Search, Social Media, Direct, Organic Search, Email, Referral |
| Product categories | Beauty, Books, Electronics, Clothing, Home & Garden, Sports |
| Regions | Central, North, East, West, South |
| Total estimated revenue | $384,349 |

Missing values were limited to `customer_satisfaction` (10 rows) and `discount_applied` (5 rows) — both handled during cleaning.

---

## 3. Main Analysis Steps

1. **Data loading and inspection** — confirmed 500 rows, 13 columns, no duplicates, minimal missing values
2. **Data cleaning** — converted `date` to datetime, imputed missing satisfaction scores with median, standardised column names, cast `returned` to integer
3. **Feature engineering** — created `estimated_revenue` (price × quantity × (1 − discount)) and `discount_pct` for readability
4. **Univariate analysis** — revenue distribution (right-skewed, majority under $1,000), customer segment counts (Returning 42%, New 41.4%, VIP 16.6%)
5. **Group-based analysis** — average revenue and return rates across customer segments, marketing channels, and product categories
6. **Relationship analysis** — segment × channel heatmap of return rates; revenue vs return rate scatter plot by channel
7. **Combined segment × channel summary table** — identified the highest and lowest performing acquisition combinations

---

## 4. Key Insights

### Insight 1 — VIP customers are the most capital-efficient segment but are under-utilised
VIP customers return products at only **3.6%** — less than half the business average of 7.2% — while generating **$771 average revenue per transaction**. Despite this, VIP accounts for only **83 of 500 transactions (16.6%)**, making them the smallest segment by volume. Returning customers, the largest segment (42%), carry the highest return rate at **9.1%**, making them the most costly segment to serve.

### Insight 2 — Paid Search is the strongest channel; Direct is a hidden margin risk
Paid Search generates the highest average revenue (**$851**) at only a **4.9% return rate** — well below the 7.2% average. The Direct channel is the inverse: below-average revenue (**$763**) with the highest return rate of any channel (**10.5%**) — more than double Paid Search. The Returning + Direct combination is the single worst performer across all 18 segment × channel combinations: **$644 average revenue and a 15.4% return rate**.



## 5. Recommendations

| Priority | Action | Based On |
|---|---|---|
| 1 | Launch a VIP retention programme (loyalty rewards, early access, personalised offers) to increase VIP transaction share from 16.6% | Insight 1 |
| 2 | Reallocate budget from Direct and Referral channels to Paid Search and Social Media | Insight 2 |


---

## 6. Limitations

- **Sample size:** 500 transactions from 472 customers is a relatively small dataset. Segment-level findings (especially VIP with only 83 transactions) may not be statistically robust.
- **No time-series analysis:** The dataset spans a full year but no seasonal or trend analysis was performed. Revenue or return patterns may shift by quarter.
- **Return reason unknown:** The dataset records whether an item was returned but not why. It is not possible to determine whether returns are driven by product quality, customer expectations, or channel-specific issues without this data.
- **Causality cannot be established:** The analysis identifies correlations (e.g. Paid Search customers return less) but cannot confirm whether the channel itself causes better behaviour, or whether a different type of customer self-selects into that channel.
- **Customer satisfaction imputation:** 10 missing satisfaction scores were filled with the median. This slightly compresses the distribution and may mask dissatisfied customers.

---

## 7. Future Work

- **Collect return reason data** to move from correlation to root-cause analysis, particularly for the Direct channel
- **Expand the dataset** to 2,000+ transactions to improve statistical confidence in segment-level findings, especially for VIP
- **Time-series analysis** to identify seasonal patterns — e.g. whether return rates spike post-holiday or revenue peaks in specific months
- **Customer lifetime value modelling** — link `customer_id` across transactions to calculate true LTV per segment, not just per-transaction averages
- **A/B test channel reallocation** — run a controlled experiment shifting a portion of Direct budget to Paid Search to validate the revenue and return rate projections from this analysis
- **Predictive model** — build a logistic regression to predict return probability at point of transaction using segment, channel, discount, and product category as features
