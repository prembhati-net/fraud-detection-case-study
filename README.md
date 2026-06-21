# Fraud Detection in Financial Transactions

## Project Overview

This project analyzes over **6.3 million financial transactions** to identify fraudulent activities using machine learning and business-driven feature engineering.

The dataset is highly imbalanced, with fraud accounting for only **0.13% of all transactions**, making traditional accuracy-based evaluation misleading.

The goal was to build an interpretable fraud detection system capable of identifying suspicious transactions while minimizing missed fraud cases.

---

## Business Problem

Financial institutions lose millions every year due to fraudulent transfers and cash withdrawals.

The objective was to:

* Identify key factors driving fraud
* Build a predictive fraud detection model
* Evaluate performance using imbalance-aware metrics
* Recommend practical fraud prevention strategies

---

## Dataset

* Transactions: 6,362,620
* Fraud Cases: ~8,200
* Fraud Rate: 0.13%

Features include:

* Transaction amount
* Transaction type
* Origin account balances
* Destination account balances
* Fraud labels

---

## Key Exploratory Findings

### Fraud Occurs Only In:

* TRANSFER
* CASH_OUT

No fraud transactions were found in:

* CASH_IN
* PAYMENT
* DEBIT

This finding significantly reduced noise and improved model focus.

---

## Feature Engineering

### Error Features

Instead of relying solely on raw balances, two engineered features were created:

errorOrig = oldbalanceOrg - amount - newbalanceOrig

errorDest = oldbalanceDest + amount - newbalanceDest

For legitimate transactions these values should be close to zero.

Fraudulent transactions frequently violate this balance relationship.

### Additional Features

* Transaction Type Encoding
* Origin Account Emptying Indicator
* Balance Consistency Checks

---

## Data Cleaning

### Missing Values

No missing values were present.

Merchant accounts (names beginning with M) contain zero destination balances by design and were retained.

### Outliers

Large transaction amounts were intentionally preserved.

In fraud detection, extreme values often represent valuable fraud signals rather than data quality issues.

### Multicollinearity

Strong correlations existed among balance variables.

Feature engineering was used to reduce redundancy while preserving information.

---

## Models Evaluated

### Logistic Regression

Used as a baseline model.

### Random Forest Classifier

Configuration:

* 100 Trees
* class_weight='balanced'
* Stratified 70/30 Train-Test Split

Random Forest was selected due to its ability to capture non-linear fraud patterns and handle feature interactions effectively.

---

## Evaluation Metrics

Accuracy was not used as the primary metric due to severe class imbalance.

Metrics considered:

* Recall
* Precision
* F1 Score
* ROC-AUC
* Precision-Recall Curve
* Confusion Matrix

### Results

* ROC-AUC > 0.97
* Strong fraud detection recall
* Significant improvement over baseline Logistic Regression

---

## Most Important Fraud Predictors

1. errorOrig
2. errorDest
3. amount
4. newbalanceOrig
5. oldbalanceOrg
6. transaction type

The engineered balance consistency features emerged as the strongest fraud indicators.

---

## Business Recommendations

### Real-Time Fraud Scoring

Score all TRANSFER and CASH_OUT transactions before approval.

### Two-Factor Authentication

Require OTP or biometric verification for high-risk transfers.

### Velocity Monitoring

Flag accounts making multiple large transactions within short periods.

### Account Drain Detection

Monitor transactions that reduce account balances to near zero.

### Mule Account Monitoring

Identify destination accounts receiving suspicious transfers and immediate cash withdrawals.

---

## Measuring Success

Track:

* Fraud Rate
* Fraud Loss Amount
* False Positive Rate
* Detection Time
* Recall and Precision

Conduct A/B testing to compare performance against existing fraud controls.

---

## Tech Stack

* Python
* Pandas
* NumPy
* Matplotlib
* Seaborn
* Scikit-Learn
* Google Colab

---

## Author

Prem Bhati

Data Analyst | Python | SQL | Machine Learning | Power BI
