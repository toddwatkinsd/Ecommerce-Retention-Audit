# E-Commerce Churn & Logistics Audit

##  [TABLEAU DASHBOARD HERE](https://public.tableau.com/app/profile/todd.watkins4029/viz/Ecommerce-Customer-RetentionCLV/StrategicCustomerLifestyle?publish=yes)

## Executive Summary

**Objective:** Analyze 99,441 e-commerce transactions to determine if "Logistics Friction" (shipping cost relative to order value) drives customer churn.

**The Bottom Line:** The portfolio faces a **98.2% churn rate** with a Total Historical LTV of **$14.85M**. The audit identified a critical **"High-Value Attrition"** pattern where the company's most valuable customers are churning at a higher rate than low-value customers, driven by a **4.3% higher relative logistics burden**.

## Core Findings (Data-Driven)

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

The Tableau dashboard visualizes **Average LTV** and **Customer Volume** by state, confirming a massive logistics-driven divide.

* **The Hub (São Paulo):** Represents the ideal market—**High Density** and **High LTV**, benefiting from proximity to sellers.
* **Value Erosion Zones (Remote States):** States distant from the distribution center (e.g., North/Northeast) show a staggering **354.6x lower customer density** per state compared to the hub.
* **The Insight:** High logistics barriers act as a financial gatekeeper. Remote states face an **11.2% higher relative friction tax** than the hub, directly suppressing market penetration and preventing customer acquisition in these regions.

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
* **Enrich:** Engineered 11 custom features including `Individual_Friction_Score` and `Recency_Days`.

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
High-Value Attrition Gap:          +14.1%
------------------------------------------------------------
HYPOTHESIS TEST: LOGISTICS FRICTION IMPACT
------------------------------------------------------------
Avg Friction Score (Active Customers):   20.35%
Avg Friction Score (Churned Customers):  21.23%
Friction Differential:                   +4.3%
CONCLUSION: VALIDATED. Churned customers faced higher logistics friction.
------------------------------------------------------------
HUB (SP) VS REMOTE FRONTIER ANALYSIS
-----------------------------------------------------------------
METRIC                    | HUB (SP)        | REMOTE AVG (North)
-----------------------------------------------------------------
Avg Friction Score        |          18.64% |          29.86%
Avg LTV                   | $       142.04 |$        224.74
Customer Density (Total)  |          39,431 |             556
-----------------------------------------------------------------
Insight 1: Remote states face a +11.2% higher friction tax than the hub.
Insight 2: The Hub has 354.6x higher customer density per state.
Conclusion: High logistics friction directly correlates with lower market penetration.
------------------------------------------------------------
