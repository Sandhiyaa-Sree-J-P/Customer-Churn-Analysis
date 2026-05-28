📡 Telecom Customer Churn Analysis

Exploratory data analysis on a telecom customer dataset of 7,043 records to identify the key behavioural, contractual, and service-level drivers of customer churn and surface targeted retention recommendations.


📋 Table of Contents

Executive Summary
Business Problem
Dataset Overview
Methodology
Skills & Tools
Key Findings & Observations
Business Recommendations
Project Structure
How to Run


🔍 Executive Summary:

This project performs a full end-to-end exploratory data analysis on a telecom company's customer dataset of 7,043 customers to understand the drivers of customer churn. The analysis covers customer demographics, contract behaviour, service subscriptions, internet service type, and payment methods — producing structured, evidence-backed findings directly from the data.
The headline finding: 26.54% of the customer base has churned — that is 1,869 customers out of 7,043. The remaining 5,174 customers (73.46%) are retained.
What makes this number business-critical is that churn is not evenly distributed. The analysis identifies that attrition is concentrated in specific, identifiable segments:

Customers on month-to-month contracts churn at a far higher rate than those on one-year or two-year contracts
Customers in the first 1–2 months of tenure show the sharpest churn concentration — new customers are the most at risk
Fiber Optic internet service subscribers churn significantly more than DSL users
Customers without add-on services (Online Security, Tech Support, Online Backup, Device Protection) are more likely to leave than those who subscribe to them
Senior citizens, though only 16.21% of the base (~1,142 customers), churn at a comparatively higher rate than non-senior customers
Customers paying via electronic check are more likely to churn than those on automatic or mailed payment methods

The dataset is clean — zero null values and zero duplicate customer IDs after preprocessing — and the analysis is built on 21 features spanning account, demographic, and service dimensions.
The six drivers identified through this EDA map directly to six targeted retention recommendations, giving the business a clear, prioritised action plan to reduce attrition.


💼 Business Problem

A telecom company with 7,043 active customers is experiencing a churn rate of 26.54% — meaning more than 1 in 4 customers is leaving. Without understanding why customers are churning, any retention effort is untargeted and inefficient.
This analysis was scoped around five core business questions:

What is the overall churn rate and how is the customer base split between churned and retained?
Do demographic factors — gender and senior citizen status — influence churn behaviour?
How does customer tenure relate to the likelihood of churning?
Which contract types, internet service tiers, and add-on subscriptions are associated with higher churn?
Does payment method correlate with customer attrition?

Answering these questions with data — rather than assumption — is the foundation for a focused, cost-efficient retention strategy.


📊 Dataset Overview

AttributeDetailTotal records7,043 customersTotal features21 columnsTarget variableChurn (Yes / No)Null values after cleaning0Duplicate customer IDs0
Feature categories:

Demographics: Gender, SeniorCitizen, Partner, Dependents
Account details: Tenure, Contract, PaperlessBilling, PaymentMethod, MonthlyCharges, TotalCharges
Services subscribed: PhoneService, MultipleLines, InternetService, OnlineSecurity, OnlineBackup, DeviceProtection, TechSupport, StreamingTV, StreamingMovies

Numerical summary from df.describe():
FeatureMeanMinQ1 (25%)Median (50%)Q3 (75%)MaxTenure (months)32.3709295572MonthlyCharges ($)64.7618.2535.5070.3589.85118.75TotalCharges ($)2,279.730398.551,394.553,786.608,684.80SeniorCitizen (proportion)0.162100001

🔬 Methodology

Phase 1 — Data Loading & Inspection

Loaded Customer_Churn.csv using Pandas: 7,043 rows × 21 columns confirmed via df.info()
Identified TotalCharges stored as object dtype due to blank string entries for customers with zero tenure
Replaced blank strings with "0" and cast the column to float
Ran df.isnull().sum() and df.isnull().sum().sum() — confirmed zero nulls across all 21 columns
Ran df["customerID"].duplicated().sum() — confirmed zero duplicate records
Converted SeniorCitizen from binary integer (0/1) to readable categorical labels (no/yes) using a custom mapping function

Phase 2 — Univariate Analysis

Plotted churn count using sns.countplot with bar labels — confirmed 1,869 churned vs 5,174 retained
Plotted churn percentage using a pie chart with autopct="%1.2f%%" — confirmed 26.54% churn rate
Plotted the count of senior citizens within the customer base using a bar-labelled count plot

Phase 3 — Bivariate & Segmented EDA

Gender vs Churn: Count plot split by churn to compare male and female attrition
Senior Citizen vs Churn: pd.crosstab normalised by index (×100) to produce percentage churn rates per group — plotted as a stacked bar chart with percentage labels
Tenure vs Churn: Histogram with 72 bins and hue = Churn to visualise churn concentration across the full 0–72 month tenure range
Contract Type vs Churn: Count plot split by churn across Month-to-Month, One Year, and Two Year contracts
9 Service Features vs Churn: 3×3 subplot grid of count plots covering PhoneService, MultipleLines, InternetService, OnlineSecurity, OnlineBackup, DeviceProtection, TechSupport, StreamingTV, StreamingMovies — each split by churn
Payment Method vs Churn: Count plot across all four payment methods split by churn

Phase 4 — Insight Synthesis

Translated visual patterns into structured observations documented inline as code comments
Ranked findings by churn signal strength
Mapped each finding to a direct, actionable business recommendation


🛠️ Skills & Tools

CategoryDetailsLanguagePython 3Data manipulationPandas, NumPyVisualisationMatplotlib, SeabornEDA techniquesUnivariate analysis, Bivariate analysis, Crosstab normalisation, Segmented profiling, Histogram binning, Stacked bar charting, Multi-panel subplot gridsData cleaningBlank string imputation, Type casting (object → float), Null validation, Duplicate detection, Binary-to-categorical encodingBusiness analysisChurn driver identification, Customer segment profiling, Retention strategy formulation, Business question framingEnvironmentJupyter Notebook, Anaconda

📈 Key Findings & Observations
1. Overall Churn — 26.54% of the Customer Base Has Left

Out of 7,043 total customers, 1,869 have churned (26.54%) and 5,174 are retained (73.46%)
More than 1 in 4 customers is leaving — this is not a marginal attrition rate; it represents a systemic retention challenge
The pie chart confirms the 26.54% figure with autopct precision


2. Gender — Not a Churn Driver

The count plot of churn split by gender shows that churn counts for male and female customers are closely matched
Gender does not emerge as a meaningful differentiator for churn and is not a useful variable for targeting retention efforts


3. Senior Citizens — Comparatively Higher Churn Rate

Senior citizens make up approximately 16.21% of the customer base (~1,142 of 7,043 customers), with non-senior customers accounting for the remaining 83.79% (~5,901 customers)
The stacked bar chart (crosstab normalised by index) shows that a comparatively greater percentage of senior citizens have churned relative to non-senior customers
Despite being a smaller segment of the base, the senior citizen group carries a disproportionately higher churn burden


4. Tenure — New Customers Churn, Long-Tenure Customers Stay

The tenure histogram (72 bins, hue = Churn) reveals a sharp concentration of churned customers at 1–2 months of tenure
Customers who have used the service for a long time have stayed; customers who have been with the company for only 1 or 2 months have churned
Tenure ranges from 0 to 72 months with a mean of 32.37 months and a median of 29 months
The bottom 25% of customers have tenure of 9 months or less — this early-lifecycle cohort is the highest-risk group for churn


5. Contract Type — Month-to-Month Is the Highest-Churn Contract

The contract count plot makes the pattern unambiguous: customers on month-to-month contracts are significantly more likely to churn than customers on one-year or two-year contracts
Customers on one-year and two-year contracts show strong retention — the commitment structure of longer contracts directly reduces the likelihood of leaving


6. Internet Service, Add-Ons & Phone — Six Service-Level Signals
From the 3×3 subplot grid analysis across nine service features:

Fiber Optic vs DSL: Customers using Fiber Optic internet service have a significantly higher churn rate compared to DSL users
Online Security: Customers without Online Security are more likely to churn than those who have it
Tech Support: Customers without Tech Support are more likely to churn than those who subscribe to it
Online Backup: Customers without Online Backup are more likely to churn
Device Protection: Customers without Device Protection are more likely to churn
Add-On pattern: Customers who subscribe to additional support and security services tend to stay longer with the company
Phone & Multiple Lines: Phone service and multiple-line users generally show lower churn, indicating better customer retention in these categories


7. Payment Method — Electronic Check Is a Churn Signal

The payment method count plot shows that customers paying via electronic check are more likely to churn compared to customers on other payment methods — credit card (automatic), bank transfer (automatic), and mailed check


💡 Business Recommendations

Recommendation 1 — Target Month-to-Month Customers with Contract Upgrade Incentives
Month-to-month contracts are the clearest churn driver in this dataset. One-year and two-year contract customers demonstrate significantly stronger retention. The business should design incentive programmes — such as discounted first months or complimentary add-on services — specifically to migrate month-to-month customers to annual contracts, directly attacking the highest-volume churn segment.

Recommendation 2 — Build a Structured Early Lifecycle Retention Programme
Churn is heavily concentrated in the first 1–2 months of tenure. The bottom quartile of the customer base has been with the company for 9 months or less. A dedicated onboarding and early engagement programme — proactive communication, setup support, and first-90-day loyalty touchpoints — directly targets the window where the risk of leaving is highest.

Recommendation 3 — Investigate the Fiber Optic Churn Gap
Fiber Optic customers churn at a significantly higher rate than DSL customers. Since Fiber Optic is the higher-price tier, this signals a perceived value gap — customers are paying more but leaving at a greater rate. A customer satisfaction review specific to Fiber Optic subscribers is recommended to identify whether the issue is pricing, reliability, or service quality.

Recommendation 4 — Drive Add-On Adoption Among Customers Without Protective Services
Customers without Online Security, Tech Support, Online Backup, and Device Protection are more likely to churn. Customers with these services stay longer. Bundled introductory offers — particularly targeted at month-to-month and low-tenure customers who are already at risk — would increase service stickiness and raise the switching cost for at-risk segments.

Recommendation 5 — Migrate Electronic Check Users to Automatic Payment
Electronic check is the payment method most associated with churn. Customers on automatic payment methods (credit card or bank transfer) show comparatively better retention. A nudge campaign encouraging electronic check users to switch to auto-pay — supported by a small billing incentive — addresses this behavioural signal at relatively low cost.

Recommendation 6 — Create Dedicated Retention Support for Senior Citizens
Senior citizens churn at a comparatively higher rate than non-senior customers despite representing only 16.21% of the base. This suggests friction — whether in billing, product usability, or support access — that disproportionately affects this segment. Simplified communication, priority support access, and proactive check-ins tailored to senior customers can reduce this retention gap.
