
<div align="center">
  <h2>ENTERPRISE REVENUE PROTECTION: Customer Churn &amp; Financial Risk Analytics</h2>
  <p><strong>End-to-End Data Analytics Project</strong></p>
  <p>SQL | Python | Statistical Analysis | Machine Learning | Revenue Intelligence</p>
  </a>



  <p align="center">
  <a href="https://public.tableau.com/app/profile/maira.zarnab/viz/Book1_17837346834310/Executive_Overview" target="_blank">Tableau Dashboards</a>
  &nbsp; • &nbsp;
  <a href="http://localhost:8888/notebooks/Work/Tech/Projects/Untitled.ipynb" target="_blank">Jupyter Notebook</a>
</p>
</div>

<hr>

<h2>1. Executive Summary</h2>

<p>Customer churn is not simply a customer-retention problem. It represents a recurring revenue risk that can affect financial performance, customer lifetime value, and long-term business growth.</p>

<p>This project develops an end-to-end analytical framework to identify customer churn patterns, quantify recurring revenue exposure, predict churn risk, and prioritize retention interventions based on potential financial impact. Using a dataset of <strong>7,043 telecom customers</strong>, I integrated SQL-based analytics, statistical hypothesis testing, survival analysis, predictive modeling, and financial scenario analysis to move from historical churn reporting toward forward-looking revenue protection.</p>



</blockquote>

<h3>Project Highlights</h3>

<table>
  <thead>
    <tr>
      <th>Analytical Area</th>
      <th>Key Result</th>
    </tr>
  </thead>
  <tbody>
    <tr><td>Customers analyzed</td><td>7,043</td></tr>
    <tr><td>Highest-risk contract segment</td><td>Month-to-Month</td></tr>
    <tr><td>Month-to-month churn rate (0–12 months)</td><td>51.35%</td></tr>
    <tr><td>XGBoost ROC-AUC</td><td>0.8387</td></tr>
    <tr><td>Test-set annualized revenue exposure</td><td>$500,998.97</td></tr>
    <tr><td>High-risk, high-value customers</td><td>349</td></tr>
    <tr><td>Share of estimated exposure in target segment</td><td>56.34%</td></tr>
    <tr><td>Hypothetical retention campaign ROI</td><td>57.3%</td></tr>
  </tbody>
</table>


<hr>

<h2>2. Project Objectives</h2>

<ol>

  <li>How can retention resources be prioritized to protect recurring revenue?</li>
  <li>How much recurring revenue is associated with customer churn? </li>
  <li>Which factors are most strongly associated with customer chrun? </li>
  <li>How does customer retention change over time and across different contract types? </li>
  <li> How accurately can customer-level churn probabilities be predicted, and which factors influence those predictions?</li>
</ol>

<hr>

<h2>3. Dataset &amp; Analytical Scope</h2>

<table>
  <thead>
    <tr><th>Data Category</th><th>Variables</th></tr>
  </thead>
  <tbody>
    <tr><td>Customer Information</td><td>Customer ID, gender, senior citizen, partner, dependents</td></tr>
    <tr><td>Account Information</td><td>Tenure, contract type, payment method, paperless billing</td></tr>
    <tr><td>Services</td><td>Internet service, online security, backup, device protection, tech support, streaming</td></tr>
    <tr><td>Financial Information</td><td>Monthly charges, total charges</td></tr>
    <tr><td>Target Variable</td><td>Churn</td></tr>
  </tbody>
</table>

<h3>Data Preparation &amp; Quality Assessment</h3>

<ul>
  <li>Identified missing and inconsistent values.</li>
  <li>Resolved whitespace-related inconsistencies in <code>TotalCharges</code>.</li>
  <li>Converted financial and tenure variables to appropriate data types.</li>
  <li>Standardized categorical service values.</li>
  <li>Checked duplicate customer records and customer identifiers.</li>
  <li>Created a binary churn indicator for statistical and machine-learning analysis.</li>
  <li>Prepared analytical variables for customer segmentation and revenue calculations.</li>
</ul>

<p>The cleaned dataset was subsequently organized into a relational SQLite database.</p>

<hr>

<h2>4. Analytical Architecture</h2>

<p>The project follows a structured analytical workflow, progressing from raw customer records to business recommendations.</p>

<div align="center">
  <svg viewBox="0 0 700 830" width="100%" xmlns="http://www.w3.org/2000/svg">
    <defs>
      <marker id="arrow" markerWidth="8" markerHeight="8" refX="5" refY="3" orient="auto">
        <path d="M0,0 L0,6 L6,3 z" fill="#64748b"/>
      </marker>
    </defs>
    <g fill="#e8f0fe" stroke="#5277aa" stroke-width="1.5">
      <rect x="170" y="15" width="360" height="48" rx="8"/>
      <rect x="170" y="105" width="360" height="48" rx="8"/>
      <rect x="170" y="195" width="360" height="48" rx="8"/>
      <rect x="170" y="285" width="360" height="48" rx="8"/>
      <rect x="170" y="375" width="360" height="48" rx="8"/>
      <rect x="170" y="465" width="360" height="48" rx="8"/>
      <rect x="170" y="555" width="360" height="48" rx="8"/>
      <rect x="170" y="645" width="360" height="48" rx="8"/>
      <rect x="170" y="735" width="360" height="48" rx="8"/>
    </g>
    <g fill="#17365d" font-size="15" text-anchor="middle" font-family="Arial">
      <text x="350" y="45">Raw Telecom Dataset — 7,043 Customers</text>
      <text x="350" y="135">Data Quality Assessment</text>
      <text x="350" y="225">Data Cleaning &amp; Transformation</text>
      <text x="350" y="315">SQLite Relational Database</text>
      <text x="350" y="405">SQL Segmentation &amp; Revenue Analysis</text>
      <text x="350" y="495">Statistical &amp; Survival Analysis</text>
      <text x="350" y="585">Predictive Modeling &amp; SHAP</text>
      <text x="350" y="675">Probability-Weighted Revenue Exposure</text>
      <text x="350" y="765">Retention Strategy &amp; ROI Assessment</text>
    </g>
    <g stroke="#64748b" stroke-width="2" marker-end="url(#arrow)">
      <path d="M350 63 V103"/>
      <path d="M350 153 V193"/>
      <path d="M350 243 V283"/>
      <path d="M350 333 V373"/>
      <path d="M350 423 V463"/>
      <path d="M350 513 V553"/>
      <path d="M350 603 V643"/>
      <path d="M350 693 V733"/>
    </g>
  </svg>
</div>

<h3>Database Design</h3>
<p> The database was organized into three relational tables using a dimensional modeling approach to improve data organization, consistency, and analytical efficiency."</p>
<table>
  <thead>
    <tr><th>Table</th><th>Purpose</th></tr>
  </thead>
  <tbody>
    <tr><td><code>dim_customers</code></td><td>Customer-level demographic and account attributes</td></tr>
    <tr><td><code>dim_services</code></td><td>Customer service subscriptions and configurations</td></tr>
    <tr><td><code>fact_customer_billing</code></td><td>Tenure, monthly charges, total charges, and churn-related financial measures</td></tr>
  </tbody>
</table>

<hr>

<h2>5. SQL Analysis: Customer Segmentation &amp; Revenue Exposure</h2>

<p>The first analytical stage focused on understanding how customer churn varies across account tenure and contract types.</p>

<p>SQL was used to calculate customer counts by tenure, churn rates by contract type, monthly recurring revenue associated with churned customers, average revenue per user, and revenue exposure across customer segments.</p>

<h3>5.1 Month-to-Month Customer Segmentation Analysis</h3>

<table>
  <thead>
    <tr>
      <th>Customer Tenure</th>
      <th>Customers</th>
      <th>Churn Rate</th>
      <th>Direct MRR Lost</th>
    </tr>
  </thead>
  <tbody>
    <tr><td>0–12 months</td><td>1,994</td><td>51.35%</td><td>$68,301.45</td></tr>
    <tr><td>13–24 months</td><td>737</td><td>37.72%</td><td>$21,980.30</td></tr>
    <tr><td>25–48 months</td><td>802</td><td>32.92%</td><td>$22,557.00</td></tr>
    <tr><td>Above 48 months</td><td>342</td><td>26.02%</td><td>$8,008.35</td></tr>
    <tr><strong><td>Total</td><td>3,875</td><td>—</td><td>$120,847.10</td></strong></tr>
  </tbody>
</table>


<h3>Business Interpretation</h3>

<p>Customer churn is concentrated in the early lifecycle. The first 12 months represent the most vulnerable period, with a churn rate of 51.35%.</p>

<p>The declining churn rate across longer-tenure cohorts suggests that early customer engagement, onboarding, and service experience may be important areas for retention intervention.</p>

<p>The first-year customer segment also represents the largest direct monthly recurring revenue loss among the cohorts examined.</p>


<h2>6. Statistical Analysis: Identifying Churn Drivers</h2>

<p>Statistical hypothesis testing was used to determine whether observed differences in customer characteristics were associated with churn.</p>

<h3>6.1 Chi-Square Tests of Independence</h3>

<p>The chi-square test was applied to evaluate associations between churn and selected categorical variables.</p>

<table>
  <thead>
    <tr><th>Variable</th><th>Chi-Square Statistic</th><th>P-Value</th></tr>
  </thead>
  <tbody>
    <tr><td>Contract Type</td><td>1,184.60</td><td>5.86 × 10⁻²⁵⁸</td></tr>
    <tr><td>Internet Service</td><td>732.31</td><td>9.57 × 10⁻¹⁶⁰</td></tr>
    <tr><td>Automatic Payment</td><td>309.35</td><td>3.03 × 10⁻⁶⁹</td></tr>
    <tr><td>Tech Support</td><td>190.17</td><td>2.92 × 10⁻⁴³</td></tr>
  </tbody>
</table>


<p><strong>Interpretation:</strong> Contract type produced the largest chi-square statistic among the variables examined, followed by internet service and payment method.</p>

<p>These results provide strong evidence of statistical association. They do not establish that any individual variable directly causes churn.</p>

<h3>6.2 Monthly Billing Differences</h3>

<p>Welch's independent-samples t-test was used to compare monthly charges between churned and retained customers.</p>

<table>
  <thead><tr><th>Metric</th><th>Churned Customers</th><th>Retained Customers</th></tr></thead>
  <tbody>
    <tr><td>Mean Monthly Charges</td><td>$74.44</td><td>$61.27</td></tr>
    <tr><td>Standard Deviation</td><td>$24.67</td><td>$31.09</td></tr>
  </tbody>
</table>

<h4>Test Results</h4>

<ul>
  <li>t-statistic: 18.4075</li>
  <li>P-value: 8.59 × 10⁻⁷³</li>
  <li>Mean difference: $13.18</li>
</ul>

<p><strong>Business Interpretation:</strong> Churned customers had higher average monthly charges than retained customers. This suggests that customers with higher recurring bills may represent an important segment for further investigation and targeted retention analysis.</p>

<hr>

<h2>7. Survival Analysis: Understanding Customer Lifecycle</h2>

<p>A Kaplan–Meier survival estimator was used to examine the probability that a customer remains active over time.</p>

<p>Unlike a conventional churn-rate comparison, survival analysis incorporates the timing of customer churn and provides a lifecycle-oriented view of retention.</p>

<p>The Kaplan–Meier estimator is defined as:</p>

<p><code>S(t) = Product of (1 - d_i / n_i)</code></p>

<ul>
  <li><code>t_i</code> represents an observed event time.</li>
  <li><code>d_i</code> represents the number of churn events at time <code>t_i</code>.</li>
  <li><code>n_i</code> represents the number of customers at risk immediately before time <code>t_i</code>.</li>
</ul>

<h3>7.1 Customer Retention Over Time</h3>

<table>
  <thead><tr><th>Customer Tenure</th><th>Estimated Retention Probability</th></tr></thead>
  <tbody>
    <tr><td>3 months</td><td>91.37%</td></tr>
    <tr><td>6 months</td><td>88.48%</td></tr>
    <tr><td>12 months</td><td>84.32%</td></tr>
    <tr><td>24 months</td><td>78.87%</td></tr>
    <tr><td>36 months</td><td>74.85%</td></tr>
    <tr><td>48 months</td><td>70.88%</td></tr>
    <tr><td>60 months</td><td>66.44%</td></tr>
    <tr><td>72 months</td><td>59.28%</td></tr>
  </tbody>
</table>

<h3>Graph 3: Kaplan–Meier Retention Estimates</h3>

<div>
  <svg viewBox="0 0 680 350" width="100%" xmlns="http://www.w3.org/2000/svg">
    <text x="340" y="24" text-anchor="middle" font-size="18" font-weight="bold" fill="currentColor">Estimated Customer Retention Over Time</text>
    <g stroke="#999">
      <line x1="80" y1="280" x2="630" y2="280"/>
      <line x1="80" y1="55" x2="80" y2="280"/>
      <line x1="80" y1="55" x2="630" y2="55" stroke-dasharray="4"/>
      <line x1="80" y1="167" x2="630" y2="167" stroke-dasharray="4"/>
    </g>
    <g fill="currentColor" font-size="12" text-anchor="end">
      <text x="70" y="284">0%</text>
      <text x="70" y="171">50%</text>
      <text x="70" y="59">100%</text>
    </g>
    <polyline points="100,74 170,80 240,90 310,103 380,112 450,121 520,131 600,147" fill="none" stroke="#3977b8" stroke-width="3"/>
    <g fill="#3977b8">
      <circle cx="100" cy="74" r="4"/><circle cx="170" cy="80" r="4"/>
      <circle cx="240" cy="90" r="4"/><circle cx="310" cy="103" r="4"/>
      <circle cx="380" cy="112" r="4"/><circle cx="450" cy="121" r="4"/>
      <circle cx="520" cy="131" r="4"/><circle cx="600" cy="147" r="4"/>
    </g>
    <g fill="currentColor" font-size="12" text-anchor="middle">
      <text x="100" y="302">3</text><text x="170" y="302">6</text>
      <text x="240" y="302">12</text><text x="310" y="302">24</text>
      <text x="380" y="302">36</text><text x="450" y="302">48</text>
      <text x="520" y="302">60</text><text x="600" y="302">72</text>
      <text x="350" y="333">Customer tenure (months)</text>
    </g>
  </svg>
</div>

<h3>7.2 Contract-Specific Retention</h3>

<table>
  <thead><tr><th>Contract Type</th><th>12-Month Survival Probability</th></tr></thead>
  <tbody>
    <tr><td>Month-to-month</td><td>70.31%</td></tr>
    <tr><td>One-year</td><td>99.08%</td></tr>
  </tbody>
</table>

<p><strong>Business Interpretation:</strong> Contract structure is associated not only with overall churn rates but also with the timing of customer churn. This makes contract-specific lifecycle monitoring useful when designing retention strategies.</p>

<hr>




<h2>8. Predictive Modeling: Customer Churn Risk</h2>

<h3>8.1 Models Evaluated</h3>

<h4>Logistic Regression</h4>
<p>Used as an interpretable baseline classification model. The model estimates the probability of churn using a logistic function.</p>

<h4>Random Forest</h4>
<p>An ensemble learning model based on multiple decision trees. Random Forest can capture nonlinear relationships and interactions between customer attributes.</p>

<h4>XGBoost</h4>
<p>A gradient-boosted decision-tree algorithm that builds an ensemble sequentially, with each boosting iteration attempting to improve the errors of the previous ensemble.</p>

<h3>8.2 Modeling Workflow</h3>

<p>The modeling workflow was designed to ensure reliable evaluation and prevent information leakage between training and testing data.</p>

<ul>
    <li>Extracted customer-level features from the SQLite database using SQL joins.</li>
    <li>Verified 7,043 customer records and unique customer IDs.</li>
    <li>Applied one-hot encoding to categorical variables.</li>
    <li>Prepared numerical features, including tenure, monthly charges, and total charges.</li>
    <li>Divided the dataset into training (60%), validation (20%), and testing (20%) subsets using stratified sampling.</li>
    <li>Applied class-weight adjustments to account for class imbalance.</li>
    <li>Trained Logistic Regression, Random Forest, and XGBoost models.</li>
    <li>Compared model performance using validation ROC-AUC.</li>
    <li>Selected the best-performing model and optimized its classification threshold using validation data.</li>
    <li>Evaluated final model performance on the independent test dataset.</li>
    <li>Applied SHAP to interpret the selected model's predictions.</li>
</ul>

<h3>8.3 Model Performance Comparison</h3>

<h3>8.3 Model Performance Comparison</h3>

<p>
    Three classification algorithms were evaluated to identify the most
    suitable model for predicting customer churn: Logistic Regression,
    Random Forest, and XGBoost.
</p>

<table>
    <thead>
        <tr>
            <th>Model</th>
            <th>Validation ROC-AUC</th>
            <th>Selection Status</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>Logistic Regression</td>
            <td>0.8364</td>
            <td>Evaluated</td>
        </tr>
        <tr>
            <td>Random Forest</td>
            <td>0.8386</td>
            <td>Evaluated</td>
        </tr>
        <tr>
            <td>XGBoost</td>
            <td>0.8387</td>
            <td><strong>Selected</strong></td>
        </tr>
    </tbody>
</table>

<div class="model-highlight">
    <h4>Selected Model: Random Forest</h4>
    <p>
        Random Forest was selected based on its validation performance.
        It was then evaluated on an independent test dataset to assess
        its ability to identify customers at risk of churn.
    </p>
</div>

<h3>8.4 Classification Threshold Optimization</h3>

<p>Instead of relying on the default 0.50 classification threshold, threshold selection was performed using validation data. The objective was to achieve approximately 80% recall for the churn class, reducing the number of customers who churn but are not identified by the model.</p>

<p>A threshold of 0.4799 was selected, producing validation precision of 48.62% and recall of 80.21%.</p>

<p>On the independent test dataset, the model achieved 50.66% precision and 81.55% recall for the churn class, with an overall accuracy of 74%.</p>

<p>The confusion matrix showed that the model correctly identified 305 of the 374 actual churners, while 69 churners were incorrectly classified as retained. It also identified 305 retained customers as potential churners.</p>

<h3>8.5 Model Interpretability Using SHAP</h3>

<p>SHAP (Shapley Additive exPlanations) was used to examine the contribution of individual features to the selected XGBoost model's predictions.</p>

<p>The five most influential features based on mean absolute SHAP values were:</p>

<ul>
    <li>Two-year contract: 0.6564</li>
    <li>Tenure: 0.4615</li>
    <li>One-year contract: 0.3016</li>
    <li>Fiber-optic internet: 0.2706</li>
    <li>Monthly charges: 0.2694</li>
</ul>

<p>Contract characteristics and customer tenure were among the most influential features in the model's predictions. Internet service type and monthly charges also contributed to churn-risk assessments. Mean absolute SHAP values indicate the magnitude of feature contributions, not their direction or causation.</p>

<h3>8.6 Customer-Level Risk Scoring</h3>

<p>The selected model generated individual churn probabilities for all 1,409 customers in the test dataset. Based on these probabilities, customers were divided into three risk categories:</p>

<ul>
    <li>Low Risk (0–0.35): 675 customers</li>
    <li>Medium Risk (above 0.35–0.65): 332 customers</li>
    <li>High Risk (above 0.65–1.00): 402 customers</li>
</ul>

<p>These customer-level probability scores were exported for subsequent financial exposure analysis and retention prioritization.</p>


<h2>9. Financial Risk Analytics: Probability-Weighted Revenue Exposure</h2>

<p>The objective of this stage was to move beyond predicting whether a customer might churn and estimate the recurring revenue associated with that risk.</p>

<p>A probability-weighted exposure metric, referred to as Probabilistic Capital at Risk (pCaR), was developed to quantify customer-level and portfolio-level revenue exposure.</p>

<h3>9.1 Customer-Level Exposure</h3>

<p>For each customer, probability-weighted monthly revenue exposure was calculated by multiplying the predicted probability of churn by the customer's monthly recurring charges.</p>

<p><strong>pCaR = P(Churn) × Monthly Charges</strong></p>

<h3>9.2 Aggregate Monthly Exposure</h3>

<p>Individual customer exposure values were aggregated to estimate the total monthly probability-weighted revenue exposure across the test portfolio.</p>

<p><strong>Monthly pCaR = Sum of Individual Customer pCaR Values</strong></p>

<h3>9.3 Annualized Revenue Exposure</h3>

<p>The monthly exposure was annualized by multiplying it by twelve to estimate the annual recurring revenue associated with predicted churn risk.</p>

<p><strong>Annualized pCaR = Monthly pCaR × 12</strong></p>

<h3>9.4 Financial Exposure Results</h3>

<p>The financial risk analysis was performed on the 1,409 customers in the independent test dataset.</p>

<ul>
    <li>Total Monthly Recurring Revenue: $90,301.20</li>
    <li>Annualized Recurring Revenue: $1,083,614.40</li>
    <li>Monthly Probability-Weighted Exposure: $41,423.51</li>
    <li>Annualized Probability-Weighted Exposure: $497,080.46</li>
    <li>Exposure as a Percentage of Monthly Recurring Revenue: 45.87%</li>
</ul>

<h3>9.5 Business Interpretation</h3>

<p>The test portfolio generated $90,301.20 in monthly recurring charges. After weighting each customer's monthly charges by their predicted probability of churn, the estimated monthly exposure was $41,409.51.</p>

<p>Annualized, this represents approximately $497,080.46 in probability-weighted recurring revenue exposure. The exposure-to-MRR ratio of 45.87% indicates that the estimated exposure is equivalent to 45.87% of the test portfolio's monthly recurring charges.</p>

<p>This figure should not be interpreted as guaranteed revenue loss. It is a probability-weighted estimate based on model predictions and assumes that current monthly charges persist over a twelve-month period.</p>


<h2>10. High-Risk, High-Value Customer Segmentation</h2>

<p>Customer prioritization was based on two dimensions: predicted probability of churn and monthly recurring revenue contribution. The objective was to identify customers who combine elevated churn risk with relatively high financial contribution.</p>

<h3>10.1 Target Segment Definition</h3>

<p>Customers were classified as high-risk, high-value when they met both of the following conditions:</p>

<ul>
    <li>Predicted churn probability greater than or equal to 0.60.</li>
    <li>Monthly charges greater than or equal to the test-set median of $69.95.</li>
</ul>

<p>This approach identifies customers who represent both elevated churn risk and relatively high recurring revenue contribution.</p>

<h3>10.2 Segmentation Results</h3>

<p>The segmentation analysis identified 359 customers meeting both criteria, representing 25.48% of the test population.</p>

<p>The target segment accounted for $288,132.93 in annualized probability-weighted revenue exposure, equivalent to 57.95% of the total estimated exposure.</p>

<h3>10.3 Business Interpretation</h3>

<p>Approximately one-quarter of the test population accounts for nearly 57.97% of the estimated annualized revenue exposure.</p>

<p>This demonstrates why prioritizing customers using both churn probability and financial contribution can be more commercially useful than ranking customers by churn probability alone.</p>

<p>The identified segment provides a focused group for evaluating targeted retention interventions and allocating retention resources more efficiently.</p>

<p>The risk-tier classification in Section 8 and this high-risk, high-value segment serve different purposes. Risk tiers group customers by probability intervals, whereas the target segment combines churn probability with revenue contribution.</p>


<h2>11. Retention Strategy &amp; Financial Scenario Analysis</h2>

<p>The final analytical stage translated the customer risk assessment into a hypothetical retention intervention. A targeted retention campaign was modeled for the 359 customers identified in the high-risk, high-value segment.</p>

<p>The objective was to evaluate whether the potential financial benefit of reducing churn could justify the cost of customer retention incentives.</p>

<h3>11.1 Campaign Assumptions</h3>

<p>The proposed retention campaign included a $10 monthly discount and a $5 monthly technical support subsidy, resulting in a total incentive of $15 per customer per month.</p>

<p>For 359 targeted customers, the estimated annual campaign expenditure was $64,620.</p>

<p>The scenario assumed a 35% relative reduction in churn probability for each targeted customer. For example, a customer with a baseline churn probability of 60% would have an assumed post-intervention probability of 39%.</p>

<p><strong>Post-Intervention Churn Probability = Baseline Churn Probability × 0.65</strong></p>

<h3>11.2 Financial Scenario Results</h3>

<p>Under the assumed intervention, the estimated preserved annualized revenue was $100,846.53, compared with a total campaign cost of $64,620.</p>

<p>The resulting net financial gain was estimated at $36,226.53.</p>

<h3>11.3 Benefit-to-Cost Ratio</h3>

<p>The benefit-to-cost ratio was calculated by dividing estimated preserved revenue by total campaign expenditure.</p>

<p><strong>Benefit-to-Cost Ratio = Preserved Revenue / Campaign Cost</strong></p>

<p>The resulting ratio was 1.56x, indicating an estimated $1.56 in preserved revenue for every $1 spent on retention incentives.</p>

<h3>11.4 Return on Investment (ROI)</h3>

<p>Net ROI was calculated by subtracting campaign expenditure from estimated preserved revenue and dividing the result by campaign expenditure.</p>

<p><strong>ROI = (Preserved Revenue − Campaign Cost) / Campaign Cost × 100</strong></p>

<p>The modeled campaign produced an estimated net ROI of 56.06%, with a net financial gain of $36,226.53.</p>

<h3>11.5 Business Interpretation and Limitations</h3>

<p>Under the assumed 35% relative reduction in churn probability, the modeled campaign generates an estimated $100,791.35 in preserved annualized revenue against a campaign expenditure of $64,620.</p>

<p>These results represent a hypothetical financial scenario rather than an observed campaign outcome. The analysis assumes that all targeted customers receive the full annual incentive and that the modeled churn reduction is achieved uniformly.</p>

<p>The estimates also use recurring revenue rather than contribution margin and do not account for customer-specific churn timing, campaign uptake, or partial-year retention.</p>

<p>Actual campaign effectiveness would need to be evaluated through controlled experimentation, such as a randomized retention campaign, before the strategy could be considered validated for operational implementation.</p>