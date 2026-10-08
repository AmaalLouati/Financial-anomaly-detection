# Problem Definition

## 1. Business Problem

Financial institutions process very large volumes of transactions every day. Among these transactions, some may present unusual patterns or potentially suspicious financial behaviour, including abnormal transaction amounts, unusual transaction velocity, repeated transaction patterns, rapid movement of funds, unusual counterparties, structuring patterns, or complex flows between multiple accounts.

Manually reviewing every transaction is neither efficient nor scalable. AML and financial crime analysts therefore need systems that can automatically identify unusual financial activity and help them focus their investigations on the transactions, accounts, and networks that require the most attention.

Traditional rule-based monitoring systems can identify predefined suspicious patterns, but relying only on fixed rules may generate a large number of alerts and may fail to capture more complex behavioural or network anomalies.

The objective of this project is to develop a Financial Anomaly Detection and AML Investigation System capable of analysing financial activity at several levels:

- transaction-level anomalies;
- customer and account behavioural anomalies;
- repeated transaction patterns;
- unusual relationships between counterparties;
- transaction velocity and rapid movement of funds;
- network and circular transaction patterns;
- machine-learning-based anomalies that may not be captured by predefined rules.

The system will combine rule-based detection, statistical analysis, machine learning, and graph analytics to generate anomaly scores and risk levels for activities requiring further investigation.

To support analysts rather than replace them, the system will also provide explanations describing the main factors behind each alert. The final investigation decision remains with the human analyst.

The system does not classify an unusual transaction as proven fraud or money laundering. An anomaly represents a deviation or suspicious pattern that requires further analysis.

Ultimately, the project aims to reduce unnecessary manual review, improve alert prioritization, and provide analysts with a more explainable and structured view of financial transaction risk.


## 2. System Objectives

The primary objective of this project is to develop an intelligent and explainable financial anomaly detection system that supports AML and financial crime analysts in identifying, assessing, and prioritizing unusual financial activities.

The system is designed to:

- **Detect financial anomalies** at transaction, behavioural, and network levels by combining rule-based detection, statistical methods, machine learning, and graph analytics.
- **Identify behavioural deviations** by comparing current transaction activity with historical account behaviour and relevant reference baselines.
- **Detect complex transaction patterns**, including unusual amounts, abnormal transaction velocity, repeated payment patterns, rapid movement of funds, unusual counterparties, structuring behaviour, collector accounts, and circular transaction flows.
- **Generate anomaly scores and risk levels** to support consistent and efficient alert prioritization.
- **Provide explainable alerts** by identifying the main factors and patterns contributing to each detected anomaly.
- **Reduce unnecessary manual review** by helping analysts focus their attention on higher-priority activities.
- **Support investigation and decision-making** through structured and interpretable information while maintaining a human-in-the-loop approach.

The system is intended to function as a decision-support tool rather than an autonomous fraud or money-laundering classifier. A detected anomaly indicates unusual behaviour requiring further investigation and does not constitute evidence of financial crime.


## 3. Target Users

The primary users of the system are:

- **AML Analysts** responsible for reviewing potentially suspicious financial activities;
- **Financial Crime Analysts** investigating unusual transaction patterns and account behaviour;
- **Risk and Compliance Teams** requiring structured information to support financial risk monitoring.

The system is designed to help these users identify high-priority cases, understand why an alert was generated, and investigate relevant transaction and network information more efficiently.


## 4. Project Scope

The first version of the project focuses on ten main categories of financial anomalies:

1. **Unusual transaction amounts**  
   Transactions whose amounts significantly deviate from the historical behaviour of an account.

2. **Repeated round or identical amounts**  
   Repeated transactions involving identical or unusually round amounts, particularly between the same counterparties.

3. **Abnormal transaction velocity**  
   An unusually high number or volume of transactions within a short period of time.

4. **Behavioural deviations**  
   Significant changes compared with an account's historical transaction behaviour.

5. **Rapid inflow and outflow of funds**  
   Funds received by an account and transferred again within an unusually short period.

6. **Unusual counterparties**  
   Significant changes in the number, frequency, or nature of counterparties interacting with an account.

7. **Collector and dispersion patterns**  
   Many-to-one or one-to-many transaction structures in which funds are collected from or distributed to multiple accounts.

8. **Structuring patterns**  
   Sequences of smaller transactions that collectively form an unusual financial pattern.

9. **Circular transaction patterns**  
   Funds moving through several accounts and eventually returning to an account already present in the transaction chain.

10. **Machine-learning-based anomalies**  
    Unusual combinations of transaction characteristics detected by anomaly detection models even when no predefined rule is triggered.


## 5. Detection Approach

The system will progressively combine several complementary approaches:

### Rule-Based Detection
Predefined and interpretable rules will be used to identify known transaction patterns.

### Statistical Analysis
Historical transaction behaviour will be analysed to establish behavioural baselines and identify significant deviations.

### Machine Learning
Anomaly detection algorithms will be used to identify unusual combinations of transaction characteristics that may not be captured by predefined rules.

### Graph Analytics
Accounts will be represented as nodes and transactions as relationships between them to identify network structures such as circular flows, collector accounts, and unusual connectivity patterns.

These approaches will contribute to a unified anomaly assessment process rather than operating as isolated detection systems.


## 6. Risk Scoring and Explainability

Detected activities will be evaluated through an anomaly scoring and risk prioritization mechanism.

The system will produce outputs such as:

- **Anomaly Score**
- **Risk Level**
- **Detected Indicators**
- **Explanation / Reasons**
- **Recommended Review Status**

For example:

> **Risk Level: HIGH**  
> Multiple unusual indicators detected, including abnormal transaction velocity, repeated amounts, rapid movement of funds, and unusual counterparties.  
> **Action: REVIEW REQUIRED**

The risk score is intended to support prioritization. It must not be interpreted as a probability that a customer has committed fraud or money laundering.


## 7. Cold-Start Strategy

Some accounts may not have enough historical information to establish a reliable individual behavioural baseline.

For accounts with sufficient history, the system will use a:

**Personal Behavioural Baseline**

For new or low-history accounts, the system will rely on:

**Reference / Peer Baseline + Rule-Based Indicators**

The system should also account for lower confidence when historical information is insufficient.

This approach allows anomaly detection to remain possible without assuming that a newly created account behaves exactly like an established account.


## 8. Multi-Currency Transactions

The project will support transactions involving multiple currencies.

Original transaction information will be preserved, including:

- original amount;
- original currency;
- received amount;
- receiving currency.

When comparisons across currencies are required, a currency normalization strategy will be applied before comparing transaction amounts.

Currency conversion must therefore be treated as a preprocessing step rather than assuming that equal numerical amounts expressed in different currencies have equal financial value.


## 9. Human-in-the-Loop Approach

The system follows a **Human-in-the-Loop (HITL)** approach.

Its purpose is to assist analysts by detecting, scoring, explaining, and prioritizing unusual activity.

The system does not make the final decision regarding whether an activity represents fraud, money laundering, or legitimate behaviour.

The final investigation and decision remain the responsibility of a qualified human analyst.


## 10. Limitations and Responsible AI

Several limitations must be considered throughout the project:

- An anomaly is not automatically evidence of fraud or money laundering.
- Legitimate behaviour may sometimes appear unusual.
- Detection systems may generate false positives and false negatives.
- Risk indicators must be explainable whenever possible.
- Historical data and labels may contain biases.
- Customer characteristics should not be used blindly as risk indicators.
- New accounts may have insufficient historical information for reliable behavioural modelling.
- The quality of anomaly detection depends on the quality and representativeness of the available data.
- Synthetic datasets may not reproduce every characteristic of real-world banking activity.

The project therefore prioritizes explainability, transparency, responsible use of data, and human oversight.


## 11. Expected System Output

The final system is expected to transform raw financial transactions into structured investigation information through the following workflow:

Transactions and Account Data  
→ Data Validation and Preprocessing  
→ Feature Engineering  
→ Rule-Based and Statistical Detection  
→ Machine Learning Anomaly Detection  
→ Graph Analysis  
→ Anomaly Scoring  
→ Risk Prioritization  
→ Explainability  
→ Human Investigation

Later components of the project may provide dashboards and investigation-support tools to help analysts explore alerts, account behaviour, transaction histories, and network relationships.


## 12. Project Vision

The long-term objective is not to build a simple binary fraud classifier.

Instead, the project aims to build an explainable financial anomaly intelligence system capable of answering three key questions:

1. **What is unusual?**
2. **Why is it unusual?**
3. **Which cases should an analyst investigate first?**

This approach places anomaly detection, explainability, and human decision-making at the core of the system.
