
<div align="center">

<h1>Enterprise Revenue Protection &amp; Customer Churn Analytics</h1>

<h3>Customer Intelligence | Predictive Analytics | Revenue Risk Assessment | Retention Strategy</h3>

<p>
  An end-to-end business analytics project focused on understanding
  customer attrition, quantifying potential recurring revenue exposure,
  and developing data-driven customer retention strategies.
</p>

<p>
  <a href="https://public.tableau.com/app/profile/maira.zarnab/viz/Book1_17837346834310/Executive_Overview">
    <strong>Dashboards</strong>
  </a>
</p>

</div>

<hr>

<h2>1. Executive Summary</h2>

<p>
Customer churn is a significant commercial challenge for subscription-based
businesses. The loss of customers directly affects recurring revenue,
customer lifetime value, acquisition costs, and long-term profitability. 
</p>

<p>
This project develops an integrated analytical framework to investigate
customer churn within the telecommunications industry. Using a dataset
of 7,043 customer records, the analysis combines SQL, Python, statistical
analysis, predictive modeling, financial assessment, and Tableau
visualization to translate customer-level information into actionable
business intelligence.
</p>

<p>
Rather than approaching churn as an isolated classification problem,
the project treats customer attrition as a business performance and
revenue protection challenge.
</p>

<h2>2. Business Problem and Strategic Context</h2>

<p><strong>The project addresses the following business questions:</strong></p>

<table>
<thead>
<tr>
<th>Business Area</th>
<th>Analytical Question</th>
</tr>
</thead>
<tbody>
<tr>
<td>Customer Retention</td>
<td>Which customer segments demonstrate the highest churn rates?</td>
</tr>
<tr>
<td>Customer Lifecycle</td>
<td>How does customer tenure relate to attrition behavior?</td>
</tr>
<tr>
<td>Contract Strategy</td>
<td>How do month-to-month, one-year, and two-year contracts differ in retention performance?</td>
</tr>
<tr>
<td>Service Analysis</td>
<td>Which subscribed services are associated with higher customer attrition?</td>
</tr>
<tr>
<td>Revenue Exposure</td>
<td>What recurring revenue is associated with customers carrying elevated predicted churn risk?</td>
</tr>
<tr>
<td>Risk Prioritization</td>
<td>Which customers combine high churn probability with substantial revenue contribution?</td>
</tr>
<tr>
<td>Retention Investment</td>
<td>What is the potential financial impact of targeted retention interventions?</td>
</tr>
</tbody>
</table>

<h2>3. Dataset Overview</h2>

<p>
The project uses a telecommunications customer dataset containing
7,043 customer records and 21 variables. It includes demographic
characteristics, subscription information, contractual arrangements,
billing details, customer tenure, and historical churn outcomes.
</p>

<h3>Dataset Characteristics</h3>

<table>
<thead>
<tr>
<th>Attribute</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>Records</td>
<td>7,043 customer observations</td>
</tr>
<tr>
<td>Variables</td>
<td>21 features</td>
</tr>
<tr>
<td>Customer Identifier</td>
<td>CustomerID</td>
</tr>
<tr>
<td>Target Variable</td>
<td>Churn</td>
</tr>
<tr>
<td>Data Types</td>
<td>Numerical, categorical, and binary</td>
</tr>
<tr>
<td>Industry</td>
<td>Telecommunications</td>
</tr>
</tbody>
</table>

<h3>Analytical Variable Categories</h3>

<table>
<thead>
<tr>
<th>Category</th>
<th>Variables</th>
<th>Analytical Purpose</th>
</tr>
</thead>
<tbody>
<tr>
<td>Customer Identification</td>
<td>CustomerID</td>
<td>Record identification and uniqueness validation</td>
</tr>
<tr>
<td>Demographics</td>
<td>Gender, SeniorCitizen, Partner, Dependents</td>
<td>Customer profile segmentation</td>
</tr>
<tr>
<td>Customer Lifecycle</td>
<td>Tenure</td>
<td>Customer retention and lifecycle analysis</td>
</tr>
<tr>
<td>Contractual Information</td>
<td>Contract, PaperlessBilling, PaymentMethod</td>
<td>Contract and billing behavior</td>
</tr>
<tr>
<td>Service Subscriptions</td>
<td>PhoneService, InternetService, OnlineSecurity, TechSupport, StreamingServices</td>
<td>Service-level churn investigation</td>
</tr>
<tr>
<td>Financial Information</td>
<td>MonthlyCharges, TotalCharges</td>
<td>Revenue contribution and financial assessment</td>
</tr>
<tr>
<td>Target Variable</td>
<td>Churn</td>
<td>Historical customer attrition</td>
</tr>
</tbody>
</table>

<h2>4. Data Quality Assessment and Preparation</h2>

<p>
Before conducting the analysis, the raw dataset was examined for
structural inconsistencies, missing information, duplicate observations,
and formatting issues.
</p>

<h3>Data Quality Assessment</h3>

<table>
<thead>
<tr>
<th>Quality Check</th>
<th>Result</th>
</tr>
</thead>
<tbody>
<tr>
<td>Total Records</td>
<td>7,043</td>
</tr>
<tr>
<td>Unique Customer Identifiers</td>
<td>7,043</td>
</tr>
<tr>
<td>Duplicate Records</td>
<td>0</td>
</tr>
<tr>
<td>Whitespace Entries in TotalCharges</td>
<td>11</td>
</tr>
<tr>
<td>Missing Values After Cleaning</td>
<td>0</td>
</tr>
</tbody>
</table>

<h3>Data Preparation Activities</h3>

<ul>
<li>Inspected dataset dimensions, variable types, and categorical distributions.</li>
<li>Verified customer identifier uniqueness.</li>
<li>Identified and investigated duplicate observations.</li>
<li>Resolved whitespace-related entries in <code>TotalCharges</code>.</li>
<li>Converted financial variables into appropriate numerical formats.</li>
<li>Reviewed numerical distributions and potential outliers.</li>
<li>Prepared categorical and numerical variables for downstream analysis.</li>
<li>Standardized the analytical dataset for SQL queries and predictive modeling.</li>
</ul>

<p>
The objective was to establish a consistent analytical foundation
while preserving the underlying customer information.
</p>

<h2>5. SQL-Based Customer and Revenue Analysis</h2>

<p>
SQL was used to investigate customer characteristics, examine
attrition patterns, and evaluate recurring revenue across
different customer segments.
</p>

<h3>5.1 Customer Segmentation</h3>

<p>
Customers were grouped according to their contractual arrangements,
tenure, subscribed services, billing characteristics, and historical
churn status.
</p>

<p>
This segmentation provided a structured basis for comparing customer
retention performance and identifying groups with elevated attrition.
</p>

<h3>5.2 Churn Rate Analysis</h3>

<p>
Churn rates were calculated across customer segments to quantify
differences in retention performance.
</p>

<p><strong>Calculation:</strong></p>

<pre><code>Churn Rate =
(Churned Customers / Total Customers) × 100</code></pre>

<p>
The resulting comparisons helped identify customer categories
with disproportionately high attrition rates.
</p>

<h3>5.3 Contract and Tenure Cohort Analysis</h3>

<p>
A cohort-based approach was used to examine how customer retention
varies according to contract duration and length of service.
</p>

<table>
<thead>
<tr>
<th>Contract Type</th>
<th>Tenure Group</th>
<th>Churn Rate</th>
</tr>
</thead>
<tbody>
<tr>
<td>Month-to-month</td>
<td>0–12 months</td>
<td>51.35%</td>
</tr>
<tr>
<td>Month-to-month</td>
<td>13–24 months</td>
<td>37.72%</td>
</tr>
<tr>
<td>Month-to-month</td>
<td>Above 24 months</td>
<td>30.86%</td>
</tr>
<tr>
<td>One-year</td>
<td>0–12 months</td>
<td>10.48%</td>
</tr>
<tr>
<td>One-year</td>
<td>13–24 months</td>
<td>8.12%</td>
</tr>
<tr>
<td>One-year</td>
<td>Above 24 months</td>
<td>11.89%</td>
</tr>
<tr>
<tr>
<td>Two-year</td>
<td>0-12 months</td>
<td>0.00%</td>
</tr>
<tr>
<td>Two-year</td>
<td>13-24 months</td>
<td>0.00%</td>
</tr>
<td>Two-year</td>
<td>Above 24 months</td>
<td>3.12%</td>
</tr>
</tbody>
</table>

<p><strong>Business Interpretation</strong></p>

<ul>
<li> Early Lifecycle Trap: 51.35% of 0-12 Month M-to-M users churn, losing $68,301.45/mo (49% of total MRR loss).
</li>
<li> Contract Protection: 1-Year contracts drop early churn to 10.48%; 2-Year contracts eliminate 0-24 mo churn.
</li>
<li> Total M-to-M Exposure: Month-to-Month accounts accumulate $120,847.10/mo in direct revenue leakage.
</li>
</ul>

<h2>6. Statistical Analysis and Customer Survival</h2>

<p>
Descriptive analysis was supplemented with statistical methods
to investigate customer retention patterns and examine relationships
between customer characteristics and historical attrition.
</p>

<h3>Areas of Investigation</h3>

<ul>
<li>Differences in churn rates across contract categories.</li>
<li>Relationships between customer tenure and attrition.</li>
<li>Differences in financial characteristics between customer groups.</li>
<li>Customer lifecycle and retention patterns.</li>
<li>Statistical evidence supporting observed differences.</li>
</ul>

<h3>Kaplan-Meier Survival Analysis</h3>

<p>
Survival analysis was incorporated to examine customer retention
over time. The Kaplan-Meier estimator provides an estimate of the
probability that a customer remains active beyond a specified duration.
</p>

<p><strong>Survival Function:</strong></p>

<pre><code>S(t) = P(T &gt; t)</code></pre>

<p>Where:</p>

<ul>
<li><code>S(t)</code> represents the probability of remaining a customer beyond time t.</li>
<li><code>T</code> represents customer lifetime.</li>
<li><code>t</code> represents the duration of the customer relationship.</li>
</ul>

<p>
The Lifelines library was used for survival analysis, providing
a lifecycle-oriented perspective that complements conventional
churn-rate comparisons.
</p>

<h2>7. Predictive Modeling and Customer Risk Assessment</h2>

<p>
Historical churn analysis explains observed customer behavior,
while predictive modeling provides a framework for estimating
the probability of attrition at the individual customer level.
</p>

<p>
Multiple classification algorithms were evaluated to compare
their ability to distinguish between customers who churn and
customers who remain.
</p>

<h3>7.1 Logistic Regression</h3>

<p>
Logistic Regression was implemented as an interpretable baseline
classification model. It estimates the probability of a binary
outcome using a logistic function.
</p>

<p>
Its performance provides a benchmark against which more complex
classification algorithms can be assessed.
</p>

<h3>7.2 Random Forest</h3>

<p>
Random Forest combines predictions from multiple decision trees.
It provides a flexible modeling approach capable of capturing
nonlinear relationships and interactions among customer characteristics.
</p>

<h3>7.3 XGBoost</h3>

<p>
XGBoost applies gradient boosting to construct an ensemble of
decision trees through sequential optimization.
</p>

<p>
It was evaluated to determine whether boosting could improve
predictive discrimination relative to the baseline and
Random Forest models.
</p>

<h3>7.4 Model Performance Comparison</h3>

<table>
<thead>
<tr>
<th>Model</th>
<th>ROC-AUC</th>
</tr>
</thead>
<tbody>
<tr>
<td>Logistic Regression</td>
<td>0.8407</td>
</tr>
<tr>
<td>Random Forest</td>
<td>0.8420</td>
</tr>
<tr>
<td><strong>XGBoost</strong></td>
<td><strong>0.8432</strong></td>
</tr>
</tbody>
</table>

<p>
XGBoost achieved the highest ROC-AUC among the evaluated models,
indicating the strongest overall ranking performance in this comparison.
</p>

<h3>7.5 Classification Threshold Assessment</h3>

<p>
Predictive models generate probabilities rather than fixed customer
classifications. A classification threshold determines when a
customer is flagged as a potential churner.
</p>

<p>
At the conventional 0.50 threshold, the model achieved a recall
of 81.82%.
</p>

<p>
An additional threshold experiment achieved 100% recall but
classified every test customer as a potential churner, producing
zero true negatives.
</p>

<p>
Although this approach eliminates false negatives in the evaluated
test set, it offers limited operational value because it does not
distinguish between customers according to their relative risk.
</p>

<p>
This demonstrates the importance of balancing sensitivity,
specificity, intervention capacity, and the financial consequences
of classification errors when selecting a decision threshold.
</p>

<h3>7.6 Model Interpretability with SHAP</h3>

<p>
SHAP (SHapley Additive exPlanations) was used to examine how
individual customer characteristics contribute to model predictions.
</p>

<p><strong>Influential features identified:</strong></p>

<ol>
<li>Two-year contract.</li>
<li>Customer tenure.</li>
<li>Fiber-optic internet service.</li>
<li>One-year contract.</li>
<li>Monthly charges.</li>
</ol>

<p>
The interpretation process provides greater transparency into
the model's predictions and helps translate predictive outputs
into business-relevant customer characteristics.
</p>

<p>
Feature importance indicates model association and should not
automatically be interpreted as evidence of causation.
</p>

<h2>8. Revenue at Risk: Probability-Weighted Financial Assessment</h2>

<p>
A central component of the project is connecting predictive
churn analysis with financial exposure.
</p>

<p>
Traditional churn reporting often focuses on the number or
percentage of customers expected to leave. However, the financial
significance of customer attrition also depends on the recurring
revenue contribution of individual accounts.
</p>

<p>
To incorporate this dimension, the project applies a
probability-weighted revenue exposure metric.
</p>

<h3>8.1 Probability-Weighted Churn Exposure (pCaR)</h3>

<p><strong>Monthly Calculation:</strong></p>

<pre><code>Monthly pCaR =
Predicted Churn Probability × Monthly Charges</code></pre>

<p><strong>Annualized Calculation:</strong></p>

<pre><code>Annualized pCaR =
Monthly pCaR × 12</code></pre>

<h3>8.2 Illustrative Customer-Level Calculation</h3>

<p>
Consider a hypothetical customer with monthly charges of $100
and a predicted churn probability of 70%.
</p>

<table>
<thead>
<tr>
<th>Metric</th>
<th>Calculation</th>
<th>Value</th>
</tr>
</thead>
<tbody>
<tr>
<td>Monthly Charges</td>
<td>Given</td>
<td>$100</td>
</tr>
<tr>
<td>Churn Probability</td>
<td>Given</td>
<td>70%</td>
</tr>
<tr>
<td>Monthly pCaR</td>
<td>0.70 × 100</td>
<td>$70</td>
</tr>
<tr>
<td>Annualized pCaR</td>
<td>70 × 12</td>
<td>$840</td>
</tr>
</tbody>
</table>

<p>
The resulting $840 represents probability-weighted annualized
recurring revenue exposure. It is not a confirmed future loss.
</p>

<h3>8.3 Test Portfolio Financial Assessment</h3>

<p>
The exposure calculations were applied to the 1,409-customer
test portfolio.
</p>

<table>
<thead>
<tr>
<th>Portfolio Metric</th>
<th>Estimated Value</th>
</tr>
</thead>
<tbody>
<tr>
<td>Test Portfolio Size</td>
<td>1,409 customers</td>
</tr>
<tr>
<td>Monthly Recurring Revenue</td>
<td>$90,301.20</td>
</tr>
<tr>
<td>Annualized Recurring Revenue</td>
<td>$1,083,614.40</td>
</tr>
<tr>
<td>Expected Monthly pCaR</td>
<td>$41,749.91</td>
</tr>
<tr>
<td>Annualized pCaR</td>
<td>$500,998.97</td>
</tr>
<tr>
<td>pCaR / Monthly Revenue</td>
<td>46.23%</td>
</tr>
</tbody>
</table>

<p>
The results indicate that a substantial proportion of the test
portfolio's recurring revenue is associated with customers carrying
predicted churn risk.
</p>

<p>
The 46.23% ratio represents probability-weighted monthly exposure
relative to monthly recurring revenue. It should not be interpreted
as a forecast that 46.23% of revenue will actually be lost.
</p>

<h3>8.4 Revenue Exposure by Customer Segment</h3>

<table>
<thead>
<tr>
<th>Customer Segment</th>
<th>Estimated Monthly Revenue Exposure</th>
</tr>
</thead>
<tbody>
<tr>
<td>Early-Tenure Month-to-Month Customers</td>
<td>$68,301.45</td>
</tr>
<tr>
<td>All Month-to-Month Customers</td>
<td>$120,847.10</td>
</tr>
</tbody>
</table>

<p>
The early-tenure month-to-month segment accounted for approximately
49% of the total monthly revenue associated with churned accounts
in the reported analysis.
</p>

<p>
This highlights the commercial importance of examining customer
attrition alongside recurring revenue contribution.
</p>

<h2>9. High-Priority Customer Identification</h2>

<p>
To translate portfolio-level findings into an actionable customer
prioritization framework, predicted churn probability was combined
with monthly revenue contribution.
</p>

<h3>Prioritization Criteria</h3>

<ul>
<li><strong>Churn Risk:</strong> Predicted churn probability of at least 60%.</li>
<li><strong>Revenue Contribution:</strong> Monthly charges at or above the portfolio median of $69.95.</li>
</ul>

<p>
This framework identifies customers who combine elevated predicted
attrition risk with comparatively high recurring revenue contribution.
</p>

<h3>Priority Segment Results</h3>

<table>
<thead>
<tr>
<th>Metric</th>
<th>Result</th>
</tr>
</thead>
<tbody>
<tr>
<td>Priority Customers</td>
<td>349</td>
</tr>
<tr>
<td>Share of Test Portfolio</td>
<td>24.77%</td>
</tr>
<tr>
<td>Annualized pCaR</td>
<td>$282,247.21</td>
</tr>
<tr>
<td>Share of Portfolio pCaR</td>
<td>56.34%</td>
</tr>
</tbody>
</table>

<p>
The priority segment represents approximately one-quarter of
the test portfolio while accounting for more than half of its
estimated probability-weighted revenue exposure.
</p>

<p>
This concentration provides a potential basis for more selective
retention resource allocation rather than applying identical
interventions across the entire customer portfolio.
</p>

<h2>10. Retention Investment and ROI Scenario Analysis</h2>

<p>
After identifying customers with elevated churn risk and
comparatively high revenue contribution, a hypothetical
retention intervention was developed to assess its potential
financial implications.
</p>

<h3>10.1 Intervention Assumptions</h3>

<table>
<thead>
<tr>
<th>Component</th>
<th>Scenario Assumption</th>
</tr>
</thead>
<tbody>
<tr>
<td>Targeted Customers</td>
<td>349</td>
</tr>
<tr>
<td>Monthly Customer Discount</td>
<td>$10</td>
</tr>
<tr>
<td>Monthly Support Subsidy</td>
<td>$5</td>
</tr>
<tr>
<td>Total Monthly Intervention Cost per Customer</td>
<td>$15</td>
</tr>
<tr>
<td>Annual Intervention Cost per Customer</td>
<td>$180</td>
</tr>
<tr>
<td>Assumed Relative Churn Probability Reduction</td>
<td>35%</td>
</tr>
</tbody>
</table>

<h3>10.2 Financial Calculations</h3>

<p><strong>Annual Intervention Cost</strong></p>

<pre><code>349 × $15 × 12 = $62,820</code></pre>

<p><strong>Estimated Annual Revenue Preserved</strong></p>

<pre><code>$282,247.21 × 35% = $98,786.52</code></pre>

<p><strong>Estimated Net Financial Benefit</strong></p>

<pre><code>$98,786.52 - $62,820 = $35,966.52</code></pre>

<p><strong>Benefit-to-Cost Ratio</strong></p>

<pre><code>$98,786.52 / $62,820 = 1.57x</code></pre>

<p><strong>Estimated Net ROI</strong></p>

<pre><code>($35,966.52 / $62,820) × 100 = 57.3%</code></pre>

<h3>10.3 Scenario Results</h3>

<table>
<thead>
<tr>
<th>Financial Indicator</th>
<th>Estimated Value</th>
</tr>
</thead>
<tbody>
<tr>
<td>Annual Intervention Cost</td>
<td>$62,820.00</td>
</tr>
<tr>
<td>Estimated Annual Revenue Preserved</td>
<td>$98,786.52</td>
</tr>
<tr>
<td>Estimated Net Benefit</td>
<td>$35,966.52</td>
</tr>
<tr>
<td>Benefit-to-Cost Ratio</td>
<td>1.57x</td>
</tr>
<tr>
<td>Estimated Net ROI</td>
<td>57.3%</td>
</tr>
</tbody>
</table>

<p>
Under the specified assumptions, the modeled intervention produces
an estimated net benefit of $35,966.52.
</p>

<p>
The scenario illustrates how predictive analytics can be integrated
with financial assessment to evaluate potential customer retention
investments.
</p>

<p>
<strong>Financial qualification:</strong> The assumed 35% relative
reduction in churn probability has not been experimentally validated.
These results represent a hypothetical scenario, not observed
incremental revenue, realized profit, or proven intervention returns.
A controlled experiment would be required to establish the actual
effectiveness of the proposed strategy.
</p>

<h2>11. Business Intelligence and Tableau Visualization</h2>

<p>
Tableau was used to communicate the analytical findings through
interactive visualizations designed to make customer attrition,
revenue exposure, and retention priorities more accessible.
</p>

<h3>Visualization Areas</h3>

<ul>
<li>Executive-level customer and churn overview.</li>
<li>Customer segment vulnerability.</li>
<li>Contract and tenure-based churn patterns.</li>
<li>Revenue exposure analysis.</li>
<li>Customer prioritization and retention insights.</li>
</ul>

<h3>Dashboard Previews</h3>

<p align="center">
  <img src="images/executive_overview.png"
       alt="Executive Customer Churn Overview"
       width="90%">
</p>
<p align="center"><em>Executive overview of customer attrition and revenue exposure.</em></p>

<p align="center">
  <img src="images/product_vulnerability.png"
       alt="Customer Segment Vulnerability"
       width="90%">
</p>
<p align="center"><em>Customer vulnerability across service and contract segments.</em></p>

<p align="center">
  <img src="images/retention_analysis.png"
       alt="Customer Retention Analysis"
       width="90%">
</p>
<p align="center"><em>Customer retention analysis and prioritization.</em></p>

<p align="center">
  <a href="https://public.tableau.com/app/profile/maira.zarnab/vizzes">
    <strong>Explore Interactive Tableau Visualizations</strong>
  </a>
</p>

<h2>12. Key Business Findings</h2>

<table>
<thead>
<tr>
<th>Finding</th>
<th>Business Significance</th>
</tr>
</thead>
<tbody>
<tr>
<td>Month-to-month customers demonstrate higher churn rates.</td>
<td>Contract structure is an important dimension for retention analysis.</td>
</tr>
<tr>
<td>Early-tenure customers exhibit elevated attrition.</td>
<td>Early customer engagement deserves particular attention.</td>
</tr>
<tr>
<td>Churn risk varies across customer and service characteristics.</td>
<td>Retention strategies should account for customer heterogeneity.</td>
</tr>
<tr>
<td>XGBoost achieved the highest ROC-AUC among the evaluated models.</td>
<td>Predictive modeling can support customer risk ranking.</td>
</tr>
<tr>
<td>Revenue exposure is concentrated within the high-priority segment.</td>
<td>Retention resources can be directed toward customers with greater estimated financial exposure.</td>
</tr>
<tr>
<td>The hypothetical intervention scenario produces a positive modeled net benefit.</td>
<td>Scenario analysis can support preliminary retention investment assessment.</td>
</tr>
</tbody>
</table>

<h2>13. Strategic Recommendations</h2>

<h3>13.1 Strengthen Early Customer Engagement</h3>

<p>
Prioritize customer engagement during the first year of service,
particularly among month-to-month subscribers. Potential initiatives
include improved onboarding, proactive service reviews, and early
identification of customer dissatisfaction.
</p>

<h3>13.2 Evaluate Contract-Based Retention Strategies</h3>

<p>
Investigate opportunities to improve long-term contract adoption
among month-to-month customers. Any proposed incentives should be
evaluated against their effect on recurring revenue and subscription
margins.
</p>

<h3>13.3 Introduce Risk-Based Customer Prioritization</h3>

<p>
Use predicted churn probabilities alongside recurring revenue
contribution to identify customers who may warrant more immediate
retention attention.
</p>

<h3>13.4 Monitor Customer Revenue Exposure</h3>

<p>
Incorporate probability-weighted churn exposure into recurring
customer portfolio reviews. Monitoring changes in customer-level
risk scores can help identify shifts in estimated portfolio exposure.
</p>

<h3>13.5 Validate Retention Interventions</h3>

<p>
Use controlled experiments to evaluate the effectiveness of
discounts, support improvements, and other retention initiatives.
Measure actual retention outcomes, incremental revenue, intervention
costs, and customer lifetime value before scaling an intervention.
</p>

<h2>14. Technology Stack</h2>

<table>
<thead>
<tr>
<th>Analytical Component</th>
<th>Technology</th>
<th>Application</th>
</tr>
</thead>
<tbody>
<tr>
<td>Data Preparation</td>
<td>Python, Pandas, NumPy</td>
<td>Data cleaning, transformation, and feature preparation</td>
</tr>
<tr>
<td>Database Analysis</td>
<td>SQL, SQLite</td>
<td>Customer segmentation and structured analytical queries</td>
</tr>
<tr>
<td>Statistical Analysis</td>
<td>SciPy</td>
<td>Statistical investigation and hypothesis testing</td>
</tr>
<tr>
<td>Survival Analysis</td>
<td>Lifelines</td>
<td>Customer retention and survival analysis</td>
</tr>
<tr>
<td>Predictive Modeling</td>
<td>Scikit-learn</td>
<td>Classification, evaluation, and validation</td>
</tr>
<tr>
<td>Gradient Boosting</td>
<td>XGBoost</td>
<td>Predictive churn modeling</td>
</tr>
<tr>
<td>Model Interpretation</td>
<td>SHAP</td>
<td>Feature contribution and model explainability</td>
</tr>
<tr>
<td>Data Visualization</td>
<td>Tableau, Matplotlib</td>
<td>Analytical reporting and dashboard development</td>
</tr>
<tr>
<td>Development Environment</td>
<td>Jupyter Notebook</td>
<td>Reproducible analytical workflow</td>
</tr>
</tbody>
</table>

<h2>15. Project Deliverables</h2>

<ul>
<li>Cleaned and analysis-ready customer dataset.</li>
<li>SQL-based customer segmentation and revenue analysis.</li>
<li>Statistical investigation of customer attrition patterns.</li>
<li>Customer survival analysis.</li>
<li>Predictive churn models and comparative performance evaluation.</li>
<li>Model interpretation and feature importance assessment.</li>
<li>Probability-weighted revenue exposure estimates.</li>
<li>Prioritized customer retention segments.</li>
<li>Hypothetical retention investment and ROI assessment.</li>
<li>Interactive Tableau dashboards.</li>
</ul>

<h2>16. Project Limitations and Analytical Considerations</h2>

<p>
A rigorous analytical assessment requires distinguishing predictive
estimates from realized business outcomes. The following limitations
should be considered when interpreting the findings:
</p>

<ol>
<li><strong>Historical Data:</strong> The analysis reflects patterns in the available dataset and may not fully represent future customer behavior.</li>
<li><strong>Predictive Performance:</strong> ROC-AUC evaluates discriminatory performance but does not independently establish probability calibration or operational effectiveness.</li>
<li><strong>Revenue Exposure:</strong> pCaR is a probability-weighted recurring revenue estimate, not a confirmed financial loss.</li>
<li><strong>Retention Assumptions:</strong> The assumed 35% relative reduction in churn probability has not been validated through an experiment.</li>
<li><strong>Causal Interpretation:</strong> Statistical associations and model feature contributions should not automatically be interpreted as causal effects.</li>
<li><strong>Generalizability:</strong> Findings from one telecommunications dataset may not transfer directly to other businesses or customer populations.</li>
</ol>

<h2>17. Repository Structure</h2>

<pre><code>Enterprise-Revenue-Protection/
│
├── README.md
│
├── data/
│   └── telco_churn.csv
│
├── sql/
│   └── churn_analysis.sql
│
├── notebooks/
│   └── churn_prediction_analysis.ipynb
│
├── tableau/
│   └── revenue_protection_dashboard.twbx
│
└── images/
    ├── executive_overview.png
    ├── product_vulnerability.png
    └── retention_analysis.png
</code></pre>

<h2>18. Conclusion</h2>

<p>
This project demonstrates how multiple analytical disciplines
can be integrated to address a commercially relevant business problem.
</p>

<p>
By combining data preparation, SQL-based investigation, statistical
analysis, survival analysis, predictive modeling, model interpretation,
and probability-weighted financial assessment, the project establishes
a structured approach to understanding customer attrition and its
potential financial implications.
</p>

<p>
The analysis progresses from identifying customer behavior to
evaluating revenue exposure and developing a framework for
prioritizing retention efforts.
</p>

<p>
Its broader objective is to demonstrate how data analytics can
support business decisions by connecting customer intelligence
with financial considerations, improving portfolio visibility,
and informing evidence-based retention strategies.
</p>

<hr>

<div align="center">

<h3>Customer Intelligence | Predictive Analytics | Financial Assessment | Business Intelligence</h3>

<p><em>Turning customer data into commercially relevant insights.</em></p>

</div>
