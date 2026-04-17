
# Financial Fraud Detection Project - Data Analysis

## Dataset Overview
- **Total Transactions:** 6,362,620
- **Time Period:** 1-743 hours (30.9 days)
- **File Size:** 761.59 MB

## Critical Findings
1. **Fraud Rate:** 0.1291% (8,213 frauds)
2. **Imbalance Ratio:** 1:773.70
3. **Fraud Only In:** CASH_OUT (4,116) and TRANSFER (4,097)
4. **Amount Pattern:** Fraud amounts are 8.2x higher
5. **Destination Pattern:** 100% of frauds go to customer accounts (never merchants)
6. **User Pattern:** Each fraudster has exactly 1 transaction (no history)

## Files Created
- `analysis_summary.json` - Complete analysis results
- Raw data saved to: `artifacts/raw/Synthetic_Financial_datasets_log.csv`

**Important Note:** Since fraudsters have no transaction history, use GLOBAL time-based sequences, not per-user sequences!


## Data Preprocessing Summary

### Steps Performed
- Loaded dataset (6.36M rows, 11 columns)
- Dropped unnecessary balance columns
- Removed duplicates (none found)
- Feature Engineering:
  - Customer transaction count per sender
  - Destination fraud rate encoding
  - Temporal features (hour_of_cycle, day_of_cycle)
  - One-time transaction indicators
  - High-risk transaction interactions
- One-hot encoded transaction type
- Normalized `amount`, `step`, and engineered features
- Handled class imbalance using **class weights**
- Removed `isFlaggedFraud` to prevent data leakage
- Validated train/test separation (no customer overlap)
- Split data into Train (70%), Validation (15%), Test (15%)

### Features Used in Model (18 total)
- step, amount (normalized)
- sender_transaction_count
- is_first_transaction
- dest_fraud_rate
- hour_of_cycle, day_of_cycle
- high_amount_to_fraud_dest
- type_CASH_IN, type_CASH_OUT, type_DEBIT, type_PAYMENT, type_TRANSFER
- type_*_avg_deviation features

### Correlation Insights
- Most predictive feature: dest_fraud_rate (correlation: 0.7061)
- 3 features with |correlation| > 0.1
- 5 features with |correlation| > 0.05

### Important Notes
- Data Leakage Prevention: `isFlaggedFraud` excluded (bank's output, not model input)
- Customer Separation: No fraudster appears in both train and test
- Temporal Patterns: Captured through engineered features
- Behavioral Features: Customer transaction history and destination risk rates

### Saved Files
- `cleaned_data.parquet` - Main processed dataset
- `cleaned_data_with_identifiers.csv` - CSV copy for inspection
- `class_weights.json` - Class weight mapping
- `scaler.pkl` - Feature scaling transformer
- `feature_names.txt` - List of model features
