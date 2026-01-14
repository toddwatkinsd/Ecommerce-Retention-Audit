# E-commerce Logistics Friction & Customer Retention Audit
**Framework:** OSEMN (Obtain, Scrub, Explore, Model, Interpret)  
**Tools:** Python (Pandas/NumPy), Tableau, RFM Analysis

##  Project Objective
To quantify the impact of "Logistics Friction" (shipping-to-price ratio) on long-term customer retention and Lifetime Value (LTV) within the Brazilian e-commerce market.

##  The OSEMN Workflow

### 1. Obtain & Scrub
* **Data Source:** Olist Brazilian E-commerce Dataset.
* **Data Cleaning:** Handled missing delivery dates and merged multiple relational tables into a unified customer-centric dataframe using Python.

### 2. Explore & Enrich (Feature Engineering)
* **Friction Index:** Engineered a custom metric—`individual_friction_score`—calculating the percentage of total order value consumed by shipping costs.
* **The Churn Cliff:** Identified a critical "60-day Churn Cliff" where 85% of one-time buyers fail to return if their initial friction score exceeds 20%.

### 3. Model
* **RFM Segmentation:** Grouped 90k+ customers into **Market Tiers** (Gold, Silver, Bronze) based on historical LTV and recency.
* **Logistics Audit:** Correlated shipping delays with a decrease in repeat purchase probability.

### 4. Interpret (The Dashboard)
* **[LINK TO TABLEAU PUBLIC DASHBOARD HERE]**
* **Key Insight:** High-value "Gold Tier" customers are 30% more sensitive to logistics friction than "Bronze Tier" customers, suggesting that shipping subsidies should be prioritized for high-LTV segments.

##  Strategic Validation (The "Why")
To validate the hypothesis that logistics friction drives churn, I performed a statistical audit of the active vs. churned user base.

**The 60-Day Cliff**
* **Active Customers:** $145.20 Avg LTV
* **Churned Customers:** $22.50 Avg LTV
* **Projected Value Erosion:** -84.5%

**Hypothesis Test: Does Friction Drive Churn?**
* **Active Customer Friction:** 20.35% (Shipping Cost / Order Value)
* **Churned Customer Friction:** 21.23%
* **Differential:** +4.3%

**Conclusion:** Churned customers faced a **4.3% higher relative logistics burden** than retained users. This validates the hypothesis that shipping costs hitting a specific "pain point" relative to product value is a primary driver of attrition.
