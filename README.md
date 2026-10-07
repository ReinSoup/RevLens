# RevLens | Explainable SaaS Customer Risk Intelligence

An academic analytics and decision-support project for SaaS businesses. RevLens connects customer behavior, subscriptions, revenue, churn risk, explainable machine learning, customer value, and revenue exposure to answer a practical question:

> Which customers are most likely to churn, what observable factors are associated with that prediction, how much revenue is exposed, and which customers should receive the greatest business attention?

> Status: Planned / under development  
> Scope: Two-semester academic project

---

## Abstract

SaaS businesses generate connected data across customers, subscriptions, product activity, revenue, acquisition, retention, and customer economics. Individual metrics such as MRR, churn rate, engagement, and customer value are useful, but they do not by themselves answer the customer-level decision question: which potential churn events matter most to the business, and what observable evidence supports the risk prediction?

RevLens is designed as an end-to-end customer-risk intelligence and decision-support system. It will ingest and validate SaaS customer, subscription, usage, and revenue data; engineer customer-level behavioral and economic features; predict customer churn risk; explain individual predictions using SHAP; translate model evidence into traceable human-readable explanations; quantify revenue exposure; and prioritize customers using risk, value, and financial context.

The project does not claim to invent a new machine-learning algorithm or determine the true psychological cause of churn. Its central contribution is an integrated and explainable analytical workflow that connects prediction with observable evidence and business impact.

Quantitative results will be reported only after implementation and evaluation.

---

## 1. Project Definition

RevLens is not simply a dashboard containing SaaS metrics and several machine-learning models.

The central system is:

```text
SaaS Customer Data
        ↓
Customer-Level Features
        ↓
Churn-Risk Prediction
        ↓
Explainable ML
        ↓
Observable Risk Factors
        ↓
Revenue Exposure
        ↓
Customer Value
        ↓
Business Priority
        ↓
Decision-Support Insight
```

The Streamlit application is the interface through which these outputs are explored.

### One-sentence definition

> RevLens is an explainable SaaS customer-risk intelligence system that predicts churn, identifies observable factors contributing to each prediction, quantifies revenue exposure, and prioritizes customers based on business importance.

---

## 2. Problem Statement

SaaS companies collect information from multiple operational areas:

- Customer accounts
- Subscriptions
- Product usage
- Revenue and transactions
- Acquisition
- Retention
- Customer interactions
- Customer economics

These areas are often analyzed for different operational purposes. The problem is not that separate analysis is incorrect.

The problem is that a cross-functional business question requires these outputs to be connected:

> Why is revenue at risk, which customers are contributing to that risk, what observable behavior is associated with their predicted churn, and which customers matter most financially?

A churn probability alone does not answer that question.

For example:

```text
Customer A
90% churn probability
$50 MRR

Customer B
75% churn probability
$8,000 MRR
```

Customer A has the higher predicted risk, but Customer B may represent substantially greater financial exposure.

RevLens therefore separates:

```text
Churn Risk
≠
Customer Value
≠
Revenue Exposure
≠
Business Priority
```

and then connects them at the decision-support stage.

---

## 3. Project Gap and Contribution

Existing SaaS analytics and customer-success systems already provide capabilities such as:

- Revenue reporting
- Churn analysis
- Retention analysis
- Customer segmentation
- Forecasting
- Customer-risk analysis

RevLens does not claim that these individual capabilities are novel.

The project focuses on the integration of these outputs into a traceable customer-risk workflow.

The intended contribution is:

```text
Prediction
    ↓
Explanation
    ↓
Customer Value Context
    ↓
Revenue Exposure
    ↓
Business Priority
```

The project will investigate whether this enriched output provides more useful business context than presenting a standalone churn probability.

This makes RevLens an integrated analytical and decision-support framework rather than a collection of unrelated models.

---

## 4. Research Question

The central research question is:

> Can observable customer behavior be used to predict churn risk, explain the model's predictions, and connect those predictions to customer value and revenue exposure for business prioritization?

The project will evaluate:

1. Predictive performance
2. Explainability of individual predictions
3. Strength of observable evidence
4. Accuracy and traceability of revenue-exposure calculations
5. Customer prioritization
6. Whether enriched decision-support output provides more useful context than a standalone risk score

---

## 5. Input, Processing, and Output

### 5.1 Input

The predictive customer-risk component requires data that supports customer-level temporal analysis.

Required characteristics include:

- Customer identifier
- Timestamps
- Subscription status or observable churn event
- Historical customer activity
- Revenue or subscription value
- Sufficient observations to construct behavioral features
- Enough history to define a prediction window without leakage

Planned data domains:

| Domain | Purpose |
|---|---|
| Customers | Customer identity, cohorts, profiles |
| Subscriptions | Plan, state, tenure |
| Revenue / Transactions | MRR, revenue movement, customer value |
| Product Activity | Engagement and behavioral features |
| Acquisition | Channel and acquisition analysis |
| Business Expenses | Unit economics where supported |

The final dataset must be selected before the predictive pipeline is implemented.

The project will not force an unsuitable dataset into the problem.

### 5.2 Processing

```text
Raw SaaS Data
      ↓
Data Ingestion
      ↓
Validation
      ↓
Cleaning & Standardization
      ↓
Integrated Data Model
      ↓
Customer-Level Feature Engineering
      ↓
Business Analytics
      ↓
Churn Model
      ↓
SHAP Explainability
      ↓
Human-Readable Interpretation
      ↓
Revenue Exposure
      ↓
Customer Prioritization
      ↓
Streamlit Application
```

### 5.3 Primary Output

The primary output is an explainable customer-risk profile.

Example:

```text
CUSTOMER RISK PROFILE

Customer: C1042
Plan: Enterprise
MRR: $8,000
Tenure: 18 months

Predicted churn probability:
87% HIGH

Top contributing factors:
1. Product usage declined 31%
2. 12 days since last activity
3. Session frequency declined 24%
4. Feature engagement declined

Human-readable explanation:
"Churn risk is primarily associated with declining
product usage, increased inactivity, and reduced
session frequency."

Evidence quality:
HIGH

Revenue exposure:
$8,000 MRR

Customer value:
HIGH

Business priority:
CRITICAL
```

All values shown above are illustrative. Actual values will come from the implemented dataset and model.

---

## 6. Core Analytical Workflow

The core RevLens workflow is:

```text
Customer
    ↓
Subscription
    ↓
Usage / Activity
    ↓
Customer Behavior
    ↓
Churn Prediction
    ↓
SHAP
    ↓
Feature Contributions
    ↓
Human Interpretation
    ↓
Revenue Exposure
    ↓
Customer Value
    ↓
Business Priority
```

This is the primary technical direction of the project.

Supporting analytics provide the business context required to interpret the customer-risk output.

---

## 7. Business Intelligence Layer

The BI layer establishes the business context before and alongside machine learning.

### Revenue Intelligence

Where supported by the dataset:

- Monthly Recurring Revenue (MRR)
- Annual Recurring Revenue (ARR)
- New revenue
- Expansion revenue
- Contraction revenue
- Churned revenue
- Revenue growth
- Revenue by plan
- Revenue by segment
- Revenue by acquisition channel

The objective is not only to display revenue trends, but to identify where changes occurred and connect them to customer and behavioral context.

### Acquisition and Retention

Potential analysis includes:

- Customers acquired by channel
- CAC
- Conversion
- Cohort retention
- Customer lifetime
- Acquisition-to-revenue efficiency

### Churn Intelligence

Potential analysis includes:

- Churn rate
- Churn by plan
- Churn by cohort
- Churn by acquisition channel
- Churn by segment
- Revenue lost through churn
- Predicted churn risk
- Revenue exposure

### Customer Intelligence

Customer-level behavioral features will be derived from available usage, subscription, revenue, and interaction data.

These features support:

- Customer segmentation
- Behavioral analysis
- Churn prediction
- Explainability
- Customer prioritization

### Unit Economics

Where the dataset supports the calculations:

- CAC
- LTV
- ARPU
- Gross margin
- Contribution margin
- LTV:CAC
- Customer payback period
- Revenue per customer

Not every metric will be forced into the project if the selected dataset cannot support it reliably.

---

## 8. Customer Segmentation

Customer segmentation is a supporting analytical component.

The initial approach will investigate clustering using behavioral and economic features.

```text
Customer Data
      ↓
Behavioral Features
      ↓
Feature Preparation
      ↓
Clustering
      ↓
Cluster Evaluation
      ↓
Cluster Interpretation
```

K-Means may be used as an initial method.

The purpose is not simply to produce clusters. The resulting groups must be interpretable and useful for understanding customer behavior and business value.

Segmentation will remain secondary to the explainable customer-risk workflow.

---

## 9. Explainable Churn Prediction

### 9.1 What the model predicts

The churn model answers:

> Based on information available before the prediction point, how likely is this customer to churn within the defined prediction window?

Example:

```text
Customer C1042

Predicted churn probability:
87%

Risk category:
HIGH
```

The target definition and prediction window must be explicitly defined.

### 9.2 Data leakage prevention

Information that occurs after the prediction point must not be used to generate features for that prediction.

For example, cancellation-related information that only becomes available after cancellation cannot be used to predict that cancellation.

Temporal feature construction and validation will therefore be a core part of the modelling process.

---

## 10. Explainable Machine Learning

Explainable ML is the primary technical focus of RevLens.

The core architecture is:

```text
Customer Behavior
      ↓
Feature Engineering
      ↓
Churn Model
      ↓
Churn Probability
      ↓
SHAP
      ↓
Feature Contributions
      ↓
Human-Readable Interpretation
```

The project distinguishes three different questions:

### Prediction

> How likely is the customer to churn?

### Model explanation

> Which observed features contributed to the model's prediction?

### Causal explanation

> What actually caused the customer to cancel?

RevLens primarily addresses the first two.

It does not claim to automatically determine the third.

---

## 11. SHAP-Based Explanation

SHAP will be investigated as the primary model-explainability method.

For an individual customer, SHAP can identify how features contributed to the model's prediction.

Illustrative example:

```text
Predicted churn probability = 82%

Feature contribution:

Listening time change       +0.32
Days since last active      +0.24
Sessions per week           +0.18
Playlist interaction        +0.12
Saved songs                 -0.08
Account tenure              -0.06
```

These values are illustrative only.

Actual SHAP values will be calculated from the trained model.

A positive contribution indicates that the feature pushes the model toward a higher churn prediction, while a negative contribution pushes it toward a lower prediction. The exact interpretation depends on the model and SHAP explainer used.

### Local explanation

Answers:

> Why did the model assign this customer a high risk?

This is the most important explanation for the customer-risk page.

### Global explanation

Answers:

> Which features generally influence churn predictions across the customer population?

Global SHAP analysis can help assess overall model behavior and feature influence.

---

## 12. SHAP Does Not Prove Causation

This distinction is mandatory throughout the project.

If SHAP shows:

```text
Usage decline
        ↓
Strong positive contribution
        ↓
Higher predicted churn
```

the correct interpretation is:

> Declining usage contributed strongly to the model's prediction.

The project must not state:

> Declining usage caused the customer to churn.

Unobserved factors may have influenced the actual customer decision.

Preferred terminology:

- Contributing factor
- Associated with the prediction
- Model-attributed factor
- Observable risk signal
- Predictive driver

Avoid causal language unless a separate causal methodology is implemented.

---

## 13. Human-Readable Explanation Layer

SHAP produces technical feature contributions. RevLens will translate the strongest supported contributions into a human-readable explanation.

An NLP model or LLM is not required for this.

The preferred architecture is deterministic Python logic:

```text
Churn Model
      ↓
SHAP
      ↓
Top Contributing Features
      ↓
Actual Customer Feature Values
      ↓
Feature-to-Text Mapping
      ↓
Human-Readable Explanation
```

Example:

```python
explanation_text = {
    "listening_time_change": "declining listening activity",
    "days_since_last_active": "increased inactivity",
    "sessions_change": "reduced session frequency",
    "playlist_interaction": "lower playlist engagement"
}
```

The application can then construct a sentence from the strongest supported contributors.

Example:

> Churn risk is primarily associated with declining listening activity, increased inactivity, and reduced session frequency.

Where appropriate, the explanation can include actual measured values:

> The prediction is primarily associated with a 38% decline in listening time, 16 days since last activity, and a 43% reduction in weekly sessions.

The values must come from the actual customer data.

### Why this approach?

The explanation layer should be:

- Transparent
- Deterministic
- Traceable
- Easy to test
- Directly tied to model evidence
- Resistant to unsupported explanations

An LLM will not be added simply to convert model output into sentences.

---

## 14. Evidence Quality

RevLens will investigate an Evidence Quality indicator to distinguish between:

```text
High predicted risk
+
Strong observable evidence
```

and:

```text
High predicted risk
+
Weak observable evidence
```

Example:

```text
Churn probability: 82%

Evidence quality: HIGH

Reason:
Multiple independent behavioral signals
show significant deterioration.
```

Another case:

```text
Churn probability: 82%

Evidence quality: LOW

Reason:
No significant observable behavioral
deterioration was detected.
```

The exact evidence-quality calculation will be designed and evaluated during implementation.

It must not be presented as a standardized industry metric.

The conceptual distinction is:

```text
Risk Probability
        ≠
Strength of Observable Evidence
```

---

## 15. Unexpected and Unexplained Churn

A major limitation of predictive analytics is that the available data may not contain the actual reason a customer leaves.

Consider a customer who:

- Uses the product consistently
- Has stable engagement
- Has no payment problems
- Has no recorded support issues
- Has long tenure

and then suddenly cancels for an unknown personal reason.

RevLens should not fabricate an explanation.

Instead:

```text
Predicted risk before cancellation:
LOW

Observed behavior:
STABLE

Actual outcome:
CUSTOMER CANCELLED

Interpretation:
UNEXPECTED / INSUFFICIENTLY EXPLAINED CHURN

Evidence quality:
LOW
```

This is an important system behavior rather than a failure to hide.

RevLens should explicitly represent uncertainty when the available data cannot explain an outcome.

---

## 16. Revenue Exposure

Prediction alone is not enough for business prioritization.

Consider:

```text
Customer A
90% churn probability
$50 MRR

Customer B
75% churn probability
$8,000 MRR
```

Customer A has greater predicted risk.

Customer B may represent greater financial exposure.

Therefore RevLens connects:

```text
Risk
+
Customer Value
+
Revenue Exposure
=
Business Priority
```

A simple conceptual calculation is:

```text
Expected revenue exposure
=
Predicted churn probability × relevant recurring revenue
```

However, the final implementation must explicitly define whether it uses:

- MRR
- Expected remaining recurring revenue
- LTV
- Another justified measure

A probability × MRR calculation must not be described as actual financial loss without clearly stating its assumptions.

---

## 17. Customer Value and Generalization

Customer value should not depend on fixed dollar thresholds.

For example, defining:

```text
>$5,000 MRR = High Value
```

would not generalize across companies.

Instead, RevLens should evaluate customer value relative to the company's own customer population.

Possible approaches include:

- Revenue percentile
- MRR percentile
- Revenue share of company MRR
- LTV percentile where supported
- Tenure and economic context

Illustrative relative classification:

```text
0–50th percentile      Low
50–80th percentile     Medium
80–95th percentile     High
95–100th percentile    Very High
```

The exact thresholds are implementation decisions and must be documented and justified.

This allows the same analytical framework to work across different SaaS scales without relying on arbitrary absolute dollar values.

---

## 18. Business Priority

RevLens should not rank customers solely by churn probability.

The decision-support layer considers:

- Churn probability
- Customer value
- Recurring revenue
- Revenue exposure
- Customer segment
- Behavioral evidence
- Evidence quality

Conceptually:

```text
Prediction
    ↓
Explainability
    ↓
Customer Value
    ↓
Revenue Exposure
    ↓
Evidence Quality
    ↓
Business Priority
```

The final prioritization method must be explicit and reproducible.

Risk, value, and priority should remain separate fields rather than being collapsed into one opaque score without justification.

---

## 19. Recommended Actions: Project Boundary

RevLens can identify a customer as high risk.

That does not automatically mean:

> Give the customer a 20% discount.

That recommendation would require evidence that the intervention is appropriate and effective.

Unless a separate causal or uplift framework is implemented, the application should use cautious language:

- Suggested investigation
- Consider re-engagement
- Review recent engagement decline
- Potential retention action

The system should not claim that a specific intervention will prevent churn.

---

## 20. Dashboard Structure

Streamlit is the presentation layer, not the core analytical engine.

The dashboard should prioritize information rather than display every available metric simultaneously.

### Executive Overview

```text
Revenue
Retention
Churn
Revenue Exposure
High-Priority Customers
Key Business Insights
```

### Customer Risk

Primary view:

```text
Customer
Plan
MRR
Tenure
Customer Value

Churn Probability
Risk Category

Top Contributing Factors
Evidence Quality

Revenue Exposure
Business Priority
```

Secondary investigation view:

- Activity trends
- Session trends
- Feature comparisons
- Recent activity timeline
- Local SHAP explanation
- Global SHAP summary
- Historical behavior

This keeps the primary view focused while preserving deeper analytical detail.

---

## 21. Decision-Support Layer

The decision-support layer is the central implementation of the project gap.

It connects model and business outputs:

```text
Metric / Model Output
        ↓
Change or Risk Identification
        ↓
Affected Customer / Segment
        ↓
Behavioral Context
        ↓
Model Explanation
        ↓
Financial Impact
        ↓
Business Priority
        ↓
Interpretable Insight
```

For example:

```text
High churn risk
      ↓
Usage declined
      ↓
Customer is high-value
      ↓
$8,000 MRR exposed
      ↓
Evidence quality = High
      ↓
Business priority = Critical
```

Every customer-risk insight should be traceable back to:

1. Customer data
2. Engineered feature
3. Model output
4. SHAP contribution
5. Actual customer value
6. Revenue calculation
7. Priority logic

---

## 22. Technology Stack

The project will use technologies that support a transparent and reproducible workflow.

| Technology | Purpose |
|---|---|
| Python | Data processing, feature engineering, analytics, modelling |
| Pandas | Data manipulation and transformation |
| NumPy | Numerical operations |
| Scikit-learn | Predictive modelling and clustering |
| SHAP | Model explainability |
| Matplotlib / Seaborn / Plotly | Analytical visualization where appropriate |
| Streamlit | Interactive application |
| Git / GitHub | Version control and documentation |

Additional libraries will be added only when justified by the implemented pipeline.

---

## 23. System Architecture

```text
                    SAAS BUSINESS DATA
                           ↓
                DATA INGESTION & QUALITY
                           ↓
                 INTEGRATED DATA MODEL
                           ↓
                  CUSTOMER FEATURES
                           ↓
              ┌────────────┴────────────┐
              ↓                         ↓
      BUSINESS ANALYTICS          CHURN MODEL
              ↓                         ↓
   Revenue / Retention /        Churn Probability
   Churn / Unit Economics              ↓
                                      SHAP
                                        ↓
                              Feature Contributions
                                        ↓
                              Human Interpretation
              │                         │
              └────────────┬────────────┘
                           ↓
                   CUSTOMER VALUE
                           ↓
                   REVENUE EXPOSURE
                           ↓
                  EVIDENCE QUALITY
                           ↓
                  BUSINESS PRIORITY
                           ↓
                DECISION-SUPPORT INSIGHTS
                           ↓
                    STREAMLIT APP
                           ↓
                       EVALUATION
```

---

## 24. Development Plan

### Phase 1: Scope and Research Definition

- Finalize research question
- Finalize input and output
- Finalize project boundaries
- Select evaluation criteria
- Select the dataset

### Phase 2: Data Foundation

- Acquire and document the selected dataset
- Inspect schemas and relationships
- Identify analytical grain
- Clean and standardize data
- Validate relationships
- Build the integrated data model

### Phase 3: Business Intelligence

- Establish baseline SaaS metrics
- Analyze revenue movement
- Analyze retention and churn
- Analyze customer value
- Establish business context for later modelling

### Phase 4: Customer Feature Engineering

- Build customer-level behavioral features
- Build subscription features
- Build revenue and value features
- Define temporal feature windows
- Prevent data leakage
- Document every feature

### Phase 5: Customer Segmentation

- Prepare behavioral and economic features
- Evaluate clustering
- Interpret customer groups
- Connect segments to business metrics

### Phase 6: Explainable Churn Modelling

- Define churn target
- Define prediction window
- Establish train/validation/test strategy
- Train baseline and candidate models
- Evaluate predictive performance
- Generate local and global SHAP explanations
- Test explanation consistency

### Phase 7: Human-Readable Explanation

- Map technical features to business-readable labels
- Construct deterministic explanation templates
- Preserve original model evidence
- Handle weak or missing evidence
- Test generated explanations against actual features

### Phase 8: Revenue Exposure and Prioritization

- Define customer-value methodology
- Define revenue-exposure calculation
- Define evidence-quality logic
- Define business-priority methodology
- Compare standalone risk ranking with enriched prioritization

### Phase 9: Decision-Support Application

- Build Streamlit interface
- Create executive overview
- Build customer-risk page
- Add SHAP investigation view
- Add revenue-exposure analysis
- Add segmentation and business context
- Add traceable insights

### Phase 10: Testing and Evaluation

- Validate data transformations
- Validate business metrics
- Evaluate model performance
- Evaluate SHAP explanations
- Test unexpected/unexplained churn cases
- Test revenue-exposure calculations
- Test prioritization
- Verify dashboard outputs against analytical datasets

### Phase 11: Documentation and Finalization

- Document architecture
- Document dataset and schema
- Document methodology
- Record experimental results
- Document limitations
- Prepare academic report
- Prepare final presentation and demonstration

---

## 25. Evaluation Framework

### Data and analytical evaluation

- Data-quality validation
- Correctness of business metrics
- Relationship consistency
- Feature validity
- Temporal correctness

### Churn-model evaluation

The exact metrics will depend on the target and class distribution, but may include:

- Precision
- Recall
- F1-score
- ROC-AUC
- PR-AUC
- Calibration
- Confusion matrix

Accuracy alone will not be treated as sufficient evidence of model quality, particularly if churn is imbalanced.

### Segmentation evaluation

- Cluster quality
- Stability where appropriate
- Business interpretability
- Distinct behavioral and economic profiles

### Explainability evaluation

- Whether top SHAP contributors correspond to actual customer features
- Whether explanations are traceable to model output
- Whether explanations avoid unsupported causal claims
- Whether local explanations are understandable to a business user
- Whether global explanations provide useful model-level context

### Evidence-quality evaluation

The project will test whether the evidence-quality logic distinguishes cases with strong observable deterioration from cases where the model prediction has weak observable support.

### Decision-support evaluation

RevLens will assess whether the integrated output:

- Links high-risk customers to customer value
- Quantifies revenue exposure transparently
- Distinguishes risk from business importance
- Identifies affected customers or segments
- Provides more context than a standalone churn score

Where practical:

```text
Model-only output
        vs
Enriched RevLens output
```

will be compared to demonstrate the value of the integration.

No performance numbers will be claimed before experimental evaluation.

---

## 26. Important Limitations

RevLens can only reason from the information available in its data.

It cannot automatically know:

- A customer's personal reason for cancelling
- An unrecorded competitor influence
- A private business decision
- An external event not represented in the data
- Whether a recommended retention action would actually work

A model trained on one SaaS domain may also not generalize directly to another domain.

If the selected dataset contains insufficient observations or lacks reliable churn signals, the predictive component may not be scientifically defensible. In that situation, the correct response is to document the limitation rather than manufacture predictions.

---

## 27. What RevLens Must Never Claim

RevLens must not claim:

> The model knows why the customer will churn.

Instead:

> The model identifies observable factors that contributed to the predicted churn risk.

RevLens must not claim:

> SHAP proves declining usage caused churn.

Instead:

> SHAP indicates that declining usage contributed to the model's prediction.

RevLens must not claim:

> The system can explain every churn event.

Instead:

> The system explains predictions using available observable data and flags cases where evidence is insufficient.

RevLens must not claim:

> The recommended discount will prevent churn.

Unless a separate methodology supports that conclusion.

---

## 28. Project Boundaries

RevLens is an academic analytics and decision-support project.

It does not currently claim to provide:

- A production billing system
- A full enterprise SaaS platform
- Guaranteed real-time processing
- Production-grade financial forecasting
- Production-grade automated retention actions
- Causal inference without a dedicated causal methodology
- Guaranteed model transferability across all SaaS businesses

The project prioritizes analytical correctness, explainability, traceability, evaluation, and business usefulness.

---

## 29. Repository Structure

```text
revlens/
├── data/
│   ├── raw/
│   ├── processed/
│   └── features/
├── notebooks/
├── src/
│   ├── ingestion/
│   ├── preprocessing/
│   ├── analytics/
│   ├── modeling/
│   ├── explainability/
│   └── insights/
├── app/
├── tests/
├── models/
├── configs/
├── requirements.txt
└── README.md
```

The final repository structure will reflect the actual implementation.

---

## 30. Final Project Direction

The project should now be treated as:

```text
NOT:

SaaS Dashboard
+ Churn Model
+ Segmentation
+ Forecasting
+ Anomaly Detection

BUT:

Explainable Customer Risk Intelligence
                  ↓
          Business Context
                  ↓
          Financial Exposure
                  ↓
          Customer Priority
                  ↓
        Decision-Support System
```

Supporting analytics remain important, but they serve the central customer-risk workflow rather than competing with it.

The project should not become larger by adding random models.

It should become stronger by making the existing workflow:

- More rigorous
- More explainable
- More traceable
- More financially contextualized
- More carefully evaluated
- More defensible academically

---

## 31. Working Definition for Faculty

If asked to explain the project in 20 seconds:

> “RevLens takes customer, subscription, usage, and revenue data from a SaaS business. It predicts which customers are at risk of churn, uses explainable machine learning to identify the observable factors behind each prediction, calculates the associated revenue exposure, and prioritizes customers based on business importance. The goal is not to claim that the model knows the true reason for churn, but to turn predictive risk into a traceable business decision-support output.”

If asked for the input:

> “Customer, subscription, usage, and revenue data, with acquisition and other business data where available.”

If asked for the output:

> “An explainable customer-risk profile containing churn probability, contributing observable factors, evidence quality, customer value, revenue exposure, and business priority.”

If asked for the end goal:

> “To identify which customers are likely to churn, understand the observable signals behind the prediction, quantify the revenue exposed, and determine which customers deserve the greatest business attention.”

If asked why the metrics are combined:

> “We are not saying SaaS companies should stop analyzing metrics separately. Different teams need different metrics. RevLens connects those outputs when a cross-functional decision is required, such as determining which churn risks represent the greatest financial exposure.”

If asked what happens when a customer suddenly churns without warning:

> “The system should not invent a reason. If the customer had low predicted risk and no significant observable warning signals, RevLens flags the churn as unexpected or insufficiently explained by the available data.”

---

## 32. Implementation Principles

1. Keep the code simple and readable.
2. Select and validate the dataset before building the predictive pipeline.
3. Define the churn target and prediction window explicitly.
4. Prevent temporal data leakage.
5. Use SHAP for model-level feature attribution.
6. Use deterministic Python logic for human-readable explanations.
7. Preserve the numerical evidence behind every explanation.
8. Never present model attribution as causal proof.
9. Explicitly represent weak or unavailable evidence.
10. Separate historical analysis from prediction.
11. Separate prediction from explanation.
12. Separate explanation from causal claims.
13. Separate risk from customer value.
14. Separate customer value from business priority.
15. Avoid arbitrary fixed-dollar value thresholds.
16. Do not add models merely to make the project appear larger.
17. Prioritize depth and evaluation over model count.
18. Do not automate intervention recommendations without supporting methodology.
19. Keep Streamlit as the application layer, not the analytical engine.
20. Make every major insight traceable to its underlying data and model output.

---

## 33. Expected Final Outcome

The completed RevLens system should demonstrate:

```text
Reliable Data
      ↓
Business Metrics
      ↓
Customer Behavioral Features
      ↓
Churn Prediction
      ↓
Explainable ML
      ↓
Human-Readable Evidence
      ↓
Customer Value
      ↓
Revenue Exposure
      ↓
Business Priority
      ↓
Traceable Decision Support
      ↓
Interactive Streamlit Application
```

The project will be considered successful when it can demonstrate experimentally that the system can:

1. Build a valid customer-level analytical dataset.
2. Predict churn using information available before the prediction point.
3. Explain individual predictions using model-attributed observable features.
4. Translate those explanations into traceable human-readable output.
5. Identify cases where available evidence is insufficient.
6. Quantify revenue exposure using an explicitly defined methodology.
7. Distinguish customer risk from customer value and business priority.
8. Present the complete reasoning chain through an interactive application.
9. Evaluate the system's technical performance and decision-support usefulness.

The central idea is:

> A churn probability tells a business who may leave. RevLens is designed to show what observable evidence supports that prediction, how financially important the customer is, and why that customer should receive attention.
