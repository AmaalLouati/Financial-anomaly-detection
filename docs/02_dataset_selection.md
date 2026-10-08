# Dataset Selection and Validation

## 1. Purpose

The quality and relevance of the dataset are critical to the development of the Financial Anomaly Detection and AML Investigation System.

Rather than selecting a dataset only because it is publicly available or commonly used, the dataset selection process is based on the functional and technical requirements defined for the project.

The objective of this document is to:

- define the data requirements of the system;
- evaluate potential datasets;
- justify the selected dataset;
- identify its expected strengths and limitations;
- define the validation process that will be performed before development;
- document the final validation results once data profiling is completed.


## 2. Data Requirements

To support the objectives of the project, the selected dataset must provide enough information to analyse financial activity at transaction, behavioural, temporal, and network levels.

The dataset should ideally contain:

- sender account identifiers;
- receiver account identifiers;
- transaction amounts;
- transaction timestamps;
- currency information;
- payment or transaction types;
- sufficient transaction history to construct behavioural baselines;
- relationships between multiple accounts for graph analysis;
- enough transaction volume to analyse repeated and temporal patterns;
- labels indicating suspicious or laundering activity when available.

The dataset should also allow the construction of derived variables through feature engineering.


## 3. Required Analytical Capabilities

The selected dataset should support, directly or through feature engineering, the investigation of the following anomaly categories:

1. unusual transaction amounts;
2. repeated identical or round amounts;
3. abnormal transaction velocity;
4. behavioural deviations;
5. rapid inflow and outflow of funds;
6. unusual counterparties;
7. collector and dispersion patterns;
8. structuring patterns;
9. circular transaction flows;
10. machine-learning-based anomalies.

The dataset must therefore contain both transaction-level information and relationships between accounts.


## 4. Candidate Datasets

Three datasets were considered for the project:

- IBM Transactions for Anti-Money Laundering (AML-Data);
- PaySim;
- AMLSim.

These datasets were considered because they provide synthetic financial transaction data that can be used to study financial crime, fraud, or anomalous transaction behaviour.


## 5. Dataset Comparison

The datasets are evaluated according to the requirements of the project.

| Criterion | IBM AML-Data | PaySim | AMLSim |
|---|---|---|---|
| Financial transactions | Yes | Yes | Yes |
| Sender and receiver information | Yes | Yes | Yes |
| Transaction amounts | Yes | Yes | Yes |
| Temporal information | Yes | Yes | Yes |
| Transaction/payment types | Yes | Yes | Yes |
| Multi-currency information | Yes | Limited / dataset-dependent | Configuration-dependent |
| Account-to-account relationships | Yes | Yes | Yes |
| Suitable for behavioural analysis | Yes | Yes | Yes |
| Suitable for graph analysis | Yes | Possible | Yes |
| AML-oriented scenarios | Yes | Primarily fraud-oriented | Yes |
| Labels available | Yes | Yes, fraud labels | Scenario-dependent |
| Suitable for unsupervised anomaly detection | Yes | Yes | Yes |

This comparison is an initial assessment based on the documented structure and intended use of the candidate datasets.

The actual suitability of the selected dataset will be verified through data profiling before model development.


## 6. Preliminary Dataset Selection

### Selected Candidate

**IBM Transactions for Anti-Money Laundering (AML-Data)**

IBM AML-Data is selected as the primary candidate dataset for the first version of the project.

The dataset is particularly relevant because it contains transaction relationships between sending and receiving accounts and was designed for research involving anti-money-laundering transaction patterns.

It also provides information that can potentially support:

- temporal analysis;
- transaction amount analysis;
- account interaction analysis;
- behavioural feature engineering;
- network construction;
- graph analytics;
- supervised evaluation using laundering labels;
- unsupervised anomaly detection.

The availability of sender and receiver information is particularly important because the project is designed to analyse not only individual transactions but also financial relationships and transaction networks.


## 7. Expected IBM AML-Data Structure

The transaction dataset is expected to provide information including:

- transaction timestamp;
- sending bank;
- sending account;
- receiving bank;
- receiving account;
- amount paid;
- payment currency;
- amount received;
- receiving currency;
- payment format;
- laundering label.

These fields should provide the foundation required for transaction-level, temporal, behavioural, and network analysis.

However, their presence and quality will be verified programmatically during the data profiling phase.


## 8. Why IBM AML-Data Fits the Project

### 8.1 Transaction-Level Analysis

Transaction amounts and timestamps can be used to analyse unusual transaction values and transaction frequency.

### 8.2 Behavioural Analysis

Historical transactions associated with the same account can potentially be aggregated to construct behavioural baselines.

Examples of future features include:

- average transaction amount;
- median transaction amount;
- transaction frequency;
- number of transactions within a time window;
- number of unique counterparties;
- deviation from historical transaction behaviour.


### 8.3 Temporal Analysis

Transaction timestamps can support the creation of time-window features.

Examples include:

- transactions during the last hour;
- transactions during the last 24 hours;
- rapid sequences of transactions;
- rapid inflow followed by outflow.


### 8.4 Network Analysis

Sender and receiver account identifiers allow financial transactions to be represented as a graph.

In this representation:

**Nodes = Accounts**

**Edges = Transactions**

This structure can support the investigation of:

- circular transaction flows;
- collector accounts;
- dispersion patterns;
- unusual account connectivity;
- complex transaction chains.


### 8.5 Machine Learning

The dataset can potentially support both supervised and unsupervised approaches.

The project will initially focus on anomaly detection rather than treating the problem only as binary classification.

Potential approaches may include:

- statistical anomaly detection;
- Isolation Forest;
- clustering;
- supervised classification where appropriate.

Model selection will be performed only after exploratory data analysis and feature engineering.


## 9. Multi-Currency Considerations

The project is designed to support transactions involving different currencies.

Amounts expressed in different currencies must not be compared directly.

For example:

```text
5,000 EUR
5,000 USD
5,000 TND
