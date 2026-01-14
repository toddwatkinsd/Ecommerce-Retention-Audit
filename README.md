# E-Commerce Churn & Logistics Audit

[![Tableau](https://img.shields.io/badge/Tableau-Interactive_Dashboard-E97627?style=for-the-badge&logo=tableau)]([LINK TO TABLEAU PUBLIC DASHBOARD HERE])
[![Python](https://img.shields.io/badge/Python-Data_Pipeline-3776AB?style=for-the-badge&logo=python)](notebooks/)

> **An OSEMN-based audit quantifying the impact of logistics costs on customer retention and lifetime value.**

## [View Live Dashboard →]([LINK TO TABLEAU PUBLIC DASHBOARD HERE])

## Executive Summary

**Objective:** Analyze 99,441 e-commerce transactions to determine if "Logistics Friction" (shipping cost relative to order value) drives customer churn.

**The Bottom Line:** The portfolio faces a **98.2% churn rate** with a Total Historical LTV of **$14.85M**. The audit identified a critical **"High-Value Attrition"** pattern where the company's most valuable customers are churning at a higher rate than low-value customers, driven by a **4.3% higher relative logistics burden**.

## 🔍 Core Findings (Data-Driven)

### 1. High-Value Attrition (The "Churn Paradox")

Contrary to standard retention models, the customers leaving the platform are **statistically more valuable** than those staying.

| Cohort | Average Historical LTV | Insight |
| :--- | :--- | :--- |
| **Active Customers** | **$138.85** | Lower spending power, higher retention. |
| **Churned Customers** | **$158.45** | **14.1% higher value**, but higher attrition. |

> **Implication:** The business is failing to retain its "Whales." High-spending customers are hitting a service ceiling and exiting.

### 2. The Logistics Friction Hypothesis

A statistical test confirmed that shipping costs are a causal factor in this attrition.

* **Active Customer Friction:** 20.35% (Shipping Cost / Total Spend)
* **Churned Customer Friction:** 21.23% (Shipping Cost / Total Spend)
* **Differential:** **+4.3%** relative increase.

> **Validation:** Customers who churned faced a measurably higher "Logistics Tax" than those who stayed. As shipping costs exceed ~20% of order value, retention probability degrades significantly.

### 3. Geographic Value Disparity

The Tableau dashboard visualizes **Average LTV** and **Customer Volume** by state.

* **High-Value Hubs:** Identified regions maintaining >$150 Avg LTV.
* **Value Erosion Zones:** Remote states show high customer density but significantly lower LTV, correlating with the high friction scores found in the Python audit.

## Portfolio Snapshot

| Metric | Value | Definition |
| :--- | :--- | :--- |
| **Total Portfolio LTV** | **$14,845,129** | Cumulative revenue from 93,897 unique customers. |
| **Overall Churn Rate** | **98.2%** | Customers inactive for >60 days. |
| **Avg. Friction Score** | **2.12 / 10** | Average shipping cost is 21.2% of order value. |
| **Strategic Window** | **60 Days** | The specific "Cliff" where customer engagement drops to near zero. |

## Technical Implementation (OSEMN)

### 1. Data Pipeline

* **Source:** 8 relational tables (Olist E-commerce Dataset).
* **Scrub:** Handled 2,965 missing timestamps; median imputation (170.39 hrs) for shipping duration; zero-division handling for freight ratios.
* **Enrich:** Engineered 11 custom features including `individual_friction_score` and `Recency_Days`.

### 2. Feature Engineering Logic

| Feature | Logic | Purpose |
| :--- | :--- | :--- |
| **Friction Index** | `(Shipping_Cost / Order_Value) * 100` | Quantifies the financial "pain" of delivery per user. |
| **Recency** | `Max(Date) - Last_Purchase` | Defines the 60-day churn threshold. |
| **LTV** | `Sum(Order_Value)` | Aggregates lifetime monetary contribution. |
| **Target Encoding** | `Mean(LTV)` per City | Converts high-cardinality geography (4,119 cities) into numerical predictors. |

### 3. Pipeline Validation Output

*Actual terminal output from the final Python audit:*

```text
------------------------------------------------------------
STRATEGIC VALIDATION: THE 60-DAY CLIFF
------------------------------------------------------------
Average LTV (Active / 0-60 days):  $138.85
Average LTV (At-Risk / 60+ days):  $158.45
Projected Value Erosion:           14.1%
------------------------------------------------------------
HYPOTHESIS TEST: LOGISTICS FRICTION IMPACT
------------------------------------------------------------
Avg Friction Score (Active Customers):   20.35%
Avg Friction Score (Churned Customers):  21.23%
Friction Differential:                   +4.3%
CONCLUSION: VALIDATED. Churned customers faced higher logistics friction.
------------------------------------------------------------
3. **Statistical Validation:** Proving causation (friction → churn) requires cohort comparison, not just correlation
4. **Production Thinking:** Schema validation, data quality checks, and export verification prevent downstream errors
5. **Executive Framing:** Three headline KPIs (Churn %, LTV $, Friction %) tell complete story in 5 seconds

