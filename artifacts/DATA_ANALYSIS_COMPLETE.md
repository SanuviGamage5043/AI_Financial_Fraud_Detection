
# Financial Fraud Detection Project - Data Analysis Complete

## Dataset Overview
- **Total Transactions:** 6,362,620
- **Time Period:** 1-743 hours (30.9 days)
- **File Size:** 1950.13 MB

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
