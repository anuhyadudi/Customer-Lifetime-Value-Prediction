# 🛒 Customer Lifetime Value (CLV) Segmentation

> Predicting which customers will generate the most 
revenue in the next 6 months using XGBoost + 
LightGBM ensemble and SHAP explainability.


## 📌 Problem Statement
We currently cannot identify which customers are 
likely to generate the most revenue in the next 
6 months — limiting our ability to target marketing 
campaigns — resulting in missed revenue opportunities 
and wasted marketing spend.

---

## 🧹 Data Cleaning Decisions

| Issue | Action | Justification |
|-------|--------|---------------|
| 22.8% missing CustomerID | Dropped | Guest checkouts — cannot track CLV |
| Negative quantities | Removed | Product returns distort monetary value |
| Zero price items | Removed | Non-revenue transactions |
| Top 1% spenders | Capped at P99 | Wholesale buyers don't represent retail CLV |

---

## ⚙️ Feature Engineering — RFM

| Feature | Definition | Direction |
|---------|-----------|-----------|
| Recency | Days since last purchase | Lower = Better |
| Frequency | Unique transactions | Higher = Better |
| Monetary | Total spend | Higher = Better |

---

## 👥 CLV Tier Profiles

| Tier | Count | Avg Recency | Avg Frequency | Avg Spend |
|------|-------|-------------|---------------|-----------|
| High Value | 1,705 (29%) | 37 days | 12.8 trips | $5,188 |
| Mid Value | 2,367 (41%) | 168 days | 3.5 trips | $1,141 |
| At Risk | 1,747 (30%) | 412 days | 1.2 trips | $303 |

> High Value customers buy 10x more frequently, 
visit 11x more recently, and spend 17x more 
than At Risk customers.

---

## 🤖 Model Results

| Model | Accuracy | High Value Precision |
|-------|----------|---------------------|
| XGBoost | 95.96% | 0.98 |
| LightGBM | 95.88% | 0.98 |
| **Ensemble** | **96.05%** | **0.99** |

---

## 🔍 SHAP Analysis

**Top feature importance:**
Frequency    → 6.2 impact (most predictive)
Recency      → 4.6 impact
Monetary     → 4.0 impact

> Purchase frequency is **1.55x more predictive** 
than monetary value — customers who buy regularly 
are more valuable than one-time big spenders.

**High Value customer explanation:**
- Recency = 14 days → +2.64 contribution
- Frequency = 8 transactions → +2.27 contribution
- Behavioral patterns drive classification 
  more than raw spend

**At Risk customer explanation:**
- Recency = 725 days → +3.25 contribution
- Frequency = 3 → -1.90 (fighting against At Risk)
- Prior purchase history suggests win-back potential

---

## ✅ Business Recommendations

**High Value (29% of customers):**
Loyalty rewards, early product access, 
premium service — retain and increase frequency

**Mid Value (41% of customers):**
Personalized recommendations based on 
purchase history — goal: push to High Value tier

**At Risk (30% of customers):**
- Frequency > 2 → Win-back campaign 
  ("We miss you — 20% off")
- Frequency = 1 → New offer campaign 
  (needs stronger incentive)

---

## 🧰 Tech Stack
- **Python** — Pandas, NumPy, Scikit-learn
- **Models** — XGBoost, LightGBM
- **Explainability** — SHAP
- **Visualization** — Matplotlib, Seaborn
