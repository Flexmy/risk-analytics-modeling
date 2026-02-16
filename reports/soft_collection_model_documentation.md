Soft Collection (Early Delinquency) Risk Model
1. General Information
1.1 Purpose

This document describes the Soft Collection risk model developed to predict delinquency progression for customers in early overdue stages. The model supports early intervention and optimized collection strategy by identifying customers likely to deteriorate into severe delinquency.

1.2 Model Objective

The model predicts whether a customer currently up to 15 Days Past Due (DPD) will reach 60+ DPD within the next 60 days.
This represents the probability of non-cure / delinquency progression in early-stage overdue accounts.

2. Data Description
2.1 Data Sources

The model uses historical credit and behavioral data including:

Credit history and delinquency records

Payment behavior

Transaction activity

Collection interaction data

External credit registry delinquency indicators

Development sample covers historical contracts over multiple years, while a separate Out-of-Time (OOT) sample is used for temporal validation.

2.2 Target Definition

BAD_FLAG_60 = 1 → Customer reaches 60+ DPD within 60 days after observation date
BAD_FLAG_60 = 0 → Customer does not reach 60+ DPD during observation window

This target measures risk of further delinquency progression, not default at origination.

3. Sampling Strategy

Stratified sampling by time and target rate

Development split into Train / Test

Separate Out-of-Time (OOT) sample for temporal robustness

Balanced representation of event rate and seasonal behavior

4. Model Architecture

The model follows a modular risk modeling framework combining multiple behavioral domains:

Demographic & financial profile

Credit history and delinquency patterns

Payment behavior

Overdue dynamics

Collection interaction intensity

Transaction activity

External delinquency indicators

This structure captures both ability and willingness to repay.

5. Modeling Approach

Algorithm: LightGBM (Gradient Boosted Trees)

Minimal preprocessing (tree models handle non-linearities & missing values)

Feature selection based on model importance ranking

Final model trained on consolidated dataset

Primary discrimination metric: Gini coefficient (2×AUC − 1)

6. Model Performance

The model demonstrates stable discriminatory power and reliable predictive capability for early-stage delinquency risk.

Key evaluation:

AUC / Gini → Model discrimination

KS → Separation power

Out-of-Time performance → Temporal stability

7. Business Implementation

Customers entering early delinquency are segmented by predicted risk:

Low Risk → Likely to self-cure → minimal intervention

Medium Risk → Requires reminders / soft contact

High Risk → Requires proactive collection

This enables:

Prioritized collection effort

Improved recovery performance

Reduced operational inefficiency

8. Model Validation & Monitoring

Validation includes:

Out-of-Time testing

Stability monitoring using Population Stability Index (PSI)

Performance tracking (Gini trend over time)

Monitoring framework detects:

Data drift

Model degradation

Need for recalibration or rebuild

9. Model Limitations

Certain customer segments (e.g., irregular income profiles) may show higher variability in payment behavior, potentially affecting model stability over time.

10. Model Lifecycle

The model is periodically monitored and updated based on:

PSI thresholds

Performance deterioration

Portfolio behavioral shifts

Appendix — Feature Domains

The model incorporates features derived from:

Payment history

Delinquency dynamics

Behavioral patterns

Collection interactions

Transaction activity
