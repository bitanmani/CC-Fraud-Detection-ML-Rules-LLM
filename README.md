# CC-Fraud-Detection-ML-Rules-LLM
A production-style fraud risk system combining Machine Learning, business rules, cost tradeoffs, and operational constraints.

This project goes beyond building a classifier. It demonstrates how real payment fraud systems are designed, tuned, and deployed—balancing fraud loss, customer experience, and operational capacity.

🔍 Business Problem

In large-scale payment systems, fraud detection is not just about accuracy. Fraud is rare, customer friction is costly, and manual review teams have limited capacity.

The challenge is to:

Detect fraud reliably

Minimize false positives that block legitimate customers

Respect manual review SLAs

Make decisions that are explainable and operationally viable

This project simulates how financial institutions design real fraud decision engines, not just ML models.

📊 Dataset

## Dataset

This project uses the Credit Card Fraud Detection dataset (ULB).

Due to GitHub file size limits, the raw dataset is not included in this repository.

**How to get it**
1. Download the dataset from Kaggle (Credit Card Fraud Detection).
2. https://drive.google.com/file/d/1LkEMabd52XxWBTUVa0eqb2AbdUFSC6Je/view?usp=sharing



Size: ~284,000 transactions

Fraud Rate: ~0.17% (extreme class imbalance)

Features:

Transaction amount

Time since first transaction

PCA-transformed behavioral features (V1–V28)

Target: Class (0 = Legitimate, 1 = Fraud)

This dataset closely reflects real-world payment fraud dynamics.

🔎 Exploratory Data Analysis (EDA)

EDA was conducted with a risk and product mindset, not just statistical exploration.

Key Findings

Fraud is extremely rare → accuracy is misleading

Fraud and legitimate transactions heavily overlap in amount

Fraud occurs across time → simple time rules fail

Naïve threshold rules are insufficient

These insights justified a hybrid ML + rules approach.

🧹 Data Cleaning & Validation

Verified no missing values

Validated target labels and numeric ranges

Detected and removed 1,081 duplicate transactions

Prevented data leakage before modeling

This ensured realistic evaluation and production-quality rigor.

🤖 Baseline Machine Learning Model

Model: Logistic Regression (class-weighted)

Why:

Interpretable

Stable under class imbalance

Common baseline in fraud systems

Output: Fraud risk probabilities (not binary decisions)

Baseline Results

High fraud recall (~87%)

Extremely low precision (~4–5%)

Excessive false positives

Conclusion:
ML alone is not deployable without decision logic.

🎯 Threshold Tuning & Risk Scoring

Instead of using a default 0.50 cutoff, the model was evaluated across multiple probability thresholds.

This allowed:

Precision vs recall tradeoff analysis

Business-aligned threshold selection

Risk-based decisioning instead of binary classification

A business threshold of 0.40 was selected as a starting point.

🧠 Hybrid ML + Rules System

To make the system operational:

ML generates a risk score

Business rules act as guardrails and overrides

Example Rules

Auto-approve very small transactions unless risk is extreme

Flag very large transactions even at moderate risk

Default to ML threshold otherwise

This reduced false positives while preserving fraud capture.

⚙️ Policy Optimization

A grid of rule configurations was evaluated using:

Fraud precision

Fraud recall

False positives (customer friction)

False negatives (missed fraud)

A recommended production policy was selected based on the best tradeoff.

💰 Cost-Based Evaluation

To align with real business decisioning:

False positives were assigned an operational cost

False negatives were assigned a fraud loss cost

This converted model performance into business impact, not just metrics.

🚦 Deployable 3-Tier Decision System

The final system outputs three actions, not just fraud/no-fraud:

Approve: Low risk, no friction

Review: Medium risk, manual investigation

Block: High risk, immediate action

📈 Capacity-Aware Decisioning

Manual review capacity was constrained to 2% of transactions.

The system dynamically tuned thresholds to:

Stay under review SLA

Preserve fraud capture

Reduce operational load

Final outcome:

Review rate: 1.12%

Block rate: 0.88%

This mirrors real payment operations.

🧠 Key Takeaways

Fraud detection is a decision system, not just a model

ML should produce risk scores, not final decisions

Rules, thresholds, costs, and capacity matter

Operational realism is as important as model performance

🚀 Future Improvements

Cost-optimized thresholding using real dollar values

Tree-based or ensemble models

Segment-specific fraud policies

Real-time monitoring dashboards

LLM-powered analyst explanations (conceptual extension)

📂 Repository Contents

Fraud_Detection.ipynb — full end-to-end analysis and system design

README.md — project overview and business framing
