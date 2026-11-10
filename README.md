
<h1 align="center">Enterprise Revenue Protection</h1>

<h3 align="center">Telco Customer Churn Analysis & Predictive Retention Strategy</h3>

<p align="center">
  <strong>Data Analytics | SQL | Python | Statistical Analysis | Machine Learning | Financial Modeling</strong>
</p>

<p align="center">
  An end-to-end analytics project that transforms customer churn data into actionable revenue protection strategies.
</p>

---

## 1. Project Overview

Customer churn is one of the biggest challenges for subscription-based businesses, particularly in the telecommunications industry. When customers discontinue their subscriptions, businesses lose recurring revenue, and acquiring replacement customers can be expensive.

The goal of this project was to go beyond simply identifying how many customers leave a telecommunications company. I wanted to understand **why customers leave, which customer segments contribute most to revenue loss, how accurately churn can be predicted, and how a business can prioritize its retention budget to protect revenue.**

I developed an end-to-end revenue protection workflow using the Telco Customer Churn dataset. The project combines data cleaning, SQL-based data warehousing, cohort analysis, statistical hypothesis testing, survival analysis, machine learning, model explainability, and financial ROI modeling.

Rather than treating churn as only a classification problem, I approached it as a business and financial risk problem. The final objective was to turn customer-level predictions into an actionable retention strategy.

### Project at a Glance

| Component | Details |
|---|---|
| Industry | Telecommunications |
| Business Problem | Customer churn and recurring revenue loss |
| Dataset | Telco Customer Churn |
| Original Records | 7,043 customers |
| Data Processing | Python, Pandas, NumPy |
| Database | SQLite |
| SQL Analysis | CTEs, joins, aggregations, window functions |
| Statistical Analysis | Chi-square, Welch's t-test |
| Customer Lifecycle Analysis | Kaplan-Meier survival analysis |
| Machine Learning | Logistic Regression, Random Forest, XGBoost |
| Model Explainability | SHAP |
| Financial Analysis | Probability-weighted revenue exposure and retention ROI |

---

## 2. Business Objectives

I structured the project around five main business questions:

1. **Understanding Customer Churn:** Which customer characteristics, services, payment methods, and contract types are associated with customer churn?

2. **Identifying Revenue Leakage:** Which customer segments contribute most to lost monthly recurring revenue (MRR)?

3. **Validating Business Assumptions:** Are the relationships between customer characteristics, monthly charges, and churn statistically significant?

4. **Predicting Customer Churn:** Can machine learning identify customers who are at risk of leaving before the business loses their revenue?

5. **Prioritizing Retention Investment:** How should a business allocate its retention budget to customers who represent the greatest financial risk?

These questions shaped the entire analytical workflow, from initial data preparation to the final financial recommendations.

---

## 3. Dataset Description

I used the Telco Customer Churn dataset, which contains customer demographic information, subscribed services, account details, billing information, and churn status.

The dataset contains **7,043 customer records** and includes variables such as:

| Category | Variables |
|---|---|
| Customer Demographics | Gender, Senior Citizen, Partner, Dependents |
| Account Information | Customer ID, Tenure |
| Subscription Services | Phone Service, Multiple Lines, Internet Service |
| Additional Services | Online Security, Online Backup, Device Protection, Tech Support |
| Entertainment Services | Streaming TV, Streaming Movies |
| Billing Information | Monthly Charges, Total Charges |
| Contract Information | Contract Type, Paperless Billing, Payment Method |
| Target Variable | Churn |

The target variable was converted into a binary format:

- `1` = Customer churned.
- `0` = Customer remained with the company.

This format made the dataset suitable for statistical testing and supervised machine learning.

---

## 4. Step-by-Step Project Workflow

### Step 1: Data Loading, Auditing and Cleaning

I started by importing the dataset into Python using Pandas and NumPy.

Before performing any analysis, I checked the dataset's structure and integrity to identify potential data quality problems.

#### 1.1 Initial Data Audit

The first checks focused on:

- Total number of records and columns.
- Unique customer IDs.
- Duplicate records.
- Missing values.
- Hidden missing values represented by whitespace.
- Data types of numerical and categorical variables.

One issue I identified was that some entries in `TotalCharges` contained whitespace instead of numerical values. These entries could not be processed correctly as numerical data.

#### 1.2 Handling Missing Values and Data Types

| Issue | Action Taken |
|---|---|
| Whitespace in `TotalCharges` | Replaced whitespace with NaN |
| Non-numeric `TotalCharges` | Converted to numerical values |
| Missing charges for new customers | Handled as zero during initial cleaning |
| `SeniorCitizen` encoded as 0 and 1 | Converted into Yes/No categories |
| Churn stored as Yes/No | Created a binary `Churn_Flag` |
| Customer IDs | Checked for uniqueness |

I also created temporary verification columns to compare reported total charges against expected charges calculated using monthly charges and customer tenure.

Expected Total Charges:

```python
Expected Total Charges = Monthly Charges * Tenure
```

The absolute difference between the two values was calculated to examine possible billing discrepancies.

#### 1.3 Feature Standardization

I standardized service-related categorical variables to make them easier to analyze.

For example:

- `No internet service` was standardized to `No` for relevant add-on services.
- `No phone service` was standardized to `No` for multiple-line analysis.
- An `Is_Automatic_Payment` binary feature was created using the payment method.

**Output:** `telco_churn_cleaned_master.csv`

The purpose of this stage was to establish a consistent dataset before moving into database development and analytical modeling.

---

### Step 2: SQL Data Warehousing and Star Schema Design

After cleaning the data, I moved beyond working with a single flat dataset and designed a relational SQL warehouse using SQLite.

The objective was to organize customer information into separate logical tables, making the data easier to query, maintain, and analyze.

#### 2.1 Database Architecture

I designed a Star Schema consisting of three tables:

```text
                 dim_customers
                       |
                       |
                       |
fact_customer_billing ---- dim_services
```

#### 2.2 Table Structure

| Table | Purpose |
|---|---|
| `dim_customers` | Stores demographic and customer-related attributes |
| `dim_services` | Stores information about subscribed telecommunications services |
| `fact_customer_billing` | Stores billing, contract, tenure, and churn information |

The central fact table contained customer billing and churn metrics, while the dimension tables stored customer and service attributes.

Each table was populated using Pandas `to_sql()` and stored in the SQLite database:

`telco_revenue_risk.db`

#### 2.3 Relational SQL Analysis

Once the database was populated, I used SQL joins to combine information from the three tables.

I then developed multi-stage analytical queries using:

- Common Table Expressions (CTEs).
- CASE statements for customer segmentation.
- GROUP BY for cohort-level aggregations.
- Aggregate functions such as COUNT, SUM, and AVG.
- Window functions for calculating cumulative revenue losses.
- JOIN operations to combine customer, service, and billing information.

This allowed me to perform more structured analysis without repeatedly manipulating the original flat dataset.

**Output:** A normalized SQLite database containing three analytical tables.

---

### Step 3: Cohort Analysis and Revenue Leakage Identification

After establishing the database, I used SQL to investigate how churn behavior changes across different customer lifecycle stages and contract types.

The central question was:

**Which customer cohorts are responsible for the greatest recurring revenue losses?**

#### 3.1 Customer Lifecycle Segmentation

I divided customers into four tenure-based cohorts:

| Cohort | Customer Tenure |
|---|---|
| Early Lifecycle | 0–12 months |
| Mid Lifecycle | 13–24 months |
| Established | 25–48 months |
| Mature Accounts | More than 48 months |

I then segmented each cohort by contract type:

- Month-to-month.
- One-year.
- Two-year.

This produced a more detailed view of customer churn than examining the overall churn rate.

#### 3.2 Revenue Metrics

For each cohort, I calculated:

**Average Revenue Per User (ARPU)**

```text
ARPU = Total Monthly Charges / Number of Customers
```

**Gross Monthly Recurring Revenue (MRR)**

```text
MRR = SUM(Monthly Charges)
```

**Direct Monthly Revenue Loss**

```text
Lost MRR = SUM(Monthly Charges of Churned Customers)
```

**Cumulative MRR Loss**

I used SQL window functions to calculate cumulative revenue losses within each contract category.

This helped identify how revenue exposure accumulated across customer lifecycle segments.

#### 3.3 Cohort Analysis Findings

The SQL analysis revealed substantial differences between contract types.

**Month-to-Month Customer Cohorts**

| Tenure | Customers | Churn Rate | Direct MRR Lost |
|---|---:|---:|---:|
| 0–12 months | 1,994 | 51.35% | $68,301.45 |
| 13–24 months | 737 | 37.72% | $21,980.30 |
| 25–48 months | 802 | 32.92% | $22,557.00 |
| Over 48 months | 342 | 26.02% | $8,008.35 |

**Contract Comparison**

| Contract Type | Early Lifecycle Churn |
|---|---:|
| Month-to-month | 51.35% |
| One-year | 10.48% |
| Two-year | 0.00% |

The early-lifecycle month-to-month cohort had the highest churn rate and the largest direct monthly revenue loss.

The analysis also showed that month-to-month cohorts accumulated approximately **$120,847.10 in direct monthly revenue loss** across the four tenure segments.

**Business Implication:** Early customer engagement and retention initiatives should receive particular attention, especially for month-to-month subscribers.

---

### Step 4: Statistical Analysis and Hypothesis Testing

After identifying patterns through cohort analysis, I wanted to determine whether the observed relationships between customer characteristics and churn were statistically significant.

I used SciPy for hypothesis testing and the `lifelines` library for survival analysis.

#### 4.1 Chi-Square Test of Independence

I used the Chi-square test to investigate whether categorical customer characteristics were associated with churn.

The following relationships were tested:

1. Contract Type vs. Churn.
2. Internet Service vs. Churn.
3. Automatic Payment vs. Churn.
4. Technical Support vs. Churn.

**Hypotheses**

- Null Hypothesis (H0): There is no statistically significant association between the selected categorical variable and customer churn.
- Alternative Hypothesis (H1): There is a statistically significant association.

**Chi-Square Test Results**

| Variable | Chi-Square Statistic | P-value |
|---|---:|---:|
| Contract Type | 1184.60 | 5.86 × 10⁻²⁵⁸ |
| Internet Service | 732.31 | 9.57 × 10⁻¹⁶⁰ |
| Automatic Payment | 309.35 | 3.03 × 10⁻⁶⁹ |
| Tech Support | 190.17 | 2.92 × 10⁻⁴³ |

All four tests produced p-values below 0.001.

Therefore, I rejected the null hypothesis for each test.

The findings indicate statistically significant associations between these customer characteristics and churn. However, statistical association alone does not establish causation.

#### 4.2 Welch's Independent T-Test

Next, I investigated whether customers who churned had significantly different monthly bills from customers who remained.

I selected Welch's t-test because it does not assume equal population variances between the two groups.

**Hypotheses**

- H0: The mean monthly charges of churned and retained customers are equal.
- H1: The mean monthly charges are different.

**Test Results**

| Metric | Churned Customers | Retained Customers |
|---|---:|---:|
| Mean Monthly Bill | $74.44 | $61.27 |
| Standard Deviation | $24.67 | $31.09 |

- Welch's t-statistic: 18.4075
- P-value: 8.59 × 10⁻⁷³
- Mean monthly bill difference: $13.18

**Conclusion:** Reject H0.

Churned customers paid approximately $13.18 more per month on average.

This finding suggested that higher monthly billing was associated with greater churn in the dataset. It provided another useful direction for customer segmentation and retention analysis.

#### 4.3 Kaplan-Meier Survival Analysis

I then used Kaplan-Meier survival analysis to examine customer retention over time.

Unlike a simple churn-rate calculation, survival analysis considers the time customers remain with the company before the churn event.

I used:

- `KaplanMeierFitter` from the Lifelines library.
- Customer tenure as the duration variable.
- Churn status as the event indicator.

The survival function estimates the probability that a customer remains with the company beyond a particular point in time.

```text
S(t) = P(T > t)
```

Where T represents the time until churn.

**Retention Probabilities**

| Customer Tenure | Estimated Survival Probability |
|---|---:|
| 3 months | 91.37% |
| 6 months | 88.48% |
| 12 months | 84.32% |
| 24 months | 78.87% |
| 36 months | 74.85% |
| 48 months | 70.88% |
| 60 months | 66.44% |
| 72 months | 59.28% |

I also compared survival probabilities between different contract types.

| Contract Type | 12-Month Survival Probability |
|---|---:|
| Month-to-month | 70.31% |
| One-year | 99.08% |

The comparison reinforced the earlier cohort findings: customers on longer-term contracts demonstrated substantially higher retention probabilities.

**Business Implication:** Retention strategies should focus on the early customer lifecycle, where the probability of losing customers is comparatively high.

---

### Step 5: Machine Learning-Based Churn Prediction

After completing the descriptive and statistical analysis, I moved into predictive modeling.

The objective was to build a model that could estimate the probability of individual customers leaving the company.

Instead of relying only on historical churn percentages, I wanted to use customer demographics, subscription information, billing characteristics, and tenure to identify customers who may be at risk.

#### 5.1 Extracting the Modeling Dataset

I retrieved the customer-level data directly from the SQLite warehouse by joining:

- `fact_customer_billing`
- `dim_customers`
- `dim_services`

This produced a modeling dataset containing all 7,043 customer records.

The target variable was `churn_flag`, while the remaining customer characteristics were used as predictive features.

#### 5.2 Data Preprocessing

Before training the models, I performed the following operations:

| Operation | Purpose |
|---|---|
| Customer ID separation | Retained IDs for linking predictions to individual customers, without using them as model features |
| Target separation | Isolated `churn_flag` as the prediction target |
| One-hot encoding | Converted categorical variables into numerical representations using `pd.get_dummies()` |
| Train-test split | Divided the dataset into 80% training and 20% testing data |
| Stratification | Preserved the churn-class distribution across both datasets |
| Feature scaling | Standardized selected numerical features |

The numerical features selected for scaling were:

- `tenure_months`
- `monthly_charges`
- `total_charges`

I used `StandardScaler`, fitting it on the training data and applying the same transformation to the testing data to avoid data leakage through preprocessing.

I also used a fixed random state of 42 to make the train-test split reproducible.

#### 5.3 Model Benchmarking

I trained and compared three classification algorithms.

| Model | Purpose |
|---|---|
| Logistic Regression | Establishes a baseline classification model and provides a relatively interpretable benchmark |
| Random Forest | Captures nonlinear relationships and interactions between customer features |
| XGBoost | Uses gradient boosting to capture complex patterns in customer churn behavior |

Because the dataset contained an imbalance between churned and retained customers, I incorporated class-imbalance handling:

- `class_weight='balanced'` for Logistic Regression.
- `class_weight='balanced'` for Random Forest.
- `scale_pos_weight` for XGBoost.

#### 5.4 Model Evaluation

I used ROC-AUC to compare the models.

ROC-AUC evaluates how well a classifier distinguishes between churned and retained customers across different classification thresholds.

**Model Benchmarking Results**

| Model | ROC-AUC |
|---|---:|
| Logistic Regression | 0.8407 |
| Random Forest | 0.8420 |
| XGBoost | **0.8432** |

XGBoost achieved the highest ROC-AUC among the three models, so I selected it for the subsequent churn-risk scoring process.

#### 5.5 Recall-Oriented Threshold Tuning

A default classification threshold of 0.50 is not necessarily the best choice for a business trying to identify as many potential churners as possible.

In this project, missing a customer who is about to leave could mean losing an opportunity to intervene.

Therefore, I explored threshold adjustment with a target recall of approximately 80% or higher.

At the default threshold:

- Recall: 81.82%.

The threshold-selection procedure selected 0.01, resulting in:

| Metric | Result |
|---|---:|
| Recall | 100% |
| True Negatives | 0 |
| False Positives | 1,035 |
| False Negatives | 0 |
| True Positives | 374 |

This achieved perfect recall on the test set, but it classified every test customer as a potential churner.

That means the threshold was too aggressive for a practical retention campaign. It demonstrates an important trade-off: increasing recall can create a substantial number of false positives.

The ROC-AUC comparison was therefore more informative for model discrimination than this particular threshold result. A more balanced operating threshold would need to be selected using business costs, precision, recall, and campaign capacity.

#### 5.6 Model Explainability Using SHAP

After selecting XGBoost, I used SHAP (SHapley Additive exPlanations) to understand which features contributed most to the model's predictions.

This was important because a prediction model should not simply identify high-risk customers; it should also provide insight into the characteristics influencing its predictions.

I calculated mean absolute SHAP values to rank the global feature importance.

**Top Five Global Churn Predictors**

| Rank | Feature | Mean Absolute SHAP Value |
|---:|---|---:|
| 1 | Two-year contract | 0.6099 |
| 2 | Customer tenure | 0.4607 |
| 3 | Fiber-optic internet | 0.2861 |
| 4 | One-year contract | 0.2847 |
| 5 | Monthly charges | 0.1931 |

The results highlighted contract type, tenure, internet service, and monthly charges as important features influencing the model's predictions.

SHAP importance measures the magnitude of a feature's contribution, not whether it increases or decreases churn risk. The direction of individual feature effects would require examining SHAP values at the feature level.

**Output:** A scored test dataset containing customer information, predicted churn probabilities, and assigned risk categories.

I divided the predicted probabilities into three risk tiers:

| Risk Category | Predicted Churn Probability |
|---|---|
| Low Risk | 0–35% |
| Medium Risk | 35–65% |
| High Risk | 65–100% |

The scored dataset was exported as:

`telco_step4_scored_accounts.csv`

---

### Step 6: Financial Risk Quantification and Retention ROI Modeling

This was the final stage of the project, where I connected predictive analytics with financial decision-making.

The objective was to translate churn probabilities into estimated revenue exposure and identify which customers should receive priority in a retention campaign.

#### 6.1 Probability-Weighted Revenue Exposure

I introduced the concept of Probability-weighted Capital at Risk (pCaR).

Rather than treating every customer as equally likely to churn, I weighted their monthly revenue by the model's predicted churn probability.

The calculation was:

```text
Monthly pCaR = Predicted Churn Probability * Monthly Charges
```

Annualized exposure was calculated as:

```text
Annual pCaR = Monthly pCaR * 12
```

I then aggregated these values across the test portfolio.

This provided an estimate of expected revenue exposure based on the model's predicted churn probabilities.

#### 6.2 Portfolio-Level Financial Exposure

The model generated predictions for 1,409 customers in the test dataset.

**Test Portfolio Financial Summary**

| Financial Metric | Result |
|---|---:|
| Test Portfolio Size | 1,409 customers |
| Total Monthly Recurring Revenue | $90,301.20 |
| Annualized Recurring Revenue | $1,083,614.40 |
| Expected Monthly pCaR | $41,749.91 |
| Expected Annual pCaR | $500,998.97 |
| Monthly pCaR as a Percentage of MRR | 46.23% |

These figures represent model-based exposure estimates for the test portfolio, not confirmed future revenue losses.

#### 6.3 Identifying High-Risk, High-Value Customers

I did not want to allocate retention resources equally across all customers.

Instead, I introduced a targeting strategy that prioritized customers meeting two conditions:

```text
Predicted Churn Probability >= 0.60

AND

Monthly Charges >= Median Monthly Bill
```

The median monthly bill in the test portfolio was $69.95.

This approach focused on customers who had both a relatively high predicted probability of leaving and comparatively high monthly billing.

**Priority Retention Cohort**

| Metric | Result |
|---|---:|
| Targeted Customers | 349 |
| Percentage of Test Portfolio | 24.77% |
| Annual pCaR Exposure | $282,247.21 |
| Share of Total pCaR | 56.34% |

The results showed that approximately one-quarter of the test portfolio accounted for more than half of its estimated churn-related revenue exposure.

This provided a clear basis for prioritizing retention resources.

#### 6.4 Retention Campaign Design

I then developed a hypothetical retention campaign to evaluate whether targeted customer interventions could generate a positive financial return.

The proposed intervention consisted of:

| Intervention | Monthly Cost per Customer |
|---|---:|
| Contract Pricing Discount | $10 |
| Technical Support Subsidy | $5 |
| **Total Monthly Cost** | **$15** |

The annual retention cost per targeted customer was:

```text
15 * 12 = $180
```

I also introduced an assumed relative churn reduction of 35%.

This was a modeling assumption used to simulate potential campaign performance, not an experimentally measured retention rate.

#### 6.5 Financial Impact Simulation

I estimated preserved annual revenue by applying the assumed 35% retention success rate to the annual pCaR exposure of the targeted cohort.

```text
Preserved Revenue = Target Annual pCaR * 35%
```

The net financial gain was calculated as:

```text
Net Gain = Preserved Revenue - Retention Cost
```

I also calculated the campaign's revenue-to-cost ratio:

```text
Revenue-to-Cost Ratio = Preserved Revenue / Retention Spend
```

**Retention Campaign Simulation Results**

| Financial Metric | Result |
|---|---:|
| Targeted Customers | 349 |
| Annual Cost per Customer | $180 |
| Total Annual Retention Spend | $62,820.00 |
| Assumed Retention Success Rate | 35% |
| Estimated Preserved Annual Revenue | $98,786.52 |
| Estimated Net Financial Gain | $35,966.52 |
| Revenue-to-Cost Ratio | **1.57x** |
| Conventional Net ROI | **57.3%** |

The simulation suggested that a targeted retention campaign could generate more preserved revenue than its estimated intervention cost under the assumptions used.

#### 6.6 Executive Retention Action Ledger

Finally, I exported the selected high-risk, high-value customers into a prioritized action ledger.

The ledger included:

- Customer ID.
- Contract type.
- Internet service.
- Monthly charges.
- Predicted churn probability.
- Annual pCaR exposure.
- Estimated net financial gain.

I sorted the customers by annual pCaR exposure in descending order.

This produced a customer-level output that could serve as a starting point for a retention team to prioritize outreach and allocate intervention budgets.

**Output:** `telco_step5_executive_retention_action_ledger.csv`

---

## 5. Final Business Findings

The project brought together customer behavior, statistical evidence, predictive modeling, and financial analysis.

| Finding | Business Significance |
|---|---|
| Early-stage month-to-month customers had a 51.35% churn rate. | Prioritize retention during the first year. |
| Two-year contracts showed substantially lower churn. | Contract duration is an important segmentation variable. |
| Churned customers had higher average monthly bills. | Investigate pricing and perceived service value. |
| Contract type, internet service, automatic payment, and tech support were significantly associated with churn. | Use these characteristics in customer segmentation. |
| XGBoost achieved a ROC-AUC of 0.8432. | Demonstrated useful predictive discrimination. |
| 349 test customers met the high-risk, high-value targeting criteria. | Focus retention resources on a smaller customer segment. |
| The hypothetical campaign generated a modeled $35,966.52 net gain. | Targeted retention may offer financial value under the stated assumptions. |

---

## 6. Technical Skills Demonstrated

| Area | Tools and Techniques |
|---|---|
| Data Cleaning | Python, Pandas, NumPy |
| Data Integrity | Duplicate checks, missing-value handling, type conversion |
| Database Development | SQLite, relational tables, Star Schema |
| SQL Analytics | CTEs, CASE, JOINs, GROUP BY, window functions |
| Business Analytics | Cohort analysis, churn rates, ARPU, MRR |
| Statistical Analysis | Chi-square tests, Welch's t-test |
| Survival Analysis | Kaplan-Meier estimation |
| Machine Learning | Scikit-learn, XGBoost |
| Model Evaluation | ROC-AUC, recall, confusion matrix, precision-recall curve |
| Model Explainability | SHAP |
| Financial Modeling | pCaR, revenue exposure, retention cost, ROI simulation |

---

## 7. Project Deliverables

The workflow generated several reusable analytical outputs.

| File | Description |
|---|---|
| `telco_churn_cleaned_master.csv` | Cleaned customer dataset |
| `telco_revenue_risk.db` | SQLite database containing the Star Schema |
| `telco_step3_statistical_summary.csv` | Statistical summary export |
| `telco_step4_scored_accounts.csv` | Test customers with predicted churn probabilities and risk categories |
| `telco_step5_executive_retention_action_ledger.csv` | Prioritized high-risk customer list with financial exposure estimates |

---

## 8. Limitations and Further Improvements

I also identified several areas that would need further attention before this workflow could be deployed in a real business environment.

1. **Classification Threshold:** The selected 0.01 threshold produced 100% recall but also classified every test customer as a churn risk. A more balanced threshold should be selected based on campaign capacity and the relative costs of false positives and false negatives.

2. **Retention Assumptions:** The 35% churn reduction was an assumed scenario. An actual retention campaign or controlled experiment would be needed to establish its effectiveness.

3. **Financial Exposure:** pCaR is a probability-weighted revenue estimate, not a guaranteed future loss. It assumes that monthly charges represent the revenue exposure over the annualized horizon.

4. **ROI Terminology:** The reported 1.57x figure is preserved revenue divided by campaign spend. Expressed as conventional net ROI, the modeled return is approximately 57.3%.

5. **Model Validation:** Further validation using cross-validation, calibration analysis, and a separate validation dataset would strengthen confidence in the predictions.

6. **Data Cleaning Consistency:** The notebook initially fills zero-tenure customers' total charges with zero, but a later processing stage changes those values to monthly charges. This should be standardized and documented before final deployment.

These improvements would help move the project from an analytical prototype towards a more reliable business decision-support system.

---

## 9. Conclusion

This project allowed me to approach customer churn from multiple perspectives rather than treating it as a standalone machine learning problem.

I started with raw customer data, investigated its quality, developed a relational SQL database, and used cohort analysis to understand revenue leakage. I then applied statistical techniques to validate important customer relationships, built predictive models to estimate churn probabilities, and used SHAP to interpret the model's predictions.

Finally, I translated those predictions into financial exposure estimates and developed a hypothetical retention campaign to evaluate how a business could prioritize its resources.

**The main takeaway was that identifying customers who might leave is only one part of solving the churn problem. The real business value comes from understanding which customers represent the greatest financial risk and using that information to make better retention decisions.**

---

<p align="center">
  <strong>Enterprise Revenue Protection | End-to-End Data Analytics Project</strong>
</p>
