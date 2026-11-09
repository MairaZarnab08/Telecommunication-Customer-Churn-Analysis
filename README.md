<h1>Enterprise Revenue Protection & Predictive Churn Analytics Suite</h1>
<p><b>End-to-End Data Engineering, Machine Learning Scoring, and Executive Tableau Command Center</b></p>

<hr>

<h2>Executive Overview</h2>
<p>Customer churn represents a direct threat to recurring revenue in subscription-based telecommunications. While traditional business intelligence focuses on measuring churn after cancellation, this project takes a forward-looking approach by identifying revenue exposure before customers leave.</p>
<p>Using the IBM Telco Customer Churn dataset, I developed an end-to-end analytics solution integrating SQL-based data engineering, Python-based predictive modeling, financial risk quantification, and Tableau visualization. The objective was to translate customer-level churn predictions into actionable financial intelligence through a custom metric: <b>Predicted Churn at Risk (pCaR)</b>.</p>

<hr>

<h2>Business Objectives</h2>
<ul>
  <li><b>Quantify Revenue Exposure:</b> Estimate recurring revenue associated with customers exhibiting elevated churn probabilities.</li>
  <li><b>Identify Churn Drivers:</b> Evaluate the relationship between customer tenure, service configurations, contract structures, and payment methods.</li>
  <li><b>Measure Financial Risk:</b> Translate predictive model outputs into a dollar-denominated estimate of revenue exposure.</li>
  <li><b>Prioritize Retention Efforts:</b> Develop a risk-based customer prioritization framework to support targeted retention strategies.</li>
</ul>

<hr>

<h2>Core Analytics Questions</h2>
<ol>
  <li>How much recurring revenue is potentially exposed to customer churn across the subscriber base?</li>
  <li>Which product and service combinations (e.g., Fiber Optic tiers without Tech Support) exhibit structural churn vulnerability?</li>
  <li>How do contract types and payment methods relate to monthly recurring revenue (MRR) loss?</li>
  <li>At what specific stage of the customer lifecycle is churn hazard highest?</li>
  <li>How can retention teams prioritize daily outreach using both churn probability and dollar exposure?</li>
</ol>

<hr>

<h2>Technology Stack & Methods Employed</h2>

<table>
  <thead>
    <tr>
      <th width="20%">Technology</th>
      <th width="25%">Layer</th>
      <th width="55%">Methods & Analytical Techniques</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><b>SQL Server</b></td>
      <td>Data Engineering</td>
      <td>Multi-stage Common Table Expressions (CTEs), null handling (<code>ISNULL</code>, <code>NULLIF</code>), type casting (<code>CAST</code>), window functions (<code>AVG OVER PARTITION</code>, <code>DENSE_RANK</code>), conditional logic (<code>CASE WHEN</code>).</td>
    </tr>
    <tr>
      <td><b>Python</b></td>
      <td>Quantitative Analytics</td>
      <td>Vectorized data processing (<code>Pandas</code>), conditional risk tiering (<code>NumPy</code>), probabilistic classification scoring (<code>Scikit-Learn</code>), financial array calculations.</td>
    </tr>
    <tr>
      <td><b>Tableau Desktop</b></td>
      <td>Business Intelligence</td>
      <td>Interactive multi-tier command center, parameter-driven filtering, cohort area charts, friction matrix heatmaps, priority intervention ledger.</td>
    </tr>
  </tbody>
</table>

<hr>

<h2>End-to-End Analytics Workflow</h2>

<h3>Step 1: Data Architecture & SQL Staging Pipeline</h3>
<p>Designed a modular, multi-stage Common Table Expression (CTE) pipeline in SQL Server to stage, clean, and enrich raw subscriber records without altering underlying source tables:</p>
<ul>
  <li><b>Data Hygiene & Null Imputation:</b> Resolved whitespace anomalies in billing fields, imputing zero-dollar charges for zero-tenure onboarding accounts using <code>NULLIF</code> and <code>ISNULL</code>.</li>
  <li><b>Lifecycle Cohort Engineering:</b> Categorized account tenure into discrete risk bands (<code>0–12 Months</code>, <code>13–24 Months</code>, <code>25–48 Months</code>, and <code>49+ Months</code>).</li>
  <li><b>Service Vulnerability Indicators:</b> Flagged high-risk product configurations, specifically identifying accounts with Fiber Optic service lacking technical support.</li>
  <li><b>Windowed Spending Benchmarks:</b> Established cohort-level spending baselines using partitioned averages (<code>AVG() OVER (PARTITION BY)</code>) and ranked high-value accounts within segments.</li>
</ul>

<h4>Key SQL Implementation Snippet</h4>
<pre><code>-- Multi-Stage CTE: Staging, Null Imputation, and Service Risk Feature Engineering
WITH Cleaned_Base AS (
    SELECT 
        customerID,
        tenure,
        Contract,
        PaymentMethod,
        InternetService,
        TechSupport,
        MonthlyCharges,
        CAST(ISNULL(NULLIF(RTRIM(TotalCharges), ''), '0') AS DECIMAL(10,2)) AS TotalCharges_Cleaned
    FROM dbo.Telco_Churn_Raw
),
Enriched_Metrics AS (
    SELECT *,
        CASE 
            WHEN InternetService = 'Fiber Optic' AND TechSupport = 'No' THEN 1 
            ELSE 0 
        END AS Is_Vulnerable_Fiber_Account,
        AVG(MonthlyCharges) OVER(PARTITION BY Contract) AS Avg_Contract_Monthly_Charge
    FROM Cleaned_Base
)
SELECT * FROM Enriched_Metrics;</code></pre>

<h3>Step 2: Predictive Scoring & Risk Vectorization</h3>
<p>Exported the staged dataset into Python to run model inference and engineer financial risk vectors:</p>
<ul>
  <li><b>Probabilistic Model Scoring:</b> Generated continuous churn risk probabilities ($P\text{-Churn}$ from <code>0.00</code> to <code>1.00</code>) per active account using <code>predict_proba()</code>.</li>
  <li><b>Vectorized Financial Exposure:</b> Applied vectorized array calculations to evaluate dollar-denominated financial risk:
    <br><code>Annualized ARR = Monthly Charges × 12</code>
    <br><code>pCaR Exposure = Annualized ARR × P-Churn</code>
  </li>
  <li><b>Risk Stratification:</b> Bucketized account records into dynamic operational risk tiers using <code>np.select()</code>:
    <ul>
      <li><b>High Risk:</b> $P\text{-Churn} \ge 0.60$</li>
      <li><b>Medium Risk:</b> $0.30 \le P\text{-Churn} < 0.60$</li>
      <li><b>Low Risk:</b> $P\text{-Churn} < 0.30$</li>
    </ul>
  </li>
</ul>

<h4>Key Python Vectorization Snippet</h4>
<pre><code>import numpy as np
import pandas as pd

# Vectorized Financial Risk Calculation (pCaR)
df['Annual_ARR'] = df['MonthlyCharges'] * 12
df['pCaR_Exposure'] = df['Annual_ARR'] * df['Churn_Probability']

# Operational Risk Stratification
conditions = [
    (df['Churn_Probability'] >= 0.60),
    (df['Churn_Probability'] >= 0.30) & (df['Churn_Probability'] < 0.60),
    (df['Churn_Probability'] < 0.30)
]
choices = ['High Risk', 'Medium Risk', 'Low Risk']
df['Risk_Tier'] = np.select(conditions, choices, default='Low Risk')</code></pre>

<h3>Step 3: Financial Risk Quantification (pCaR Metric)</h3>
<p>To connect machine learning outputs directly with top-line financial planning, I established the <b>Predicted Churn at Risk (pCaR)</b> framework:</p>

<blockquote style="border-left: 4px solid #002C6C; padding-left: 10px; margin: 15px 0;">
  <b>Customer pCaR = Churn Probability × Annualized Recurring Revenue (ARR)</b>
</blockquote>

<p>Aggregating customer-level pCaR provides a revenue-weighted view of churn exposure, ensuring that retention budgets are allocated based on monetary value rather than raw account counts.</p>

<h3>Step 4: Executive Tableau Command Center Layout</h3>
<p>Structured the analytics output into a three-tier dashboard suite matching distinct organizational workflows:</p>
<ul>
  <li><b>Tier 1: Executive Portfolio Overview (Macro View)</b><br>
  Designed for executive leadership. Features a 4-card KPI summary banner (<b>$501.00K pCaR Exposure</b>, <b>370 High-Risk Accounts</b>, <b>26.54% Churn Rate</b>, and <b>$1.08M ARR</b>), tenure decay curves, and payment friction revenue loss charts.</li>
  <li><b>Tier 2: Product Vulnerability & Service Friction (Diagnostic View)</b><br>
  Designed for product managers. Displays service add-on vulnerability matrices, monthly charge scatter plots, and contract-by-payment friction heatmaps.</li>
  <li><b>Tier 3: Proactive Retention Action Ledger (Operational View)</b><br>
  Designed for frontline retention leads. Combines risk tier breakdowns with a priority table sorted by pCaR exposure, enabling agents to execute revenue-weighted outreach.</li>
</ul>

<hr>

<h2>Key Analytical Findings</h2>
<ul>
  <li><b>Quantified Portfolio Exposure:</b> Identified <b>$501.00K in Annualized pCaR Exposure</b> concentrated across <b>370 high-risk accounts</b>.</li>
  <li><b>Early Lifecycle Vulnerability:</b> Churn risk peaks within the <b>0–12 month onboarding window</b>, indicating the need for structured early customer success interventions.</li>
  <li><b>Billing & Service Friction:</b> Electronic Check represents the largest payment-related churn driver, while Fiber Optic plans lacking Tech Support exhibit an elevated <b>~49.78% churn rate</b>.</li>
  <li><b>Operationalized Retention:</b> Shifted outreach strategy from unprioritized lists to a revenue-weighted daily action queue.</li>
</ul>

<hr>

<h2>Technical Challenges & Analytical Solutions</h2>

<table>
  <thead>
    <tr>
      <th width="25%">Challenge</th>
      <th width="35%">Root Cause</th>
      <th width="40%">Analytical Approach</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><b>Inconsistent Billing Data</b></td>
      <td>Blank string values in total charge fields for new accounts.</td>
      <td>Applied SQL <code>ISNULL()</code> and <code>NULLIF()</code> logic to standardize billing records dynamically.</td>
    </tr>
    <tr>
      <td><b>Probability Interpretation</b></td>
      <td>Abstract model probability scores were disconnected from revenue impact.</td>
      <td>Developed the dollar-denominated <b>pCaR</b> metric to connect risk likelihood directly to ARR exposure.</td>
    </tr>
    <tr>
      <td><b>Outreach Prioritization</b></td>
      <td>Retention agents treated all churning accounts with equal urgency.</td>
      <td>Created a revenue-weighted <b>Priority Action Ledger</b> sorted by calculated financial exposure.</td>
    </tr>
  </tbody>
</table>

<hr>

<h2>Project Deliverables & Links</h2>
<ul>
  <li><b>Interactive Dashboard:</b> <a href="#">View Tableau Executive Command Center &rarr;</a></li>
  <li><b>Predictive Pipeline Notebook:</b> <a href="notebooks/churn_prediction_analysis.ipynb">View Python Notebook &rarr;</a></li>
  <li><b>Database Architecture:</b> <a href="#">View SQL Staging Scripts &rarr;</a></li>
</ul>

<hr>

<h2>References & Acknowledgements</h2>
<ul>
  <li><b>Dataset:</b> IBM Telco Customer Churn | Source: Kaggle</li>
  <li><b>Methodology & Framework:</b> End-to-end data engineering, vectorized financial risk modeling, and executive dashboard design developed by author.</li>
</ul>

<p><i>Note: pCaR represents estimated revenue exposure based on model probabilities and annualized recurring revenue. It serves as an analytical risk assessment metric rather than a guarantee of actual revenue loss.</i></p>
