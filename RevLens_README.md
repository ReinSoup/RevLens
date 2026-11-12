# RevLens
## Agentic AI for SaaS Churn & Decision Support

RevLens is an AI-powered SaaS customer-risk intelligence system designed to predict customer churn, explain individual customer predictions, and assess recurring revenue exposure. It combines XGBoost-based churn prediction and SHAP explainability with a **Revenue Risk Investigation Agent** that interprets business queries, selects analytical tools, retrieves relevant evidence, and produces structured reports for human review.

**Project status:** Academic project under development. This README documents the agreed project scope and planned architecture. It does not imply that every described component has already been implemented or evaluated.

---

## Abstract

RevLens is an AI-powered SaaS customer-risk intelligence system that predicts customer churn and measures recurring revenue exposure. It uses XGBoost to estimate churn probability and SHAP to explain individual customer predictions. Accounts are prioritised for attention based on a combination of customer value and revenue exposure.

A Revenue Risk Investigation Agent leverages a local large language model to understand business queries, choose analytical tools, retrieve relevant evidence, and produce structured reports. An interactive Streamlit application presents customer risk profiles, model explanations, financial exposure, and AI-generated insights for human review. The project assesses predictive performance and the trustworthiness of agentic AI for supporting business decisions.

---

## 1. Project Overview

SaaS businesses maintain information about customers, subscriptions, product usage, and recurring revenue. Each data domain provides useful information, but a churn probability alone does not explain the customer's financial importance or show which accounts should be investigated first.

RevLens connects these analytical outputs through two major components.

### Customer Risk Intelligence

The analytical foundation of the system:

- Customer and subscription data preparation
- Customer-level feature engineering
- Churn probability prediction using XGBoost
- Individual prediction explanations using SHAP
- Customer value assessment
- Recurring revenue exposure calculation
- Customer prioritisation

### Revenue Risk Investigation Agent

The agentic decision-support layer:

- Understands business questions expressed in natural language
- Selects relevant analytical tools
- Retrieves customer, revenue, and model evidence
- Connects findings across analytical components
- Verifies calculations and evidence
- Produces structured investigation reports for human review

The agent does not replace the analytical models. It coordinates their outputs to investigate broader business questions.

---

## 2. Problem Statement

A churn prediction indicates how likely a customer is to churn according to the model. It does not, by itself, show how financially important the customer is or what the business should investigate.

Consider this illustrative example:

| Customer | Predicted churn probability | Monthly recurring revenue |
|---|---:|---:|
| Customer A | 90% | $50 |
| Customer B | 75% | $8,000 |

Customer A has the higher predicted churn probability, but Customer B may represent greater risk-weighted recurring revenue exposure.

RevLens therefore keeps four concepts distinct:

| Concept | Meaning |
|---|---|
| Churn risk | Model-estimated probability of churn |
| Customer value | Customer's relative economic importance |
| Revenue exposure | Estimated recurring revenue associated with predicted risk |
| Business priority | Reproducible prioritisation based on defined business logic |

A second challenge is that users may need to navigate multiple dashboard sections to connect revenue trends, customer details, churn predictions, and model explanations. The Revenue Risk Investigation Agent is intended to coordinate those analytical steps in response to a business question.

---

## 3. Project Objectives

RevLens aims to:

1. Prepare and validate SaaS customer, subscription, usage, and revenue data.
2. Engineer customer-level features using information available at the prediction point.
3. Predict churn probability using XGBoost.
4. Explain individual predictions using SHAP.
5. Present model evidence in an interpretable form.
6. Assess customer value and calculate recurring revenue exposure.
7. Prioritise accounts using explicit, reproducible logic.
8. Develop an agent that investigates business queries using controlled analytical tools.
9. Verify agent findings against underlying analytical evidence.
10. Evaluate predictive performance and the reliability of agentic AI for business decision support.

The project focuses on connecting explainable churn analytics with evidence-grounded investigation. It does not claim to introduce a new machine-learning algorithm.

---

## 4. System Architecture

RevLens is organised into three connected layers:

1. Customer Risk Intelligence
2. Revenue Risk Investigation Agent
3. Streamlit Application

### 4.1 High-level architecture

```text
                 SAAS CUSTOMER DATA
                         |
                         v
              DATA INGESTION AND QUALITY
                         |
                         v
              CUSTOMER-LEVEL FEATURES
                         |
                         v
                  XGBOOST MODEL
                         |
                         v
                CHURN PROBABILITY
                         |
                         v
                   SHAP EXPLANATION
                         |
                         v
               CUSTOMER RISK EVIDENCE
                         |
              +----------+----------+
              |                     |
              v                     v
        CUSTOMER VALUE        REVENUE EXPOSURE
              |                     |
              +----------+----------+
                         |
                         v
              CUSTOMER PRIORITISATION
                         |
                         v
              SHARED ANALYTICAL TOOLS
                         |
                         v
         REVENUE RISK INVESTIGATION AGENT
                         |
                         v
           VERIFIED INVESTIGATION REPORT
                         |
                         v
                STREAMLIT APPLICATION
```

### 4.2 Component responsibilities

| Component | Responsibility |
|---|---|
| Data pipeline | Ingest, validate, clean, and prepare source data |
| Feature engineering | Create customer-level predictive features |
| XGBoost | Estimate churn probability |
| SHAP | Explain model-attributed feature contributions |
| Revenue analytics | Calculate supported recurring revenue metrics |
| Exposure and priority logic | Calculate revenue exposure and customer priority |
| Ollama-hosted LLM | Interpret business questions and select relevant tools |
| Python orchestrator | Validate and execute tool calls, maintain state, and enforce limits |
| Evidence verifier | Check calculations, references, and evidence support |
| Streamlit | Present customer-risk information, investigation progress, and reports |

The dashboard and agent should use the same underlying analytical services. Revenue calculations, churn predictions, SHAP explanations, and prioritisation should not be independently reimplemented inside the agent.

---

## 5. Customer Risk Intelligence

### 5.1 Churn prediction

The churn model addresses:

> Based on information available before the prediction point, how likely is this customer to churn within the defined prediction window?

XGBoost is the planned primary churn model. The project must explicitly define:

- The customer or account unit of analysis
- The churn target
- The historical observation window
- The prediction horizon
- The train, validation, and test strategy

### 5.2 Customer-level feature engineering

Potential feature groups include:

| Feature group | Examples |
|---|---|
| Subscription | Plan, subscription status, tenure, renewal timing |
| Revenue | Customer MRR, ARR, recurring-value changes |
| Engagement | Sessions, active days, feature usage |
| Behavioural trends | Usage changes over 1, 3, or 6 months |
| Customer history | Plan changes, previous cancellations, support activity |
| Customer value | MRR percentile, revenue share, historical expansion |

Potential features include `customer_tenure_months`, `customer_mrr`, `mrr_change_3m`, `sessions_change_30d`, `days_since_last_activity`, and `downgrade_count_6m`. The final list depends on the selected dataset and must be documented.

### 5.3 Temporal leakage prevention

For a prediction made at time T, features must use only information available at or before T.

```text
       HISTORICAL OBSERVATION WINDOW
  ---------------------------------------
      Information available at time T
                      |
                      v
               PREDICTION POINT
                      |
                      v
         FUTURE CHURN OBSERVATION WINDOW
               Used for the target
```

Information that becomes available after cancellation or after the prediction point must not be used to construct features for that prediction. Validation should respect the temporal structure of the data.

### 5.4 Model evaluation

Potential metrics include:

- Precision
- Recall
- F1-score
- ROC-AUC
- PR-AUC / Average Precision
- Confusion matrix
- Probability calibration

Accuracy alone is insufficient when churn is imbalanced. Quantitative results will be reported only after evaluation.

---

## 6. SHAP Explainability

SHAP is the planned method for explaining how input features contribute to an individual model prediction.

### Local explanations

Local explanations answer:

> Which features contributed to this customer's predicted churn risk?

The customer-risk view should present the strongest contributing features together with the corresponding customer values.

### Global explanations

Global explanations answer:

> Which features generally influence predictions across the evaluated customer population?

Global analysis can help assess model behaviour and feature influence.

### Interpretation boundary

SHAP explains model attribution. It does not establish the actual cause of a customer's decision to cancel.

Use language such as:

- Feature contributing to the prediction
- Model-attributed factor
- Observable risk signal
- Predictive contributor

Avoid causal statements unless a separate causal methodology is implemented.

### Human-readable explanations

The preferred initial approach is deterministic Python mapping from SHAP contributors and actual feature values to business-readable descriptions. The language model must not invent, replace, or alter SHAP evidence.

If evidence is weak or unavailable, the system should state that limitation rather than generate an unsupported explanation.

---

## 7. Customer Value and Revenue Exposure

### 7.1 Customer value

Customer value should be assessed relative to the available customer population rather than using arbitrary fixed-dollar thresholds.

Potential measures include:

- MRR percentile
- Revenue share of company MRR
- LTV percentile, if supported by the data
- Historical expansion and subscription context

Any relative classifications must be documented and justified.

### 7.2 Revenue exposure

An initial risk-weighted MRR estimate may be defined as:

```text
Risk-Weighted MRR Exposure
=
Churn Probability x Customer MRR
```

For example, an 80% churn probability for a customer with $5,000 MRR produces an estimated risk-weighted MRR exposure of $4,000.

This is an estimate, not guaranteed financial loss. The implementation must document the recurring-revenue measure, prediction horizon, and assumptions. The calculation must be performed by deterministic Python logic, not generated by the LLM.

### 7.3 Customer prioritisation

Customer priority should not be based on churn probability alone. Potential inputs include:

- Churn probability
- Customer value
- Revenue exposure
- Evidence quality, if implemented
- Customer and subscription context

The final prioritisation method must be explicit, reproducible, and evaluated. Risk, value, exposure, and priority remain separate outputs.

---

## 8. Revenue Risk Investigation Agent

### 8.1 Purpose

The Revenue Risk Investigation Agent (RRIA) is the agentic AI component of RevLens.

It allows a business user to ask a question in natural language and have the system investigate it by selecting controlled analytical tools, retrieving evidence, connecting findings, verifying results, and generating a structured report.

The agent is an orchestration layer over RevLens analytical services. It is not a replacement for XGBoost, SHAP, or deterministic business calculations.

### 8.2 Example business query

> Our revenue growth has slowed this month. Investigate what is happening, identify affected customer segments and accounts, estimate the recurring revenue exposed to churn risk, and identify which accounts should be investigated first.

A possible investigation is:

1. Retrieve current and comparison-period revenue KPIs.
2. Compare MRR, growth, new MRR, expansion MRR, contraction MRR, and churned MRR.
3. Decompose revenue movement and check whether supported components reconcile.
4. Identify affected plans, cohorts, or customer segments.
5. Retrieve relevant customer and subscription records.
6. Retrieve existing churn predictions for relevant active customers.
7. Retrieve SHAP explanations associated with those predictions.
8. Retrieve historical activity where available.
9. Calculate risk-weighted recurring revenue exposure.
10. Apply deterministic customer prioritisation.
11. Verify the evidence and generate an investigation report.

The agent should choose follow-up tools based on intermediate results. It should not execute every available tool for every question.

### 8.3 Investigation lifecycle

```text
          BUSINESS QUESTION
                  |
                  v
                 PLAN
       Understand and structure task
                  |
                  v
               EXECUTE
        Select and call a tool
                  |
                  v
           INSPECT RESULTS
                  |
                  v
       MORE INVESTIGATION NEEDED?
             /           \
           YES            NO
            |              |
            v              v
       SELECT NEXT       VERIFY
          TOOL           EVIDENCE
            |              |
            +----<---------+
                           |
                           v
                         REPORT
                           |
                           v
                      HUMAN REVIEW
```

**Plan:** Interpret the question, reporting period, required evidence, and expected output.

**Execute:** Select a permitted tool and validate its name and arguments.

**Investigate:** Inspect returned results and conditionally select follow-up tools.

**Verify:** Check calculations, time-period alignment, customer identifiers, prediction references, SHAP associations, exposure calculations, and priority outputs.

**Report:** Generate a structured response using verified evidence. State where information is unavailable or insufficient.

The Python orchestrator enforces tool permissions, timeouts, error handling, and maximum call limits. The LLM does not control these safeguards.

### 8.4 Initial analytical tool registry

The planned toolset includes:

| Tool | Purpose |
|---|---|
| `get_revenue_kpis` | Retrieve validated revenue KPIs for a reporting period |
| `compare_revenue_periods` | Compare current and reference-period metrics |
| `decompose_revenue_change` | Examine new, expansion, contraction, and churned MRR contributions |
| `get_segment_analysis` | Analyse supported customer or subscription segments |
| `get_customer_profile` | Retrieve customer and subscription context |
| `get_churn_prediction` | Retrieve an existing churn prediction and model metadata |
| `get_shap_explanation` | Retrieve the explanation associated with a specific prediction |
| `get_customer_activity_history` | Retrieve historical behavioural observations |
| `calculate_revenue_exposure` | Apply the documented exposure calculation |

These are logical capabilities. Related tools may share internal analytical functions rather than duplicate calculations.

Each tool must have:

- A defined purpose and name
- Typed and validated arguments
- A documented structured return value
- Controlled data access
- Error handling for missing or invalid inputs
- Tests for normal, empty, and invalid cases

The agent must not have unrestricted SQL execution, arbitrary Python execution, or uncontrolled file access.

### 8.5 Investigation state and traceability

The orchestrator should maintain structured state containing:

- Original question and investigation identifier
- Reporting and comparison periods
- Investigation plan and current stage
- Tools called, arguments, status, and results
- Evidence references and relevant customer identifiers
- Data snapshot and prediction timestamps
- Model version where available
- Verified findings and unresolved questions
- Errors, limitations, and final report metadata

Important report claims should be traceable to the corresponding analytical result. SHAP evidence must refer to the correct customer prediction and feature snapshot.

### 8.6 Verification and safeguards

Verification is a required system component, not an LLM self-check.

The verifier should check:

- Revenue calculations against metric definitions
- Revenue movement reconciliation where supported
- Reporting-period and data-snapshot alignment
- Customer identifier validity
- Prediction availability and timestamp
- SHAP-to-prediction association
- Revenue-exposure inputs and formula
- Customer priority against deterministic output
- Evidence supporting report statements

The LLM may summarise verified results but must not alter numerical outputs or customer rankings. Failed checks must cause findings to be withheld, qualified, or marked unresolved.

### 8.7 Investigation report format

The initial report should contain:

1. Investigation question and reporting period
2. Executive finding
3. Revenue movements
4. Segment findings
5. Relevant customer accounts
6. Churn predictions and SHAP evidence
7. Revenue exposure and assumptions
8. Prioritised accounts
9. Suggested investigations for human review
10. Limitations and unanswered questions

The report must distinguish observed facts, model predictions, model-attributed contributors, calculated estimates, and recommendations.

### 8.8 Technology approach

| Technology | Planned responsibility |
|---|---|
| Python | Tool functions, orchestration, validation, and verification |
| Ollama | Local LLM inference and tool-calling interface |
| Pandas / SQL services | Controlled analytics and data retrieval |
| Pydantic or equivalent | Optional validation of tool arguments and structured outputs |
| Streamlit | Investigation interface and report display |
| Python logging / structured records | Execution trace and investigation history |

The initial implementation will use one local LLM and one explicit Python orchestrator. Model selection will depend on tool-calling reliability, structured output, latency, and available hardware.

No manual fine-tuning is required for the initial version. Prompt instructions, tool schemas, and controlled Python functions are the starting point.

### 8.9 Initial exclusions

The first agent version will not include:

- Multiple collaborating agents
- Autonomous customer emails or CRM changes
- Automatic discounts or retention interventions
- LLM-generated churn predictions or SHAP values
- Unrestricted SQL or Python execution
- Fine-tuning without an evaluated need
- Automatic learning from previous investigations
- Guaranteed real-time monitoring

The agent remains read-only and supports human decision-making.

---

## 9. Streamlit Application

Streamlit is the user interface, not the analytical engine.

The planned application will contain three primary views.

### Executive Overview

- Revenue and retention KPIs
- Churn overview
- Revenue exposure
- High-priority customer summary
- Relevant business insights

### Customer Risk

- Customer profile and subscription context
- MRR and customer value
- Predicted churn probability
- SHAP contributors and actual feature values
- Revenue exposure
- Business priority
- Historical activity where available

### AI Investigation

- Natural-language business question
- Reporting-period selection where needed
- Investigation progress from actual orchestrator events
- Tool execution status
- Supporting evidence and analytical results
- Prioritised customer findings
- Structured investigation report
- Verification status and limitations

The application must display actual execution progress rather than simulated tool activity.

---

## 10. Evaluation Plan

Predictive model quality and agent quality must be evaluated separately.

### Predictive evaluation

- Precision, recall, and F1-score
- ROC-AUC and PR-AUC
- Confusion matrix
- Probability calibration
- Temporal validation and leakage checks

### Explainability evaluation

- SHAP contributors correspond to actual customer features
- Explanations refer to the correct model prediction
- Actual feature values are preserved
- Explanations avoid unsupported causal claims

### Revenue and prioritisation evaluation

- Revenue KPI calculation correctness
- Exposure formula correctness
- Customer-value methodology
- Priority reproducibility
- Comparison of model-only ranking with enriched prioritisation

### Agent evaluation

| Dimension | Evaluation question |
|---|---|
| Tool-selection accuracy | Did the agent select relevant tools? |
| Evidence accuracy | Do report claims match returned data? |
| Investigation completeness | Did it retrieve the necessary evidence? |
| Calculation integrity | Did deterministic checks pass? |
| Traceability | Can findings be traced to their sources? |
| Decision-support usefulness | Does the report add useful context beyond a standalone churn score? |

### Initial investigation scenarios

1. **Revenue growth slowdown:** Identify relevant revenue movements, affected segments, and accounts.
2. **High-value customer investigation:** Investigate a high-value customer with elevated predicted churn risk.
3. **Segment-level churn investigation:** Identify segments with elevated churn risk and associated revenue exposure.

Expected findings should be manually verified for test scenarios. The project must not assume agent-assisted prioritisation is better before evaluating it.

---

## 11. Development Roadmap

| Phase | Focus | Main deliverables |
|---|---|---|
| 1 | Scope and dataset | Research question, dataset assessment, target definition |
| 2 | Data foundation | Ingestion, cleaning, validation, integrated data model |
| 3 | Revenue and customer analytics | Supported SaaS metrics and customer analysis |
| 4 | Feature engineering | Customer-level temporal features and leakage controls |
| 5 | Churn modelling | Baseline and XGBoost model evaluation |
| 6 | Explainability | SHAP explanations and deterministic interpretation |
| 7 | Exposure and prioritisation | Customer value, exposure, and priority methodology |
| 8 | Core Streamlit application | Executive and customer-risk views |
| 9 | Agent tool foundation | Tested Python analytical tools |
| 10 | Agent integration | Ollama, tool registry, and orchestrator |
| 11 | Verification and reporting | Investigation state, evidence checks, structured reports |
| 12 | AI investigation interface | Streamlit investigation page |
| 13 | Evaluation and documentation | Scenario tests, results, limitations, final report |

### First agent milestone

The initial working demonstration should be deliberately narrow.

**Question:** "Why has MRR growth slowed this month?"

**Initial tools:**

1. `get_revenue_kpis`
2. `compare_revenue_periods`
3. `decompose_revenue_change`

**Success criteria:**

- The LLM selects relevant tools.
- Python validates and executes the calls.
- Returned results contain actual analytical values.
- The agent identifies supported contributors to the slowdown.
- Verification checks the calculations.
- The final report matches the Python results and identifies limitations.

Customer-level and SHAP investigation should be added after this workflow works reliably.

---

## 12. Technology Stack

| Technology | Purpose |
|---|---|
| Python | Data processing, analytics, modelling, and orchestration |
| SQL | Structured data retrieval and analysis |
| Pandas / NumPy | Data manipulation and numerical operations |
| Scikit-learn | Preprocessing, evaluation, and supporting methods |
| XGBoost | Churn prediction |
| SHAP | Model explainability |
| Ollama | Local LLM for agentic investigation |
| Streamlit | Interactive web application |
| Matplotlib / Seaborn / Plotly | Visualisation where appropriate |
| Git / GitHub | Version control and documentation |

Dependencies should be added only when justified by the implementation.

---

## 13. Proposed Repository Structure

The following structure represents the planned architecture. It should be reconciled with the actual repository as implementation progresses.

```text
RevLens/
├── data/
│   ├── raw/
│   ├── processed/
│   └── features/
├── notebooks/
├── src/
│   ├── ingestion/
│   ├── preprocessing/
│   ├── features/
│   ├── analytics/
│   │   ├── revenue_analysis.py
│   │   ├── customer_analysis.py
│   │   └── segment_analysis.py
│   ├── modeling/
│   │   └── churn_model.py
│   ├── explainability/
│   │   └── shap_explainer.py
│   ├── prioritization/
│   │   ├── revenue_exposure.py
│   │   └── customer_priority.py
│   ├── tools/
│   │   ├── revenue_tools.py
│   │   ├── customer_tools.py
│   │   └── churn_tools.py
│   └── agent/
│       ├── llm_client.py
│       ├── orchestrator.py
│       ├── tool_registry.py
│       ├── investigation_state.py
│       ├── prompts.py
│       ├── verifier.py
│       └── report_generator.py
├── app/
│   ├── streamlit_app.py
│   └── pages/
│       └── investigation.py
├── tests/
│   ├── test_analytics.py
│   ├── test_agent_tools.py
│   ├── test_orchestrator.py
│   ├── test_verifier.py
│   └── test_investigations.py
├── models/
├── configs/
├── requirements.txt
└── README.md
```

Do not create empty placeholder modules simply to match the diagram. Add modules as the corresponding functionality is implemented.

---

## 14. Limitations and Responsible Interpretation

RevLens can only investigate information represented in its available data.

It cannot automatically determine:

- A customer's private reason for cancelling
- An unrecorded competitor influence
- A business decision not represented in the data
- Whether a suggested retention action will succeed

Additional limitations:

- Synthetic data demonstrates a technical workflow, not real-world business outcomes.
- A model trained on one SaaS dataset may not generalise to another business.
- SHAP explains model behaviour, not causation.
- Revenue exposure is an estimate under documented assumptions.
- An LLM can select inappropriate tools or summarise evidence incorrectly; validation and verification are required.
- Missing or stale data may make an investigation incomplete.

The system must explicitly report insufficient evidence rather than inventing explanations or unsupported recommendations.

---

## 15. Final Project Direction

RevLens is organised around one central objective:

```text
Predict customer churn
        |
        v
Explain model predictions
        |
        v
Assess customer value
        |
        v
Estimate recurring revenue exposure
        |
        v
Prioritise customers
        |
        v
Investigate business questions
        |
        v
Verify evidence and report findings
        |
        v
Support human decisions
```

The analytical system establishes what the data and models indicate. The Revenue Risk Investigation Agent coordinates those capabilities to answer broader business questions and present the evidence in a structured form.

### Final project definition

> **RevLens is an AI-powered SaaS customer-risk intelligence and decision-support system that predicts churn using XGBoost, explains individual predictions with SHAP, assesses customer value and recurring revenue exposure, and uses a Revenue Risk Investigation Agent to investigate business queries through controlled analytical tools and evidence-backed reports.**

The central idea is:

> A churn prediction identifies who may leave. RevLens is designed to explain the model's risk signals, assess the associated financial exposure, and help business users investigate which customers require attention.

---

## 16. Academic Project Information

**Title:** RevLens: Agentic AI for SaaS Churn & Decision Support

**Domain:** Data Analytics, Business Intelligence, Machine Learning and Artificial Intelligence

**Platform:** Python, SQL, Streamlit (Web Application), XGBoost, SHAP, Ollama (Local LLM)

**Project type:** B.E. VII Semester CSE Project Work I, Academic Year 2026–27

**Authors:**
- Abdul Rab
- Bonthu Sai Vennela
