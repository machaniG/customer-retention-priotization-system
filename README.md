# AI-Powered Customer Lifetime Value & Revenue-at-Risk Retention Platform | Python, SQL, PostgreSQL, LangChain, FastAPI, Streamlit


In this project, I built a system that helps focus retention efforts on the customers most likely to leave and cost you money.


## Problem 

- With thousands of customers who should we prioritize for retention? 
- How can we identify and prioritize customers whose potential loss represents the highest value at risk?


## Solution

I engineered customer-level features from transactional data, built and trained three machine learning models; churn risk classification, Customer Lifetime Value (CLV) estimation, and K-Means clustering for advanced behavioral segmentation.

Combined the outputs from the three models into one table, calculated **Estimated Revenue-at-Risk metric (RaR: churn probability x estimated CLV)**, and used the estimated RaR feature to rank customers for retention prioritization.

Created a local PostgreSQL database where I stored processed customer features, combined models output, and relational metadata.

**System Performance:** **targeting the top 20% by estimated revenue-at-risk captured 52% of potential revenue loss vs. 43% using CLV alone and 20% under random targeting.**

Integrated a provider-agnostic tool-calling LLM agent layer with LangChain (OpenAI/Claude/Llama) non-technical teams to securely generate grounded customer-level explanations from model outputs and behavioral features.

Exposed functionality using FastAPI endpoints, built a Streamlit interface for non-technical teams like retention managers to use and containerized for cloud deployment.


- The system ranks customers based on expected value loss (revenue at risk) and highlights who to contact first and highlights key insights about their purchasing behavior. 
- Results are delivered through a simple user streamlit chatbot, making it easy for teams to act quickly without manual analysis. 
- **It is designed to stay up to date as new data arrives (by simply providing new month's date to the prediction endpoint/button), allowing teams to easily refresh customer scores and keep retention efforts aligned with the latest behavior.**
- It can be adapted to different data environments as it needs miminal data preprocessing, allowing performance to scale with the quality and richness of available customer data.


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
