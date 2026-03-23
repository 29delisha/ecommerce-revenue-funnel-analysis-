# E-Commerce Revenue Drop & Conversion Funnel Analysis

**Tools:** Python · SQL (Pandas) · Gemini API · Statistical Testing · Tableau Public  
**Dataset:** Olist Brazilian E-Commerce (99,992 orders, Kaggle)  
**Tableau Dashboard:** https://public.tableau.com/app/profile/delisha.lakhanpal/viz/Book1_17741660524630/Dashboard1

---

## Project Summary

End-to-end analysis of a Brazilian e-commerce platform covering revenue trends,
conversion funnel drop-off, geographic cohort performance, payment behaviour,
and category-level satisfaction. Includes an AI-augmented insight layer using
Gemini API, with a structured human validation step that identified where AI
outputs were incorrect or incomplete.

---

## Key Findings

**Funnel:**
- Biggest drop-off at Placed→Approved (-1.25%) driven by credit card 
  payment failures (70% of approval failures)
- Last-mile delivery failures concentrated in RJ (2.41% failure rate 
  vs SP's 0.86%) — 2.8x worse, indicating a carrier-level problem

**Geographic Cohort (statistically significant, p < 0.001):**
- RJ delivery rate (96.06%) significantly worse than SP (97.02%)
- RJ + BA combined revenue at risk: R$107,543 across 634 failed deliveries
- Higher freight cost negatively correlates with review score (r = -0.090)

**Payment Cohort (statistically significant, p < 0.001):**
- Credit card AOV (R$166.45) significantly higher than boleto (R$144.99)
- Boleto cancellation rate (0.48%) is LOWER than credit card (0.58%) — 
  contrary to common assumption, boleto users show stronger purchase intent

**Category Analysis:**
- office_furniture: highest AOV (R$268) but 1.8x more low-rating reviews 
  than national average (22.4% vs 12.7%)
- watches_gifts: R$732,577 revenue upside if order volume matched 
  health_beauty at its own AOV

---

## AI-Augmented Layer

Used Gemini API (gemini-2.5-flash) to generate business recommendations
from verified Python-computed metrics. Key validation findings:

| AI Claim | Validation Result |
|----------|------------------|
| Boleto conversion is counterintuitive due to low conversion | INCORRECT — boleto cancellation rate is lower than credit card |
| Focus payment audit on boleto abandonment | INCORRECT — 70% of approval failures are credit card, not boleto |
| RJ/BA logistics improvement needed | CONFIRMED — statistically significant (p < 0.001) |
| Office furniture quality review needed | CONFIRMED — 1.8x worse than national avg |
| Watches & gifts is growth opportunity | CONFIRMED — R$732K revenue upside quantified |

---

## Statistical Tests Performed

All tests significant at p < 0.001:
1. SP vs RJ delivery rate — two-proportion z-test (z = 5.42)
2. SP vs RJ review scores — independent t-test (t = 22.06)
3. Freight cost vs review score — Pearson correlation (r = -0.090)
4. Credit card vs boleto AOV — independent t-test (t = 12.16)

---

## Project Structure
```
ecommerce_project/
├── data/
│   ├── [Olist CSV files]
│   └── tableau_exports/
│       ├── 01_monthly_revenue.csv
│       ├── 02_funnel.csv
│       ├── 03_state_cohort.csv
│       ├── 04_payment_cohort.csv
│       ├── 05_category_performance.csv
│       └── 06_orders_delivered.csv
└── notebooks/
    └── ecommerce_analysis.ipynb
```

---

## How to Run

1. Download the Olist dataset from Kaggle
2. Place CSV files in `data/` folder
3. Install requirements: `pip3 install pandas numpy matplotlib seaborn plotly scipy statsmodels google-generativeai`
4. Add your Gemini API key in the notebook
5. Run all cells in `ecommerce_analysis.ipynb`
```

Save the file. Then push to GitHub:
```
cd ~/Desktop/ecommerce_project
git init
git add .
git commit -m "E-commerce revenue and funnel analysis with AI-augmented insights"
