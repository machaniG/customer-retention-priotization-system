# Strategic Case Study: Customer Retention & Revenue Protection 

## Executive Summary

Senior executives frequently face a major frustration with enterprise data science: Great insights, but how does this help my team close more sales or save more revenue today? To solve this execution gap, I built a decision engine that transforms complex customer data into immediate, prioritized retention actions. By combining advanced customer valuation, churn risk modeling, and localized AI, the system identifies, quantifies, and ranks exactly which accounts customer-facing teams must contact first to maximize revenue protection.


## The Business Execution Gap

Most companies suffer from fragmented customer data insights and struggle to turn data analytics into bottom-line financial results:

- **The "Dashboard Blindness" Gap:** Teams look at churn charts but do not know which specific customer to call today.

- **Misaligned Priorities:** Marketing budgets are wasted chasing high-churn, low-value customers while quietly losing high-value accounts.

## The Solution: Predictive Engine & Architecture

To solve this, I built a three-layered data and AI architecture focused entirely on maximizing retention efficiency:

```plaintext

[Raw Transaction Data]
          │
          ▼
┌────────────────────────────────────────┐
│      Predictive Analytics Layer        │
│  - CLV Model (Future Value)            │
│  - Churn Model (Risk Probability)      │
│  - K-Means (Behavioral Segmentation)   │
└────────────────────────────────────────┘
          │
          ▼
┌────────────────────────────────────────┐
│         Data & Storage Layer           │
│  - PostgreSQL Database                 │
│  - Unified "Revenue-at-Risk" Metric    │
└────────────────────────────────────────┘
          │
          ▼
┌────────────────────────────────────────┐
│      Intelligent Action Layer          │
│  - Local Llama LLM via SQL Functions   │
│  - Streamlit UI for Sales/CS Teams     │
└────────────────────────────────────────┘
```

**The Scoring Engine:** 

The system calculates a unified "Revenue-at-Risk" metric by intersecting customer value (CLV), churn probability, and behavioral clusters via K-Means segmentation.

**The Storage Layer:** M

odel scores and customer behavioral features are stored and continually updated within a PostgreSQL database.

**The AI Execution & Streamlit Layer:** 

To make the data instantly actionable for non-technical teams, a local Llama LLM queries the database via custom SQL functions. This is served through a simple, intuitive Streamlit user interface. Sales and account management teams can use natural language to instantly pull high-priority task lists (e.g., *"Show me our highest-value clients who are at immediate risk of leaving"*).

---

## Strategic Business Impact 

Evaluating this system against traditional methods on historical data yielded massive performance improvements:

- **21% Efficiency Lift:** The combined Revenue-at-Risk framework achieved a **+9 percentage point lift** over targeting by customer value alone, and vastly outperformed a churn-only approach.

- **Resource Optimization:** By targeting just the top 20% of accounts flagged by this system, account management teams can **capture ~52% of all potential revenue loss** over the following three months.

- **Operational ROI:** Sales and Customer Success teams save more contract value with less manual labor, entirely optimizing the business's retention budget.

![Cumulative capture curve](artifacts/assets/evaluation.png)

---

## Live Demo

Watch the system below:

[▶️ Demo Video](https://www.loom.com/share/b88a7162a7d149e6946e60b30c0bf962)

---

## Limitations# Customer Retention Prioritization System

In this project, I built a system that helps focus retention efforts on the customers most likely to leave and cost you money.


## Problem 

With thousands of customers, how can we identify and prioritize those whose potential loss represents the greatest value at risk?


## Solution

I built a retention prioritization system from scratch by training three Machine Learning models; churn risk classification, customer life value (CLV) estimation, and K-Means advanced behavioral segmentation, and combining their outputs into a unified customer profile stored in PostgreSQL database. I then created a calculated metric Estimated **Revenue-at-Risk** (churn probability x CLV) which is used to rank customers for retention prioritization. 

**System Performance:** targeting the **top 20% by estimated revenue-at-risk captured 52% of potential revenue loss** vs. 43% using CLV alone and 20% random targeting.


The system ranks customers based on expected value loss (revenue at risk) and highlights who to contact first and highlights key insights about their purchasing behavior. 
Results are delivered through a simple user streamlit chatbot, making it easy for teams to act quickly without manual analysis. It is designed to stay up to date as new data arrives (by simply provide new month's date to the prediction endpoint/button), allowing teams to easily refresh customer scores and keep retention efforts aligned with the latest behavior. It can be adapted to different data environments as it needs miminal data preprocessing, allowing performance to scale with the quality and richness of available customer data.


## Impact (Evaluation)

On historical data:

Targeting the top 20% of customers identified by the system captures **~52% of total revenue loss**
This outperforms:
        - Using customer value alone (43%)
        - Using churn prediction alone (14%)

This means businesses can save more revenue with the same effort by focusing on the right customers.

![Cumulative capture curve](artifacts/assets/evaluation.png)

**Insights**

- The combined revenue-at-risk model outperforms both value-only and churn-only approaches, capturing the highest proportion of revenue loss across all customer segments.
- Customer value provides the primary signal while churn probability improves prioritization by identifying which high-value customers are at immediate risk, leading to better targeting efficiency.


**Baseline comparisons**

- Churn-only captures 14% of total revenue 
- Value-only captures 43% of total revenue 
- Combined approach captures 52% of revenue 

- The +9 percentage lift on total loss, which is ~21% relative improvement over CLV-only implies that when teams can only contact to 5-20% of customers, more revenue is saved with the same budget.

- While value explains most of the signal, churn adds critical timing information that improves targeting efficiency.

- Results reflect the characteristics of the dataset where customer value is a stronger predictor than churn. The system is designed to incorporate richer behavioral signals, and performance is expected to improve in environments with more informative churn patterns.

## Next Steps

Automate delivery of ranked list of customers to act on now to the relevant team vis prefect or airflow. 


## Live Demo

Watch the system below:

[▶️ Demo Video](https://www.loom.com/share/b88a7162a7d149e6946e60b30c0bf962)


## Design

I then build a system using machine learning approaches that helps recognize early warning signs and enables the team to take targeted preventive action. 

The system takes raw transactional data, automatically transforms it into customer features, and turns those features into clear retention prioritization list based on expected revenue loss should the customer leave. It combines churn risk modeling, K-means customer profiling, and CLV prediction to identify which customers are most valuable and most likely to leave. 
The churn model detects the early warning signs, the clustering model gives the customer profile, and the CVL model adds the estimated value of the customer based history; the calculated estimated revenue-at-risk provides the risk score and ranking metric. Together, they form a retention priotization system that ranks customers based on expected value loss (revenue at risk) and highlights who to contact first and highlights key insights about their purchasing behavior. 


## Limitations

- Results depend on data quality and available signals
- In this dataset, customer value was a stronger driver and churn adds incremental improvement. In other settings with stronger churn signals, the uplift could be larger.
- Performance is expected to improve with richer behavioral data
- CLV is approximated using predicted purchase frequency and historical AOV, which introduces bias in absolute values. However, since the business objective is prioritization rather than exact forecasting, I evaluated the system based on its ability to rank customers by revenue-at-risk.

- Results depend on data quality and available signals
- In this dataset, customer value was a stronger driver and churn adds incremental improvement. In other settings with stronger churn signals, the uplift could be larger.
- Performance is expected to improve with richer behavioral data
- CLV is approximated using predicted purchase frequency and historical AOV, which introduces bias in absolute values. However, since the business objective is prioritization rather than exact forecasting, I evaluated the system based on its ability to rank customers by revenue-at-risk. Other CLV methods can yield different results