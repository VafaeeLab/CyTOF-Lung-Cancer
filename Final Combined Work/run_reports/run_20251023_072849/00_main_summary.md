# Biomarker Discovery: Main Summary Report

---
- **Methodology**: Nested Cross-Validation (40 outer folds) with stratified bootstrapped inner stability (10 resamples)
- **Key Finding**: Performance metrics reported here are unbiased estimates of generalization performance.
- **Best Unbiased ROC-AUC**: 0.7388

## Top 10 Performing Model Combinations (Mean Unbiased Nested CV Performance)

|    | signature_method       | classifier   |   roc_auc_mean |   roc_auc_std | roc_auc_ci   |   auprc_mean |   auprc_std | auprc_ci    |   accuracy_mean |   accuracy_std |   precision_mean |   precision_std |   recall_mean |   recall_std |   specificity_mean |   specificity_std |   f1_score_mean |   f1_score_std | f1_score_ci   |
|---:|:-----------------------|:-------------|---------------:|--------------:|:-------------|-------------:|------------:|:------------|----------------:|---------------:|-----------------:|----------------:|--------------:|-------------:|-------------------:|------------------:|----------------:|---------------:|:--------------|
|  0 | FDR (p < 0.1)_t40      | RandomForest |       0.738766 |     0.103033  | 0.706-0.772  |     0.696515 |   0.0961415 | 0.666-0.727 |        0.665217 |      0.100418  |         0.650117 |        0.138473 |        0.61   |     0.14641  |           0.710256 |          0.156017 |        0.618394 |       0.111974 | 0.583-0.654   |
|  1 | FDR (p < 0.1)_t50      | RandomForest |       0.725024 |     0.103661  | 0.692-0.758  |     0.68006  |   0.092858  | 0.650-0.710 |        0.66749  |      0.0999787 |         0.644042 |        0.121727 |        0.6275 |     0.137724 |           0.700321 |          0.145256 |        0.627258 |       0.108746 | 0.592-0.662   |
|  2 | RFE (RandomForest)_t50 | XGBoost      |       0.717901 |     0.104802  | 0.684-0.751  |     0.682792 |   0.0937667 | 0.653-0.713 |        0.653953 |      0.094612  |         0.625747 |        0.119668 |        0.6025 |     0.144093 |           0.696314 |          0.128695 |        0.606288 |       0.114819 | 0.570-0.643   |
|  3 | RF_Importance_t40      | XGBoost      |       0.716218 |     0.110242  | 0.681-0.751  |     0.686992 |   0.10473   | 0.653-0.720 |        0.673123 |      0.116574  |         0.64305  |        0.149721 |        0.645  |     0.170895 |           0.696314 |          0.145712 |        0.635052 |       0.140173 | 0.590-0.680   |
|  4 | RF_Importance_t60      | XGBoost      |       0.715016 |     0.0972393 | 0.684-0.746  |     0.684788 |   0.0991994 | 0.653-0.717 |        0.651877 |      0.095769  |         0.620774 |        0.127193 |        0.61   |     0.149872 |           0.687019 |          0.129561 |        0.607526 |       0.119448 | 0.569-0.646   |
|  5 | RF_Importance_t50      | RandomForest |       0.714295 |     0.0918824 | 0.685-0.744  |     0.668234 |   0.081543  | 0.642-0.694 |        0.656423 |      0.0927246 |         0.636998 |        0.116685 |        0.575  |     0.158114 |           0.723397 |          0.131062 |        0.593533 |       0.123567 | 0.554-0.633   |
|  6 | RFE (RandomForest)_t60 | XGBoost      |       0.713814 |     0.100097  | 0.682-0.746  |     0.683987 |   0.0949624 | 0.654-0.714 |        0.66413  |      0.0951125 |         0.638896 |        0.125646 |        0.6175 |     0.137538 |           0.702404 |          0.126691 |        0.620713 |       0.108303 | 0.586-0.655   |
|  7 | FDR (p < 0.05)_t40     | RandomForest |       0.712212 |     0.0995974 | 0.680-0.744  |     0.668574 |   0.100091  | 0.637-0.701 |        0.661709 |      0.0873459 |         0.64417  |        0.121153 |        0.6125 |     0.141761 |           0.702244 |          0.140209 |        0.614683 |       0.106883 | 0.581-0.649   |
|  8 | RFE (RandomForest)_t40 | XGBoost      |       0.710433 |     0.10436   | 0.677-0.744  |     0.684313 |   0.096313  | 0.654-0.715 |        0.656126 |      0.0946397 |         0.630966 |        0.131096 |        0.595  |     0.150128 |           0.70609  |          0.128677 |        0.603945 |       0.120776 | 0.565-0.643   |
|  9 | XGB_Importance_t50     | RandomForest |       0.709607 |     0.109168  | 0.675-0.745  |     0.677667 |   0.106582  | 0.644-0.712 |        0.663982 |      0.0914347 |         0.647679 |        0.123432 |        0.605  |     0.14841  |           0.712821 |          0.145274 |        0.613859 |       0.10634  | 0.580-0.648   |

## Feature Selection Method Signatures Summary

### Understanding Method Names and Thresholds

**Method Naming Convention**:

- **Base Method**: The underlying feature selection algorithm (e.g., `SVM_RBF_Permutation_Top10%`)
- **Threshold Suffix**: Stability filtering applied (e.g., `_t40`, `_t50`, `_t60`, `_t70`, `_t80`)

**How Thresholds Work**:

1. **Feature Selection**: The base method selects features from each bootstrap sample
2. **Frequency Counting**: Features are counted across all bootstrap samples
3. **Threshold Filtering**: Only features meeting the stability threshold are kept:
   - `_t40`: Keep features selected in ≥40% of bootstrap samples
   - `_t50`: Keep features selected in ≥50% of bootstrap samples
   - `_t60`: Keep features selected in ≥60% of bootstrap samples
   - `_t70`: Keep features selected in ≥70% of bootstrap samples
   - `_t80`: Keep features selected in ≥80% of bootstrap samples

**Why Different Thresholds Produce Different Results**:

The same base method (e.g., `SVM_RBF_Permutation_Top10%`) can produce different final feature sets because bootstrap resampling creates variability in feature selection. Higher thresholds (e.g., `_t80`) result in fewer but more stable features, while lower thresholds (e.g., `_t40`) include more features but with lower stability.

---

### Signature Discovery Across All Folds

| Method | Signatures Found | Total Features | Avg Features/Signature |
|--------|------------------|----------------|------------------------|
| All Features (Baseline)_t40 | 40 | 166 | 4.2 |
| All Features (Baseline)_t50 | 40 | 166 | 4.2 |
| All Features (Baseline)_t60 | 40 | 166 | 4.2 |
| All Features (Baseline)_t70 | 40 | 166 | 4.2 |
| All Features (Baseline)_t80 | 40 | 166 | 4.2 |
| ElasticNet_Lenient_t40 | 40 | 104 | 2.6 |
| ElasticNet_Lenient_t50 | 40 | 82 | 2.0 |
| ElasticNet_Lenient_t60 | 40 | 54 | 1.4 |
| ElasticNet_Lenient_t70 | 39 | 35 | 0.9 |
| ElasticNet_Lenient_t80 | 32 | 19 | 0.6 |
| ElasticNet_RFE_t40 | 40 | 85 | 2.1 |
| ElasticNet_RFE_t50 | 40 | 62 | 1.6 |
| ElasticNet_RFE_t60 | 39 | 38 | 1.0 |
| ElasticNet_RFE_t70 | 36 | 24 | 0.7 |
| ElasticNet_RFE_t80 | 26 | 14 | 0.5 |
| ElasticNet_Strict_t40 | 40 | 45 | 1.1 |
| ElasticNet_Strict_t50 | 38 | 31 | 0.8 |
| ElasticNet_Strict_t60 | 31 | 17 | 0.5 |
| ElasticNet_Strict_t70 | 20 | 9 | 0.5 |
| ElasticNet_Strict_t80 | 9 | 4 | 0.4 |
| FDR (p < 0.01)_t40 | 36 | 39 | 1.1 |
| FDR (p < 0.01)_t50 | 27 | 29 | 1.1 |
| FDR (p < 0.01)_t60 | 20 | 21 | 1.1 |
| FDR (p < 0.01)_t70 | 13 | 15 | 1.2 |
| FDR (p < 0.01)_t80 | 5 | 11 | 2.2 |
| FDR (p < 0.05)_t40 | 40 | 81 | 2.0 |
| FDR (p < 0.05)_t50 | 40 | 60 | 1.5 |
| FDR (p < 0.05)_t60 | 36 | 50 | 1.4 |
| FDR (p < 0.05)_t70 | 31 | 39 | 1.3 |
| FDR (p < 0.05)_t80 | 29 | 32 | 1.1 |
| FDR (p < 0.1)_t40 | 40 | 103 | 2.6 |
| FDR (p < 0.1)_t50 | 40 | 85 | 2.1 |
| FDR (p < 0.1)_t60 | 40 | 70 | 1.8 |
| FDR (p < 0.1)_t70 | 38 | 54 | 1.4 |
| FDR (p < 0.1)_t80 | 33 | 43 | 1.3 |
| LASSO_Lenient_t40 | 40 | 90 | 2.2 |
| LASSO_Lenient_t50 | 40 | 59 | 1.5 |
| LASSO_Lenient_t60 | 40 | 40 | 1.0 |
| LASSO_Lenient_t70 | 33 | 24 | 0.7 |
| LASSO_Lenient_t80 | 24 | 12 | 0.5 |
| LASSO_RFE_t40 | 40 | 72 | 1.8 |
| LASSO_RFE_t50 | 40 | 47 | 1.2 |
| LASSO_RFE_t60 | 40 | 28 | 0.7 |
| LASSO_RFE_t70 | 31 | 18 | 0.6 |
| LASSO_RFE_t80 | 21 | 9 | 0.4 |
| LASSO_Strict_t40 | 40 | 38 | 0.9 |
| LASSO_Strict_t50 | 32 | 20 | 0.6 |
| LASSO_Strict_t60 | 22 | 11 | 0.5 |
| LASSO_Strict_t70 | 13 | 5 | 0.4 |
| LASSO_Strict_t80 | 5 | 3 | 0.6 |
| LogisticRegression_Permutation_AboveMean_t40 | 31 | 25 | 0.8 |
| LogisticRegression_Permutation_AboveMean_t50 | 26 | 16 | 0.6 |
| LogisticRegression_Permutation_AboveMean_t60 | 14 | 10 | 0.7 |
| LogisticRegression_Permutation_AboveMean_t70 | 10 | 7 | 0.7 |
| LogisticRegression_Permutation_AboveMean_t80 | 3 | 3 | 1.0 |
| LogisticRegression_Permutation_Top10%_t40 | 40 | 36 | 0.9 |
| LogisticRegression_Permutation_Top10%_t50 | 40 | 29 | 0.7 |
| LogisticRegression_Permutation_Top10%_t60 | 40 | 26 | 0.7 |
| LogisticRegression_Permutation_Top10%_t70 | 40 | 23 | 0.6 |
| LogisticRegression_Permutation_Top10%_t80 | 39 | 19 | 0.5 |
| Mutual Information (Top 10%)_t40 | 40 | 88 | 2.2 |
| Mutual Information (Top 10%)_t50 | 40 | 56 | 1.4 |
| Mutual Information (Top 10%)_t60 | 33 | 32 | 1.0 |
| Mutual Information (Top 10%)_t70 | 22 | 16 | 0.7 |
| Mutual Information (Top 10%)_t80 | 6 | 4 | 0.7 |
| NaiveBayes_Permutation_AboveMean_t40 | 40 | 165 | 4.1 |
| NaiveBayes_Permutation_AboveMean_t50 | 40 | 159 | 4.0 |
| NaiveBayes_Permutation_AboveMean_t60 | 40 | 141 | 3.5 |
| NaiveBayes_Permutation_AboveMean_t70 | 40 | 111 | 2.8 |
| NaiveBayes_Permutation_AboveMean_t80 | 40 | 68 | 1.7 |
| NaiveBayes_Permutation_Top10%_t40 | 40 | 68 | 1.7 |
| NaiveBayes_Permutation_Top10%_t50 | 40 | 42 | 1.1 |
| NaiveBayes_Permutation_Top10%_t60 | 40 | 34 | 0.8 |
| NaiveBayes_Permutation_Top10%_t70 | 36 | 22 | 0.6 |
| NaiveBayes_Permutation_Top10%_t80 | 25 | 15 | 0.6 |
| RFE (RandomForest)_t40 | 40 | 166 | 4.2 |
| RFE (RandomForest)_t50 | 40 | 166 | 4.2 |
| RFE (RandomForest)_t60 | 40 | 166 | 4.2 |
| RFE (RandomForest)_t70 | 40 | 163 | 4.1 |
| RFE (RandomForest)_t80 | 40 | 163 | 4.1 |
| RF_Importance_t40 | 40 | 165 | 4.1 |
| RF_Importance_t50 | 40 | 155 | 3.9 |
| RF_Importance_t60 | 40 | 130 | 3.2 |
| RF_Importance_t70 | 40 | 92 | 2.3 |
| RF_Importance_t80 | 40 | 66 | 1.6 |
| RandomForest_Permutation_AboveMean_t40 | 18 | 32 | 1.8 |
| RandomForest_Permutation_AboveMean_t50 | 2 | 4 | 2.0 |
| RandomForest_Permutation_AboveMean_t60 | 1 | 3 | 3.0 |
| RandomForest_Permutation_Top10%_t40 | 40 | 30 | 0.8 |
| RandomForest_Permutation_Top10%_t50 | 40 | 16 | 0.4 |
| RandomForest_Permutation_Top10%_t60 | 34 | 13 | 0.4 |
| RandomForest_Permutation_Top10%_t70 | 29 | 11 | 0.4 |
| RandomForest_Permutation_Top10%_t80 | 21 | 11 | 0.5 |
| Ridge_Strict_t40 | 40 | 160 | 4.0 |
| Ridge_Strict_t50 | 40 | 155 | 3.9 |
| Ridge_Strict_t60 | 40 | 150 | 3.8 |
| Ridge_Strict_t70 | 40 | 136 | 3.4 |
| Ridge_Strict_t80 | 40 | 115 | 2.9 |
| SVM_RBF_Permutation_AboveMean_t40 | 38 | 166 | 4.4 |
| SVM_RBF_Permutation_AboveMean_t50 | 35 | 160 | 4.6 |
| SVM_RBF_Permutation_AboveMean_t60 | 31 | 143 | 4.6 |
| SVM_RBF_Permutation_AboveMean_t70 | 15 | 67 | 4.5 |
| SVM_RBF_Permutation_AboveMean_t80 | 8 | 24 | 3.0 |
| SVM_RBF_Permutation_Top10%_t40 | 40 | 48 | 1.2 |
| SVM_RBF_Permutation_Top10%_t50 | 35 | 30 | 0.9 |
| SVM_RBF_Permutation_Top10%_t60 | 23 | 22 | 1.0 |
| SVM_RBF_Permutation_Top10%_t70 | 9 | 12 | 1.3 |
| SVM_RBF_Permutation_Top10%_t80 | 3 | 4 | 1.3 |
| XGB_Importance_t40 | 40 | 126 | 3.1 |
| XGB_Importance_t50 | 40 | 82 | 2.0 |
| XGB_Importance_t60 | 40 | 44 | 1.1 |
| XGB_Importance_t70 | 40 | 25 | 0.6 |
| XGB_Importance_t80 | 36 | 13 | 0.4 |
| XGBoost_Permutation_AboveMean_t40 | 23 | 6 | 0.3 |
| XGBoost_Permutation_AboveMean_t50 | 17 | 6 | 0.4 |
| XGBoost_Permutation_AboveMean_t60 | 10 | 4 | 0.4 |
| XGBoost_Permutation_AboveMean_t70 | 3 | 2 | 0.7 |
| XGBoost_Permutation_AboveMean_t80 | 2 | 1 | 0.5 |
| XGBoost_Permutation_Top10%_t40 | 40 | 22 | 0.6 |
| XGBoost_Permutation_Top10%_t50 | 40 | 21 | 0.5 |
| XGBoost_Permutation_Top10%_t60 | 40 | 20 | 0.5 |
| XGBoost_Permutation_Top10%_t70 | 40 | 16 | 0.4 |
| XGBoost_Permutation_Top10%_t80 | 40 | 15 | 0.4 |
| mRMR (Top 10%)_t40 | 40 | 78 | 1.9 |
| mRMR (Top 10%)_t50 | 40 | 53 | 1.3 |
| mRMR (Top 10%)_t60 | 40 | 38 | 0.9 |
| mRMR (Top 10%)_t70 | 39 | 27 | 0.7 |
| mRMR (Top 10%)_t80 | 27 | 22 | 0.8 |

### Threshold-Specific Signature Breakdown

This section shows which signatures were discovered at each stability threshold. **Key Point**: The same base method (e.g., `SVM_RBF_Permutation_Top10%`) appears at multiple thresholds because each threshold represents a different stability filter applied to the same underlying feature selection process.

**Example**: If `SVM_RBF_Permutation_Top10%` appears at both 40% and 50% thresholds, it means:
- At 40% threshold: Features selected in ≥40% of bootstrap samples are kept
- At 50% threshold: Features selected in ≥50% of bootstrap samples are kept
- The 50% threshold will have fewer features than the 40% threshold

#### Threshold 40%

| Base Method | Signatures Found | Total Features | Avg Features/Signature |
|-------------|------------------|----------------|------------------------|
| All Features (Baseline) | 40 | 166 | 4.2 |
| ElasticNet_Lenient | 40 | 104 | 2.6 |
| ElasticNet_RFE | 40 | 85 | 2.1 |
| ElasticNet_Strict | 40 | 45 | 1.1 |
| FDR (p < 0.01) | 36 | 39 | 1.1 |
| FDR (p < 0.05) | 40 | 81 | 2.0 |
| FDR (p < 0.1) | 40 | 103 | 2.6 |
| LASSO_Lenient | 40 | 90 | 2.2 |
| LASSO_RFE | 40 | 72 | 1.8 |
| LASSO_Strict | 40 | 38 | 0.9 |
| LogisticRegression_Permutation_AboveMean | 31 | 25 | 0.8 |
| LogisticRegression_Permutation_Top10% | 40 | 36 | 0.9 |
| Mutual Information (Top 10%) | 40 | 88 | 2.2 |
| NaiveBayes_Permutation_AboveMean | 40 | 165 | 4.1 |
| NaiveBayes_Permutation_Top10% | 40 | 68 | 1.7 |
| RFE (RandomForest) | 40 | 166 | 4.2 |
| RF_Importance | 40 | 165 | 4.1 |
| RandomForest_Permutation_AboveMean | 18 | 32 | 1.8 |
| RandomForest_Permutation_Top10% | 40 | 30 | 0.8 |
| Ridge_Strict | 40 | 160 | 4.0 |
| SVM_RBF_Permutation_AboveMean | 38 | 166 | 4.4 |
| SVM_RBF_Permutation_Top10% | 40 | 48 | 1.2 |
| XGB_Importance | 40 | 126 | 3.1 |
| XGBoost_Permutation_AboveMean | 23 | 6 | 0.3 |
| XGBoost_Permutation_Top10% | 40 | 22 | 0.6 |
| mRMR (Top 10%) | 40 | 78 | 1.9 |

**Total signatures at 40% threshold**: 986

#### Threshold 50%

| Base Method | Signatures Found | Total Features | Avg Features/Signature |
|-------------|------------------|----------------|------------------------|
| All Features (Baseline) | 40 | 166 | 4.2 |
| ElasticNet_Lenient | 40 | 82 | 2.0 |
| ElasticNet_RFE | 40 | 62 | 1.6 |
| ElasticNet_Strict | 38 | 31 | 0.8 |
| FDR (p < 0.01) | 27 | 29 | 1.1 |
| FDR (p < 0.05) | 40 | 60 | 1.5 |
| FDR (p < 0.1) | 40 | 85 | 2.1 |
| LASSO_Lenient | 40 | 59 | 1.5 |
| LASSO_RFE | 40 | 47 | 1.2 |
| LASSO_Strict | 32 | 20 | 0.6 |
| LogisticRegression_Permutation_AboveMean | 26 | 16 | 0.6 |
| LogisticRegression_Permutation_Top10% | 40 | 29 | 0.7 |
| Mutual Information (Top 10%) | 40 | 56 | 1.4 |
| NaiveBayes_Permutation_AboveMean | 40 | 159 | 4.0 |
| NaiveBayes_Permutation_Top10% | 40 | 42 | 1.1 |
| RFE (RandomForest) | 40 | 166 | 4.2 |
| RF_Importance | 40 | 155 | 3.9 |
| RandomForest_Permutation_AboveMean | 2 | 4 | 2.0 |
| RandomForest_Permutation_Top10% | 40 | 16 | 0.4 |
| Ridge_Strict | 40 | 155 | 3.9 |
| SVM_RBF_Permutation_AboveMean | 35 | 160 | 4.6 |
| SVM_RBF_Permutation_Top10% | 35 | 30 | 0.9 |
| XGB_Importance | 40 | 82 | 2.0 |
| XGBoost_Permutation_AboveMean | 17 | 6 | 0.4 |
| XGBoost_Permutation_Top10% | 40 | 21 | 0.5 |
| mRMR (Top 10%) | 40 | 53 | 1.3 |

**Total signatures at 50% threshold**: 932

#### Threshold 60%

| Base Method | Signatures Found | Total Features | Avg Features/Signature |
|-------------|------------------|----------------|------------------------|
| All Features (Baseline) | 40 | 166 | 4.2 |
| ElasticNet_Lenient | 40 | 54 | 1.4 |
| ElasticNet_RFE | 39 | 38 | 1.0 |
| ElasticNet_Strict | 31 | 17 | 0.5 |
| FDR (p < 0.01) | 20 | 21 | 1.1 |
| FDR (p < 0.05) | 36 | 50 | 1.4 |
| FDR (p < 0.1) | 40 | 70 | 1.8 |
| LASSO_Lenient | 40 | 40 | 1.0 |
| LASSO_RFE | 40 | 28 | 0.7 |
| LASSO_Strict | 22 | 11 | 0.5 |
| LogisticRegression_Permutation_AboveMean | 14 | 10 | 0.7 |
| LogisticRegression_Permutation_Top10% | 40 | 26 | 0.7 |
| Mutual Information (Top 10%) | 33 | 32 | 1.0 |
| NaiveBayes_Permutation_AboveMean | 40 | 141 | 3.5 |
| NaiveBayes_Permutation_Top10% | 40 | 34 | 0.8 |
| RFE (RandomForest) | 40 | 166 | 4.2 |
| RF_Importance | 40 | 130 | 3.2 |
| RandomForest_Permutation_AboveMean | 1 | 3 | 3.0 |
| RandomForest_Permutation_Top10% | 34 | 13 | 0.4 |
| Ridge_Strict | 40 | 150 | 3.8 |
| SVM_RBF_Permutation_AboveMean | 31 | 143 | 4.6 |
| SVM_RBF_Permutation_Top10% | 23 | 22 | 1.0 |
| XGB_Importance | 40 | 44 | 1.1 |
| XGBoost_Permutation_AboveMean | 10 | 4 | 0.4 |
| XGBoost_Permutation_Top10% | 40 | 20 | 0.5 |
| mRMR (Top 10%) | 40 | 38 | 0.9 |

**Total signatures at 60% threshold**: 854

#### Threshold 70%

| Base Method | Signatures Found | Total Features | Avg Features/Signature |
|-------------|------------------|----------------|------------------------|
| All Features (Baseline) | 40 | 166 | 4.2 |
| ElasticNet_Lenient | 39 | 35 | 0.9 |
| ElasticNet_RFE | 36 | 24 | 0.7 |
| ElasticNet_Strict | 20 | 9 | 0.5 |
| FDR (p < 0.01) | 13 | 15 | 1.2 |
| FDR (p < 0.05) | 31 | 39 | 1.3 |
| FDR (p < 0.1) | 38 | 54 | 1.4 |
| LASSO_Lenient | 33 | 24 | 0.7 |
| LASSO_RFE | 31 | 18 | 0.6 |
| LASSO_Strict | 13 | 5 | 0.4 |
| LogisticRegression_Permutation_AboveMean | 10 | 7 | 0.7 |
| LogisticRegression_Permutation_Top10% | 40 | 23 | 0.6 |
| Mutual Information (Top 10%) | 22 | 16 | 0.7 |
| NaiveBayes_Permutation_AboveMean | 40 | 111 | 2.8 |
| NaiveBayes_Permutation_Top10% | 36 | 22 | 0.6 |
| RFE (RandomForest) | 40 | 163 | 4.1 |
| RF_Importance | 40 | 92 | 2.3 |
| RandomForest_Permutation_Top10% | 29 | 11 | 0.4 |
| Ridge_Strict | 40 | 136 | 3.4 |
| SVM_RBF_Permutation_AboveMean | 15 | 67 | 4.5 |
| SVM_RBF_Permutation_Top10% | 9 | 12 | 1.3 |
| XGB_Importance | 40 | 25 | 0.6 |
| XGBoost_Permutation_AboveMean | 3 | 2 | 0.7 |
| XGBoost_Permutation_Top10% | 40 | 16 | 0.4 |
| mRMR (Top 10%) | 39 | 27 | 0.7 |

**Total signatures at 70% threshold**: 737

#### Threshold 80%

| Base Method | Signatures Found | Total Features | Avg Features/Signature |
|-------------|------------------|----------------|------------------------|
| All Features (Baseline) | 40 | 166 | 4.2 |
| ElasticNet_Lenient | 32 | 19 | 0.6 |
| ElasticNet_RFE | 26 | 14 | 0.5 |
| ElasticNet_Strict | 9 | 4 | 0.4 |
| FDR (p < 0.01) | 5 | 11 | 2.2 |
| FDR (p < 0.05) | 29 | 32 | 1.1 |
| FDR (p < 0.1) | 33 | 43 | 1.3 |
| LASSO_Lenient | 24 | 12 | 0.5 |
| LASSO_RFE | 21 | 9 | 0.4 |
| LASSO_Strict | 5 | 3 | 0.6 |
| LogisticRegression_Permutation_AboveMean | 3 | 3 | 1.0 |
| LogisticRegression_Permutation_Top10% | 39 | 19 | 0.5 |
| Mutual Information (Top 10%) | 6 | 4 | 0.7 |
| NaiveBayes_Permutation_AboveMean | 40 | 68 | 1.7 |
| NaiveBayes_Permutation_Top10% | 25 | 15 | 0.6 |
| RFE (RandomForest) | 40 | 163 | 4.1 |
| RF_Importance | 40 | 66 | 1.6 |
| RandomForest_Permutation_Top10% | 21 | 11 | 0.5 |
| Ridge_Strict | 40 | 115 | 2.9 |
| SVM_RBF_Permutation_AboveMean | 8 | 24 | 3.0 |
| SVM_RBF_Permutation_Top10% | 3 | 4 | 1.3 |
| XGB_Importance | 36 | 13 | 0.4 |
| XGBoost_Permutation_AboveMean | 2 | 1 | 0.5 |
| XGBoost_Permutation_Top10% | 40 | 15 | 0.4 |
| mRMR (Top 10%) | 27 | 22 | 0.8 |

**Total signatures at 80% threshold**: 594


### Feature Selection Frequency by Method (Stable signatures only)

#### All Features (Baseline)_t40

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD3pos_total | 100.0% |
| CD4 Tconv_total | 100.0% |
| CD4 Tconv mem_total | 100.0% |
| Tconv memCCR4_total | 100.0% |
| Tconv memCCR5_total | 100.0% |
| Tconv memCCR6_total | 100.0% |
| Tconv memCD27_total | 100.0% |
| Tconv memCD56_total | 100.0% |
| Tconv memCXCR3_total | 100.0% |
| Tconv memDR_total | 100.0% |
| Tconv memintB7_total | 100.0% |
| Tconv memKi67_total | 100.0% |
| Tconv memPD1_total | 100.0% |
| Tconv memTIGIT_total | 100.0% |
| Tconv naive_total | 100.0% |
| CD4 Treg_total | 100.0% |
| Treg naive_total | 100.0% |
| Treg memory_total | 100.0% |
| CD4neg_total | 100.0% |
| CD3hi_total | 100.0% |
| CD8pos_total | 100.0% |
| CD8 RA_total | 100.0% |
| CD8 RA naive_total | 100.0% |
| CD8 RO_total | 100.0% |
| CD8 RO CCR4_total | 100.0% |
| CD8 RO CCR5_total | 100.0% |
| CD8 RO CCR6_total | 100.0% |
| CD8 RO CD27_total | 100.0% |
| CD8 RO CD56_total | 100.0% |
| CD8 RO CXCR3_total | 100.0% |
| CD8 RO DR_total | 100.0% |
| CD8 RO intB7_total | 100.0% |
| CD8 RO Ki67_total | 100.0% |
| CD8 RO PD1_total | 100.0% |
| CD8 RO TIGIT_total | 100.0% |
| CD3neg_total | 100.0% |
| nonTnonB_total | 100.0% |
| NK_total | 100.0% |
| NKCD16_total | 100.0% |
| NKCD56hi_total | 100.0% |
| NK Ki67_total | 100.0% |
| myeloid_total | 100.0% |
| CD14mono_total | 100.0% |
| CD16+mono_total | 100.0% |
| CD14+16+mono_total | 100.0% |
| Bcells_total | 100.0% |
| Bcells CD27posIgDneg_total | 100.0% |
| Bcells CD27negIgDneg_total | 100.0% |
| Bcells Ki67_total | 100.0% |
| Bcells memory_total | 100.0% |
| Bcells naive_total | 100.0% |
| CD4 Tconv_CD3 | 100.0% |
| Tconv mem_CD3 | 100.0% |
| Tconv memCCR4_CD3 | 100.0% |
| Tconv memCCR5_CD3 | 100.0% |
| Tconv memCCR6_CD3 | 100.0% |
| Tconv memCD27_CD3 | 100.0% |
| Tconv memCD56_CD3 | 100.0% |
| Tconv memCXCR3_CD3 | 100.0% |
| Tconv memDR_CD3 | 100.0% |
| Tconv memintB7_CD3 | 100.0% |
| Tconv memKi67_CD3 | 100.0% |
| Tconv memPD1_CD3 | 100.0% |
| Tconv memTIGIT_CD3 | 100.0% |
| Tconv naive_CD3 | 100.0% |
| CD4 Treg _CD3 | 100.0% |
| Treg naive_CD3 | 100.0% |
| Treg memory_CD3 | 100.0% |
| CD4neg_CD3 | 100.0% |
| CD3hi_CD3 | 100.0% |
| CD8pos_CD3 | 100.0% |
| CD8 RA_CD3 | 100.0% |
| CD8 RA naive_CD3 | 100.0% |
| CD8 RO_CD3 | 100.0% |
| CD8 ncytotox RO CCR4_CD3 | 100.0% |
| CD8 RO CCR5_CD3 | 100.0% |
| CD8 RO CCR6_CD3 | 100.0% |
| CD8 RO CD27_CD3 | 100.0% |
| CD8 RO CD56_CD3 | 100.0% |
| CD8 RO CXCR3_CD3 | 100.0% |
| CD8 RO DR_CD3 | 100.0% |
| CD8 RO intB7_CD3 | 100.0% |
| CD8  RO Ki67_CD3 | 100.0% |
| CD8 RO PD1_CD3 | 100.0% |
| CD8 RO TIGIT_CD3 | 100.0% |
| CD4 Treg_CD4 | 100.0% |
| Treg naive_CD4 | 100.0% |
| Treg memory_CD4 | 100.0% |
| Tconv mem_Tconv | 100.0% |
| Tconv memCCR4_Tconv | 100.0% |
| Tconv memCCR5_Tconv | 100.0% |
| Tconv memCCR6_Tconv | 100.0% |
| Tconv memCD27_Tconv | 100.0% |
| Tconv memCD56_Tconv | 100.0% |
| Tconv memCXCR3_Tconv | 100.0% |
| Tconv memDR_Tconv | 100.0% |
| Tconv memintB7_Tconv | 100.0% |
| Tconv memKi67_Tconv | 100.0% |
| Tconv memPD1_Tconv | 100.0% |
| Tconv memTIGIT_Tconv | 100.0% |
| Tconv naive_Tconv | 100.0% |
| Tconv memCCR4_mem | 100.0% |
| Tconv memCCR5_mem | 100.0% |
| Tconv memCCR6_mem | 100.0% |
| Tconv memCD27_mem | 100.0% |
| Tconv memCD56_mem | 100.0% |
| Tconv memCXCR3_mem | 100.0% |
| Tconv memDR_mem | 100.0% |
| Tconv memintB7_mem | 100.0% |
| Tconv memKi67_mem | 100.0% |
| Tconv memPD1_mem | 100.0% |
| Tconv memTIGIT_mem | 100.0% |
| CD3hi_CD4neg | 100.0% |
| CD8 RA_CD8 | 100.0% |
| CD8 RA CCR7 naive_CD8 | 100.0% |
| CD8 RO_CD8 | 100.0% |
| CD8 ncytotox RO CCR4_CD8ntox | 100.0% |
| CD8 RO CCR5_CD8 | 100.0% |
| CD8 RO CCR6_CD8 | 100.0% |
| CD8 RO CD27_CD8 | 100.0% |
| CD8 RO CD56_CD8 | 100.0% |
| CD8 RO CXCR3_CD8 | 100.0% |
| CD8 RO DR_CD8 | 100.0% |
| CD8 RO intB7_CD8 | 100.0% |
| CD8 RO Ki67_CD8 | 100.0% |
| CD8 RO PD1_CD8 | 100.0% |
| CD8 RO TIGIT_CD8 | 100.0% |
| CCR4_CD8RO | 100.0% |
| CCR5_CD8RO | 100.0% |
| CCR6_CD8RO | 100.0% |
| CD27_CD8RO | 100.0% |
| CD56_CD8RO | 100.0% |
| CXCR3_CD8RO | 100.0% |
| DR_CD8RO | 100.0% |
| intB7_CD8RO | 100.0% |
| Ki67_CD8RO | 100.0% |
| PD1_CD8RO | 100.0% |
| TIGIT_CD8RO | 100.0% |
| nonTnonB_CD3neg | 100.0% |
| NK_CD3neg | 100.0% |
| NKCD16_CD3neg | 100.0% |
| NKCD56hi_CD3neg | 100.0% |
| NK Ki67_CD3neg | 100.0% |
| myeloid_CD3neg | 100.0% |
| CD14mono_CD3neg | 100.0% |
| CD16mono_CD3neg | 100.0% |
| CD14+16+mono_CD3neg | 100.0% |
| Bcells_CD3neg | 100.0% |
| Bcells Ki67_CD3neg | 100.0% |
| Bcells memory_CD3neg | 100.0% |
| Bcells naive_CD3neg | 100.0% |
| NK_nonTnonB | 100.0% |
| NKCD16_nonTnonB | 100.0% |
| NKCD56hi_nonTnonB | 100.0% |
| NK Ki67_nonTnonB | 100.0% |
| NKCD16_NK | 100.0% |
| NKCD56hi_NK | 100.0% |
| NK Ki67_NK | 100.0% |
| CD14mono_myeloid | 100.0% |
| CD16mono_myeloid | 100.0% |
| CD14+16+mono_myeloid | 100.0% |
| CD27IgD_Bcells | 100.0% |
| CD27negIgDneg_Bcells | 100.0% |
| Ki67_Bcells | 100.0% |
| memory_Bcells | 100.0% |
| naive_Bcells | 100.0% |

**Total features selected by All Features (Baseline)_t40**: 166

#### All Features (Baseline)_t50

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD3pos_total | 100.0% |
| CD4 Tconv_total | 100.0% |
| CD4 Tconv mem_total | 100.0% |
| Tconv memCCR4_total | 100.0% |
| Tconv memCCR5_total | 100.0% |
| Tconv memCCR6_total | 100.0% |
| Tconv memCD27_total | 100.0% |
| Tconv memCD56_total | 100.0% |
| Tconv memCXCR3_total | 100.0% |
| Tconv memDR_total | 100.0% |
| Tconv memintB7_total | 100.0% |
| Tconv memKi67_total | 100.0% |
| Tconv memPD1_total | 100.0% |
| Tconv memTIGIT_total | 100.0% |
| Tconv naive_total | 100.0% |
| CD4 Treg_total | 100.0% |
| Treg naive_total | 100.0% |
| Treg memory_total | 100.0% |
| CD4neg_total | 100.0% |
| CD3hi_total | 100.0% |
| CD8pos_total | 100.0% |
| CD8 RA_total | 100.0% |
| CD8 RA naive_total | 100.0% |
| CD8 RO_total | 100.0% |
| CD8 RO CCR4_total | 100.0% |
| CD8 RO CCR5_total | 100.0% |
| CD8 RO CCR6_total | 100.0% |
| CD8 RO CD27_total | 100.0% |
| CD8 RO CD56_total | 100.0% |
| CD8 RO CXCR3_total | 100.0% |
| CD8 RO DR_total | 100.0% |
| CD8 RO intB7_total | 100.0% |
| CD8 RO Ki67_total | 100.0% |
| CD8 RO PD1_total | 100.0% |
| CD8 RO TIGIT_total | 100.0% |
| CD3neg_total | 100.0% |
| nonTnonB_total | 100.0% |
| NK_total | 100.0% |
| NKCD16_total | 100.0% |
| NKCD56hi_total | 100.0% |
| NK Ki67_total | 100.0% |
| myeloid_total | 100.0% |
| CD14mono_total | 100.0% |
| CD16+mono_total | 100.0% |
| CD14+16+mono_total | 100.0% |
| Bcells_total | 100.0% |
| Bcells CD27posIgDneg_total | 100.0% |
| Bcells CD27negIgDneg_total | 100.0% |
| Bcells Ki67_total | 100.0% |
| Bcells memory_total | 100.0% |
| Bcells naive_total | 100.0% |
| CD4 Tconv_CD3 | 100.0% |
| Tconv mem_CD3 | 100.0% |
| Tconv memCCR4_CD3 | 100.0% |
| Tconv memCCR5_CD3 | 100.0% |
| Tconv memCCR6_CD3 | 100.0% |
| Tconv memCD27_CD3 | 100.0% |
| Tconv memCD56_CD3 | 100.0% |
| Tconv memCXCR3_CD3 | 100.0% |
| Tconv memDR_CD3 | 100.0% |
| Tconv memintB7_CD3 | 100.0% |
| Tconv memKi67_CD3 | 100.0% |
| Tconv memPD1_CD3 | 100.0% |
| Tconv memTIGIT_CD3 | 100.0% |
| Tconv naive_CD3 | 100.0% |
| CD4 Treg _CD3 | 100.0% |
| Treg naive_CD3 | 100.0% |
| Treg memory_CD3 | 100.0% |
| CD4neg_CD3 | 100.0% |
| CD3hi_CD3 | 100.0% |
| CD8pos_CD3 | 100.0% |
| CD8 RA_CD3 | 100.0% |
| CD8 RA naive_CD3 | 100.0% |
| CD8 RO_CD3 | 100.0% |
| CD8 ncytotox RO CCR4_CD3 | 100.0% |
| CD8 RO CCR5_CD3 | 100.0% |
| CD8 RO CCR6_CD3 | 100.0% |
| CD8 RO CD27_CD3 | 100.0% |
| CD8 RO CD56_CD3 | 100.0% |
| CD8 RO CXCR3_CD3 | 100.0% |
| CD8 RO DR_CD3 | 100.0% |
| CD8 RO intB7_CD3 | 100.0% |
| CD8  RO Ki67_CD3 | 100.0% |
| CD8 RO PD1_CD3 | 100.0% |
| CD8 RO TIGIT_CD3 | 100.0% |
| CD4 Treg_CD4 | 100.0% |
| Treg naive_CD4 | 100.0% |
| Treg memory_CD4 | 100.0% |
| Tconv mem_Tconv | 100.0% |
| Tconv memCCR4_Tconv | 100.0% |
| Tconv memCCR5_Tconv | 100.0% |
| Tconv memCCR6_Tconv | 100.0% |
| Tconv memCD27_Tconv | 100.0% |
| Tconv memCD56_Tconv | 100.0% |
| Tconv memCXCR3_Tconv | 100.0% |
| Tconv memDR_Tconv | 100.0% |
| Tconv memintB7_Tconv | 100.0% |
| Tconv memKi67_Tconv | 100.0% |
| Tconv memPD1_Tconv | 100.0% |
| Tconv memTIGIT_Tconv | 100.0% |
| Tconv naive_Tconv | 100.0% |
| Tconv memCCR4_mem | 100.0% |
| Tconv memCCR5_mem | 100.0% |
| Tconv memCCR6_mem | 100.0% |
| Tconv memCD27_mem | 100.0% |
| Tconv memCD56_mem | 100.0% |
| Tconv memCXCR3_mem | 100.0% |
| Tconv memDR_mem | 100.0% |
| Tconv memintB7_mem | 100.0% |
| Tconv memKi67_mem | 100.0% |
| Tconv memPD1_mem | 100.0% |
| Tconv memTIGIT_mem | 100.0% |
| CD3hi_CD4neg | 100.0% |
| CD8 RA_CD8 | 100.0% |
| CD8 RA CCR7 naive_CD8 | 100.0% |
| CD8 RO_CD8 | 100.0% |
| CD8 ncytotox RO CCR4_CD8ntox | 100.0% |
| CD8 RO CCR5_CD8 | 100.0% |
| CD8 RO CCR6_CD8 | 100.0% |
| CD8 RO CD27_CD8 | 100.0% |
| CD8 RO CD56_CD8 | 100.0% |
| CD8 RO CXCR3_CD8 | 100.0% |
| CD8 RO DR_CD8 | 100.0% |
| CD8 RO intB7_CD8 | 100.0% |
| CD8 RO Ki67_CD8 | 100.0% |
| CD8 RO PD1_CD8 | 100.0% |
| CD8 RO TIGIT_CD8 | 100.0% |
| CCR4_CD8RO | 100.0% |
| CCR5_CD8RO | 100.0% |
| CCR6_CD8RO | 100.0% |
| CD27_CD8RO | 100.0% |
| CD56_CD8RO | 100.0% |
| CXCR3_CD8RO | 100.0% |
| DR_CD8RO | 100.0% |
| intB7_CD8RO | 100.0% |
| Ki67_CD8RO | 100.0% |
| PD1_CD8RO | 100.0% |
| TIGIT_CD8RO | 100.0% |
| nonTnonB_CD3neg | 100.0% |
| NK_CD3neg | 100.0% |
| NKCD16_CD3neg | 100.0% |
| NKCD56hi_CD3neg | 100.0% |
| NK Ki67_CD3neg | 100.0% |
| myeloid_CD3neg | 100.0% |
| CD14mono_CD3neg | 100.0% |
| CD16mono_CD3neg | 100.0% |
| CD14+16+mono_CD3neg | 100.0% |
| Bcells_CD3neg | 100.0% |
| Bcells Ki67_CD3neg | 100.0% |
| Bcells memory_CD3neg | 100.0% |
| Bcells naive_CD3neg | 100.0% |
| NK_nonTnonB | 100.0% |
| NKCD16_nonTnonB | 100.0% |
| NKCD56hi_nonTnonB | 100.0% |
| NK Ki67_nonTnonB | 100.0% |
| NKCD16_NK | 100.0% |
| NKCD56hi_NK | 100.0% |
| NK Ki67_NK | 100.0% |
| CD14mono_myeloid | 100.0% |
| CD16mono_myeloid | 100.0% |
| CD14+16+mono_myeloid | 100.0% |
| CD27IgD_Bcells | 100.0% |
| CD27negIgDneg_Bcells | 100.0% |
| Ki67_Bcells | 100.0% |
| memory_Bcells | 100.0% |
| naive_Bcells | 100.0% |

**Total features selected by All Features (Baseline)_t50**: 166

#### All Features (Baseline)_t60

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD3pos_total | 100.0% |
| CD4 Tconv_total | 100.0% |
| CD4 Tconv mem_total | 100.0% |
| Tconv memCCR4_total | 100.0% |
| Tconv memCCR5_total | 100.0% |
| Tconv memCCR6_total | 100.0% |
| Tconv memCD27_total | 100.0% |
| Tconv memCD56_total | 100.0% |
| Tconv memCXCR3_total | 100.0% |
| Tconv memDR_total | 100.0% |
| Tconv memintB7_total | 100.0% |
| Tconv memKi67_total | 100.0% |
| Tconv memPD1_total | 100.0% |
| Tconv memTIGIT_total | 100.0% |
| Tconv naive_total | 100.0% |
| CD4 Treg_total | 100.0% |
| Treg naive_total | 100.0% |
| Treg memory_total | 100.0% |
| CD4neg_total | 100.0% |
| CD3hi_total | 100.0% |
| CD8pos_total | 100.0% |
| CD8 RA_total | 100.0% |
| CD8 RA naive_total | 100.0% |
| CD8 RO_total | 100.0% |
| CD8 RO CCR4_total | 100.0% |
| CD8 RO CCR5_total | 100.0% |
| CD8 RO CCR6_total | 100.0% |
| CD8 RO CD27_total | 100.0% |
| CD8 RO CD56_total | 100.0% |
| CD8 RO CXCR3_total | 100.0% |
| CD8 RO DR_total | 100.0% |
| CD8 RO intB7_total | 100.0% |
| CD8 RO Ki67_total | 100.0% |
| CD8 RO PD1_total | 100.0% |
| CD8 RO TIGIT_total | 100.0% |
| CD3neg_total | 100.0% |
| nonTnonB_total | 100.0% |
| NK_total | 100.0% |
| NKCD16_total | 100.0% |
| NKCD56hi_total | 100.0% |
| NK Ki67_total | 100.0% |
| myeloid_total | 100.0% |
| CD14mono_total | 100.0% |
| CD16+mono_total | 100.0% |
| CD14+16+mono_total | 100.0% |
| Bcells_total | 100.0% |
| Bcells CD27posIgDneg_total | 100.0% |
| Bcells CD27negIgDneg_total | 100.0% |
| Bcells Ki67_total | 100.0% |
| Bcells memory_total | 100.0% |
| Bcells naive_total | 100.0% |
| CD4 Tconv_CD3 | 100.0% |
| Tconv mem_CD3 | 100.0% |
| Tconv memCCR4_CD3 | 100.0% |
| Tconv memCCR5_CD3 | 100.0% |
| Tconv memCCR6_CD3 | 100.0% |
| Tconv memCD27_CD3 | 100.0% |
| Tconv memCD56_CD3 | 100.0% |
| Tconv memCXCR3_CD3 | 100.0% |
| Tconv memDR_CD3 | 100.0% |
| Tconv memintB7_CD3 | 100.0% |
| Tconv memKi67_CD3 | 100.0% |
| Tconv memPD1_CD3 | 100.0% |
| Tconv memTIGIT_CD3 | 100.0% |
| Tconv naive_CD3 | 100.0% |
| CD4 Treg _CD3 | 100.0% |
| Treg naive_CD3 | 100.0% |
| Treg memory_CD3 | 100.0% |
| CD4neg_CD3 | 100.0% |
| CD3hi_CD3 | 100.0% |
| CD8pos_CD3 | 100.0% |
| CD8 RA_CD3 | 100.0% |
| CD8 RA naive_CD3 | 100.0% |
| CD8 RO_CD3 | 100.0% |
| CD8 ncytotox RO CCR4_CD3 | 100.0% |
| CD8 RO CCR5_CD3 | 100.0% |
| CD8 RO CCR6_CD3 | 100.0% |
| CD8 RO CD27_CD3 | 100.0% |
| CD8 RO CD56_CD3 | 100.0% |
| CD8 RO CXCR3_CD3 | 100.0% |
| CD8 RO DR_CD3 | 100.0% |
| CD8 RO intB7_CD3 | 100.0% |
| CD8  RO Ki67_CD3 | 100.0% |
| CD8 RO PD1_CD3 | 100.0% |
| CD8 RO TIGIT_CD3 | 100.0% |
| CD4 Treg_CD4 | 100.0% |
| Treg naive_CD4 | 100.0% |
| Treg memory_CD4 | 100.0% |
| Tconv mem_Tconv | 100.0% |
| Tconv memCCR4_Tconv | 100.0% |
| Tconv memCCR5_Tconv | 100.0% |
| Tconv memCCR6_Tconv | 100.0% |
| Tconv memCD27_Tconv | 100.0% |
| Tconv memCD56_Tconv | 100.0% |
| Tconv memCXCR3_Tconv | 100.0% |
| Tconv memDR_Tconv | 100.0% |
| Tconv memintB7_Tconv | 100.0% |
| Tconv memKi67_Tconv | 100.0% |
| Tconv memPD1_Tconv | 100.0% |
| Tconv memTIGIT_Tconv | 100.0% |
| Tconv naive_Tconv | 100.0% |
| Tconv memCCR4_mem | 100.0% |
| Tconv memCCR5_mem | 100.0% |
| Tconv memCCR6_mem | 100.0% |
| Tconv memCD27_mem | 100.0% |
| Tconv memCD56_mem | 100.0% |
| Tconv memCXCR3_mem | 100.0% |
| Tconv memDR_mem | 100.0% |
| Tconv memintB7_mem | 100.0% |
| Tconv memKi67_mem | 100.0% |
| Tconv memPD1_mem | 100.0% |
| Tconv memTIGIT_mem | 100.0% |
| CD3hi_CD4neg | 100.0% |
| CD8 RA_CD8 | 100.0% |
| CD8 RA CCR7 naive_CD8 | 100.0% |
| CD8 RO_CD8 | 100.0% |
| CD8 ncytotox RO CCR4_CD8ntox | 100.0% |
| CD8 RO CCR5_CD8 | 100.0% |
| CD8 RO CCR6_CD8 | 100.0% |
| CD8 RO CD27_CD8 | 100.0% |
| CD8 RO CD56_CD8 | 100.0% |
| CD8 RO CXCR3_CD8 | 100.0% |
| CD8 RO DR_CD8 | 100.0% |
| CD8 RO intB7_CD8 | 100.0% |
| CD8 RO Ki67_CD8 | 100.0% |
| CD8 RO PD1_CD8 | 100.0% |
| CD8 RO TIGIT_CD8 | 100.0% |
| CCR4_CD8RO | 100.0% |
| CCR5_CD8RO | 100.0% |
| CCR6_CD8RO | 100.0% |
| CD27_CD8RO | 100.0% |
| CD56_CD8RO | 100.0% |
| CXCR3_CD8RO | 100.0% |
| DR_CD8RO | 100.0% |
| intB7_CD8RO | 100.0% |
| Ki67_CD8RO | 100.0% |
| PD1_CD8RO | 100.0% |
| TIGIT_CD8RO | 100.0% |
| nonTnonB_CD3neg | 100.0% |
| NK_CD3neg | 100.0% |
| NKCD16_CD3neg | 100.0% |
| NKCD56hi_CD3neg | 100.0% |
| NK Ki67_CD3neg | 100.0% |
| myeloid_CD3neg | 100.0% |
| CD14mono_CD3neg | 100.0% |
| CD16mono_CD3neg | 100.0% |
| CD14+16+mono_CD3neg | 100.0% |
| Bcells_CD3neg | 100.0% |
| Bcells Ki67_CD3neg | 100.0% |
| Bcells memory_CD3neg | 100.0% |
| Bcells naive_CD3neg | 100.0% |
| NK_nonTnonB | 100.0% |
| NKCD16_nonTnonB | 100.0% |
| NKCD56hi_nonTnonB | 100.0% |
| NK Ki67_nonTnonB | 100.0% |
| NKCD16_NK | 100.0% |
| NKCD56hi_NK | 100.0% |
| NK Ki67_NK | 100.0% |
| CD14mono_myeloid | 100.0% |
| CD16mono_myeloid | 100.0% |
| CD14+16+mono_myeloid | 100.0% |
| CD27IgD_Bcells | 100.0% |
| CD27negIgDneg_Bcells | 100.0% |
| Ki67_Bcells | 100.0% |
| memory_Bcells | 100.0% |
| naive_Bcells | 100.0% |

**Total features selected by All Features (Baseline)_t60**: 166

#### All Features (Baseline)_t70

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD3pos_total | 100.0% |
| CD4 Tconv_total | 100.0% |
| CD4 Tconv mem_total | 100.0% |
| Tconv memCCR4_total | 100.0% |
| Tconv memCCR5_total | 100.0% |
| Tconv memCCR6_total | 100.0% |
| Tconv memCD27_total | 100.0% |
| Tconv memCD56_total | 100.0% |
| Tconv memCXCR3_total | 100.0% |
| Tconv memDR_total | 100.0% |
| Tconv memintB7_total | 100.0% |
| Tconv memKi67_total | 100.0% |
| Tconv memPD1_total | 100.0% |
| Tconv memTIGIT_total | 100.0% |
| Tconv naive_total | 100.0% |
| CD4 Treg_total | 100.0% |
| Treg naive_total | 100.0% |
| Treg memory_total | 100.0% |
| CD4neg_total | 100.0% |
| CD3hi_total | 100.0% |
| CD8pos_total | 100.0% |
| CD8 RA_total | 100.0% |
| CD8 RA naive_total | 100.0% |
| CD8 RO_total | 100.0% |
| CD8 RO CCR4_total | 100.0% |
| CD8 RO CCR5_total | 100.0% |
| CD8 RO CCR6_total | 100.0% |
| CD8 RO CD27_total | 100.0% |
| CD8 RO CD56_total | 100.0% |
| CD8 RO CXCR3_total | 100.0% |
| CD8 RO DR_total | 100.0% |
| CD8 RO intB7_total | 100.0% |
| CD8 RO Ki67_total | 100.0% |
| CD8 RO PD1_total | 100.0% |
| CD8 RO TIGIT_total | 100.0% |
| CD3neg_total | 100.0% |
| nonTnonB_total | 100.0% |
| NK_total | 100.0% |
| NKCD16_total | 100.0% |
| NKCD56hi_total | 100.0% |
| NK Ki67_total | 100.0% |
| myeloid_total | 100.0% |
| CD14mono_total | 100.0% |
| CD16+mono_total | 100.0% |
| CD14+16+mono_total | 100.0% |
| Bcells_total | 100.0% |
| Bcells CD27posIgDneg_total | 100.0% |
| Bcells CD27negIgDneg_total | 100.0% |
| Bcells Ki67_total | 100.0% |
| Bcells memory_total | 100.0% |
| Bcells naive_total | 100.0% |
| CD4 Tconv_CD3 | 100.0% |
| Tconv mem_CD3 | 100.0% |
| Tconv memCCR4_CD3 | 100.0% |
| Tconv memCCR5_CD3 | 100.0% |
| Tconv memCCR6_CD3 | 100.0% |
| Tconv memCD27_CD3 | 100.0% |
| Tconv memCD56_CD3 | 100.0% |
| Tconv memCXCR3_CD3 | 100.0% |
| Tconv memDR_CD3 | 100.0% |
| Tconv memintB7_CD3 | 100.0% |
| Tconv memKi67_CD3 | 100.0% |
| Tconv memPD1_CD3 | 100.0% |
| Tconv memTIGIT_CD3 | 100.0% |
| Tconv naive_CD3 | 100.0% |
| CD4 Treg _CD3 | 100.0% |
| Treg naive_CD3 | 100.0% |
| Treg memory_CD3 | 100.0% |
| CD4neg_CD3 | 100.0% |
| CD3hi_CD3 | 100.0% |
| CD8pos_CD3 | 100.0% |
| CD8 RA_CD3 | 100.0% |
| CD8 RA naive_CD3 | 100.0% |
| CD8 RO_CD3 | 100.0% |
| CD8 ncytotox RO CCR4_CD3 | 100.0% |
| CD8 RO CCR5_CD3 | 100.0% |
| CD8 RO CCR6_CD3 | 100.0% |
| CD8 RO CD27_CD3 | 100.0% |
| CD8 RO CD56_CD3 | 100.0% |
| CD8 RO CXCR3_CD3 | 100.0% |
| CD8 RO DR_CD3 | 100.0% |
| CD8 RO intB7_CD3 | 100.0% |
| CD8  RO Ki67_CD3 | 100.0% |
| CD8 RO PD1_CD3 | 100.0% |
| CD8 RO TIGIT_CD3 | 100.0% |
| CD4 Treg_CD4 | 100.0% |
| Treg naive_CD4 | 100.0% |
| Treg memory_CD4 | 100.0% |
| Tconv mem_Tconv | 100.0% |
| Tconv memCCR4_Tconv | 100.0% |
| Tconv memCCR5_Tconv | 100.0% |
| Tconv memCCR6_Tconv | 100.0% |
| Tconv memCD27_Tconv | 100.0% |
| Tconv memCD56_Tconv | 100.0% |
| Tconv memCXCR3_Tconv | 100.0% |
| Tconv memDR_Tconv | 100.0% |
| Tconv memintB7_Tconv | 100.0% |
| Tconv memKi67_Tconv | 100.0% |
| Tconv memPD1_Tconv | 100.0% |
| Tconv memTIGIT_Tconv | 100.0% |
| Tconv naive_Tconv | 100.0% |
| Tconv memCCR4_mem | 100.0% |
| Tconv memCCR5_mem | 100.0% |
| Tconv memCCR6_mem | 100.0% |
| Tconv memCD27_mem | 100.0% |
| Tconv memCD56_mem | 100.0% |
| Tconv memCXCR3_mem | 100.0% |
| Tconv memDR_mem | 100.0% |
| Tconv memintB7_mem | 100.0% |
| Tconv memKi67_mem | 100.0% |
| Tconv memPD1_mem | 100.0% |
| Tconv memTIGIT_mem | 100.0% |
| CD3hi_CD4neg | 100.0% |
| CD8 RA_CD8 | 100.0% |
| CD8 RA CCR7 naive_CD8 | 100.0% |
| CD8 RO_CD8 | 100.0% |
| CD8 ncytotox RO CCR4_CD8ntox | 100.0% |
| CD8 RO CCR5_CD8 | 100.0% |
| CD8 RO CCR6_CD8 | 100.0% |
| CD8 RO CD27_CD8 | 100.0% |
| CD8 RO CD56_CD8 | 100.0% |
| CD8 RO CXCR3_CD8 | 100.0% |
| CD8 RO DR_CD8 | 100.0% |
| CD8 RO intB7_CD8 | 100.0% |
| CD8 RO Ki67_CD8 | 100.0% |
| CD8 RO PD1_CD8 | 100.0% |
| CD8 RO TIGIT_CD8 | 100.0% |
| CCR4_CD8RO | 100.0% |
| CCR5_CD8RO | 100.0% |
| CCR6_CD8RO | 100.0% |
| CD27_CD8RO | 100.0% |
| CD56_CD8RO | 100.0% |
| CXCR3_CD8RO | 100.0% |
| DR_CD8RO | 100.0% |
| intB7_CD8RO | 100.0% |
| Ki67_CD8RO | 100.0% |
| PD1_CD8RO | 100.0% |
| TIGIT_CD8RO | 100.0% |
| nonTnonB_CD3neg | 100.0% |
| NK_CD3neg | 100.0% |
| NKCD16_CD3neg | 100.0% |
| NKCD56hi_CD3neg | 100.0% |
| NK Ki67_CD3neg | 100.0% |
| myeloid_CD3neg | 100.0% |
| CD14mono_CD3neg | 100.0% |
| CD16mono_CD3neg | 100.0% |
| CD14+16+mono_CD3neg | 100.0% |
| Bcells_CD3neg | 100.0% |
| Bcells Ki67_CD3neg | 100.0% |
| Bcells memory_CD3neg | 100.0% |
| Bcells naive_CD3neg | 100.0% |
| NK_nonTnonB | 100.0% |
| NKCD16_nonTnonB | 100.0% |
| NKCD56hi_nonTnonB | 100.0% |
| NK Ki67_nonTnonB | 100.0% |
| NKCD16_NK | 100.0% |
| NKCD56hi_NK | 100.0% |
| NK Ki67_NK | 100.0% |
| CD14mono_myeloid | 100.0% |
| CD16mono_myeloid | 100.0% |
| CD14+16+mono_myeloid | 100.0% |
| CD27IgD_Bcells | 100.0% |
| CD27negIgDneg_Bcells | 100.0% |
| Ki67_Bcells | 100.0% |
| memory_Bcells | 100.0% |
| naive_Bcells | 100.0% |

**Total features selected by All Features (Baseline)_t70**: 166

#### All Features (Baseline)_t80

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD3pos_total | 100.0% |
| CD4 Tconv_total | 100.0% |
| CD4 Tconv mem_total | 100.0% |
| Tconv memCCR4_total | 100.0% |
| Tconv memCCR5_total | 100.0% |
| Tconv memCCR6_total | 100.0% |
| Tconv memCD27_total | 100.0% |
| Tconv memCD56_total | 100.0% |
| Tconv memCXCR3_total | 100.0% |
| Tconv memDR_total | 100.0% |
| Tconv memintB7_total | 100.0% |
| Tconv memKi67_total | 100.0% |
| Tconv memPD1_total | 100.0% |
| Tconv memTIGIT_total | 100.0% |
| Tconv naive_total | 100.0% |
| CD4 Treg_total | 100.0% |
| Treg naive_total | 100.0% |
| Treg memory_total | 100.0% |
| CD4neg_total | 100.0% |
| CD3hi_total | 100.0% |
| CD8pos_total | 100.0% |
| CD8 RA_total | 100.0% |
| CD8 RA naive_total | 100.0% |
| CD8 RO_total | 100.0% |
| CD8 RO CCR4_total | 100.0% |
| CD8 RO CCR5_total | 100.0% |
| CD8 RO CCR6_total | 100.0% |
| CD8 RO CD27_total | 100.0% |
| CD8 RO CD56_total | 100.0% |
| CD8 RO CXCR3_total | 100.0% |
| CD8 RO DR_total | 100.0% |
| CD8 RO intB7_total | 100.0% |
| CD8 RO Ki67_total | 100.0% |
| CD8 RO PD1_total | 100.0% |
| CD8 RO TIGIT_total | 100.0% |
| CD3neg_total | 100.0% |
| nonTnonB_total | 100.0% |
| NK_total | 100.0% |
| NKCD16_total | 100.0% |
| NKCD56hi_total | 100.0% |
| NK Ki67_total | 100.0% |
| myeloid_total | 100.0% |
| CD14mono_total | 100.0% |
| CD16+mono_total | 100.0% |
| CD14+16+mono_total | 100.0% |
| Bcells_total | 100.0% |
| Bcells CD27posIgDneg_total | 100.0% |
| Bcells CD27negIgDneg_total | 100.0% |
| Bcells Ki67_total | 100.0% |
| Bcells memory_total | 100.0% |
| Bcells naive_total | 100.0% |
| CD4 Tconv_CD3 | 100.0% |
| Tconv mem_CD3 | 100.0% |
| Tconv memCCR4_CD3 | 100.0% |
| Tconv memCCR5_CD3 | 100.0% |
| Tconv memCCR6_CD3 | 100.0% |
| Tconv memCD27_CD3 | 100.0% |
| Tconv memCD56_CD3 | 100.0% |
| Tconv memCXCR3_CD3 | 100.0% |
| Tconv memDR_CD3 | 100.0% |
| Tconv memintB7_CD3 | 100.0% |
| Tconv memKi67_CD3 | 100.0% |
| Tconv memPD1_CD3 | 100.0% |
| Tconv memTIGIT_CD3 | 100.0% |
| Tconv naive_CD3 | 100.0% |
| CD4 Treg _CD3 | 100.0% |
| Treg naive_CD3 | 100.0% |
| Treg memory_CD3 | 100.0% |
| CD4neg_CD3 | 100.0% |
| CD3hi_CD3 | 100.0% |
| CD8pos_CD3 | 100.0% |
| CD8 RA_CD3 | 100.0% |
| CD8 RA naive_CD3 | 100.0% |
| CD8 RO_CD3 | 100.0% |
| CD8 ncytotox RO CCR4_CD3 | 100.0% |
| CD8 RO CCR5_CD3 | 100.0% |
| CD8 RO CCR6_CD3 | 100.0% |
| CD8 RO CD27_CD3 | 100.0% |
| CD8 RO CD56_CD3 | 100.0% |
| CD8 RO CXCR3_CD3 | 100.0% |
| CD8 RO DR_CD3 | 100.0% |
| CD8 RO intB7_CD3 | 100.0% |
| CD8  RO Ki67_CD3 | 100.0% |
| CD8 RO PD1_CD3 | 100.0% |
| CD8 RO TIGIT_CD3 | 100.0% |
| CD4 Treg_CD4 | 100.0% |
| Treg naive_CD4 | 100.0% |
| Treg memory_CD4 | 100.0% |
| Tconv mem_Tconv | 100.0% |
| Tconv memCCR4_Tconv | 100.0% |
| Tconv memCCR5_Tconv | 100.0% |
| Tconv memCCR6_Tconv | 100.0% |
| Tconv memCD27_Tconv | 100.0% |
| Tconv memCD56_Tconv | 100.0% |
| Tconv memCXCR3_Tconv | 100.0% |
| Tconv memDR_Tconv | 100.0% |
| Tconv memintB7_Tconv | 100.0% |
| Tconv memKi67_Tconv | 100.0% |
| Tconv memPD1_Tconv | 100.0% |
| Tconv memTIGIT_Tconv | 100.0% |
| Tconv naive_Tconv | 100.0% |
| Tconv memCCR4_mem | 100.0% |
| Tconv memCCR5_mem | 100.0% |
| Tconv memCCR6_mem | 100.0% |
| Tconv memCD27_mem | 100.0% |
| Tconv memCD56_mem | 100.0% |
| Tconv memCXCR3_mem | 100.0% |
| Tconv memDR_mem | 100.0% |
| Tconv memintB7_mem | 100.0% |
| Tconv memKi67_mem | 100.0% |
| Tconv memPD1_mem | 100.0% |
| Tconv memTIGIT_mem | 100.0% |
| CD3hi_CD4neg | 100.0% |
| CD8 RA_CD8 | 100.0% |
| CD8 RA CCR7 naive_CD8 | 100.0% |
| CD8 RO_CD8 | 100.0% |
| CD8 ncytotox RO CCR4_CD8ntox | 100.0% |
| CD8 RO CCR5_CD8 | 100.0% |
| CD8 RO CCR6_CD8 | 100.0% |
| CD8 RO CD27_CD8 | 100.0% |
| CD8 RO CD56_CD8 | 100.0% |
| CD8 RO CXCR3_CD8 | 100.0% |
| CD8 RO DR_CD8 | 100.0% |
| CD8 RO intB7_CD8 | 100.0% |
| CD8 RO Ki67_CD8 | 100.0% |
| CD8 RO PD1_CD8 | 100.0% |
| CD8 RO TIGIT_CD8 | 100.0% |
| CCR4_CD8RO | 100.0% |
| CCR5_CD8RO | 100.0% |
| CCR6_CD8RO | 100.0% |
| CD27_CD8RO | 100.0% |
| CD56_CD8RO | 100.0% |
| CXCR3_CD8RO | 100.0% |
| DR_CD8RO | 100.0% |
| intB7_CD8RO | 100.0% |
| Ki67_CD8RO | 100.0% |
| PD1_CD8RO | 100.0% |
| TIGIT_CD8RO | 100.0% |
| nonTnonB_CD3neg | 100.0% |
| NK_CD3neg | 100.0% |
| NKCD16_CD3neg | 100.0% |
| NKCD56hi_CD3neg | 100.0% |
| NK Ki67_CD3neg | 100.0% |
| myeloid_CD3neg | 100.0% |
| CD14mono_CD3neg | 100.0% |
| CD16mono_CD3neg | 100.0% |
| CD14+16+mono_CD3neg | 100.0% |
| Bcells_CD3neg | 100.0% |
| Bcells Ki67_CD3neg | 100.0% |
| Bcells memory_CD3neg | 100.0% |
| Bcells naive_CD3neg | 100.0% |
| NK_nonTnonB | 100.0% |
| NKCD16_nonTnonB | 100.0% |
| NKCD56hi_nonTnonB | 100.0% |
| NK Ki67_nonTnonB | 100.0% |
| NKCD16_NK | 100.0% |
| NKCD56hi_NK | 100.0% |
| NK Ki67_NK | 100.0% |
| CD14mono_myeloid | 100.0% |
| CD16mono_myeloid | 100.0% |
| CD14+16+mono_myeloid | 100.0% |
| CD27IgD_Bcells | 100.0% |
| CD27negIgDneg_Bcells | 100.0% |
| Ki67_Bcells | 100.0% |
| memory_Bcells | 100.0% |
| naive_Bcells | 100.0% |

**Total features selected by All Features (Baseline)_t80**: 166

#### ElasticNet_Lenient_t40

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| DR_CD8RO | 90.0% |
| CD16mono_myeloid | 87.5% |
| CD8 RO DR_CD8 | 75.0% |
| Ki67_Bcells | 70.0% |
| NKCD56hi_total | 67.5% |
| CD27IgD_Bcells | 57.5% |
| CD14+16+mono_myeloid | 52.5% |
| CD3hi_total | 47.5% |
| CD8pos_CD3 | 40.0% |
| Treg memory_CD3 | 35.0% |
| CD16mono_CD3neg | 32.5% |
| Bcells memory_total | 32.5% |
| CD14mono_myeloid | 32.5% |
| Tconv memDR_Tconv | 30.0% |
| Tconv memDR_CD3 | 27.5% |
| Tconv mem_Tconv | 27.5% |
| CD8 RO intB7_CD8 | 25.0% |
| Bcells CD27negIgDneg_total | 25.0% |
| Tconv memPD1_mem | 25.0% |
| memory_Bcells | 25.0% |
| intB7_CD8RO | 25.0% |
| CD8 RO CD56_CD8 | 25.0% |
| Bcells CD27posIgDneg_total | 25.0% |
| Tconv memKi67_mem | 25.0% |
| CD8 RO CD56_CD3 | 22.5% |
| CD8 RO DR_CD3 | 22.5% |
| Tconv memCCR4_mem | 20.0% |
| Tconv memCD56_total | 20.0% |
| NK Ki67_total | 20.0% |
| Treg memory_CD4 | 20.0% |
| CD8 RO PD1_CD3 | 20.0% |
| NKCD16_NK | 17.5% |
| Tconv memDR_total | 17.5% |
| Tconv memCCR5_mem | 17.5% |
| NKCD56hi_NK | 17.5% |
| CD8 RA_CD3 | 17.5% |
| CD8 RA CCR7 naive_CD8 | 15.0% |
| CCR4_CD8RO | 15.0% |
| Tconv memTIGIT_mem | 15.0% |
| Tconv memCD27_Tconv | 15.0% |
| CD8 RO CXCR3_CD3 | 12.5% |
| CD8 RO CXCR3_CD8 | 12.5% |
| CD4 Treg _CD3 | 12.5% |
| Tconv memCCR6_total | 12.5% |
| Bcells naive_total | 12.5% |
| CD4 Treg_CD4 | 12.5% |
| NKCD56hi_nonTnonB | 12.5% |
| Bcells Ki67_CD3neg | 12.5% |
| Tconv memKi67_total | 12.5% |
| Tconv memCCR6_mem | 12.5% |
| CD8 RO TIGIT_CD3 | 12.5% |
| CCR6_CD8RO | 12.5% |
| CD27negIgDneg_Bcells | 12.5% |
| Tconv memintB7_Tconv | 12.5% |
| Tconv naive_Tconv | 12.5% |
| NK Ki67_NK | 10.0% |
| Tconv memCXCR3_mem | 10.0% |
| CD3hi_CD3 | 10.0% |
| Tconv memDR_mem | 10.0% |
| Treg naive_total | 10.0% |
| CD27_CD8RO | 10.0% |
| Tconv memintB7_mem | 7.5% |
| Tconv memCCR5_total | 7.5% |
| CD4neg_total | 7.5% |
| CD4 Tconv_total | 7.5% |
| CD3hi_CD4neg | 7.5% |
| CXCR3_CD8RO | 7.5% |
| Treg naive_CD3 | 7.5% |
| CCR5_CD8RO | 7.5% |
| Tconv naive_total | 7.5% |
| Tconv naive_CD3 | 7.5% |
| Bcells Ki67_total | 7.5% |
| NK_total | 5.0% |
| CD8 RO TIGIT_CD8 | 5.0% |
| Treg memory_total | 5.0% |
| NK Ki67_nonTnonB | 5.0% |
| CD8 RA naive_total | 5.0% |
| CD3neg_total | 5.0% |
| CD3pos_total | 5.0% |
| CD56_CD8RO | 5.0% |
| Tconv memintB7_CD3 | 5.0% |
| CD8 RO intB7_total | 5.0% |
| naive_Bcells | 5.0% |
| Tconv mem_CD3 | 5.0% |
| Tconv memKi67_CD3 | 5.0% |
| CD4 Tconv_CD3 | 5.0% |
| CD4neg_CD3 | 5.0% |
| CD8 RA naive_CD3 | 5.0% |
| CD8 RO CCR5_total | 5.0% |
| CD8 RO CCR6_CD8 | 2.5% |
| CD8 RO DR_total | 2.5% |
| Bcells_total | 2.5% |
| CD8 RO Ki67_total | 2.5% |
| CD8 RO PD1_total | 2.5% |
| Tconv memintB7_total | 2.5% |
| Tconv memCD56_CD3 | 2.5% |
| Tconv memTIGIT_Tconv | 2.5% |
| Tconv memCXCR3_Tconv | 2.5% |
| CD8 RO CD56_total | 2.5% |
| Tconv memCD27_mem | 2.5% |
| Tconv memCCR4_total | 2.5% |
| Tconv memCXCR3_total | 2.5% |
| CD8 RO CD27_CD3 | 2.5% |
| Treg naive_CD4 | 2.5% |

**Total features selected by ElasticNet_Lenient_t40**: 104

#### ElasticNet_Lenient_t50

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| DR_CD8RO | 77.5% |
| CD16mono_myeloid | 75.0% |
| Ki67_Bcells | 55.0% |
| CD8 RO DR_CD8 | 55.0% |
| NKCD56hi_total | 50.0% |
| CD14+16+mono_myeloid | 35.0% |
| CD3hi_total | 32.5% |
| CD8pos_CD3 | 30.0% |
| CD27IgD_Bcells | 27.5% |
| CD16mono_CD3neg | 22.5% |
| Bcells CD27posIgDneg_total | 22.5% |
| Treg memory_CD3 | 22.5% |
| Tconv mem_Tconv | 20.0% |
| Tconv memKi67_mem | 20.0% |
| CD8 RO DR_CD3 | 17.5% |
| Tconv memPD1_mem | 15.0% |
| Bcells memory_total | 15.0% |
| Tconv memDR_Tconv | 15.0% |
| memory_Bcells | 15.0% |
| NKCD16_NK | 15.0% |
| CD14mono_myeloid | 15.0% |
| Tconv memintB7_Tconv | 12.5% |
| Tconv memCCR5_mem | 12.5% |
| CD8 RA_CD3 | 12.5% |
| Tconv memDR_CD3 | 12.5% |
| CD8 RO CD56_CD8 | 12.5% |
| Tconv memDR_total | 12.5% |
| CD8 RO PD1_CD3 | 10.0% |
| Treg memory_CD4 | 10.0% |
| Tconv memDR_mem | 10.0% |
| Bcells CD27negIgDneg_total | 10.0% |
| Tconv memCD56_total | 10.0% |
| NKCD56hi_NK | 7.5% |
| CD8 RA CCR7 naive_CD8 | 7.5% |
| Tconv memCCR6_total | 7.5% |
| Tconv memKi67_total | 7.5% |
| CD27negIgDneg_Bcells | 7.5% |
| CD8 RO intB7_CD8 | 7.5% |
| Tconv memCXCR3_mem | 7.5% |
| Tconv memCCR4_mem | 7.5% |
| NK Ki67_total | 5.0% |
| Tconv memCCR5_total | 5.0% |
| CD27_CD8RO | 5.0% |
| CCR5_CD8RO | 5.0% |
| Tconv naive_total | 5.0% |
| Treg naive_total | 5.0% |
| Tconv memCD27_Tconv | 5.0% |
| intB7_CD8RO | 5.0% |
| CD8 RO CXCR3_CD3 | 5.0% |
| CD8 RO CD56_CD3 | 5.0% |
| CD8 RO CXCR3_CD8 | 5.0% |
| Tconv memTIGIT_mem | 5.0% |
| CXCR3_CD8RO | 5.0% |
| CCR4_CD8RO | 2.5% |
| CD8 RO TIGIT_CD3 | 2.5% |
| CD3hi_CD3 | 2.5% |
| CD3pos_total | 2.5% |
| CD3neg_total | 2.5% |
| Tconv memintB7_CD3 | 2.5% |
| Bcells Ki67_CD3neg | 2.5% |
| Tconv naive_Tconv | 2.5% |
| CD8 RO TIGIT_CD8 | 2.5% |
| NKCD56hi_nonTnonB | 2.5% |
| CD8 RO DR_total | 2.5% |
| CD4 Tconv_CD3 | 2.5% |
| CD8 RO Ki67_total | 2.5% |
| CD8 RO CCR5_total | 2.5% |
| Tconv naive_CD3 | 2.5% |
| Tconv memTIGIT_Tconv | 2.5% |
| CD8 RA naive_CD3 | 2.5% |
| CCR6_CD8RO | 2.5% |
| CD4 Treg_CD4 | 2.5% |
| CD8 RA naive_total | 2.5% |
| Bcells naive_total | 2.5% |
| Tconv memKi67_CD3 | 2.5% |
| Treg naive_CD3 | 2.5% |
| CD4neg_CD3 | 2.5% |
| Tconv memintB7_mem | 2.5% |
| CD3hi_CD4neg | 2.5% |
| CD4 Treg _CD3 | 2.5% |
| Tconv memCCR4_total | 2.5% |
| Tconv memCXCR3_total | 2.5% |

**Total features selected by ElasticNet_Lenient_t50**: 82

#### ElasticNet_Lenient_t60

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| DR_CD8RO | 67.5% |
| CD16mono_myeloid | 62.5% |
| CD8 RO DR_CD8 | 37.5% |
| NKCD56hi_total | 35.0% |
| CD14+16+mono_myeloid | 27.5% |
| Ki67_Bcells | 25.0% |
| CD3hi_total | 20.0% |
| CD27IgD_Bcells | 20.0% |
| CD16mono_CD3neg | 17.5% |
| CD14mono_myeloid | 15.0% |
| Bcells CD27posIgDneg_total | 12.5% |
| CD8pos_CD3 | 12.5% |
| CD8 RO DR_CD3 | 10.0% |
| Tconv memintB7_Tconv | 10.0% |
| Treg memory_CD3 | 10.0% |
| Tconv memKi67_mem | 10.0% |
| CD8 RO CD56_CD8 | 10.0% |
| Tconv memDR_Tconv | 10.0% |
| Bcells CD27negIgDneg_total | 7.5% |
| NKCD16_NK | 7.5% |
| Bcells memory_total | 7.5% |
| Tconv memPD1_mem | 7.5% |
| Tconv mem_Tconv | 7.5% |
| CD8 RO CXCR3_CD8 | 5.0% |
| CD8 RO PD1_CD3 | 5.0% |
| CCR5_CD8RO | 5.0% |
| NKCD56hi_NK | 5.0% |
| CD8 RO intB7_CD8 | 5.0% |
| NK Ki67_total | 5.0% |
| CD8 RA_CD3 | 5.0% |
| Tconv memDR_CD3 | 5.0% |
| Tconv memDR_total | 5.0% |
| Tconv memCCR5_mem | 5.0% |
| Tconv memDR_mem | 5.0% |
| Treg memory_CD4 | 5.0% |
| CD3neg_total | 2.5% |
| CD3pos_total | 2.5% |
| intB7_CD8RO | 2.5% |
| Bcells Ki67_CD3neg | 2.5% |
| memory_Bcells | 2.5% |
| CD8 RO CD56_CD3 | 2.5% |
| Tconv naive_total | 2.5% |
| Tconv memCCR4_mem | 2.5% |
| Tconv memintB7_CD3 | 2.5% |
| Tconv memCD27_Tconv | 2.5% |
| CD8 RA naive_CD3 | 2.5% |
| Tconv memCXCR3_mem | 2.5% |
| Tconv naive_CD3 | 2.5% |
| CD8 RO CCR5_total | 2.5% |
| Tconv memKi67_total | 2.5% |
| CXCR3_CD8RO | 2.5% |
| CD27negIgDneg_Bcells | 2.5% |
| Tconv memCD56_total | 2.5% |
| Tconv memCCR4_total | 2.5% |

**Total features selected by ElasticNet_Lenient_t60**: 54

#### ElasticNet_Lenient_t70

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD16mono_myeloid | 61.5% |
| DR_CD8RO | 48.7% |
| NKCD56hi_total | 30.8% |
| CD14+16+mono_myeloid | 23.1% |
| CD8 RO DR_CD8 | 23.1% |
| CD16mono_CD3neg | 15.4% |
| CD27IgD_Bcells | 15.4% |
| CD14mono_myeloid | 10.3% |
| Ki67_Bcells | 10.3% |
| CD3hi_total | 7.7% |
| Tconv memDR_Tconv | 7.7% |
| Treg memory_CD3 | 7.7% |
| Treg memory_CD4 | 5.1% |
| Tconv memCCR5_mem | 5.1% |
| CD8 RO DR_CD3 | 5.1% |
| CD3neg_total | 2.6% |
| CD3pos_total | 2.6% |
| NKCD56hi_NK | 2.6% |
| Bcells Ki67_CD3neg | 2.6% |
| Tconv memKi67_mem | 2.6% |
| Tconv memDR_CD3 | 2.6% |
| Tconv memCD27_Tconv | 2.6% |
| Tconv mem_Tconv | 2.6% |
| Tconv naive_CD3 | 2.6% |
| CD8pos_CD3 | 2.6% |
| CD8 RO PD1_CD3 | 2.6% |
| CD8 RA_CD3 | 2.6% |
| Tconv memPD1_mem | 2.6% |
| CD27negIgDneg_Bcells | 2.6% |
| NKCD16_NK | 2.6% |
| Bcells memory_total | 2.6% |
| Tconv memDR_mem | 2.6% |
| Tconv memDR_total | 2.6% |
| Tconv memintB7_Tconv | 2.6% |
| Tconv memCCR4_total | 2.6% |

**Total features selected by ElasticNet_Lenient_t70**: 35

#### ElasticNet_Lenient_t80

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD16mono_myeloid | 43.8% |
| DR_CD8RO | 37.5% |
| CD14+16+mono_myeloid | 15.6% |
| NKCD56hi_total | 12.5% |
| CD27IgD_Bcells | 9.4% |
| Ki67_Bcells | 6.2% |
| CD16mono_CD3neg | 6.2% |
| NKCD56hi_NK | 3.1% |
| CD3hi_total | 3.1% |
| Tconv memCD27_Tconv | 3.1% |
| Tconv memCCR5_mem | 3.1% |
| Tconv memDR_CD3 | 3.1% |
| Tconv memDR_Tconv | 3.1% |
| CD14mono_myeloid | 3.1% |
| CD8 RO PD1_CD3 | 3.1% |
| CD8 RO DR_CD8 | 3.1% |
| Tconv memPD1_mem | 3.1% |
| Bcells memory_total | 3.1% |
| Tconv memDR_mem | 3.1% |

**Total features selected by ElasticNet_Lenient_t80**: 19

#### ElasticNet_RFE_t40

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD16mono_myeloid | 87.5% |
| DR_CD8RO | 75.0% |
| CD8 RO DR_CD8 | 65.0% |
| CD27IgD_Bcells | 55.0% |
| NKCD56hi_total | 50.0% |
| Ki67_Bcells | 45.0% |
| CD8pos_CD3 | 37.5% |
| CD3hi_total | 35.0% |
| CD14+16+mono_myeloid | 32.5% |
| CD16mono_CD3neg | 30.0% |
| Treg memory_CD3 | 30.0% |
| CD14mono_myeloid | 27.5% |
| Bcells CD27posIgDneg_total | 25.0% |
| Bcells memory_total | 22.5% |
| Tconv memDR_Tconv | 22.5% |
| Tconv mem_Tconv | 22.5% |
| CD8 RO DR_CD3 | 20.0% |
| Tconv memDR_CD3 | 17.5% |
| Tconv memPD1_mem | 17.5% |
| Treg memory_CD4 | 17.5% |
| CD8 RA CCR7 naive_CD8 | 15.0% |
| memory_Bcells | 15.0% |
| CD8 RO PD1_CD3 | 15.0% |
| CD8 RO CD56_CD8 | 15.0% |
| Tconv memDR_total | 15.0% |
| NKCD16_NK | 15.0% |
| Tconv naive_Tconv | 12.5% |
| Tconv memKi67_mem | 12.5% |
| NKCD56hi_NK | 12.5% |
| Tconv memCD27_Tconv | 12.5% |
| intB7_CD8RO | 12.5% |
| CD4 Treg_CD4 | 12.5% |
| CD4 Treg _CD3 | 10.0% |
| Tconv memTIGIT_mem | 10.0% |
| Tconv memCCR5_mem | 10.0% |
| Tconv memintB7_Tconv | 10.0% |
| CD8 RO CXCR3_CD3 | 10.0% |
| CD8 RA_CD3 | 10.0% |
| Tconv memCCR6_total | 10.0% |
| Bcells CD27negIgDneg_total | 10.0% |
| CD27negIgDneg_Bcells | 10.0% |
| Bcells naive_total | 10.0% |
| CCR4_CD8RO | 7.5% |
| CCR6_CD8RO | 7.5% |
| NK Ki67_total | 7.5% |
| CD8 RO TIGIT_CD3 | 7.5% |
| Tconv naive_CD3 | 7.5% |
| Tconv memKi67_total | 7.5% |
| Tconv memDR_mem | 7.5% |
| CD8 RO CXCR3_CD8 | 7.5% |
| Tconv naive_total | 7.5% |
| Tconv memCCR4_mem | 7.5% |
| CD3hi_CD3 | 7.5% |
| CCR5_CD8RO | 7.5% |
| Treg memory_total | 5.0% |
| Tconv memCCR5_total | 5.0% |
| CD3neg_total | 5.0% |
| CD3pos_total | 5.0% |
| Bcells Ki67_CD3neg | 5.0% |
| CD8 RO intB7_CD8 | 5.0% |
| naive_Bcells | 5.0% |
| NKCD56hi_nonTnonB | 5.0% |
| CD8 RO CD56_CD3 | 5.0% |
| CD27_CD8RO | 5.0% |
| Tconv memCD56_total | 5.0% |
| Treg naive_CD3 | 5.0% |
| Tconv memCXCR3_mem | 5.0% |
| CD8 RO TIGIT_CD8 | 2.5% |
| NK Ki67_nonTnonB | 2.5% |
| CD4neg_CD3 | 2.5% |
| CD8 RO DR_total | 2.5% |
| CD4 Tconv_CD3 | 2.5% |
| CXCR3_CD8RO | 2.5% |
| NK Ki67_NK | 2.5% |
| CD8 RO CCR5_total | 2.5% |
| CD8 RA naive_CD3 | 2.5% |
| Tconv memCD56_CD3 | 2.5% |
| Tconv memTIGIT_Tconv | 2.5% |
| CD8 RO intB7_total | 2.5% |
| CD4 Tconv_total | 2.5% |
| Treg naive_total | 2.5% |
| CD3hi_CD4neg | 2.5% |
| Tconv memCCR4_total | 2.5% |
| Tconv memCXCR3_total | 2.5% |
| CD8 RO CD27_CD3 | 2.5% |

**Total features selected by ElasticNet_RFE_t40**: 85

#### ElasticNet_RFE_t50

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| DR_CD8RO | 72.5% |
| CD16mono_myeloid | 70.0% |
| NKCD56hi_total | 35.0% |
| CD8 RO DR_CD8 | 35.0% |
| Ki67_Bcells | 32.5% |
| CD27IgD_Bcells | 27.5% |
| CD16mono_CD3neg | 22.5% |
| CD14+16+mono_myeloid | 22.5% |
| Bcells CD27posIgDneg_total | 22.5% |
| CD3hi_total | 22.5% |
| Tconv mem_Tconv | 20.0% |
| CD8pos_CD3 | 20.0% |
| Treg memory_CD3 | 17.5% |
| CD8 RO DR_CD3 | 15.0% |
| CD14mono_myeloid | 15.0% |
| Tconv memDR_Tconv | 12.5% |
| Treg memory_CD4 | 10.0% |
| Tconv memKi67_mem | 7.5% |
| Tconv memDR_mem | 7.5% |
| Bcells memory_total | 7.5% |
| CD8 RO CD56_CD8 | 7.5% |
| Tconv memintB7_Tconv | 7.5% |
| CD8 RO PD1_CD3 | 7.5% |
| Tconv memDR_CD3 | 7.5% |
| NKCD16_NK | 7.5% |
| Tconv memDR_total | 5.0% |
| intB7_CD8RO | 5.0% |
| Tconv naive_total | 5.0% |
| NKCD56hi_NK | 5.0% |
| Tconv memCCR5_mem | 5.0% |
| Tconv memCD56_total | 5.0% |
| CD8 RA_CD3 | 5.0% |
| CD27negIgDneg_Bcells | 5.0% |
| Tconv memKi67_total | 5.0% |
| Tconv memPD1_mem | 5.0% |
| CCR5_CD8RO | 5.0% |
| CD8 RA CCR7 naive_CD8 | 2.5% |
| CD8 RO intB7_CD8 | 2.5% |
| Tconv naive_Tconv | 2.5% |
| Tconv memCCR4_mem | 2.5% |
| CD3neg_total | 2.5% |
| Bcells Ki67_CD3neg | 2.5% |
| CD3pos_total | 2.5% |
| CD8 RO CXCR3_CD3 | 2.5% |
| Tconv memCD27_Tconv | 2.5% |
| CD4 Tconv_CD3 | 2.5% |
| Tconv naive_CD3 | 2.5% |
| CD8 RO DR_total | 2.5% |
| CD8 RO CD56_CD3 | 2.5% |
| CD27_CD8RO | 2.5% |
| CD8 RA naive_CD3 | 2.5% |
| Tconv memTIGIT_Tconv | 2.5% |
| CD8 RO CXCR3_CD8 | 2.5% |
| CD8 RO CCR5_total | 2.5% |
| Bcells CD27negIgDneg_total | 2.5% |
| CD4 Treg_CD4 | 2.5% |
| Bcells naive_total | 2.5% |
| Tconv memCXCR3_mem | 2.5% |
| Treg naive_total | 2.5% |
| CD3hi_CD4neg | 2.5% |
| CD4 Treg _CD3 | 2.5% |
| Tconv memCCR4_total | 2.5% |

**Total features selected by ElasticNet_RFE_t50**: 62

#### ElasticNet_RFE_t60

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD16mono_myeloid | 59.0% |
| DR_CD8RO | 43.6% |
| CD8 RO DR_CD8 | 30.8% |
| NKCD56hi_total | 20.5% |
| CD14+16+mono_myeloid | 20.5% |
| CD27IgD_Bcells | 20.5% |
| CD16mono_CD3neg | 17.9% |
| Bcells CD27posIgDneg_total | 12.8% |
| CD14mono_myeloid | 12.8% |
| CD3hi_total | 10.3% |
| Treg memory_CD3 | 10.3% |
| CD8pos_CD3 | 10.3% |
| Tconv memDR_Tconv | 7.7% |
| CD8 RO DR_CD3 | 7.7% |
| Ki67_Bcells | 7.7% |
| NKCD56hi_NK | 5.1% |
| CCR5_CD8RO | 5.1% |
| Tconv mem_Tconv | 5.1% |
| Tconv memDR_CD3 | 5.1% |
| Tconv memKi67_mem | 5.1% |
| Tconv memDR_mem | 5.1% |
| CD8 RO PD1_CD3 | 5.1% |
| Treg memory_CD4 | 5.1% |
| Tconv naive_total | 2.6% |
| Tconv memCCR5_mem | 2.6% |
| CD3pos_total | 2.6% |
| CD3neg_total | 2.6% |
| Tconv memCD27_Tconv | 2.6% |
| Tconv naive_CD3 | 2.6% |
| CD8 RO CCR5_total | 2.6% |
| CD8 RO CXCR3_CD8 | 2.6% |
| CD8 RA naive_CD3 | 2.6% |
| CD8 RO CD56_CD8 | 2.6% |
| NKCD16_NK | 2.6% |
| Bcells memory_total | 2.6% |
| Tconv memDR_total | 2.6% |
| Tconv memintB7_Tconv | 2.6% |
| Tconv memCCR4_total | 2.6% |

**Total features selected by ElasticNet_RFE_t60**: 38

#### ElasticNet_RFE_t70

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD16mono_myeloid | 55.6% |
| DR_CD8RO | 33.3% |
| CD27IgD_Bcells | 16.7% |
| CD8 RO DR_CD8 | 13.9% |
| CD14+16+mono_myeloid | 11.1% |
| CD16mono_CD3neg | 11.1% |
| NKCD56hi_total | 11.1% |
| Treg memory_CD3 | 8.3% |
| CD14mono_myeloid | 5.6% |
| Ki67_Bcells | 5.6% |
| CD3hi_total | 2.8% |
| CD3pos_total | 2.8% |
| CD3neg_total | 2.8% |
| Tconv memCCR5_mem | 2.8% |
| Tconv memCD27_Tconv | 2.8% |
| Tconv mem_Tconv | 2.8% |
| Tconv memDR_CD3 | 2.8% |
| Tconv memDR_Tconv | 2.8% |
| Tconv naive_CD3 | 2.8% |
| CD8pos_CD3 | 2.8% |
| Bcells memory_total | 2.8% |
| Tconv memDR_mem | 2.8% |
| Treg memory_CD4 | 2.8% |
| Tconv memCCR4_total | 2.8% |

**Total features selected by ElasticNet_RFE_t70**: 24

#### ElasticNet_RFE_t80

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD16mono_myeloid | 46.2% |
| DR_CD8RO | 23.1% |
| CD27IgD_Bcells | 11.5% |
| Ki67_Bcells | 7.7% |
| NKCD56hi_total | 7.7% |
| CD3hi_total | 3.8% |
| Tconv memCCR5_mem | 3.8% |
| Tconv memCD27_Tconv | 3.8% |
| Tconv memDR_Tconv | 3.8% |
| Tconv memDR_CD3 | 3.8% |
| CD14mono_myeloid | 3.8% |
| CD8 RO DR_CD8 | 3.8% |
| CD16mono_CD3neg | 3.8% |
| Tconv memDR_mem | 3.8% |

**Total features selected by ElasticNet_RFE_t80**: 14

#### ElasticNet_Strict_t40

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| DR_CD8RO | 60.0% |
| CD16mono_myeloid | 50.0% |
| NKCD56hi_total | 40.0% |
| CD8 RO DR_CD8 | 37.5% |
| CD14+16+mono_myeloid | 22.5% |
| CD27IgD_Bcells | 22.5% |
| CD14mono_myeloid | 17.5% |
| CD16mono_CD3neg | 15.0% |
| Tconv memKi67_mem | 15.0% |
| CD3hi_total | 15.0% |
| Tconv memDR_Tconv | 12.5% |
| Bcells CD27posIgDneg_total | 12.5% |
| Ki67_Bcells | 12.5% |
| Tconv memCCR5_mem | 10.0% |
| CD8 RO CD56_CD8 | 10.0% |
| CD8 RO DR_CD3 | 10.0% |
| Tconv mem_Tconv | 7.5% |
| NKCD56hi_NK | 7.5% |
| CD8 RA_CD3 | 7.5% |
| Tconv memDR_CD3 | 7.5% |
| memory_Bcells | 7.5% |
| Treg memory_CD3 | 5.0% |
| intB7_CD8RO | 5.0% |
| CD8 RO TIGIT_CD3 | 5.0% |
| CD8pos_CD3 | 5.0% |
| Tconv memintB7_Tconv | 5.0% |
| Bcells memory_total | 5.0% |
| CD8 RO intB7_CD8 | 2.5% |
| CD8 RA CCR7 naive_CD8 | 2.5% |
| Bcells CD27negIgDneg_total | 2.5% |
| CCR5_CD8RO | 2.5% |
| Tconv naive_Tconv | 2.5% |
| Tconv memCD27_Tconv | 2.5% |
| CD4 Treg_CD4 | 2.5% |
| Tconv naive_CD3 | 2.5% |
| CD8 RO CCR5_total | 2.5% |
| Tconv memCCR5_total | 2.5% |
| Tconv memKi67_total | 2.5% |
| CD8 RO PD1_CD3 | 2.5% |
| Tconv memPD1_mem | 2.5% |
| NKCD16_NK | 2.5% |
| Tconv memCD56_total | 2.5% |
| Tconv memDR_mem | 2.5% |
| Tconv memDR_total | 2.5% |
| Tconv memCCR4_total | 2.5% |

**Total features selected by ElasticNet_Strict_t40**: 45

#### ElasticNet_Strict_t50

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| DR_CD8RO | 47.4% |
| CD16mono_myeloid | 44.7% |
| NKCD56hi_total | 28.9% |
| CD8 RO DR_CD8 | 26.3% |
| CD14+16+mono_myeloid | 15.8% |
| CD27IgD_Bcells | 13.2% |
| Tconv memKi67_mem | 10.5% |
| CD16mono_CD3neg | 10.5% |
| CD3hi_total | 10.5% |
| Tconv memCCR5_mem | 7.9% |
| CD14mono_myeloid | 7.9% |
| memory_Bcells | 5.3% |
| Treg memory_CD3 | 5.3% |
| Ki67_Bcells | 5.3% |
| Tconv memDR_Tconv | 5.3% |
| Bcells CD27posIgDneg_total | 5.3% |
| CD8 RO DR_CD3 | 2.6% |
| CD8pos_CD3 | 2.6% |
| NKCD56hi_NK | 2.6% |
| Tconv mem_Tconv | 2.6% |
| CD8 RO CD56_CD8 | 2.6% |
| CD8 RO CCR5_total | 2.6% |
| Tconv naive_CD3 | 2.6% |
| CD8 RA_CD3 | 2.6% |
| intB7_CD8RO | 2.6% |
| Tconv memKi67_total | 2.6% |
| CD8 RO PD1_CD3 | 2.6% |
| Tconv memPD1_mem | 2.6% |
| NKCD16_NK | 2.6% |
| Tconv memDR_mem | 2.6% |
| Tconv memDR_total | 2.6% |

**Total features selected by ElasticNet_Strict_t50**: 31

#### ElasticNet_Strict_t60

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD16mono_myeloid | 45.2% |
| DR_CD8RO | 19.4% |
| CD8 RO DR_CD8 | 16.1% |
| NKCD56hi_total | 16.1% |
| CD14+16+mono_myeloid | 12.9% |
| CD27IgD_Bcells | 12.9% |
| CD3hi_total | 9.7% |
| CD16mono_CD3neg | 9.7% |
| NKCD56hi_NK | 3.2% |
| Tconv memCCR5_mem | 3.2% |
| Tconv mem_Tconv | 3.2% |
| Tconv naive_CD3 | 3.2% |
| Tconv memDR_Tconv | 3.2% |
| CD14mono_myeloid | 3.2% |
| Tconv memKi67_total | 3.2% |
| CD8 RO PD1_CD3 | 3.2% |
| Tconv memDR_mem | 3.2% |

**Total features selected by ElasticNet_Strict_t60**: 17

#### ElasticNet_Strict_t70

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD16mono_myeloid | 55.0% |
| DR_CD8RO | 15.0% |
| NKCD56hi_total | 15.0% |
| CD27IgD_Bcells | 10.0% |
| CD3hi_total | 5.0% |
| CD14+16+mono_myeloid | 5.0% |
| NKCD56hi_NK | 5.0% |
| CD8 RO PD1_CD3 | 5.0% |
| CD16mono_CD3neg | 5.0% |

**Total features selected by ElasticNet_Strict_t70**: 9

#### ElasticNet_Strict_t80

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD16mono_myeloid | 55.6% |
| NKCD56hi_total | 22.2% |
| CD3hi_total | 11.1% |
| DR_CD8RO | 11.1% |

**Total features selected by ElasticNet_Strict_t80**: 4

#### FDR (p < 0.01)_t40

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Bcells CD27posIgDneg_total | 77.8% |
| CD8 RO DR_CD3 | 50.0% |
| Tconv naive_total | 47.2% |
| CD4 Treg_CD4 | 33.3% |
| Treg memory_CD4 | 33.3% |
| CD4 Tconv_total | 33.3% |
| CD16mono_myeloid | 22.2% |
| Tconv naive_CD3 | 22.2% |
| CD3neg_total | 19.4% |
| CD3pos_total | 19.4% |
| Tconv memDR_Tconv | 13.9% |
| Tconv naive_Tconv | 13.9% |
| Tconv mem_Tconv | 13.9% |
| Tconv memCD27_Tconv | 13.9% |
| CD27IgD_Bcells | 11.1% |
| Tconv memDR_CD3 | 11.1% |
| CD4 Tconv_CD3 | 8.3% |
| nonTnonB_CD3neg | 8.3% |
| Bcells_CD3neg | 8.3% |
| nonTnonB_total | 8.3% |
| Tconv memCCR4_total | 8.3% |
| CD14mono_total | 8.3% |
| CD14mono_myeloid | 8.3% |
| CD16mono_CD3neg | 8.3% |
| Treg memory_CD3 | 8.3% |
| Bcells memory_CD3neg | 5.6% |
| CD4 Treg _CD3 | 5.6% |
| CD8 RO_CD3 | 5.6% |
| CD14+16+mono_total | 5.6% |
| Tconv memCCR4_Tconv | 5.6% |
| CD8pos_CD3 | 2.8% |
| CD14mono_CD3neg | 2.8% |
| CD8 RO CD27_CD3 | 2.8% |
| Tconv mem_CD3 | 2.8% |
| Tconv memCXCR3_Tconv | 2.8% |
| CD8 RO CXCR3_CD3 | 2.8% |
| Tconv memCD27_total | 2.8% |
| CD8 RO CD56_CD3 | 2.8% |
| Tconv memintB7_Tconv | 2.8% |

**Total features selected by FDR (p < 0.01)_t40**: 39

#### FDR (p < 0.01)_t50

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Bcells CD27posIgDneg_total | 74.1% |
| Tconv naive_total | 44.4% |
| CD4 Tconv_total | 37.0% |
| Treg memory_CD4 | 37.0% |
| CD8 RO DR_CD3 | 33.3% |
| CD4 Treg_CD4 | 29.6% |
| CD16mono_myeloid | 14.8% |
| Tconv naive_CD3 | 14.8% |
| Tconv memDR_Tconv | 14.8% |
| Tconv mem_Tconv | 11.1% |
| Tconv naive_Tconv | 11.1% |
| Tconv memDR_CD3 | 11.1% |
| CD16mono_CD3neg | 11.1% |
| CD14mono_total | 7.4% |
| nonTnonB_total | 7.4% |
| CD14mono_myeloid | 7.4% |
| CD3pos_total | 7.4% |
| CD3neg_total | 7.4% |
| Tconv memCD27_Tconv | 7.4% |
| CD27IgD_Bcells | 7.4% |
| Bcells memory_CD3neg | 3.7% |
| CD14+16+mono_total | 3.7% |
| Treg memory_CD3 | 3.7% |
| CD4 Tconv_CD3 | 3.7% |
| CD8pos_CD3 | 3.7% |
| Tconv memCCR4_Tconv | 3.7% |
| CD8 RO_CD3 | 3.7% |
| Tconv memCXCR3_Tconv | 3.7% |
| Tconv memCCR4_total | 3.7% |

**Total features selected by FDR (p < 0.01)_t50**: 29

#### FDR (p < 0.01)_t60

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Bcells CD27posIgDneg_total | 70.0% |
| Tconv naive_total | 35.0% |
| CD8 RO DR_CD3 | 25.0% |
| Treg memory_CD4 | 25.0% |
| CD4 Treg_CD4 | 20.0% |
| CD16mono_myeloid | 15.0% |
| CD4 Tconv_total | 15.0% |
| Tconv mem_Tconv | 15.0% |
| Tconv naive_CD3 | 15.0% |
| Tconv naive_Tconv | 15.0% |
| CD3pos_total | 10.0% |
| CD3neg_total | 10.0% |
| Tconv memDR_Tconv | 10.0% |
| CD4 Tconv_CD3 | 5.0% |
| nonTnonB_total | 5.0% |
| CD8 RO_CD3 | 5.0% |
| CD8pos_CD3 | 5.0% |
| Tconv memCD27_Tconv | 5.0% |
| CD14mono_myeloid | 5.0% |
| Tconv memDR_CD3 | 5.0% |
| CD16mono_CD3neg | 5.0% |

**Total features selected by FDR (p < 0.01)_t60**: 21

#### FDR (p < 0.01)_t70

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Bcells CD27posIgDneg_total | 76.9% |
| Tconv naive_total | 46.2% |
| Tconv mem_Tconv | 23.1% |
| Tconv naive_CD3 | 15.4% |
| CD4 Tconv_total | 15.4% |
| CD8 RO DR_CD3 | 15.4% |
| Tconv naive_Tconv | 15.4% |
| Treg memory_CD4 | 15.4% |
| CD16mono_myeloid | 15.4% |
| CD3neg_total | 7.7% |
| CD3pos_total | 7.7% |
| CD4 Treg_CD4 | 7.7% |
| Tconv memCD27_Tconv | 7.7% |
| CD14mono_myeloid | 7.7% |
| CD16mono_CD3neg | 7.7% |

**Total features selected by FDR (p < 0.01)_t70**: 15

#### FDR (p < 0.01)_t80

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Bcells CD27posIgDneg_total | 60.0% |
| Tconv naive_total | 60.0% |
| Tconv naive_CD3 | 40.0% |
| Tconv mem_Tconv | 40.0% |
| Tconv naive_Tconv | 40.0% |
| CD16mono_myeloid | 40.0% |
| Treg memory_CD4 | 40.0% |
| CD8 RO DR_CD3 | 20.0% |
| CD4 Tconv_total | 20.0% |
| CD4 Treg_CD4 | 20.0% |
| Tconv memCD27_Tconv | 20.0% |

**Total features selected by FDR (p < 0.01)_t80**: 11

#### FDR (p < 0.05)_t40

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Bcells CD27posIgDneg_total | 97.5% |
| Tconv naive_total | 90.0% |
| CD8 RO DR_CD3 | 87.5% |
| Treg memory_CD4 | 82.5% |
| CD4 Treg_CD4 | 82.5% |
| Tconv memDR_Tconv | 75.0% |
| Tconv naive_CD3 | 65.0% |
| Tconv mem_Tconv | 65.0% |
| Tconv naive_Tconv | 62.5% |
| CD4 Tconv_total | 60.0% |
| CD27IgD_Bcells | 55.0% |
| Tconv memDR_CD3 | 55.0% |
| CD16mono_myeloid | 55.0% |
| CD3pos_total | 52.5% |
| CD3neg_total | 52.5% |
| nonTnonB_total | 47.5% |
| Treg memory_CD3 | 45.0% |
| Bcells memory_CD3neg | 37.5% |
| CD8pos_CD3 | 37.5% |
| nonTnonB_CD3neg | 32.5% |
| CD8 RO DR_CD8 | 32.5% |
| CD16mono_CD3neg | 30.0% |
| Bcells_CD3neg | 30.0% |
| Tconv memCD27_Tconv | 27.5% |
| CD4 Tconv_CD3 | 25.0% |
| CD14mono_total | 25.0% |
| CD8 RO PD1_CD3 | 25.0% |
| CD14mono_myeloid | 22.5% |
| CD4 Treg _CD3 | 22.5% |
| Tconv memCCR4_Tconv | 20.0% |
| CD8 RO CD56_CD3 | 20.0% |
| Bcells naive_CD3neg | 20.0% |
| CD4neg_CD3 | 20.0% |
| CD8  RO Ki67_CD3 | 17.5% |
| CD8 RO TIGIT_CD3 | 15.0% |
| Tconv mem_CD3 | 15.0% |
| CD8 RO_CD3 | 12.5% |
| CD14+16+mono_total | 12.5% |
| Bcells memory_total | 12.5% |
| Tconv memDR_mem | 12.5% |
| myeloid_total | 12.5% |
| CD14mono_CD3neg | 12.5% |
| Treg naive_total | 10.0% |
| CD14+16+mono_myeloid | 10.0% |
| Tconv memCCR4_total | 10.0% |
| Tconv memCXCR3_Tconv | 10.0% |
| Tconv memCD27_total | 10.0% |
| CD8 RO CXCR3_CD3 | 10.0% |
| CD8 RA CCR7 naive_CD8 | 7.5% |
| Tconv memTIGIT_Tconv | 7.5% |
| CD8 RO CD27_CD3 | 7.5% |
| CD8 RO DR_total | 7.5% |
| DR_CD8RO | 7.5% |
| Tconv memPD1_total | 7.5% |
| Bcells_total | 7.5% |
| CD14+16+mono_CD3neg | 7.5% |
| Tconv memKi67_Tconv | 5.0% |
| Tconv memCXCR3_CD3 | 5.0% |
| Tconv memCCR6_total | 5.0% |
| CD4 Tconv mem_total | 5.0% |
| Tconv memCCR6_Tconv | 5.0% |
| CD16+mono_total | 5.0% |
| Ki67_Bcells | 2.5% |
| Tconv memPD1_Tconv | 2.5% |
| Tconv memintB7_total | 2.5% |
| NK_nonTnonB | 2.5% |
| myeloid_CD3neg | 2.5% |
| Tconv memCD27_mem | 2.5% |
| Tconv memCXCR3_mem | 2.5% |
| NKCD56hi_NK | 2.5% |
| CD8 RO CXCR3_CD8 | 2.5% |
| CD3hi_CD3 | 2.5% |
| Bcells CD27negIgDneg_total | 2.5% |
| CD8 RO CCR5_CD3 | 2.5% |
| Tconv memCCR4_CD3 | 2.5% |
| Tconv memintB7_Tconv | 2.5% |
| CD8 RA_total | 2.5% |
| CD8 RA naive_total | 2.5% |
| Tconv memCD56_CD3 | 2.5% |
| Tconv memTIGIT_CD3 | 2.5% |
| Tconv memCD56_Tconv | 2.5% |

**Total features selected by FDR (p < 0.05)_t40**: 81

#### FDR (p < 0.05)_t50

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Bcells CD27posIgDneg_total | 97.5% |
| Tconv naive_total | 72.5% |
| CD8 RO DR_CD3 | 67.5% |
| Treg memory_CD4 | 65.0% |
| CD4 Treg_CD4 | 65.0% |
| Tconv naive_CD3 | 55.0% |
| Tconv memDR_Tconv | 55.0% |
| CD4 Tconv_total | 47.5% |
| Tconv naive_Tconv | 42.5% |
| Tconv mem_Tconv | 42.5% |
| CD3pos_total | 42.5% |
| CD3neg_total | 42.5% |
| CD27IgD_Bcells | 42.5% |
| CD16mono_myeloid | 40.0% |
| Treg memory_CD3 | 32.5% |
| Tconv memDR_CD3 | 30.0% |
| nonTnonB_total | 30.0% |
| CD16mono_CD3neg | 22.5% |
| Tconv memCD27_Tconv | 20.0% |
| nonTnonB_CD3neg | 20.0% |
| Bcells_CD3neg | 17.5% |
| Bcells memory_CD3neg | 17.5% |
| CD8pos_CD3 | 15.0% |
| CD4 Treg _CD3 | 15.0% |
| CD14mono_myeloid | 15.0% |
| CD8 RO CD56_CD3 | 15.0% |
| CD4 Tconv_CD3 | 15.0% |
| CD14mono_total | 12.5% |
| CD8 RO DR_CD8 | 12.5% |
| CD14+16+mono_total | 12.5% |
| CD8  RO Ki67_CD3 | 10.0% |
| CD4neg_CD3 | 10.0% |
| Tconv memCCR4_Tconv | 10.0% |
| Bcells naive_CD3neg | 10.0% |
| Tconv memDR_mem | 10.0% |
| CD8 RO_CD3 | 7.5% |
| CD8 RO CD27_CD3 | 7.5% |
| myeloid_total | 7.5% |
| CD14+16+mono_CD3neg | 7.5% |
| Bcells memory_total | 7.5% |
| CD8 RO PD1_CD3 | 7.5% |
| Tconv mem_CD3 | 7.5% |
| Tconv memCCR4_total | 7.5% |
| CD14mono_CD3neg | 5.0% |
| Tconv memCXCR3_Tconv | 5.0% |
| Tconv memCD27_total | 5.0% |
| CD14+16+mono_myeloid | 5.0% |
| DR_CD8RO | 2.5% |
| Tconv memintB7_total | 2.5% |
| CD8 RA CCR7 naive_CD8 | 2.5% |
| CD8 RO CXCR3_CD3 | 2.5% |
| Tconv memCXCR3_CD3 | 2.5% |
| Tconv memPD1_total | 2.5% |
| CD16+mono_total | 2.5% |
| CD8 RO TIGIT_CD3 | 2.5% |
| Tconv memintB7_Tconv | 2.5% |
| Tconv memTIGIT_Tconv | 2.5% |
| CD8 RA naive_total | 2.5% |
| Bcells_total | 2.5% |
| Tconv memCD56_CD3 | 2.5% |

**Total features selected by FDR (p < 0.05)_t50**: 60

#### FDR (p < 0.05)_t60

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Bcells CD27posIgDneg_total | 86.1% |
| Tconv naive_total | 72.2% |
| CD8 RO DR_CD3 | 63.9% |
| CD4 Treg_CD4 | 55.6% |
| Treg memory_CD4 | 55.6% |
| CD4 Tconv_total | 50.0% |
| Tconv memDR_Tconv | 38.9% |
| CD3pos_total | 36.1% |
| CD3neg_total | 36.1% |
| Tconv naive_CD3 | 33.3% |
| Tconv mem_Tconv | 33.3% |
| CD27IgD_Bcells | 30.6% |
| Tconv naive_Tconv | 27.8% |
| CD16mono_myeloid | 25.0% |
| nonTnonB_total | 22.2% |
| Tconv memDR_CD3 | 19.4% |
| Bcells memory_CD3neg | 16.7% |
| CD4 Tconv_CD3 | 13.9% |
| Treg memory_CD3 | 13.9% |
| Tconv memCD27_Tconv | 13.9% |
| CD8 RO CD56_CD3 | 11.1% |
| CD4 Treg _CD3 | 11.1% |
| CD14mono_myeloid | 11.1% |
| CD8 RO DR_CD8 | 11.1% |
| CD14+16+mono_total | 8.3% |
| CD8pos_CD3 | 8.3% |
| Bcells_CD3neg | 8.3% |
| nonTnonB_CD3neg | 8.3% |
| CD16mono_CD3neg | 8.3% |
| CD14mono_total | 5.6% |
| CD8 RO CD27_CD3 | 5.6% |
| Tconv mem_CD3 | 5.6% |
| Tconv memCCR4_total | 5.6% |
| myeloid_total | 5.6% |
| Bcells memory_total | 5.6% |
| CD8 RO_CD3 | 5.6% |
| CD8 RO PD1_CD3 | 5.6% |
| Tconv memDR_mem | 5.6% |
| CD8  RO Ki67_CD3 | 2.8% |
| CD8 RO CXCR3_CD3 | 2.8% |
| Tconv memCCR4_Tconv | 2.8% |
| CD14mono_CD3neg | 2.8% |
| Tconv memCXCR3_CD3 | 2.8% |
| Tconv memCXCR3_Tconv | 2.8% |
| CD16+mono_total | 2.8% |
| Tconv memPD1_total | 2.8% |
| Tconv memintB7_Tconv | 2.8% |
| CD14+16+mono_CD3neg | 2.8% |
| CD14+16+mono_myeloid | 2.8% |
| CD4neg_CD3 | 2.8% |

**Total features selected by FDR (p < 0.05)_t60**: 50

#### FDR (p < 0.05)_t70

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Bcells CD27posIgDneg_total | 80.6% |
| Tconv naive_total | 54.8% |
| CD8 RO DR_CD3 | 48.4% |
| Treg memory_CD4 | 48.4% |
| CD4 Tconv_total | 41.9% |
| CD4 Treg_CD4 | 35.5% |
| Tconv mem_Tconv | 29.0% |
| Tconv naive_CD3 | 25.8% |
| Tconv naive_Tconv | 25.8% |
| Tconv memDR_Tconv | 25.8% |
| CD16mono_myeloid | 22.6% |
| CD3neg_total | 22.6% |
| CD3pos_total | 22.6% |
| CD4 Tconv_CD3 | 12.9% |
| nonTnonB_total | 12.9% |
| CD27IgD_Bcells | 12.9% |
| Tconv memDR_CD3 | 12.9% |
| CD8pos_CD3 | 9.7% |
| Tconv memCD27_Tconv | 9.7% |
| Treg memory_CD3 | 9.7% |
| CD16mono_CD3neg | 9.7% |
| CD14mono_total | 6.5% |
| Bcells memory_CD3neg | 6.5% |
| CD8 RO CD56_CD3 | 6.5% |
| CD8 RO_CD3 | 3.2% |
| CD8 RO CD27_CD3 | 3.2% |
| Tconv memCCR4_Tconv | 3.2% |
| CD8 RO DR_CD8 | 3.2% |
| CD14mono_myeloid | 3.2% |
| Tconv memCXCR3_Tconv | 3.2% |
| Tconv memDR_mem | 3.2% |
| CD14+16+mono_total | 3.2% |
| nonTnonB_CD3neg | 3.2% |
| CD14+16+mono_CD3neg | 3.2% |
| Bcells_CD3neg | 3.2% |
| CD14+16+mono_myeloid | 3.2% |
| Bcells memory_total | 3.2% |
| CD4 Treg _CD3 | 3.2% |
| Tconv memCCR4_total | 3.2% |

**Total features selected by FDR (p < 0.05)_t70**: 39

#### FDR (p < 0.05)_t80

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Bcells CD27posIgDneg_total | 72.4% |
| Tconv naive_total | 44.8% |
| CD8 RO DR_CD3 | 37.9% |
| Treg memory_CD4 | 27.6% |
| CD4 Treg_CD4 | 24.1% |
| CD4 Tconv_total | 20.7% |
| Tconv memDR_Tconv | 17.2% |
| CD16mono_myeloid | 17.2% |
| Tconv naive_CD3 | 13.8% |
| CD3pos_total | 10.3% |
| CD3neg_total | 10.3% |
| nonTnonB_total | 10.3% |
| Tconv naive_Tconv | 10.3% |
| Tconv mem_Tconv | 10.3% |
| Bcells memory_CD3neg | 6.9% |
| Tconv memCD27_Tconv | 6.9% |
| CD27IgD_Bcells | 6.9% |
| CD16mono_CD3neg | 6.9% |
| Treg memory_CD3 | 6.9% |
| CD14mono_total | 3.4% |
| CD8 RO_CD3 | 3.4% |
| Tconv memCCR4_Tconv | 3.4% |
| CD8pos_CD3 | 3.4% |
| CD4 Tconv_CD3 | 3.4% |
| CD8 RO DR_CD8 | 3.4% |
| CD14mono_myeloid | 3.4% |
| CD8 RO CD56_CD3 | 3.4% |
| Tconv memDR_mem | 3.4% |
| nonTnonB_CD3neg | 3.4% |
| Bcells_CD3neg | 3.4% |
| CD4 Treg _CD3 | 3.4% |
| Tconv memCCR4_total | 3.4% |

**Total features selected by FDR (p < 0.05)_t80**: 32

#### FDR (p < 0.1)_t40

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Tconv naive_total | 97.5% |
| Bcells CD27posIgDneg_total | 97.5% |
| Treg memory_CD4 | 97.5% |
| CD8 RO DR_CD3 | 95.0% |
| CD4 Treg_CD4 | 92.5% |
| Tconv memDR_Tconv | 85.0% |
| CD4 Tconv_total | 82.5% |
| CD27IgD_Bcells | 82.5% |
| Tconv naive_CD3 | 82.5% |
| Tconv mem_Tconv | 77.5% |
| CD16mono_myeloid | 77.5% |
| Tconv naive_Tconv | 75.0% |
| CD3pos_total | 75.0% |
| CD3neg_total | 75.0% |
| Treg memory_CD3 | 72.5% |
| Tconv memDR_CD3 | 70.0% |
| nonTnonB_total | 62.5% |
| CD4 Treg _CD3 | 60.0% |
| Bcells memory_CD3neg | 57.5% |
| CD14mono_total | 55.0% |
| CD8 RO DR_CD8 | 52.5% |
| CD16mono_CD3neg | 50.0% |
| CD8pos_CD3 | 47.5% |
| Tconv memCD27_Tconv | 45.0% |
| Tconv memDR_mem | 45.0% |
| CD4neg_CD3 | 42.5% |
| Bcells_CD3neg | 42.5% |
| CD4 Tconv_CD3 | 42.5% |
| nonTnonB_CD3neg | 42.5% |
| Bcells naive_CD3neg | 40.0% |
| CD8  RO Ki67_CD3 | 40.0% |
| CD8 RO_CD3 | 37.5% |
| Tconv memCCR4_Tconv | 37.5% |
| CD14mono_myeloid | 35.0% |
| CD8 RO PD1_CD3 | 35.0% |
| CD14+16+mono_total | 35.0% |
| Bcells memory_total | 32.5% |
| CD8 RO CD56_CD3 | 32.5% |
| myeloid_total | 27.5% |
| CD14mono_CD3neg | 27.5% |
| Tconv mem_CD3 | 25.0% |
| Tconv memCXCR3_Tconv | 25.0% |
| CD8 RO DR_total | 25.0% |
| CD8 RO CD27_CD3 | 25.0% |
| DR_CD8RO | 25.0% |
| CD8 RO TIGIT_CD3 | 22.5% |
| Bcells_total | 22.5% |
| CD8 RA CCR7 naive_CD8 | 20.0% |
| Tconv memCD27_CD3 | 17.5% |
| Ki67_Bcells | 17.5% |
| Tconv memPD1_total | 17.5% |
| CD8 RO CXCR3_CD3 | 17.5% |
| CD14+16+mono_myeloid | 17.5% |
| Tconv memCD27_total | 17.5% |
| CD8 RA naive_total | 15.0% |
| Treg naive_total | 15.0% |
| Tconv memPD1_Tconv | 15.0% |
| Tconv memintB7_Tconv | 15.0% |
| Tconv memCCR4_total | 15.0% |
| CD4 Tconv mem_total | 12.5% |
| Tconv memCCR6_Tconv | 12.5% |
| CD14+16+mono_CD3neg | 10.0% |
| Tconv memKi67_Tconv | 10.0% |
| Tconv memCXCR3_CD3 | 10.0% |
| Tconv memCD56_Tconv | 10.0% |
| Tconv memTIGIT_Tconv | 10.0% |
| CD8 ncytotox RO CCR4_CD3 | 7.5% |
| CD8 RO CD56_CD8 | 7.5% |
| CD8 RO CXCR3_CD8 | 7.5% |
| Tconv memCCR4_CD3 | 7.5% |
| Tconv memTIGIT_total | 7.5% |
| Tconv memintB7_mem | 5.0% |
| CD8 RO CCR5_CD3 | 5.0% |
| Bcells naive_total | 5.0% |
| Tconv memintB7_total | 5.0% |
| Bcells Ki67_CD3neg | 5.0% |
| Tconv memCCR6_total | 5.0% |
| Tconv memCD56_CD3 | 5.0% |
| NKCD16_NK | 5.0% |
| CD8 RA_total | 5.0% |
| CD16+mono_total | 5.0% |
| Tconv memTIGIT_CD3 | 5.0% |
| Tconv memCD27_mem | 5.0% |
| Tconv memKi67_CD3 | 2.5% |
| Ki67_CD8RO | 2.5% |
| Tconv memCCR4_mem | 2.5% |
| myeloid_CD3neg | 2.5% |
| Bcells CD27negIgDneg_total | 2.5% |
| NK Ki67_nonTnonB | 2.5% |
| NK_nonTnonB | 2.5% |
| NKCD16_nonTnonB | 2.5% |
| CD8 RO CD56_total | 2.5% |
| Tconv memCXCR3_mem | 2.5% |
| Tconv memCCR6_CD3 | 2.5% |
| NKCD56hi_NK | 2.5% |
| Tconv memKi67_total | 2.5% |
| CD3hi_CD3 | 2.5% |
| CD8 RA_CD3 | 2.5% |
| CD8 RO intB7_CD3 | 2.5% |
| CXCR3_CD8RO | 2.5% |
| Tconv memDR_total | 2.5% |
| Tconv memintB7_CD3 | 2.5% |
| CD8 RO CCR6_CD3 | 2.5% |

**Total features selected by FDR (p < 0.1)_t40**: 103

#### FDR (p < 0.1)_t50

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Bcells CD27posIgDneg_total | 97.5% |
| Tconv naive_total | 90.0% |
| CD8 RO DR_CD3 | 90.0% |
| Treg memory_CD4 | 90.0% |
| CD4 Treg_CD4 | 80.0% |
| Tconv naive_CD3 | 75.0% |
| Tconv memDR_Tconv | 72.5% |
| CD4 Tconv_total | 70.0% |
| Tconv mem_Tconv | 62.5% |
| CD27IgD_Bcells | 62.5% |
| Tconv memDR_CD3 | 62.5% |
| Tconv naive_Tconv | 62.5% |
| CD16mono_myeloid | 60.0% |
| CD3neg_total | 55.0% |
| CD3pos_total | 55.0% |
| Treg memory_CD3 | 55.0% |
| nonTnonB_total | 50.0% |
| CD8 RO DR_CD8 | 47.5% |
| CD4 Treg _CD3 | 42.5% |
| Tconv memCD27_Tconv | 35.0% |
| CD8pos_CD3 | 35.0% |
| CD16mono_CD3neg | 35.0% |
| Bcells memory_CD3neg | 32.5% |
| Bcells_CD3neg | 32.5% |
| CD14mono_total | 32.5% |
| nonTnonB_CD3neg | 32.5% |
| CD4 Tconv_CD3 | 30.0% |
| CD4neg_CD3 | 27.5% |
| CD8 RO CD56_CD3 | 27.5% |
| CD8  RO Ki67_CD3 | 25.0% |
| Bcells naive_CD3neg | 25.0% |
| CD8 RO PD1_CD3 | 22.5% |
| Tconv memDR_mem | 20.0% |
| Tconv memCCR4_Tconv | 20.0% |
| CD14mono_myeloid | 17.5% |
| CD14+16+mono_total | 17.5% |
| CD8 RO_CD3 | 17.5% |
| Tconv mem_CD3 | 17.5% |
| myeloid_total | 15.0% |
| Bcells memory_total | 15.0% |
| CD8 RO TIGIT_CD3 | 15.0% |
| CD8 RO DR_total | 15.0% |
| CD14+16+mono_myeloid | 12.5% |
| Ki67_Bcells | 12.5% |
| CD14mono_CD3neg | 12.5% |
| Tconv memCXCR3_Tconv | 12.5% |
| CD14+16+mono_CD3neg | 10.0% |
| Treg naive_total | 10.0% |
| CD8 RO CD27_CD3 | 10.0% |
| Tconv memCD27_total | 10.0% |
| Tconv memPD1_total | 10.0% |
| Bcells_total | 7.5% |
| CD4 Tconv mem_total | 7.5% |
| Tconv memCD56_Tconv | 7.5% |
| CD8 RA CCR7 naive_CD8 | 7.5% |
| DR_CD8RO | 7.5% |
| Tconv memCXCR3_CD3 | 7.5% |
| Tconv memCCR4_total | 7.5% |
| Tconv memKi67_Tconv | 5.0% |
| Tconv memTIGIT_Tconv | 5.0% |
| Tconv memCCR6_total | 5.0% |
| Tconv memintB7_Tconv | 5.0% |
| CD8 RA naive_total | 5.0% |
| Tconv memCD27_CD3 | 5.0% |
| CD8 RO CXCR3_CD3 | 5.0% |
| CD16+mono_total | 5.0% |
| Ki67_CD8RO | 2.5% |
| Tconv memPD1_Tconv | 2.5% |
| Tconv memintB7_total | 2.5% |
| NK_nonTnonB | 2.5% |
| myeloid_CD3neg | 2.5% |
| Tconv memCD27_mem | 2.5% |
| Bcells CD27negIgDneg_total | 2.5% |
| Tconv memCXCR3_mem | 2.5% |
| Tconv memTIGIT_total | 2.5% |
| CD3hi_CD3 | 2.5% |
| NKCD16_nonTnonB | 2.5% |
| Tconv memKi67_total | 2.5% |
| CD8 RO CCR5_CD3 | 2.5% |
| CD8 RO CD56_CD8 | 2.5% |
| CD8 RO intB7_CD3 | 2.5% |
| Tconv memintB7_mem | 2.5% |
| CD8 RA_total | 2.5% |
| CD8 ncytotox RO CCR4_CD3 | 2.5% |
| Tconv memCD56_CD3 | 2.5% |

**Total features selected by FDR (p < 0.1)_t50**: 85

#### FDR (p < 0.1)_t60

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Bcells CD27posIgDneg_total | 92.5% |
| Tconv naive_total | 82.5% |
| CD8 RO DR_CD3 | 80.0% |
| CD4 Treg_CD4 | 70.0% |
| Treg memory_CD4 | 70.0% |
| CD4 Tconv_total | 62.5% |
| Tconv naive_CD3 | 62.5% |
| Tconv mem_Tconv | 55.0% |
| CD27IgD_Bcells | 55.0% |
| Tconv naive_Tconv | 52.5% |
| Tconv memDR_Tconv | 50.0% |
| CD16mono_myeloid | 47.5% |
| CD3pos_total | 45.0% |
| CD3neg_total | 45.0% |
| Tconv memDR_CD3 | 40.0% |
| Treg memory_CD3 | 37.5% |
| CD8 RO DR_CD8 | 35.0% |
| nonTnonB_total | 30.0% |
| CD8pos_CD3 | 25.0% |
| Bcells memory_CD3neg | 25.0% |
| CD4 Treg _CD3 | 22.5% |
| Tconv memCD27_Tconv | 22.5% |
| CD4 Tconv_CD3 | 20.0% |
| nonTnonB_CD3neg | 20.0% |
| Bcells_CD3neg | 20.0% |
| CD16mono_CD3neg | 15.0% |
| CD14+16+mono_total | 15.0% |
| CD4neg_CD3 | 15.0% |
| CD8 RO CD56_CD3 | 15.0% |
| Tconv memDR_mem | 15.0% |
| Tconv memCCR4_Tconv | 12.5% |
| Bcells naive_CD3neg | 12.5% |
| CD14mono_myeloid | 12.5% |
| Bcells memory_total | 12.5% |
| Tconv mem_CD3 | 10.0% |
| CD8 RO PD1_CD3 | 10.0% |
| CD8 RO DR_total | 10.0% |
| CD8 RO CD27_CD3 | 10.0% |
| CD8 RA CCR7 naive_CD8 | 7.5% |
| Tconv memCXCR3_Tconv | 7.5% |
| CD8 RO_CD3 | 7.5% |
| CD14+16+mono_myeloid | 7.5% |
| Tconv memCCR4_total | 7.5% |
| Tconv memCD27_total | 7.5% |
| CD14mono_total | 7.5% |
| CD8  RO Ki67_CD3 | 7.5% |
| CD16+mono_total | 5.0% |
| CD14+16+mono_CD3neg | 5.0% |
| Tconv memTIGIT_Tconv | 5.0% |
| myeloid_total | 5.0% |
| Ki67_Bcells | 5.0% |
| Tconv memCXCR3_CD3 | 5.0% |
| CD14mono_CD3neg | 5.0% |
| Treg naive_total | 5.0% |
| Bcells_total | 5.0% |
| CD8 RO TIGIT_CD3 | 5.0% |
| Tconv memCCR6_total | 2.5% |
| Tconv memKi67_Tconv | 2.5% |
| Tconv memintB7_total | 2.5% |
| NKCD16_nonTnonB | 2.5% |
| CD8 RO CXCR3_CD3 | 2.5% |
| NK_nonTnonB | 2.5% |
| Tconv memCXCR3_mem | 2.5% |
| Tconv memPD1_total | 2.5% |
| Tconv memTIGIT_total | 2.5% |
| Tconv memKi67_total | 2.5% |
| CD8 ncytotox RO CCR4_CD3 | 2.5% |
| Tconv memintB7_Tconv | 2.5% |
| Tconv memCD56_Tconv | 2.5% |
| CD4 Tconv mem_total | 2.5% |

**Total features selected by FDR (p < 0.1)_t60**: 70

#### FDR (p < 0.1)_t70

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Bcells CD27posIgDneg_total | 89.5% |
| Tconv naive_total | 76.3% |
| CD8 RO DR_CD3 | 60.5% |
| CD4 Treg_CD4 | 57.9% |
| Treg memory_CD4 | 52.6% |
| CD4 Tconv_total | 50.0% |
| Tconv naive_CD3 | 44.7% |
| CD27IgD_Bcells | 42.1% |
| Tconv mem_Tconv | 39.5% |
| Tconv naive_Tconv | 39.5% |
| Tconv memDR_Tconv | 36.8% |
| CD3neg_total | 28.9% |
| CD16mono_myeloid | 28.9% |
| CD3pos_total | 28.9% |
| Tconv memDR_CD3 | 26.3% |
| nonTnonB_total | 18.4% |
| CD8 RO DR_CD8 | 18.4% |
| Tconv memCD27_Tconv | 18.4% |
| CD8pos_CD3 | 15.8% |
| Treg memory_CD3 | 15.8% |
| Tconv memCCR4_Tconv | 13.2% |
| CD8 RO CD56_CD3 | 13.2% |
| nonTnonB_CD3neg | 10.5% |
| Bcells memory_CD3neg | 10.5% |
| CD16mono_CD3neg | 10.5% |
| CD4 Tconv_CD3 | 10.5% |
| Bcells_CD3neg | 10.5% |
| CD14mono_myeloid | 10.5% |
| CD4neg_CD3 | 7.9% |
| Bcells memory_total | 7.9% |
| CD14mono_total | 5.3% |
| CD8 RO PD1_CD3 | 5.3% |
| CD8 RO_CD3 | 5.3% |
| Tconv memDR_mem | 5.3% |
| Bcells naive_CD3neg | 5.3% |
| CD14+16+mono_total | 5.3% |
| Tconv memCCR4_total | 5.3% |
| CD8 RO CD27_CD3 | 5.3% |
| CD4 Treg _CD3 | 5.3% |
| Tconv memintB7_total | 2.6% |
| CD8  RO Ki67_CD3 | 2.6% |
| Tconv mem_CD3 | 2.6% |
| CD14mono_CD3neg | 2.6% |
| Tconv memCXCR3_CD3 | 2.6% |
| CD8 RA CCR7 naive_CD8 | 2.6% |
| myeloid_total | 2.6% |
| Tconv memCXCR3_Tconv | 2.6% |
| CD8 RO CXCR3_CD3 | 2.6% |
| CD8 RO TIGIT_CD3 | 2.6% |
| Tconv memPD1_total | 2.6% |
| Tconv memintB7_Tconv | 2.6% |
| CD14+16+mono_CD3neg | 2.6% |
| CD14+16+mono_myeloid | 2.6% |
| Bcells_total | 2.6% |

**Total features selected by FDR (p < 0.1)_t70**: 54

#### FDR (p < 0.1)_t80

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Bcells CD27posIgDneg_total | 84.8% |
| Tconv naive_total | 69.7% |
| CD8 RO DR_CD3 | 57.6% |
| Treg memory_CD4 | 42.4% |
| CD4 Treg_CD4 | 36.4% |
| CD4 Tconv_total | 30.3% |
| Tconv memDR_Tconv | 30.3% |
| CD27IgD_Bcells | 24.2% |
| CD3neg_total | 21.2% |
| CD3pos_total | 21.2% |
| CD16mono_myeloid | 21.2% |
| Tconv naive_Tconv | 21.2% |
| Tconv mem_Tconv | 21.2% |
| Tconv naive_CD3 | 21.2% |
| CD8pos_CD3 | 15.2% |
| Tconv memCD27_Tconv | 15.2% |
| nonTnonB_total | 12.1% |
| CD8 RO CD56_CD3 | 9.1% |
| Tconv memDR_CD3 | 9.1% |
| CD4 Tconv_CD3 | 9.1% |
| CD16mono_CD3neg | 9.1% |
| CD8 RO DR_CD8 | 6.1% |
| Bcells memory_CD3neg | 6.1% |
| CD14+16+mono_total | 6.1% |
| Treg memory_CD3 | 6.1% |
| Bcells memory_total | 6.1% |
| CD8 RO_CD3 | 6.1% |
| nonTnonB_CD3neg | 6.1% |
| Bcells_CD3neg | 6.1% |
| myeloid_total | 3.0% |
| Tconv memintB7_total | 3.0% |
| CD8 RO CD27_CD3 | 3.0% |
| CD14mono_total | 3.0% |
| Tconv memCCR4_Tconv | 3.0% |
| CD8 RA CCR7 naive_CD8 | 3.0% |
| Tconv memCXCR3_Tconv | 3.0% |
| Tconv memCXCR3_CD3 | 3.0% |
| CD14mono_CD3neg | 3.0% |
| CD14mono_myeloid | 3.0% |
| Tconv memPD1_total | 3.0% |
| Tconv memDR_mem | 3.0% |
| CD4 Treg _CD3 | 3.0% |
| Tconv memCCR4_total | 3.0% |

**Total features selected by FDR (p < 0.1)_t80**: 43

#### LASSO_Lenient_t40

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD16mono_myeloid | 80.0% |
| DR_CD8RO | 80.0% |
| NKCD56hi_total | 65.0% |
| Ki67_Bcells | 60.0% |
| CD8 RO DR_CD8 | 60.0% |
| CD14+16+mono_myeloid | 47.5% |
| CD27IgD_Bcells | 45.0% |
| CD3hi_total | 40.0% |
| CD8pos_CD3 | 35.0% |
| Bcells memory_total | 35.0% |
| CD16mono_CD3neg | 27.5% |
| CD14mono_myeloid | 27.5% |
| CD8 RO CD56_CD8 | 25.0% |
| Bcells CD27posIgDneg_total | 22.5% |
| Treg memory_CD3 | 20.0% |
| Tconv memKi67_mem | 20.0% |
| Tconv memPD1_mem | 20.0% |
| memory_Bcells | 20.0% |
| intB7_CD8RO | 17.5% |
| CD8 RO DR_CD3 | 17.5% |
| Tconv mem_Tconv | 15.0% |
| Tconv memDR_CD3 | 15.0% |
| CD8 RO intB7_CD8 | 15.0% |
| CD8 RO PD1_CD3 | 15.0% |
| Tconv memDR_total | 15.0% |
| Tconv memDR_Tconv | 15.0% |
| Bcells CD27negIgDneg_total | 15.0% |
| Tconv memCCR4_mem | 12.5% |
| CD8 RO CXCR3_CD3 | 12.5% |
| NKCD16_NK | 12.5% |
| Tconv memCCR5_mem | 12.5% |
| Tconv memCCR6_total | 12.5% |
| Tconv memintB7_Tconv | 12.5% |
| CD8 RA CCR7 naive_CD8 | 12.5% |
| NK Ki67_total | 12.5% |
| Tconv memKi67_total | 10.0% |
| NKCD56hi_NK | 10.0% |
| Tconv memCD27_Tconv | 10.0% |
| Tconv memTIGIT_mem | 10.0% |
| Tconv memDR_mem | 10.0% |
| Tconv memCCR6_mem | 10.0% |
| Tconv memCD56_total | 10.0% |
| Treg memory_CD4 | 10.0% |
| Treg naive_total | 7.5% |
| Bcells naive_total | 7.5% |
| CD8 RO CD56_CD3 | 7.5% |
| CCR6_CD8RO | 7.5% |
| NK Ki67_NK | 7.5% |
| CD8 RA_CD3 | 7.5% |
| Bcells Ki67_CD3neg | 7.5% |
| CCR5_CD8RO | 7.5% |
| CD8 RO CXCR3_CD8 | 7.5% |
| CD8 RO TIGIT_CD3 | 5.0% |
| CD56_CD8RO | 5.0% |
| CCR4_CD8RO | 5.0% |
| Tconv memintB7_mem | 5.0% |
| CD27negIgDneg_Bcells | 5.0% |
| CD8 RO TIGIT_CD8 | 5.0% |
| Tconv memCXCR3_mem | 5.0% |
| CD4neg_CD3 | 5.0% |
| Tconv naive_CD3 | 5.0% |
| CD27_CD8RO | 5.0% |
| Treg memory_total | 5.0% |
| CD3hi_CD4neg | 5.0% |
| naive_Bcells | 5.0% |
| CD3hi_CD3 | 5.0% |
| Treg naive_CD3 | 5.0% |
| TIGIT_CD8RO | 2.5% |
| Tconv naive_total | 2.5% |
| CD8 RO intB7_total | 2.5% |
| CD3neg_total | 2.5% |
| Bcells Ki67_total | 2.5% |
| CD16+mono_total | 2.5% |
| CD3pos_total | 2.5% |
| CD4 Treg_CD4 | 2.5% |
| Bcells_total | 2.5% |
| CD8 RO Ki67_total | 2.5% |
| CD4 Tconv_CD3 | 2.5% |
| CD8 RA naive_CD3 | 2.5% |
| Tconv memCCR5_total | 2.5% |
| NKCD56hi_nonTnonB | 2.5% |
| CD8 RO CCR5_total | 2.5% |
| CD4 Tconv_total | 2.5% |
| Tconv memTIGIT_Tconv | 2.5% |
| CD4 Treg _CD3 | 2.5% |
| Tconv memCD27_mem | 2.5% |
| CD8 ncytotox RO CCR4_CD8ntox | 2.5% |
| CD8 RO CD56_total | 2.5% |
| Tconv memCCR4_total | 2.5% |
| Tconv memCXCR3_total | 2.5% |

**Total features selected by LASSO_Lenient_t40**: 90

#### LASSO_Lenient_t50

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD16mono_myeloid | 67.5% |
| DR_CD8RO | 60.0% |
| CD8 RO DR_CD8 | 42.5% |
| NKCD56hi_total | 40.0% |
| Ki67_Bcells | 35.0% |
| CD14+16+mono_myeloid | 30.0% |
| CD27IgD_Bcells | 25.0% |
| CD16mono_CD3neg | 22.5% |
| CD3hi_total | 22.5% |
| CD14mono_myeloid | 17.5% |
| Bcells CD27posIgDneg_total | 15.0% |
| CD8pos_CD3 | 15.0% |
| CD8 RO CD56_CD8 | 15.0% |
| Tconv memKi67_mem | 15.0% |
| Tconv memCCR5_mem | 12.5% |
| Bcells memory_total | 12.5% |
| Tconv memPD1_mem | 10.0% |
| Tconv memintB7_Tconv | 10.0% |
| Bcells CD27negIgDneg_total | 10.0% |
| Treg memory_CD3 | 10.0% |
| memory_Bcells | 10.0% |
| CD8 RO PD1_CD3 | 7.5% |
| Tconv memDR_CD3 | 7.5% |
| Tconv memDR_Tconv | 7.5% |
| Tconv memCD56_total | 7.5% |
| CD8 RO DR_CD3 | 5.0% |
| NK Ki67_total | 5.0% |
| NKCD16_NK | 5.0% |
| Tconv memDR_total | 5.0% |
| Treg memory_CD4 | 5.0% |
| Tconv memDR_mem | 5.0% |
| NKCD56hi_NK | 5.0% |
| intB7_CD8RO | 5.0% |
| Tconv memCD27_Tconv | 5.0% |
| Tconv mem_Tconv | 5.0% |
| Tconv memKi67_total | 5.0% |
| CCR5_CD8RO | 5.0% |
| Tconv memCXCR3_mem | 5.0% |
| Tconv memCCR4_mem | 5.0% |
| CD8 RO CXCR3_CD8 | 5.0% |
| CD8 RA_CD3 | 5.0% |
| CD27negIgDneg_Bcells | 5.0% |
| NK Ki67_NK | 2.5% |
| CD3pos_total | 2.5% |
| CD3neg_total | 2.5% |
| CD8 RO TIGIT_CD3 | 2.5% |
| CD8 RO CD56_CD3 | 2.5% |
| Tconv naive_total | 2.5% |
| CD8 RA CCR7 naive_CD8 | 2.5% |
| CD8 RO Ki67_total | 2.5% |
| CD4 Tconv_CD3 | 2.5% |
| CD27_CD8RO | 2.5% |
| CD8 RO CCR5_total | 2.5% |
| Tconv naive_CD3 | 2.5% |
| Tconv memTIGIT_Tconv | 2.5% |
| Bcells naive_total | 2.5% |
| Treg naive_CD3 | 2.5% |
| CD3hi_CD4neg | 2.5% |
| Tconv memCCR4_total | 2.5% |

**Total features selected by LASSO_Lenient_t50**: 59

#### LASSO_Lenient_t60

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD16mono_myeloid | 60.0% |
| DR_CD8RO | 45.0% |
| NKCD56hi_total | 27.5% |
| CD8 RO DR_CD8 | 27.5% |
| CD14+16+mono_myeloid | 20.0% |
| Ki67_Bcells | 20.0% |
| CD27IgD_Bcells | 15.0% |
| CD8pos_CD3 | 12.5% |
| CD16mono_CD3neg | 12.5% |
| CD14mono_myeloid | 12.5% |
| Treg memory_CD3 | 10.0% |
| Tconv memintB7_Tconv | 7.5% |
| Bcells memory_total | 7.5% |
| CD3hi_total | 7.5% |
| Tconv memKi67_mem | 7.5% |
| NKCD56hi_NK | 5.0% |
| Tconv memDR_Tconv | 5.0% |
| Bcells CD27posIgDneg_total | 5.0% |
| Tconv memCCR5_mem | 5.0% |
| CD8 RO CD56_CD8 | 5.0% |
| CD8 RO DR_CD3 | 5.0% |
| Tconv memPD1_mem | 5.0% |
| Tconv memCD27_Tconv | 2.5% |
| Bcells CD27negIgDneg_total | 2.5% |
| Tconv memDR_CD3 | 2.5% |
| memory_Bcells | 2.5% |
| Tconv memCCR4_mem | 2.5% |
| CD8 RO CCR5_total | 2.5% |
| Treg memory_CD4 | 2.5% |
| Tconv memKi67_total | 2.5% |
| CD8 RO PD1_CD3 | 2.5% |
| Tconv naive_CD3 | 2.5% |
| CD8 RO CXCR3_CD8 | 2.5% |
| CD8 RA_CD3 | 2.5% |
| Tconv memCXCR3_mem | 2.5% |
| NKCD16_NK | 2.5% |
| Tconv memDR_mem | 2.5% |
| Tconv memCD56_total | 2.5% |
| CD3hi_CD4neg | 2.5% |
| Tconv memCCR4_total | 2.5% |

**Total features selected by LASSO_Lenient_t60**: 40

#### LASSO_Lenient_t70

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD16mono_myeloid | 54.5% |
| DR_CD8RO | 33.3% |
| NKCD56hi_total | 21.2% |
| CD14+16+mono_myeloid | 21.2% |
| Ki67_Bcells | 12.1% |
| CD27IgD_Bcells | 9.1% |
| Tconv memKi67_mem | 6.1% |
| CD14mono_myeloid | 6.1% |
| CD16mono_CD3neg | 6.1% |
| NKCD56hi_NK | 3.0% |
| CD3hi_total | 3.0% |
| Tconv memCCR5_mem | 3.0% |
| Tconv memCD27_Tconv | 3.0% |
| Tconv memDR_Tconv | 3.0% |
| Tconv naive_CD3 | 3.0% |
| CD8 RO DR_CD8 | 3.0% |
| CD8pos_CD3 | 3.0% |
| Tconv memKi67_total | 3.0% |
| CD8 RO PD1_CD3 | 3.0% |
| Tconv memPD1_mem | 3.0% |
| NKCD16_NK | 3.0% |
| Treg memory_CD3 | 3.0% |
| Bcells memory_total | 3.0% |
| Tconv memintB7_Tconv | 3.0% |

**Total features selected by LASSO_Lenient_t70**: 24

#### LASSO_Lenient_t80

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD16mono_myeloid | 50.0% |
| DR_CD8RO | 16.7% |
| NKCD56hi_total | 12.5% |
| CD14+16+mono_myeloid | 8.3% |
| Ki67_Bcells | 8.3% |
| NKCD56hi_NK | 4.2% |
| CD3hi_total | 4.2% |
| Tconv memCCR5_mem | 4.2% |
| Tconv memCD27_Tconv | 4.2% |
| CD14mono_myeloid | 4.2% |
| CD27IgD_Bcells | 4.2% |
| CD8 RO PD1_CD3 | 4.2% |

**Total features selected by LASSO_Lenient_t80**: 12

#### LASSO_RFE_t40

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD16mono_myeloid | 80.0% |
| DR_CD8RO | 65.0% |
| CD8 RO DR_CD8 | 55.0% |
| CD27IgD_Bcells | 42.5% |
| Ki67_Bcells | 42.5% |
| NKCD56hi_total | 37.5% |
| CD8pos_CD3 | 35.0% |
| CD14+16+mono_myeloid | 32.5% |
| CD3hi_total | 27.5% |
| CD16mono_CD3neg | 25.0% |
| Bcells CD27posIgDneg_total | 22.5% |
| Bcells memory_total | 17.5% |
| CD14mono_myeloid | 17.5% |
| Treg memory_CD3 | 17.5% |
| Tconv memDR_CD3 | 15.0% |
| Bcells CD27negIgDneg_total | 12.5% |
| intB7_CD8RO | 12.5% |
| CD8 RO CD56_CD8 | 12.5% |
| NKCD16_NK | 12.5% |
| Tconv mem_Tconv | 12.5% |
| Tconv memDR_Tconv | 12.5% |
| CD8 RO DR_CD3 | 12.5% |
| Tconv memDR_mem | 10.0% |
| Tconv memintB7_Tconv | 10.0% |
| CD8 RO PD1_CD3 | 10.0% |
| Treg memory_CD4 | 10.0% |
| Tconv memDR_total | 10.0% |
| CD8 RA CCR7 naive_CD8 | 10.0% |
| Tconv memCCR6_total | 7.5% |
| CD8 RO CXCR3_CD8 | 7.5% |
| Tconv memPD1_mem | 7.5% |
| Tconv memCD27_Tconv | 7.5% |
| Tconv memTIGIT_mem | 7.5% |
| Tconv memCCR5_mem | 7.5% |
| Tconv memKi67_mem | 7.5% |
| memory_Bcells | 7.5% |
| NKCD56hi_NK | 7.5% |
| Tconv memCD56_total | 7.5% |
| Tconv naive_CD3 | 5.0% |
| NK Ki67_NK | 5.0% |
| CD8 RA_CD3 | 5.0% |
| CCR5_CD8RO | 5.0% |
| Treg naive_CD3 | 5.0% |
| CD8 RO CXCR3_CD3 | 5.0% |
| Tconv memCCR6_mem | 5.0% |
| Tconv memCXCR3_mem | 5.0% |
| Tconv memCCR4_mem | 5.0% |
| CD56_CD8RO | 2.5% |
| Tconv naive_total | 2.5% |
| CD3hi_CD3 | 2.5% |
| CD27negIgDneg_Bcells | 2.5% |
| Bcells Ki67_CD3neg | 2.5% |
| CD3neg_total | 2.5% |
| CD3pos_total | 2.5% |
| CD8 RO TIGIT_CD8 | 2.5% |
| naive_Bcells | 2.5% |
| CD8 RO CD56_CD3 | 2.5% |
| CD4 Tconv_CD3 | 2.5% |
| NK Ki67_total | 2.5% |
| CCR6_CD8RO | 2.5% |
| CD4neg_CD3 | 2.5% |
| Treg naive_total | 2.5% |
| CD4 Treg_CD4 | 2.5% |
| CD27_CD8RO | 2.5% |
| CD8 RO CCR5_total | 2.5% |
| NKCD56hi_nonTnonB | 2.5% |
| CD4 Tconv_total | 2.5% |
| Tconv memTIGIT_Tconv | 2.5% |
| Bcells naive_total | 2.5% |
| Tconv memKi67_total | 2.5% |
| CD8 RO intB7_CD8 | 2.5% |
| Tconv memCCR4_total | 2.5% |

**Total features selected by LASSO_RFE_t40**: 72

#### LASSO_RFE_t50

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD16mono_myeloid | 65.0% |
| DR_CD8RO | 45.0% |
| CD8 RO DR_CD8 | 37.5% |
| NKCD56hi_total | 25.0% |
| CD14+16+mono_myeloid | 25.0% |
| CD27IgD_Bcells | 25.0% |
| Ki67_Bcells | 22.5% |
| CD16mono_CD3neg | 22.5% |
| Bcells CD27posIgDneg_total | 15.0% |
| CD14mono_myeloid | 15.0% |
| CD3hi_total | 15.0% |
| CD8pos_CD3 | 10.0% |
| Tconv memintB7_Tconv | 10.0% |
| Treg memory_CD3 | 10.0% |
| Bcells CD27negIgDneg_total | 7.5% |
| Tconv memDR_Tconv | 7.5% |
| CD8 RO PD1_CD3 | 7.5% |
| Tconv memCCR5_mem | 7.5% |
| Tconv memCD27_Tconv | 5.0% |
| Bcells memory_total | 5.0% |
| Treg memory_CD4 | 5.0% |
| Tconv memPD1_mem | 5.0% |
| CD8 RO DR_CD3 | 5.0% |
| Tconv memDR_CD3 | 5.0% |
| NKCD16_NK | 5.0% |
| CD8 RO CXCR3_CD8 | 5.0% |
| NK Ki67_NK | 2.5% |
| NKCD56hi_NK | 2.5% |
| Tconv memCCR4_mem | 2.5% |
| CD3pos_total | 2.5% |
| CD3neg_total | 2.5% |
| Tconv memCD56_total | 2.5% |
| CD8 RA_CD3 | 2.5% |
| Tconv mem_Tconv | 2.5% |
| CCR5_CD8RO | 2.5% |
| Tconv naive_total | 2.5% |
| CD8 RO CCR5_total | 2.5% |
| Tconv memKi67_mem | 2.5% |
| Tconv naive_CD3 | 2.5% |
| intB7_CD8RO | 2.5% |
| Bcells naive_total | 2.5% |
| Treg naive_CD3 | 2.5% |
| Tconv memKi67_total | 2.5% |
| Tconv memCXCR3_mem | 2.5% |
| Tconv memDR_mem | 2.5% |
| Tconv memDR_total | 2.5% |
| Tconv memCCR4_total | 2.5% |

**Total features selected by LASSO_RFE_t50**: 47

#### LASSO_RFE_t60

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD16mono_myeloid | 55.0% |
| DR_CD8RO | 30.0% |
| CD8 RO DR_CD8 | 25.0% |
| NKCD56hi_total | 17.5% |
| CD14+16+mono_myeloid | 15.0% |
| CD27IgD_Bcells | 15.0% |
| CD8pos_CD3 | 10.0% |
| CD16mono_CD3neg | 10.0% |
| Treg memory_CD3 | 10.0% |
| CD3hi_total | 7.5% |
| Ki67_Bcells | 7.5% |
| CD8 RO DR_CD3 | 5.0% |
| Tconv memintB7_Tconv | 5.0% |
| CD14mono_myeloid | 5.0% |
| Bcells CD27posIgDneg_total | 5.0% |
| Tconv memDR_Tconv | 5.0% |
| NKCD56hi_NK | 2.5% |
| Tconv memCD27_Tconv | 2.5% |
| Tconv memCCR4_mem | 2.5% |
| Tconv memCCR5_mem | 2.5% |
| Tconv naive_CD3 | 2.5% |
| CD8 RO CCR5_total | 2.5% |
| Treg memory_CD4 | 2.5% |
| Tconv memKi67_total | 2.5% |
| CD8 RO PD1_CD3 | 2.5% |
| NKCD16_NK | 2.5% |
| Tconv memDR_mem | 2.5% |
| Tconv memCCR4_total | 2.5% |

**Total features selected by LASSO_RFE_t60**: 28

#### LASSO_RFE_t70

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD16mono_myeloid | 51.6% |
| DR_CD8RO | 19.4% |
| CD14+16+mono_myeloid | 12.9% |
| NKCD56hi_total | 12.9% |
| CD27IgD_Bcells | 9.7% |
| CD16mono_CD3neg | 6.5% |
| Ki67_Bcells | 6.5% |
| CD3hi_total | 3.2% |
| NKCD56hi_NK | 3.2% |
| CD8 RO DR_CD8 | 3.2% |
| Tconv memCD27_Tconv | 3.2% |
| Tconv memCCR5_mem | 3.2% |
| CD14mono_myeloid | 3.2% |
| Tconv memDR_Tconv | 3.2% |
| CD8pos_CD3 | 3.2% |
| NKCD16_NK | 3.2% |
| Treg memory_CD3 | 3.2% |
| Tconv memintB7_Tconv | 3.2% |

**Total features selected by LASSO_RFE_t70**: 18

#### LASSO_RFE_t80

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD16mono_myeloid | 47.6% |
| DR_CD8RO | 14.3% |
| Ki67_Bcells | 9.5% |
| NKCD56hi_total | 9.5% |
| CD3hi_total | 4.8% |
| Tconv memCD27_Tconv | 4.8% |
| CD14mono_myeloid | 4.8% |
| CD27IgD_Bcells | 4.8% |
| CD14+16+mono_myeloid | 4.8% |

**Total features selected by LASSO_RFE_t80**: 9

#### LASSO_Strict_t40

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD16mono_myeloid | 50.0% |
| DR_CD8RO | 42.5% |
| NKCD56hi_total | 30.0% |
| CD8 RO DR_CD8 | 30.0% |
| CD27IgD_Bcells | 20.0% |
| CD14+16+mono_myeloid | 15.0% |
| CD3hi_total | 12.5% |
| CD14mono_myeloid | 10.0% |
| CD16mono_CD3neg | 10.0% |
| Tconv memKi67_mem | 10.0% |
| Tconv memCCR5_mem | 7.5% |
| Bcells CD27posIgDneg_total | 7.5% |
| CD8 RO DR_CD3 | 7.5% |
| Ki67_Bcells | 7.5% |
| CD8 RO CD56_CD8 | 7.5% |
| Treg memory_CD3 | 7.5% |
| Tconv memDR_Tconv | 7.5% |
| Tconv memPD1_mem | 5.0% |
| intB7_CD8RO | 5.0% |
| Tconv memintB7_Tconv | 5.0% |
| CD8 RA CCR7 naive_CD8 | 2.5% |
| CD8 RO intB7_CD8 | 2.5% |
| Tconv mem_Tconv | 2.5% |
| CD3pos_total | 2.5% |
| CD8pos_CD3 | 2.5% |
| Tconv memCD27_Tconv | 2.5% |
| memory_Bcells | 2.5% |
| CD4 Treg_CD4 | 2.5% |
| CD8 RO CCR5_total | 2.5% |
| Bcells memory_total | 2.5% |
| NKCD56hi_NK | 2.5% |
| CD8 RA_CD3 | 2.5% |
| Tconv memKi67_total | 2.5% |
| Tconv memDR_CD3 | 2.5% |
| CD8 RO PD1_CD3 | 2.5% |
| NKCD16_NK | 2.5% |
| Tconv memDR_mem | 2.5% |
| Tconv memDR_total | 2.5% |

**Total features selected by LASSO_Strict_t40**: 38

#### LASSO_Strict_t50

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD16mono_myeloid | 46.9% |
| DR_CD8RO | 25.0% |
| CD8 RO DR_CD8 | 15.6% |
| NKCD56hi_total | 15.6% |
| CD14+16+mono_myeloid | 15.6% |
| CD27IgD_Bcells | 12.5% |
| CD16mono_CD3neg | 12.5% |
| Ki67_Bcells | 6.2% |
| CD3hi_total | 6.2% |
| Bcells CD27posIgDneg_total | 6.2% |
| Tconv memKi67_mem | 6.2% |
| CD8 RO CD56_CD8 | 3.1% |
| CD14mono_myeloid | 3.1% |
| Tconv memDR_Tconv | 3.1% |
| Tconv memCD27_Tconv | 3.1% |
| CD8 RO CCR5_total | 3.1% |
| Tconv memKi67_total | 3.1% |
| NKCD16_NK | 3.1% |
| Treg memory_CD3 | 3.1% |
| Tconv memDR_mem | 3.1% |

**Total features selected by LASSO_Strict_t50**: 20

#### LASSO_Strict_t60

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD16mono_myeloid | 50.0% |
| NKCD56hi_total | 18.2% |
| CD14+16+mono_myeloid | 13.6% |
| DR_CD8RO | 13.6% |
| CD3hi_total | 9.1% |
| CD8 RO DR_CD8 | 9.1% |
| CD27IgD_Bcells | 9.1% |
| Ki67_Bcells | 4.5% |
| Tconv memDR_Tconv | 4.5% |
| CD14mono_myeloid | 4.5% |
| CD16mono_CD3neg | 4.5% |

**Total features selected by LASSO_Strict_t60**: 11

#### LASSO_Strict_t70

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD16mono_myeloid | 53.8% |
| DR_CD8RO | 15.4% |
| NKCD56hi_total | 15.4% |
| CD3hi_total | 7.7% |
| CD27IgD_Bcells | 7.7% |

**Total features selected by LASSO_Strict_t70**: 5

#### LASSO_Strict_t80

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD16mono_myeloid | 60.0% |
| DR_CD8RO | 20.0% |
| NKCD56hi_total | 20.0% |

**Total features selected by LASSO_Strict_t80**: 3

#### LogisticRegression_Permutation_AboveMean_t40

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| DR_CD8RO | 51.6% |
| CD8 RO DR_CD8 | 35.5% |
| Bcells CD27posIgDneg_total | 32.3% |
| CD3hi_total | 16.1% |
| CD8 RO intB7_total | 16.1% |
| CD16mono_myeloid | 16.1% |
| Ki67_Bcells | 12.9% |
| CCR4_CD8RO | 12.9% |
| CD8 RO intB7_CD8 | 12.9% |
| CD27IgD_Bcells | 9.7% |
| Tconv memCCR5_mem | 9.7% |
| Bcells CD27negIgDneg_total | 9.7% |
| memory_Bcells | 9.7% |
| NKCD56hi_total | 6.5% |
| Tconv memCD56_total | 6.5% |
| CD8 RO intB7_CD3 | 3.2% |
| CD8 RA_CD3 | 3.2% |
| Bcells Ki67_total | 3.2% |
| CD3hi_CD3 | 3.2% |
| Tconv memDR_total | 3.2% |
| intB7_CD8RO | 3.2% |
| CD8 RO CD56_CD8 | 3.2% |
| CD8 RO DR_total | 3.2% |
| CD16+mono_total | 3.2% |
| CD16mono_CD3neg | 3.2% |

**Total features selected by LogisticRegression_Permutation_AboveMean_t40**: 25

#### LogisticRegression_Permutation_AboveMean_t50

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| DR_CD8RO | 42.3% |
| Bcells CD27posIgDneg_total | 23.1% |
| CD8 RO DR_CD8 | 23.1% |
| CD8 RO intB7_total | 11.5% |
| Ki67_Bcells | 11.5% |
| memory_Bcells | 11.5% |
| Tconv memCD56_total | 7.7% |
| CD3hi_total | 7.7% |
| CD8 RO intB7_CD8 | 7.7% |
| Tconv memCCR5_mem | 7.7% |
| CCR4_CD8RO | 7.7% |
| CD16mono_myeloid | 7.7% |
| CD8 RA_CD3 | 3.8% |
| NKCD56hi_total | 3.8% |
| Bcells CD27negIgDneg_total | 3.8% |
| Tconv memDR_total | 3.8% |

**Total features selected by LogisticRegression_Permutation_AboveMean_t50**: 16

#### LogisticRegression_Permutation_AboveMean_t60

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| DR_CD8RO | 50.0% |
| CD8 RO intB7_total | 14.3% |
| Bcells CD27posIgDneg_total | 14.3% |
| CD8 RO intB7_CD8 | 14.3% |
| CD8 RO DR_CD8 | 14.3% |
| CD3hi_total | 7.1% |
| CCR4_CD8RO | 7.1% |
| Ki67_Bcells | 7.1% |
| memory_Bcells | 7.1% |
| CD16mono_myeloid | 7.1% |

**Total features selected by LogisticRegression_Permutation_AboveMean_t60**: 10

#### LogisticRegression_Permutation_AboveMean_t70

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| DR_CD8RO | 50.0% |
| Bcells CD27posIgDneg_total | 20.0% |
| CD8 RO intB7_CD8 | 20.0% |
| CD8 RO intB7_total | 10.0% |
| CD3hi_total | 10.0% |
| Ki67_Bcells | 10.0% |
| CCR4_CD8RO | 10.0% |

**Total features selected by LogisticRegression_Permutation_AboveMean_t70**: 7

#### LogisticRegression_Permutation_AboveMean_t80

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD3hi_total | 33.3% |
| Ki67_Bcells | 33.3% |
| DR_CD8RO | 33.3% |

**Total features selected by LogisticRegression_Permutation_AboveMean_t80**: 3

#### LogisticRegression_Permutation_Top10%_t40

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Tconv memCXCR3_total | 100.0% |
| Tconv memCD27_total | 100.0% |
| Tconv memCD56_total | 100.0% |
| Tconv memintB7_total | 97.5% |
| Tconv memDR_total | 97.5% |
| Tconv naive_total | 97.5% |
| Tconv memKi67_total | 97.5% |
| Tconv memPD1_total | 97.5% |
| CD4 Treg_total | 92.5% |
| Tconv memTIGIT_total | 90.0% |
| CD3pos_total | 90.0% |
| Tconv memCCR6_total | 87.5% |
| CD4 Tconv mem_total | 85.0% |
| Tconv memCCR5_total | 85.0% |
| CD4 Tconv_total | 75.0% |
| Tconv memCCR4_total | 72.5% |
| DR_CD8RO | 42.5% |
| CD8 RO DR_CD8 | 27.5% |
| Bcells CD27posIgDneg_total | 25.0% |
| CD3hi_total | 10.0% |
| Ki67_Bcells | 10.0% |
| CD8 RO intB7_total | 10.0% |
| CCR4_CD8RO | 10.0% |
| CD16mono_myeloid | 7.5% |
| Bcells CD27negIgDneg_total | 7.5% |
| Tconv memCCR5_mem | 7.5% |
| memory_Bcells | 7.5% |
| CD8 RO intB7_CD8 | 5.0% |
| CD27IgD_Bcells | 5.0% |
| NKCD56hi_total | 5.0% |
| CD8 RO intB7_CD3 | 2.5% |
| CD8 RA_CD3 | 2.5% |
| CD3hi_CD3 | 2.5% |
| intB7_CD8RO | 2.5% |
| CD8 RO DR_total | 2.5% |
| CD16+mono_total | 2.5% |

**Total features selected by LogisticRegression_Permutation_Top10%_t40**: 36

#### LogisticRegression_Permutation_Top10%_t50

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Tconv memCD27_total | 97.5% |
| Tconv memCD56_total | 97.5% |
| Tconv memCXCR3_total | 97.5% |
| Tconv memKi67_total | 97.5% |
| Tconv memintB7_total | 97.5% |
| Tconv memPD1_total | 97.5% |
| Tconv memDR_total | 97.5% |
| Tconv naive_total | 95.0% |
| Tconv memTIGIT_total | 87.5% |
| CD4 Treg_total | 85.0% |
| CD4 Tconv mem_total | 82.5% |
| CD3pos_total | 80.0% |
| Tconv memCCR6_total | 75.0% |
| CD4 Tconv_total | 60.0% |
| Tconv memCCR4_total | 60.0% |
| Tconv memCCR5_total | 52.5% |
| DR_CD8RO | 25.0% |
| CD8 RO DR_CD8 | 15.0% |
| Bcells CD27posIgDneg_total | 12.5% |
| Ki67_Bcells | 7.5% |
| CD8 RO intB7_total | 7.5% |
| CD3hi_total | 5.0% |
| CD8 RO intB7_CD8 | 5.0% |
| Tconv memCCR5_mem | 5.0% |
| CCR4_CD8RO | 5.0% |
| CD16mono_myeloid | 5.0% |
| NKCD56hi_total | 2.5% |
| Bcells CD27negIgDneg_total | 2.5% |
| memory_Bcells | 2.5% |

**Total features selected by LogisticRegression_Permutation_Top10%_t50**: 29

#### LogisticRegression_Permutation_Top10%_t60

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Tconv memintB7_total | 97.5% |
| Tconv memCD27_total | 97.5% |
| Tconv memDR_total | 97.5% |
| Tconv memKi67_total | 97.5% |
| Tconv memPD1_total | 97.5% |
| Tconv memCD56_total | 95.0% |
| Tconv memCXCR3_total | 92.5% |
| Tconv naive_total | 90.0% |
| Tconv memTIGIT_total | 77.5% |
| CD3pos_total | 75.0% |
| CD4 Treg_total | 75.0% |
| CD4 Tconv mem_total | 70.0% |
| Tconv memCCR6_total | 60.0% |
| CD4 Tconv_total | 47.5% |
| Tconv memCCR4_total | 42.5% |
| Tconv memCCR5_total | 42.5% |
| DR_CD8RO | 17.5% |
| CD8 RO intB7_total | 5.0% |
| Bcells CD27posIgDneg_total | 5.0% |
| CD8 RO intB7_CD8 | 5.0% |
| CD8 RO DR_CD8 | 5.0% |
| CD3hi_total | 2.5% |
| CCR4_CD8RO | 2.5% |
| Ki67_Bcells | 2.5% |
| memory_Bcells | 2.5% |
| CD16mono_myeloid | 2.5% |

**Total features selected by LogisticRegression_Permutation_Top10%_t60**: 26

#### LogisticRegression_Permutation_Top10%_t70

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Tconv memKi67_total | 95.0% |
| Tconv memintB7_total | 95.0% |
| Tconv memCD56_total | 95.0% |
| Tconv memDR_total | 95.0% |
| Tconv memPD1_total | 95.0% |
| Tconv memCD27_total | 90.0% |
| Tconv memCXCR3_total | 87.5% |
| Tconv naive_total | 85.0% |
| Tconv memTIGIT_total | 72.5% |
| CD4 Treg_total | 67.5% |
| CD3pos_total | 60.0% |
| CD4 Tconv mem_total | 57.5% |
| Tconv memCCR6_total | 40.0% |
| Tconv memCCR4_total | 35.0% |
| Tconv memCCR5_total | 27.5% |
| CD4 Tconv_total | 27.5% |
| DR_CD8RO | 12.5% |
| Bcells CD27posIgDneg_total | 5.0% |
| CD8 RO intB7_CD8 | 5.0% |
| CD3hi_total | 2.5% |
| CD8 RO intB7_total | 2.5% |
| Ki67_Bcells | 2.5% |
| CCR4_CD8RO | 2.5% |

**Total features selected by LogisticRegression_Permutation_Top10%_t70**: 23

#### LogisticRegression_Permutation_Top10%_t80

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Tconv memCD56_total | 94.9% |
| Tconv memKi67_total | 94.9% |
| Tconv memintB7_total | 89.7% |
| Tconv memDR_total | 87.2% |
| Tconv memPD1_total | 87.2% |
| Tconv memCD27_total | 84.6% |
| Tconv memCXCR3_total | 76.9% |
| Tconv naive_total | 74.4% |
| Tconv memTIGIT_total | 59.0% |
| CD3pos_total | 51.3% |
| CD4 Treg_total | 43.6% |
| CD4 Tconv mem_total | 35.9% |
| Tconv memCCR6_total | 23.1% |
| Tconv memCCR4_total | 15.4% |
| CD4 Tconv_total | 12.8% |
| Tconv memCCR5_total | 7.7% |
| CD3hi_total | 2.6% |
| Ki67_Bcells | 2.6% |
| DR_CD8RO | 2.6% |

**Total features selected by LogisticRegression_Permutation_Top10%_t80**: 19

#### Mutual Information (Top 10%)_t40

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Bcells CD27posIgDneg_total | 42.5% |
| Tconv mem_Tconv | 37.5% |
| Tconv naive_Tconv | 35.0% |
| CD8pos_CD3 | 35.0% |
| CD27IgD_Bcells | 32.5% |
| Tconv memCD27_CD3 | 30.0% |
| nonTnonB_total | 30.0% |
| CD14mono_total | 30.0% |
| CD8 ncytotox RO CCR4_CD8ntox | 27.5% |
| Treg memory_CD4 | 27.5% |
| CD4 Treg_CD4 | 25.0% |
| CD8 RO DR_CD3 | 25.0% |
| CD3neg_total | 25.0% |
| CD3pos_total | 25.0% |
| nonTnonB_CD3neg | 25.0% |
| CD8 RO_CD3 | 22.5% |
| Tconv naive_total | 22.5% |
| Treg memory_CD3 | 22.5% |
| CD8  RO Ki67_CD3 | 20.0% |
| CD8 RA_CD8 | 20.0% |
| CD14mono_CD3neg | 17.5% |
| Tconv naive_CD3 | 17.5% |
| CD8 RA CCR7 naive_CD8 | 15.0% |
| Bcells_CD3neg | 12.5% |
| intB7_CD8RO | 12.5% |
| NKCD16_CD3neg | 12.5% |
| CD16mono_myeloid | 12.5% |
| CD4 Treg_total | 10.0% |
| Treg naive_CD3 | 10.0% |
| CD8 RO CCR5_CD3 | 10.0% |
| CD4 Treg _CD3 | 10.0% |
| CD8 RO CD27_CD3 | 10.0% |
| Treg naive_CD4 | 10.0% |
| Tconv memCCR6_CD3 | 10.0% |
| Tconv memTIGIT_CD3 | 10.0% |
| Bcells memory_CD3neg | 10.0% |
| Ki67_Bcells | 10.0% |
| Tconv memKi67_CD3 | 10.0% |
| Treg naive_total | 10.0% |
| myeloid_total | 7.5% |
| Tconv memintB7_Tconv | 7.5% |
| CD16mono_CD3neg | 7.5% |
| CD8 RO CCR6_CD3 | 7.5% |
| DR_CD8RO | 7.5% |
| NKCD16_nonTnonB | 7.5% |
| CD8 RO CCR4_total | 7.5% |
| NK_nonTnonB | 7.5% |
| naive_Bcells | 5.0% |
| Tconv memDR_CD3 | 5.0% |
| CD8 RO CCR5_total | 5.0% |
| Tconv memCCR6_Tconv | 5.0% |
| CD4neg_CD3 | 5.0% |
| CD8 RO_total | 5.0% |
| Tconv memCXCR3_mem | 5.0% |
| NK Ki67_nonTnonB | 5.0% |
| CD4 Tconv mem_total | 5.0% |
| CD8 RA naive_CD3 | 5.0% |
| Tconv memCD27_Tconv | 5.0% |
| CD8 RO DR_CD8 | 5.0% |
| CD4 Tconv_total | 2.5% |
| CD8 RO CD27_CD8 | 2.5% |
| CD8 RO TIGIT_CD3 | 2.5% |
| NK Ki67_NK | 2.5% |
| Tconv memintB7_total | 2.5% |
| CD8 RO Ki67_total | 2.5% |
| Tconv memKi67_total | 2.5% |
| Tconv memCD56_Tconv | 2.5% |
| CD8 RO CXCR3_CD8 | 2.5% |
| Tconv memTIGIT_mem | 2.5% |
| Ki67_CD8RO | 2.5% |
| Tconv memintB7_CD3 | 2.5% |
| Tconv memCCR6_mem | 2.5% |
| Tconv memKi67_mem | 2.5% |
| CD8 RO CCR5_CD8 | 2.5% |
| Tconv memPD1_total | 2.5% |
| Tconv memCCR4_mem | 2.5% |
| Tconv memDR_mem | 2.5% |
| CD8 RA_CD3 | 2.5% |
| CD8 RA naive_total | 2.5% |
| CD8 RO CCR6_total | 2.5% |
| Tconv memPD1_CD3 | 2.5% |
| CD8pos_total | 2.5% |
| CD27negIgDneg_Bcells | 2.5% |
| Bcells memory_total | 2.5% |
| Tconv memCXCR3_Tconv | 2.5% |
| TIGIT_CD8RO | 2.5% |
| Bcells_total | 2.5% |
| CD8 RO CD27_total | 2.5% |

**Total features selected by Mutual Information (Top 10%)_t40**: 88

#### Mutual Information (Top 10%)_t50

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Tconv mem_Tconv | 30.0% |
| CD14mono_total | 22.5% |
| Tconv naive_Tconv | 22.5% |
| Bcells CD27posIgDneg_total | 22.5% |
| CD27IgD_Bcells | 22.5% |
| Treg memory_CD3 | 17.5% |
| CD8pos_CD3 | 15.0% |
| CD8 RO DR_CD3 | 15.0% |
| Treg memory_CD4 | 15.0% |
| nonTnonB_total | 15.0% |
| Tconv memCD27_CD3 | 15.0% |
| CD8 RO_CD3 | 12.5% |
| Tconv naive_total | 12.5% |
| CD8 RA_CD8 | 12.5% |
| CD4 Treg_CD4 | 10.0% |
| CD16mono_myeloid | 10.0% |
| CD3pos_total | 7.5% |
| CD3neg_total | 7.5% |
| CD14mono_CD3neg | 7.5% |
| CD4 Treg _CD3 | 7.5% |
| Bcells_CD3neg | 7.5% |
| Tconv naive_CD3 | 7.5% |
| nonTnonB_CD3neg | 7.5% |
| Bcells memory_CD3neg | 7.5% |
| CD8 ncytotox RO CCR4_CD8ntox | 7.5% |
| CD8 RA CCR7 naive_CD8 | 5.0% |
| Ki67_Bcells | 5.0% |
| CD4neg_CD3 | 5.0% |
| CD4 Tconv mem_total | 5.0% |
| NK Ki67_nonTnonB | 5.0% |
| myeloid_total | 5.0% |
| CD8 RO_total | 5.0% |
| CD8 RO CCR6_CD3 | 5.0% |
| CD4 Treg_total | 5.0% |
| NK_nonTnonB | 5.0% |
| Treg naive_total | 5.0% |
| CD8  RO Ki67_CD3 | 5.0% |
| NKCD16_CD3neg | 2.5% |
| Tconv memKi67_CD3 | 2.5% |
| CD8 RO CXCR3_CD8 | 2.5% |
| Tconv memTIGIT_CD3 | 2.5% |
| CD8 RO CCR5_CD8 | 2.5% |
| Tconv memCCR6_CD3 | 2.5% |
| NKCD16_nonTnonB | 2.5% |
| CD8 RO CCR4_total | 2.5% |
| CD8 RO CCR5_CD3 | 2.5% |
| DR_CD8RO | 2.5% |
| Tconv memKi67_mem | 2.5% |
| Tconv memCXCR3_mem | 2.5% |
| CD27negIgDneg_Bcells | 2.5% |
| Treg naive_CD4 | 2.5% |
| Treg naive_CD3 | 2.5% |
| CD8 RA naive_CD3 | 2.5% |
| Tconv memCXCR3_Tconv | 2.5% |
| Bcells_total | 2.5% |
| CD8 RO CD27_total | 2.5% |

**Total features selected by Mutual Information (Top 10%)_t50**: 56

#### Mutual Information (Top 10%)_t60

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD14mono_total | 21.2% |
| Bcells CD27posIgDneg_total | 21.2% |
| Tconv mem_Tconv | 15.2% |
| Tconv naive_Tconv | 12.1% |
| CD8pos_CD3 | 12.1% |
| Treg memory_CD4 | 12.1% |
| CD27IgD_Bcells | 12.1% |
| nonTnonB_total | 9.1% |
| Treg memory_CD3 | 9.1% |
| CD8 ncytotox RO CCR4_CD8ntox | 9.1% |
| CD4 Treg_CD4 | 6.1% |
| Tconv memCD27_CD3 | 6.1% |
| CD14mono_CD3neg | 6.1% |
| CD4 Treg _CD3 | 6.1% |
| myeloid_total | 6.1% |
| nonTnonB_CD3neg | 6.1% |
| Tconv naive_CD3 | 6.1% |
| Tconv memKi67_CD3 | 3.0% |
| Tconv naive_total | 3.0% |
| CD4neg_CD3 | 3.0% |
| CD8 RO_total | 3.0% |
| Bcells_CD3neg | 3.0% |
| CD8 RO DR_CD3 | 3.0% |
| Bcells memory_CD3neg | 3.0% |
| Tconv memCCR6_CD3 | 3.0% |
| CD8 RA_CD8 | 3.0% |
| CD8 RO_CD3 | 3.0% |
| CD3pos_total | 3.0% |
| CD3neg_total | 3.0% |
| Bcells_total | 3.0% |
| CD16mono_myeloid | 3.0% |
| CD8 RO CD27_total | 3.0% |

**Total features selected by Mutual Information (Top 10%)_t60**: 32

#### Mutual Information (Top 10%)_t70

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Bcells CD27posIgDneg_total | 27.3% |
| nonTnonB_total | 13.6% |
| CD14mono_total | 13.6% |
| Tconv naive_Tconv | 9.1% |
| Tconv mem_Tconv | 9.1% |
| Treg memory_CD3 | 9.1% |
| CD27IgD_Bcells | 9.1% |
| nonTnonB_CD3neg | 4.5% |
| CD14mono_CD3neg | 4.5% |
| CD4 Treg _CD3 | 4.5% |
| Tconv memKi67_CD3 | 4.5% |
| Bcells_CD3neg | 4.5% |
| CD4 Treg_CD4 | 4.5% |
| Tconv memCD27_CD3 | 4.5% |
| Bcells memory_CD3neg | 4.5% |
| Bcells_total | 4.5% |

**Total features selected by Mutual Information (Top 10%)_t70**: 16

#### Mutual Information (Top 10%)_t80

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Bcells CD27posIgDneg_total | 50.0% |
| Treg memory_CD3 | 33.3% |
| CD14mono_total | 16.7% |
| CD4 Treg_CD4 | 16.7% |

**Total features selected by Mutual Information (Top 10%)_t80**: 4

#### NaiveBayes_Permutation_AboveMean_t40

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Bcells CD27posIgDneg_total | 97.5% |
| CD3hi_total | 97.5% |
| Bcells memory_total | 92.5% |
| Bcells memory_CD3neg | 92.5% |
| CD8 RO CD56_total | 92.5% |
| NKCD56hi_NK | 90.0% |
| CD8 RO CD56_CD3 | 90.0% |
| CD8 RO DR_total | 90.0% |
| CD8 RO DR_CD3 | 90.0% |
| CD16mono_myeloid | 90.0% |
| Tconv memCXCR3_total | 87.5% |
| Ki67_CD8RO | 87.5% |
| NKCD16_NK | 85.0% |
| DR_CD8RO | 85.0% |
| Tconv memCD56_total | 85.0% |
| CD27IgD_Bcells | 85.0% |
| Ki67_Bcells | 82.5% |
| CD8  RO Ki67_CD3 | 82.5% |
| Tconv memCXCR3_CD3 | 82.5% |
| NK Ki67_total | 82.5% |
| Tconv memCXCR3_Tconv | 82.5% |
| NK Ki67_NK | 80.0% |
| CD8 RO Ki67_total | 80.0% |
| CD14+16+mono_total | 80.0% |
| Bcells CD27negIgDneg_total | 80.0% |
| Tconv memKi67_total | 77.5% |
| CD8 RO Ki67_CD8 | 77.5% |
| CD14+16+mono_CD3neg | 75.0% |
| NKCD56hi_total | 75.0% |
| Tconv memCD56_Tconv | 72.5% |
| NK Ki67_nonTnonB | 72.5% |
| CD8 RA naive_CD3 | 72.5% |
| CD14+16+mono_myeloid | 72.5% |
| Tconv memCD56_mem | 70.0% |
| CD8 RO DR_CD8 | 70.0% |
| CD8 RA_CD3 | 67.5% |
| Tconv memintB7_CD3 | 65.0% |
| Bcells naive_total | 65.0% |
| Tconv memCD56_CD3 | 62.5% |
| Bcells Ki67_CD3neg | 62.5% |
| CD8 RO CXCR3_CD3 | 62.5% |
| CD3hi_CD3 | 62.5% |
| CD8 RO intB7_CD3 | 62.5% |
| Tconv memCXCR3_mem | 62.5% |
| Treg naive_CD3 | 60.0% |
| Tconv memDR_mem | 60.0% |
| CD4 Treg_CD4 | 60.0% |
| NKCD16_total | 60.0% |
| Treg memory_CD4 | 60.0% |
| CD8 RA naive_total | 57.5% |
| NK_total | 57.5% |
| Tconv memintB7_mem | 57.5% |
| CD16mono_CD3neg | 57.5% |
| Tconv memTIGIT_mem | 57.5% |
| Treg memory_total | 55.0% |
| CD16+mono_total | 55.0% |
| CD14mono_myeloid | 55.0% |
| CCR4_CD8RO | 55.0% |
| CD27_CD8RO | 55.0% |
| Treg memory_CD3 | 55.0% |
| Bcells Ki67_total | 52.5% |
| NK Ki67_CD3neg | 52.5% |
| CD4 Treg _CD3 | 52.5% |
| Tconv memPD1_mem | 52.5% |
| Tconv memCCR5_total | 52.5% |
| Tconv memCCR6_CD3 | 52.5% |
| Tconv memintB7_Tconv | 50.0% |
| CCR5_CD8RO | 50.0% |
| Tconv mem_Tconv | 50.0% |
| Tconv memCD27_mem | 47.5% |
| CD8 RO intB7_total | 47.5% |
| Tconv memCD27_Tconv | 47.5% |
| CD8 ncytotox RO CCR4_CD8ntox | 47.5% |
| Bcells_total | 47.5% |
| Tconv memCCR4_Tconv | 47.5% |
| CD8 RO CCR5_CD3 | 47.5% |
| CD27negIgDneg_Bcells | 47.5% |
| Treg naive_CD4 | 47.5% |
| CXCR3_CD8RO | 45.0% |
| CD8 RO CXCR3_total | 45.0% |
| Tconv memCCR4_CD3 | 45.0% |
| CD4neg_CD3 | 45.0% |
| CD8 RO CD56_CD8 | 42.5% |
| CD4 Treg_total | 42.5% |
| intB7_CD8RO | 42.5% |
| Tconv memCCR5_mem | 42.5% |
| Tconv memCCR6_mem | 40.0% |
| CD3hi_CD4neg | 40.0% |
| CD8 RO intB7_CD8 | 40.0% |
| Tconv mem_CD3 | 40.0% |
| CD4neg_total | 40.0% |
| Tconv memCCR6_total | 40.0% |
| CD8 RO TIGIT_CD8 | 40.0% |
| NKCD56hi_CD3neg | 37.5% |
| NKCD56hi_nonTnonB | 37.5% |
| naive_Bcells | 37.5% |
| NKCD16_CD3neg | 37.5% |
| Tconv memCCR6_Tconv | 37.5% |
| CD8 RO CXCR3_CD8 | 35.0% |
| CD8 RO PD1_total | 35.0% |
| CD8 RO CCR6_CD3 | 35.0% |
| Tconv naive_Tconv | 35.0% |
| NK_nonTnonB | 35.0% |
| CCR6_CD8RO | 35.0% |
| CD8 RO CCR5_total | 35.0% |
| CD8 RA_total | 35.0% |
| Treg naive_total | 35.0% |
| CD8 RO CCR5_CD8 | 35.0% |
| Tconv memCD27_CD3 | 35.0% |
| NKCD16_nonTnonB | 35.0% |
| Tconv memDR_total | 32.5% |
| CD8 RO CCR4_total | 32.5% |
| CD8 RA CCR7 naive_CD8 | 32.5% |
| CD8 RO_CD8 | 30.0% |
| CD8 RO CCR6_CD8 | 30.0% |
| CD8 RO PD1_CD8 | 30.0% |
| NK_CD3neg | 30.0% |
| Tconv memDR_CD3 | 27.5% |
| CD8pos_CD3 | 27.5% |
| Tconv memCCR5_CD3 | 27.5% |
| CD8 RO PD1_CD3 | 27.5% |
| Bcells naive_CD3neg | 25.0% |
| PD1_CD8RO | 25.0% |
| Tconv memCCR4_mem | 25.0% |
| CD8 RO CCR6_total | 25.0% |
| Tconv memCCR5_Tconv | 25.0% |
| Tconv memCCR4_total | 25.0% |
| CD8 ncytotox RO CCR4_CD3 | 25.0% |
| CD8 RO TIGIT_CD3 | 22.5% |
| Tconv memintB7_total | 22.5% |
| memory_Bcells | 22.5% |
| Tconv naive_CD3 | 20.0% |
| CD8pos_total | 20.0% |
| Tconv memKi67_mem | 20.0% |
| Tconv memPD1_total | 20.0% |
| CD8 RA_CD8 | 20.0% |
| CD8 RO CD27_CD8 | 20.0% |
| CD8 RO CD27_CD3 | 17.5% |
| Tconv memDR_Tconv | 17.5% |
| Tconv memTIGIT_total | 17.5% |
| Tconv memTIGIT_CD3 | 15.0% |
| Tconv memKi67_CD3 | 15.0% |
| TIGIT_CD8RO | 15.0% |
| CD8 RO CD27_total | 15.0% |
| CD56_CD8RO | 15.0% |
| CD8 RO TIGIT_total | 15.0% |
| myeloid_CD3neg | 12.5% |
| CD14mono_CD3neg | 12.5% |
| Tconv naive_total | 12.5% |
| Tconv memCD27_total | 12.5% |
| CD4 Tconv_CD3 | 12.5% |
| nonTnonB_CD3neg | 10.0% |
| CD4 Tconv mem_total | 10.0% |
| Bcells_CD3neg | 10.0% |
| Tconv memTIGIT_Tconv | 10.0% |
| myeloid_total | 7.5% |
| CD8 RO_CD3 | 7.5% |
| Tconv memKi67_Tconv | 7.5% |
| CD8 RO_total | 7.5% |
| Tconv memPD1_CD3 | 5.0% |
| CD14mono_total | 2.5% |
| CD4 Tconv_total | 2.5% |
| CD3neg_total | 2.5% |
| CD3pos_total | 2.5% |
| nonTnonB_total | 2.5% |

**Total features selected by NaiveBayes_Permutation_AboveMean_t40**: 165

#### NaiveBayes_Permutation_AboveMean_t50

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD3hi_total | 97.5% |
| Bcells CD27posIgDneg_total | 95.0% |
| CD8 RO CD56_total | 87.5% |
| Bcells memory_total | 85.0% |
| CD8 RO DR_total | 85.0% |
| CD16mono_myeloid | 82.5% |
| Ki67_CD8RO | 82.5% |
| CD8 RO DR_CD3 | 80.0% |
| NKCD56hi_NK | 77.5% |
| Bcells memory_CD3neg | 77.5% |
| NK Ki67_NK | 77.5% |
| Tconv memCD56_total | 77.5% |
| NKCD16_NK | 75.0% |
| Ki67_Bcells | 75.0% |
| Tconv memCXCR3_total | 70.0% |
| CD8  RO Ki67_CD3 | 70.0% |
| CD27IgD_Bcells | 67.5% |
| DR_CD8RO | 67.5% |
| CD8 RO Ki67_CD8 | 67.5% |
| NK Ki67_total | 67.5% |
| CD8 RO CD56_CD3 | 65.0% |
| CD14+16+mono_total | 65.0% |
| CD14+16+mono_CD3neg | 62.5% |
| CD8 RO Ki67_total | 62.5% |
| Tconv memCXCR3_CD3 | 62.5% |
| Bcells CD27negIgDneg_total | 60.0% |
| NKCD56hi_total | 57.5% |
| Tconv memCD56_mem | 57.5% |
| CD8 RA naive_CD3 | 55.0% |
| Tconv memCXCR3_Tconv | 55.0% |
| CD14+16+mono_myeloid | 55.0% |
| Tconv memCD56_Tconv | 52.5% |
| NK Ki67_nonTnonB | 50.0% |
| Tconv memKi67_total | 50.0% |
| CD3hi_CD3 | 50.0% |
| NKCD16_total | 50.0% |
| Tconv memCXCR3_mem | 47.5% |
| CD8 RO DR_CD8 | 45.0% |
| CD8 RO intB7_CD3 | 45.0% |
| CD16mono_CD3neg | 45.0% |
| Tconv memCD56_CD3 | 42.5% |
| Bcells naive_total | 42.5% |
| NK_total | 40.0% |
| CD4 Treg _CD3 | 40.0% |
| CD8 RA_CD3 | 40.0% |
| Treg memory_CD4 | 40.0% |
| CD27_CD8RO | 37.5% |
| CD14mono_myeloid | 35.0% |
| Bcells_total | 35.0% |
| Tconv memCCR5_total | 35.0% |
| Tconv memintB7_CD3 | 35.0% |
| CD8 RO CXCR3_CD3 | 35.0% |
| CD16+mono_total | 35.0% |
| Tconv memTIGIT_mem | 32.5% |
| Treg naive_CD3 | 32.5% |
| Treg memory_CD3 | 32.5% |
| CCR4_CD8RO | 32.5% |
| CD8 RA naive_total | 30.0% |
| Tconv memCCR6_CD3 | 30.0% |
| Tconv memCCR4_Tconv | 30.0% |
| NK Ki67_CD3neg | 30.0% |
| Tconv memCCR4_CD3 | 30.0% |
| CD8 RO intB7_total | 30.0% |
| Bcells Ki67_total | 30.0% |
| Tconv memPD1_mem | 30.0% |
| CD4 Treg_CD4 | 30.0% |
| Tconv memintB7_mem | 27.5% |
| Treg naive_CD4 | 27.5% |
| Bcells Ki67_CD3neg | 27.5% |
| Tconv memCD27_Tconv | 27.5% |
| CD3hi_CD4neg | 25.0% |
| CCR6_CD8RO | 25.0% |
| CD8 RO intB7_CD8 | 25.0% |
| Tconv memCCR6_mem | 25.0% |
| Tconv memCCR6_total | 25.0% |
| Tconv memCD27_CD3 | 25.0% |
| Treg memory_total | 25.0% |
| CD8 RO CD56_CD8 | 25.0% |
| Tconv memDR_mem | 25.0% |
| naive_Bcells | 22.5% |
| CD4 Treg_total | 22.5% |
| CD8 RO CCR4_total | 22.5% |
| Tconv naive_Tconv | 22.5% |
| Tconv memintB7_Tconv | 22.5% |
| Tconv memCD27_mem | 22.5% |
| CD8 RO CCR5_CD3 | 22.5% |
| CD8 RO CXCR3_CD8 | 20.0% |
| Tconv mem_CD3 | 20.0% |
| Tconv memCCR5_mem | 20.0% |
| CCR5_CD8RO | 20.0% |
| NKCD16_nonTnonB | 20.0% |
| CD27negIgDneg_Bcells | 20.0% |
| intB7_CD8RO | 20.0% |
| Tconv mem_Tconv | 20.0% |
| CD8 RO PD1_CD8 | 17.5% |
| NK_nonTnonB | 17.5% |
| NKCD56hi_nonTnonB | 17.5% |
| CXCR3_CD8RO | 17.5% |
| CD8 RO CCR5_CD8 | 17.5% |
| CD8 RO PD1_total | 17.5% |
| CD8 RO CCR6_CD3 | 17.5% |
| CD8 RO CCR6_CD8 | 17.5% |
| NKCD56hi_CD3neg | 17.5% |
| Treg naive_total | 15.0% |
| CD8 ncytotox RO CCR4_CD8ntox | 15.0% |
| CD8 RO CCR5_total | 15.0% |
| NKCD16_CD3neg | 15.0% |
| Tconv memCCR6_Tconv | 15.0% |
| CD8 RO CXCR3_total | 15.0% |
| Tconv memDR_total | 15.0% |
| CD8 RO TIGIT_CD8 | 15.0% |
| CD4neg_total | 15.0% |
| CD8 RO PD1_CD3 | 15.0% |
| Bcells naive_CD3neg | 12.5% |
| Tconv memDR_CD3 | 12.5% |
| Tconv naive_CD3 | 12.5% |
| CD8 RO_CD8 | 12.5% |
| CD8 RA_total | 12.5% |
| Tconv memintB7_total | 12.5% |
| Tconv memKi67_mem | 12.5% |
| CD56_CD8RO | 12.5% |
| Tconv memPD1_total | 12.5% |
| CD8 RO CCR6_total | 12.5% |
| Tconv memCCR5_CD3 | 10.0% |
| CD4neg_CD3 | 10.0% |
| CD8 ncytotox RO CCR4_CD3 | 10.0% |
| CD8 RO TIGIT_CD3 | 10.0% |
| memory_Bcells | 10.0% |
| Tconv memCCR5_Tconv | 10.0% |
| CD8 RO CD27_CD8 | 10.0% |
| PD1_CD8RO | 10.0% |
| CD8 RA_CD8 | 10.0% |
| CD8 RA CCR7 naive_CD8 | 7.5% |
| Tconv memDR_Tconv | 7.5% |
| NK_CD3neg | 7.5% |
| Tconv memKi67_CD3 | 7.5% |
| CD8 RO CD27_CD3 | 7.5% |
| Tconv memTIGIT_total | 7.5% |
| CD14mono_CD3neg | 5.0% |
| CD8 RO CD27_total | 5.0% |
| Tconv memTIGIT_CD3 | 5.0% |
| CD4 Tconv mem_total | 5.0% |
| CD8 RO_total | 5.0% |
| CD8pos_CD3 | 5.0% |
| Tconv memCD27_total | 5.0% |
| Tconv memCCR4_mem | 5.0% |
| TIGIT_CD8RO | 5.0% |
| Tconv naive_total | 5.0% |
| CD4 Tconv_CD3 | 5.0% |
| Tconv memCCR4_total | 5.0% |
| CD8 RO_CD3 | 2.5% |
| CD8 RO TIGIT_total | 2.5% |
| CD8pos_total | 2.5% |
| Tconv memTIGIT_Tconv | 2.5% |
| CD3neg_total | 2.5% |
| nonTnonB_total | 2.5% |
| CD3pos_total | 2.5% |
| nonTnonB_CD3neg | 2.5% |
| Bcells_CD3neg | 2.5% |

**Total features selected by NaiveBayes_Permutation_AboveMean_t50**: 159

#### NaiveBayes_Permutation_AboveMean_t60

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD3hi_total | 97.5% |
| Bcells CD27posIgDneg_total | 87.5% |
| Bcells memory_total | 77.5% |
| Tconv memCD56_total | 70.0% |
| Ki67_CD8RO | 70.0% |
| CD8 RO CD56_total | 67.5% |
| Ki67_Bcells | 67.5% |
| CD8 RO DR_CD3 | 65.0% |
| CD16mono_myeloid | 65.0% |
| CD8  RO Ki67_CD3 | 62.5% |
| CD8 RO DR_total | 62.5% |
| NKCD56hi_NK | 62.5% |
| Bcells memory_CD3neg | 57.5% |
| Tconv memCXCR3_total | 55.0% |
| DR_CD8RO | 55.0% |
| CD8 RO CD56_CD3 | 52.5% |
| NK Ki67_NK | 52.5% |
| CD8 RO Ki67_total | 52.5% |
| NKCD16_NK | 50.0% |
| CD8 RO Ki67_CD8 | 50.0% |
| CD14+16+mono_total | 47.5% |
| Tconv memCD56_mem | 42.5% |
| CD8 RA naive_CD3 | 42.5% |
| CD27IgD_Bcells | 42.5% |
| Tconv memCXCR3_Tconv | 42.5% |
| NK Ki67_total | 42.5% |
| Tconv memCD56_Tconv | 40.0% |
| CD14+16+mono_myeloid | 37.5% |
| Bcells CD27negIgDneg_total | 37.5% |
| CD14+16+mono_CD3neg | 35.0% |
| Tconv memCXCR3_CD3 | 35.0% |
| CD3hi_CD3 | 32.5% |
| NKCD56hi_total | 32.5% |
| NK Ki67_nonTnonB | 30.0% |
| CD14mono_myeloid | 30.0% |
| NK_total | 30.0% |
| CD8 RO DR_CD8 | 30.0% |
| NKCD16_total | 30.0% |
| Treg memory_CD3 | 27.5% |
| CD16mono_CD3neg | 27.5% |
| Treg memory_CD4 | 25.0% |
| Tconv memKi67_total | 25.0% |
| CD8 RA_CD3 | 25.0% |
| Bcells_total | 22.5% |
| CD27_CD8RO | 22.5% |
| CD16+mono_total | 22.5% |
| Tconv memCD56_CD3 | 22.5% |
| Tconv memintB7_CD3 | 20.0% |
| Bcells naive_total | 20.0% |
| Tconv memCCR4_Tconv | 20.0% |
| Treg naive_CD3 | 20.0% |
| Tconv memCXCR3_mem | 20.0% |
| Bcells Ki67_total | 20.0% |
| Tconv memCCR5_total | 20.0% |
| Tconv memCCR4_CD3 | 17.5% |
| NK Ki67_CD3neg | 17.5% |
| CD8 RO CXCR3_CD3 | 17.5% |
| CD4 Treg _CD3 | 17.5% |
| Bcells Ki67_CD3neg | 17.5% |
| Tconv memPD1_mem | 15.0% |
| CD8 RA naive_total | 15.0% |
| Tconv memCD27_CD3 | 15.0% |
| Tconv memTIGIT_mem | 15.0% |
| CD4 Treg_total | 12.5% |
| intB7_CD8RO | 12.5% |
| Tconv memCCR6_total | 12.5% |
| CD8 RO CXCR3_CD8 | 12.5% |
| Tconv memintB7_mem | 12.5% |
| CD8 RO CD56_CD8 | 12.5% |
| Tconv memDR_CD3 | 12.5% |
| CD8 RO intB7_CD3 | 12.5% |
| Treg memory_total | 12.5% |
| Tconv memDR_mem | 12.5% |
| CD4 Treg_CD4 | 12.5% |
| CD3hi_CD4neg | 12.5% |
| CCR4_CD8RO | 10.0% |
| Tconv memCCR6_CD3 | 10.0% |
| CD8 RO CCR6_CD3 | 10.0% |
| CD8 RO PD1_CD3 | 10.0% |
| Tconv memCD27_Tconv | 10.0% |
| CD8 RO intB7_total | 10.0% |
| CCR6_CD8RO | 10.0% |
| CCR5_CD8RO | 10.0% |
| Tconv memCCR6_Tconv | 10.0% |
| Tconv memintB7_Tconv | 7.5% |
| CD8 RO CCR5_total | 7.5% |
| CD8 RA CCR7 naive_CD8 | 7.5% |
| NK_nonTnonB | 7.5% |
| CD8 RO CXCR3_total | 7.5% |
| CD27negIgDneg_Bcells | 7.5% |
| naive_Bcells | 7.5% |
| CD8 RO PD1_total | 7.5% |
| NKCD56hi_CD3neg | 7.5% |
| Treg naive_CD4 | 7.5% |
| CXCR3_CD8RO | 7.5% |
| CD8 RO CCR5_CD8 | 7.5% |
| CD8 RO CCR6_CD8 | 7.5% |
| CD8 RO intB7_CD8 | 7.5% |
| CD4neg_CD3 | 5.0% |
| NKCD16_nonTnonB | 5.0% |
| NKCD56hi_nonTnonB | 5.0% |
| CD8 RO CCR4_total | 5.0% |
| memory_Bcells | 5.0% |
| Tconv memCCR4_total | 5.0% |
| Tconv memCCR5_mem | 5.0% |
| Tconv memintB7_total | 5.0% |
| Tconv memDR_Tconv | 5.0% |
| Tconv mem_CD3 | 5.0% |
| Tconv memCD27_mem | 5.0% |
| Tconv memDR_total | 5.0% |
| CD8 RO CCR5_CD3 | 5.0% |
| CD8pos_CD3 | 5.0% |
| CD8 RO TIGIT_CD8 | 5.0% |
| Tconv memKi67_CD3 | 5.0% |
| CD8 RA_total | 5.0% |
| Tconv naive_CD3 | 5.0% |
| Tconv mem_Tconv | 5.0% |
| Tconv memCCR5_CD3 | 5.0% |
| CD8 RO CD27_CD8 | 5.0% |
| Tconv memCCR4_mem | 5.0% |
| NK_CD3neg | 2.5% |
| CD14mono_CD3neg | 2.5% |
| Tconv memTIGIT_total | 2.5% |
| NKCD16_CD3neg | 2.5% |
| Tconv memCCR6_mem | 2.5% |
| CD8 RO CD27_CD3 | 2.5% |
| Treg naive_total | 2.5% |
| CD8 RO CCR6_total | 2.5% |
| Tconv naive_Tconv | 2.5% |
| CD8 RO_CD3 | 2.5% |
| CD56_CD8RO | 2.5% |
| TIGIT_CD8RO | 2.5% |
| CD4 Tconv_CD3 | 2.5% |
| Tconv naive_total | 2.5% |
| Tconv memTIGIT_Tconv | 2.5% |
| Tconv memKi67_mem | 2.5% |
| Tconv memCCR5_Tconv | 2.5% |
| CD8 RO TIGIT_CD3 | 2.5% |
| CD8 RA_CD8 | 2.5% |
| CD8 RO_CD8 | 2.5% |
| CD4neg_total | 2.5% |

**Total features selected by NaiveBayes_Permutation_AboveMean_t60**: 141

#### NaiveBayes_Permutation_AboveMean_t70

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD3hi_total | 90.0% |
| Bcells CD27posIgDneg_total | 82.5% |
| Bcells memory_total | 65.0% |
| CD8 RO DR_total | 52.5% |
| CD16mono_myeloid | 47.5% |
| CD8  RO Ki67_CD3 | 42.5% |
| Ki67_CD8RO | 42.5% |
| Bcells memory_CD3neg | 42.5% |
| Tconv memCD56_total | 40.0% |
| NKCD56hi_NK | 40.0% |
| Ki67_Bcells | 40.0% |
| CD8 RO DR_CD3 | 40.0% |
| CD8 RO Ki67_total | 37.5% |
| NK Ki67_NK | 37.5% |
| Tconv memCXCR3_total | 35.0% |
| CD8 RO CD56_total | 35.0% |
| CD8 RO Ki67_CD8 | 35.0% |
| NKCD16_NK | 32.5% |
| CD8 RO CD56_CD3 | 30.0% |
| CD8 RA naive_CD3 | 27.5% |
| CD27IgD_Bcells | 27.5% |
| CD14+16+mono_total | 25.0% |
| Tconv memCXCR3_Tconv | 25.0% |
| CD14+16+mono_myeloid | 25.0% |
| Bcells CD27negIgDneg_total | 22.5% |
| DR_CD8RO | 20.0% |
| Tconv memCD56_Tconv | 20.0% |
| CD14+16+mono_CD3neg | 20.0% |
| CD3hi_CD3 | 17.5% |
| NK_total | 17.5% |
| NK Ki67_total | 17.5% |
| NKCD56hi_total | 17.5% |
| NKCD16_total | 15.0% |
| Tconv memKi67_total | 15.0% |
| Tconv memCCR4_CD3 | 15.0% |
| Tconv memCXCR3_CD3 | 15.0% |
| NK Ki67_nonTnonB | 15.0% |
| CD8 RO DR_CD8 | 15.0% |
| CD16mono_CD3neg | 12.5% |
| Tconv memCD56_mem | 12.5% |
| Bcells Ki67_CD3neg | 10.0% |
| Treg memory_CD3 | 10.0% |
| Tconv memCCR5_total | 10.0% |
| CCR4_CD8RO | 10.0% |
| Bcells_total | 10.0% |
| NK Ki67_CD3neg | 10.0% |
| Tconv memTIGIT_mem | 10.0% |
| Treg memory_CD4 | 7.5% |
| Tconv memCXCR3_mem | 7.5% |
| CD27_CD8RO | 7.5% |
| Treg naive_CD3 | 7.5% |
| Tconv memCD56_CD3 | 7.5% |
| Tconv memCCR6_total | 7.5% |
| CCR6_CD8RO | 7.5% |
| intB7_CD8RO | 7.5% |
| CD8 RA_CD3 | 7.5% |
| Tconv memCCR4_Tconv | 5.0% |
| NKCD56hi_nonTnonB | 5.0% |
| CD8 RO intB7_total | 5.0% |
| CD8 RO intB7_CD3 | 5.0% |
| Bcells Ki67_total | 5.0% |
| CD8 RO CCR6_CD3 | 5.0% |
| CD14mono_myeloid | 5.0% |
| CD27negIgDneg_Bcells | 5.0% |
| CD4 Treg_CD4 | 5.0% |
| CD8 RO CCR5_total | 5.0% |
| Tconv memPD1_mem | 5.0% |
| Tconv memDR_mem | 5.0% |
| CD3hi_CD4neg | 5.0% |
| CD8 RA_total | 5.0% |
| CD8 RO CXCR3_CD8 | 5.0% |
| CD4neg_CD3 | 2.5% |
| NK_nonTnonB | 2.5% |
| NKCD16_nonTnonB | 2.5% |
| CD4 Treg _CD3 | 2.5% |
| NK_CD3neg | 2.5% |
| NKCD16_CD3neg | 2.5% |
| Tconv memTIGIT_total | 2.5% |
| CD8 RA CCR7 naive_CD8 | 2.5% |
| CD14mono_CD3neg | 2.5% |
| Tconv memCD27_mem | 2.5% |
| CD4 Tconv_CD3 | 2.5% |
| Tconv memCCR6_CD3 | 2.5% |
| naive_Bcells | 2.5% |
| Tconv memCD27_Tconv | 2.5% |
| CD8 RO PD1_total | 2.5% |
| Tconv mem_Tconv | 2.5% |
| Tconv memDR_Tconv | 2.5% |
| Tconv memCCR6_mem | 2.5% |
| CD8 RO_CD3 | 2.5% |
| Tconv memCCR6_Tconv | 2.5% |
| Tconv memCD27_CD3 | 2.5% |
| CD8 RO CCR5_CD3 | 2.5% |
| Bcells naive_total | 2.5% |
| Tconv memintB7_mem | 2.5% |
| Tconv memKi67_mem | 2.5% |
| Tconv memintB7_Tconv | 2.5% |
| CD8pos_CD3 | 2.5% |
| CD8 RO intB7_CD8 | 2.5% |
| CD8 RO CXCR3_CD3 | 2.5% |
| CD8 RO CCR6_CD8 | 2.5% |
| CD8 RO CXCR3_total | 2.5% |
| CD4 Treg_total | 2.5% |
| CD8 RO PD1_CD3 | 2.5% |
| Treg naive_CD4 | 2.5% |
| Tconv memCCR5_mem | 2.5% |
| CD8 RO TIGIT_CD3 | 2.5% |
| CD16+mono_total | 2.5% |
| Treg memory_total | 2.5% |
| CD8 RO CCR4_total | 2.5% |
| CD4neg_total | 2.5% |

**Total features selected by NaiveBayes_Permutation_AboveMean_t70**: 111

#### NaiveBayes_Permutation_AboveMean_t80

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD3hi_total | 70.0% |
| Bcells CD27posIgDneg_total | 65.0% |
| CD8 RO DR_total | 35.0% |
| CD8 RO DR_CD3 | 30.0% |
| Ki67_Bcells | 30.0% |
| CD16mono_myeloid | 25.0% |
| Bcells memory_total | 25.0% |
| Bcells memory_CD3neg | 22.5% |
| CD8 RO Ki67_CD8 | 22.5% |
| CD8  RO Ki67_CD3 | 22.5% |
| Tconv memCD56_total | 22.5% |
| NKCD56hi_NK | 22.5% |
| NK Ki67_NK | 20.0% |
| Ki67_CD8RO | 20.0% |
| CD27IgD_Bcells | 17.5% |
| CD14+16+mono_myeloid | 17.5% |
| CD14+16+mono_CD3neg | 15.0% |
| CD8 RO CD56_total | 15.0% |
| CD8 RO CD56_CD3 | 15.0% |
| CD8 RO Ki67_total | 15.0% |
| CD8 RA naive_CD3 | 15.0% |
| NKCD16_NK | 12.5% |
| Bcells CD27negIgDneg_total | 10.0% |
| Tconv memCXCR3_total | 10.0% |
| CD14+16+mono_total | 10.0% |
| NK Ki67_total | 7.5% |
| Tconv memCXCR3_Tconv | 7.5% |
| CCR4_CD8RO | 7.5% |
| Tconv memKi67_total | 7.5% |
| NK Ki67_nonTnonB | 5.0% |
| Tconv memCD56_Tconv | 5.0% |
| NKCD16_total | 5.0% |
| DR_CD8RO | 5.0% |
| Bcells Ki67_CD3neg | 5.0% |
| CD8 RA_CD3 | 5.0% |
| NK_total | 5.0% |
| CD3hi_CD3 | 5.0% |
| Tconv memDR_mem | 5.0% |
| CD8 RO DR_CD8 | 5.0% |
| NKCD56hi_total | 5.0% |
| Tconv memTIGIT_total | 2.5% |
| NKCD16_CD3neg | 2.5% |
| Tconv memTIGIT_mem | 2.5% |
| NKCD56hi_nonTnonB | 2.5% |
| Tconv memCD27_Tconv | 2.5% |
| CD8 RO CCR5_CD3 | 2.5% |
| Tconv memCCR4_CD3 | 2.5% |
| Tconv memCD27_mem | 2.5% |
| CD16mono_CD3neg | 2.5% |
| CD27_CD8RO | 2.5% |
| intB7_CD8RO | 2.5% |
| Bcells naive_total | 2.5% |
| CD8 RA_total | 2.5% |
| Tconv memCCR5_total | 2.5% |
| Tconv memCXCR3_mem | 2.5% |
| CD8 RO intB7_total | 2.5% |
| CD4 Treg_CD4 | 2.5% |
| Treg memory_CD4 | 2.5% |
| CD27negIgDneg_Bcells | 2.5% |
| CD8 RO CXCR3_CD8 | 2.5% |
| Tconv memCXCR3_CD3 | 2.5% |
| Bcells_total | 2.5% |
| CD16+mono_total | 2.5% |
| Tconv memCCR4_Tconv | 2.5% |
| Treg naive_CD3 | 2.5% |
| Tconv memCD56_mem | 2.5% |
| CD3hi_CD4neg | 2.5% |
| CD8 RO CCR5_total | 2.5% |

**Total features selected by NaiveBayes_Permutation_AboveMean_t80**: 68

#### NaiveBayes_Permutation_Top10%_t40

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Bcells CD27posIgDneg_total | 80.0% |
| CD3hi_total | 80.0% |
| Bcells memory_total | 70.0% |
| Ki67_Bcells | 60.0% |
| CD8 RO Ki67_CD8 | 57.5% |
| Ki67_CD8RO | 57.5% |
| CD8  RO Ki67_CD3 | 57.5% |
| Tconv memCD56_total | 52.5% |
| CD8 RO Ki67_total | 50.0% |
| CD8 RO DR_CD3 | 50.0% |
| CD8 RO DR_total | 47.5% |
| CD14+16+mono_total | 47.5% |
| NK Ki67_NK | 47.5% |
| Bcells memory_CD3neg | 47.5% |
| CD8 RO CD56_CD3 | 42.5% |
| CD8 RO CD56_total | 42.5% |
| Tconv memCXCR3_total | 40.0% |
| NKCD56hi_NK | 40.0% |
| NKCD16_NK | 30.0% |
| CD16mono_myeloid | 30.0% |
| CD14+16+mono_CD3neg | 27.5% |
| Tconv memCXCR3_Tconv | 20.0% |
| Tconv memCD56_Tconv | 20.0% |
| CD14+16+mono_myeloid | 17.5% |
| CD8 RA naive_CD3 | 15.0% |
| Tconv memCD56_mem | 15.0% |
| Tconv memKi67_total | 12.5% |
| CD3hi_CD3 | 12.5% |
| CD8 RO DR_CD8 | 12.5% |
| Bcells CD27negIgDneg_total | 12.5% |
| NK Ki67_total | 12.5% |
| Tconv memCD56_CD3 | 10.0% |
| NKCD56hi_total | 10.0% |
| CD27IgD_Bcells | 7.5% |
| Tconv memCXCR3_CD3 | 7.5% |
| CD8 RO intB7_CD3 | 7.5% |
| CD14mono_myeloid | 7.5% |
| Tconv memintB7_CD3 | 7.5% |
| DR_CD8RO | 5.0% |
| CD8 RO CCR4_total | 5.0% |
| Bcells Ki67_CD3neg | 5.0% |
| Tconv memCCR5_total | 5.0% |
| CD8 RO CD56_CD8 | 5.0% |
| NK_total | 5.0% |
| Bcells naive_total | 5.0% |
| CD8 RO CCR5_total | 5.0% |
| Tconv memintB7_mem | 5.0% |
| CD4neg_CD3 | 2.5% |
| intB7_CD8RO | 2.5% |
| Bcells Ki67_total | 2.5% |
| Treg memory_CD4 | 2.5% |
| Tconv memintB7_Tconv | 2.5% |
| NK Ki67_CD3neg | 2.5% |
| CD8 RA_CD3 | 2.5% |
| NK Ki67_nonTnonB | 2.5% |
| CD27_CD8RO | 2.5% |
| Tconv naive_CD3 | 2.5% |
| CCR4_CD8RO | 2.5% |
| CD8 RO CXCR3_total | 2.5% |
| Tconv memKi67_mem | 2.5% |
| Tconv memDR_mem | 2.5% |
| CD8 RA naive_total | 2.5% |
| CD8 RO intB7_total | 2.5% |
| CD16+mono_total | 2.5% |
| CD16mono_CD3neg | 2.5% |
| CD27negIgDneg_Bcells | 2.5% |
| Tconv memCXCR3_mem | 2.5% |
| Treg memory_CD3 | 2.5% |

**Total features selected by NaiveBayes_Permutation_Top10%_t40**: 68

#### NaiveBayes_Permutation_Top10%_t50

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD3hi_total | 72.5% |
| Bcells CD27posIgDneg_total | 70.0% |
| Bcells memory_total | 52.5% |
| CD8  RO Ki67_CD3 | 47.5% |
| Bcells memory_CD3neg | 42.5% |
| CD8 RO DR_CD3 | 40.0% |
| CD8 RO Ki67_total | 40.0% |
| Ki67_CD8RO | 37.5% |
| Tconv memCD56_total | 37.5% |
| CD8 RO DR_total | 35.0% |
| CD8 RO Ki67_CD8 | 35.0% |
| Ki67_Bcells | 35.0% |
| CD14+16+mono_total | 30.0% |
| NKCD56hi_NK | 27.5% |
| Tconv memCXCR3_total | 25.0% |
| CD8 RO CD56_CD3 | 22.5% |
| CD8 RO CD56_total | 22.5% |
| NK Ki67_NK | 20.0% |
| NKCD16_NK | 17.5% |
| CD14+16+mono_myeloid | 17.5% |
| CD16mono_myeloid | 15.0% |
| Tconv memCXCR3_Tconv | 12.5% |
| CD14+16+mono_CD3neg | 12.5% |
| Tconv memCD56_Tconv | 10.0% |
| CD8 RA naive_CD3 | 10.0% |
| Tconv memCD56_mem | 7.5% |
| Bcells CD27negIgDneg_total | 7.5% |
| Tconv memCXCR3_CD3 | 5.0% |
| CD8 RO DR_CD8 | 5.0% |
| CD3hi_CD3 | 5.0% |
| Tconv memKi67_total | 5.0% |
| DR_CD8RO | 5.0% |
| CD4neg_CD3 | 2.5% |
| Bcells Ki67_CD3neg | 2.5% |
| CD27IgD_Bcells | 2.5% |
| Bcells naive_total | 2.5% |
| CD8 RO CCR4_total | 2.5% |
| NK Ki67_total | 2.5% |
| CD27_CD8RO | 2.5% |
| CD8 RO intB7_CD3 | 2.5% |
| CD27negIgDneg_Bcells | 2.5% |
| Tconv memCCR5_total | 2.5% |

**Total features selected by NaiveBayes_Permutation_Top10%_t50**: 42

#### NaiveBayes_Permutation_Top10%_t60

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Bcells CD27posIgDneg_total | 62.5% |
| CD3hi_total | 55.0% |
| Bcells memory_total | 42.5% |
| CD8  RO Ki67_CD3 | 35.0% |
| Tconv memCD56_total | 27.5% |
| CD8 RO DR_CD3 | 25.0% |
| CD8 RO Ki67_CD8 | 25.0% |
| CD8 RO DR_total | 22.5% |
| Ki67_Bcells | 22.5% |
| Ki67_CD8RO | 20.0% |
| CD14+16+mono_total | 20.0% |
| NKCD56hi_NK | 17.5% |
| CD8 RO CD56_CD3 | 15.0% |
| CD8 RO Ki67_total | 15.0% |
| CD8 RO CD56_total | 15.0% |
| Bcells memory_CD3neg | 12.5% |
| NKCD16_NK | 10.0% |
| CD14+16+mono_CD3neg | 10.0% |
| CD14+16+mono_myeloid | 7.5% |
| NK Ki67_NK | 7.5% |
| CD8 RA naive_CD3 | 7.5% |
| Tconv memCXCR3_total | 5.0% |
| Tconv memCD56_Tconv | 5.0% |
| Bcells CD27negIgDneg_total | 5.0% |
| Tconv memCXCR3_Tconv | 2.5% |
| Tconv memCXCR3_CD3 | 2.5% |
| Bcells Ki67_CD3neg | 2.5% |
| Bcells naive_total | 2.5% |
| NK Ki67_total | 2.5% |
| Tconv memCD56_mem | 2.5% |
| CD27_CD8RO | 2.5% |
| CD16mono_myeloid | 2.5% |
| DR_CD8RO | 2.5% |
| CD27negIgDneg_Bcells | 2.5% |

**Total features selected by NaiveBayes_Permutation_Top10%_t60**: 34

#### NaiveBayes_Permutation_Top10%_t70

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Bcells CD27posIgDneg_total | 50.0% |
| CD3hi_total | 44.4% |
| CD8  RO Ki67_CD3 | 25.0% |
| Bcells memory_total | 22.2% |
| CD8 RO DR_CD3 | 19.4% |
| CD8 RO Ki67_CD8 | 16.7% |
| Ki67_CD8RO | 13.9% |
| Ki67_Bcells | 11.1% |
| Tconv memCD56_total | 11.1% |
| CD8 RO Ki67_total | 11.1% |
| CD8 RO CD56_CD3 | 8.3% |
| CD14+16+mono_total | 8.3% |
| NKCD16_NK | 8.3% |
| NKCD56hi_NK | 5.6% |
| Bcells memory_CD3neg | 5.6% |
| CD8 RO DR_total | 5.6% |
| CD14+16+mono_CD3neg | 5.6% |
| Bcells naive_total | 2.8% |
| Tconv memCD56_Tconv | 2.8% |
| CD8 RO CD56_total | 2.8% |
| CD14+16+mono_myeloid | 2.8% |
| CD8 RA naive_CD3 | 2.8% |

**Total features selected by NaiveBayes_Permutation_Top10%_t70**: 22

#### NaiveBayes_Permutation_Top10%_t80

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Bcells CD27posIgDneg_total | 40.0% |
| CD3hi_total | 24.0% |
| CD8  RO Ki67_CD3 | 16.0% |
| CD8 RO Ki67_CD8 | 12.0% |
| Ki67_Bcells | 8.0% |
| CD8 RO Ki67_total | 8.0% |
| Tconv memCD56_total | 8.0% |
| Bcells memory_total | 8.0% |
| Bcells naive_total | 4.0% |
| CD14+16+mono_myeloid | 4.0% |
| CD8 RO CD56_CD3 | 4.0% |
| CD14+16+mono_total | 4.0% |
| CD8 RO DR_CD3 | 4.0% |
| CD8 RO DR_total | 4.0% |
| Ki67_CD8RO | 4.0% |

**Total features selected by NaiveBayes_Permutation_Top10%_t80**: 15

#### RFE (RandomForest)_t40

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Bcells CD27posIgDneg_total | 100.0% |
| Tconv naive_Tconv | 100.0% |
| Tconv memCD27_Tconv | 100.0% |
| Tconv mem_Tconv | 100.0% |
| CD8  RO Ki67_CD3 | 100.0% |
| Tconv naive_CD3 | 100.0% |
| CD27IgD_Bcells | 100.0% |
| CD16mono_CD3neg | 100.0% |
| CD16mono_myeloid | 100.0% |
| Bcells_CD3neg | 100.0% |
| Bcells memory_CD3neg | 100.0% |
| CD8 RO DR_total | 100.0% |
| Tconv memPD1_total | 100.0% |
| memory_Bcells | 100.0% |
| Tconv memDR_CD3 | 100.0% |
| CD56_CD8RO | 100.0% |
| CD8 RO DR_CD3 | 100.0% |
| CD4 Treg_CD4 | 100.0% |
| Tconv memDR_mem | 100.0% |
| Tconv memDR_Tconv | 100.0% |
| Treg memory_CD4 | 100.0% |
| CD4 Treg _CD3 | 100.0% |
| DR_CD8RO | 100.0% |
| CD8 RO DR_CD8 | 100.0% |
| CD8 RO CCR5_CD3 | 97.5% |
| nonTnonB_CD3neg | 97.5% |
| Tconv naive_total | 97.5% |
| CD16+mono_total | 97.5% |
| Tconv memCCR5_mem | 97.5% |
| Tconv memCXCR3_mem | 97.5% |
| Treg memory_CD3 | 97.5% |
| CD27_CD8RO | 97.5% |
| CD14mono_myeloid | 97.5% |
| naive_Bcells | 97.5% |
| NKCD56hi_nonTnonB | 97.5% |
| Ki67_CD8RO | 97.5% |
| CXCR3_CD8RO | 97.5% |
| CCR4_CD8RO | 97.5% |
| Tconv memTIGIT_mem | 97.5% |
| CD27negIgDneg_Bcells | 95.0% |
| CD8 RO CD56_CD3 | 95.0% |
| CD8 RO CXCR3_CD3 | 95.0% |
| CCR5_CD8RO | 95.0% |
| CD8 RO CXCR3_CD8 | 95.0% |
| NKCD16_NK | 95.0% |
| Tconv memCCR6_CD3 | 95.0% |
| Tconv memPD1_mem | 95.0% |
| Ki67_Bcells | 95.0% |
| CD14+16+mono_myeloid | 95.0% |
| Bcells Ki67_total | 95.0% |
| CD8pos_CD3 | 95.0% |
| CD8 RO PD1_CD3 | 95.0% |
| Tconv memCXCR3_Tconv | 95.0% |
| Bcells_total | 95.0% |
| Tconv memCCR6_mem | 92.5% |
| Tconv memCD27_CD3 | 92.5% |
| Tconv memCCR4_total | 92.5% |
| CD8 RO CCR5_total | 92.5% |
| Tconv memCCR6_Tconv | 92.5% |
| Tconv memKi67_total | 92.5% |
| Tconv memCD27_mem | 92.5% |
| CD8 RO CD56_CD8 | 92.5% |
| NKCD56hi_NK | 92.5% |
| CD8 ncytotox RO CCR4_CD8ntox | 92.5% |
| intB7_CD8RO | 92.5% |
| Bcells naive_CD3neg | 92.5% |
| Tconv memCCR4_mem | 92.5% |
| CD8 RO CCR5_CD8 | 92.5% |
| CD4neg_CD3 | 92.5% |
| PD1_CD8RO | 92.5% |
| NKCD56hi_total | 92.5% |
| CD8 RA_CD3 | 92.5% |
| Tconv memKi67_mem | 92.5% |
| Tconv memPD1_Tconv | 92.5% |
| TIGIT_CD8RO | 90.0% |
| CCR6_CD8RO | 90.0% |
| CD8 RO PD1_CD8 | 90.0% |
| Bcells Ki67_CD3neg | 90.0% |
| CD4 Tconv_CD3 | 90.0% |
| Tconv memCXCR3_CD3 | 90.0% |
| CD3hi_CD3 | 90.0% |
| CD3neg_total | 90.0% |
| CD3pos_total | 90.0% |
| Tconv memCCR5_total | 90.0% |
| CD14mono_CD3neg | 90.0% |
| CD8 RO CD56_total | 90.0% |
| nonTnonB_total | 90.0% |
| CD3hi_total | 90.0% |
| NK_CD3neg | 90.0% |
| NK Ki67_nonTnonB | 90.0% |
| CD8 RO TIGIT_CD3 | 90.0% |
| Tconv memCD56_mem | 90.0% |
| NKCD16_total | 87.5% |
| Tconv memPD1_CD3 | 87.5% |
| Tconv memTIGIT_Tconv | 87.5% |
| CD8 RA_CD8 | 87.5% |
| CD8 RA naive_CD3 | 87.5% |
| CD4 Tconv_total | 87.5% |
| CD8 RO Ki67_CD8 | 87.5% |
| CD14+16+mono_CD3neg | 87.5% |
| NKCD16_CD3neg | 87.5% |
| NKCD56hi_CD3neg | 87.5% |
| CD8 RA CCR7 naive_CD8 | 87.5% |
| CD3hi_CD4neg | 87.5% |
| Bcells CD27negIgDneg_total | 85.0% |
| Treg naive_CD4 | 85.0% |
| CD8 RO CCR6_CD3 | 85.0% |
| CD8 RO CCR6_CD8 | 85.0% |
| Tconv memintB7_mem | 85.0% |
| CD8 RO CD27_CD3 | 85.0% |
| CD8 RO CD27_CD8 | 85.0% |
| Tconv memCD56_Tconv | 85.0% |
| Tconv memCD56_CD3 | 85.0% |
| NK Ki67_NK | 85.0% |
| CD14mono_total | 85.0% |
| Tconv memCXCR3_total | 85.0% |
| myeloid_CD3neg | 85.0% |
| Tconv memTIGIT_total | 85.0% |
| CD8 RO PD1_total | 82.5% |
| NKCD16_nonTnonB | 82.5% |
| Tconv memCD56_total | 82.5% |
| Tconv memCCR6_total | 82.5% |
| Treg naive_total | 82.5% |
| NK_nonTnonB | 82.5% |
| NK Ki67_CD3neg | 82.5% |
| CD8 RO_CD8 | 82.5% |
| CD4 Treg_total | 82.5% |
| CD8 RO_CD3 | 82.5% |
| CD8 ncytotox RO CCR4_CD3 | 82.5% |
| Tconv memTIGIT_CD3 | 82.5% |
| Bcells memory_total | 82.5% |
| CD8 RO TIGIT_CD8 | 82.5% |
| Tconv memCCR4_Tconv | 82.5% |
| CD8 RO intB7_CD8 | 80.0% |
| myeloid_total | 80.0% |
| Tconv memCCR5_CD3 | 80.0% |
| Tconv memintB7_total | 80.0% |
| NK Ki67_total | 77.5% |
| CD14+16+mono_total | 77.5% |
| Tconv memCCR4_CD3 | 77.5% |
| Tconv memintB7_Tconv | 77.5% |
| Treg memory_total | 77.5% |
| Tconv mem_CD3 | 77.5% |
| Bcells naive_total | 75.0% |
| Tconv memDR_total | 75.0% |
| Tconv memCCR5_Tconv | 75.0% |
| CD4neg_total | 72.5% |
| CD8pos_total | 72.5% |
| Treg naive_CD3 | 72.5% |
| NK_total | 72.5% |
| CD8 RO intB7_CD3 | 72.5% |
| CD4 Tconv mem_total | 70.0% |
| CD8 RA_total | 70.0% |
| CD8 RO CXCR3_total | 67.5% |
| CD8 RO Ki67_total | 65.0% |
| Tconv memCD27_total | 65.0% |
| Tconv memKi67_CD3 | 65.0% |
| Tconv memintB7_CD3 | 65.0% |
| CD8 RO TIGIT_total | 65.0% |
| Tconv memKi67_Tconv | 65.0% |
| CD8 RA naive_total | 62.5% |
| CD8 RO CCR4_total | 62.5% |
| CD8 RO CCR6_total | 60.0% |
| CD8 RO intB7_total | 57.5% |
| CD8 RO_total | 52.5% |
| CD8 RO CD27_total | 40.0% |

**Total features selected by RFE (RandomForest)_t40**: 166

#### RFE (RandomForest)_t50

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Bcells CD27posIgDneg_total | 100.0% |
| CD27IgD_Bcells | 100.0% |
| CD16mono_CD3neg | 100.0% |
| CD16mono_myeloid | 100.0% |
| CD4 Treg_CD4 | 100.0% |
| CD8 RO DR_CD3 | 100.0% |
| Bcells_CD3neg | 100.0% |
| Tconv memDR_mem | 100.0% |
| naive_Bcells | 97.5% |
| Tconv memCXCR3_mem | 97.5% |
| Tconv mem_Tconv | 97.5% |
| DR_CD8RO | 97.5% |
| Tconv naive_CD3 | 97.5% |
| Tconv naive_total | 97.5% |
| CD8 RO DR_CD8 | 97.5% |
| Tconv naive_Tconv | 95.0% |
| Tconv memPD1_total | 95.0% |
| CD14mono_myeloid | 95.0% |
| CD8 RO DR_total | 92.5% |
| memory_Bcells | 92.5% |
| nonTnonB_CD3neg | 92.5% |
| Tconv memDR_CD3 | 92.5% |
| CD8 RO PD1_CD3 | 92.5% |
| Treg memory_CD4 | 90.0% |
| CD8 RO CCR5_CD3 | 90.0% |
| CD8  RO Ki67_CD3 | 90.0% |
| Tconv memCD27_Tconv | 90.0% |
| CD3hi_total | 90.0% |
| Tconv memDR_Tconv | 90.0% |
| Tconv memCXCR3_Tconv | 90.0% |
| CD27_CD8RO | 90.0% |
| CD56_CD8RO | 90.0% |
| NKCD56hi_nonTnonB | 87.5% |
| Treg memory_CD3 | 87.5% |
| CD4 Treg _CD3 | 87.5% |
| Bcells_total | 87.5% |
| Tconv memPD1_mem | 87.5% |
| CD8pos_CD3 | 87.5% |
| CCR5_CD8RO | 85.0% |
| CD27negIgDneg_Bcells | 85.0% |
| Bcells naive_CD3neg | 85.0% |
| Bcells memory_CD3neg | 85.0% |
| intB7_CD8RO | 85.0% |
| NKCD56hi_NK | 85.0% |
| Ki67_Bcells | 85.0% |
| CD8 RO CCR5_total | 85.0% |
| CD16+mono_total | 85.0% |
| CD8 RO CXCR3_CD8 | 85.0% |
| Bcells Ki67_total | 85.0% |
| Tconv memTIGIT_mem | 85.0% |
| CXCR3_CD8RO | 82.5% |
| PD1_CD8RO | 82.5% |
| Tconv memCCR5_mem | 82.5% |
| Tconv memCCR6_mem | 82.5% |
| Tconv memCCR4_total | 82.5% |
| Tconv memCD27_mem | 82.5% |
| CD8 RO CD56_CD3 | 82.5% |
| Tconv memCCR6_Tconv | 80.0% |
| CCR6_CD8RO | 80.0% |
| CD14mono_CD3neg | 80.0% |
| CD8 RO CD56_CD8 | 80.0% |
| Tconv memPD1_CD3 | 80.0% |
| Tconv memCCR6_CD3 | 80.0% |
| NK_CD3neg | 80.0% |
| CD14+16+mono_myeloid | 80.0% |
| CCR4_CD8RO | 80.0% |
| CD8 RA naive_CD3 | 80.0% |
| CD4 Tconv_total | 77.5% |
| CD8 RO CXCR3_CD3 | 77.5% |
| Ki67_CD8RO | 77.5% |
| Tconv memKi67_mem | 77.5% |
| CD8 RO PD1_CD8 | 77.5% |
| Tconv memCXCR3_CD3 | 77.5% |
| TIGIT_CD8RO | 77.5% |
| NK Ki67_NK | 77.5% |
| CD8 RO CCR5_CD8 | 77.5% |
| CD8 RA CCR7 naive_CD8 | 77.5% |
| Tconv memCD56_mem | 77.5% |
| CD8 RO_CD3 | 77.5% |
| Bcells memory_total | 75.0% |
| CD4neg_CD3 | 75.0% |
| NKCD16_NK | 75.0% |
| CD3hi_CD3 | 75.0% |
| NKCD56hi_total | 75.0% |
| Tconv memPD1_Tconv | 75.0% |
| nonTnonB_total | 72.5% |
| CD4 Tconv_CD3 | 72.5% |
| Tconv memCCR4_mem | 72.5% |
| Bcells Ki67_CD3neg | 72.5% |
| NK Ki67_nonTnonB | 72.5% |
| CD3hi_CD4neg | 72.5% |
| CD8 ncytotox RO CCR4_CD8ntox | 72.5% |
| Tconv memCCR4_Tconv | 72.5% |
| NKCD56hi_CD3neg | 72.5% |
| CD8 RA_CD3 | 72.5% |
| NKCD16_total | 72.5% |
| CD3pos_total | 72.5% |
| Tconv memTIGIT_Tconv | 70.0% |
| Tconv memKi67_total | 70.0% |
| Tconv memCCR5_total | 70.0% |
| Treg naive_CD4 | 70.0% |
| CD3neg_total | 70.0% |
| Tconv memTIGIT_total | 70.0% |
| NKCD16_CD3neg | 70.0% |
| Tconv memCD27_CD3 | 70.0% |
| Tconv memintB7_mem | 67.5% |
| Tconv memCCR6_total | 67.5% |
| NKCD16_nonTnonB | 67.5% |
| CD8 RA_CD8 | 67.5% |
| NK_nonTnonB | 67.5% |
| CD8 RO Ki67_CD8 | 67.5% |
| CD8 RO TIGIT_CD3 | 67.5% |
| CD8 RO CD56_total | 67.5% |
| CD4 Treg_total | 65.0% |
| CD14+16+mono_CD3neg | 65.0% |
| CD8 RO intB7_CD8 | 65.0% |
| CD14mono_total | 65.0% |
| CD8 RO CD27_CD3 | 65.0% |
| Tconv memintB7_total | 65.0% |
| Tconv memDR_total | 62.5% |
| Tconv memCD56_Tconv | 62.5% |
| Bcells CD27negIgDneg_total | 62.5% |
| Tconv memCD56_total | 62.5% |
| Tconv mem_CD3 | 62.5% |
| Tconv memintB7_Tconv | 62.5% |
| CD8 RO CCR6_CD8 | 62.5% |
| CD8 ncytotox RO CCR4_CD3 | 60.0% |
| CD8 RO PD1_total | 60.0% |
| Tconv memKi67_Tconv | 60.0% |
| CD8 RO intB7_CD3 | 60.0% |
| Bcells naive_total | 60.0% |
| Treg naive_CD3 | 60.0% |
| Tconv memCXCR3_total | 60.0% |
| CD8 RO TIGIT_CD8 | 60.0% |
| CD8 RO CCR6_CD3 | 57.5% |
| NK_total | 57.5% |
| Tconv memCCR4_CD3 | 57.5% |
| NK Ki67_CD3neg | 57.5% |
| CD8 RA_total | 57.5% |
| Tconv memTIGIT_CD3 | 55.0% |
| Treg memory_total | 55.0% |
| CD8 RO CD27_CD8 | 55.0% |
| CD4 Tconv mem_total | 55.0% |
| myeloid_CD3neg | 55.0% |
| Tconv memCCR5_Tconv | 55.0% |
| CD14+16+mono_total | 55.0% |
| NK Ki67_total | 52.5% |
| CD8 RO_CD8 | 52.5% |
| Tconv memCCR5_CD3 | 52.5% |
| Tconv memCD56_CD3 | 50.0% |
| myeloid_total | 47.5% |
| CD8 RO Ki67_total | 47.5% |
| Tconv memCD27_total | 45.0% |
| CD8 RO CXCR3_total | 45.0% |
| CD8pos_total | 45.0% |
| Treg naive_total | 45.0% |
| Tconv memintB7_CD3 | 42.5% |
| Tconv memKi67_CD3 | 42.5% |
| CD8 RA naive_total | 37.5% |
| CD8 RO CCR4_total | 35.0% |
| CD4neg_total | 32.5% |
| CD8 RO intB7_total | 32.5% |
| CD8 RO CCR6_total | 32.5% |
| CD8 RO TIGIT_total | 30.0% |
| CD8 RO_total | 25.0% |
| CD8 RO CD27_total | 20.0% |

**Total features selected by RFE (RandomForest)_t50**: 166

#### RFE (RandomForest)_t60

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Bcells CD27posIgDneg_total | 100.0% |
| CD16mono_myeloid | 100.0% |
| CD27IgD_Bcells | 100.0% |
| CD16mono_CD3neg | 100.0% |
| Tconv naive_total | 97.5% |
| CD8 RO DR_CD3 | 97.5% |
| Tconv memDR_mem | 95.0% |
| DR_CD8RO | 92.5% |
| CD8 RO DR_CD8 | 92.5% |
| Tconv memPD1_total | 92.5% |
| CD4 Treg_CD4 | 90.0% |
| naive_Bcells | 90.0% |
| Tconv naive_CD3 | 90.0% |
| Tconv mem_Tconv | 87.5% |
| CD4 Treg _CD3 | 87.5% |
| Tconv naive_Tconv | 85.0% |
| Tconv memCD27_Tconv | 85.0% |
| Treg memory_CD4 | 85.0% |
| Bcells_CD3neg | 85.0% |
| Tconv memDR_Tconv | 82.5% |
| CD3hi_total | 80.0% |
| CD8  RO Ki67_CD3 | 80.0% |
| Tconv memCXCR3_Tconv | 80.0% |
| CD8 RO PD1_CD3 | 80.0% |
| CD14mono_myeloid | 77.5% |
| CCR5_CD8RO | 77.5% |
| Bcells memory_CD3neg | 77.5% |
| nonTnonB_CD3neg | 77.5% |
| CD16+mono_total | 77.5% |
| CD8 RO DR_total | 77.5% |
| memory_Bcells | 77.5% |
| Tconv memCXCR3_mem | 75.0% |
| Tconv memPD1_mem | 75.0% |
| Ki67_Bcells | 75.0% |
| Treg memory_CD3 | 75.0% |
| Tconv memDR_CD3 | 72.5% |
| Tconv memCCR6_mem | 72.5% |
| Tconv memCCR6_Tconv | 70.0% |
| Tconv memCCR6_CD3 | 70.0% |
| CD8 RO CCR5_CD3 | 70.0% |
| CD8 RO CD56_CD3 | 70.0% |
| Bcells naive_CD3neg | 70.0% |
| Tconv memTIGIT_mem | 70.0% |
| intB7_CD8RO | 70.0% |
| NKCD56hi_nonTnonB | 67.5% |
| CD27_CD8RO | 67.5% |
| Tconv memCCR5_mem | 65.0% |
| CD8 RO CCR5_total | 65.0% |
| CD8 RO CXCR3_CD3 | 65.0% |
| CD8pos_CD3 | 65.0% |
| CD56_CD8RO | 65.0% |
| CD4 Tconv_total | 65.0% |
| CD8 RA CCR7 naive_CD8 | 65.0% |
| NKCD56hi_NK | 65.0% |
| CD8 RO CD56_CD8 | 65.0% |
| Tconv memCXCR3_CD3 | 62.5% |
| CD8 RO PD1_CD8 | 62.5% |
| Tconv memCD27_CD3 | 62.5% |
| TIGIT_CD8RO | 62.5% |
| Tconv memCCR4_Tconv | 62.5% |
| CD27negIgDneg_Bcells | 62.5% |
| Tconv memPD1_Tconv | 60.0% |
| CD3pos_total | 60.0% |
| NK Ki67_nonTnonB | 60.0% |
| CCR6_CD8RO | 60.0% |
| NKCD16_NK | 60.0% |
| Tconv memCD56_mem | 60.0% |
| Bcells Ki67_CD3neg | 60.0% |
| CD8 RA naive_CD3 | 60.0% |
| CD14+16+mono_myeloid | 60.0% |
| Bcells_total | 57.5% |
| CD8 ncytotox RO CCR4_CD8ntox | 57.5% |
| CD14mono_CD3neg | 57.5% |
| NKCD56hi_total | 57.5% |
| CD8 RO CXCR3_CD8 | 57.5% |
| CXCR3_CD8RO | 57.5% |
| nonTnonB_total | 55.0% |
| Tconv memCCR4_total | 55.0% |
| Bcells Ki67_total | 55.0% |
| CD3hi_CD3 | 55.0% |
| NK_CD3neg | 55.0% |
| Tconv memPD1_CD3 | 55.0% |
| CD4neg_CD3 | 55.0% |
| NKCD56hi_CD3neg | 55.0% |
| PD1_CD8RO | 55.0% |
| NKCD16_CD3neg | 55.0% |
| Tconv memTIGIT_total | 52.5% |
| CD8 RO TIGIT_CD3 | 52.5% |
| Tconv memKi67_mem | 52.5% |
| NK Ki67_NK | 52.5% |
| CD3neg_total | 52.5% |
| CD3hi_CD4neg | 50.0% |
| Tconv memDR_total | 50.0% |
| CD8 RA_CD3 | 50.0% |
| CCR4_CD8RO | 47.5% |
| Tconv memCCR4_mem | 47.5% |
| Bcells memory_total | 47.5% |
| Bcells CD27negIgDneg_total | 47.5% |
| Treg naive_CD4 | 47.5% |
| Tconv memCD27_mem | 47.5% |
| CD4 Tconv_CD3 | 47.5% |
| CD8 RO_CD3 | 47.5% |
| Tconv memCCR6_total | 45.0% |
| Ki67_CD8RO | 45.0% |
| Tconv mem_CD3 | 45.0% |
| CD8 RO CCR5_CD8 | 45.0% |
| Tconv memCD56_Tconv | 45.0% |
| CD14+16+mono_CD3neg | 42.5% |
| Tconv memintB7_Tconv | 42.5% |
| Tconv memTIGIT_Tconv | 42.5% |
| CD8 RO CD27_CD3 | 42.5% |
| CD8 RO TIGIT_CD8 | 42.5% |
| CD14mono_total | 42.5% |
| CD8 RO CD56_total | 42.5% |
| NK Ki67_CD3neg | 42.5% |
| NKCD16_total | 40.0% |
| Tconv memCCR5_total | 40.0% |
| Treg memory_total | 40.0% |
| CD8 RA_CD8 | 40.0% |
| CD8 RO intB7_CD8 | 40.0% |
| NK_total | 40.0% |
| Tconv memCCR5_Tconv | 40.0% |
| CD4 Treg_total | 40.0% |
| Tconv memCCR4_CD3 | 37.5% |
| Tconv memKi67_total | 37.5% |
| CD8 RO Ki67_CD8 | 37.5% |
| Tconv memCCR5_CD3 | 37.5% |
| Bcells naive_total | 37.5% |
| Tconv memintB7_total | 37.5% |
| Tconv memKi67_Tconv | 35.0% |
| Tconv memCD56_CD3 | 35.0% |
| CD8 RO Ki67_total | 35.0% |
| CD14+16+mono_total | 35.0% |
| myeloid_total | 35.0% |
| Tconv memintB7_CD3 | 35.0% |
| NK_nonTnonB | 35.0% |
| Tconv memCXCR3_total | 32.5% |
| Treg naive_CD3 | 32.5% |
| NKCD16_nonTnonB | 32.5% |
| CD8 RO intB7_CD3 | 32.5% |
| CD8 ncytotox RO CCR4_CD3 | 32.5% |
| CD8 RO PD1_total | 32.5% |
| NK Ki67_total | 30.0% |
| CD8 RO CCR6_CD8 | 30.0% |
| CD4 Tconv mem_total | 30.0% |
| CD8 RO CCR6_CD3 | 30.0% |
| Tconv memTIGIT_CD3 | 30.0% |
| CD8pos_total | 27.5% |
| CD8 RO CD27_CD8 | 27.5% |
| Tconv memintB7_mem | 27.5% |
| CD8 RO_CD8 | 27.5% |
| myeloid_CD3neg | 27.5% |
| Treg naive_total | 25.0% |
| CD8 RO CXCR3_total | 22.5% |
| CD8 RO CCR6_total | 22.5% |
| Tconv memCD27_total | 22.5% |
| Tconv memCD56_total | 22.5% |
| Tconv memKi67_CD3 | 22.5% |
| CD8 RA naive_total | 20.0% |
| CD8 RA_total | 20.0% |
| CD8 RO TIGIT_total | 12.5% |
| CD4neg_total | 12.5% |
| CD8 RO intB7_total | 12.5% |
| CD8 RO_total | 10.0% |
| CD8 RO CCR4_total | 10.0% |
| CD8 RO CD27_total | 5.0% |

**Total features selected by RFE (RandomForest)_t60**: 166

#### RFE (RandomForest)_t70

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Bcells CD27posIgDneg_total | 100.0% |
| CD27IgD_Bcells | 97.5% |
| CD16mono_CD3neg | 95.0% |
| CD16mono_myeloid | 95.0% |
| CD8 RO DR_CD3 | 95.0% |
| CD4 Treg_CD4 | 90.0% |
| Tconv naive_total | 87.5% |
| Tconv naive_CD3 | 85.0% |
| CD8 RO DR_CD8 | 80.0% |
| Tconv memDR_mem | 80.0% |
| Tconv mem_Tconv | 77.5% |
| DR_CD8RO | 77.5% |
| Tconv naive_Tconv | 75.0% |
| Treg memory_CD4 | 75.0% |
| Bcells_CD3neg | 72.5% |
| Tconv memDR_Tconv | 70.0% |
| Tconv memCD27_Tconv | 67.5% |
| CD8 RO PD1_CD3 | 65.0% |
| CD14mono_myeloid | 65.0% |
| memory_Bcells | 62.5% |
| Bcells memory_CD3neg | 62.5% |
| CD4 Treg _CD3 | 62.5% |
| Tconv memDR_CD3 | 60.0% |
| Tconv memCXCR3_Tconv | 60.0% |
| Treg memory_CD3 | 60.0% |
| nonTnonB_CD3neg | 60.0% |
| Ki67_Bcells | 60.0% |
| CD3hi_total | 55.0% |
| Tconv memCXCR3_mem | 55.0% |
| CD8  RO Ki67_CD3 | 52.5% |
| CD16+mono_total | 52.5% |
| Tconv memCCR6_Tconv | 52.5% |
| Tconv memPD1_mem | 52.5% |
| naive_Bcells | 52.5% |
| CD4 Tconv_total | 50.0% |
| Tconv memCCR5_mem | 50.0% |
| Tconv memPD1_total | 50.0% |
| CD8 RO CCR5_CD3 | 47.5% |
| Tconv memTIGIT_mem | 47.5% |
| CD8 RO DR_total | 47.5% |
| CD8 RA CCR7 naive_CD8 | 45.0% |
| NK Ki67_nonTnonB | 45.0% |
| NKCD16_NK | 45.0% |
| CCR5_CD8RO | 45.0% |
| Tconv memCXCR3_CD3 | 45.0% |
| CD8pos_CD3 | 45.0% |
| Bcells naive_CD3neg | 45.0% |
| CXCR3_CD8RO | 45.0% |
| NKCD56hi_nonTnonB | 45.0% |
| CD56_CD8RO | 45.0% |
| NKCD56hi_NK | 42.5% |
| CD8 RO CXCR3_CD3 | 42.5% |
| CD27_CD8RO | 42.5% |
| Tconv memCCR6_mem | 42.5% |
| CD14+16+mono_myeloid | 42.5% |
| CD8 RO CD56_CD3 | 42.5% |
| intB7_CD8RO | 42.5% |
| CD8 RO CD56_CD8 | 40.0% |
| nonTnonB_total | 40.0% |
| CD8 RA naive_CD3 | 40.0% |
| CD27negIgDneg_Bcells | 40.0% |
| Tconv memCCR6_CD3 | 40.0% |
| NK Ki67_NK | 40.0% |
| Bcells Ki67_CD3neg | 37.5% |
| TIGIT_CD8RO | 37.5% |
| CD3neg_total | 37.5% |
| CD14mono_CD3neg | 37.5% |
| CD3hi_CD3 | 37.5% |
| Tconv memCD56_mem | 35.0% |
| Tconv memPD1_Tconv | 35.0% |
| Tconv memCCR4_Tconv | 35.0% |
| Tconv mem_CD3 | 35.0% |
| NKCD56hi_total | 35.0% |
| CD3pos_total | 35.0% |
| CD8 RO TIGIT_CD3 | 35.0% |
| Bcells Ki67_total | 32.5% |
| CD8 RO CXCR3_CD8 | 32.5% |
| Bcells_total | 32.5% |
| NKCD56hi_CD3neg | 32.5% |
| Tconv memTIGIT_total | 30.0% |
| CD8 RO_CD3 | 30.0% |
| Tconv memCD56_Tconv | 30.0% |
| Bcells memory_total | 30.0% |
| CD4neg_CD3 | 30.0% |
| CD3hi_CD4neg | 30.0% |
| CD8 RA_CD3 | 30.0% |
| Tconv memCD27_CD3 | 30.0% |
| CD8 RO CCR5_total | 30.0% |
| PD1_CD8RO | 30.0% |
| Tconv memKi67_mem | 30.0% |
| Tconv memintB7_Tconv | 30.0% |
| NK_total | 27.5% |
| Bcells CD27negIgDneg_total | 27.5% |
| CD8 RO PD1_CD8 | 27.5% |
| NKCD16_CD3neg | 27.5% |
| Tconv memKi67_total | 27.5% |
| CCR6_CD8RO | 27.5% |
| NKCD16_total | 27.5% |
| CD8 RO CCR5_CD8 | 27.5% |
| CD8 ncytotox RO CCR4_CD8ntox | 25.0% |
| Treg naive_CD4 | 25.0% |
| CD4 Tconv_CD3 | 25.0% |
| CD14+16+mono_CD3neg | 25.0% |
| Treg memory_total | 25.0% |
| Tconv memCCR5_total | 25.0% |
| myeloid_total | 25.0% |
| Bcells naive_total | 25.0% |
| Tconv memPD1_CD3 | 25.0% |
| Tconv memCCR4_total | 25.0% |
| Tconv memCCR6_total | 25.0% |
| CD4 Tconv mem_total | 25.0% |
| CCR4_CD8RO | 25.0% |
| CD14mono_total | 22.5% |
| CD4 Treg_total | 22.5% |
| Tconv memCD27_mem | 22.5% |
| NK_CD3neg | 22.5% |
| Tconv memDR_total | 22.5% |
| Tconv memintB7_total | 22.5% |
| Tconv memTIGIT_Tconv | 22.5% |
| Tconv memCCR4_mem | 22.5% |
| Tconv memCCR5_Tconv | 22.5% |
| CD14+16+mono_total | 20.0% |
| Tconv memintB7_CD3 | 20.0% |
| CD8 RO CD27_CD3 | 20.0% |
| CD8 RA_CD8 | 20.0% |
| NK_nonTnonB | 20.0% |
| Ki67_CD8RO | 20.0% |
| NK Ki67_total | 20.0% |
| NK Ki67_CD3neg | 20.0% |
| Tconv memTIGIT_CD3 | 17.5% |
| Tconv memCD56_total | 17.5% |
| CD8 RO Ki67_CD8 | 17.5% |
| CD8 RO CD56_total | 17.5% |
| Tconv memintB7_mem | 17.5% |
| CD8 RO intB7_CD8 | 17.5% |
| CD8 RO CCR6_CD8 | 17.5% |
| Tconv memCCR4_CD3 | 17.5% |
| Tconv memCCR5_CD3 | 17.5% |
| CD8 RO CCR6_CD3 | 17.5% |
| CD8pos_total | 15.0% |
| CD8 RO TIGIT_CD8 | 15.0% |
| Tconv memKi67_Tconv | 15.0% |
| CD8 RO_CD8 | 15.0% |
| CD8 RO PD1_total | 15.0% |
| Tconv memCD56_CD3 | 15.0% |
| Tconv memCXCR3_total | 15.0% |
| CD8 ncytotox RO CCR4_CD3 | 15.0% |
| CD8 RO CXCR3_total | 15.0% |
| CD8 RO intB7_CD3 | 12.5% |
| Tconv memCD27_total | 12.5% |
| Treg naive_total | 12.5% |
| NKCD16_nonTnonB | 12.5% |
| CD8 RO Ki67_total | 12.5% |
| Treg naive_CD3 | 12.5% |
| CD8 RA_total | 12.5% |
| Tconv memKi67_CD3 | 10.0% |
| CD4neg_total | 10.0% |
| CD8 RO CD27_CD8 | 10.0% |
| myeloid_CD3neg | 7.5% |
| CD8 RO CCR4_total | 5.0% |
| CD8 RO CCR6_total | 5.0% |
| CD8 RO CD27_total | 2.5% |
| CD8 RO TIGIT_total | 2.5% |

**Total features selected by RFE (RandomForest)_t70**: 163

#### RFE (RandomForest)_t80

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Bcells CD27posIgDneg_total | 97.5% |
| CD27IgD_Bcells | 92.5% |
| CD8 RO DR_CD3 | 90.0% |
| CD16mono_myeloid | 85.0% |
| CD4 Treg_CD4 | 70.0% |
| Tconv naive_total | 70.0% |
| CD16mono_CD3neg | 70.0% |
| Treg memory_CD4 | 65.0% |
| Tconv memDR_Tconv | 62.5% |
| DR_CD8RO | 62.5% |
| Tconv memDR_mem | 62.5% |
| Tconv mem_Tconv | 57.5% |
| CD8 RO DR_CD8 | 57.5% |
| Tconv naive_CD3 | 55.0% |
| Tconv naive_Tconv | 52.5% |
| Bcells_CD3neg | 47.5% |
| nonTnonB_CD3neg | 42.5% |
| Tconv memCXCR3_mem | 42.5% |
| Bcells memory_CD3neg | 40.0% |
| CD14mono_myeloid | 40.0% |
| Tconv memPD1_mem | 37.5% |
| Ki67_Bcells | 37.5% |
| Tconv memCD27_Tconv | 37.5% |
| Tconv memDR_CD3 | 37.5% |
| CD8 RO DR_total | 37.5% |
| CD8 RO PD1_CD3 | 35.0% |
| naive_Bcells | 35.0% |
| CD3hi_total | 35.0% |
| Treg memory_CD3 | 35.0% |
| CD8  RO Ki67_CD3 | 32.5% |
| CD4 Tconv_total | 32.5% |
| CD14+16+mono_myeloid | 30.0% |
| Tconv memCXCR3_Tconv | 30.0% |
| NKCD16_NK | 30.0% |
| Bcells naive_CD3neg | 30.0% |
| CD4 Treg _CD3 | 30.0% |
| Tconv memCCR6_Tconv | 27.5% |
| CD8 RA CCR7 naive_CD8 | 27.5% |
| CD8pos_CD3 | 27.5% |
| CCR5_CD8RO | 27.5% |
| NKCD56hi_total | 25.0% |
| Tconv memTIGIT_mem | 25.0% |
| Tconv memPD1_total | 25.0% |
| NK Ki67_nonTnonB | 25.0% |
| CD8 RO CCR5_CD3 | 25.0% |
| CD56_CD8RO | 25.0% |
| CD3neg_total | 22.5% |
| CD8 RO CD56_CD3 | 22.5% |
| Tconv memCCR6_mem | 22.5% |
| NKCD56hi_NK | 22.5% |
| CD3hi_CD3 | 22.5% |
| CD3pos_total | 20.0% |
| CD4 Tconv_CD3 | 20.0% |
| Tconv memCCR6_total | 20.0% |
| Tconv memPD1_Tconv | 20.0% |
| CD27negIgDneg_Bcells | 20.0% |
| CD8 RO CCR5_CD8 | 20.0% |
| CD8 RO CXCR3_CD3 | 20.0% |
| NK Ki67_NK | 20.0% |
| Tconv memCXCR3_CD3 | 20.0% |
| Bcells memory_total | 20.0% |
| CD16+mono_total | 20.0% |
| Tconv memCD27_mem | 20.0% |
| Tconv mem_CD3 | 20.0% |
| Bcells Ki67_total | 17.5% |
| nonTnonB_total | 17.5% |
| myeloid_total | 17.5% |
| CD8 RO CXCR3_CD8 | 17.5% |
| TIGIT_CD8RO | 17.5% |
| CCR6_CD8RO | 17.5% |
| CD8 RO_CD3 | 17.5% |
| Bcells Ki67_CD3neg | 17.5% |
| memory_Bcells | 17.5% |
| NKCD56hi_nonTnonB | 17.5% |
| Tconv memintB7_Tconv | 17.5% |
| CD8 RO CCR5_total | 17.5% |
| Tconv memCD56_mem | 17.5% |
| Tconv memCCR5_mem | 17.5% |
| CD8 RO CD56_CD8 | 15.0% |
| NKCD56hi_CD3neg | 15.0% |
| CD8 RA naive_CD3 | 15.0% |
| intB7_CD8RO | 15.0% |
| Tconv memKi67_mem | 15.0% |
| CXCR3_CD8RO | 15.0% |
| CD14+16+mono_CD3neg | 15.0% |
| CD8 RA_CD3 | 15.0% |
| Tconv memCCR6_CD3 | 15.0% |
| CD4neg_CD3 | 15.0% |
| Bcells_total | 15.0% |
| Treg naive_CD4 | 15.0% |
| CD27_CD8RO | 15.0% |
| NKCD16_CD3neg | 12.5% |
| Tconv memPD1_CD3 | 12.5% |
| Tconv memTIGIT_total | 12.5% |
| NK_total | 12.5% |
| Tconv memCCR5_total | 12.5% |
| CD14mono_CD3neg | 12.5% |
| Tconv memCCR4_total | 12.5% |
| CD3hi_CD4neg | 12.5% |
| CD8 RO TIGIT_CD3 | 12.5% |
| Tconv memCD27_CD3 | 12.5% |
| Tconv memCCR4_mem | 12.5% |
| Tconv memDR_total | 12.5% |
| NKCD16_total | 12.5% |
| Treg memory_total | 12.5% |
| Tconv memCD56_Tconv | 10.0% |
| Bcells CD27negIgDneg_total | 10.0% |
| CD8 RO CXCR3_total | 10.0% |
| CD8 RO PD1_total | 10.0% |
| CCR4_CD8RO | 10.0% |
| Tconv memCCR4_Tconv | 10.0% |
| CD8 RA_CD8 | 10.0% |
| CD8 RA_total | 10.0% |
| Tconv memKi67_total | 10.0% |
| CD14+16+mono_total | 10.0% |
| CD8 RO CD27_CD3 | 10.0% |
| CD4 Treg_total | 10.0% |
| CD8 RO PD1_CD8 | 10.0% |
| CD8 RO intB7_CD3 | 7.5% |
| CD4 Tconv mem_total | 7.5% |
| NK_CD3neg | 7.5% |
| PD1_CD8RO | 7.5% |
| NK Ki67_total | 7.5% |
| NKCD16_nonTnonB | 7.5% |
| CD8 RO intB7_CD8 | 7.5% |
| Ki67_CD8RO | 7.5% |
| Treg naive_total | 7.5% |
| Tconv memCCR4_CD3 | 7.5% |
| Tconv memintB7_mem | 7.5% |
| Tconv memCD27_total | 5.0% |
| CD14mono_total | 5.0% |
| Tconv memCCR5_Tconv | 5.0% |
| Tconv memintB7_total | 5.0% |
| CD8 ncytotox RO CCR4_CD8ntox | 5.0% |
| Tconv memCCR5_CD3 | 5.0% |
| CD8 RO CCR6_CD3 | 5.0% |
| CD8 RO Ki67_total | 5.0% |
| CD8 RO TIGIT_CD8 | 5.0% |
| Tconv memCD56_CD3 | 5.0% |
| Tconv memTIGIT_Tconv | 5.0% |
| CD8 RO CD27_CD8 | 5.0% |
| CD8 RO Ki67_CD8 | 5.0% |
| CD8 ncytotox RO CCR4_CD3 | 2.5% |
| CD8 RO CCR4_total | 2.5% |
| CD4neg_total | 2.5% |
| Treg naive_CD3 | 2.5% |
| Bcells naive_total | 2.5% |
| CD8 RO_CD8 | 2.5% |
| NK Ki67_CD3neg | 2.5% |
| myeloid_CD3neg | 2.5% |
| NK_nonTnonB | 2.5% |
| Tconv memCD56_total | 2.5% |
| Tconv memKi67_CD3 | 2.5% |
| Tconv memTIGIT_CD3 | 2.5% |
| CD8 RO CCR6_total | 2.5% |
| Tconv memKi67_Tconv | 2.5% |
| Tconv memCXCR3_total | 2.5% |
| CD8pos_total | 2.5% |
| CD8 RO CD27_total | 2.5% |
| CD8 RO CD56_total | 2.5% |
| CD8 RO CCR6_CD8 | 2.5% |
| CD8 RO TIGIT_total | 2.5% |
| Tconv memintB7_CD3 | 2.5% |

**Total features selected by RFE (RandomForest)_t80**: 163

#### RF_Importance_t40

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Bcells CD27posIgDneg_total | 100.0% |
| CD27IgD_Bcells | 100.0% |
| CD4 Treg_CD4 | 100.0% |
| CD16mono_myeloid | 100.0% |
| Tconv mem_Tconv | 97.5% |
| Treg memory_CD4 | 97.5% |
| CD8 RO DR_CD3 | 97.5% |
| Tconv naive_CD3 | 97.5% |
| Tconv naive_total | 97.5% |
| Tconv memDR_Tconv | 95.0% |
| Tconv memDR_mem | 95.0% |
| CD8 RO DR_CD8 | 90.0% |
| Tconv memCD27_Tconv | 87.5% |
| Tconv naive_Tconv | 87.5% |
| CD16mono_CD3neg | 87.5% |
| Tconv memDR_CD3 | 85.0% |
| DR_CD8RO | 80.0% |
| Treg memory_CD3 | 80.0% |
| Bcells memory_CD3neg | 77.5% |
| Tconv memPD1_total | 77.5% |
| Tconv memCXCR3_Tconv | 75.0% |
| Ki67_Bcells | 75.0% |
| nonTnonB_total | 75.0% |
| CD3neg_total | 75.0% |
| CD8pos_CD3 | 72.5% |
| Bcells_CD3neg | 70.0% |
| nonTnonB_CD3neg | 70.0% |
| CD4 Treg _CD3 | 70.0% |
| CD8 RO DR_total | 70.0% |
| Bcells_total | 67.5% |
| CD3hi_total | 67.5% |
| CD4 Tconv_total | 67.5% |
| CD14mono_myeloid | 62.5% |
| CD8 RO PD1_CD3 | 62.5% |
| CD8  RO Ki67_CD3 | 62.5% |
| CD8 RO CXCR3_CD3 | 60.0% |
| CD3pos_total | 60.0% |
| Bcells memory_total | 60.0% |
| CD8 RO CD56_CD3 | 57.5% |
| Tconv memCXCR3_mem | 55.0% |
| Tconv memCXCR3_CD3 | 55.0% |
| CD8 RA CCR7 naive_CD8 | 55.0% |
| CCR5_CD8RO | 55.0% |
| CD16+mono_total | 55.0% |
| CD8 RO CCR5_CD3 | 52.5% |
| CD3hi_CD3 | 52.5% |
| CD8 RO CCR5_total | 52.5% |
| CD8 RA naive_CD3 | 50.0% |
| Tconv memTIGIT_total | 50.0% |
| CD14mono_total | 47.5% |
| Tconv mem_CD3 | 47.5% |
| naive_Bcells | 47.5% |
| Tconv memCCR6_Tconv | 47.5% |
| CD8 RO TIGIT_CD3 | 47.5% |
| Tconv memTIGIT_mem | 47.5% |
| CD4 Tconv_CD3 | 47.5% |
| Tconv memCCR5_mem | 45.0% |
| CD56_CD8RO | 45.0% |
| Tconv memCD27_CD3 | 45.0% |
| NKCD56hi_nonTnonB | 42.5% |
| Tconv memCD27_mem | 42.5% |
| Tconv memPD1_mem | 42.5% |
| NKCD16_NK | 40.0% |
| NKCD56hi_NK | 40.0% |
| CD4neg_CD3 | 40.0% |
| Bcells naive_CD3neg | 40.0% |
| memory_Bcells | 37.5% |
| NKCD56hi_total | 37.5% |
| CD8 RO_CD3 | 35.0% |
| CD8 RO CXCR3_CD8 | 35.0% |
| Tconv memintB7_Tconv | 35.0% |
| CD8pos_total | 35.0% |
| Tconv memCCR6_total | 35.0% |
| CD8 RA_CD3 | 35.0% |
| Tconv memCCR4_Tconv | 35.0% |
| myeloid_total | 32.5% |
| NKCD16_total | 32.5% |
| Tconv memKi67_total | 32.5% |
| CD14mono_CD3neg | 32.5% |
| CD8 RO CCR5_CD8 | 32.5% |
| CD27negIgDneg_Bcells | 32.5% |
| Tconv memDR_total | 32.5% |
| Tconv memCCR6_mem | 30.0% |
| Tconv memCCR6_CD3 | 30.0% |
| Tconv memCCR4_CD3 | 30.0% |
| CD14+16+mono_myeloid | 30.0% |
| Tconv memCCR4_mem | 30.0% |
| Tconv memCXCR3_total | 27.5% |
| Treg naive_total | 27.5% |
| Tconv memCCR4_total | 27.5% |
| CD4 Tconv mem_total | 27.5% |
| Tconv memCCR5_total | 27.5% |
| NK_total | 27.5% |
| intB7_CD8RO | 27.5% |
| CD8 RO CD56_CD8 | 27.5% |
| Tconv memPD1_CD3 | 27.5% |
| NK Ki67_CD3neg | 25.0% |
| Tconv memTIGIT_Tconv | 25.0% |
| Treg naive_CD4 | 25.0% |
| NKCD16_CD3neg | 25.0% |
| Tconv memKi67_mem | 25.0% |
| TIGIT_CD8RO | 25.0% |
| CD8 RO CXCR3_total | 25.0% |
| CD8 RO CD27_CD3 | 22.5% |
| NK Ki67_NK | 22.5% |
| Tconv memintB7_total | 22.5% |
| CD14+16+mono_total | 22.5% |
| Bcells Ki67_CD3neg | 22.5% |
| CD8 RO CD56_total | 22.5% |
| CD4 Treg_total | 22.5% |
| Bcells naive_total | 22.5% |
| Tconv memCD56_Tconv | 22.5% |
| Tconv memPD1_Tconv | 22.5% |
| NKCD56hi_CD3neg | 20.0% |
| Tconv memCCR5_Tconv | 20.0% |
| Ki67_CD8RO | 20.0% |
| CD8 ncytotox RO CCR4_CD8ntox | 20.0% |
| CD8 RO TIGIT_CD8 | 20.0% |
| Tconv memintB7_mem | 20.0% |
| CD27_CD8RO | 20.0% |
| NK Ki67_nonTnonB | 20.0% |
| Tconv memCD27_total | 20.0% |
| CD8 RO PD1_CD8 | 20.0% |
| Tconv memKi67_Tconv | 20.0% |
| PD1_CD8RO | 17.5% |
| CD8 RO PD1_total | 17.5% |
| Tconv memCD56_mem | 17.5% |
| Tconv memCD56_CD3 | 17.5% |
| CD8 RA naive_total | 17.5% |
| CD3hi_CD4neg | 17.5% |
| CCR4_CD8RO | 15.0% |
| CXCR3_CD8RO | 15.0% |
| NK_CD3neg | 15.0% |
| NK Ki67_total | 15.0% |
| CD8 ncytotox RO CCR4_CD3 | 15.0% |
| CD8 RA_total | 15.0% |
| Treg naive_CD3 | 15.0% |
| Tconv memTIGIT_CD3 | 15.0% |
| CD8 RO intB7_CD3 | 12.5% |
| Bcells CD27negIgDneg_total | 12.5% |
| CD8 RA_CD8 | 12.5% |
| CD8 RO CD27_CD8 | 12.5% |
| CD14+16+mono_CD3neg | 12.5% |
| NKCD16_nonTnonB | 12.5% |
| CCR6_CD8RO | 12.5% |
| Bcells Ki67_total | 12.5% |
| Treg memory_total | 12.5% |
| Tconv memCD56_total | 12.5% |
| CD8 RO Ki67_CD8 | 10.0% |
| CD8 RO TIGIT_total | 10.0% |
| Tconv memCCR5_CD3 | 10.0% |
| CD8 RO CCR4_total | 10.0% |
| myeloid_CD3neg | 7.5% |
| CD8 RO_CD8 | 7.5% |
| Tconv memintB7_CD3 | 7.5% |
| CD8 RO CCR6_CD3 | 7.5% |
| CD8 RO Ki67_total | 7.5% |
| NK_nonTnonB | 7.5% |
| CD4neg_total | 5.0% |
| CD8 RO CCR6_total | 5.0% |
| CD8 RO intB7_CD8 | 5.0% |
| CD8 RO intB7_total | 5.0% |
| CD8 RO_total | 2.5% |
| CD8 RO CCR6_CD8 | 2.5% |
| CD8 RO CD27_total | 2.5% |

**Total features selected by RF_Importance_t40**: 165

#### RF_Importance_t50

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Bcells CD27posIgDneg_total | 100.0% |
| CD16mono_myeloid | 100.0% |
| Tconv mem_Tconv | 97.5% |
| CD8 RO DR_CD3 | 97.5% |
| CD27IgD_Bcells | 97.5% |
| CD4 Treg_CD4 | 95.0% |
| Tconv naive_total | 92.5% |
| Treg memory_CD4 | 92.5% |
| Tconv naive_CD3 | 90.0% |
| Tconv memDR_Tconv | 82.5% |
| Tconv memDR_mem | 80.0% |
| CD16mono_CD3neg | 77.5% |
| CD8 RO DR_CD8 | 77.5% |
| Tconv naive_Tconv | 72.5% |
| Tconv memDR_CD3 | 70.0% |
| Treg memory_CD3 | 67.5% |
| DR_CD8RO | 67.5% |
| Tconv memCD27_Tconv | 67.5% |
| Bcells_CD3neg | 62.5% |
| Tconv memPD1_total | 62.5% |
| CD4 Tconv_total | 60.0% |
| Tconv memCXCR3_Tconv | 52.5% |
| Bcells memory_CD3neg | 50.0% |
| nonTnonB_total | 50.0% |
| CD3neg_total | 50.0% |
| CD4 Treg _CD3 | 50.0% |
| nonTnonB_CD3neg | 50.0% |
| CD8pos_CD3 | 50.0% |
| CD8 RO PD1_CD3 | 47.5% |
| CD8 RO CD56_CD3 | 45.0% |
| CD8  RO Ki67_CD3 | 45.0% |
| Ki67_Bcells | 42.5% |
| CD14mono_myeloid | 42.5% |
| CD16+mono_total | 40.0% |
| CD3pos_total | 40.0% |
| CD8 RO CXCR3_CD3 | 37.5% |
| CD3hi_total | 37.5% |
| CCR5_CD8RO | 35.0% |
| naive_Bcells | 35.0% |
| CD8 RA CCR7 naive_CD8 | 35.0% |
| CD8 RO DR_total | 35.0% |
| Bcells_total | 35.0% |
| Tconv memCXCR3_CD3 | 32.5% |
| CD4 Tconv_CD3 | 32.5% |
| Tconv memCXCR3_mem | 30.0% |
| CD14mono_total | 30.0% |
| Tconv memCCR6_Tconv | 27.5% |
| CD8 RO CCR5_CD3 | 27.5% |
| CD8 RA naive_CD3 | 27.5% |
| Tconv memTIGIT_total | 27.5% |
| Tconv memCD27_CD3 | 27.5% |
| CD8 RO TIGIT_CD3 | 25.0% |
| Bcells memory_total | 25.0% |
| CD8pos_total | 25.0% |
| NKCD56hi_nonTnonB | 25.0% |
| CD8 RO_CD3 | 22.5% |
| CD3hi_CD3 | 22.5% |
| NKCD16_total | 22.5% |
| CD14mono_CD3neg | 22.5% |
| Tconv memKi67_total | 22.5% |
| CD8 RO CXCR3_CD8 | 22.5% |
| NKCD16_NK | 22.5% |
| CD8 RO CCR5_total | 22.5% |
| Tconv memCCR4_total | 22.5% |
| Tconv mem_CD3 | 22.5% |
| Tconv memCD27_mem | 22.5% |
| CD4neg_CD3 | 20.0% |
| NKCD56hi_total | 20.0% |
| Bcells naive_CD3neg | 20.0% |
| Tconv memTIGIT_mem | 20.0% |
| Tconv memCCR5_mem | 20.0% |
| CD56_CD8RO | 20.0% |
| CD27negIgDneg_Bcells | 17.5% |
| Tconv memCCR4_Tconv | 17.5% |
| Tconv memCD27_total | 17.5% |
| myeloid_total | 17.5% |
| Tconv memPD1_CD3 | 17.5% |
| intB7_CD8RO | 17.5% |
| NKCD56hi_NK | 17.5% |
| CD4 Tconv mem_total | 17.5% |
| CD8 RO CCR5_CD8 | 15.0% |
| Tconv memCCR4_CD3 | 15.0% |
| Tconv memPD1_mem | 15.0% |
| memory_Bcells | 15.0% |
| CD14+16+mono_total | 15.0% |
| CD4 Treg_total | 15.0% |
| CD8 RA_CD3 | 15.0% |
| Tconv memCCR6_mem | 15.0% |
| Treg naive_total | 15.0% |
| CD14+16+mono_myeloid | 15.0% |
| Tconv memCCR6_CD3 | 15.0% |
| Tconv memintB7_Tconv | 15.0% |
| CD8 RO CD56_CD8 | 15.0% |
| NK_total | 12.5% |
| Tconv memCCR6_total | 12.5% |
| Tconv memCCR5_Tconv | 12.5% |
| Tconv memPD1_Tconv | 12.5% |
| Tconv memCD56_Tconv | 12.5% |
| CD8 ncytotox RO CCR4_CD8ntox | 12.5% |
| Tconv memCXCR3_total | 12.5% |
| NK Ki67_total | 10.0% |
| Tconv memDR_total | 10.0% |
| Tconv memCD56_mem | 10.0% |
| Tconv memintB7_mem | 10.0% |
| Tconv memKi67_mem | 10.0% |
| NK Ki67_NK | 10.0% |
| Treg naive_CD4 | 10.0% |
| Treg naive_CD3 | 10.0% |
| PD1_CD8RO | 7.5% |
| NKCD16_CD3neg | 7.5% |
| CD8 RO CD56_total | 7.5% |
| Tconv memKi67_Tconv | 7.5% |
| Tconv memCD56_CD3 | 7.5% |
| CD8 RA naive_total | 7.5% |
| Tconv memCCR4_mem | 7.5% |
| Tconv memTIGIT_Tconv | 7.5% |
| Tconv memCCR5_total | 7.5% |
| Bcells Ki67_CD3neg | 7.5% |
| CD8 RO CXCR3_total | 7.5% |
| CD14+16+mono_CD3neg | 7.5% |
| CD8 RO PD1_CD8 | 7.5% |
| CXCR3_CD8RO | 7.5% |
| Bcells naive_total | 7.5% |
| CD3hi_CD4neg | 5.0% |
| TIGIT_CD8RO | 5.0% |
| NK Ki67_nonTnonB | 5.0% |
| CCR4_CD8RO | 5.0% |
| Treg memory_total | 5.0% |
| Tconv memCCR5_CD3 | 5.0% |
| CD8 RO TIGIT_CD8 | 5.0% |
| Tconv memintB7_total | 5.0% |
| CCR6_CD8RO | 5.0% |
| CD8 RO PD1_total | 5.0% |
| CD27_CD8RO | 5.0% |
| CD8 ncytotox RO CCR4_CD3 | 5.0% |
| CD8 RO intB7_CD3 | 5.0% |
| Bcells CD27negIgDneg_total | 5.0% |
| CD8 RO CD27_CD3 | 5.0% |
| NKCD56hi_CD3neg | 5.0% |
| Tconv memintB7_CD3 | 2.5% |
| CD8 RA_total | 2.5% |
| CD8 RA_CD8 | 2.5% |
| CD8 RO CD27_CD8 | 2.5% |
| CD8 RO intB7_total | 2.5% |
| CD8 RO_total | 2.5% |
| NK_nonTnonB | 2.5% |
| CD8 RO_CD8 | 2.5% |
| CD4neg_total | 2.5% |
| NK_CD3neg | 2.5% |
| Bcells Ki67_total | 2.5% |
| Tconv memCD56_total | 2.5% |
| NK Ki67_CD3neg | 2.5% |
| Tconv memTIGIT_CD3 | 2.5% |
| NKCD16_nonTnonB | 2.5% |
| CD8 RO CCR6_CD3 | 2.5% |

**Total features selected by RF_Importance_t50**: 155

#### RF_Importance_t60

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD27IgD_Bcells | 97.5% |
| Bcells CD27posIgDneg_total | 97.5% |
| CD8 RO DR_CD3 | 95.0% |
| CD4 Treg_CD4 | 92.5% |
| Tconv naive_total | 90.0% |
| CD16mono_myeloid | 90.0% |
| Treg memory_CD4 | 80.0% |
| Tconv naive_CD3 | 80.0% |
| Tconv mem_Tconv | 77.5% |
| CD16mono_CD3neg | 65.0% |
| Tconv memDR_mem | 60.0% |
| Tconv naive_Tconv | 57.5% |
| DR_CD8RO | 57.5% |
| Tconv memDR_Tconv | 57.5% |
| Tconv memDR_CD3 | 55.0% |
| CD8 RO DR_CD8 | 52.5% |
| Tconv memCD27_Tconv | 50.0% |
| Treg memory_CD3 | 47.5% |
| Bcells_CD3neg | 45.0% |
| CD4 Tconv_total | 45.0% |
| CD4 Treg _CD3 | 40.0% |
| CD8pos_CD3 | 37.5% |
| nonTnonB_total | 37.5% |
| Tconv memPD1_total | 37.5% |
| CD8 RO PD1_CD3 | 35.0% |
| Bcells memory_CD3neg | 35.0% |
| CD3pos_total | 30.0% |
| CD3neg_total | 30.0% |
| CD8 RO CD56_CD3 | 30.0% |
| CD14mono_myeloid | 30.0% |
| nonTnonB_CD3neg | 27.5% |
| Tconv memCXCR3_Tconv | 27.5% |
| CD8  RO Ki67_CD3 | 25.0% |
| Ki67_Bcells | 25.0% |
| CD8 RO DR_total | 25.0% |
| CD8 RA CCR7 naive_CD8 | 22.5% |
| CD3hi_total | 22.5% |
| Tconv memCXCR3_mem | 22.5% |
| CD8 RO CCR5_CD3 | 22.5% |
| CD8 RO TIGIT_CD3 | 20.0% |
| CD4 Tconv_CD3 | 20.0% |
| CD16+mono_total | 20.0% |
| Tconv memCD27_CD3 | 17.5% |
| Tconv memCCR6_Tconv | 17.5% |
| CD14mono_total | 17.5% |
| CCR5_CD8RO | 15.0% |
| Tconv mem_CD3 | 15.0% |
| CD14+16+mono_total | 15.0% |
| CD8 RO CCR5_total | 15.0% |
| naive_Bcells | 15.0% |
| Tconv memCXCR3_CD3 | 15.0% |
| CD8 RA naive_CD3 | 15.0% |
| CD8 RO CXCR3_CD3 | 15.0% |
| CD3hi_CD3 | 12.5% |
| CD56_CD8RO | 12.5% |
| Tconv memCCR5_mem | 12.5% |
| NKCD56hi_nonTnonB | 12.5% |
| Bcells_total | 12.5% |
| CD8 RO_CD3 | 12.5% |
| Tconv memCCR4_total | 12.5% |
| NKCD16_total | 10.0% |
| Bcells memory_total | 10.0% |
| Treg naive_total | 10.0% |
| CD14+16+mono_myeloid | 10.0% |
| Tconv memTIGIT_total | 10.0% |
| Tconv memKi67_total | 10.0% |
| NKCD56hi_total | 10.0% |
| Bcells naive_CD3neg | 10.0% |
| Tconv memPD1_CD3 | 10.0% |
| intB7_CD8RO | 7.5% |
| CD4 Treg_total | 7.5% |
| NKCD56hi_NK | 7.5% |
| CD8 RO CXCR3_CD8 | 7.5% |
| memory_Bcells | 7.5% |
| Tconv memPD1_mem | 7.5% |
| CD14mono_CD3neg | 7.5% |
| myeloid_total | 7.5% |
| Tconv memintB7_Tconv | 7.5% |
| Tconv memCCR6_total | 7.5% |
| CD8 RA_CD3 | 7.5% |
| NK_total | 7.5% |
| NKCD16_NK | 7.5% |
| CD8 RO CCR5_CD8 | 5.0% |
| CXCR3_CD8RO | 5.0% |
| Tconv memTIGIT_mem | 5.0% |
| Tconv memKi67_Tconv | 5.0% |
| CD4 Tconv mem_total | 5.0% |
| Tconv memCCR6_CD3 | 5.0% |
| CD8 ncytotox RO CCR4_CD8ntox | 5.0% |
| Tconv memCD27_total | 5.0% |
| Treg naive_CD3 | 5.0% |
| NKCD16_CD3neg | 5.0% |
| Tconv memCCR4_Tconv | 5.0% |
| CD8 RO CXCR3_total | 5.0% |
| CD4neg_CD3 | 5.0% |
| Tconv memCCR6_mem | 5.0% |
| CD27negIgDneg_Bcells | 2.5% |
| CD8 RA naive_total | 2.5% |
| TIGIT_CD8RO | 2.5% |
| Tconv memintB7_total | 2.5% |
| Tconv memintB7_mem | 2.5% |
| CD8 RA_CD8 | 2.5% |
| Tconv memCCR4_mem | 2.5% |
| Bcells CD27negIgDneg_total | 2.5% |
| CD14+16+mono_CD3neg | 2.5% |
| CD8 RO intB7_total | 2.5% |
| CD8 RO_CD8 | 2.5% |
| Tconv memCD27_mem | 2.5% |
| CCR4_CD8RO | 2.5% |
| NKCD56hi_CD3neg | 2.5% |
| NK Ki67_NK | 2.5% |
| CD4neg_total | 2.5% |
| CD3hi_CD4neg | 2.5% |
| CCR6_CD8RO | 2.5% |
| Tconv memCXCR3_total | 2.5% |
| Tconv memKi67_mem | 2.5% |
| Bcells Ki67_total | 2.5% |
| CD8 RO TIGIT_CD8 | 2.5% |
| Tconv memCCR5_total | 2.5% |
| Treg naive_CD4 | 2.5% |
| Tconv memCD56_total | 2.5% |
| Tconv memCD56_mem | 2.5% |
| Tconv memPD1_Tconv | 2.5% |
| CD8pos_total | 2.5% |
| Tconv memCCR5_CD3 | 2.5% |
| Tconv memCCR5_Tconv | 2.5% |
| CD8 ncytotox RO CCR4_CD3 | 2.5% |
| Tconv memCCR4_CD3 | 2.5% |
| Tconv memDR_total | 2.5% |
| CD8 RO CCR6_CD3 | 2.5% |

**Total features selected by RF_Importance_t60**: 130

#### RF_Importance_t70

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Bcells CD27posIgDneg_total | 95.0% |
| CD8 RO DR_CD3 | 85.0% |
| CD27IgD_Bcells | 85.0% |
| Tconv naive_total | 77.5% |
| CD16mono_myeloid | 75.0% |
| CD4 Treg_CD4 | 75.0% |
| Tconv mem_Tconv | 62.5% |
| Tconv naive_CD3 | 60.0% |
| Treg memory_CD4 | 55.0% |
| Tconv naive_Tconv | 50.0% |
| CD16mono_CD3neg | 45.0% |
| Tconv memDR_mem | 35.0% |
| Tconv memDR_Tconv | 35.0% |
| CD4 Tconv_total | 32.5% |
| DR_CD8RO | 32.5% |
| CD8 RO DR_CD8 | 30.0% |
| Bcells_CD3neg | 30.0% |
| Tconv memDR_CD3 | 27.5% |
| Tconv memCD27_Tconv | 27.5% |
| CD8pos_CD3 | 27.5% |
| Treg memory_CD3 | 25.0% |
| CD8 RO PD1_CD3 | 20.0% |
| Tconv memPD1_total | 20.0% |
| Bcells memory_CD3neg | 20.0% |
| CD8  RO Ki67_CD3 | 20.0% |
| CD3neg_total | 20.0% |
| Ki67_Bcells | 17.5% |
| CD14mono_myeloid | 17.5% |
| CD8 RO CCR5_CD3 | 17.5% |
| nonTnonB_total | 17.5% |
| CD4 Treg _CD3 | 15.0% |
| CD3pos_total | 15.0% |
| nonTnonB_CD3neg | 15.0% |
| Tconv memCXCR3_Tconv | 12.5% |
| CD3hi_total | 12.5% |
| CD8 RA CCR7 naive_CD8 | 12.5% |
| Tconv memCXCR3_mem | 12.5% |
| CD14+16+mono_total | 10.0% |
| CD16+mono_total | 10.0% |
| CD8 RO_CD3 | 10.0% |
| CD8 RO CD56_CD3 | 10.0% |
| CD4 Tconv_CD3 | 10.0% |
| naive_Bcells | 10.0% |
| CCR5_CD8RO | 10.0% |
| CD8 RO DR_total | 10.0% |
| CD14mono_total | 10.0% |
| CD8 RO TIGIT_CD3 | 10.0% |
| Tconv memPD1_mem | 7.5% |
| CD8 RA naive_CD3 | 7.5% |
| Tconv memCCR4_total | 7.5% |
| CD8 RA_CD3 | 7.5% |
| NKCD16_total | 7.5% |
| CD14+16+mono_myeloid | 7.5% |
| Tconv memPD1_CD3 | 7.5% |
| Tconv memCD27_CD3 | 7.5% |
| Tconv memCCR6_Tconv | 5.0% |
| Bcells naive_CD3neg | 5.0% |
| CD8 RO CXCR3_CD3 | 5.0% |
| NK_total | 5.0% |
| memory_Bcells | 5.0% |
| NKCD56hi_total | 5.0% |
| Bcells_total | 5.0% |
| Tconv mem_CD3 | 5.0% |
| CD14mono_CD3neg | 5.0% |
| Treg naive_CD3 | 5.0% |
| NKCD56hi_nonTnonB | 5.0% |
| Tconv memintB7_Tconv | 5.0% |
| Tconv memTIGIT_total | 5.0% |
| CD56_CD8RO | 2.5% |
| Tconv memintB7_total | 2.5% |
| Tconv memCCR6_CD3 | 2.5% |
| CD8 ncytotox RO CCR4_CD8ntox | 2.5% |
| CD4 Tconv mem_total | 2.5% |
| Tconv memKi67_total | 2.5% |
| CD8 RO CCR5_CD8 | 2.5% |
| CXCR3_CD8RO | 2.5% |
| Bcells CD27negIgDneg_total | 2.5% |
| Bcells memory_total | 2.5% |
| Tconv memCD27_mem | 2.5% |
| CD4neg_total | 2.5% |
| Tconv memKi67_mem | 2.5% |
| CD4neg_CD3 | 2.5% |
| CD3hi_CD3 | 2.5% |
| CD8 RO CXCR3_CD8 | 2.5% |
| Tconv memCCR5_total | 2.5% |
| Tconv memCCR6_total | 2.5% |
| Tconv memCD56_mem | 2.5% |
| CD4 Treg_total | 2.5% |
| CD8 RO CXCR3_total | 2.5% |
| Tconv memCCR5_Tconv | 2.5% |
| Tconv memCCR5_mem | 2.5% |
| Treg naive_total | 2.5% |

**Total features selected by RF_Importance_t70**: 92

#### RF_Importance_t80

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Bcells CD27posIgDneg_total | 90.0% |
| CD8 RO DR_CD3 | 80.0% |
| CD27IgD_Bcells | 67.5% |
| Tconv naive_total | 55.0% |
| CD4 Treg_CD4 | 52.5% |
| Tconv mem_Tconv | 47.5% |
| Tconv naive_CD3 | 45.0% |
| CD16mono_myeloid | 42.5% |
| Tconv naive_Tconv | 40.0% |
| Treg memory_CD4 | 37.5% |
| CD16mono_CD3neg | 30.0% |
| Tconv memDR_mem | 22.5% |
| CD4 Tconv_total | 17.5% |
| CD8 RO DR_CD8 | 15.0% |
| Tconv memCD27_Tconv | 15.0% |
| CD8 RO CCR5_CD3 | 15.0% |
| Treg memory_CD3 | 15.0% |
| Tconv memPD1_total | 15.0% |
| CD8 RO PD1_CD3 | 15.0% |
| CD8pos_CD3 | 12.5% |
| Tconv memDR_Tconv | 12.5% |
| DR_CD8RO | 12.5% |
| Tconv memDR_CD3 | 12.5% |
| Bcells memory_CD3neg | 10.0% |
| Bcells_CD3neg | 10.0% |
| CD3neg_total | 7.5% |
| CD14+16+mono_total | 7.5% |
| CD8  RO Ki67_CD3 | 7.5% |
| nonTnonB_total | 7.5% |
| naive_Bcells | 7.5% |
| CD4 Tconv_CD3 | 7.5% |
| CD3hi_total | 7.5% |
| nonTnonB_CD3neg | 7.5% |
| CD3pos_total | 7.5% |
| CD14mono_myeloid | 7.5% |
| CD8 RO DR_total | 7.5% |
| CD16+mono_total | 5.0% |
| CD14+16+mono_myeloid | 5.0% |
| CCR5_CD8RO | 5.0% |
| Tconv memCCR4_total | 5.0% |
| Tconv memCCR6_Tconv | 5.0% |
| CD4 Tconv mem_total | 2.5% |
| CD8 RO_CD3 | 2.5% |
| Ki67_Bcells | 2.5% |
| Bcells naive_CD3neg | 2.5% |
| CD8 RO CD56_CD3 | 2.5% |
| Tconv memintB7_total | 2.5% |
| Tconv memCXCR3_mem | 2.5% |
| Tconv memCCR6_CD3 | 2.5% |
| Tconv memintB7_Tconv | 2.5% |
| Bcells_total | 2.5% |
| CD8 RO TIGIT_CD3 | 2.5% |
| Tconv mem_CD3 | 2.5% |
| CD8 RA naive_CD3 | 2.5% |
| CD4 Treg _CD3 | 2.5% |
| CD14mono_total | 2.5% |
| Bcells memory_total | 2.5% |
| CD14mono_CD3neg | 2.5% |
| NKCD16_total | 2.5% |
| Tconv memCD27_mem | 2.5% |
| Tconv memPD1_CD3 | 2.5% |
| NKCD56hi_nonTnonB | 2.5% |
| Tconv memKi67_mem | 2.5% |
| Tconv memCXCR3_Tconv | 2.5% |
| CD3hi_CD3 | 2.5% |
| Tconv memCCR5_mem | 2.5% |

**Total features selected by RF_Importance_t80**: 66

#### RandomForest_Permutation_AboveMean_t40

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Tconv memCCR6_Tconv | 16.7% |
| CD8 RO CD27_CD8 | 11.1% |
| NKCD16_CD3neg | 11.1% |
| NK_nonTnonB | 11.1% |
| Tconv memCXCR3_Tconv | 5.6% |
| CD8 RO PD1_CD8 | 5.6% |
| CD8 RO CCR6_CD8 | 5.6% |
| CD8 RO CD56_CD8 | 5.6% |
| CD8 RO CCR4_total | 5.6% |
| Tconv memCCR5_mem | 5.6% |
| Treg memory_CD3 | 5.6% |
| CD8 RO TIGIT_total | 5.6% |
| Tconv memCCR6_CD3 | 5.6% |
| CCR4_CD8RO | 5.6% |
| Tconv memCD56_Tconv | 5.6% |
| CD3hi_total | 5.6% |
| Tconv memDR_total | 5.6% |
| Tconv memintB7_mem | 5.6% |
| CD8 RO intB7_CD3 | 5.6% |
| CD8 RA_CD3 | 5.6% |
| Tconv mem_CD3 | 5.6% |
| CCR5_CD8RO | 5.6% |
| CD14mono_myeloid | 5.6% |
| CD16+mono_total | 5.6% |
| CD14+16+mono_myeloid | 5.6% |
| CD8pos_total | 5.6% |
| Tconv memCCR5_CD3 | 5.6% |
| Tconv memKi67_CD3 | 5.6% |
| CD4neg_CD3 | 5.6% |
| CD8 RO CD56_CD3 | 5.6% |
| Tconv memDR_CD3 | 5.6% |
| CD8 RO PD1_CD3 | 5.6% |

**Total features selected by RandomForest_Permutation_AboveMean_t40**: 32

#### RandomForest_Permutation_AboveMean_t50

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Tconv memCD56_Tconv | 50.0% |
| NK_nonTnonB | 50.0% |
| CD14+16+mono_myeloid | 50.0% |
| NKCD16_CD3neg | 50.0% |

**Total features selected by RandomForest_Permutation_AboveMean_t50**: 4

#### RandomForest_Permutation_AboveMean_t60

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| NK_nonTnonB | 100.0% |
| CD14+16+mono_myeloid | 100.0% |
| NKCD16_CD3neg | 100.0% |

**Total features selected by RandomForest_Permutation_AboveMean_t60**: 3

#### RandomForest_Permutation_Top10%_t40

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Tconv memCCR6_total | 92.5% |
| Tconv memCD27_total | 92.5% |
| Tconv memCD56_total | 87.5% |
| Tconv memintB7_total | 87.5% |
| Tconv memKi67_total | 85.0% |
| Tconv memPD1_total | 85.0% |
| Tconv memDR_total | 80.0% |
| Tconv memCXCR3_total | 77.5% |
| Tconv naive_total | 72.5% |
| Tconv memTIGIT_total | 72.5% |
| Tconv memCCR5_total | 60.0% |
| CD4 Treg_total | 45.0% |
| CD3pos_total | 27.5% |
| CD4 Tconv mem_total | 20.0% |
| Tconv memCCR6_Tconv | 5.0% |
| Tconv memCCR4_total | 5.0% |
| CD4 Tconv_total | 5.0% |
| CD8 RO CD56_CD8 | 2.5% |
| Tconv memCCR5_mem | 2.5% |
| CD8 RO CCR4_total | 2.5% |
| CD8 RO TIGIT_total | 2.5% |
| CCR4_CD8RO | 2.5% |
| Tconv memCD56_Tconv | 2.5% |
| CD8 RA_CD3 | 2.5% |
| CD8 RO intB7_CD3 | 2.5% |
| CCR5_CD8RO | 2.5% |
| CD14mono_myeloid | 2.5% |
| CD16+mono_total | 2.5% |
| NK_nonTnonB | 2.5% |
| NKCD16_CD3neg | 2.5% |

**Total features selected by RandomForest_Permutation_Top10%_t40**: 30

#### RandomForest_Permutation_Top10%_t50

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Tconv memKi67_total | 80.0% |
| Tconv memCD27_total | 77.5% |
| Tconv memintB7_total | 77.5% |
| Tconv memCCR6_total | 75.0% |
| Tconv memCD56_total | 72.5% |
| Tconv memPD1_total | 67.5% |
| Tconv memDR_total | 67.5% |
| Tconv naive_total | 65.0% |
| Tconv memCXCR3_total | 57.5% |
| Tconv memTIGIT_total | 57.5% |
| Tconv memCCR5_total | 45.0% |
| CD4 Treg_total | 27.5% |
| CD4 Tconv mem_total | 15.0% |
| CD3pos_total | 7.5% |
| Tconv memCCR4_total | 2.5% |
| CD4 Tconv_total | 2.5% |

**Total features selected by RandomForest_Permutation_Top10%_t50**: 16

#### RandomForest_Permutation_Top10%_t60

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Tconv memintB7_total | 85.3% |
| Tconv memKi67_total | 82.4% |
| Tconv memCCR6_total | 70.6% |
| Tconv memCD56_total | 70.6% |
| Tconv memCD27_total | 70.6% |
| Tconv memPD1_total | 67.6% |
| Tconv memDR_total | 55.9% |
| Tconv naive_total | 50.0% |
| Tconv memCXCR3_total | 44.1% |
| Tconv memTIGIT_total | 26.5% |
| Tconv memCCR5_total | 20.6% |
| CD4 Treg_total | 17.6% |
| CD3pos_total | 8.8% |

**Total features selected by RandomForest_Permutation_Top10%_t60**: 13

#### RandomForest_Permutation_Top10%_t70

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Tconv memKi67_total | 79.3% |
| Tconv memintB7_total | 62.1% |
| Tconv memCCR6_total | 62.1% |
| Tconv memCD27_total | 55.2% |
| Tconv memCD56_total | 48.3% |
| Tconv memPD1_total | 48.3% |
| Tconv memDR_total | 44.8% |
| Tconv naive_total | 41.4% |
| Tconv memCXCR3_total | 31.0% |
| Tconv memTIGIT_total | 17.2% |
| CD4 Treg_total | 13.8% |

**Total features selected by RandomForest_Permutation_Top10%_t70**: 11

#### RandomForest_Permutation_Top10%_t80

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Tconv memKi67_total | 71.4% |
| Tconv memintB7_total | 57.1% |
| Tconv memCD27_total | 38.1% |
| Tconv memCCR6_total | 28.6% |
| Tconv memCD56_total | 23.8% |
| Tconv memPD1_total | 19.0% |
| Tconv memDR_total | 19.0% |
| Tconv memCXCR3_total | 19.0% |
| Tconv naive_total | 19.0% |
| CD4 Treg_total | 9.5% |
| Tconv memTIGIT_total | 4.8% |

**Total features selected by RandomForest_Permutation_Top10%_t80**: 11

#### Ridge_Strict_t40

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| DR_CD8RO | 100.0% |
| CD27IgD_Bcells | 100.0% |
| CD16mono_myeloid | 100.0% |
| Ki67_Bcells | 100.0% |
| CD8 RO DR_CD8 | 100.0% |
| Bcells CD27posIgDneg_total | 97.5% |
| CD3hi_total | 97.5% |
| CD3hi_CD3 | 95.0% |
| CD8 RO intB7_CD8 | 95.0% |
| Tconv memDR_total | 95.0% |
| memory_Bcells | 95.0% |
| CD14mono_myeloid | 95.0% |
| CD8 RA_total | 92.5% |
| CD8 RO intB7_total | 92.5% |
| CXCR3_CD8RO | 92.5% |
| Bcells Ki67_total | 92.5% |
| Tconv memKi67_mem | 92.5% |
| Tconv memCCR5_mem | 92.5% |
| CD8 RO CD56_CD8 | 90.0% |
| Tconv memPD1_mem | 90.0% |
| TIGIT_CD8RO | 87.5% |
| CD8 ncytotox RO CCR4_CD8ntox | 87.5% |
| Tconv memDR_mem | 87.5% |
| NKCD56hi_total | 87.5% |
| CD16mono_CD3neg | 87.5% |
| CD8 RA CCR7 naive_CD8 | 87.5% |
| CCR5_CD8RO | 85.0% |
| CD8 RO CCR6_CD8 | 85.0% |
| Bcells memory_total | 85.0% |
| CD8 RA naive_total | 85.0% |
| CD8 RA_CD3 | 85.0% |
| Tconv memCD27_mem | 85.0% |
| Bcells CD27negIgDneg_total | 85.0% |
| Tconv memKi67_CD3 | 82.5% |
| Tconv memCCR4_mem | 82.5% |
| CCR4_CD8RO | 82.5% |
| CD14+16+mono_myeloid | 82.5% |
| NKCD16_NK | 80.0% |
| CD4neg_total | 80.0% |
| CD8 RA naive_CD3 | 80.0% |
| Tconv memCCR6_mem | 80.0% |
| intB7_CD8RO | 77.5% |
| CD16+mono_total | 77.5% |
| CD27negIgDneg_Bcells | 77.5% |
| Tconv memCD56_total | 77.5% |
| CD8 RO CCR5_total | 77.5% |
| CD3hi_CD4neg | 77.5% |
| NK Ki67_NK | 75.0% |
| CD8 RO PD1_CD3 | 75.0% |
| CD8pos_CD3 | 75.0% |
| Tconv memintB7_CD3 | 72.5% |
| CD8 RO TIGIT_CD3 | 72.5% |
| NKCD56hi_NK | 72.5% |
| CCR6_CD8RO | 72.5% |
| Tconv mem_Tconv | 72.5% |
| Treg naive_total | 70.0% |
| Treg naive_CD4 | 70.0% |
| CD8 RO Ki67_CD8 | 67.5% |
| CD8 RO CCR4_total | 67.5% |
| Tconv memKi67_Tconv | 67.5% |
| CD8 RO PD1_total | 67.5% |
| Ki67_CD8RO | 67.5% |
| Tconv memTIGIT_mem | 67.5% |
| CD8 RO CXCR3_CD8 | 67.5% |
| Tconv memintB7_mem | 67.5% |
| Tconv memCXCR3_total | 67.5% |
| Tconv memCCR5_total | 65.0% |
| Tconv memDR_CD3 | 65.0% |
| Tconv memCCR6_Tconv | 65.0% |
| CD8 RO DR_CD3 | 65.0% |
| CD4neg_CD3 | 65.0% |
| CD27_CD8RO | 65.0% |
| PD1_CD8RO | 65.0% |
| Tconv memDR_Tconv | 65.0% |
| CD8 RO CD56_CD3 | 65.0% |
| CD56_CD8RO | 62.5% |
| Tconv memCXCR3_mem | 62.5% |
| NK Ki67_total | 62.5% |
| Treg memory_total | 62.5% |
| Tconv naive_Tconv | 62.5% |
| CD8 RO DR_total | 62.5% |
| Tconv memintB7_Tconv | 60.0% |
| Bcells Ki67_CD3neg | 60.0% |
| Tconv memKi67_total | 60.0% |
| NKCD56hi_CD3neg | 60.0% |
| Bcells memory_CD3neg | 57.5% |
| Tconv memCCR5_Tconv | 57.5% |
| Tconv memTIGIT_Tconv | 55.0% |
| NKCD56hi_nonTnonB | 55.0% |
| Tconv memCCR6_CD3 | 55.0% |
| CD14+16+mono_CD3neg | 55.0% |
| Tconv memCCR5_CD3 | 52.5% |
| Bcells naive_total | 52.5% |
| naive_Bcells | 50.0% |
| CD8 RO TIGIT_CD8 | 50.0% |
| CD4 Treg_total | 50.0% |
| CD8 RO CD56_total | 50.0% |
| NK Ki67_nonTnonB | 50.0% |
| Bcells naive_CD3neg | 47.5% |
| Tconv memintB7_total | 47.5% |
| CD8 RO CCR5_CD3 | 47.5% |
| Tconv memCCR6_total | 47.5% |
| Tconv memPD1_CD3 | 47.5% |
| Tconv mem_CD3 | 47.5% |
| CD8 RO CD27_CD3 | 45.0% |
| CD8 RO CCR6_CD3 | 45.0% |
| CD8 RO CXCR3_CD3 | 45.0% |
| CD8 RO intB7_CD3 | 45.0% |
| Treg naive_CD3 | 45.0% |
| NK Ki67_CD3neg | 45.0% |
| CD8 RO PD1_CD8 | 45.0% |
| Tconv memPD1_total | 42.5% |
| CD8 RO Ki67_total | 42.5% |
| CD8 RO_CD3 | 40.0% |
| CD8 RO CD27_CD8 | 40.0% |
| CD14+16+mono_total | 37.5% |
| CD8 RO CCR6_total | 35.0% |
| Tconv memPD1_Tconv | 35.0% |
| Tconv memCD56_CD3 | 35.0% |
| Tconv memCD27_Tconv | 35.0% |
| CD8 ncytotox RO CCR4_CD3 | 35.0% |
| Tconv memTIGIT_total | 35.0% |
| CD8 RO CCR5_CD8 | 35.0% |
| CD8 RO CXCR3_total | 32.5% |
| Tconv memCCR4_CD3 | 32.5% |
| Tconv memCD56_mem | 32.5% |
| Bcells_total | 30.0% |
| Tconv memCXCR3_CD3 | 30.0% |
| Tconv memCXCR3_Tconv | 30.0% |
| CD8 RA_CD8 | 27.5% |
| Tconv naive_CD3 | 27.5% |
| Tconv memCD27_total | 25.0% |
| CD8 RO TIGIT_total | 22.5% |
| CD14mono_CD3neg | 22.5% |
| Tconv memCCR4_Tconv | 22.5% |
| NK_total | 22.5% |
| Treg memory_CD4 | 22.5% |
| Tconv memCCR4_total | 20.0% |
| Tconv memTIGIT_CD3 | 20.0% |
| NKCD16_total | 20.0% |
| Tconv memCD56_Tconv | 20.0% |
| Treg memory_CD3 | 17.5% |
| CD8pos_total | 15.0% |
| CD8  RO Ki67_CD3 | 15.0% |
| Tconv naive_total | 15.0% |
| CD4 Treg_CD4 | 12.5% |
| NKCD16_nonTnonB | 10.0% |
| Tconv memCD27_CD3 | 10.0% |
| CD8 RO_CD8 | 7.5% |
| nonTnonB_CD3neg | 7.5% |
| CD4 Treg _CD3 | 7.5% |
| CD4 Tconv mem_total | 7.5% |
| NKCD16_CD3neg | 7.5% |
| Bcells_CD3neg | 5.0% |
| NK_CD3neg | 5.0% |
| CD4 Tconv_CD3 | 5.0% |
| NK_nonTnonB | 5.0% |
| CD8 RO CD27_total | 2.5% |
| CD14mono_total | 2.5% |
| CD4 Tconv_total | 2.5% |

**Total features selected by Ridge_Strict_t40**: 160

#### Ridge_Strict_t50

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| DR_CD8RO | 100.0% |
| CD8 RO DR_CD8 | 100.0% |
| CD3hi_total | 97.5% |
| CD27IgD_Bcells | 97.5% |
| CD16mono_myeloid | 97.5% |
| Ki67_Bcells | 95.0% |
| CD3hi_CD3 | 92.5% |
| CD8 RO intB7_CD8 | 90.0% |
| memory_Bcells | 87.5% |
| Tconv memKi67_mem | 85.0% |
| Tconv memDR_total | 85.0% |
| NKCD56hi_total | 85.0% |
| CD8 RA_total | 85.0% |
| CD8 RO intB7_total | 85.0% |
| CD8 RA CCR7 naive_CD8 | 80.0% |
| CD14mono_myeloid | 80.0% |
| CD8 RO CD56_CD8 | 80.0% |
| CXCR3_CD8RO | 80.0% |
| Bcells CD27posIgDneg_total | 80.0% |
| Tconv memPD1_mem | 80.0% |
| Bcells Ki67_total | 77.5% |
| CD8 RA_CD3 | 75.0% |
| TIGIT_CD8RO | 75.0% |
| CD8 RO CCR6_CD8 | 75.0% |
| Tconv memCCR5_mem | 75.0% |
| CD16mono_CD3neg | 72.5% |
| Tconv memKi67_CD3 | 72.5% |
| CD8 ncytotox RO CCR4_CD8ntox | 72.5% |
| CCR4_CD8RO | 70.0% |
| intB7_CD8RO | 67.5% |
| Tconv memCCR4_mem | 67.5% |
| CD8pos_CD3 | 67.5% |
| Bcells memory_total | 67.5% |
| NKCD56hi_NK | 67.5% |
| CD4neg_total | 65.0% |
| Tconv memKi67_Tconv | 62.5% |
| CD14+16+mono_myeloid | 62.5% |
| CD8 RO TIGIT_CD3 | 62.5% |
| Tconv memintB7_CD3 | 62.5% |
| CD8 RO CXCR3_CD8 | 60.0% |
| CD8 RO CCR5_total | 60.0% |
| CD3hi_CD4neg | 60.0% |
| Tconv memDR_mem | 60.0% |
| Bcells CD27negIgDneg_total | 60.0% |
| CD8 RA naive_total | 60.0% |
| NKCD16_NK | 57.5% |
| Tconv memCD27_mem | 57.5% |
| CD27negIgDneg_Bcells | 57.5% |
| CD8 RO PD1_CD3 | 55.0% |
| Tconv memCCR6_mem | 55.0% |
| CCR5_CD8RO | 55.0% |
| Tconv memDR_CD3 | 55.0% |
| Tconv mem_Tconv | 52.5% |
| NK Ki67_NK | 52.5% |
| Tconv memCD56_total | 52.5% |
| Tconv memKi67_total | 52.5% |
| Treg naive_total | 52.5% |
| CD8 RA naive_CD3 | 52.5% |
| CD8 RO CD56_CD3 | 50.0% |
| Treg naive_CD4 | 50.0% |
| CD16+mono_total | 50.0% |
| Tconv memintB7_mem | 50.0% |
| Tconv memCCR5_total | 50.0% |
| CD8 RO DR_total | 50.0% |
| Tconv memCCR6_Tconv | 50.0% |
| CD8 RO DR_CD3 | 50.0% |
| CD4neg_CD3 | 47.5% |
| CD8 RO PD1_total | 47.5% |
| CD8 RO CCR4_total | 47.5% |
| NK Ki67_total | 47.5% |
| PD1_CD8RO | 47.5% |
| CCR6_CD8RO | 45.0% |
| Ki67_CD8RO | 45.0% |
| Bcells Ki67_CD3neg | 45.0% |
| CD56_CD8RO | 45.0% |
| Tconv memintB7_Tconv | 42.5% |
| Treg memory_total | 42.5% |
| Tconv memCXCR3_total | 42.5% |
| Tconv memDR_Tconv | 42.5% |
| Tconv memCXCR3_mem | 40.0% |
| CD27_CD8RO | 40.0% |
| CD8 RO Ki67_CD8 | 40.0% |
| Tconv naive_Tconv | 40.0% |
| CD8 RO CD27_CD3 | 40.0% |
| Tconv mem_CD3 | 40.0% |
| NKCD56hi_CD3neg | 37.5% |
| naive_Bcells | 37.5% |
| Bcells naive_CD3neg | 37.5% |
| Bcells naive_total | 37.5% |
| Tconv memTIGIT_mem | 35.0% |
| CD14+16+mono_CD3neg | 35.0% |
| CD8 RO TIGIT_CD8 | 35.0% |
| NKCD56hi_nonTnonB | 32.5% |
| Bcells memory_CD3neg | 32.5% |
| NK Ki67_nonTnonB | 32.5% |
| CD8 RO intB7_CD3 | 32.5% |
| CD8 RO CD56_total | 32.5% |
| CD4 Treg_total | 32.5% |
| Tconv memCCR5_Tconv | 32.5% |
| Tconv memCCR6_CD3 | 30.0% |
| CD8 RO CXCR3_CD3 | 30.0% |
| Treg naive_CD3 | 30.0% |
| CD8 RO PD1_CD8 | 30.0% |
| Tconv memCCR5_CD3 | 30.0% |
| Tconv memPD1_CD3 | 30.0% |
| CD8 RO CD27_CD8 | 30.0% |
| Tconv memCCR6_total | 27.5% |
| NK Ki67_CD3neg | 27.5% |
| CD8 RO CCR5_CD3 | 27.5% |
| Tconv memPD1_total | 27.5% |
| Tconv memTIGIT_Tconv | 25.0% |
| Tconv memintB7_total | 25.0% |
| Tconv memTIGIT_total | 22.5% |
| CD8 RO CXCR3_total | 20.0% |
| Tconv memCXCR3_CD3 | 20.0% |
| CD14+16+mono_total | 20.0% |
| Tconv memPD1_Tconv | 20.0% |
| CD8 RO Ki67_total | 20.0% |
| CD8 RO_CD3 | 20.0% |
| Tconv memCXCR3_Tconv | 20.0% |
| Tconv memCCR4_CD3 | 20.0% |
| CD8 RO CCR6_CD3 | 17.5% |
| Tconv memCD27_Tconv | 17.5% |
| CD8 ncytotox RO CCR4_CD3 | 17.5% |
| CD8 RO CCR5_CD8 | 17.5% |
| Tconv memCD56_CD3 | 15.0% |
| Tconv memCD56_mem | 15.0% |
| CD8 RO TIGIT_total | 12.5% |
| Tconv memCCR4_Tconv | 12.5% |
| CD8 RA_CD8 | 12.5% |
| Treg memory_CD4 | 12.5% |
| NK_total | 12.5% |
| Tconv memCD27_total | 10.0% |
| Tconv naive_CD3 | 10.0% |
| Bcells_total | 10.0% |
| Tconv naive_total | 10.0% |
| NKCD16_total | 10.0% |
| CD14mono_CD3neg | 10.0% |
| Tconv memCD56_Tconv | 7.5% |
| Tconv memTIGIT_CD3 | 7.5% |
| CD8  RO Ki67_CD3 | 7.5% |
| CD8 RO CCR6_total | 7.5% |
| Tconv memCD27_CD3 | 7.5% |
| CD8 RO_CD8 | 5.0% |
| CD8pos_total | 5.0% |
| CD4 Treg_CD4 | 5.0% |
| NKCD16_nonTnonB | 5.0% |
| NKCD16_CD3neg | 5.0% |
| Bcells_CD3neg | 2.5% |
| nonTnonB_CD3neg | 2.5% |
| NK_CD3neg | 2.5% |
| CD4 Tconv_CD3 | 2.5% |
| Treg memory_CD3 | 2.5% |
| CD4 Tconv mem_total | 2.5% |
| Tconv memCCR4_total | 2.5% |

**Total features selected by Ridge_Strict_t50**: 155

#### Ridge_Strict_t60

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| DR_CD8RO | 100.0% |
| CD8 RO DR_CD8 | 100.0% |
| CD27IgD_Bcells | 92.5% |
| CD16mono_myeloid | 92.5% |
| Ki67_Bcells | 87.5% |
| CD3hi_CD3 | 85.0% |
| Tconv memDR_total | 82.5% |
| CD3hi_total | 82.5% |
| CD8 RA CCR7 naive_CD8 | 75.0% |
| CD8 RO intB7_total | 75.0% |
| NKCD56hi_total | 75.0% |
| CD8 RO intB7_CD8 | 75.0% |
| Tconv memKi67_mem | 72.5% |
| CD14mono_myeloid | 72.5% |
| CD8 RO CD56_CD8 | 70.0% |
| Bcells CD27posIgDneg_total | 70.0% |
| Tconv memPD1_mem | 70.0% |
| CD8 RO CCR6_CD8 | 65.0% |
| CD8 RA_CD3 | 65.0% |
| CD8 RA_total | 65.0% |
| Tconv memCCR5_mem | 62.5% |
| Tconv memKi67_CD3 | 62.5% |
| Bcells Ki67_total | 60.0% |
| CD16mono_CD3neg | 57.5% |
| CCR4_CD8RO | 57.5% |
| TIGIT_CD8RO | 55.0% |
| CD8pos_CD3 | 55.0% |
| memory_Bcells | 55.0% |
| CXCR3_CD8RO | 55.0% |
| CD8 ncytotox RO CCR4_CD8ntox | 55.0% |
| Tconv memKi67_Tconv | 52.5% |
| Bcells CD27negIgDneg_total | 52.5% |
| CD8 RO TIGIT_CD3 | 52.5% |
| intB7_CD8RO | 50.0% |
| Tconv memCCR4_mem | 50.0% |
| CD8 RO CCR5_total | 50.0% |
| Bcells memory_total | 47.5% |
| CD3hi_CD4neg | 45.0% |
| NKCD56hi_NK | 45.0% |
| Tconv mem_Tconv | 45.0% |
| CD8 RO CXCR3_CD8 | 42.5% |
| Tconv memDR_CD3 | 42.5% |
| CD8 RA naive_total | 40.0% |
| CD56_CD8RO | 40.0% |
| Tconv memintB7_CD3 | 40.0% |
| Tconv memCCR5_total | 40.0% |
| Tconv memKi67_total | 40.0% |
| CD8 RA naive_CD3 | 37.5% |
| Tconv memCD27_mem | 37.5% |
| CD14+16+mono_myeloid | 37.5% |
| CD27negIgDneg_Bcells | 37.5% |
| Tconv memDR_mem | 37.5% |
| NK Ki67_total | 35.0% |
| CD8 RO PD1_CD3 | 35.0% |
| CD8 RO DR_CD3 | 35.0% |
| Tconv memDR_Tconv | 35.0% |
| Tconv memCD56_total | 35.0% |
| Tconv naive_Tconv | 35.0% |
| Tconv mem_CD3 | 32.5% |
| Treg naive_CD4 | 32.5% |
| Treg memory_total | 32.5% |
| CD8 RO DR_total | 32.5% |
| CD4neg_CD3 | 32.5% |
| CD8 RO CD56_CD3 | 30.0% |
| CD8 RO CCR4_total | 30.0% |
| NKCD16_NK | 30.0% |
| CCR5_CD8RO | 30.0% |
| NK Ki67_nonTnonB | 27.5% |
| Tconv memCCR5_Tconv | 27.5% |
| CD4neg_total | 27.5% |
| Tconv memCCR6_mem | 27.5% |
| Tconv memCCR6_Tconv | 27.5% |
| CD14+16+mono_CD3neg | 27.5% |
| Tconv memCXCR3_total | 27.5% |
| NKCD56hi_CD3neg | 27.5% |
| Tconv memPD1_CD3 | 25.0% |
| Bcells Ki67_CD3neg | 25.0% |
| Tconv memintB7_Tconv | 25.0% |
| Tconv memCXCR3_mem | 25.0% |
| CCR6_CD8RO | 25.0% |
| CD16+mono_total | 25.0% |
| CD8 RO PD1_total | 22.5% |
| Treg naive_total | 22.5% |
| NKCD56hi_nonTnonB | 22.5% |
| CD8 RO intB7_CD3 | 22.5% |
| CD8 RO Ki67_CD8 | 22.5% |
| CD8 RO CD56_total | 20.0% |
| Ki67_CD8RO | 20.0% |
| Tconv memCCR6_total | 20.0% |
| PD1_CD8RO | 20.0% |
| CD8 RO CCR5_CD3 | 20.0% |
| Bcells naive_CD3neg | 20.0% |
| Tconv memintB7_mem | 20.0% |
| NK Ki67_CD3neg | 20.0% |
| NK Ki67_NK | 20.0% |
| CD4 Treg_total | 17.5% |
| CD8 RO CXCR3_CD3 | 17.5% |
| Bcells memory_CD3neg | 17.5% |
| Tconv memCCR5_CD3 | 15.0% |
| CD8 RO PD1_CD8 | 15.0% |
| Tconv memPD1_total | 15.0% |
| Treg naive_CD3 | 15.0% |
| naive_Bcells | 15.0% |
| CD8 RO_CD3 | 15.0% |
| CD8 RO CD27_CD3 | 15.0% |
| CD27_CD8RO | 15.0% |
| CD8 ncytotox RO CCR4_CD3 | 12.5% |
| Tconv memCXCR3_Tconv | 12.5% |
| Tconv memPD1_Tconv | 12.5% |
| Tconv memCXCR3_CD3 | 12.5% |
| CD8 RO CXCR3_total | 12.5% |
| CD8 RO Ki67_total | 12.5% |
| Tconv memCCR6_CD3 | 12.5% |
| CD8 RO TIGIT_CD8 | 10.0% |
| CD8 RO CD27_CD8 | 10.0% |
| CD8 RO TIGIT_total | 10.0% |
| Tconv memTIGIT_mem | 10.0% |
| CD14+16+mono_total | 10.0% |
| Tconv memTIGIT_Tconv | 10.0% |
| Bcells naive_total | 7.5% |
| CD8 RO CCR6_CD3 | 7.5% |
| Tconv memCD27_Tconv | 7.5% |
| Tconv memCCR4_Tconv | 7.5% |
| Tconv naive_total | 7.5% |
| CD8 RO_CD8 | 5.0% |
| CD8 RA_CD8 | 5.0% |
| Tconv memCD56_mem | 5.0% |
| Bcells_total | 5.0% |
| NK_total | 5.0% |
| Tconv memCCR4_CD3 | 5.0% |
| CD8 RO CCR6_total | 5.0% |
| Tconv memCD27_CD3 | 5.0% |
| CD8 RO CCR5_CD8 | 5.0% |
| Tconv memCD56_CD3 | 5.0% |
| Tconv memTIGIT_CD3 | 5.0% |
| NKCD16_CD3neg | 5.0% |
| CD14mono_CD3neg | 2.5% |
| NKCD16_nonTnonB | 2.5% |
| Tconv naive_CD3 | 2.5% |
| nonTnonB_CD3neg | 2.5% |
| Bcells_CD3neg | 2.5% |
| Treg memory_CD4 | 2.5% |
| Tconv memCD27_total | 2.5% |
| NK_CD3neg | 2.5% |
| CD8  RO Ki67_CD3 | 2.5% |
| Tconv memintB7_total | 2.5% |
| Tconv memTIGIT_total | 2.5% |
| NKCD16_total | 2.5% |
| CD4 Tconv mem_total | 2.5% |
| Tconv memCCR4_total | 2.5% |

**Total features selected by Ridge_Strict_t60**: 150

#### Ridge_Strict_t70

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| DR_CD8RO | 100.0% |
| CD8 RO DR_CD8 | 97.5% |
| CD16mono_myeloid | 90.0% |
| CD27IgD_Bcells | 87.5% |
| CD3hi_total | 70.0% |
| CD3hi_CD3 | 70.0% |
| Tconv memDR_total | 67.5% |
| Bcells CD27posIgDneg_total | 65.0% |
| CD8 RO intB7_CD8 | 65.0% |
| CD8 RO intB7_total | 65.0% |
| Ki67_Bcells | 65.0% |
| NKCD56hi_total | 60.0% |
| CD8 RA CCR7 naive_CD8 | 55.0% |
| Tconv memKi67_mem | 52.5% |
| CD8 RO CD56_CD8 | 52.5% |
| CD14mono_myeloid | 50.0% |
| CD8 RA_CD3 | 50.0% |
| CD8pos_CD3 | 47.5% |
| Tconv memPD1_mem | 47.5% |
| Tconv memCCR5_mem | 45.0% |
| CD8 RA_total | 45.0% |
| CXCR3_CD8RO | 45.0% |
| CCR4_CD8RO | 45.0% |
| Tconv memKi67_CD3 | 42.5% |
| memory_Bcells | 42.5% |
| CD16mono_CD3neg | 40.0% |
| Bcells CD27negIgDneg_total | 40.0% |
| Bcells Ki67_total | 40.0% |
| CD8 RO CCR6_CD8 | 37.5% |
| Tconv mem_Tconv | 37.5% |
| intB7_CD8RO | 35.0% |
| CD8 ncytotox RO CCR4_CD8ntox | 35.0% |
| CD8 RO TIGIT_CD3 | 35.0% |
| Bcells memory_total | 32.5% |
| TIGIT_CD8RO | 32.5% |
| Tconv memCCR4_mem | 32.5% |
| Tconv memKi67_Tconv | 30.0% |
| CD3hi_CD4neg | 27.5% |
| CD8 RO CCR5_total | 27.5% |
| Tconv memintB7_CD3 | 27.5% |
| CD14+16+mono_myeloid | 27.5% |
| CD27negIgDneg_Bcells | 25.0% |
| NK Ki67_total | 25.0% |
| Tconv memKi67_total | 25.0% |
| CD56_CD8RO | 25.0% |
| NKCD16_NK | 22.5% |
| Tconv memCCR5_total | 22.5% |
| CD8 RO DR_CD3 | 22.5% |
| Tconv memDR_mem | 22.5% |
| CD8 RA naive_CD3 | 22.5% |
| CD8 RO PD1_total | 20.0% |
| Tconv memDR_Tconv | 20.0% |
| CD8 RO DR_total | 20.0% |
| NKCD56hi_NK | 20.0% |
| PD1_CD8RO | 17.5% |
| CD8 RA naive_total | 17.5% |
| CD8 RO CXCR3_CD8 | 17.5% |
| Tconv memPD1_CD3 | 17.5% |
| CCR5_CD8RO | 17.5% |
| Tconv naive_Tconv | 17.5% |
| Tconv memCD56_total | 17.5% |
| Tconv memDR_CD3 | 17.5% |
| Tconv memCCR6_Tconv | 17.5% |
| Tconv mem_CD3 | 17.5% |
| CD8 RO CCR5_CD3 | 17.5% |
| CD4neg_CD3 | 17.5% |
| Tconv memCCR6_total | 15.0% |
| CD8 RO intB7_CD3 | 15.0% |
| Tconv memintB7_Tconv | 15.0% |
| CCR6_CD8RO | 15.0% |
| Tconv memCCR6_mem | 15.0% |
| Treg naive_CD4 | 15.0% |
| Tconv memCD27_mem | 15.0% |
| CD8 RO PD1_CD3 | 15.0% |
| NK Ki67_nonTnonB | 12.5% |
| CD27_CD8RO | 12.5% |
| Tconv memCXCR3_mem | 12.5% |
| Tconv memintB7_mem | 12.5% |
| Bcells Ki67_CD3neg | 12.5% |
| NKCD56hi_CD3neg | 12.5% |
| CD8 RO Ki67_CD8 | 12.5% |
| Ki67_CD8RO | 12.5% |
| CD8 RO CD56_total | 12.5% |
| Tconv memCCR5_Tconv | 12.5% |
| CD8 RO CD56_CD3 | 12.5% |
| Tconv memCXCR3_total | 12.5% |
| Treg memory_total | 12.5% |
| Bcells memory_CD3neg | 10.0% |
| Tconv memCCR6_CD3 | 10.0% |
| CD8 RO CCR4_total | 10.0% |
| naive_Bcells | 10.0% |
| CD14+16+mono_CD3neg | 10.0% |
| CD4neg_total | 10.0% |
| CD16+mono_total | 10.0% |
| NK Ki67_CD3neg | 10.0% |
| CD8 RO TIGIT_CD8 | 7.5% |
| CD8 RO Ki67_total | 7.5% |
| NKCD56hi_nonTnonB | 7.5% |
| Treg naive_CD3 | 7.5% |
| CD8 RO_CD3 | 7.5% |
| NK Ki67_NK | 7.5% |
| Tconv memCXCR3_Tconv | 7.5% |
| Treg naive_total | 7.5% |
| CD8 RO CCR6_CD3 | 7.5% |
| CD4 Treg_total | 7.5% |
| CD8 RO_CD8 | 5.0% |
| CD8 ncytotox RO CCR4_CD3 | 5.0% |
| Tconv memTIGIT_mem | 5.0% |
| Bcells naive_CD3neg | 5.0% |
| Tconv naive_total | 5.0% |
| CD8 RO CD27_CD3 | 5.0% |
| CD8 RO CXCR3_CD3 | 5.0% |
| Tconv memCCR5_CD3 | 5.0% |
| CD8 RO CD27_CD8 | 5.0% |
| CD8 RO CCR5_CD8 | 5.0% |
| Tconv memTIGIT_Tconv | 5.0% |
| Tconv memPD1_total | 2.5% |
| Tconv naive_CD3 | 2.5% |
| Tconv memPD1_Tconv | 2.5% |
| CD14mono_CD3neg | 2.5% |
| Tconv memCD27_CD3 | 2.5% |
| Bcells_CD3neg | 2.5% |
| Tconv memCD27_Tconv | 2.5% |
| CD8 RO PD1_CD8 | 2.5% |
| nonTnonB_CD3neg | 2.5% |
| CD8 RO TIGIT_total | 2.5% |
| CD8 RA_CD8 | 2.5% |
| Tconv memCCR4_Tconv | 2.5% |
| Tconv memCD56_CD3 | 2.5% |
| Tconv memintB7_total | 2.5% |
| Bcells_total | 2.5% |
| Tconv memCXCR3_CD3 | 2.5% |
| Tconv memTIGIT_total | 2.5% |
| CD4 Tconv mem_total | 2.5% |
| Tconv memCCR4_total | 2.5% |
| Tconv memCCR4_CD3 | 2.5% |

**Total features selected by Ridge_Strict_t70**: 136

#### Ridge_Strict_t80

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| DR_CD8RO | 95.0% |
| CD8 RO DR_CD8 | 85.0% |
| CD16mono_myeloid | 77.5% |
| CD27IgD_Bcells | 62.5% |
| CD3hi_total | 62.5% |
| CD8 RO intB7_total | 55.0% |
| CD3hi_CD3 | 52.5% |
| Ki67_Bcells | 50.0% |
| Bcells CD27posIgDneg_total | 50.0% |
| Tconv memDR_total | 47.5% |
| NKCD56hi_total | 45.0% |
| CD8 RO intB7_CD8 | 45.0% |
| Tconv memKi67_mem | 45.0% |
| CD8 RO CD56_CD8 | 40.0% |
| Tconv memCCR5_mem | 37.5% |
| Tconv memKi67_CD3 | 37.5% |
| CD8 RA CCR7 naive_CD8 | 35.0% |
| Tconv memPD1_mem | 35.0% |
| CD8pos_CD3 | 32.5% |
| CXCR3_CD8RO | 32.5% |
| CD14mono_myeloid | 32.5% |
| CD8 RA_CD3 | 30.0% |
| memory_Bcells | 30.0% |
| CD8 RO CCR6_CD8 | 30.0% |
| CD8 RA_total | 27.5% |
| CD8 RO TIGIT_CD3 | 27.5% |
| CD8 ncytotox RO CCR4_CD8ntox | 25.0% |
| Bcells CD27negIgDneg_total | 25.0% |
| TIGIT_CD8RO | 25.0% |
| CD16mono_CD3neg | 25.0% |
| Tconv mem_Tconv | 22.5% |
| CCR4_CD8RO | 20.0% |
| CD8 RO CCR5_total | 20.0% |
| CD14+16+mono_myeloid | 20.0% |
| intB7_CD8RO | 20.0% |
| Bcells memory_total | 20.0% |
| CD8 RO DR_CD3 | 17.5% |
| Tconv mem_CD3 | 15.0% |
| CD8 RO DR_total | 15.0% |
| Tconv memKi67_Tconv | 15.0% |
| Tconv memDR_CD3 | 15.0% |
| Tconv memintB7_CD3 | 12.5% |
| Tconv memCCR4_mem | 12.5% |
| CD8 RO PD1_total | 12.5% |
| NKCD16_NK | 12.5% |
| Bcells Ki67_total | 12.5% |
| CD27negIgDneg_Bcells | 12.5% |
| NK Ki67_total | 12.5% |
| CCR6_CD8RO | 12.5% |
| Tconv memKi67_total | 12.5% |
| Tconv memCCR5_total | 12.5% |
| Tconv memintB7_Tconv | 10.0% |
| Tconv memDR_mem | 10.0% |
| Bcells Ki67_CD3neg | 10.0% |
| Tconv memCCR5_Tconv | 10.0% |
| CD8 RA naive_total | 10.0% |
| CD8 RA naive_CD3 | 10.0% |
| CD8 RO CD56_CD3 | 10.0% |
| CD3hi_CD4neg | 7.5% |
| Tconv memCCR6_mem | 7.5% |
| NKCD56hi_CD3neg | 7.5% |
| Tconv memCCR6_total | 7.5% |
| Tconv memCXCR3_total | 7.5% |
| Tconv memDR_Tconv | 7.5% |
| Tconv memintB7_mem | 7.5% |
| CD56_CD8RO | 7.5% |
| CD8 RO intB7_CD3 | 7.5% |
| CD8 RO CXCR3_CD8 | 7.5% |
| CD8 RO TIGIT_CD8 | 5.0% |
| CD16+mono_total | 5.0% |
| CCR5_CD8RO | 5.0% |
| CD8 RO CD56_total | 5.0% |
| CD8 RO_CD8 | 5.0% |
| NKCD56hi_NK | 5.0% |
| NK Ki67_nonTnonB | 5.0% |
| PD1_CD8RO | 5.0% |
| Tconv memCD27_mem | 5.0% |
| CD8 RO CCR5_CD3 | 5.0% |
| Treg naive_total | 5.0% |
| Tconv memCD56_total | 5.0% |
| CD8 RO CD27_CD3 | 5.0% |
| Tconv memCCR6_Tconv | 5.0% |
| NK Ki67_NK | 5.0% |
| CD4neg_total | 5.0% |
| CD8 RO Ki67_total | 5.0% |
| CD8 RO PD1_CD3 | 5.0% |
| Bcells memory_CD3neg | 5.0% |
| Tconv memCXCR3_mem | 5.0% |
| CD8 RO_CD3 | 5.0% |
| Tconv naive_Tconv | 5.0% |
| CD8 RO CD27_CD8 | 2.5% |
| CD14mono_CD3neg | 2.5% |
| Tconv memTIGIT_Tconv | 2.5% |
| Tconv memTIGIT_mem | 2.5% |
| CD8 RO CCR5_CD8 | 2.5% |
| Tconv memCD27_Tconv | 2.5% |
| CD27_CD8RO | 2.5% |
| CD8 RO CXCR3_CD3 | 2.5% |
| Tconv naive_CD3 | 2.5% |
| CD8 RO CCR4_total | 2.5% |
| CD8 RO TIGIT_total | 2.5% |
| CD8 RA_CD8 | 2.5% |
| NK Ki67_CD3neg | 2.5% |
| Bcells_CD3neg | 2.5% |
| CD14+16+mono_CD3neg | 2.5% |
| Tconv memPD1_CD3 | 2.5% |
| Treg memory_total | 2.5% |
| CD8 RO Ki67_CD8 | 2.5% |
| naive_Bcells | 2.5% |
| Tconv memTIGIT_total | 2.5% |
| Treg naive_CD3 | 2.5% |
| NKCD56hi_nonTnonB | 2.5% |
| CD4 Tconv mem_total | 2.5% |
| Bcells naive_CD3neg | 2.5% |
| Tconv memCCR4_CD3 | 2.5% |

**Total features selected by Ridge_Strict_t80**: 115

#### SVM_RBF_Permutation_AboveMean_t40

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CCR4_CD8RO | 76.3% |
| DR_CD8RO | 71.1% |
| Tconv memPD1_mem | 65.8% |
| Bcells CD27posIgDneg_total | 63.2% |
| CD8 RO DR_CD8 | 63.2% |
| CD3hi_CD4neg | 63.2% |
| memory_Bcells | 60.5% |
| naive_Bcells | 60.5% |
| CD16mono_CD3neg | 60.5% |
| CD27IgD_Bcells | 57.9% |
| CD16+mono_total | 57.9% |
| CD27negIgDneg_Bcells | 57.9% |
| CD16mono_myeloid | 57.9% |
| Treg memory_total | 55.3% |
| NKCD56hi_CD3neg | 55.3% |
| CD8 RA_total | 55.3% |
| CD3hi_total | 55.3% |
| Bcells Ki67_total | 55.3% |
| TIGIT_CD8RO | 55.3% |
| Tconv memintB7_total | 52.6% |
| NKCD56hi_total | 52.6% |
| CD8 ncytotox RO CCR4_CD8ntox | 52.6% |
| Tconv memKi67_CD3 | 52.6% |
| Tconv memTIGIT_mem | 50.0% |
| Tconv memDR_total | 50.0% |
| Bcells CD27negIgDneg_total | 50.0% |
| Tconv memKi67_mem | 50.0% |
| Tconv memCCR4_mem | 50.0% |
| CD8 RA_CD3 | 50.0% |
| CD8 RA naive_total | 50.0% |
| Tconv memCCR5_mem | 50.0% |
| CD8 RO DR_total | 47.4% |
| Tconv memCCR6_mem | 47.4% |
| CD4 Treg_total | 47.4% |
| Tconv memDR_mem | 47.4% |
| Bcells Ki67_CD3neg | 47.4% |
| CD27_CD8RO | 44.7% |
| Tconv memCD56_total | 44.7% |
| CD3hi_CD3 | 44.7% |
| Tconv memKi67_total | 44.7% |
| CD8 RO TIGIT_CD8 | 44.7% |
| Tconv memKi67_Tconv | 44.7% |
| Tconv memCXCR3_CD3 | 44.7% |
| NK Ki67_CD3neg | 42.1% |
| NK Ki67_nonTnonB | 42.1% |
| Tconv memCCR5_Tconv | 42.1% |
| CD8 RO Ki67_total | 42.1% |
| NK Ki67_total | 42.1% |
| Bcells memory_total | 42.1% |
| NKCD56hi_nonTnonB | 42.1% |
| Tconv memCD27_CD3 | 39.5% |
| NKCD56hi_NK | 39.5% |
| CD8 RO PD1_CD3 | 39.5% |
| CD8 RO intB7_CD8 | 39.5% |
| Bcells naive_total | 39.5% |
| Tconv memCCR4_total | 39.5% |
| Tconv memintB7_CD3 | 39.5% |
| Tconv memintB7_Tconv | 39.5% |
| Bcells_total | 39.5% |
| NKCD16_NK | 36.8% |
| CD56_CD8RO | 36.8% |
| CD8 RO DR_CD3 | 36.8% |
| Tconv memTIGIT_Tconv | 36.8% |
| CD8 RO PD1_CD8 | 36.8% |
| Ki67_Bcells | 36.8% |
| CCR6_CD8RO | 36.8% |
| Tconv memTIGIT_CD3 | 36.8% |
| CD8 RA naive_CD3 | 36.8% |
| Bcells naive_CD3neg | 36.8% |
| CD8 RO intB7_total | 36.8% |
| CD8 RO CD56_total | 36.8% |
| CD8 RO CXCR3_total | 36.8% |
| CD8 RO CXCR3_CD3 | 36.8% |
| Tconv memCXCR3_Tconv | 36.8% |
| Tconv memCD27_mem | 36.8% |
| Tconv memintB7_mem | 36.8% |
| Tconv memCCR6_CD3 | 36.8% |
| CXCR3_CD8RO | 36.8% |
| CCR5_CD8RO | 36.8% |
| intB7_CD8RO | 36.8% |
| CD14+16+mono_CD3neg | 36.8% |
| Tconv memCXCR3_mem | 34.2% |
| CD8 RO CD27_CD3 | 34.2% |
| Tconv memPD1_Tconv | 34.2% |
| CD4neg_total | 34.2% |
| Tconv memDR_CD3 | 34.2% |
| Tconv memCXCR3_total | 34.2% |
| Tconv memCCR5_CD3 | 34.2% |
| CD8 RO CCR5_CD3 | 34.2% |
| CD8 ncytotox RO CCR4_CD3 | 34.2% |
| CD8 RO CCR5_CD8 | 34.2% |
| NK Ki67_NK | 34.2% |
| Tconv mem_CD3 | 34.2% |
| CD8 RO intB7_CD3 | 34.2% |
| CD8pos_total | 34.2% |
| Treg naive_CD4 | 34.2% |
| Tconv memCCR4_CD3 | 31.6% |
| CD8 RO CXCR3_CD8 | 31.6% |
| Treg naive_CD3 | 31.6% |
| CD8 RO CD56_CD8 | 31.6% |
| Ki67_CD8RO | 31.6% |
| CD14+16+mono_myeloid | 31.6% |
| Tconv memPD1_CD3 | 31.6% |
| CD8 RO CCR4_total | 31.6% |
| CD8 RO CD27_total | 31.6% |
| Bcells memory_CD3neg | 31.6% |
| Tconv memDR_Tconv | 28.9% |
| CD8 RO CD56_CD3 | 28.9% |
| CD8 RO PD1_total | 28.9% |
| CD8 RO Ki67_CD8 | 28.9% |
| CD4 Tconv mem_total | 28.9% |
| CD8 RO TIGIT_total | 28.9% |
| CD14mono_myeloid | 28.9% |
| CD8 RO_total | 28.9% |
| Treg memory_CD3 | 28.9% |
| Tconv memCD56_CD3 | 26.3% |
| Tconv memCD56_mem | 26.3% |
| Treg naive_total | 26.3% |
| CD8 RO CD27_CD8 | 26.3% |
| CD8 RO_CD8 | 26.3% |
| CD14+16+mono_total | 26.3% |
| Tconv memCCR6_Tconv | 26.3% |
| Tconv memCCR6_total | 26.3% |
| NK_nonTnonB | 26.3% |
| Tconv memCCR5_total | 26.3% |
| Tconv memTIGIT_total | 26.3% |
| Tconv memCD27_total | 26.3% |
| CD8pos_CD3 | 26.3% |
| CD8 RO TIGIT_CD3 | 26.3% |
| CD8  RO Ki67_CD3 | 26.3% |
| CD8 RO_CD3 | 23.7% |
| NKCD16_nonTnonB | 23.7% |
| Tconv memCD56_Tconv | 23.7% |
| CD8 RO CCR6_total | 23.7% |
| Tconv memCD27_Tconv | 23.7% |
| NKCD16_CD3neg | 23.7% |
| CD8 RO CCR5_total | 23.7% |
| PD1_CD8RO | 23.7% |
| CD8 RO CCR6_CD3 | 23.7% |
| nonTnonB_CD3neg | 21.1% |
| NK_CD3neg | 21.1% |
| NK_total | 21.1% |
| Tconv memPD1_total | 21.1% |
| CD8 RO CCR6_CD8 | 21.1% |
| CD8 RA CCR7 naive_CD8 | 21.1% |
| Bcells_CD3neg | 21.1% |
| CD8 RA_CD8 | 21.1% |
| CD4neg_CD3 | 18.4% |
| myeloid_CD3neg | 18.4% |
| NKCD16_total | 18.4% |
| CD4 Treg _CD3 | 18.4% |
| CD4 Treg_CD4 | 18.4% |
| myeloid_total | 15.8% |
| CD3neg_total | 15.8% |
| CD14mono_total | 15.8% |
| CD3pos_total | 15.8% |
| Tconv naive_Tconv | 15.8% |
| Tconv mem_Tconv | 15.8% |
| CD4 Tconv_CD3 | 13.2% |
| Tconv naive_total | 10.5% |
| CD4 Tconv_total | 10.5% |
| Tconv memCCR4_Tconv | 10.5% |
| CD14mono_CD3neg | 10.5% |
| nonTnonB_total | 10.5% |
| Tconv naive_CD3 | 7.9% |
| Treg memory_CD4 | 7.9% |

**Total features selected by SVM_RBF_Permutation_AboveMean_t40**: 166

#### SVM_RBF_Permutation_AboveMean_t50

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD27IgD_Bcells | 51.4% |
| Bcells CD27posIgDneg_total | 51.4% |
| DR_CD8RO | 48.6% |
| memory_Bcells | 45.7% |
| CD16mono_myeloid | 45.7% |
| CCR4_CD8RO | 45.7% |
| CD8 RO DR_CD8 | 42.9% |
| TIGIT_CD8RO | 40.0% |
| Tconv memKi67_mem | 40.0% |
| CD8 RA_total | 37.1% |
| naive_Bcells | 37.1% |
| CD8 ncytotox RO CCR4_CD8ntox | 37.1% |
| Bcells Ki67_total | 34.3% |
| Bcells Ki67_CD3neg | 34.3% |
| CD16mono_CD3neg | 34.3% |
| CD3hi_CD4neg | 34.3% |
| CD3hi_total | 31.4% |
| Tconv memPD1_mem | 31.4% |
| CD16+mono_total | 31.4% |
| CD8 RA_CD3 | 31.4% |
| Tconv memCCR4_mem | 31.4% |
| Tconv memCCR6_mem | 28.6% |
| CD27negIgDneg_Bcells | 28.6% |
| CD8 RO TIGIT_CD8 | 28.6% |
| Tconv memKi67_CD3 | 28.6% |
| Tconv memDR_total | 28.6% |
| Tconv memCCR5_mem | 28.6% |
| Tconv memTIGIT_mem | 28.6% |
| NK Ki67_nonTnonB | 25.7% |
| CD4 Tconv mem_total | 25.7% |
| Bcells CD27negIgDneg_total | 25.7% |
| Tconv memCD56_total | 25.7% |
| Tconv memKi67_total | 25.7% |
| Tconv memCD27_CD3 | 25.7% |
| Tconv memCCR5_Tconv | 25.7% |
| CD3hi_CD3 | 25.7% |
| Ki67_Bcells | 25.7% |
| CD8 RO CXCR3_total | 25.7% |
| Tconv memCCR6_CD3 | 25.7% |
| Bcells memory_total | 25.7% |
| CD8 RO PD1_CD3 | 25.7% |
| Treg memory_total | 25.7% |
| CD8 RO DR_CD3 | 25.7% |
| CD8 RO CD27_total | 25.7% |
| Tconv memDR_CD3 | 25.7% |
| NKCD56hi_nonTnonB | 22.9% |
| Tconv memCCR6_Tconv | 22.9% |
| Tconv memCCR4_total | 22.9% |
| Tconv memDR_mem | 22.9% |
| Tconv memCXCR3_mem | 22.9% |
| Tconv memintB7_CD3 | 22.9% |
| Bcells naive_total | 22.9% |
| Tconv memCXCR3_total | 22.9% |
| CD8 RO PD1_total | 22.9% |
| Tconv memCCR5_total | 22.9% |
| Treg naive_CD4 | 22.9% |
| NKCD56hi_CD3neg | 22.9% |
| NK Ki67_CD3neg | 22.9% |
| CD8 RO CD56_CD8 | 22.9% |
| Tconv mem_CD3 | 22.9% |
| CD8 RO intB7_CD8 | 20.0% |
| CD14+16+mono_myeloid | 20.0% |
| CD8 RO CCR5_CD8 | 20.0% |
| NKCD16_NK | 20.0% |
| Bcells_total | 20.0% |
| CD8 RO TIGIT_total | 20.0% |
| CD4 Treg_total | 20.0% |
| CD8pos_total | 20.0% |
| CD8 RO TIGIT_CD3 | 20.0% |
| NK Ki67_NK | 20.0% |
| intB7_CD8RO | 20.0% |
| Bcells naive_CD3neg | 20.0% |
| CD14+16+mono_CD3neg | 20.0% |
| Tconv memCXCR3_Tconv | 20.0% |
| CD8 RA naive_total | 20.0% |
| NK Ki67_total | 20.0% |
| Treg naive_CD3 | 17.1% |
| NKCD56hi_total | 17.1% |
| CD4neg_total | 17.1% |
| Tconv memCCR6_total | 17.1% |
| Tconv memCCR5_CD3 | 17.1% |
| CXCR3_CD8RO | 17.1% |
| CD8 RO PD1_CD8 | 17.1% |
| CD8 RO CD56_CD3 | 17.1% |
| CD8 RO_total | 17.1% |
| CD14mono_myeloid | 17.1% |
| CD8 RO intB7_total | 17.1% |
| CD8 RO intB7_CD3 | 17.1% |
| CD56_CD8RO | 17.1% |
| CCR6_CD8RO | 17.1% |
| NKCD56hi_NK | 17.1% |
| Tconv memintB7_mem | 17.1% |
| CCR5_CD8RO | 17.1% |
| CD8 RO CCR6_total | 17.1% |
| Tconv memPD1_Tconv | 14.3% |
| Tconv memCD56_CD3 | 14.3% |
| CD8 RO DR_total | 14.3% |
| Tconv memKi67_Tconv | 14.3% |
| CD8 RO Ki67_total | 14.3% |
| CD8 RO CXCR3_CD3 | 14.3% |
| CD8 RO CD27_CD8 | 14.3% |
| Tconv memPD1_CD3 | 14.3% |
| CD27_CD8RO | 14.3% |
| CD8 RA_CD8 | 14.3% |
| CD8 RO CCR5_total | 14.3% |
| Tconv memTIGIT_Tconv | 14.3% |
| CD8 RO CCR5_CD3 | 14.3% |
| Tconv memCCR4_CD3 | 14.3% |
| Tconv memCD27_mem | 14.3% |
| Ki67_CD8RO | 14.3% |
| Tconv memintB7_Tconv | 14.3% |
| CD8 RO CD56_total | 14.3% |
| Bcells_CD3neg | 14.3% |
| CD14+16+mono_total | 14.3% |
| CD8 RA naive_CD3 | 14.3% |
| Tconv memPD1_total | 14.3% |
| nonTnonB_CD3neg | 14.3% |
| Tconv memCD56_Tconv | 11.4% |
| NK_total | 11.4% |
| CD8 RO CCR6_CD8 | 11.4% |
| Tconv memCD27_total | 11.4% |
| CD8 RO CXCR3_CD8 | 11.4% |
| Tconv memTIGIT_total | 11.4% |
| Bcells memory_CD3neg | 11.4% |
| CD8 RO CCR4_total | 11.4% |
| PD1_CD8RO | 11.4% |
| CD8 RO_CD8 | 11.4% |
| Tconv memCD56_mem | 8.6% |
| CD8 ncytotox RO CCR4_CD3 | 8.6% |
| CD8 RO CD27_CD3 | 8.6% |
| CD8 RO CCR6_CD3 | 8.6% |
| Tconv memintB7_total | 8.6% |
| NKCD16_total | 8.6% |
| myeloid_total | 8.6% |
| CD8pos_CD3 | 8.6% |
| Treg naive_total | 8.6% |
| CD8 RO Ki67_CD8 | 8.6% |
| Tconv memDR_Tconv | 8.6% |
| Tconv memCXCR3_CD3 | 8.6% |
| Tconv memTIGIT_CD3 | 8.6% |
| Tconv memCCR4_Tconv | 5.7% |
| CD4 Tconv_CD3 | 5.7% |
| CD3pos_total | 5.7% |
| CD3neg_total | 5.7% |
| Treg memory_CD3 | 5.7% |
| myeloid_CD3neg | 5.7% |
| nonTnonB_total | 5.7% |
| CD8  RO Ki67_CD3 | 5.7% |
| NK_nonTnonB | 5.7% |
| CD8 RO_CD3 | 5.7% |
| NKCD16_CD3neg | 5.7% |
| NKCD16_nonTnonB | 5.7% |
| CD14mono_CD3neg | 5.7% |
| CD8 RA CCR7 naive_CD8 | 5.7% |
| NK_CD3neg | 5.7% |
| CD4 Treg _CD3 | 5.7% |
| CD14mono_total | 5.7% |
| Tconv memCD27_Tconv | 2.9% |
| CD4 Tconv_total | 2.9% |
| CD4neg_CD3 | 2.9% |

**Total features selected by SVM_RBF_Permutation_AboveMean_t50**: 160

#### SVM_RBF_Permutation_AboveMean_t60

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CCR4_CD8RO | 32.3% |
| CD16mono_myeloid | 32.3% |
| Bcells CD27posIgDneg_total | 29.0% |
| DR_CD8RO | 25.8% |
| CD8 RO DR_CD8 | 25.8% |
| CD27IgD_Bcells | 25.8% |
| Bcells CD27negIgDneg_total | 22.6% |
| memory_Bcells | 22.6% |
| Tconv memKi67_mem | 22.6% |
| CD8 ncytotox RO CCR4_CD8ntox | 22.6% |
| Tconv memCCR4_mem | 19.4% |
| CD8 RO DR_CD3 | 19.4% |
| CD16+mono_total | 19.4% |
| naive_Bcells | 19.4% |
| Bcells Ki67_total | 19.4% |
| Tconv memCCR6_mem | 19.4% |
| Bcells Ki67_CD3neg | 19.4% |
| Tconv memKi67_CD3 | 16.1% |
| NK Ki67_nonTnonB | 16.1% |
| Tconv memDR_total | 16.1% |
| CD3hi_total | 16.1% |
| Tconv memCCR6_CD3 | 16.1% |
| Tconv memCCR6_Tconv | 16.1% |
| Tconv memTIGIT_mem | 16.1% |
| Tconv memCCR5_mem | 16.1% |
| CD3hi_CD4neg | 16.1% |
| Tconv memDR_mem | 12.9% |
| CD8 RO CD27_total | 12.9% |
| CD8 RO PD1_total | 12.9% |
| TIGIT_CD8RO | 12.9% |
| CD4 Tconv mem_total | 12.9% |
| CD8 RA naive_CD3 | 12.9% |
| Tconv memCXCR3_mem | 12.9% |
| Treg naive_CD4 | 12.9% |
| Treg naive_CD3 | 12.9% |
| CD8 RA_total | 12.9% |
| CD8 RO TIGIT_total | 12.9% |
| Tconv memKi67_total | 12.9% |
| Tconv memCCR5_Tconv | 12.9% |
| Ki67_Bcells | 12.9% |
| CD8 RO CD27_CD8 | 12.9% |
| CD8 RA_CD3 | 12.9% |
| CD16mono_CD3neg | 12.9% |
| Tconv memintB7_CD3 | 12.9% |
| Tconv memCD56_total | 12.9% |
| CD4neg_total | 9.7% |
| NKCD56hi_CD3neg | 9.7% |
| Tconv memCD27_CD3 | 9.7% |
| Tconv memDR_Tconv | 9.7% |
| NKCD16_NK | 9.7% |
| Tconv memCD56_mem | 9.7% |
| CD8 RO_CD8 | 9.7% |
| Bcells naive_CD3neg | 9.7% |
| Tconv memDR_CD3 | 9.7% |
| NK Ki67_total | 9.7% |
| Treg naive_total | 9.7% |
| CD8 RO CXCR3_total | 9.7% |
| Tconv memPD1_mem | 9.7% |
| CD8 RA_CD8 | 9.7% |
| CD3hi_CD3 | 9.7% |
| Tconv memKi67_Tconv | 9.7% |
| Bcells memory_total | 9.7% |
| Tconv memCCR6_total | 9.7% |
| Tconv memCCR4_CD3 | 9.7% |
| CD8 RO TIGIT_CD8 | 9.7% |
| CD8 RO intB7_CD8 | 9.7% |
| intB7_CD8RO | 9.7% |
| CD8 RO DR_total | 9.7% |
| CD8 RA naive_total | 9.7% |
| NKCD56hi_nonTnonB | 9.7% |
| Treg memory_total | 9.7% |
| CCR6_CD8RO | 9.7% |
| CD8 RO TIGIT_CD3 | 9.7% |
| CD14+16+mono_myeloid | 6.5% |
| CD14mono_myeloid | 6.5% |
| CD27negIgDneg_Bcells | 6.5% |
| CD8 RO CCR6_total | 6.5% |
| Tconv memPD1_CD3 | 6.5% |
| PD1_CD8RO | 6.5% |
| CD8 RO CD27_CD3 | 6.5% |
| NKCD56hi_NK | 6.5% |
| Tconv memCCR4_total | 6.5% |
| Tconv memintB7_mem | 6.5% |
| Tconv memCXCR3_total | 6.5% |
| Tconv memCCR5_total | 6.5% |
| CD8 RO CD56_CD8 | 6.5% |
| CD8 RO_total | 6.5% |
| Tconv memCD56_CD3 | 6.5% |
| CD4 Treg_total | 6.5% |
| CD8 RO CD56_CD3 | 6.5% |
| CD8 RO CD56_total | 6.5% |
| CD8 RO CXCR3_CD3 | 6.5% |
| Tconv memCD56_Tconv | 6.5% |
| CD56_CD8RO | 6.5% |
| CD8 RO CXCR3_CD8 | 6.5% |
| NK Ki67_NK | 6.5% |
| CD8pos_total | 6.5% |
| Tconv memintB7_Tconv | 6.5% |
| nonTnonB_CD3neg | 6.5% |
| Tconv memTIGIT_total | 6.5% |
| myeloid_total | 6.5% |
| CXCR3_CD8RO | 6.5% |
| Tconv memCXCR3_Tconv | 6.5% |
| Bcells_total | 6.5% |
| CD8 RO Ki67_CD8 | 6.5% |
| CD8 RO PD1_CD3 | 6.5% |
| Tconv memCCR5_CD3 | 6.5% |
| Ki67_CD8RO | 6.5% |
| CD8 RO CCR5_CD8 | 6.5% |
| Bcells naive_total | 6.5% |
| NKCD56hi_total | 3.2% |
| NK_total | 3.2% |
| CD8 RO CCR5_total | 3.2% |
| NK_nonTnonB | 3.2% |
| NK Ki67_CD3neg | 3.2% |
| CD8 RO intB7_CD3 | 3.2% |
| CD8 RO intB7_total | 3.2% |
| CD8 ncytotox RO CCR4_CD3 | 3.2% |
| myeloid_CD3neg | 3.2% |
| NK_CD3neg | 3.2% |
| CD8 RO CCR6_CD8 | 3.2% |
| NKCD16_nonTnonB | 3.2% |
| Tconv mem_CD3 | 3.2% |
| Tconv memTIGIT_CD3 | 3.2% |
| NKCD16_CD3neg | 3.2% |
| CD4 Tconv_total | 3.2% |
| NKCD16_total | 3.2% |
| Bcells_CD3neg | 3.2% |
| CD8 RO CCR6_CD3 | 3.2% |
| CD8 RO CCR4_total | 3.2% |
| Tconv memintB7_total | 3.2% |
| CD4 Tconv_CD3 | 3.2% |
| CD4neg_CD3 | 3.2% |
| Tconv memCXCR3_CD3 | 3.2% |
| Tconv memCD27_total | 3.2% |
| CD14+16+mono_total | 3.2% |
| Tconv memPD1_total | 3.2% |
| CD14+16+mono_CD3neg | 3.2% |
| CCR5_CD8RO | 3.2% |
| CD14mono_total | 3.2% |
| CD8 RO PD1_CD8 | 3.2% |
| Tconv memCD27_mem | 3.2% |
| CD8 RO CCR5_CD3 | 3.2% |

**Total features selected by SVM_RBF_Permutation_AboveMean_t60**: 143

#### SVM_RBF_Permutation_AboveMean_t70

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD16mono_myeloid | 33.3% |
| CCR4_CD8RO | 33.3% |
| CD27IgD_Bcells | 26.7% |
| CD3hi_total | 26.7% |
| naive_Bcells | 26.7% |
| Tconv memCCR4_mem | 26.7% |
| CD8 RO DR_CD8 | 20.0% |
| Treg naive_CD3 | 20.0% |
| Tconv memKi67_mem | 20.0% |
| memory_Bcells | 20.0% |
| DR_CD8RO | 20.0% |
| Bcells memory_total | 20.0% |
| Tconv memCCR5_Tconv | 13.3% |
| CD3hi_CD3 | 13.3% |
| Bcells CD27negIgDneg_total | 13.3% |
| Tconv memCCR6_Tconv | 13.3% |
| CD16mono_CD3neg | 13.3% |
| CCR6_CD8RO | 13.3% |
| Tconv memCCR5_mem | 13.3% |
| Tconv memDR_mem | 13.3% |
| Tconv memDR_total | 13.3% |
| Bcells CD27posIgDneg_total | 13.3% |
| CD16+mono_total | 13.3% |
| CD8 RO CXCR3_total | 13.3% |
| CD8 RA_total | 13.3% |
| CD8 RO PD1_total | 6.7% |
| NKCD56hi_CD3neg | 6.7% |
| TIGIT_CD8RO | 6.7% |
| CD8 RO DR_CD3 | 6.7% |
| Treg memory_total | 6.7% |
| CD4 Treg_total | 6.7% |
| Treg naive_CD4 | 6.7% |
| NKCD16_NK | 6.7% |
| Tconv memCCR4_CD3 | 6.7% |
| NKCD56hi_NK | 6.7% |
| CD8 RO TIGIT_total | 6.7% |
| Tconv memKi67_CD3 | 6.7% |
| Bcells naive_total | 6.7% |
| Bcells Ki67_CD3neg | 6.7% |
| CD8 RO CD56_total | 6.7% |
| Tconv memCCR6_CD3 | 6.7% |
| Tconv memPD1_mem | 6.7% |
| Tconv memintB7_mem | 6.7% |
| CD8 RA_CD3 | 6.7% |
| CD8 ncytotox RO CCR4_CD8ntox | 6.7% |
| CD8pos_total | 6.7% |
| Bcells naive_CD3neg | 6.7% |
| NKCD56hi_nonTnonB | 6.7% |
| Tconv memCD27_total | 6.7% |
| CD4neg_CD3 | 6.7% |
| Tconv memintB7_total | 6.7% |
| CD8 RO CXCR3_CD3 | 6.7% |
| intB7_CD8RO | 6.7% |
| Tconv memCCR6_total | 6.7% |
| Tconv memCD56_total | 6.7% |
| Tconv memCD56_CD3 | 6.7% |
| Tconv memCD56_Tconv | 6.7% |
| CCR5_CD8RO | 6.7% |
| Tconv memCD56_mem | 6.7% |
| CD3hi_CD4neg | 6.7% |
| CD8 RO CCR5_CD8 | 6.7% |
| Bcells Ki67_total | 6.7% |
| Ki67_Bcells | 6.7% |
| CD14mono_myeloid | 6.7% |
| CD8 RA naive_CD3 | 6.7% |
| CD8 RO TIGIT_CD3 | 6.7% |
| NK Ki67_NK | 6.7% |

**Total features selected by SVM_RBF_Permutation_AboveMean_t70**: 67

#### SVM_RBF_Permutation_AboveMean_t80

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| naive_Bcells | 37.5% |
| CD16mono_myeloid | 37.5% |
| CCR4_CD8RO | 37.5% |
| DR_CD8RO | 25.0% |
| CD8 RO DR_CD8 | 25.0% |
| memory_Bcells | 25.0% |
| Tconv memCCR4_mem | 25.0% |
| CD3hi_total | 25.0% |
| Bcells memory_total | 25.0% |
| CD8 RO PD1_total | 12.5% |
| Treg naive_CD3 | 12.5% |
| Tconv memCCR6_CD3 | 12.5% |
| Tconv memDR_total | 12.5% |
| CD16mono_CD3neg | 12.5% |
| CD16+mono_total | 12.5% |
| CD8 RO TIGIT_total | 12.5% |
| CD8 RA_CD3 | 12.5% |
| CD8 ncytotox RO CCR4_CD8ntox | 12.5% |
| intB7_CD8RO | 12.5% |
| CD3hi_CD3 | 12.5% |
| CD3hi_CD4neg | 12.5% |
| Bcells CD27posIgDneg_total | 12.5% |
| CD27IgD_Bcells | 12.5% |
| CD8 RO TIGIT_CD3 | 12.5% |

**Total features selected by SVM_RBF_Permutation_AboveMean_t80**: 24

#### SVM_RBF_Permutation_Top10%_t40

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD4 Treg_total | 75.0% |
| Tconv memDR_total | 70.0% |
| Tconv memCXCR3_total | 70.0% |
| Tconv memKi67_total | 70.0% |
| Tconv memCD56_total | 67.5% |
| Tconv memCD27_total | 62.5% |
| Tconv memPD1_total | 62.5% |
| Tconv memTIGIT_total | 60.0% |
| Tconv memintB7_total | 55.0% |
| Tconv naive_total | 52.5% |
| CD3pos_total | 42.5% |
| CD4 Tconv mem_total | 40.0% |
| Tconv memCCR6_total | 37.5% |
| Tconv memCCR5_total | 35.0% |
| CD4 Tconv_total | 32.5% |
| Tconv memCCR4_total | 32.5% |
| DR_CD8RO | 27.5% |
| CCR4_CD8RO | 17.5% |
| CD8 RO DR_CD8 | 17.5% |
| CD16mono_myeloid | 17.5% |
| Bcells CD27posIgDneg_total | 12.5% |
| CD3hi_total | 10.0% |
| CD16mono_CD3neg | 10.0% |
| Tconv memDR_mem | 7.5% |
| CD8 RA naive_total | 5.0% |
| Bcells memory_total | 5.0% |
| CD16+mono_total | 5.0% |
| CD3hi_CD4neg | 5.0% |
| Tconv memPD1_mem | 2.5% |
| Ki67_Bcells | 2.5% |
| CD8 RO DR_total | 2.5% |
| CD27negIgDneg_Bcells | 2.5% |
| CD8 RO CXCR3_total | 2.5% |
| Tconv memCCR6_CD3 | 2.5% |
| CD56_CD8RO | 2.5% |
| CD8 RO DR_CD3 | 2.5% |
| CD8 RO CD56_total | 2.5% |
| NKCD16_NK | 2.5% |
| CD8 ncytotox RO CCR4_CD8ntox | 2.5% |
| CD8 RO CD27_total | 2.5% |
| CD4neg_total | 2.5% |
| CD27IgD_Bcells | 2.5% |
| CD8 RO TIGIT_CD8 | 2.5% |
| CCR5_CD8RO | 2.5% |
| intB7_CD8RO | 2.5% |
| NKCD56hi_CD3neg | 2.5% |
| Tconv memintB7_CD3 | 2.5% |
| NK Ki67_nonTnonB | 2.5% |

**Total features selected by SVM_RBF_Permutation_Top10%_t40**: 48

#### SVM_RBF_Permutation_Top10%_t50

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD4 Treg_total | 54.3% |
| Tconv memCXCR3_total | 54.3% |
| Tconv memKi67_total | 48.6% |
| Tconv memCD56_total | 48.6% |
| Tconv memDR_total | 45.7% |
| Tconv memintB7_total | 40.0% |
| Tconv memPD1_total | 40.0% |
| Tconv naive_total | 37.1% |
| Tconv memCD27_total | 34.3% |
| CD3pos_total | 34.3% |
| Tconv memTIGIT_total | 28.6% |
| Tconv memCCR4_total | 22.9% |
| Tconv memCCR6_total | 20.0% |
| CD4 Tconv_total | 20.0% |
| Tconv memCCR5_total | 20.0% |
| CD4 Tconv mem_total | 17.1% |
| CCR4_CD8RO | 11.4% |
| CD3hi_total | 8.6% |
| CD16mono_myeloid | 8.6% |
| CD16mono_CD3neg | 8.6% |
| CD8 RA naive_total | 5.7% |
| DR_CD8RO | 5.7% |
| CD8 RO DR_CD8 | 5.7% |
| Tconv memPD1_mem | 2.9% |
| CD8 RO CXCR3_total | 2.9% |
| CD8 RO DR_CD3 | 2.9% |
| Bcells memory_total | 2.9% |
| CD16+mono_total | 2.9% |
| Tconv memDR_mem | 2.9% |
| NK Ki67_nonTnonB | 2.9% |

**Total features selected by SVM_RBF_Permutation_Top10%_t50**: 30

#### SVM_RBF_Permutation_Top10%_t60

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Tconv memCXCR3_total | 47.8% |
| Tconv memKi67_total | 43.5% |
| Tconv memCD56_total | 39.1% |
| Tconv memDR_total | 39.1% |
| Tconv memintB7_total | 34.8% |
| Tconv memPD1_total | 30.4% |
| Tconv memTIGIT_total | 30.4% |
| Tconv memCD27_total | 26.1% |
| Tconv naive_total | 26.1% |
| CD4 Treg_total | 26.1% |
| Tconv memCCR5_total | 17.4% |
| CD3pos_total | 17.4% |
| CD4 Tconv_total | 13.0% |
| CD4 Tconv mem_total | 8.7% |
| Tconv memCCR4_total | 8.7% |
| CD16mono_CD3neg | 8.7% |
| CD3hi_total | 4.3% |
| CD8 RO DR_CD3 | 4.3% |
| CCR4_CD8RO | 4.3% |
| CD16+mono_total | 4.3% |
| CD16mono_myeloid | 4.3% |
| Tconv memDR_mem | 4.3% |

**Total features selected by SVM_RBF_Permutation_Top10%_t60**: 22

#### SVM_RBF_Permutation_Top10%_t70

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Tconv memKi67_total | 55.6% |
| Tconv memCXCR3_total | 55.6% |
| Tconv memDR_total | 44.4% |
| CD4 Treg_total | 33.3% |
| Tconv memintB7_total | 22.2% |
| Tconv memPD1_total | 22.2% |
| Tconv memTIGIT_total | 22.2% |
| CD3pos_total | 11.1% |
| Tconv memCD56_total | 11.1% |
| Tconv memCD27_total | 11.1% |
| CD4 Tconv_total | 11.1% |
| Tconv naive_total | 11.1% |

**Total features selected by SVM_RBF_Permutation_Top10%_t70**: 12

#### SVM_RBF_Permutation_Top10%_t80

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Tconv memDR_total | 66.7% |
| Tconv memPD1_total | 33.3% |
| CD4 Treg_total | 33.3% |
| Tconv memCXCR3_total | 33.3% |

**Total features selected by SVM_RBF_Permutation_Top10%_t80**: 4

#### XGB_Importance_t40

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Bcells CD27posIgDneg_total | 100.0% |
| CD27IgD_Bcells | 92.5% |
| CD8 RO DR_CD3 | 90.0% |
| CD16mono_myeloid | 82.5% |
| Tconv naive_total | 65.0% |
| CD16mono_CD3neg | 65.0% |
| Tconv memDR_mem | 60.0% |
| Tconv memPD1_total | 55.0% |
| CD4 Treg_CD4 | 52.5% |
| Ki67_Bcells | 45.0% |
| CD8  RO Ki67_CD3 | 37.5% |
| CD16+mono_total | 35.0% |
| CD8 RO PD1_CD3 | 35.0% |
| NKCD56hi_total | 32.5% |
| CD3hi_total | 30.0% |
| naive_Bcells | 30.0% |
| CD8pos_CD3 | 30.0% |
| CD3pos_total | 27.5% |
| Tconv naive_CD3 | 25.0% |
| NKCD16_NK | 25.0% |
| Tconv mem_Tconv | 25.0% |
| Tconv memCXCR3_total | 22.5% |
| Tconv memDR_CD3 | 22.5% |
| CD8 RA naive_CD3 | 22.5% |
| memory_Bcells | 22.5% |
| CD4 Tconv_total | 22.5% |
| CD8 RA CCR7 naive_CD8 | 20.0% |
| CD56_CD8RO | 20.0% |
| Tconv memKi67_total | 20.0% |
| CD8 RO DR_CD8 | 20.0% |
| CD4 Tconv mem_total | 20.0% |
| nonTnonB_CD3neg | 20.0% |
| CD8 RO CD56_CD3 | 20.0% |
| Bcells_total | 17.5% |
| Tconv memTIGIT_total | 17.5% |
| CD8 RO CCR5_total | 15.0% |
| Tconv memDR_Tconv | 15.0% |
| NKCD56hi_nonTnonB | 15.0% |
| CD8 RA_CD3 | 15.0% |
| Tconv memCCR4_total | 15.0% |
| NK Ki67_total | 12.5% |
| CD8 RO CXCR3_CD8 | 12.5% |
| Tconv memCD27_CD3 | 12.5% |
| NK_total | 12.5% |
| Tconv memDR_total | 12.5% |
| Tconv memPD1_mem | 12.5% |
| CD8 RO CCR5_CD3 | 12.5% |
| DR_CD8RO | 12.5% |
| Treg memory_CD4 | 12.5% |
| Bcells memory_total | 12.5% |
| CD8 RO CD56_total | 10.0% |
| Tconv memCD27_Tconv | 10.0% |
| intB7_CD8RO | 10.0% |
| CD8 RA_total | 10.0% |
| CD4 Treg_total | 10.0% |
| Tconv memCCR5_mem | 10.0% |
| CD14+16+mono_myeloid | 10.0% |
| CD8 RO CXCR3_CD3 | 10.0% |
| Tconv memCXCR3_CD3 | 10.0% |
| Bcells Ki67_total | 10.0% |
| CD3hi_CD3 | 10.0% |
| Tconv memKi67_mem | 10.0% |
| NK Ki67_NK | 10.0% |
| CD8 RO DR_total | 10.0% |
| CCR5_CD8RO | 10.0% |
| Tconv memCCR4_Tconv | 7.5% |
| Bcells CD27negIgDneg_total | 7.5% |
| Tconv memTIGIT_mem | 7.5% |
| CD8 RO CCR5_CD8 | 7.5% |
| CD8pos_total | 7.5% |
| CD4 Tconv_CD3 | 7.5% |
| CD14mono_total | 7.5% |
| NKCD56hi_NK | 7.5% |
| Tconv memPD1_CD3 | 7.5% |
| Tconv memCCR6_total | 7.5% |
| NK_CD3neg | 7.5% |
| Tconv memCCR6_mem | 7.5% |
| Tconv memCCR6_Tconv | 5.0% |
| CD8 RO PD1_CD8 | 5.0% |
| Tconv memCXCR3_mem | 5.0% |
| CD14+16+mono_total | 5.0% |
| CD8 RO TIGIT_total | 5.0% |
| Treg naive_total | 5.0% |
| CD8 RO CD56_CD8 | 5.0% |
| Tconv memTIGIT_CD3 | 5.0% |
| Tconv memintB7_total | 5.0% |
| TIGIT_CD8RO | 5.0% |
| CD8 RO Ki67_total | 5.0% |
| Tconv memCD27_mem | 5.0% |
| CD8 RO TIGIT_CD8 | 5.0% |
| Tconv memCCR6_CD3 | 5.0% |
| CD27_CD8RO | 5.0% |
| CD4neg_CD3 | 5.0% |
| CD3hi_CD4neg | 5.0% |
| CD14+16+mono_CD3neg | 2.5% |
| Tconv memTIGIT_Tconv | 2.5% |
| Tconv memCCR4_mem | 2.5% |
| CD27negIgDneg_Bcells | 2.5% |
| CD8 RO CXCR3_total | 2.5% |
| CD8 RO CD27_CD8 | 2.5% |
| Tconv memintB7_mem | 2.5% |
| Tconv memintB7_CD3 | 2.5% |
| Treg memory_CD3 | 2.5% |
| Bcells naive_total | 2.5% |
| CD14mono_CD3neg | 2.5% |
| Tconv mem_CD3 | 2.5% |
| CD8 RA_CD8 | 2.5% |
| NKCD16_total | 2.5% |
| Tconv memCCR5_CD3 | 2.5% |
| NK_nonTnonB | 2.5% |
| CD4 Treg _CD3 | 2.5% |
| NKCD56hi_CD3neg | 2.5% |
| CD8 RO intB7_total | 2.5% |
| Treg memory_total | 2.5% |
| Tconv memintB7_Tconv | 2.5% |
| CD8 RO PD1_total | 2.5% |
| CD8 RA naive_total | 2.5% |
| Treg naive_CD4 | 2.5% |
| CD8 RO intB7_CD8 | 2.5% |
| Tconv memCD56_total | 2.5% |
| Tconv memCXCR3_Tconv | 2.5% |
| myeloid_total | 2.5% |
| CD8 RO CCR6_CD3 | 2.5% |
| Tconv memCD27_total | 2.5% |
| Ki67_CD8RO | 2.5% |
| nonTnonB_total | 2.5% |

**Total features selected by XGB_Importance_t40**: 126

#### XGB_Importance_t50

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Bcells CD27posIgDneg_total | 95.0% |
| CD27IgD_Bcells | 80.0% |
| CD8 RO DR_CD3 | 75.0% |
| CD16mono_myeloid | 67.5% |
| CD16mono_CD3neg | 47.5% |
| Tconv memDR_mem | 47.5% |
| Tconv memPD1_total | 42.5% |
| Ki67_Bcells | 37.5% |
| CD4 Treg_CD4 | 37.5% |
| Tconv naive_total | 37.5% |
| CD8  RO Ki67_CD3 | 30.0% |
| CD3hi_total | 20.0% |
| CD16+mono_total | 20.0% |
| Tconv mem_Tconv | 20.0% |
| naive_Bcells | 20.0% |
| NKCD56hi_total | 20.0% |
| CD8 RO CD56_CD3 | 15.0% |
| Tconv memDR_CD3 | 15.0% |
| NKCD16_NK | 12.5% |
| Tconv memKi67_total | 12.5% |
| CD8 RO PD1_CD3 | 12.5% |
| nonTnonB_CD3neg | 10.0% |
| Tconv memPD1_mem | 10.0% |
| CD8 RO DR_CD8 | 10.0% |
| CD3pos_total | 10.0% |
| Bcells_total | 10.0% |
| Tconv memTIGIT_total | 10.0% |
| CCR5_CD8RO | 10.0% |
| Tconv memCCR4_total | 10.0% |
| CD8pos_CD3 | 10.0% |
| CD4 Tconv_total | 7.5% |
| CD4 Tconv mem_total | 7.5% |
| memory_Bcells | 7.5% |
| NK_total | 7.5% |
| CD56_CD8RO | 7.5% |
| CD8 RA CCR7 naive_CD8 | 7.5% |
| Tconv memDR_total | 7.5% |
| CD8 RA naive_CD3 | 7.5% |
| CD14+16+mono_myeloid | 7.5% |
| CD4 Tconv_CD3 | 5.0% |
| CD8 RO CD56_CD8 | 5.0% |
| NKCD56hi_NK | 5.0% |
| Tconv memCCR6_CD3 | 5.0% |
| CD8 RO DR_total | 5.0% |
| CD8pos_total | 5.0% |
| Tconv memCD27_mem | 5.0% |
| Bcells memory_total | 5.0% |
| Tconv naive_CD3 | 5.0% |
| Tconv memCXCR3_CD3 | 5.0% |
| CD14mono_total | 5.0% |
| DR_CD8RO | 5.0% |
| Tconv memTIGIT_mem | 2.5% |
| Tconv memCD27_Tconv | 2.5% |
| CD4neg_CD3 | 2.5% |
| Treg naive_total | 2.5% |
| Tconv memCCR5_mem | 2.5% |
| Bcells Ki67_total | 2.5% |
| Tconv memintB7_total | 2.5% |
| CD8 RO CD56_total | 2.5% |
| CD8 RO CD27_CD8 | 2.5% |
| CD8 RA_total | 2.5% |
| Tconv memCD27_CD3 | 2.5% |
| Tconv memCCR4_Tconv | 2.5% |
| CD8 RA_CD3 | 2.5% |
| Tconv memintB7_mem | 2.5% |
| intB7_CD8RO | 2.5% |
| Treg memory_CD4 | 2.5% |
| Tconv memDR_Tconv | 2.5% |
| Tconv mem_CD3 | 2.5% |
| CD8 RO TIGIT_CD8 | 2.5% |
| Tconv memKi67_mem | 2.5% |
| CD8 RO CCR5_total | 2.5% |
| CD8 RO CCR5_CD8 | 2.5% |
| CD8 RO CXCR3_CD3 | 2.5% |
| Tconv memCCR6_total | 2.5% |
| CD3hi_CD3 | 2.5% |
| NK Ki67_NK | 2.5% |
| Tconv memCCR6_mem | 2.5% |
| NK Ki67_total | 2.5% |
| Tconv memCXCR3_Tconv | 2.5% |
| NKCD56hi_nonTnonB | 2.5% |
| CD14+16+mono_total | 2.5% |

**Total features selected by XGB_Importance_t50**: 82

#### XGB_Importance_t60

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Bcells CD27posIgDneg_total | 87.5% |
| CD8 RO DR_CD3 | 60.0% |
| CD27IgD_Bcells | 57.5% |
| CD16mono_myeloid | 50.0% |
| CD16mono_CD3neg | 45.0% |
| Ki67_Bcells | 25.0% |
| Tconv memDR_mem | 20.0% |
| Tconv naive_total | 20.0% |
| CD4 Treg_CD4 | 17.5% |
| CD8  RO Ki67_CD3 | 17.5% |
| CD3hi_total | 12.5% |
| Tconv memPD1_total | 10.0% |
| CD16+mono_total | 7.5% |
| NKCD56hi_total | 7.5% |
| Tconv memKi67_total | 7.5% |
| Tconv mem_Tconv | 7.5% |
| Tconv memPD1_mem | 5.0% |
| Tconv memDR_CD3 | 5.0% |
| naive_Bcells | 5.0% |
| CD4 Tconv mem_total | 5.0% |
| CD8 RO DR_CD8 | 5.0% |
| nonTnonB_CD3neg | 5.0% |
| CCR5_CD8RO | 5.0% |
| CD8 RO CD56_CD3 | 5.0% |
| NKCD16_NK | 5.0% |
| CD8 RO PD1_CD3 | 5.0% |
| CD4 Tconv_CD3 | 2.5% |
| CD8 RO CD56_CD8 | 2.5% |
| CD4 Tconv_total | 2.5% |
| Tconv naive_CD3 | 2.5% |
| CD4neg_CD3 | 2.5% |
| Bcells Ki67_total | 2.5% |
| NK_total | 2.5% |
| Bcells memory_total | 2.5% |
| CD14+16+mono_myeloid | 2.5% |
| CD8 RO TIGIT_CD8 | 2.5% |
| DR_CD8RO | 2.5% |
| Tconv memKi67_mem | 2.5% |
| Tconv memTIGIT_total | 2.5% |
| CD8 RO CCR5_total | 2.5% |
| CD8 RA naive_CD3 | 2.5% |
| CD8 RO DR_total | 2.5% |
| Tconv memCCR4_total | 2.5% |
| CD3pos_total | 2.5% |

**Total features selected by XGB_Importance_t60**: 44

#### XGB_Importance_t70

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Bcells CD27posIgDneg_total | 82.5% |
| CD8 RO DR_CD3 | 47.5% |
| CD16mono_myeloid | 40.0% |
| CD27IgD_Bcells | 37.5% |
| CD16mono_CD3neg | 25.0% |
| Tconv memDR_mem | 12.5% |
| CD8  RO Ki67_CD3 | 10.0% |
| Tconv naive_total | 10.0% |
| Ki67_Bcells | 7.5% |
| CD4 Treg_CD4 | 7.5% |
| NKCD56hi_total | 5.0% |
| CD8 RO PD1_CD3 | 5.0% |
| Tconv mem_Tconv | 5.0% |
| Tconv memPD1_total | 5.0% |
| Tconv memPD1_mem | 2.5% |
| naive_Bcells | 2.5% |
| NK_total | 2.5% |
| NKCD16_NK | 2.5% |
| Tconv naive_CD3 | 2.5% |
| Tconv memDR_CD3 | 2.5% |
| CD4 Tconv_total | 2.5% |
| CD3hi_total | 2.5% |
| CD8 RA naive_CD3 | 2.5% |
| Tconv memCCR4_total | 2.5% |
| CD3pos_total | 2.5% |

**Total features selected by XGB_Importance_t70**: 25

#### XGB_Importance_t80

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Bcells CD27posIgDneg_total | 66.7% |
| CD16mono_myeloid | 38.9% |
| CD8 RO DR_CD3 | 27.8% |
| CD27IgD_Bcells | 25.0% |
| CD16mono_CD3neg | 13.9% |
| Tconv naive_total | 11.1% |
| Ki67_Bcells | 5.6% |
| CD4 Treg_CD4 | 5.6% |
| Tconv memPD1_mem | 2.8% |
| Tconv memDR_CD3 | 2.8% |
| NKCD16_NK | 2.8% |
| CD8  RO Ki67_CD3 | 2.8% |
| Tconv memDR_mem | 2.8% |

**Total features selected by XGB_Importance_t80**: 13

#### XGBoost_Permutation_AboveMean_t40

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Bcells CD27posIgDneg_total | 65.2% |
| CD16mono_myeloid | 34.8% |
| CD8 RO DR_CD3 | 8.7% |
| Ki67_Bcells | 4.3% |
| Tconv naive_total | 4.3% |
| Tconv memDR_mem | 4.3% |

**Total features selected by XGBoost_Permutation_AboveMean_t40**: 6

#### XGBoost_Permutation_AboveMean_t50

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Bcells CD27posIgDneg_total | 58.8% |
| CD16mono_myeloid | 23.5% |
| CD8 RO DR_CD3 | 11.8% |
| Ki67_Bcells | 5.9% |
| Tconv naive_total | 5.9% |
| Tconv memDR_mem | 5.9% |

**Total features selected by XGBoost_Permutation_AboveMean_t50**: 6

#### XGBoost_Permutation_AboveMean_t60

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Bcells CD27posIgDneg_total | 60.0% |
| CD8 RO DR_CD3 | 20.0% |
| CD16mono_myeloid | 10.0% |
| Tconv naive_total | 10.0% |

**Total features selected by XGBoost_Permutation_AboveMean_t60**: 4

#### XGBoost_Permutation_AboveMean_t70

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Bcells CD27posIgDneg_total | 66.7% |
| CD8 RO DR_CD3 | 33.3% |

**Total features selected by XGBoost_Permutation_AboveMean_t70**: 2

#### XGBoost_Permutation_AboveMean_t80

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Bcells CD27posIgDneg_total | 100.0% |

**Total features selected by XGBoost_Permutation_AboveMean_t80**: 1

#### XGBoost_Permutation_Top10%_t40

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Tconv memPD1_total | 100.0% |
| Tconv memCXCR3_total | 100.0% |
| Tconv memCD27_total | 100.0% |
| Tconv memintB7_total | 100.0% |
| Tconv memDR_total | 100.0% |
| Tconv memCD56_total | 100.0% |
| Tconv memTIGIT_total | 100.0% |
| Tconv naive_total | 100.0% |
| Tconv memKi67_total | 100.0% |
| CD4 Treg_total | 97.5% |
| CD3pos_total | 95.0% |
| Tconv memCCR6_total | 85.0% |
| CD4 Tconv_total | 72.5% |
| CD4 Tconv mem_total | 72.5% |
| Tconv memCCR4_total | 50.0% |
| Tconv memCCR5_total | 42.5% |
| Bcells CD27posIgDneg_total | 42.5% |
| CD16mono_myeloid | 22.5% |
| CD8 RO DR_CD3 | 10.0% |
| Ki67_Bcells | 7.5% |
| Tconv memCCR6_Tconv | 2.5% |
| Tconv memDR_mem | 2.5% |

**Total features selected by XGBoost_Permutation_Top10%_t40**: 22

#### XGBoost_Permutation_Top10%_t50

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Tconv memPD1_total | 100.0% |
| Tconv memCD27_total | 100.0% |
| Tconv memCXCR3_total | 100.0% |
| Tconv memCD56_total | 100.0% |
| Tconv memDR_total | 100.0% |
| Tconv memKi67_total | 100.0% |
| Tconv memintB7_total | 100.0% |
| Tconv naive_total | 100.0% |
| Tconv memTIGIT_total | 97.5% |
| CD4 Treg_total | 92.5% |
| CD3pos_total | 75.0% |
| Tconv memCCR6_total | 70.0% |
| CD4 Tconv mem_total | 65.0% |
| CD4 Tconv_total | 32.5% |
| Bcells CD27posIgDneg_total | 27.5% |
| Tconv memCCR5_total | 17.5% |
| CD16mono_myeloid | 15.0% |
| Tconv memCCR4_total | 10.0% |
| CD8 RO DR_CD3 | 5.0% |
| Ki67_Bcells | 2.5% |
| Tconv memDR_mem | 2.5% |

**Total features selected by XGBoost_Permutation_Top10%_t50**: 21

#### XGBoost_Permutation_Top10%_t60

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Tconv memPD1_total | 100.0% |
| Tconv memCD27_total | 100.0% |
| Tconv memCD56_total | 100.0% |
| Tconv memintB7_total | 100.0% |
| Tconv memKi67_total | 100.0% |
| Tconv memDR_total | 97.5% |
| Tconv memTIGIT_total | 95.0% |
| Tconv naive_total | 95.0% |
| CD4 Treg_total | 90.0% |
| Tconv memCXCR3_total | 90.0% |
| CD3pos_total | 65.0% |
| Tconv memCCR6_total | 42.5% |
| CD4 Tconv mem_total | 35.0% |
| Bcells CD27posIgDneg_total | 22.5% |
| CD4 Tconv_total | 15.0% |
| Tconv memCCR4_total | 7.5% |
| CD8 RO DR_CD3 | 5.0% |
| Tconv memCCR5_total | 5.0% |
| Ki67_Bcells | 2.5% |
| CD16mono_myeloid | 2.5% |

**Total features selected by XGBoost_Permutation_Top10%_t60**: 20

#### XGBoost_Permutation_Top10%_t70

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Tconv memPD1_total | 100.0% |
| Tconv memCD56_total | 100.0% |
| Tconv memintB7_total | 100.0% |
| Tconv memKi67_total | 100.0% |
| Tconv memCD27_total | 97.5% |
| Tconv memDR_total | 95.0% |
| Tconv naive_total | 90.0% |
| Tconv memCXCR3_total | 85.0% |
| CD4 Treg_total | 82.5% |
| Tconv memTIGIT_total | 80.0% |
| CD3pos_total | 45.0% |
| Tconv memCCR6_total | 25.0% |
| CD4 Tconv mem_total | 12.5% |
| CD4 Tconv_total | 7.5% |
| Bcells CD27posIgDneg_total | 5.0% |
| CD8 RO DR_CD3 | 2.5% |

**Total features selected by XGBoost_Permutation_Top10%_t70**: 16

#### XGBoost_Permutation_Top10%_t80

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Tconv memPD1_total | 97.5% |
| Tconv memKi67_total | 97.5% |
| Tconv memintB7_total | 95.0% |
| Tconv memCD56_total | 92.5% |
| Tconv memCD27_total | 92.5% |
| Tconv memDR_total | 90.0% |
| Tconv naive_total | 85.0% |
| Tconv memCXCR3_total | 82.5% |
| Tconv memTIGIT_total | 72.5% |
| CD4 Treg_total | 72.5% |
| CD3pos_total | 32.5% |
| Tconv memCCR6_total | 15.0% |
| CD4 Tconv mem_total | 7.5% |
| Bcells CD27posIgDneg_total | 5.0% |
| CD4 Tconv_total | 5.0% |

**Total features selected by XGBoost_Permutation_Top10%_t80**: 15

#### mRMR (Top 10%)_t40

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD16mono_myeloid | 77.5% |
| CD8 RO DR_CD3 | 77.5% |
| CD8 RO DR_CD8 | 70.0% |
| Treg memory_CD4 | 57.5% |
| Treg memory_CD3 | 52.5% |
| CD4 Tconv_total | 50.0% |
| CD4 Treg_CD4 | 47.5% |
| CD14mono_myeloid | 45.0% |
| DR_CD8RO | 45.0% |
| Tconv mem_Tconv | 42.5% |
| Tconv memDR_Tconv | 37.5% |
| Tconv naive_CD3 | 37.5% |
| CD16mono_CD3neg | 32.5% |
| CD4 Treg _CD3 | 30.0% |
| NKCD56hi_total | 30.0% |
| CD14+16+mono_myeloid | 30.0% |
| Tconv memDR_CD3 | 27.5% |
| CD27IgD_Bcells | 27.5% |
| Tconv naive_Tconv | 27.5% |
| Tconv naive_total | 25.0% |
| CD8pos_CD3 | 25.0% |
| CD3neg_total | 25.0% |
| CD3pos_total | 25.0% |
| CD3hi_total | 22.5% |
| Bcells CD27posIgDneg_total | 22.5% |
| CD8 RO CD56_CD3 | 17.5% |
| CD4 Tconv_CD3 | 15.0% |
| Tconv memDR_mem | 15.0% |
| Tconv memCD27_Tconv | 15.0% |
| Ki67_Bcells | 12.5% |
| NKCD16_NK | 12.5% |
| NKCD56hi_NK | 12.5% |
| nonTnonB_total | 10.0% |
| CD8 RO PD1_CD3 | 10.0% |
| CD8 RO CXCR3_CD3 | 10.0% |
| Tconv memCCR6_total | 10.0% |
| Bcells memory_CD3neg | 10.0% |
| CD14+16+mono_CD3neg | 7.5% |
| Tconv memCD56_total | 7.5% |
| CD8 RO_CD3 | 7.5% |
| CD8 RA_CD3 | 5.0% |
| CD8 RA naive_total | 5.0% |
| Tconv memintB7_Tconv | 5.0% |
| Tconv memTIGIT_mem | 5.0% |
| CD4neg_CD3 | 5.0% |
| Bcells CD27negIgDneg_total | 5.0% |
| CD8 RO TIGIT_CD3 | 5.0% |
| Tconv mem_CD3 | 5.0% |
| CD16+mono_total | 5.0% |
| NK Ki67_NK | 5.0% |
| CD8 RO DR_total | 5.0% |
| CCR4_CD8RO | 5.0% |
| memory_Bcells | 5.0% |
| intB7_CD8RO | 5.0% |
| Tconv memCCR5_total | 2.5% |
| Tconv memintB7_CD3 | 2.5% |
| CD8 ncytotox RO CCR4_CD3 | 2.5% |
| Bcells Ki67_CD3neg | 2.5% |
| CD27_CD8RO | 2.5% |
| CD14mono_total | 2.5% |
| Tconv memCD27_mem | 2.5% |
| NK Ki67_total | 2.5% |
| CD14mono_CD3neg | 2.5% |
| Bcells naive_CD3neg | 2.5% |
| nonTnonB_CD3neg | 2.5% |
| Bcells_CD3neg | 2.5% |
| Bcells naive_total | 2.5% |
| CD14+16+mono_total | 2.5% |
| NKCD56hi_CD3neg | 2.5% |
| CD27negIgDneg_Bcells | 2.5% |
| Tconv memCXCR3_Tconv | 2.5% |
| Tconv memKi67_total | 2.5% |
| CD8 RO Ki67_CD8 | 2.5% |
| Tconv memPD1_mem | 2.5% |
| Treg naive_total | 2.5% |
| CD8 RO intB7_CD8 | 2.5% |
| Tconv memCCR4_total | 2.5% |
| CD8 RO CD27_CD3 | 2.5% |

**Total features selected by mRMR (Top 10%)_t40**: 78

#### mRMR (Top 10%)_t50

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD16mono_myeloid | 67.5% |
| CD8 RO DR_CD8 | 57.5% |
| Treg memory_CD4 | 50.0% |
| CD4 Tconv_total | 45.0% |
| CD4 Treg_CD4 | 40.0% |
| Treg memory_CD3 | 37.5% |
| CD14mono_myeloid | 35.0% |
| CD8 RO DR_CD3 | 35.0% |
| Tconv memDR_Tconv | 32.5% |
| DR_CD8RO | 30.0% |
| Tconv mem_Tconv | 25.0% |
| Tconv naive_total | 20.0% |
| Tconv memDR_CD3 | 20.0% |
| CD16mono_CD3neg | 20.0% |
| CD3neg_total | 17.5% |
| Tconv naive_CD3 | 17.5% |
| CD3hi_total | 17.5% |
| CD14+16+mono_myeloid | 17.5% |
| NKCD56hi_total | 17.5% |
| Bcells CD27posIgDneg_total | 17.5% |
| CD27IgD_Bcells | 17.5% |
| CD8pos_CD3 | 15.0% |
| CD4 Treg _CD3 | 15.0% |
| Tconv naive_Tconv | 12.5% |
| CD3pos_total | 12.5% |
| nonTnonB_total | 10.0% |
| CD4 Tconv_CD3 | 10.0% |
| Ki67_Bcells | 7.5% |
| CD8 RO CD56_CD3 | 7.5% |
| NKCD16_NK | 7.5% |
| NKCD56hi_NK | 7.5% |
| CD8 RA naive_total | 5.0% |
| Bcells memory_CD3neg | 5.0% |
| CD8 RO TIGIT_CD3 | 5.0% |
| CD8 RO PD1_CD3 | 5.0% |
| CD4neg_CD3 | 2.5% |
| Bcells Ki67_CD3neg | 2.5% |
| NK Ki67_total | 2.5% |
| Tconv memintB7_CD3 | 2.5% |
| Tconv memTIGIT_mem | 2.5% |
| CD8 RO_CD3 | 2.5% |
| Tconv memCD27_Tconv | 2.5% |
| NK Ki67_NK | 2.5% |
| CD8 RO DR_total | 2.5% |
| CD14mono_total | 2.5% |
| Bcells CD27negIgDneg_total | 2.5% |
| nonTnonB_CD3neg | 2.5% |
| CD14+16+mono_CD3neg | 2.5% |
| CD8 RO CXCR3_CD3 | 2.5% |
| intB7_CD8RO | 2.5% |
| Tconv memPD1_mem | 2.5% |
| Tconv memDR_mem | 2.5% |
| Tconv memCCR4_total | 2.5% |

**Total features selected by mRMR (Top 10%)_t50**: 53

#### mRMR (Top 10%)_t60

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD16mono_myeloid | 52.5% |
| CD8 RO DR_CD8 | 40.0% |
| CD4 Tconv_total | 35.0% |
| Treg memory_CD4 | 32.5% |
| CD8 RO DR_CD3 | 30.0% |
| Tconv memDR_Tconv | 20.0% |
| CD4 Treg_CD4 | 20.0% |
| Tconv mem_Tconv | 17.5% |
| CD14mono_myeloid | 17.5% |
| Treg memory_CD3 | 15.0% |
| DR_CD8RO | 15.0% |
| CD3hi_total | 12.5% |
| CD27IgD_Bcells | 12.5% |
| Tconv naive_total | 12.5% |
| CD16mono_CD3neg | 10.0% |
| CD14+16+mono_myeloid | 10.0% |
| CD4 Treg _CD3 | 10.0% |
| CD4 Tconv_CD3 | 10.0% |
| Bcells CD27posIgDneg_total | 7.5% |
| Tconv naive_CD3 | 7.5% |
| CD3pos_total | 7.5% |
| CD3neg_total | 7.5% |
| Tconv memDR_CD3 | 7.5% |
| Tconv naive_Tconv | 5.0% |
| NKCD56hi_total | 5.0% |
| CD8 RA naive_total | 2.5% |
| CD8 RO CD56_CD3 | 2.5% |
| Bcells Ki67_CD3neg | 2.5% |
| CD14+16+mono_CD3neg | 2.5% |
| CD8 RO DR_total | 2.5% |
| NKCD56hi_NK | 2.5% |
| CD8pos_CD3 | 2.5% |
| NKCD16_NK | 2.5% |
| CD8 RO CXCR3_CD3 | 2.5% |
| CD8 RO PD1_CD3 | 2.5% |
| Tconv memDR_mem | 2.5% |
| nonTnonB_total | 2.5% |
| Tconv memCCR4_total | 2.5% |

**Total features selected by mRMR (Top 10%)_t60**: 38

#### mRMR (Top 10%)_t70

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD16mono_myeloid | 48.7% |
| Treg memory_CD4 | 23.1% |
| CD8 RO DR_CD8 | 20.5% |
| CD4 Tconv_total | 17.9% |
| CD8 RO DR_CD3 | 12.8% |
| CD4 Treg_CD4 | 12.8% |
| Tconv memDR_Tconv | 10.3% |
| CD14+16+mono_myeloid | 7.7% |
| Tconv naive_total | 7.7% |
| Tconv mem_Tconv | 7.7% |
| DR_CD8RO | 7.7% |
| Bcells CD27posIgDneg_total | 7.7% |
| CD16mono_CD3neg | 5.1% |
| CD3hi_total | 5.1% |
| CD3pos_total | 5.1% |
| Tconv memDR_CD3 | 5.1% |
| CD14mono_myeloid | 5.1% |
| Treg memory_CD3 | 5.1% |
| Tconv naive_CD3 | 5.1% |
| CD27IgD_Bcells | 5.1% |
| CD3neg_total | 2.6% |
| Tconv naive_Tconv | 2.6% |
| NKCD56hi_NK | 2.6% |
| CD8pos_CD3 | 2.6% |
| CD4 Tconv_CD3 | 2.6% |
| Tconv memDR_mem | 2.6% |
| Tconv memCCR4_total | 2.6% |

**Total features selected by mRMR (Top 10%)_t70**: 27

#### mRMR (Top 10%)_t80

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD16mono_myeloid | 44.4% |
| Treg memory_CD4 | 22.2% |
| CD8 RO DR_CD3 | 11.1% |
| CD4 Tconv_total | 11.1% |
| CD8 RO DR_CD8 | 7.4% |
| Tconv naive_CD3 | 7.4% |
| Tconv naive_total | 7.4% |
| Tconv memDR_Tconv | 7.4% |
| CD4 Treg_CD4 | 7.4% |
| Tconv mem_Tconv | 7.4% |
| CD27IgD_Bcells | 7.4% |
| Tconv naive_Tconv | 3.7% |
| CD3pos_total | 3.7% |
| CD3neg_total | 3.7% |
| Tconv memDR_CD3 | 3.7% |
| CD14+16+mono_myeloid | 3.7% |
| CD14mono_myeloid | 3.7% |
| Bcells CD27posIgDneg_total | 3.7% |
| DR_CD8RO | 3.7% |
| NKCD56hi_NK | 3.7% |
| Treg memory_CD3 | 3.7% |
| CD16mono_CD3neg | 3.7% |

**Total features selected by mRMR (Top 10%)_t80**: 22

## Overall Stable Features by Threshold

### Threshold 40%

`CD16mono_myeloid`, `Bcells CD27posIgDneg_total`

### Threshold 50%

No features met the 50% global stability threshold.

### Threshold 60%

No features met the 60% global stability threshold.

### Threshold 70%

No features met the 70% global stability threshold.

### Threshold 80%

No features met the 80% global stability threshold.


## Full Per-Method Feature Frequencies (All Bootstraps)

**IMPORTANT**: These tables show the raw feature selection frequencies for each method across all bootstrap runs. The stability threshold suffixes (_t40, _t50, etc.) indicate different filtering criteria applied to these same underlying frequencies:

- **Base Method** (e.g., `SVM_RBF_Permutation_Top10%`): Raw feature selection frequencies from bootstrap resampling
- **Threshold Variants** (e.g., `_t40`, `_t50`): Features filtered by stability threshold (≥40%, ≥50% selection frequency)

**Example**: `SVM_RBF_Permutation_Top10%_t40` keeps features selected in ≥40% of bootstrap samples, while `SVM_RBF_Permutation_Top10%_t50` keeps only features selected in ≥50% of bootstrap samples. This is why the same base method can produce different final feature sets.

---

### All Features (Baseline)

**Base Method**: Raw feature selection frequencies across all bootstrap samples

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD3pos_total | 100.0% |
| CD4 Tconv_total | 100.0% |
| CD4 Tconv mem_total | 100.0% |
| Tconv memCCR4_total | 100.0% |
| Tconv memCCR5_total | 100.0% |
| Tconv memCCR6_total | 100.0% |
| Tconv memCD27_total | 100.0% |
| Tconv memCD56_total | 100.0% |
| Tconv memCXCR3_total | 100.0% |
| Tconv memDR_total | 100.0% |
| Tconv memintB7_total | 100.0% |
| Tconv memKi67_total | 100.0% |
| Tconv memPD1_total | 100.0% |
| Tconv memTIGIT_total | 100.0% |
| Tconv naive_total | 100.0% |
| CD4 Treg_total | 100.0% |
| Treg naive_total | 100.0% |
| Treg memory_total | 100.0% |
| CD4neg_total | 100.0% |
| CD3hi_total | 100.0% |
| CD8pos_total | 100.0% |
| CD8 RA_total | 100.0% |
| CD8 RA naive_total | 100.0% |
| CD8 RO_total | 100.0% |
| CD8 RO CCR4_total | 100.0% |
| CD8 RO CCR5_total | 100.0% |
| CD8 RO CCR6_total | 100.0% |
| CD8 RO CD27_total | 100.0% |
| CD8 RO CD56_total | 100.0% |
| CD8 RO CXCR3_total | 100.0% |
| CD8 RO DR_total | 100.0% |
| CD8 RO intB7_total | 100.0% |
| CD8 RO Ki67_total | 100.0% |
| CD8 RO PD1_total | 100.0% |
| CD8 RO TIGIT_total | 100.0% |
| CD3neg_total | 100.0% |
| nonTnonB_total | 100.0% |
| NK_total | 100.0% |
| NKCD16_total | 100.0% |
| NKCD56hi_total | 100.0% |
| NK Ki67_total | 100.0% |
| myeloid_total | 100.0% |
| CD14mono_total | 100.0% |
| CD16+mono_total | 100.0% |
| CD14+16+mono_total | 100.0% |
| Bcells_total | 100.0% |
| Bcells CD27posIgDneg_total | 100.0% |
| Bcells CD27negIgDneg_total | 100.0% |
| Bcells Ki67_total | 100.0% |
| Bcells memory_total | 100.0% |
| Bcells naive_total | 100.0% |
| CD4 Tconv_CD3 | 100.0% |
| Tconv mem_CD3 | 100.0% |
| Tconv memCCR4_CD3 | 100.0% |
| Tconv memCCR5_CD3 | 100.0% |
| Tconv memCCR6_CD3 | 100.0% |
| Tconv memCD27_CD3 | 100.0% |
| Tconv memCD56_CD3 | 100.0% |
| Tconv memCXCR3_CD3 | 100.0% |
| Tconv memDR_CD3 | 100.0% |
| Tconv memintB7_CD3 | 100.0% |
| Tconv memKi67_CD3 | 100.0% |
| Tconv memPD1_CD3 | 100.0% |
| Tconv memTIGIT_CD3 | 100.0% |
| Tconv naive_CD3 | 100.0% |
| CD4 Treg _CD3 | 100.0% |
| Treg naive_CD3 | 100.0% |
| Treg memory_CD3 | 100.0% |
| CD4neg_CD3 | 100.0% |
| CD3hi_CD3 | 100.0% |
| CD8pos_CD3 | 100.0% |
| CD8 RA_CD3 | 100.0% |
| CD8 RA naive_CD3 | 100.0% |
| CD8 RO_CD3 | 100.0% |
| CD8 ncytotox RO CCR4_CD3 | 100.0% |
| CD8 RO CCR5_CD3 | 100.0% |
| CD8 RO CCR6_CD3 | 100.0% |
| CD8 RO CD27_CD3 | 100.0% |
| CD8 RO CD56_CD3 | 100.0% |
| CD8 RO CXCR3_CD3 | 100.0% |
| CD8 RO DR_CD3 | 100.0% |
| CD8 RO intB7_CD3 | 100.0% |
| CD8  RO Ki67_CD3 | 100.0% |
| CD8 RO PD1_CD3 | 100.0% |
| CD8 RO TIGIT_CD3 | 100.0% |
| CD4 Treg_CD4 | 100.0% |
| Treg naive_CD4 | 100.0% |
| Treg memory_CD4 | 100.0% |
| Tconv mem_Tconv | 100.0% |
| Tconv memCCR4_Tconv | 100.0% |
| Tconv memCCR5_Tconv | 100.0% |
| Tconv memCCR6_Tconv | 100.0% |
| Tconv memCD27_Tconv | 100.0% |
| Tconv memCD56_Tconv | 100.0% |
| Tconv memCXCR3_Tconv | 100.0% |
| Tconv memDR_Tconv | 100.0% |
| Tconv memintB7_Tconv | 100.0% |
| Tconv memKi67_Tconv | 100.0% |
| Tconv memPD1_Tconv | 100.0% |
| Tconv memTIGIT_Tconv | 100.0% |
| Tconv naive_Tconv | 100.0% |
| Tconv memCCR4_mem | 100.0% |
| Tconv memCCR5_mem | 100.0% |
| Tconv memCCR6_mem | 100.0% |
| Tconv memCD27_mem | 100.0% |
| Tconv memCD56_mem | 100.0% |
| Tconv memCXCR3_mem | 100.0% |
| Tconv memDR_mem | 100.0% |
| Tconv memintB7_mem | 100.0% |
| Tconv memKi67_mem | 100.0% |
| Tconv memPD1_mem | 100.0% |
| Tconv memTIGIT_mem | 100.0% |
| CD3hi_CD4neg | 100.0% |
| CD8 RA_CD8 | 100.0% |
| CD8 RA CCR7 naive_CD8 | 100.0% |
| CD8 RO_CD8 | 100.0% |
| CD8 ncytotox RO CCR4_CD8ntox | 100.0% |
| CD8 RO CCR5_CD8 | 100.0% |
| CD8 RO CCR6_CD8 | 100.0% |
| CD8 RO CD27_CD8 | 100.0% |
| CD8 RO CD56_CD8 | 100.0% |
| CD8 RO CXCR3_CD8 | 100.0% |
| CD8 RO DR_CD8 | 100.0% |
| CD8 RO intB7_CD8 | 100.0% |
| CD8 RO Ki67_CD8 | 100.0% |
| CD8 RO PD1_CD8 | 100.0% |
| CD8 RO TIGIT_CD8 | 100.0% |
| CCR4_CD8RO | 100.0% |
| CCR5_CD8RO | 100.0% |
| CCR6_CD8RO | 100.0% |
| CD27_CD8RO | 100.0% |
| CD56_CD8RO | 100.0% |
| CXCR3_CD8RO | 100.0% |
| DR_CD8RO | 100.0% |
| intB7_CD8RO | 100.0% |
| Ki67_CD8RO | 100.0% |
| PD1_CD8RO | 100.0% |
| TIGIT_CD8RO | 100.0% |
| nonTnonB_CD3neg | 100.0% |
| NK_CD3neg | 100.0% |
| NKCD16_CD3neg | 100.0% |
| NKCD56hi_CD3neg | 100.0% |
| NK Ki67_CD3neg | 100.0% |
| myeloid_CD3neg | 100.0% |
| CD14mono_CD3neg | 100.0% |
| CD16mono_CD3neg | 100.0% |
| CD14+16+mono_CD3neg | 100.0% |
| Bcells_CD3neg | 100.0% |
| Bcells Ki67_CD3neg | 100.0% |
| Bcells memory_CD3neg | 100.0% |
| Bcells naive_CD3neg | 100.0% |
| NK_nonTnonB | 100.0% |
| NKCD16_nonTnonB | 100.0% |
| NKCD56hi_nonTnonB | 100.0% |
| NK Ki67_nonTnonB | 100.0% |
| NKCD16_NK | 100.0% |
| NKCD56hi_NK | 100.0% |
| NK Ki67_NK | 100.0% |
| CD14mono_myeloid | 100.0% |
| CD16mono_myeloid | 100.0% |
| CD14+16+mono_myeloid | 100.0% |
| CD27IgD_Bcells | 100.0% |
| CD27negIgDneg_Bcells | 100.0% |
| Ki67_Bcells | 100.0% |
| memory_Bcells | 100.0% |
| naive_Bcells | 100.0% |

### ElasticNet_Lenient

**Base Method**: Raw feature selection frequencies across all bootstrap samples

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD16mono_myeloid | 63.7% |
| DR_CD8RO | 62.7% |
| CD8 RO DR_CD8 | 47.8% |
| NKCD56hi_total | 46.2% |
| Ki67_Bcells | 44.2% |
| CD14+16+mono_myeloid | 41.2% |
| CD27IgD_Bcells | 41.0% |
| CD3hi_total | 36.5% |
| Treg memory_CD3 | 29.0% |
| CD14mono_myeloid | 29.0% |
| Bcells CD27posIgDneg_total | 28.7% |
| CD16mono_CD3neg | 28.2% |
| CD8pos_CD3 | 28.2% |
| CD8 RO CD56_CD8 | 27.5% |
| Tconv memDR_CD3 | 26.8% |
| Tconv memDR_Tconv | 26.5% |
| Bcells memory_total | 26.2% |
| Tconv mem_Tconv | 24.8% |
| Tconv memKi67_mem | 24.2% |
| Tconv memPD1_mem | 24.2% |
| Bcells CD27negIgDneg_total | 24.2% |
| CD8 RA_CD3 | 24.0% |
| intB7_CD8RO | 22.8% |
| NKCD56hi_NK | 22.8% |
| memory_Bcells | 22.8% |
| NKCD16_NK | 22.5% |
| Tconv memDR_total | 21.8% |
| Tconv memTIGIT_mem | 21.8% |
| Tconv memCCR4_mem | 21.2% |
| CD8 RO CD56_CD3 | 21.2% |
| CD8 RO intB7_CD8 | 21.2% |
| Tconv memCCR5_mem | 21.0% |
| Tconv memCD56_total | 21.0% |
| CD8 RO PD1_CD3 | 20.5% |
| CD27negIgDneg_Bcells | 20.0% |
| Treg memory_CD4 | 19.2% |
| NK Ki67_total | 19.0% |
| Tconv memCCR6_total | 18.5% |
| Tconv memDR_mem | 18.2% |
| Tconv memintB7_Tconv | 18.0% |
| Tconv memCD27_Tconv | 17.8% |
| Tconv memCCR6_mem | 17.8% |
| CD8 RA CCR7 naive_CD8 | 17.8% |
| CCR4_CD8RO | 17.5% |
| CCR6_CD8RO | 17.5% |
| Tconv memKi67_total | 16.5% |
| CCR5_CD8RO | 16.2% |
| Bcells Ki67_total | 16.2% |
| CD4 Treg _CD3 | 16.0% |
| Tconv memintB7_mem | 15.8% |
| CD8 RO CXCR3_CD8 | 15.5% |
| Treg memory_total | 15.2% |
| NK Ki67_NK | 15.2% |
| Tconv memCCR5_total | 14.8% |
| CD8 RO intB7_total | 14.8% |
| CD8 RO DR_CD3 | 14.5% |
| CXCR3_CD8RO | 14.2% |
| CD8 RO TIGIT_CD3 | 14.0% |
| Treg naive_total | 13.8% |
| Tconv naive_CD3 | 13.5% |
| Bcells Ki67_CD3neg | 13.5% |
| Tconv memCXCR3_mem | 13.2% |
| CD3hi_CD4neg | 13.2% |
| Tconv memintB7_CD3 | 13.2% |
| Tconv naive_Tconv | 13.2% |
| Bcells naive_total | 13.2% |
| CD8 RO CXCR3_CD3 | 13.2% |
| CD4 Treg_CD4 | 13.0% |
| CD27_CD8RO | 13.0% |
| CD56_CD8RO | 12.8% |
| Tconv memCD27_mem | 12.5% |
| NKCD56hi_nonTnonB | 12.5% |
| CD4 Tconv_total | 12.5% |
| CD3hi_CD3 | 12.5% |
| Treg naive_CD4 | 12.2% |
| Tconv naive_total | 12.2% |
| NK_total | 12.0% |
| CD4neg_CD3 | 11.8% |
| Treg naive_CD3 | 11.0% |
| CD3pos_total | 11.0% |
| CD3neg_total | 10.8% |
| naive_Bcells | 10.8% |
| CD8 RA naive_total | 10.2% |
| CD4neg_total | 10.2% |
| Tconv memKi67_CD3 | 10.2% |
| CD8 RA_total | 10.0% |
| Tconv memCXCR3_total | 10.0% |
| NK Ki67_nonTnonB | 10.0% |
| CD8 RA naive_CD3 | 10.0% |
| Tconv memTIGIT_Tconv | 9.5% |
| CD8 RO Ki67_CD8 | 9.0% |
| CD16+mono_total | 8.2% |
| Tconv memCCR6_Tconv | 8.2% |
| Tconv memCCR6_CD3 | 8.2% |
| TIGIT_CD8RO | 8.2% |
| CD8 RO TIGIT_CD8 | 8.2% |
| CD8 RO CD27_CD3 | 8.2% |
| Tconv mem_CD3 | 8.0% |
| CD8 RO CCR5_total | 8.0% |
| CD8 RO CD56_total | 7.8% |
| Bcells_total | 7.2% |
| CD8 RO CCR6_CD8 | 7.0% |
| Tconv memCCR4_Tconv | 7.0% |
| CD8 RO PD1_total | 7.0% |
| Bcells naive_CD3neg | 6.8% |
| Tconv memCXCR3_CD3 | 6.5% |
| CD8 ncytotox RO CCR4_CD8ntox | 6.5% |
| CD4 Tconv_CD3 | 6.5% |
| NK Ki67_CD3neg | 6.5% |
| Tconv memCCR4_total | 6.2% |
| Tconv memCD56_CD3 | 6.2% |
| NKCD56hi_CD3neg | 6.2% |
| CD4 Treg_total | 6.0% |
| Ki67_CD8RO | 6.0% |
| CD8 RO PD1_CD8 | 6.0% |
| CD8 RO CCR4_total | 6.0% |
| PD1_CD8RO | 5.8% |
| CD14+16+mono_CD3neg | 5.8% |
| NKCD16_total | 5.5% |
| Tconv memPD1_total | 5.5% |
| CD8 RO CCR5_CD8 | 5.5% |
| CD14+16+mono_total | 5.2% |
| CD8 RO DR_total | 5.2% |
| CD8 RO CCR6_CD3 | 5.2% |
| Tconv memintB7_total | 5.0% |
| Tconv memCXCR3_Tconv | 4.8% |
| NKCD16_nonTnonB | 4.2% |
| CD8 RO CD27_CD8 | 4.2% |
| Bcells memory_CD3neg | 4.0% |
| NK_nonTnonB | 4.0% |
| NKCD16_CD3neg | 3.8% |
| CD8 RO CXCR3_total | 3.8% |
| CD8 RO Ki67_total | 3.8% |
| Tconv memCCR4_CD3 | 3.8% |
| Tconv memCD56_mem | 3.5% |
| Tconv memTIGIT_CD3 | 3.5% |
| Tconv memCD27_total | 3.5% |
| CD8 RO CD27_total | 3.5% |
| CD8 RO_CD3 | 3.5% |
| Tconv memCD56_Tconv | 3.5% |
| CD8 RO CCR6_total | 3.2% |
| Tconv memPD1_Tconv | 3.2% |
| CD8 ncytotox RO CCR4_CD3 | 3.2% |
| NK_CD3neg | 3.0% |
| Tconv memTIGIT_total | 2.8% |
| Bcells_CD3neg | 2.5% |
| CD14mono_CD3neg | 2.2% |
| Tconv memCD27_CD3 | 2.2% |
| Tconv memCCR5_CD3 | 2.0% |
| CD8 RO CCR5_CD3 | 2.0% |
| Tconv memPD1_CD3 | 2.0% |
| CD8  RO Ki67_CD3 | 1.8% |
| nonTnonB_CD3neg | 1.8% |
| nonTnonB_total | 1.8% |
| Tconv memKi67_Tconv | 1.8% |
| CD8 RA_CD8 | 1.8% |
| CD8 RO TIGIT_total | 1.2% |
| CD8 RO intB7_CD3 | 1.2% |
| CD8 RO_total | 1.2% |
| CD8pos_total | 1.2% |
| Tconv memCCR5_Tconv | 1.2% |
| CD4 Tconv mem_total | 1.2% |
| CD8 RO_CD8 | 1.0% |
| myeloid_CD3neg | 0.2% |

### ElasticNet_RFE

**Base Method**: Raw feature selection frequencies across all bootstrap samples

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD16mono_myeloid | 59.8% |
| DR_CD8RO | 53.2% |
| CD8 RO DR_CD8 | 42.0% |
| CD27IgD_Bcells | 39.8% |
| Ki67_Bcells | 35.8% |
| NKCD56hi_total | 34.5% |
| CD14+16+mono_myeloid | 30.5% |
| CD3hi_total | 29.8% |
| Bcells CD27posIgDneg_total | 28.0% |
| CD16mono_CD3neg | 27.0% |
| Treg memory_CD3 | 26.5% |
| CD8pos_CD3 | 25.8% |
| CD14mono_myeloid | 25.5% |
| Tconv memDR_CD3 | 24.0% |
| Tconv mem_Tconv | 23.5% |
| Tconv memDR_Tconv | 23.0% |
| Bcells memory_total | 20.8% |
| CD8 RO CD56_CD8 | 19.8% |
| intB7_CD8RO | 19.2% |
| NKCD56hi_NK | 18.8% |
| Treg memory_CD4 | 18.2% |
| CD8 RA_CD3 | 18.0% |
| Tconv memKi67_mem | 17.8% |
| CD8 RO PD1_CD3 | 17.5% |
| Tconv memPD1_mem | 17.5% |
| Bcells CD27negIgDneg_total | 17.5% |
| memory_Bcells | 16.8% |
| Tconv memDR_mem | 16.8% |
| Tconv memTIGIT_mem | 16.2% |
| NKCD16_NK | 16.2% |
| CD8 RO CD56_CD3 | 15.8% |
| CD8 RA CCR7 naive_CD8 | 15.8% |
| Tconv memCCR5_mem | 15.5% |
| Tconv memCD27_Tconv | 15.5% |
| CD27negIgDneg_Bcells | 15.2% |
| Tconv memCCR6_total | 15.0% |
| Tconv memCD56_total | 15.0% |
| Tconv memDR_total | 15.0% |
| Tconv memCCR4_mem | 14.8% |
| CD4 Treg _CD3 | 14.5% |
| CCR6_CD8RO | 14.0% |
| Tconv naive_CD3 | 13.2% |
| Tconv naive_Tconv | 13.2% |
| CD8 RO DR_CD3 | 13.2% |
| Tconv memCCR6_mem | 13.0% |
| CCR5_CD8RO | 13.0% |
| Tconv memintB7_Tconv | 12.8% |
| NK Ki67_total | 12.8% |
| Tconv memKi67_total | 12.5% |
| CD8 RO intB7_CD8 | 12.2% |
| CD4 Treg_CD4 | 12.0% |
| Tconv naive_total | 11.5% |
| CD8 RO TIGIT_CD3 | 11.5% |
| CCR4_CD8RO | 11.5% |
| Tconv memCCR5_total | 11.2% |
| Tconv memCXCR3_mem | 11.0% |
| CD4 Tconv_total | 11.0% |
| CD8 RO CXCR3_CD3 | 10.8% |
| Bcells Ki67_total | 10.8% |
| CD3pos_total | 10.2% |
| CD3hi_CD4neg | 10.0% |
| Bcells Ki67_CD3neg | 10.0% |
| CD4neg_CD3 | 10.0% |
| CXCR3_CD8RO | 10.0% |
| CD56_CD8RO | 10.0% |
| naive_Bcells | 10.0% |
| CD8 RO CXCR3_CD8 | 9.8% |
| Treg naive_total | 9.8% |
| CD3hi_CD3 | 9.8% |
| NK_total | 9.2% |
| CD27_CD8RO | 9.2% |
| NKCD56hi_nonTnonB | 9.2% |
| NK Ki67_NK | 9.0% |
| CD3neg_total | 9.0% |
| Bcells naive_total | 9.0% |
| CD8 RO intB7_total | 8.8% |
| Tconv memintB7_mem | 8.8% |
| Treg memory_total | 8.5% |
| Tconv memCD27_mem | 8.5% |
| CD8 RA_total | 8.2% |
| Tconv memTIGIT_Tconv | 7.8% |
| Treg naive_CD3 | 7.2% |
| Tconv memCXCR3_total | 7.2% |
| CD8 RA naive_total | 7.0% |
| CD4neg_total | 7.0% |
| Tconv mem_CD3 | 7.0% |
| CD8 RO CD27_CD3 | 6.8% |
| CD8 RO CCR5_total | 6.8% |
| Treg naive_CD4 | 6.5% |
| Tconv memKi67_CD3 | 6.5% |
| Tconv memCCR6_CD3 | 6.5% |
| CD8 RA naive_CD3 | 6.2% |
| Tconv memintB7_CD3 | 6.2% |
| NK Ki67_nonTnonB | 6.2% |
| CD8 RO Ki67_CD8 | 6.0% |
| CD16+mono_total | 6.0% |
| CD4 Tconv_CD3 | 5.8% |
| Tconv memCCR4_Tconv | 5.8% |
| CD8 RO TIGIT_CD8 | 5.8% |
| Tconv memCCR6_Tconv | 5.5% |
| Tconv memPD1_total | 5.5% |
| Tconv memCCR4_total | 5.5% |
| CD8 RO CCR4_total | 5.2% |
| CD8 RO CD56_total | 5.2% |
| CD8 RO PD1_total | 5.2% |
| CD4 Treg_total | 5.0% |
| Tconv memCXCR3_CD3 | 5.0% |
| Bcells_total | 5.0% |
| Ki67_CD8RO | 4.8% |
| Tconv memCD56_CD3 | 4.8% |
| CD14+16+mono_CD3neg | 4.5% |
| CD8 ncytotox RO CCR4_CD8ntox | 4.5% |
| Bcells naive_CD3neg | 4.5% |
| CD8 RO DR_total | 4.2% |
| CD8 RO CCR5_CD8 | 4.2% |
| CD8 RO CCR6_CD8 | 4.2% |
| Tconv memCXCR3_Tconv | 4.0% |
| NKCD56hi_CD3neg | 4.0% |
| Tconv memintB7_total | 4.0% |
| TIGIT_CD8RO | 3.8% |
| Bcells memory_CD3neg | 3.8% |
| NKCD16_total | 3.8% |
| Tconv memTIGIT_CD3 | 3.2% |
| CD8 RO_CD3 | 3.2% |
| CD14+16+mono_total | 3.0% |
| CD8 RO PD1_CD8 | 3.0% |
| CD8 RO CCR6_CD3 | 3.0% |
| NK Ki67_CD3neg | 3.0% |
| CD8 RO CXCR3_total | 3.0% |
| CD8 RO CD27_CD8 | 3.0% |
| NKCD16_nonTnonB | 2.8% |
| CD8 RO CCR6_total | 2.5% |
| CD8 RO CD27_total | 2.5% |
| Tconv memCD56_mem | 2.5% |
| NKCD16_CD3neg | 2.5% |
| NK_nonTnonB | 2.5% |
| CD8 ncytotox RO CCR4_CD3 | 2.2% |
| Bcells_CD3neg | 2.2% |
| Tconv memCD27_total | 2.2% |
| Tconv memCCR4_CD3 | 2.2% |
| Tconv memTIGIT_total | 2.2% |
| PD1_CD8RO | 2.0% |
| Tconv memPD1_Tconv | 2.0% |
| Tconv memCD27_CD3 | 2.0% |
| NK_CD3neg | 1.8% |
| nonTnonB_CD3neg | 1.8% |
| nonTnonB_total | 1.8% |
| CD8 RO CCR5_CD3 | 1.5% |
| Tconv memCD56_Tconv | 1.5% |
| Tconv memPD1_CD3 | 1.5% |
| CD14mono_CD3neg | 1.5% |
| CD8 RO TIGIT_total | 1.2% |
| CD8  RO Ki67_CD3 | 1.2% |
| CD8pos_total | 1.2% |
| CD8 RA_CD8 | 1.0% |
| CD8 RO_CD8 | 1.0% |
| CD8 RO Ki67_total | 1.0% |
| Tconv memKi67_Tconv | 1.0% |
| CD4 Tconv mem_total | 1.0% |
| Tconv memCCR5_CD3 | 1.0% |
| CD8 RO intB7_CD3 | 0.8% |
| CD8 RO_total | 0.5% |
| Tconv memCCR5_Tconv | 0.5% |
| myeloid_CD3neg | 0.2% |

### ElasticNet_Strict

**Base Method**: Raw feature selection frequencies across all bootstrap samples

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD16mono_myeloid | 41.5% |
| DR_CD8RO | 39.2% |
| CD8 RO DR_CD8 | 29.8% |
| NKCD56hi_total | 29.5% |
| CD27IgD_Bcells | 24.5% |
| CD14+16+mono_myeloid | 21.2% |
| CD3hi_total | 19.8% |
| Ki67_Bcells | 18.2% |
| CD16mono_CD3neg | 16.2% |
| CD14mono_myeloid | 15.2% |
| CD8 RO CD56_CD8 | 15.0% |
| Tconv memKi67_mem | 13.8% |
| Tconv memDR_Tconv | 13.2% |
| Bcells CD27posIgDneg_total | 12.2% |
| CD8pos_CD3 | 12.2% |
| CD8 RA_CD3 | 12.2% |
| Treg memory_CD3 | 11.5% |
| Tconv memDR_CD3 | 11.2% |
| Tconv mem_Tconv | 10.8% |
| Tconv memPD1_mem | 10.5% |
| Tconv memCCR5_mem | 10.2% |
| Tconv memDR_total | 10.2% |
| memory_Bcells | 9.8% |
| NKCD16_NK | 9.0% |
| CD8 RO PD1_CD3 | 9.0% |
| Bcells memory_total | 9.0% |
| CD8 RO intB7_CD8 | 8.8% |
| intB7_CD8RO | 8.8% |
| Bcells CD27negIgDneg_total | 8.5% |
| CD8 RO DR_CD3 | 8.0% |
| Tconv memCCR4_mem | 8.0% |
| Tconv memDR_mem | 7.8% |
| CD8 RO TIGIT_CD3 | 7.8% |
| NKCD56hi_NK | 7.8% |
| Tconv memKi67_total | 7.8% |
| CCR4_CD8RO | 7.5% |
| Tconv memTIGIT_mem | 7.5% |
| Tconv memCXCR3_mem | 7.0% |
| Tconv memintB7_Tconv | 7.0% |
| Tconv memCD27_Tconv | 6.8% |
| Tconv memCCR5_total | 6.5% |
| CD8 RA CCR7 naive_CD8 | 6.5% |
| CD8 RO intB7_total | 6.2% |
| Tconv naive_CD3 | 6.2% |
| Tconv memCCR6_total | 6.2% |
| CD8 RO CD56_CD3 | 6.0% |
| Tconv memCD56_total | 5.8% |
| CD3hi_CD3 | 5.8% |
| CCR5_CD8RO | 5.5% |
| Tconv memintB7_mem | 5.5% |
| Tconv memCCR6_mem | 5.5% |
| CD4 Tconv_total | 5.2% |
| Treg memory_total | 5.2% |
| CD8 RO CXCR3_CD3 | 5.2% |
| NKCD56hi_nonTnonB | 5.2% |
| NK Ki67_NK | 5.2% |
| Tconv memintB7_CD3 | 5.0% |
| CD8 RA_total | 5.0% |
| Bcells Ki67_CD3neg | 4.8% |
| Bcells Ki67_total | 4.8% |
| CD8 RO CCR5_total | 4.8% |
| CD4 Treg _CD3 | 4.8% |
| CD56_CD8RO | 4.5% |
| Tconv naive_total | 4.5% |
| CCR6_CD8RO | 4.5% |
| NK Ki67_total | 4.5% |
| Tconv memCD27_mem | 4.0% |
| Tconv memKi67_CD3 | 4.0% |
| CD27negIgDneg_Bcells | 4.0% |
| CD4 Treg_CD4 | 4.0% |
| CD3hi_CD4neg | 4.0% |
| Treg memory_CD4 | 3.8% |
| Treg naive_total | 3.8% |
| CD27_CD8RO | 3.8% |
| CD4neg_CD3 | 3.8% |
| Tconv naive_Tconv | 3.8% |
| CXCR3_CD8RO | 3.8% |
| CD8 RO Ki67_CD8 | 3.5% |
| Bcells naive_total | 3.5% |
| CD8 RO CXCR3_CD8 | 3.5% |
| Tconv memCXCR3_total | 3.2% |
| CD8 RO TIGIT_CD8 | 3.2% |
| CD8 RA naive_CD3 | 3.0% |
| TIGIT_CD8RO | 3.0% |
| CD8 RO CD27_CD3 | 3.0% |
| Tconv mem_CD3 | 3.0% |
| naive_Bcells | 2.8% |
| Tconv memCXCR3_CD3 | 2.8% |
| Treg naive_CD3 | 2.5% |
| CD8 RO PD1_total | 2.5% |
| CD8 ncytotox RO CCR4_CD8ntox | 2.2% |
| CD8 RA naive_total | 2.2% |
| Bcells_total | 2.2% |
| Treg naive_CD4 | 2.2% |
| CD14+16+mono_total | 2.2% |
| CD4neg_total | 2.2% |
| CD3neg_total | 2.2% |
| Tconv memCCR4_total | 2.2% |
| CD3pos_total | 2.2% |
| CD8 RO CCR6_CD3 | 2.0% |
| Tconv memPD1_total | 2.0% |
| Bcells naive_CD3neg | 2.0% |
| CD4 Tconv_CD3 | 2.0% |
| NKCD56hi_CD3neg | 2.0% |
| CD8 RO CD56_total | 2.0% |
| NK Ki67_nonTnonB | 1.8% |
| CD8 RO PD1_CD8 | 1.8% |
| CD8 RO DR_total | 1.8% |
| CD16+mono_total | 1.8% |
| Tconv memCXCR3_Tconv | 1.8% |
| Tconv memCCR4_Tconv | 1.8% |
| Tconv memCCR6_CD3 | 1.8% |
| CD14+16+mono_CD3neg | 1.5% |
| Bcells memory_CD3neg | 1.5% |
| Tconv memCCR6_Tconv | 1.2% |
| CD8 RO Ki67_total | 1.2% |
| Ki67_CD8RO | 1.2% |
| CD8 RO CCR5_CD8 | 1.2% |
| CD8 RO CCR4_total | 1.2% |
| Tconv memCD56_mem | 1.2% |
| CD4 Treg_total | 1.2% |
| PD1_CD8RO | 1.2% |
| Tconv memTIGIT_Tconv | 1.2% |
| NK Ki67_CD3neg | 1.0% |
| CD8 RO CD27_CD8 | 1.0% |
| Tconv memCD56_CD3 | 1.0% |
| Tconv memPD1_Tconv | 1.0% |
| CD8 RO_CD3 | 1.0% |
| CD8 RO CCR6_CD8 | 1.0% |
| CD8 RO CCR5_CD3 | 0.8% |
| NK_total | 0.8% |
| Tconv memintB7_total | 0.8% |
| nonTnonB_total | 0.8% |
| CD8 RO CCR6_total | 0.8% |
| CD8 ncytotox RO CCR4_CD3 | 0.8% |
| CD8 RO CXCR3_total | 0.8% |
| Tconv memKi67_Tconv | 0.5% |
| CD8 RO CD27_total | 0.5% |
| CD8 RO intB7_CD3 | 0.5% |
| Tconv memCCR4_CD3 | 0.5% |
| Tconv memPD1_CD3 | 0.5% |
| Tconv memCCR5_Tconv | 0.5% |
| CD14mono_CD3neg | 0.5% |
| Tconv memCCR5_CD3 | 0.5% |
| CD8 RO_CD8 | 0.2% |
| Tconv memCD27_total | 0.2% |
| Tconv memCD27_CD3 | 0.2% |
| Tconv memCD56_Tconv | 0.2% |
| NKCD16_total | 0.2% |
| NKCD16_CD3neg | 0.2% |
| CD8 RO TIGIT_total | 0.2% |
| NKCD16_nonTnonB | 0.2% |
| myeloid_CD3neg | 0.2% |
| CD4 Tconv mem_total | 0.2% |
| NK_nonTnonB | 0.2% |
| Tconv memTIGIT_CD3 | 0.2% |

### FDR (p < 0.01)

**Base Method**: Raw feature selection frequencies across all bootstrap samples

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Bcells CD27posIgDneg_total | 48.0% |
| Tconv naive_total | 36.2% |
| CD8 RO DR_CD3 | 31.8% |
| Treg memory_CD4 | 31.2% |
| CD4 Treg_CD4 | 29.5% |
| CD4 Tconv_total | 25.8% |
| CD16mono_myeloid | 23.8% |
| Tconv naive_CD3 | 23.0% |
| Tconv memDR_Tconv | 21.5% |
| Tconv mem_Tconv | 20.5% |
| Tconv naive_Tconv | 19.5% |
| CD3neg_total | 18.8% |
| CD3pos_total | 18.8% |
| Tconv memDR_CD3 | 17.2% |
| CD27IgD_Bcells | 17.0% |
| Treg memory_CD3 | 14.2% |
| Tconv memCD27_Tconv | 13.5% |
| nonTnonB_total | 13.0% |
| CD4 Tconv_CD3 | 11.5% |
| CD14mono_total | 11.5% |
| Bcells memory_CD3neg | 11.2% |
| CD16mono_CD3neg | 10.5% |
| CD4 Treg _CD3 | 10.5% |
| nonTnonB_CD3neg | 10.5% |
| Bcells_CD3neg | 10.5% |
| CD8pos_CD3 | 10.2% |
| CD8 RO DR_CD8 | 10.0% |
| CD14mono_myeloid | 9.8% |
| CD8 RO CD56_CD3 | 7.5% |
| CD8 RO_CD3 | 7.5% |
| Tconv memCCR4_Tconv | 7.2% |
| Tconv memDR_mem | 7.0% |
| Bcells memory_total | 6.8% |
| CD4neg_CD3 | 6.5% |
| Tconv memCXCR3_Tconv | 6.5% |
| CD14+16+mono_total | 6.5% |
| CD8 RO PD1_CD3 | 6.2% |
| CD8  RO Ki67_CD3 | 6.2% |
| CD14mono_CD3neg | 6.0% |
| Tconv memCCR4_total | 6.0% |
| CD8 RO CXCR3_CD3 | 5.8% |
| Tconv mem_CD3 | 5.5% |
| myeloid_total | 5.2% |
| CD4 Tconv mem_total | 4.2% |
| Bcells naive_CD3neg | 4.2% |
| Tconv memCD27_total | 4.0% |
| CD8 RO CD27_CD3 | 4.0% |
| Treg naive_total | 4.0% |
| Tconv memTIGIT_Tconv | 4.0% |
| Tconv memPD1_total | 4.0% |
| CD8 RO TIGIT_CD3 | 4.0% |
| Ki67_Bcells | 3.8% |
| CD8 RA CCR7 naive_CD8 | 3.5% |
| Tconv memCXCR3_CD3 | 3.5% |
| DR_CD8RO | 3.2% |
| CD8 RO DR_total | 3.0% |
| CD14+16+mono_myeloid | 3.0% |
| CD8 RA naive_total | 3.0% |
| Bcells_total | 3.0% |
| Tconv memCCR6_Tconv | 2.8% |
| CD8 RO CD56_CD8 | 2.8% |
| Tconv memCD27_CD3 | 2.8% |
| Tconv memPD1_Tconv | 2.5% |
| Tconv memCCR6_total | 2.5% |
| CD14+16+mono_CD3neg | 2.5% |
| Tconv memintB7_Tconv | 2.5% |
| Bcells naive_total | 2.2% |
| CD8 RA_CD3 | 2.2% |
| Tconv memKi67_Tconv | 2.2% |
| Tconv memCD56_Tconv | 2.0% |
| CD8 RO intB7_CD3 | 2.0% |
| CD8 RO CCR5_CD3 | 2.0% |
| myeloid_CD3neg | 2.0% |
| CD8 RO CXCR3_total | 1.8% |
| CD3hi_CD3 | 1.8% |
| Tconv memTIGIT_total | 1.8% |
| CD16+mono_total | 1.8% |
| Tconv memKi67_total | 1.8% |
| Tconv memintB7_total | 1.8% |
| CD8pos_total | 1.5% |
| Tconv memCCR5_total | 1.5% |
| Tconv memCCR4_CD3 | 1.5% |
| CD8 RO CCR5_total | 1.5% |
| CD8 RO CD56_total | 1.5% |
| Tconv memTIGIT_CD3 | 1.5% |
| NK_nonTnonB | 1.5% |
| Tconv memCCR6_CD3 | 1.5% |
| Tconv memDR_total | 1.5% |
| CD8 RO CXCR3_CD8 | 1.5% |
| NKCD16_nonTnonB | 1.2% |
| CD8 RO intB7_total | 1.2% |
| Tconv memCCR5_Tconv | 1.2% |
| CD3hi_total | 1.2% |
| CD8 ncytotox RO CCR4_CD3 | 1.2% |
| Tconv memCCR5_CD3 | 1.2% |
| CD8 RO_total | 1.2% |
| Tconv memKi67_CD3 | 1.2% |
| CD8 RO CCR6_CD3 | 1.0% |
| CD8 RO CCR6_total | 1.0% |
| Tconv memCD27_mem | 1.0% |
| CD8 RA_total | 1.0% |
| NKCD56hi_total | 1.0% |
| CD8 RO Ki67_CD8 | 1.0% |
| Tconv memCXCR3_mem | 1.0% |
| Tconv memintB7_CD3 | 0.8% |
| Bcells Ki67_CD3neg | 0.8% |
| NKCD16_NK | 0.8% |
| NKCD56hi_nonTnonB | 0.8% |
| NKCD16_CD3neg | 0.8% |
| CCR6_CD8RO | 0.8% |
| intB7_CD8RO | 0.8% |
| CD56_CD8RO | 0.8% |
| CCR4_CD8RO | 0.8% |
| CD8 RO CD27_total | 0.8% |
| CD8 RO TIGIT_total | 0.8% |
| NK_CD3neg | 0.8% |
| CCR5_CD8RO | 0.8% |
| NKCD56hi_NK | 0.8% |
| CXCR3_CD8RO | 0.8% |
| Tconv memKi67_mem | 0.8% |
| Tconv memCD56_CD3 | 0.8% |
| NK Ki67_NK | 0.5% |
| CD8 RO CCR5_CD8 | 0.5% |
| CD8 RO CCR6_CD8 | 0.5% |
| Tconv memCXCR3_total | 0.5% |
| CD8 RO CCR4_total | 0.5% |
| Ki67_CD8RO | 0.5% |
| Tconv memCCR5_mem | 0.5% |
| Bcells CD27negIgDneg_total | 0.5% |
| NKCD56hi_CD3neg | 0.5% |
| CD8 RO CD27_CD8 | 0.5% |
| Treg naive_CD4 | 0.5% |
| CD4 Treg_total | 0.5% |
| CD8 RA_CD8 | 0.5% |
| Tconv memCD56_total | 0.5% |
| Tconv memPD1_CD3 | 0.5% |
| Tconv memCD56_mem | 0.5% |
| Tconv memPD1_mem | 0.5% |
| CD8 RA naive_CD3 | 0.2% |
| Tconv memintB7_mem | 0.2% |
| NK Ki67_nonTnonB | 0.2% |
| CD4neg_total | 0.2% |
| CD8 RO intB7_CD8 | 0.2% |
| NKCD16_total | 0.2% |
| Treg memory_total | 0.2% |
| naive_Bcells | 0.2% |
| memory_Bcells | 0.2% |
| NK_total | 0.2% |
| Treg naive_CD3 | 0.2% |
| CD3hi_CD4neg | 0.2% |
| CD8 ncytotox RO CCR4_CD8ntox | 0.2% |
| CD27_CD8RO | 0.2% |
| Tconv memCCR6_mem | 0.2% |
| CD8 RO Ki67_total | 0.2% |
| CD8 RO PD1_total | 0.2% |
| CD8 RO PD1_CD8 | 0.2% |
| CD27negIgDneg_Bcells | 0.2% |

### FDR (p < 0.05)

**Base Method**: Raw feature selection frequencies across all bootstrap samples

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Bcells CD27posIgDneg_total | 71.5% |
| Tconv naive_total | 62.5% |
| CD8 RO DR_CD3 | 59.0% |
| Treg memory_CD4 | 56.5% |
| CD4 Treg_CD4 | 54.2% |
| CD4 Tconv_total | 47.8% |
| Tconv memDR_Tconv | 46.5% |
| Tconv naive_CD3 | 46.2% |
| Tconv mem_Tconv | 43.8% |
| Tconv naive_Tconv | 42.8% |
| CD16mono_myeloid | 42.0% |
| CD3neg_total | 41.5% |
| CD3pos_total | 41.5% |
| CD27IgD_Bcells | 40.5% |
| Tconv memDR_CD3 | 36.8% |
| Treg memory_CD3 | 34.8% |
| nonTnonB_total | 34.0% |
| Bcells memory_CD3neg | 29.8% |
| CD8 RO DR_CD8 | 27.8% |
| CD8pos_CD3 | 27.5% |
| nonTnonB_CD3neg | 27.0% |
| Tconv memCD27_Tconv | 26.8% |
| Bcells_CD3neg | 26.8% |
| CD16mono_CD3neg | 26.2% |
| CD4 Treg _CD3 | 26.2% |
| CD4 Tconv_CD3 | 25.8% |
| CD14mono_total | 24.2% |
| CD8 RO CD56_CD3 | 23.8% |
| CD14mono_myeloid | 23.8% |
| Tconv memDR_mem | 21.8% |
| CD8  RO Ki67_CD3 | 20.8% |
| Bcells memory_total | 20.2% |
| Tconv memCCR4_Tconv | 20.0% |
| Bcells naive_CD3neg | 19.8% |
| CD14+16+mono_total | 19.5% |
| CD4neg_CD3 | 18.2% |
| CD14mono_CD3neg | 18.0% |
| CD8 RO_CD3 | 17.5% |
| CD8 RO PD1_CD3 | 16.8% |
| myeloid_total | 16.8% |
| Treg naive_total | 15.0% |
| CD8 RO TIGIT_CD3 | 14.8% |
| Tconv memCXCR3_Tconv | 14.5% |
| CD8 RO DR_total | 14.0% |
| CD8 RO CXCR3_CD3 | 13.5% |
| Tconv mem_CD3 | 13.2% |
| Ki67_Bcells | 13.2% |
| CD8 RO CD27_CD3 | 13.2% |
| Bcells_total | 13.2% |
| DR_CD8RO | 13.0% |
| CD14+16+mono_myeloid | 12.2% |
| Tconv memPD1_total | 12.2% |
| Tconv memCCR4_total | 12.0% |
| CD8 RA CCR7 naive_CD8 | 11.5% |
| Tconv memKi67_Tconv | 11.2% |
| CD8 RO CCR5_CD3 | 11.0% |
| Tconv memCD27_total | 11.0% |
| Tconv memTIGIT_Tconv | 10.5% |
| Tconv memintB7_Tconv | 10.2% |
| Tconv memCXCR3_CD3 | 10.0% |
| CD8 RA naive_total | 9.8% |
| CD4 Tconv mem_total | 9.5% |
| CD8 RO CD56_CD8 | 9.5% |
| CD14+16+mono_CD3neg | 9.5% |
| Tconv memCCR6_Tconv | 9.2% |
| Tconv memintB7_total | 8.8% |
| Tconv memCCR6_total | 8.2% |
| Tconv memCD56_Tconv | 8.0% |
| Tconv memPD1_Tconv | 7.8% |
| Tconv memCD27_CD3 | 7.5% |
| CD8 RO CCR6_CD3 | 7.2% |
| myeloid_CD3neg | 6.8% |
| Tconv memCXCR3_mem | 6.5% |
| Tconv memKi67_total | 6.5% |
| CD8 RO CXCR3_CD8 | 6.5% |
| Bcells naive_total | 6.2% |
| NK_nonTnonB | 6.0% |
| Tconv memCCR5_Tconv | 6.0% |
| Tconv memTIGIT_CD3 | 5.8% |
| CD8 RA_CD3 | 5.8% |
| CD16+mono_total | 5.8% |
| CD8 RO CCR5_total | 5.5% |
| NKCD16_nonTnonB | 5.5% |
| CD8 RO intB7_CD3 | 5.5% |
| Tconv memCCR4_CD3 | 5.2% |
| NKCD16_NK | 5.2% |
| Bcells Ki67_CD3neg | 5.0% |
| Tconv memTIGIT_total | 5.0% |
| CD8 RO CCR5_CD8 | 5.0% |
| CD8 RO CD56_total | 5.0% |
| NKCD56hi_NK | 5.0% |
| CD8 RO CXCR3_total | 4.8% |
| CD8 RO CCR6_total | 4.8% |
| Tconv memCCR6_CD3 | 4.8% |
| NKCD56hi_total | 4.8% |
| Tconv memCD27_mem | 4.8% |
| Tconv memKi67_CD3 | 4.8% |
| CD8 RO intB7_total | 4.5% |
| CD8 RA_total | 4.5% |
| Tconv memCCR5_total | 4.5% |
| CD56_CD8RO | 4.5% |
| CD8 RO Ki67_CD8 | 4.5% |
| CD8 ncytotox RO CCR4_CD3 | 4.5% |
| Tconv memPD1_CD3 | 4.2% |
| CD3hi_CD3 | 4.2% |
| intB7_CD8RO | 4.0% |
| CD27negIgDneg_Bcells | 4.0% |
| CD8pos_total | 4.0% |
| Ki67_CD8RO | 4.0% |
| CD8 RA_CD8 | 4.0% |
| Bcells CD27negIgDneg_total | 4.0% |
| Tconv memCD56_CD3 | 4.0% |
| Tconv memCXCR3_total | 3.8% |
| Tconv memDR_total | 3.8% |
| CXCR3_CD8RO | 3.5% |
| Tconv memCCR4_mem | 3.5% |
| CD3hi_total | 3.5% |
| NKCD16_CD3neg | 3.5% |
| NK_CD3neg | 3.2% |
| CD3hi_CD4neg | 3.2% |
| CD8 RO_CD8 | 3.2% |
| Tconv memCCR5_mem | 3.2% |
| Tconv memCCR5_CD3 | 3.0% |
| Tconv memintB7_mem | 3.0% |
| naive_Bcells | 3.0% |
| CD8 RO PD1_total | 3.0% |
| NK Ki67_nonTnonB | 3.0% |
| CD8 RO PD1_CD8 | 3.0% |
| Tconv memPD1_mem | 3.0% |
| NKCD56hi_nonTnonB | 3.0% |
| CD27_CD8RO | 2.8% |
| NKCD56hi_CD3neg | 2.8% |
| Tconv memKi67_mem | 2.8% |
| CD8 RO TIGIT_CD8 | 2.8% |
| CCR5_CD8RO | 2.8% |
| CD8 RO_total | 2.8% |
| NK Ki67_CD3neg | 2.5% |
| Tconv memintB7_CD3 | 2.5% |
| CD8 ncytotox RO CCR4_CD8ntox | 2.5% |
| Treg memory_total | 2.5% |
| CCR6_CD8RO | 2.5% |
| CD4 Treg_total | 2.5% |
| CD8 RO intB7_CD8 | 2.2% |
| CD8 RO CCR4_total | 2.2% |
| CD8 RA naive_CD3 | 2.0% |
| Tconv memCD56_mem | 2.0% |
| CD8 RO CCR6_CD8 | 2.0% |
| Tconv memCD56_total | 2.0% |
| Treg naive_CD3 | 2.0% |
| Treg naive_CD4 | 2.0% |
| CD8 RO CD27_CD8 | 2.0% |
| CD8 RO CD27_total | 2.0% |
| CCR4_CD8RO | 2.0% |
| CD8 RO TIGIT_total | 1.8% |
| NKCD16_total | 1.8% |
| CD8 RO Ki67_total | 1.8% |
| TIGIT_CD8RO | 1.8% |
| CD4neg_total | 1.8% |
| memory_Bcells | 1.8% |
| NK_total | 1.8% |
| NK Ki67_NK | 1.5% |
| Tconv memCCR6_mem | 1.5% |
| Tconv memTIGIT_mem | 1.2% |
| NK Ki67_total | 1.2% |
| PD1_CD8RO | 1.2% |
| Bcells Ki67_total | 1.0% |

### FDR (p < 0.1)

**Base Method**: Raw feature selection frequencies across all bootstrap samples

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Bcells CD27posIgDneg_total | 81.2% |
| Tconv naive_total | 74.8% |
| CD8 RO DR_CD3 | 70.2% |
| Treg memory_CD4 | 66.8% |
| CD4 Treg_CD4 | 65.2% |
| CD4 Tconv_total | 59.8% |
| Tconv naive_CD3 | 58.5% |
| Tconv memDR_Tconv | 57.5% |
| CD27IgD_Bcells | 55.8% |
| Tconv mem_Tconv | 54.5% |
| Tconv naive_Tconv | 53.5% |
| CD16mono_myeloid | 53.0% |
| CD3neg_total | 51.5% |
| CD3pos_total | 51.5% |
| Tconv memDR_CD3 | 48.5% |
| Treg memory_CD3 | 47.0% |
| nonTnonB_total | 44.8% |
| CD8 RO DR_CD8 | 42.5% |
| CD4 Treg _CD3 | 39.2% |
| Bcells memory_CD3neg | 39.2% |
| Tconv memCD27_Tconv | 37.5% |
| CD8pos_CD3 | 37.0% |
| CD16mono_CD3neg | 36.8% |
| Bcells_CD3neg | 36.5% |
| nonTnonB_CD3neg | 36.5% |
| CD14mono_total | 35.8% |
| CD4 Tconv_CD3 | 35.2% |
| CD8 RO CD56_CD3 | 32.8% |
| Tconv memDR_mem | 32.5% |
| CD14mono_myeloid | 32.0% |
| CD8  RO Ki67_CD3 | 30.8% |
| Tconv memCCR4_Tconv | 30.2% |
| CD4neg_CD3 | 29.5% |
| Bcells naive_CD3neg | 29.5% |
| CD14+16+mono_total | 28.2% |
| Bcells memory_total | 28.2% |
| CD8 RO_CD3 | 26.0% |
| myeloid_total | 25.2% |
| CD8 RO PD1_CD3 | 25.2% |
| CD14mono_CD3neg | 24.5% |
| CD8 RO DR_total | 23.8% |
| DR_CD8RO | 22.8% |
| Tconv memCXCR3_Tconv | 22.8% |
| Tconv mem_CD3 | 22.5% |
| Bcells_total | 22.5% |
| CD8 RO TIGIT_CD3 | 22.0% |
| Ki67_Bcells | 21.0% |
| CD8 RO CD27_CD3 | 20.8% |
| Treg naive_total | 20.2% |
| Tconv memPD1_total | 19.5% |
| CD8 RA CCR7 naive_CD8 | 19.0% |
| CD14+16+mono_myeloid | 18.2% |
| CD8 RO CXCR3_CD3 | 18.0% |
| Tconv memCCR4_total | 17.5% |
| Tconv memKi67_Tconv | 17.2% |
| Tconv memCD27_total | 17.2% |
| CD8 RO CD56_CD8 | 16.2% |
| CD14+16+mono_CD3neg | 16.2% |
| CD8 RO CCR5_CD3 | 16.0% |
| CD8 RA naive_total | 16.0% |
| Tconv memCXCR3_CD3 | 15.8% |
| Tconv memintB7_Tconv | 15.5% |
| Tconv memCD56_Tconv | 15.5% |
| Tconv memCCR6_Tconv | 15.2% |
| Tconv memPD1_Tconv | 14.5% |
| Tconv memintB7_total | 14.5% |
| Tconv memTIGIT_Tconv | 14.2% |
| CD4 Tconv mem_total | 14.2% |
| CD8 RO CCR6_CD3 | 13.8% |
| Tconv memCCR6_total | 13.2% |
| Bcells naive_total | 13.0% |
| Tconv memTIGIT_total | 12.5% |
| myeloid_CD3neg | 12.5% |
| Tconv memCD27_CD3 | 12.2% |
| Tconv memKi67_total | 11.2% |
| CD8 ncytotox RO CCR4_CD3 | 10.8% |
| NKCD16_nonTnonB | 10.2% |
| NK_nonTnonB | 10.2% |
| CD16+mono_total | 10.2% |
| Tconv memCXCR3_mem | 10.2% |
| Tconv memCCR5_Tconv | 10.2% |
| CD8 RA_total | 10.0% |
| CD8 RO intB7_CD3 | 10.0% |
| Tconv memCCR4_CD3 | 10.0% |
| Tconv memCD27_mem | 9.8% |
| CD8 RO CXCR3_CD8 | 9.8% |
| Bcells Ki67_CD3neg | 9.5% |
| Tconv memCD56_CD3 | 9.2% |
| CD8 RO Ki67_CD8 | 9.2% |
| CD8 RA_CD8 | 9.0% |
| NKCD56hi_NK | 9.0% |
| NKCD16_NK | 8.8% |
| CD8 RO CCR5_total | 8.5% |
| NKCD56hi_total | 8.5% |
| CD8 RO CD56_total | 8.5% |
| Tconv memintB7_mem | 8.5% |
| CD56_CD8RO | 8.5% |
| CD27negIgDneg_Bcells | 8.2% |
| CD8 RO CXCR3_total | 8.2% |
| CD8 RO CCR5_CD8 | 8.2% |
| Tconv memKi67_CD3 | 8.0% |
| CD3hi_CD3 | 8.0% |
| Tconv memCCR5_CD3 | 8.0% |
| CD8 RA_CD3 | 8.0% |
| Bcells CD27negIgDneg_total | 8.0% |
| Tconv memCXCR3_total | 7.8% |
| NKCD16_CD3neg | 7.8% |
| Tconv memCCR5_total | 7.8% |
| intB7_CD8RO | 7.5% |
| CD8 RO intB7_total | 7.5% |
| Tconv memDR_total | 7.5% |
| Tconv memTIGIT_CD3 | 7.5% |
| Tconv memCCR6_CD3 | 7.5% |
| Tconv memPD1_mem | 7.5% |
| CXCR3_CD8RO | 7.5% |
| CD8 RO_CD8 | 7.2% |
| Tconv memPD1_CD3 | 7.2% |
| CD8 RO CCR6_total | 7.0% |
| NK_CD3neg | 7.0% |
| Tconv memintB7_CD3 | 6.8% |
| CD3hi_total | 6.5% |
| Tconv memCCR4_mem | 6.5% |
| Ki67_CD8RO | 6.5% |
| CD8 RO CD27_total | 6.2% |
| Treg naive_CD3 | 6.2% |
| CD8pos_total | 6.2% |
| CD8 RO TIGIT_CD8 | 6.0% |
| CD8 RO_total | 6.0% |
| CD3hi_CD4neg | 6.0% |
| CD8 RO PD1_total | 5.8% |
| Treg naive_CD4 | 5.8% |
| Tconv memCCR5_mem | 5.8% |
| CD8 RO TIGIT_total | 5.8% |
| NK Ki67_nonTnonB | 5.8% |
| NKCD56hi_nonTnonB | 5.5% |
| Tconv memCD56_mem | 5.2% |
| Treg memory_total | 5.2% |
| CCR5_CD8RO | 5.2% |
| Tconv memKi67_mem | 5.2% |
| CD8 RO PD1_CD8 | 5.0% |
| CCR4_CD8RO | 5.0% |
| CD27_CD8RO | 5.0% |
| CD4 Treg_total | 5.0% |
| CD8 RO CD27_CD8 | 4.8% |
| memory_Bcells | 4.8% |
| naive_Bcells | 4.8% |
| NK Ki67_NK | 4.8% |
| NKCD56hi_CD3neg | 4.5% |
| CCR6_CD8RO | 4.5% |
| CD4neg_total | 4.5% |
| CD8 RO CCR4_total | 4.2% |
| CD8 RO Ki67_total | 4.2% |
| NK Ki67_total | 4.2% |
| CD8 RO intB7_CD8 | 4.0% |
| NKCD16_total | 4.0% |
| NK_total | 4.0% |
| NK Ki67_CD3neg | 4.0% |
| CD8 RO CCR6_CD8 | 3.8% |
| TIGIT_CD8RO | 3.8% |
| Tconv memCCR6_mem | 3.5% |
| CD8 RA naive_CD3 | 3.5% |
| PD1_CD8RO | 3.5% |
| Tconv memCD56_total | 3.5% |
| Bcells Ki67_total | 3.0% |
| Tconv memTIGIT_mem | 3.0% |
| CD8 ncytotox RO CCR4_CD8ntox | 3.0% |

### LASSO_Lenient

**Base Method**: Raw feature selection frequencies across all bootstrap samples

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD16mono_myeloid | 58.8% |
| DR_CD8RO | 52.0% |
| NKCD56hi_total | 42.0% |
| Ki67_Bcells | 40.0% |
| CD8 RO DR_CD8 | 38.8% |
| CD27IgD_Bcells | 36.8% |
| CD14+16+mono_myeloid | 36.2% |
| CD3hi_total | 30.2% |
| CD14mono_myeloid | 26.8% |
| CD8 RO CD56_CD8 | 26.5% |
| Bcells CD27posIgDneg_total | 25.2% |
| CD16mono_CD3neg | 23.8% |
| Bcells memory_total | 23.5% |
| CD8pos_CD3 | 23.5% |
| Treg memory_CD3 | 22.8% |
| Tconv memKi67_mem | 22.0% |
| memory_Bcells | 21.2% |
| Tconv memPD1_mem | 21.0% |
| Tconv memDR_CD3 | 20.8% |
| Bcells CD27negIgDneg_total | 20.2% |
| intB7_CD8RO | 20.2% |
| CD8 RA_CD3 | 19.8% |
| Tconv memDR_Tconv | 19.0% |
| Tconv memDR_total | 18.5% |
| Tconv memCD56_total | 18.2% |
| Tconv memCCR5_mem | 18.0% |
| Tconv memTIGIT_mem | 18.0% |
| Tconv memCCR4_mem | 18.0% |
| CD8 RO CD56_CD3 | 17.8% |
| NKCD16_NK | 17.2% |
| CD8 RO PD1_CD3 | 17.0% |
| NKCD56hi_NK | 17.0% |
| CD8 RO intB7_CD8 | 16.8% |
| Tconv memCCR6_mem | 16.2% |
| Tconv mem_Tconv | 15.8% |
| NK Ki67_total | 15.5% |
| CD27negIgDneg_Bcells | 15.5% |
| CCR5_CD8RO | 15.2% |
| Tconv memDR_mem | 15.2% |
| Bcells Ki67_total | 15.0% |
| Tconv memCD27_Tconv | 15.0% |
| CCR4_CD8RO | 14.8% |
| Tconv memintB7_Tconv | 14.5% |
| Tconv memCCR6_total | 14.2% |
| CCR6_CD8RO | 14.0% |
| CD8 RA CCR7 naive_CD8 | 14.0% |
| NK Ki67_NK | 13.8% |
| Tconv memKi67_total | 13.5% |
| Treg memory_total | 13.5% |
| CD8 RO intB7_total | 12.2% |
| CD3hi_CD4neg | 12.0% |
| Bcells naive_total | 12.0% |
| Tconv memintB7_mem | 11.8% |
| CD8 RO CXCR3_CD8 | 11.8% |
| Tconv memCXCR3_mem | 11.5% |
| Treg naive_total | 11.5% |
| Treg memory_CD4 | 11.2% |
| CD8 RO DR_CD3 | 11.2% |
| CD8 RO TIGIT_CD3 | 11.2% |
| CD56_CD8RO | 11.0% |
| Tconv memCCR5_total | 10.8% |
| CD27_CD8RO | 10.8% |
| Tconv memCD27_mem | 10.5% |
| NK_total | 10.2% |
| Tconv naive_CD3 | 10.2% |
| CD4 Treg _CD3 | 10.0% |
| CD4neg_CD3 | 10.0% |
| CD3hi_CD3 | 9.8% |
| CXCR3_CD8RO | 9.5% |
| CD8 RO CXCR3_CD3 | 9.5% |
| Bcells Ki67_CD3neg | 9.5% |
| Tconv naive_total | 9.0% |
| Treg naive_CD3 | 9.0% |
| Tconv memintB7_CD3 | 9.0% |
| Treg naive_CD4 | 9.0% |
| naive_Bcells | 8.8% |
| CD4 Tconv_total | 8.8% |
| Tconv memCXCR3_total | 8.5% |
| CD3pos_total | 8.5% |
| CD8 RA_total | 8.2% |
| CD4neg_total | 8.0% |
| NKCD56hi_nonTnonB | 8.0% |
| NK Ki67_nonTnonB | 8.0% |
| TIGIT_CD8RO | 7.8% |
| CD8 RA naive_total | 7.8% |
| Tconv memTIGIT_Tconv | 7.8% |
| CD3neg_total | 7.5% |
| CD8 RO Ki67_CD8 | 7.5% |
| CD8 RA naive_CD3 | 7.5% |
| CD4 Treg_CD4 | 7.0% |
| Tconv memCCR6_CD3 | 6.8% |
| Tconv memKi67_CD3 | 6.2% |
| CD8 RO CCR5_total | 6.2% |
| CD8 RO CD56_total | 6.2% |
| CD8 RO TIGIT_CD8 | 6.2% |
| Tconv mem_CD3 | 6.0% |
| Bcells naive_CD3neg | 6.0% |
| CD16+mono_total | 6.0% |
| Bcells_total | 5.8% |
| CD8 RO CCR6_CD8 | 5.8% |
| Tconv memCCR4_total | 5.2% |
| CD4 Tconv_CD3 | 5.2% |
| CD8 RO CCR6_CD3 | 5.2% |
| CD8 RO CD27_CD3 | 5.2% |
| CD8 RO PD1_total | 5.2% |
| CD8 RO PD1_CD8 | 5.2% |
| Tconv memCCR6_Tconv | 5.0% |
| CD8 RO CCR4_total | 4.8% |
| CD8 ncytotox RO CCR4_CD8ntox | 4.8% |
| Ki67_CD8RO | 4.5% |
| NK Ki67_CD3neg | 4.5% |
| Tconv memCD56_CD3 | 4.5% |
| Tconv memCCR4_Tconv | 4.5% |
| CD14+16+mono_CD3neg | 4.5% |
| PD1_CD8RO | 4.0% |
| CD4 Treg_total | 4.0% |
| NKCD56hi_CD3neg | 4.0% |
| CD8 RO CCR5_CD8 | 4.0% |
| Tconv memPD1_total | 3.8% |
| Bcells memory_CD3neg | 3.8% |
| Tconv memCXCR3_CD3 | 3.8% |
| CD8 RO DR_total | 3.8% |
| CD14+16+mono_total | 3.8% |
| CD8 RO CD27_CD8 | 3.5% |
| CD8 RO Ki67_total | 3.2% |
| Tconv memTIGIT_CD3 | 3.0% |
| CD8 RO CXCR3_total | 2.8% |
| Tconv memintB7_total | 2.8% |
| Tconv memPD1_Tconv | 2.8% |
| CD8 RO CCR6_total | 2.8% |
| CD8 RO CD27_total | 2.5% |
| NKCD16_nonTnonB | 2.5% |
| Tconv memCCR4_CD3 | 2.5% |
| Tconv memCXCR3_Tconv | 2.5% |
| Tconv memCD27_total | 2.2% |
| Tconv memCD56_Tconv | 2.2% |
| NK_nonTnonB | 2.2% |
| Tconv memCD56_mem | 2.2% |
| CD8 ncytotox RO CCR4_CD3 | 2.0% |
| CD8 RO_CD3 | 2.0% |
| CD14mono_CD3neg | 2.0% |
| Tconv memPD1_CD3 | 1.8% |
| Tconv memTIGIT_total | 1.8% |
| nonTnonB_CD3neg | 1.5% |
| CD8 RO CCR5_CD3 | 1.5% |
| NKCD16_CD3neg | 1.5% |
| CD8 RO intB7_CD3 | 1.2% |
| Tconv naive_Tconv | 1.2% |
| NKCD16_total | 1.0% |
| Tconv memCCR5_Tconv | 1.0% |
| NK_CD3neg | 1.0% |
| CD8  RO Ki67_CD3 | 1.0% |
| CD8 RO TIGIT_total | 1.0% |
| CD4 Tconv mem_total | 1.0% |
| nonTnonB_total | 1.0% |
| CD8 RO_CD8 | 0.8% |
| Tconv memKi67_Tconv | 0.8% |
| Tconv memCD27_CD3 | 0.8% |
| CD8 RA_CD8 | 0.8% |
| Bcells_CD3neg | 0.8% |
| CD8pos_total | 0.8% |
| Tconv memCCR5_CD3 | 0.8% |
| CD8 RO_total | 0.2% |
| myeloid_CD3neg | 0.2% |

### LASSO_RFE

**Base Method**: Raw feature selection frequencies across all bootstrap samples

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD16mono_myeloid | 56.5% |
| DR_CD8RO | 43.2% |
| CD8 RO DR_CD8 | 36.5% |
| CD27IgD_Bcells | 35.8% |
| Ki67_Bcells | 33.5% |
| NKCD56hi_total | 32.8% |
| CD14+16+mono_myeloid | 28.7% |
| CD3hi_total | 26.0% |
| Bcells CD27posIgDneg_total | 24.2% |
| CD16mono_CD3neg | 23.2% |
| CD14mono_myeloid | 23.0% |
| CD8pos_CD3 | 22.0% |
| Treg memory_CD3 | 21.2% |
| CD8 RO CD56_CD8 | 18.5% |
| Tconv memDR_CD3 | 18.2% |
| Tconv memDR_Tconv | 17.8% |
| Bcells memory_total | 17.8% |
| intB7_CD8RO | 16.0% |
| Bcells CD27negIgDneg_total | 16.0% |
| CD8 RA_CD3 | 15.2% |
| memory_Bcells | 15.0% |
| CD8 RO PD1_CD3 | 15.0% |
| Tconv mem_Tconv | 14.8% |
| Tconv memKi67_mem | 14.8% |
| Tconv memTIGIT_mem | 14.5% |
| Tconv memCD27_Tconv | 14.0% |
| NKCD16_NK | 13.8% |
| Tconv memPD1_mem | 13.8% |
| NKCD56hi_NK | 13.5% |
| Tconv memDR_mem | 13.5% |
| Tconv memCCR5_mem | 13.2% |
| Tconv memCCR6_mem | 12.8% |
| CD8 RO CD56_CD3 | 12.8% |
| Tconv memCCR4_mem | 12.5% |
| Tconv memCCR6_total | 12.0% |
| Tconv memintB7_Tconv | 12.0% |
| CCR5_CD8RO | 12.0% |
| CD27negIgDneg_Bcells | 11.8% |
| Tconv memDR_total | 11.8% |
| Tconv memCD56_total | 11.8% |
| CD8 RA CCR7 naive_CD8 | 11.8% |
| Treg memory_CD4 | 10.8% |
| CCR6_CD8RO | 10.8% |
| CCR4_CD8RO | 10.8% |
| CD8 RO DR_CD3 | 10.2% |
| Tconv memKi67_total | 10.0% |
| Tconv memCXCR3_mem | 10.0% |
| NK Ki67_total | 9.8% |
| CD56_CD8RO | 9.8% |
| Tconv naive_CD3 | 9.5% |
| NK Ki67_NK | 9.5% |
| Treg memory_total | 9.2% |
| Treg naive_total | 9.0% |
| Tconv naive_total | 9.0% |
| CD4 Treg _CD3 | 9.0% |
| Bcells Ki67_total | 9.0% |
| CD8 RO intB7_CD8 | 8.8% |
| CD4 Tconv_total | 8.8% |
| CD4neg_CD3 | 8.8% |
| Tconv memCCR5_total | 8.8% |
| CD3hi_CD4neg | 8.5% |
| CD8 RO CXCR3_CD8 | 8.2% |
| CD27_CD8RO | 8.2% |
| naive_Bcells | 8.2% |
| CD8 RO TIGIT_CD3 | 8.2% |
| Bcells naive_total | 8.0% |
| CD3hi_CD3 | 8.0% |
| CD3pos_total | 7.8% |
| CD8 RO CXCR3_CD3 | 7.8% |
| Tconv memCD27_mem | 7.5% |
| NK_total | 7.5% |
| Treg naive_CD3 | 7.2% |
| Bcells Ki67_CD3neg | 7.2% |
| Treg naive_CD4 | 7.2% |
| CXCR3_CD8RO | 7.2% |
| Tconv memintB7_mem | 6.5% |
| CD3neg_total | 6.5% |
| CD4 Treg_CD4 | 6.2% |
| Tconv memTIGIT_Tconv | 6.2% |
| CD8 RO intB7_total | 6.2% |
| CD8 RA_total | 6.2% |
| CD8 RA naive_CD3 | 5.8% |
| CD8 RO CCR5_total | 5.5% |
| Tconv mem_CD3 | 5.5% |
| Tconv memCXCR3_total | 5.5% |
| CD8 RO TIGIT_CD8 | 5.5% |
| NK Ki67_nonTnonB | 5.0% |
| NKCD56hi_nonTnonB | 5.0% |
| Tconv memCCR4_total | 5.0% |
| Bcells naive_CD3neg | 5.0% |
| Tconv memCCR6_CD3 | 4.8% |
| CD8 RA naive_total | 4.5% |
| CD4neg_total | 4.5% |
| Bcells_total | 4.5% |
| CD4 Tconv_CD3 | 4.5% |
| Tconv memintB7_CD3 | 4.5% |
| CD8 RO Ki67_CD8 | 4.5% |
| CD8 RO PD1_total | 4.2% |
| TIGIT_CD8RO | 4.2% |
| CD8 RO CD27_CD3 | 4.2% |
| Tconv memCCR4_Tconv | 4.0% |
| Tconv memKi67_CD3 | 4.0% |
| CD8 RO CCR6_CD3 | 3.8% |
| CD8 RO CCR5_CD8 | 3.5% |
| Tconv memCXCR3_CD3 | 3.5% |
| CD8 RO DR_total | 3.5% |
| CD8 RO CCR6_CD8 | 3.5% |
| CD16+mono_total | 3.5% |
| Tconv memPD1_total | 3.5% |
| CD8 RO PD1_CD8 | 3.2% |
| Ki67_CD8RO | 3.2% |
| Tconv memCCR6_Tconv | 3.2% |
| CD4 Treg_total | 3.0% |
| Tconv memTIGIT_CD3 | 3.0% |
| PD1_CD8RO | 3.0% |
| CD8 RO CD56_total | 3.0% |
| Bcells memory_CD3neg | 3.0% |
| CD8 ncytotox RO CCR4_CD8ntox | 2.8% |
| Tconv memintB7_total | 2.8% |
| NK Ki67_CD3neg | 2.8% |
| Tconv memPD1_Tconv | 2.5% |
| NKCD56hi_CD3neg | 2.5% |
| NKCD16_nonTnonB | 2.5% |
| CD14+16+mono_total | 2.5% |
| Tconv memCD56_CD3 | 2.5% |
| CD8 RO CCR4_total | 2.2% |
| Tconv memCXCR3_Tconv | 2.2% |
| CD14+16+mono_CD3neg | 2.2% |
| CD8 RO CXCR3_total | 2.2% |
| CD8 RO_CD3 | 2.0% |
| CD8 RO CD27_total | 2.0% |
| Tconv memCD56_Tconv | 2.0% |
| Tconv memCD27_total | 2.0% |
| CD8 RO Ki67_total | 2.0% |
| CD8 RO CCR6_total | 1.8% |
| CD14mono_CD3neg | 1.8% |
| Tconv memCD56_mem | 1.5% |
| Tconv memCCR4_CD3 | 1.5% |
| CD8 RO CD27_CD8 | 1.5% |
| NKCD16_CD3neg | 1.5% |
| NK_nonTnonB | 1.5% |
| nonTnonB_CD3neg | 1.5% |
| Tconv naive_Tconv | 1.2% |
| Tconv memTIGIT_total | 1.2% |
| CD8 ncytotox RO CCR4_CD3 | 1.2% |
| Tconv memPD1_CD3 | 1.2% |
| nonTnonB_total | 1.0% |
| CD8 RO TIGIT_total | 1.0% |
| CD8  RO Ki67_CD3 | 1.0% |
| CD8 RA_CD8 | 0.8% |
| NKCD16_total | 0.8% |
| CD8pos_total | 0.8% |
| Tconv memCD27_CD3 | 0.8% |
| NK_CD3neg | 0.8% |
| CD4 Tconv mem_total | 0.8% |
| CD8 RO_CD8 | 0.5% |
| CD8 RO CCR5_CD3 | 0.5% |
| Tconv memCCR5_Tconv | 0.5% |
| Bcells_CD3neg | 0.5% |
| Tconv memKi67_Tconv | 0.2% |
| CD8 RO_total | 0.2% |
| Tconv memCCR5_CD3 | 0.2% |
| myeloid_CD3neg | 0.2% |

### LASSO_Strict

**Base Method**: Raw feature selection frequencies across all bootstrap samples

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD16mono_myeloid | 36.2% |
| DR_CD8RO | 32.8% |
| NKCD56hi_total | 25.2% |
| CD8 RO DR_CD8 | 24.8% |
| CD27IgD_Bcells | 21.0% |
| CD14+16+mono_myeloid | 16.8% |
| Ki67_Bcells | 15.8% |
| CD3hi_total | 15.8% |
| CD16mono_CD3neg | 12.8% |
| CD14mono_myeloid | 12.8% |
| CD8 RO CD56_CD8 | 11.5% |
| Tconv memKi67_mem | 11.2% |
| Tconv memDR_Tconv | 11.0% |
| CD8pos_CD3 | 9.8% |
| Treg memory_CD3 | 9.8% |
| Tconv memDR_CD3 | 9.8% |
| Bcells CD27posIgDneg_total | 9.5% |
| Tconv mem_Tconv | 9.5% |
| CD8 RA_CD3 | 9.5% |
| Tconv memPD1_mem | 8.8% |
| Tconv memCCR5_mem | 8.0% |
| memory_Bcells | 7.8% |
| Bcells memory_total | 7.5% |
| CD8 RO PD1_CD3 | 7.5% |
| Tconv memDR_total | 7.5% |
| NKCD16_NK | 7.5% |
| CCR4_CD8RO | 7.0% |
| intB7_CD8RO | 7.0% |
| CD8 RO intB7_CD8 | 7.0% |
| CD8 RO DR_CD3 | 7.0% |
| Tconv memDR_mem | 6.8% |
| Tconv memCCR5_total | 6.5% |
| Tconv memCXCR3_mem | 6.5% |
| Tconv memCCR6_total | 6.0% |
| Tconv memintB7_Tconv | 5.8% |
| Tconv memCD27_Tconv | 5.8% |
| NKCD56hi_NK | 5.8% |
| CD8 RA CCR7 naive_CD8 | 5.8% |
| Tconv memKi67_total | 5.5% |
| Tconv memTIGIT_mem | 5.5% |
| CD8 RO TIGIT_CD3 | 5.5% |
| Bcells CD27negIgDneg_total | 5.2% |
| Tconv memCCR4_mem | 5.2% |
| CD8 RO intB7_total | 5.2% |
| Tconv memCD56_total | 5.0% |
| CD8 RO CXCR3_CD3 | 4.8% |
| Treg memory_total | 4.8% |
| Bcells Ki67_CD3neg | 4.5% |
| Tconv naive_CD3 | 4.5% |
| Tconv memintB7_mem | 4.5% |
| CCR5_CD8RO | 4.5% |
| CD3hi_CD4neg | 4.2% |
| NKCD56hi_nonTnonB | 4.2% |
| Tconv naive_total | 4.2% |
| CD3pos_total | 4.0% |
| CD56_CD8RO | 4.0% |
| Treg memory_CD4 | 3.8% |
| CD3hi_CD3 | 3.8% |
| Tconv memCCR6_mem | 3.8% |
| CD4neg_CD3 | 3.5% |
| CCR6_CD8RO | 3.5% |
| Tconv memKi67_CD3 | 3.5% |
| CD4 Treg _CD3 | 3.5% |
| CD4 Tconv_total | 3.5% |
| CD8 RA_total | 3.5% |
| Tconv memintB7_CD3 | 3.2% |
| Tconv memCD27_mem | 3.2% |
| CD8 RO CCR5_total | 3.2% |
| CD8 RO CD56_CD3 | 3.2% |
| NK Ki67_NK | 3.2% |
| CD27negIgDneg_Bcells | 3.2% |
| CD8 RO CXCR3_CD8 | 3.2% |
| CD27_CD8RO | 3.0% |
| CD4 Treg_CD4 | 3.0% |
| Bcells Ki67_total | 3.0% |
| TIGIT_CD8RO | 3.0% |
| Treg naive_total | 3.0% |
| CXCR3_CD8RO | 2.8% |
| NK Ki67_total | 2.8% |
| Tconv memCXCR3_total | 2.8% |
| CD8 RO PD1_total | 2.8% |
| CD8 RO TIGIT_CD8 | 2.5% |
| CD8 RO CD27_CD3 | 2.5% |
| Tconv memCCR6_CD3 | 2.2% |
| CD8 RO CCR6_CD3 | 2.2% |
| CD4neg_total | 2.2% |
| Tconv mem_CD3 | 2.2% |
| CD8 RA naive_CD3 | 2.2% |
| Treg naive_CD4 | 2.2% |
| CD8 RA naive_total | 2.2% |
| Bcells_total | 2.0% |
| CD8 RO Ki67_CD8 | 2.0% |
| Bcells naive_total | 2.0% |
| Tconv memPD1_total | 2.0% |
| Tconv memCCR4_total | 2.0% |
| CD14+16+mono_CD3neg | 1.8% |
| CD8 RO PD1_CD8 | 1.8% |
| CD8 ncytotox RO CCR4_CD8ntox | 1.8% |
| NKCD56hi_CD3neg | 1.8% |
| Ki67_CD8RO | 1.8% |
| CD14+16+mono_total | 1.8% |
| CD4 Tconv_CD3 | 1.8% |
| naive_Bcells | 1.8% |
| Treg naive_CD3 | 1.8% |
| Tconv memTIGIT_Tconv | 1.8% |
| Bcells memory_CD3neg | 1.5% |
| Bcells naive_CD3neg | 1.5% |
| CD8 RO CCR5_CD8 | 1.5% |
| CD8 RO CD56_total | 1.5% |
| CD8 RO DR_total | 1.5% |
| CD16+mono_total | 1.5% |
| Tconv memCCR4_Tconv | 1.2% |
| Tconv memCXCR3_CD3 | 1.2% |
| NK_total | 1.2% |
| CD8 RO_CD3 | 1.2% |
| NK Ki67_nonTnonB | 1.0% |
| CD8 RO CCR6_CD8 | 1.0% |
| NK Ki67_CD3neg | 1.0% |
| Tconv memCXCR3_Tconv | 1.0% |
| Tconv memCCR4_CD3 | 1.0% |
| CD8 RO CXCR3_total | 1.0% |
| CD8 RO CD27_CD8 | 1.0% |
| Tconv memCCR6_Tconv | 0.8% |
| CD3neg_total | 0.8% |
| CD8 RO Ki67_total | 0.8% |
| CD8 ncytotox RO CCR4_CD3 | 0.8% |
| Tconv memCD56_mem | 0.8% |
| Tconv memPD1_Tconv | 0.8% |
| nonTnonB_total | 0.8% |
| CD4 Treg_total | 0.8% |
| nonTnonB_CD3neg | 0.5% |
| CD8 RO CCR5_CD3 | 0.5% |
| CD8 RO CCR4_total | 0.5% |
| Tconv memCD56_CD3 | 0.5% |
| Tconv memintB7_total | 0.5% |
| CD14mono_CD3neg | 0.5% |
| Tconv naive_Tconv | 0.5% |
| CD8 RO intB7_CD3 | 0.2% |
| CD8 RO CD27_total | 0.2% |
| Tconv memCD27_total | 0.2% |
| NKCD16_CD3neg | 0.2% |
| NKCD16_total | 0.2% |
| NK_CD3neg | 0.2% |
| CD8 RO TIGIT_total | 0.2% |
| Tconv memKi67_Tconv | 0.2% |
| Tconv memPD1_CD3 | 0.2% |
| Tconv memCCR5_Tconv | 0.2% |
| myeloid_CD3neg | 0.2% |
| PD1_CD8RO | 0.2% |
| CD8pos_total | 0.2% |
| NK_nonTnonB | 0.2% |
| CD4 Tconv mem_total | 0.2% |
| Tconv memTIGIT_total | 0.2% |
| Tconv memCCR5_CD3 | 0.2% |
| CD8 RO CCR6_total | 0.2% |
| Tconv memTIGIT_CD3 | 0.2% |

### LogisticRegression_Permutation_AboveMean

**Base Method**: Raw feature selection frequencies across all bootstrap samples

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| DR_CD8RO | 33.2% |
| CD8 RO DR_CD8 | 22.0% |
| CD3hi_total | 18.2% |
| Bcells CD27posIgDneg_total | 18.0% |
| Ki67_Bcells | 16.0% |
| CD8 RO intB7_total | 15.5% |
| CD16mono_myeloid | 15.0% |
| CCR4_CD8RO | 12.5% |
| CD8 RO intB7_CD8 | 11.8% |
| Bcells CD27negIgDneg_total | 10.5% |
| CD27IgD_Bcells | 10.5% |
| Bcells memory_total | 10.0% |
| NKCD56hi_total | 9.2% |
| Tconv memCD56_total | 8.8% |
| CD3hi_CD3 | 8.8% |
| Tconv memCCR5_mem | 8.0% |
| Bcells Ki67_total | 7.8% |
| memory_Bcells | 7.5% |
| Tconv memDR_total | 6.8% |
| intB7_CD8RO | 6.8% |
| Tconv memPD1_mem | 6.2% |
| CD14mono_myeloid | 6.0% |
| NKCD56hi_NK | 6.0% |
| CD14+16+mono_myeloid | 5.5% |
| CD8 RO CD56_CD8 | 5.5% |
| CD8 ncytotox RO CCR4_CD8ntox | 5.5% |
| TIGIT_CD8RO | 5.2% |
| CD16mono_CD3neg | 5.0% |
| Tconv memKi67_mem | 4.8% |
| NKCD16_NK | 4.8% |
| CD3hi_CD4neg | 4.5% |
| CD8 RO intB7_CD3 | 4.5% |
| CD8 RA_total | 4.0% |
| Tconv memintB7_CD3 | 4.0% |
| Tconv memKi67_total | 4.0% |
| CCR6_CD8RO | 3.8% |
| Bcells Ki67_CD3neg | 3.8% |
| CD8 RO DR_total | 3.8% |
| CD8 RA CCR7 naive_CD8 | 3.8% |
| CD8 RA_CD3 | 3.5% |
| Tconv memKi67_CD3 | 3.5% |
| CD14+16+mono_CD3neg | 3.0% |
| Tconv memCCR5_Tconv | 3.0% |
| Tconv memintB7_mem | 3.0% |
| Tconv memCCR5_total | 3.0% |
| Tconv memCCR4_mem | 3.0% |
| CD8 RA naive_CD3 | 2.8% |
| Tconv memCXCR3_total | 2.5% |
| CD8 RO CD56_total | 2.5% |
| CD8 RO Ki67_CD8 | 2.5% |
| Ki67_CD8RO | 2.5% |
| CD16+mono_total | 2.2% |
| NK Ki67_NK | 2.0% |
| Tconv memTIGIT_mem | 2.0% |
| Tconv memCCR5_CD3 | 2.0% |
| Bcells memory_CD3neg | 2.0% |
| CD8 RA naive_total | 2.0% |
| CD8 RO TIGIT_CD3 | 2.0% |
| CD4 Treg _CD3 | 1.8% |
| CD4neg_CD3 | 1.8% |
| PD1_CD8RO | 1.8% |
| Tconv memCD27_CD3 | 1.8% |
| Tconv memCD27_mem | 1.8% |
| Tconv memCCR6_total | 1.8% |
| Treg memory_total | 1.8% |
| NKCD56hi_CD3neg | 1.8% |
| CD4neg_total | 1.5% |
| CD4 Treg_total | 1.5% |
| CD8 RO TIGIT_CD8 | 1.5% |
| NKCD56hi_nonTnonB | 1.5% |
| CD8 RO PD1_CD3 | 1.5% |
| Tconv memCCR6_mem | 1.5% |
| Treg memory_CD3 | 1.5% |
| CD56_CD8RO | 1.5% |
| Tconv memCD27_Tconv | 1.2% |
| Treg naive_CD3 | 1.2% |
| CD8 RO PD1_CD8 | 1.2% |
| CD27negIgDneg_Bcells | 1.2% |
| Treg memory_CD4 | 1.2% |
| Treg naive_total | 1.2% |
| CD8 RO CCR6_CD8 | 1.2% |
| Tconv memPD1_total | 1.2% |
| Tconv mem_Tconv | 1.2% |
| Tconv mem_CD3 | 1.2% |
| Tconv memDR_CD3 | 1.2% |
| CD8 RO CCR5_total | 1.2% |
| Tconv memPD1_CD3 | 1.2% |
| Tconv memintB7_Tconv | 1.2% |
| CD4 Treg_CD4 | 1.0% |
| CD8 RO DR_CD3 | 1.0% |
| Tconv memTIGIT_Tconv | 1.0% |
| CD8pos_CD3 | 1.0% |
| NK Ki67_total | 1.0% |
| Tconv memCXCR3_mem | 1.0% |
| CD8 RO Ki67_total | 1.0% |
| CXCR3_CD8RO | 1.0% |
| CD8 RO PD1_total | 1.0% |
| CD8 RO CXCR3_CD8 | 1.0% |
| Tconv memCCR4_total | 1.0% |
| CD8 RO CCR4_total | 1.0% |
| Treg naive_CD4 | 1.0% |
| CD8 RO CXCR3_CD3 | 0.8% |
| NK Ki67_CD3neg | 0.8% |
| naive_Bcells | 0.8% |
| CD8 RO CCR6_CD3 | 0.8% |
| Tconv memDR_mem | 0.8% |
| CD8 RO CD56_CD3 | 0.8% |
| CD14+16+mono_total | 0.8% |
| Tconv memCCR6_Tconv | 0.8% |
| Tconv memCCR4_CD3 | 0.8% |
| Tconv memintB7_total | 0.8% |
| CD8 RO CCR5_CD3 | 0.8% |
| Tconv memCD56_mem | 0.5% |
| CCR5_CD8RO | 0.5% |
| Tconv memCD27_total | 0.5% |
| CD8 RO_CD8 | 0.5% |
| Tconv memTIGIT_CD3 | 0.5% |
| CD8 RA_CD8 | 0.5% |
| Bcells naive_total | 0.5% |
| Tconv memKi67_Tconv | 0.5% |
| CD27_CD8RO | 0.5% |
| Tconv naive_Tconv | 0.5% |
| Tconv memCD56_Tconv | 0.5% |
| Tconv memCD56_CD3 | 0.5% |
| Bcells naive_CD3neg | 0.2% |
| Bcells_total | 0.2% |
| NKCD16_nonTnonB | 0.2% |
| Tconv memPD1_Tconv | 0.2% |
| Tconv memCXCR3_Tconv | 0.2% |
| NK_nonTnonB | 0.2% |
| CD8 RO CD27_CD8 | 0.2% |
| CD8  RO Ki67_CD3 | 0.2% |
| Tconv memCXCR3_CD3 | 0.2% |
| CD8 RO TIGIT_total | 0.2% |
| CD8 RO CXCR3_total | 0.2% |
| CD8 RO CCR6_total | 0.2% |
| CD3neg_total | 0.2% |
| Tconv memCCR6_CD3 | 0.2% |
| Tconv memCCR4_Tconv | 0.2% |
| Tconv naive_CD3 | 0.2% |
| CD3pos_total | 0.2% |
| Tconv naive_total | 0.2% |
| Tconv memDR_Tconv | 0.2% |
| CD8 RO CD27_CD3 | 0.2% |

### LogisticRegression_Permutation_Top10%

**Base Method**: Raw feature selection frequencies across all bootstrap samples

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Tconv memCD56_total | 89.8% |
| Tconv memKi67_total | 89.5% |
| Tconv memPD1_total | 87.8% |
| Tconv memDR_total | 87.5% |
| Tconv memintB7_total | 87.2% |
| Tconv memCD27_total | 85.5% |
| Tconv memCXCR3_total | 83.2% |
| Tconv naive_total | 81.2% |
| Tconv memTIGIT_total | 74.5% |
| CD3pos_total | 69.0% |
| CD4 Treg_total | 69.0% |
| CD4 Tconv mem_total | 64.8% |
| Tconv memCCR6_total | 58.0% |
| Tconv memCCR4_total | 52.5% |
| Tconv memCCR5_total | 51.2% |
| CD4 Tconv_total | 50.2% |
| DR_CD8RO | 33.5% |
| CD8 RO DR_CD8 | 21.5% |
| Bcells CD27posIgDneg_total | 17.8% |
| CD3hi_total | 17.5% |
| Ki67_Bcells | 15.5% |
| CD8 RO intB7_total | 15.5% |
| CD16mono_myeloid | 14.5% |
| CCR4_CD8RO | 12.2% |
| CD8 RO intB7_CD8 | 10.8% |
| Bcells CD27negIgDneg_total | 10.2% |
| Bcells memory_total | 10.2% |
| CD27IgD_Bcells | 10.2% |
| NKCD56hi_total | 9.5% |
| CD3hi_CD3 | 8.5% |
| Tconv memCCR5_mem | 7.5% |
| intB7_CD8RO | 7.0% |
| Bcells Ki67_total | 6.8% |
| memory_Bcells | 6.5% |
| Tconv memPD1_mem | 6.0% |
| NKCD56hi_NK | 5.8% |
| CD14+16+mono_myeloid | 5.5% |
| CD14mono_myeloid | 5.2% |
| CD8 ncytotox RO CCR4_CD8ntox | 5.0% |
| CD16mono_CD3neg | 5.0% |
| CD8 RO CD56_CD8 | 5.0% |
| Tconv memKi67_mem | 4.5% |
| CD8 RO intB7_CD3 | 4.2% |
| TIGIT_CD8RO | 4.2% |
| CD3hi_CD4neg | 4.2% |
| NKCD16_NK | 4.0% |
| CD8 RA CCR7 naive_CD8 | 3.8% |
| Tconv memKi67_CD3 | 3.5% |
| CD8 RA_total | 3.5% |
| CCR6_CD8RO | 3.5% |
| Tconv memintB7_CD3 | 3.2% |
| CD8 RA_CD3 | 3.2% |
| CD8 RO DR_total | 3.0% |
| CD16+mono_total | 2.8% |
| Tconv memintB7_mem | 2.8% |
| CD14+16+mono_CD3neg | 2.8% |
| Tconv memCCR4_mem | 2.8% |
| Bcells Ki67_CD3neg | 2.5% |
| Ki67_CD8RO | 2.5% |
| Tconv memCD27_mem | 2.5% |
| CD8 RA naive_CD3 | 2.5% |
| Tconv memCCR5_Tconv | 2.5% |
| CD8 RO Ki67_CD8 | 2.5% |
| NK Ki67_NK | 2.2% |
| Tconv memTIGIT_mem | 2.2% |
| CD8 RO CD56_total | 2.2% |
| Bcells memory_CD3neg | 2.2% |
| CD8 RO TIGIT_CD3 | 2.0% |
| CD4neg_CD3 | 2.0% |
| CD8 RA naive_total | 1.8% |
| Tconv memCCR5_CD3 | 1.8% |
| Tconv memCCR6_mem | 1.8% |
| NKCD56hi_CD3neg | 1.5% |
| CD8 RO PD1_total | 1.5% |
| NKCD56hi_nonTnonB | 1.5% |
| Treg memory_total | 1.5% |
| CD56_CD8RO | 1.5% |
| CD8 RO DR_CD3 | 1.5% |
| Treg memory_CD4 | 1.2% |
| CD8 RO PD1_CD8 | 1.2% |
| CD4neg_total | 1.2% |
| Treg naive_total | 1.2% |
| CD4 Treg _CD3 | 1.2% |
| CD8 RO PD1_CD3 | 1.2% |
| CD8 RO TIGIT_CD8 | 1.2% |
| Tconv memPD1_CD3 | 1.2% |
| Tconv memDR_CD3 | 1.2% |
| NK Ki67_total | 1.0% |
| CD8 RO CXCR3_CD8 | 1.0% |
| Tconv mem_Tconv | 1.0% |
| CXCR3_CD8RO | 1.0% |
| CD4 Treg_CD4 | 1.0% |
| Treg memory_CD3 | 1.0% |
| Tconv memCXCR3_mem | 1.0% |
| Treg naive_CD3 | 1.0% |
| Tconv mem_CD3 | 1.0% |
| CD27negIgDneg_Bcells | 1.0% |
| CCR5_CD8RO | 1.0% |
| Tconv memCD56_CD3 | 1.0% |
| CD8 RO Ki67_total | 1.0% |
| CD8 RO CCR6_CD8 | 1.0% |
| CD8pos_CD3 | 1.0% |
| Tconv memCD56_Tconv | 1.0% |
| CD14+16+mono_total | 0.8% |
| NK Ki67_CD3neg | 0.8% |
| CD8 RO CCR6_CD3 | 0.8% |
| Tconv memKi67_Tconv | 0.8% |
| Tconv memCD56_mem | 0.8% |
| Tconv memintB7_Tconv | 0.8% |
| CD8 RO CD56_CD3 | 0.8% |
| naive_Bcells | 0.8% |
| CD8 RO CCR4_total | 0.8% |
| Tconv memPD1_Tconv | 0.8% |
| Tconv memTIGIT_CD3 | 0.8% |
| Tconv memTIGIT_Tconv | 0.8% |
| CD8 RO CCR5_total | 0.8% |
| PD1_CD8RO | 0.5% |
| Bcells_total | 0.5% |
| CD8 RO CXCR3_CD3 | 0.5% |
| Tconv memCXCR3_Tconv | 0.5% |
| CD8 RO_CD8 | 0.5% |
| CD8 ncytotox RO CCR4_CD3 | 0.5% |
| Bcells naive_total | 0.5% |
| Tconv memCCR6_Tconv | 0.5% |
| Tconv memDR_mem | 0.5% |
| Treg naive_CD4 | 0.5% |
| NK Ki67_nonTnonB | 0.5% |
| CD8 RA_CD8 | 0.5% |
| Tconv memCD27_Tconv | 0.5% |
| NK_CD3neg | 0.2% |
| NKCD16_CD3neg | 0.2% |
| CD8  RO Ki67_CD3 | 0.2% |
| CD3neg_total | 0.2% |
| CD8 RO CCR5_CD8 | 0.2% |
| Tconv memCCR6_CD3 | 0.2% |
| CD8 RO CCR5_CD3 | 0.2% |
| CD27_CD8RO | 0.2% |
| nonTnonB_total | 0.2% |
| CD14mono_total | 0.2% |
| CD8 RO CCR6_total | 0.2% |
| CD8 RO TIGIT_total | 0.2% |
| NK_total | 0.2% |
| Tconv memCCR4_CD3 | 0.2% |
| CD8 RO CD27_CD8 | 0.2% |
| CD8 RO CD27_CD3 | 0.2% |
| Tconv memCD27_CD3 | 0.2% |
| CD8 RO_total | 0.2% |

### Mutual Information (Top 10%)

**Base Method**: Raw feature selection frequencies across all bootstrap samples

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Bcells CD27posIgDneg_total | 33.2% |
| Tconv mem_Tconv | 30.8% |
| CD27IgD_Bcells | 30.5% |
| nonTnonB_total | 28.5% |
| CD14mono_total | 28.0% |
| Tconv naive_Tconv | 27.3% |
| Treg memory_CD4 | 26.2% |
| CD8 RO DR_CD3 | 25.2% |
| Tconv memCD27_CD3 | 25.2% |
| CD8pos_CD3 | 25.0% |
| CD8 ncytotox RO CCR4_CD8ntox | 24.2% |
| CD4 Treg_CD4 | 23.8% |
| Treg memory_CD3 | 23.8% |
| CD8 RA_CD8 | 23.5% |
| CD3pos_total | 23.0% |
| CD3neg_total | 23.0% |
| CD8  RO Ki67_CD3 | 22.8% |
| Tconv naive_total | 22.5% |
| nonTnonB_CD3neg | 21.8% |
| Tconv naive_CD3 | 21.0% |
| CD8 RO_CD3 | 20.0% |
| CD14mono_CD3neg | 18.8% |
| CD16mono_myeloid | 18.2% |
| NK_nonTnonB | 18.0% |
| Bcells memory_CD3neg | 17.8% |
| NKCD16_CD3neg | 17.5% |
| Bcells_CD3neg | 17.5% |
| CD8 RO_total | 17.2% |
| CD8 RA CCR7 naive_CD8 | 16.5% |
| CD4 Treg _CD3 | 16.2% |
| Ki67_Bcells | 16.0% |
| Treg naive_total | 16.0% |
| NKCD16_nonTnonB | 15.8% |
| NK Ki67_nonTnonB | 15.5% |
| Treg naive_CD4 | 15.5% |
| intB7_CD8RO | 15.0% |
| myeloid_total | 15.0% |
| CD4 Treg_total | 14.8% |
| CD8 RO CCR5_CD3 | 14.8% |
| CD16mono_CD3neg | 14.8% |
| Tconv memCD27_Tconv | 14.5% |
| Treg naive_CD3 | 14.5% |
| CD8 RO CD27_CD3 | 14.2% |
| CD8 RA naive_total | 14.0% |
| Tconv memCCR6_CD3 | 14.0% |
| CD8 RO CCR5_total | 13.8% |
| Tconv memPD1_total | 13.5% |
| naive_Bcells | 13.0% |
| DR_CD8RO | 13.0% |
| Tconv memDR_mem | 13.0% |
| CD8 RO CCR4_total | 12.8% |
| Tconv memKi67_CD3 | 12.8% |
| CD8 RA naive_CD3 | 12.8% |
| Tconv memDR_CD3 | 12.5% |
| Tconv memKi67_total | 12.2% |
| CD4 Tconv mem_total | 12.2% |
| Tconv memTIGIT_CD3 | 12.2% |
| Tconv memintB7_Tconv | 11.5% |
| CD4neg_CD3 | 11.2% |
| Tconv memCXCR3_mem | 11.0% |
| CD8 RO TIGIT_CD3 | 10.5% |
| Tconv memintB7_mem | 10.2% |
| CD4 Tconv_total | 10.2% |
| NK Ki67_NK | 10.2% |
| Tconv memCCR4_mem | 10.0% |
| NK_CD3neg | 9.8% |
| Ki67_CD8RO | 9.8% |
| CD8 RO CD27_CD8 | 9.8% |
| CD8 RO CCR6_CD3 | 9.5% |
| Bcells_total | 9.5% |
| CD8 RO CXCR3_CD8 | 9.5% |
| Tconv memintB7_CD3 | 9.2% |
| Tconv memDR_Tconv | 9.2% |
| Tconv memCD56_Tconv | 9.2% |
| PD1_CD8RO | 9.2% |
| Tconv memCCR6_Tconv | 9.0% |
| Tconv memKi67_mem | 9.0% |
| CD8 RA_total | 8.8% |
| CD8pos_total | 8.8% |
| Treg memory_total | 8.5% |
| Tconv memCD27_total | 8.5% |
| CD27_CD8RO | 8.5% |
| Bcells Ki67_total | 8.2% |
| NK Ki67_total | 8.2% |
| CD8 RO CD27_total | 8.2% |
| Tconv memCCR4_Tconv | 8.2% |
| Tconv memintB7_total | 8.0% |
| CD8 RO DR_CD8 | 8.0% |
| Tconv memCCR6_total | 7.8% |
| CD8 RO CCR6_total | 7.5% |
| Tconv memTIGIT_mem | 7.5% |
| CD8 RA_CD3 | 7.2% |
| Tconv memCCR5_total | 7.2% |
| NKCD16_total | 7.0% |
| Tconv mem_CD3 | 7.0% |
| Tconv memCXCR3_Tconv | 6.8% |
| Tconv memCCR5_mem | 6.8% |
| Tconv memTIGIT_total | 6.8% |
| CD27negIgDneg_Bcells | 6.8% |
| CD8 RO TIGIT_CD8 | 6.5% |
| Tconv memCCR6_mem | 6.5% |
| Bcells memory_total | 6.5% |
| TIGIT_CD8RO | 6.5% |
| Tconv memKi67_Tconv | 6.2% |
| CD8 RO DR_total | 6.0% |
| CD8 RO PD1_CD3 | 6.0% |
| CD3hi_CD3 | 6.0% |
| CD14mono_myeloid | 6.0% |
| Tconv memCD27_mem | 6.0% |
| CD3hi_total | 5.8% |
| CD8 RO CXCR3_CD3 | 5.8% |
| Tconv memPD1_mem | 5.8% |
| CD8 RO PD1_total | 5.8% |
| CD14+16+mono_myeloid | 5.8% |
| CD16+mono_total | 5.5% |
| CD8 RO CXCR3_total | 5.5% |
| Tconv memCXCR3_CD3 | 5.5% |
| CD14+16+mono_CD3neg | 5.5% |
| CCR4_CD8RO | 5.5% |
| CD8 RO Ki67_total | 5.5% |
| Bcells naive_CD3neg | 5.2% |
| NKCD56hi_NK | 5.2% |
| NKCD56hi_total | 5.0% |
| CD4 Tconv_CD3 | 4.8% |
| CD56_CD8RO | 4.8% |
| CD8 RO TIGIT_total | 4.8% |
| CD8 RO intB7_total | 4.5% |
| Tconv memCCR4_total | 4.5% |
| Tconv memTIGIT_Tconv | 4.5% |
| CD8 RO CCR5_CD8 | 4.2% |
| CD8 RO CCR6_CD8 | 4.2% |
| CD8 RO CD56_total | 4.2% |
| myeloid_CD3neg | 4.0% |
| CD8 RO_CD8 | 4.0% |
| NKCD16_NK | 3.8% |
| Bcells naive_total | 3.8% |
| NK_total | 3.8% |
| Tconv memCD56_mem | 3.5% |
| Tconv memCCR4_CD3 | 3.5% |
| CD14+16+mono_total | 3.2% |
| Tconv memPD1_CD3 | 3.2% |
| memory_Bcells | 3.2% |
| CCR6_CD8RO | 3.2% |
| CCR5_CD8RO | 3.2% |
| NK Ki67_CD3neg | 3.2% |
| CD8 RO Ki67_CD8 | 3.0% |
| CD8 ncytotox RO CCR4_CD3 | 3.0% |
| CD8 RO CD56_CD3 | 3.0% |
| CD8 RO PD1_CD8 | 2.8% |
| Tconv memDR_total | 2.8% |
| Tconv memCCR5_CD3 | 2.8% |
| CD8 RO CD56_CD8 | 2.8% |
| Tconv memCCR5_Tconv | 2.5% |
| Tconv memPD1_Tconv | 2.5% |
| Bcells CD27negIgDneg_total | 2.2% |
| CD8 RO intB7_CD8 | 2.0% |
| CXCR3_CD8RO | 1.8% |
| CD3hi_CD4neg | 1.8% |
| Tconv memCD56_CD3 | 1.8% |
| Tconv memCXCR3_total | 1.5% |
| NKCD56hi_nonTnonB | 1.2% |
| CD4neg_total | 1.2% |
| CD8 RO intB7_CD3 | 1.2% |
| Tconv memCD56_total | 1.0% |
| Bcells Ki67_CD3neg | 0.5% |
| NKCD56hi_CD3neg | 0.5% |

### NaiveBayes_Permutation_AboveMean

**Base Method**: Raw feature selection frequencies across all bootstrap samples

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD3hi_total | 80.8% |
| Bcells CD27posIgDneg_total | 79.0% |
| Bcells memory_total | 65.8% |
| CD8 RO DR_total | 64.2% |
| CD16mono_myeloid | 62.0% |
| CD8 RO DR_CD3 | 61.3% |
| Tconv memCD56_total | 60.5% |
| Ki67_CD8RO | 60.2% |
| Bcells memory_CD3neg | 59.5% |
| CD8 RO CD56_total | 59.5% |
| NKCD56hi_NK | 59.2% |
| Ki67_Bcells | 58.8% |
| CD8  RO Ki67_CD3 | 57.8% |
| CD8 RO CD56_CD3 | 56.2% |
| CD8 RO Ki67_CD8 | 56.2% |
| NKCD16_NK | 56.2% |
| Tconv memCXCR3_total | 55.2% |
| NK Ki67_NK | 55.0% |
| CD8 RO Ki67_total | 54.2% |
| CD27IgD_Bcells | 54.0% |
| DR_CD8RO | 52.5% |
| CD14+16+mono_total | 51.2% |
| Tconv memCXCR3_Tconv | 50.2% |
| NK Ki67_total | 50.2% |
| Tconv memCXCR3_CD3 | 49.8% |
| CD8 RA naive_CD3 | 49.8% |
| CD14+16+mono_myeloid | 49.5% |
| Bcells CD27negIgDneg_total | 49.2% |
| CD14+16+mono_CD3neg | 48.8% |
| NKCD56hi_total | 47.2% |
| Tconv memKi67_total | 47.0% |
| Tconv memCD56_Tconv | 46.5% |
| CD3hi_CD3 | 45.5% |
| Tconv memCD56_mem | 45.5% |
| NK Ki67_nonTnonB | 45.2% |
| CD8 RO DR_CD8 | 44.8% |
| Tconv memCXCR3_mem | 42.5% |
| NKCD16_total | 42.0% |
| NK_total | 41.8% |
| CD16mono_CD3neg | 41.8% |
| Tconv memCD56_CD3 | 41.2% |
| Bcells naive_total | 41.2% |
| CD8 RA_CD3 | 41.0% |
| Bcells Ki67_CD3neg | 40.2% |
| CD8 RO intB7_CD3 | 40.0% |
| Treg memory_CD4 | 39.5% |
| Tconv memTIGIT_mem | 39.2% |
| CD14mono_myeloid | 39.0% |
| Tconv memintB7_CD3 | 38.8% |
| Tconv memCCR5_total | 38.8% |
| CD27_CD8RO | 38.2% |
| NK Ki67_CD3neg | 38.2% |
| CD16+mono_total | 38.2% |
| CD8 RO CXCR3_CD3 | 38.0% |
| CD4 Treg _CD3 | 37.2% |
| CD4 Treg_CD4 | 37.2% |
| Tconv memDR_mem | 37.2% |
| Treg memory_total | 37.2% |
| Treg memory_CD3 | 37.2% |
| Bcells Ki67_total | 37.0% |
| CCR4_CD8RO | 37.0% |
| Tconv memPD1_mem | 37.0% |
| Tconv memCD27_Tconv | 36.5% |
| Tconv memintB7_mem | 36.2% |
| Tconv memCCR4_CD3 | 36.2% |
| Treg naive_CD3 | 36.2% |
| Bcells_total | 36.0% |
| Tconv memCCR6_CD3 | 35.5% |
| Tconv memintB7_Tconv | 35.2% |
| CD8 RA naive_total | 34.8% |
| Tconv memCCR4_Tconv | 34.8% |
| Tconv memCD27_mem | 34.5% |
| CD8 RO CD56_CD8 | 34.5% |
| intB7_CD8RO | 34.5% |
| CD8 RO intB7_total | 33.8% |
| CD8 RO CCR5_CD3 | 33.5% |
| Tconv memCCR6_total | 33.2% |
| naive_Bcells | 33.0% |
| CD4 Treg_total | 33.0% |
| CD8 RO CCR6_CD3 | 33.0% |
| CXCR3_CD8RO | 33.0% |
| Treg naive_CD4 | 32.8% |
| CD3hi_CD4neg | 32.8% |
| CCR5_CD8RO | 32.8% |
| CD27negIgDneg_Bcells | 32.2% |
| Tconv memCD27_CD3 | 32.2% |
| Tconv mem_Tconv | 32.2% |
| CCR6_CD8RO | 31.8% |
| CD4neg_CD3 | 31.8% |
| Tconv mem_CD3 | 31.5% |
| CD8 RO CCR5_total | 31.5% |
| Tconv memDR_total | 31.2% |
| CD8 RO CXCR3_CD8 | 31.2% |
| Tconv memCCR6_Tconv | 31.2% |
| CD8 RO CXCR3_total | 31.2% |
| CD8 RO intB7_CD8 | 31.2% |
| CD8 RO TIGIT_CD8 | 31.0% |
| Tconv naive_Tconv | 31.0% |
| Tconv memCCR5_mem | 30.8% |
| CD8 RA CCR7 naive_CD8 | 30.5% |
| CD8 RA_total | 30.5% |
| Tconv memCCR6_mem | 30.5% |
| NKCD56hi_CD3neg | 30.2% |
| CD8 ncytotox RO CCR4_CD8ntox | 30.2% |
| NKCD56hi_nonTnonB | 30.2% |
| CD8 RO CCR6_total | 29.2% |
| CD8 RO PD1_CD3 | 28.7% |
| CD8 RO_CD8 | 28.5% |
| memory_Bcells | 28.5% |
| CD4neg_total | 28.5% |
| CD8 RO PD1_total | 28.5% |
| Treg naive_total | 28.2% |
| CD8 RO CCR6_CD8 | 28.2% |
| NKCD16_nonTnonB | 28.2% |
| NK_nonTnonB | 28.0% |
| CD8 RO CCR4_total | 28.0% |
| CD8 RO PD1_CD8 | 27.8% |
| CD8 RO CCR5_CD8 | 27.8% |
| Tconv memDR_CD3 | 27.5% |
| Tconv memCCR4_mem | 26.5% |
| Tconv memKi67_mem | 26.5% |
| NKCD16_CD3neg | 26.5% |
| CD8 RA_CD8 | 26.2% |
| CD8pos_CD3 | 26.2% |
| NK_CD3neg | 26.0% |
| PD1_CD8RO | 25.8% |
| Tconv naive_CD3 | 25.2% |
| Tconv memTIGIT_total | 25.0% |
| Tconv memCCR5_CD3 | 25.0% |
| Tconv memPD1_total | 24.8% |
| CD8 RO CD27_CD8 | 24.5% |
| Tconv memCCR5_Tconv | 24.5% |
| Tconv memDR_Tconv | 24.5% |
| Bcells naive_CD3neg | 24.5% |
| CD8 ncytotox RO CCR4_CD3 | 23.5% |
| TIGIT_CD8RO | 23.2% |
| CD56_CD8RO | 23.2% |
| CD8 RO_CD3 | 22.8% |
| Tconv memintB7_total | 22.8% |
| Tconv memKi67_CD3 | 22.8% |
| CD4 Tconv_CD3 | 22.5% |
| CD8 RO CD27_CD3 | 22.5% |
| CD8 RO TIGIT_CD3 | 22.0% |
| CD8pos_total | 21.8% |
| CD8 RO TIGIT_total | 21.0% |
| Tconv naive_total | 20.8% |
| CD8 RO CD27_total | 20.8% |
| Tconv memCCR4_total | 20.8% |
| Tconv memTIGIT_CD3 | 20.8% |
| myeloid_CD3neg | 20.5% |
| Tconv memTIGIT_Tconv | 20.0% |
| CD4 Tconv mem_total | 19.8% |
| Tconv memCD27_total | 19.5% |
| CD14mono_CD3neg | 18.8% |
| Bcells_CD3neg | 18.2% |
| nonTnonB_CD3neg | 17.8% |
| Tconv memPD1_CD3 | 16.8% |
| CD8 RO_total | 16.8% |
| Tconv memPD1_Tconv | 16.2% |
| Tconv memKi67_Tconv | 14.8% |
| myeloid_total | 14.5% |
| CD14mono_total | 14.2% |
| CD4 Tconv_total | 12.2% |
| CD3neg_total | 12.0% |
| CD3pos_total | 12.0% |
| nonTnonB_total | 11.0% |

### NaiveBayes_Permutation_Top10%

**Base Method**: Raw feature selection frequencies across all bootstrap samples

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Bcells CD27posIgDneg_total | 56.8% |
| CD3hi_total | 55.8% |
| Bcells memory_total | 46.2% |
| CD8  RO Ki67_CD3 | 42.0% |
| CD8 RO Ki67_CD8 | 39.0% |
| Ki67_Bcells | 38.0% |
| Tconv memCD56_total | 37.8% |
| Ki67_CD8RO | 37.2% |
| CD8 RO DR_CD3 | 37.2% |
| Bcells memory_CD3neg | 35.8% |
| CD14+16+mono_total | 34.2% |
| CD8 RO Ki67_total | 34.0% |
| CD8 RO DR_total | 33.5% |
| CD8 RO CD56_CD3 | 32.5% |
| CD8 RO CD56_total | 32.5% |
| NKCD56hi_NK | 32.2% |
| NK Ki67_NK | 31.2% |
| NKCD16_NK | 29.0% |
| Tconv memCXCR3_total | 27.5% |
| CD16mono_myeloid | 25.2% |
| CD14+16+mono_CD3neg | 24.8% |
| Tconv memCXCR3_Tconv | 23.5% |
| Tconv memCD56_Tconv | 23.0% |
| CD14+16+mono_myeloid | 21.5% |
| NK Ki67_total | 18.2% |
| Tconv memKi67_total | 18.2% |
| Tconv memCXCR3_CD3 | 18.0% |
| Tconv memCD56_mem | 17.8% |
| DR_CD8RO | 17.8% |
| Bcells CD27negIgDneg_total | 17.2% |
| CD8 RA naive_CD3 | 17.2% |
| CD3hi_CD3 | 17.0% |
| NKCD56hi_total | 17.0% |
| CD27IgD_Bcells | 16.8% |
| CD8 RO DR_CD8 | 15.0% |
| Tconv memCD56_CD3 | 14.8% |
| Bcells naive_total | 14.5% |
| Tconv memintB7_CD3 | 13.2% |
| Bcells_total | 12.0% |
| Bcells Ki67_CD3neg | 11.2% |
| CD8 RO intB7_CD3 | 11.0% |
| Treg memory_CD4 | 11.0% |
| CD8 RO CD56_CD8 | 10.8% |
| NK Ki67_nonTnonB | 10.8% |
| CD27negIgDneg_Bcells | 10.5% |
| CD14mono_myeloid | 10.5% |
| CD8 RO CCR5_total | 10.2% |
| Tconv memCCR5_total | 10.2% |
| Tconv memCXCR3_mem | 9.2% |
| CD4 Treg_CD4 | 9.2% |
| CD8 RO intB7_total | 9.0% |
| Treg memory_total | 9.0% |
| Treg memory_CD3 | 9.0% |
| CD16mono_CD3neg | 8.8% |
| CD8 RO CXCR3_CD3 | 8.5% |
| CD27_CD8RO | 8.5% |
| NKCD16_total | 8.5% |
| CD4neg_CD3 | 8.2% |
| CD8 RO CCR4_total | 7.8% |
| CD8 RA_CD3 | 7.8% |
| NK_total | 7.5% |
| Tconv memintB7_mem | 7.5% |
| Bcells Ki67_total | 7.5% |
| Treg naive_total | 7.2% |
| Tconv memCD27_Tconv | 7.2% |
| Tconv memDR_mem | 7.0% |
| Tconv memintB7_Tconv | 6.8% |
| Treg naive_CD3 | 6.8% |
| CD4 Treg _CD3 | 6.5% |
| NK Ki67_CD3neg | 6.5% |
| CD8 RA naive_total | 6.2% |
| CD8 RO CCR5_CD3 | 6.0% |
| CD4 Treg_total | 6.0% |
| CD8 ncytotox RO CCR4_CD3 | 6.0% |
| Tconv memCD27_mem | 5.8% |
| CD16+mono_total | 5.8% |
| Tconv memCCR4_CD3 | 5.8% |
| CD8 RO intB7_CD8 | 5.8% |
| CD8 RO CCR6_CD3 | 5.5% |
| Tconv memPD1_mem | 5.5% |
| CD3hi_CD4neg | 5.0% |
| Tconv naive_total | 4.8% |
| CD8 RO CXCR3_total | 4.8% |
| CD8 RO PD1_total | 4.8% |
| CD8 RA_total | 4.8% |
| Tconv memCCR6_CD3 | 4.8% |
| Bcells naive_CD3neg | 4.5% |
| CCR4_CD8RO | 4.5% |
| CD56_CD8RO | 4.5% |
| Tconv memTIGIT_mem | 4.2% |
| Tconv memDR_CD3 | 4.2% |
| Tconv memCCR6_total | 4.2% |
| memory_Bcells | 4.2% |
| intB7_CD8RO | 4.0% |
| Treg naive_CD4 | 4.0% |
| Tconv memDR_total | 4.0% |
| NKCD56hi_nonTnonB | 3.8% |
| CD8 RO CCR6_total | 3.8% |
| Tconv mem_CD3 | 3.8% |
| Tconv memCCR4_total | 3.5% |
| CD8 RO PD1_CD3 | 3.5% |
| Tconv memCD27_CD3 | 3.5% |
| Tconv memintB7_total | 3.2% |
| Tconv memKi67_mem | 3.2% |
| Tconv memKi67_CD3 | 3.0% |
| Tconv memPD1_total | 3.0% |
| CD8 RO CXCR3_CD8 | 3.0% |
| CCR6_CD8RO | 3.0% |
| CD4neg_total | 2.8% |
| Tconv naive_CD3 | 2.8% |
| NKCD56hi_CD3neg | 2.8% |
| CD8 RO PD1_CD8 | 2.5% |
| CD8 RO TIGIT_CD8 | 2.5% |
| CD8 RA CCR7 naive_CD8 | 2.5% |
| Tconv memCCR5_mem | 2.5% |
| NKCD16_nonTnonB | 2.2% |
| Tconv memCCR5_Tconv | 2.2% |
| Tconv naive_Tconv | 2.2% |
| NKCD16_CD3neg | 2.2% |
| naive_Bcells | 2.2% |
| Tconv memDR_Tconv | 2.2% |
| CXCR3_CD8RO | 2.2% |
| Tconv memCCR6_Tconv | 2.0% |
| CCR5_CD8RO | 2.0% |
| CD8 RO CCR6_CD8 | 2.0% |
| Tconv memCCR4_Tconv | 2.0% |
| Tconv memTIGIT_total | 2.0% |
| Tconv memCCR6_mem | 2.0% |
| Tconv mem_Tconv | 2.0% |
| Tconv memCCR5_CD3 | 2.0% |
| CD8 RO_CD3 | 1.8% |
| CD8pos_CD3 | 1.8% |
| CD8 ncytotox RO CCR4_CD8ntox | 1.8% |
| CD8 RO CD27_CD3 | 1.8% |
| CD8 RO CCR5_CD8 | 1.8% |
| NK_nonTnonB | 1.8% |
| NK_CD3neg | 1.8% |
| CD8 RO CD27_total | 1.5% |
| TIGIT_CD8RO | 1.2% |
| CD4 Tconv_CD3 | 1.2% |
| Tconv memKi67_Tconv | 1.2% |
| Tconv memPD1_Tconv | 1.2% |
| CD8 RO TIGIT_CD3 | 1.2% |
| CD8 RO_total | 1.2% |
| CD4 Tconv_total | 1.0% |
| CD14mono_CD3neg | 1.0% |
| Tconv memTIGIT_CD3 | 1.0% |
| Tconv memCCR4_mem | 1.0% |
| Tconv memPD1_CD3 | 0.8% |
| Bcells_CD3neg | 0.8% |
| CD8pos_total | 0.8% |
| Tconv memTIGIT_Tconv | 0.8% |
| CD8 RO TIGIT_total | 0.8% |
| nonTnonB_CD3neg | 0.8% |
| CD8 RO_CD8 | 0.8% |
| CD8 RA_CD8 | 0.8% |
| CD8 RO CD27_CD8 | 0.8% |
| PD1_CD8RO | 0.5% |
| myeloid_CD3neg | 0.5% |
| Tconv memCD27_total | 0.5% |
| CD14mono_total | 0.5% |
| CD3neg_total | 0.2% |
| CD3pos_total | 0.2% |
| CD4 Tconv mem_total | 0.2% |

### RFE (RandomForest)

**Base Method**: Raw feature selection frequencies across all bootstrap samples

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Bcells CD27posIgDneg_total | 96.0% |
| CD8 RO DR_CD3 | 89.5% |
| CD27IgD_Bcells | 88.2% |
| CD16mono_myeloid | 87.2% |
| CD16mono_CD3neg | 83.5% |
| CD4 Treg_CD4 | 83.0% |
| Tconv naive_total | 82.2% |
| Tconv memDR_mem | 79.0% |
| Tconv mem_Tconv | 77.8% |
| Tconv naive_CD3 | 77.5% |
| DR_CD8RO | 77.5% |
| CD8 RO DR_CD8 | 77.0% |
| Treg memory_CD4 | 76.0% |
| Tconv naive_Tconv | 75.5% |
| Tconv memDR_Tconv | 75.0% |
| Bcells_CD3neg | 72.2% |
| nonTnonB_CD3neg | 70.0% |
| Tconv memCD27_Tconv | 70.0% |
| Tconv memCXCR3_mem | 69.2% |
| Tconv memDR_CD3 | 69.2% |
| Bcells memory_CD3neg | 69.2% |
| CD8 RO PD1_CD3 | 69.0% |
| CD14mono_myeloid | 68.8% |
| naive_Bcells | 68.5% |
| Tconv memPD1_total | 68.2% |
| CD8  RO Ki67_CD3 | 68.0% |
| Tconv memCXCR3_Tconv | 67.8% |
| CD3hi_total | 67.8% |
| CD8 RO DR_total | 67.8% |
| Treg memory_CD3 | 67.2% |
| CD4 Treg _CD3 | 67.2% |
| Ki67_Bcells | 66.8% |
| Tconv memPD1_mem | 66.0% |
| memory_Bcells | 65.5% |
| CD16+mono_total | 64.8% |
| CD8 RO CCR5_CD3 | 64.8% |
| CCR5_CD8RO | 64.8% |
| CD4 Tconv_total | 64.2% |
| CD8pos_CD3 | 63.5% |
| CD56_CD8RO | 63.5% |
| Bcells naive_CD3neg | 63.5% |
| Tconv memTIGIT_mem | 63.2% |
| Tconv memCCR6_Tconv | 63.0% |
| CD8 RO CD56_CD3 | 62.7% |
| NKCD56hi_nonTnonB | 62.3% |
| CD8 RA CCR7 naive_CD8 | 62.0% |
| Tconv memCCR5_mem | 62.0% |
| NKCD16_NK | 62.0% |
| CD14+16+mono_myeloid | 62.0% |
| CD27_CD8RO | 61.8% |
| Tconv memCCR6_mem | 61.8% |
| CD27negIgDneg_Bcells | 61.0% |
| NKCD56hi_NK | 60.8% |
| intB7_CD8RO | 60.8% |
| CD8 RO CXCR3_CD3 | 60.8% |
| CD8 RO CXCR3_CD8 | 60.5% |
| Tconv memCCR6_CD3 | 60.2% |
| Tconv memCXCR3_CD3 | 60.0% |
| CD8 RO CD56_CD8 | 59.8% |
| CXCR3_CD8RO | 59.8% |
| NKCD56hi_total | 59.5% |
| Bcells Ki67_total | 59.2% |
| NK Ki67_nonTnonB | 59.2% |
| CD3neg_total | 59.0% |
| CD8 RO CCR5_total | 59.0% |
| nonTnonB_total | 59.0% |
| Bcells_total | 59.0% |
| Tconv memCD56_mem | 58.8% |
| CD8 RA naive_CD3 | 58.8% |
| Tconv memPD1_Tconv | 58.8% |
| CD3pos_total | 58.5% |
| CD14mono_CD3neg | 58.2% |
| CD3hi_CD3 | 58.2% |
| CCR6_CD8RO | 58.2% |
| Bcells Ki67_CD3neg | 58.2% |
| CD4neg_CD3 | 58.0% |
| TIGIT_CD8RO | 57.8% |
| NK Ki67_NK | 57.8% |
| CD8 RO CCR5_CD8 | 57.5% |
| Tconv memCCR4_total | 57.5% |
| Tconv memKi67_mem | 57.2% |
| Tconv memCD27_mem | 57.0% |
| CD8 RO PD1_CD8 | 56.8% |
| Tconv memPD1_CD3 | 56.5% |
| CD8 RA_CD3 | 56.5% |
| NKCD56hi_CD3neg | 56.2% |
| CCR4_CD8RO | 56.2% |
| PD1_CD8RO | 56.2% |
| Tconv memCD27_CD3 | 56.0% |
| Tconv memCCR4_Tconv | 55.8% |
| Bcells memory_total | 55.8% |
| CD3hi_CD4neg | 55.5% |
| Ki67_CD8RO | 55.2% |
| CD4 Tconv_CD3 | 55.2% |
| CD8 RO TIGIT_CD3 | 55.0% |
| CD8 RO_CD3 | 55.0% |
| Tconv memTIGIT_total | 55.0% |
| CD8 ncytotox RO CCR4_CD8ntox | 55.0% |
| NK_CD3neg | 54.8% |
| NKCD16_CD3neg | 54.5% |
| Tconv memCCR4_mem | 54.2% |
| Tconv memKi67_total | 54.0% |
| Tconv memCCR6_total | 53.8% |
| Treg naive_CD4 | 53.8% |
| NKCD16_total | 53.5% |
| Tconv mem_CD3 | 53.5% |
| Tconv memCD56_Tconv | 53.2% |
| Bcells CD27negIgDneg_total | 53.0% |
| CD14+16+mono_CD3neg | 52.8% |
| Tconv memintB7_Tconv | 52.8% |
| Tconv memCCR5_total | 52.8% |
| CD4 Treg_total | 52.0% |
| CD8 RO CD56_total | 51.7% |
| Tconv memDR_total | 51.7% |
| Tconv memTIGIT_Tconv | 51.7% |
| CD8 RA_CD8 | 51.7% |
| CD8 RO CD27_CD3 | 51.5% |
| CD8 RO Ki67_CD8 | 51.2% |
| CD14mono_total | 50.7% |
| Tconv memintB7_mem | 50.2% |
| Bcells naive_total | 50.2% |
| Treg memory_total | 49.8% |
| CD8 RO TIGIT_CD8 | 49.8% |
| CD8 RO intB7_CD8 | 49.5% |
| NK_total | 49.5% |
| myeloid_total | 49.5% |
| NK_nonTnonB | 49.5% |
| NK Ki67_CD3neg | 49.5% |
| Tconv memintB7_total | 49.5% |
| Tconv memCCR5_Tconv | 49.2% |
| Tconv memCXCR3_total | 49.0% |
| CD8 RO CCR6_CD8 | 49.0% |
| CD8 ncytotox RO CCR4_CD3 | 49.0% |
| Tconv memCCR5_CD3 | 49.0% |
| CD8 RO PD1_total | 49.0% |
| CD14+16+mono_total | 49.0% |
| CD8 RO CCR6_CD3 | 49.0% |
| Tconv memCCR4_CD3 | 48.8% |
| Tconv memCD56_total | 48.5% |
| NKCD16_nonTnonB | 48.5% |
| Tconv memCD56_CD3 | 48.2% |
| Tconv memTIGIT_CD3 | 47.8% |
| CD4 Tconv mem_total | 47.8% |
| NK Ki67_total | 47.8% |
| myeloid_CD3neg | 47.2% |
| CD8 RO CD27_CD8 | 47.2% |
| Tconv memKi67_Tconv | 47.0% |
| CD8 RO intB7_CD3 | 47.0% |
| CD8 RO_CD8 | 47.0% |
| CD8 RA_total | 46.5% |
| Treg naive_total | 46.5% |
| Treg naive_CD3 | 46.0% |
| CD8 RO CXCR3_total | 45.2% |
| CD8pos_total | 44.5% |
| Tconv memintB7_CD3 | 44.0% |
| Tconv memCD27_total | 43.2% |
| CD8 RO Ki67_total | 43.0% |
| Tconv memKi67_CD3 | 42.2% |
| CD4neg_total | 41.5% |
| CD8 RO CCR6_total | 40.5% |
| CD8 RA naive_total | 40.5% |
| CD8 RO CCR4_total | 39.5% |
| CD8 RO TIGIT_total | 38.8% |
| CD8 RO intB7_total | 38.0% |
| CD8 RO_total | 35.2% |
| CD8 RO CD27_total | 33.5% |

### RF_Importance

**Base Method**: Raw feature selection frequencies across all bootstrap samples

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Bcells CD27posIgDneg_total | 89.5% |
| CD8 RO DR_CD3 | 82.0% |
| CD27IgD_Bcells | 79.8% |
| Tconv naive_total | 75.5% |
| CD16mono_myeloid | 74.8% |
| CD4 Treg_CD4 | 74.0% |
| Tconv mem_Tconv | 70.5% |
| Treg memory_CD4 | 68.8% |
| Tconv naive_CD3 | 68.8% |
| Tconv naive_Tconv | 63.2% |
| CD16mono_CD3neg | 62.0% |
| Tconv memDR_mem | 60.2% |
| Tconv memDR_Tconv | 58.2% |
| CD8 RO DR_CD8 | 57.2% |
| Tconv memCD27_Tconv | 55.0% |
| DR_CD8RO | 54.2% |
| Tconv memDR_CD3 | 54.0% |
| Treg memory_CD3 | 53.2% |
| CD4 Tconv_total | 52.2% |
| Tconv memPD1_total | 51.5% |
| Bcells_CD3neg | 49.8% |
| Bcells memory_CD3neg | 48.5% |
| CD4 Treg _CD3 | 47.2% |
| nonTnonB_total | 46.8% |
| CD3neg_total | 46.2% |
| CD8pos_CD3 | 46.2% |
| Tconv memCXCR3_Tconv | 45.2% |
| CD8  RO Ki67_CD3 | 45.0% |
| CD8 RO PD1_CD3 | 44.8% |
| nonTnonB_CD3neg | 44.5% |
| CD8 RO DR_total | 43.8% |
| CD14mono_myeloid | 43.2% |
| Ki67_Bcells | 43.2% |
| CD8 RO CD56_CD3 | 42.5% |
| CD3hi_total | 42.2% |
| CD3pos_total | 41.5% |
| CD8 RO CCR5_CD3 | 40.0% |
| CD8 RO CXCR3_CD3 | 39.5% |
| CD16+mono_total | 39.5% |
| Tconv memCXCR3_mem | 39.2% |
| naive_Bcells | 39.2% |
| Bcells_total | 39.0% |
| CD8 RA CCR7 naive_CD8 | 38.8% |
| CD4 Tconv_CD3 | 37.2% |
| CD8 RO TIGIT_CD3 | 36.8% |
| CD14mono_total | 36.8% |
| CD8 RA naive_CD3 | 36.5% |
| Tconv memCXCR3_CD3 | 36.0% |
| Bcells memory_total | 36.0% |
| Tconv memCCR6_Tconv | 35.8% |
| CD8 RO CCR5_total | 35.5% |
| CCR5_CD8RO | 35.5% |
| CD3hi_CD3 | 34.2% |
| Tconv memCCR5_mem | 34.0% |
| Tconv memCD27_CD3 | 34.0% |
| Tconv memTIGIT_total | 33.8% |
| Tconv mem_CD3 | 33.2% |
| NKCD56hi_nonTnonB | 32.8% |
| Tconv memPD1_mem | 32.8% |
| CD8 RO_CD3 | 32.5% |
| CD56_CD8RO | 32.5% |
| Tconv memTIGIT_mem | 32.2% |
| CD4neg_CD3 | 32.2% |
| CD8 RA_CD3 | 32.0% |
| CD14mono_CD3neg | 31.8% |
| Tconv memKi67_total | 31.8% |
| Tconv memCD27_mem | 31.5% |
| NKCD56hi_total | 31.2% |
| NKCD56hi_NK | 31.0% |
| CD8 RO CXCR3_CD8 | 30.8% |
| Bcells naive_CD3neg | 30.8% |
| NKCD16_NK | 30.5% |
| NKCD16_total | 30.2% |
| CD14+16+mono_myeloid | 30.0% |
| memory_Bcells | 30.0% |
| Tconv memintB7_Tconv | 29.8% |
| CD8 RO CCR5_CD8 | 29.5% |
| Tconv memCCR4_Tconv | 29.5% |
| Tconv memCCR4_total | 29.5% |
| Tconv memCCR6_mem | 29.2% |
| Tconv memCCR6_total | 29.0% |
| Treg naive_total | 29.0% |
| Tconv memPD1_CD3 | 28.7% |
| CD14+16+mono_total | 28.7% |
| Tconv memCCR6_CD3 | 28.7% |
| CD27negIgDneg_Bcells | 28.5% |
| myeloid_total | 27.8% |
| Tconv memCD56_Tconv | 27.5% |
| Tconv memKi67_mem | 27.3% |
| CD8pos_total | 27.0% |
| Tconv memCCR5_total | 26.8% |
| Tconv memCCR4_CD3 | 26.5% |
| CD4 Treg_total | 26.5% |
| Tconv memDR_total | 26.0% |
| Tconv memCCR4_mem | 25.8% |
| NKCD56hi_CD3neg | 25.8% |
| Tconv memCXCR3_total | 25.5% |
| CD8 RO CD56_CD8 | 25.5% |
| CD4 Tconv mem_total | 25.0% |
| NK_total | 24.8% |
| Ki67_CD8RO | 24.8% |
| intB7_CD8RO | 24.8% |
| TIGIT_CD8RO | 24.8% |
| CD8 ncytotox RO CCR4_CD8ntox | 24.8% |
| NK Ki67_NK | 24.2% |
| CD27_CD8RO | 24.0% |
| Tconv memCD27_total | 24.0% |
| CD3hi_CD4neg | 23.8% |
| Tconv memintB7_total | 23.8% |
| CXCR3_CD8RO | 23.8% |
| CD8 RO CD27_CD3 | 23.5% |
| Bcells naive_total | 23.5% |
| Treg naive_CD4 | 23.5% |
| Bcells Ki67_CD3neg | 23.5% |
| NK Ki67_total | 23.2% |
| CD8 RO CD56_total | 23.2% |
| CD8 RO PD1_CD8 | 23.0% |
| Bcells CD27negIgDneg_total | 23.0% |
| Tconv memTIGIT_Tconv | 22.8% |
| Tconv memCD56_mem | 22.8% |
| Tconv memPD1_Tconv | 22.5% |
| Bcells Ki67_total | 22.5% |
| CD8 RO TIGIT_CD8 | 22.5% |
| NKCD16_CD3neg | 22.5% |
| CD8 RA_total | 22.0% |
| PD1_CD8RO | 22.0% |
| CD8 RO CD27_CD8 | 22.0% |
| CCR4_CD8RO | 22.0% |
| CCR6_CD8RO | 22.0% |
| CD8 RA naive_total | 22.0% |
| CD8 RO CXCR3_total | 21.8% |
| CD8 RO CCR6_CD3 | 21.8% |
| NK Ki67_CD3neg | 21.8% |
| Tconv memTIGIT_CD3 | 21.8% |
| Tconv memCD56_total | 21.8% |
| Tconv memKi67_Tconv | 21.5% |
| CD8 RO PD1_total | 21.5% |
| Tconv memCD56_CD3 | 21.5% |
| Treg naive_CD3 | 21.2% |
| Tconv memCCR5_Tconv | 21.2% |
| CD8 RA_CD8 | 21.0% |
| NK Ki67_nonTnonB | 20.8% |
| NK_CD3neg | 20.5% |
| NKCD16_nonTnonB | 20.5% |
| Tconv memintB7_mem | 20.2% |
| CD14+16+mono_CD3neg | 19.5% |
| Treg memory_total | 18.5% |
| Tconv memCCR5_CD3 | 18.5% |
| CD8 ncytotox RO CCR4_CD3 | 18.0% |
| CD8 RO TIGIT_total | 17.8% |
| Tconv memKi67_CD3 | 17.5% |
| Tconv memintB7_CD3 | 17.5% |
| CD8 RO CCR4_total | 17.5% |
| CD8 RO intB7_CD3 | 17.2% |
| CD8 RO CCR6_CD8 | 17.2% |
| CD8 RO CCR6_total | 16.8% |
| CD8 RO Ki67_CD8 | 16.0% |
| NK_nonTnonB | 15.5% |
| myeloid_CD3neg | 15.2% |
| CD8 RO Ki67_total | 15.2% |
| CD8 RO intB7_CD8 | 15.0% |
| CD8 RO intB7_total | 14.8% |
| CD4neg_total | 14.5% |
| CD8 RO_CD8 | 14.2% |
| CD8 RO_total | 13.5% |
| CD8 RO CD27_total | 10.5% |

### RandomForest_Permutation_AboveMean

**Base Method**: Raw feature selection frequencies across all bootstrap samples

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Tconv memDR_Tconv | 10.8% |
| Bcells CD27posIgDneg_total | 10.8% |
| Tconv memCXCR3_Tconv | 10.5% |
| CD8 RO DR_CD3 | 10.2% |
| Bcells naive_CD3neg | 10.2% |
| CD3hi_CD4neg | 10.0% |
| Tconv naive_Tconv | 10.0% |
| NKCD16_NK | 9.8% |
| CD4 Tconv_CD3 | 9.8% |
| Tconv memCXCR3_mem | 9.5% |
| CD4neg_CD3 | 9.5% |
| Bcells_total | 9.5% |
| Tconv naive_CD3 | 9.5% |
| NK_CD3neg | 9.5% |
| Treg memory_CD4 | 9.5% |
| Tconv memTIGIT_mem | 9.2% |
| CD8 RO CCR6_CD8 | 9.2% |
| CD3hi_total | 9.2% |
| CD8 RO DR_CD8 | 9.2% |
| Tconv mem_CD3 | 9.0% |
| CD8 RO CXCR3_CD8 | 9.0% |
| CD27IgD_Bcells | 9.0% |
| Tconv memDR_CD3 | 9.0% |
| Bcells memory_total | 9.0% |
| NK_nonTnonB | 8.8% |
| CD4 Treg_CD4 | 8.8% |
| Tconv memCCR6_Tconv | 8.5% |
| CD8 RO intB7_CD3 | 8.5% |
| CCR5_CD8RO | 8.5% |
| Tconv memintB7_total | 8.5% |
| CD8pos_CD3 | 8.5% |
| NKCD16_CD3neg | 8.5% |
| CD8 RO CCR5_total | 8.2% |
| Treg memory_total | 8.2% |
| CD56_CD8RO | 8.2% |
| Ki67_CD8RO | 8.2% |
| CD8pos_total | 8.2% |
| CD16mono_myeloid | 8.2% |
| CD8 RA_CD3 | 8.2% |
| Tconv memintB7_mem | 8.2% |
| CD8 RO TIGIT_total | 8.2% |
| CCR6_CD8RO | 8.2% |
| Tconv memTIGIT_Tconv | 8.2% |
| CD3neg_total | 8.2% |
| CD16mono_CD3neg | 8.0% |
| Tconv memCCR6_CD3 | 8.0% |
| CD8 RA_CD8 | 8.0% |
| Tconv memDR_total | 8.0% |
| CD27_CD8RO | 7.8% |
| Tconv memDR_mem | 7.8% |
| CD3hi_CD3 | 7.8% |
| TIGIT_CD8RO | 7.8% |
| NKCD56hi_nonTnonB | 7.8% |
| CD14mono_total | 7.8% |
| Tconv memKi67_mem | 7.8% |
| Tconv memCD27_total | 7.8% |
| Bcells naive_total | 7.8% |
| CD4 Tconv_total | 7.8% |
| Treg naive_CD4 | 7.8% |
| CD16+mono_total | 7.5% |
| Tconv memCD56_total | 7.5% |
| CD8 RO PD1_CD3 | 7.5% |
| CD8 RO CCR4_total | 7.5% |
| Tconv memCD27_Tconv | 7.5% |
| Tconv memKi67_total | 7.5% |
| CD8 RO CCR5_CD3 | 7.5% |
| CD27negIgDneg_Bcells | 7.5% |
| NKCD56hi_NK | 7.5% |
| NK Ki67_total | 7.5% |
| Tconv memTIGIT_total | 7.5% |
| Tconv memTIGIT_CD3 | 7.5% |
| Ki67_Bcells | 7.2% |
| Treg memory_CD3 | 7.2% |
| CD8 RA_total | 7.2% |
| PD1_CD8RO | 7.2% |
| CD8 ncytotox RO CCR4_CD3 | 7.2% |
| NK_total | 7.2% |
| Bcells_CD3neg | 7.2% |
| CD4 Treg_total | 7.2% |
| CD8 RO CCR6_CD3 | 7.2% |
| Tconv memCXCR3_CD3 | 7.2% |
| nonTnonB_CD3neg | 7.2% |
| Tconv memCCR6_total | 7.2% |
| Bcells memory_CD3neg | 7.2% |
| Tconv memCCR5_total | 7.2% |
| CD14mono_CD3neg | 7.2% |
| CD8 RA CCR7 naive_CD8 | 7.0% |
| Tconv memCD56_CD3 | 7.0% |
| Tconv memCXCR3_total | 7.0% |
| CD8 RO Ki67_CD8 | 7.0% |
| Bcells Ki67_total | 7.0% |
| NK Ki67_NK | 7.0% |
| CD8 RO DR_total | 7.0% |
| CD8 RA naive_CD3 | 7.0% |
| CD4 Treg _CD3 | 7.0% |
| CD8 RO intB7_CD8 | 7.0% |
| CD8 RO CCR6_total | 7.0% |
| Tconv memCD27_CD3 | 7.0% |
| CD8 RO CD27_total | 7.0% |
| CXCR3_CD8RO | 7.0% |
| DR_CD8RO | 7.0% |
| NKCD16_nonTnonB | 7.0% |
| CD4 Tconv mem_total | 6.8% |
| CD8 RO CD56_CD8 | 6.8% |
| Tconv mem_Tconv | 6.8% |
| CCR4_CD8RO | 6.8% |
| CD8 RO CD27_CD3 | 6.8% |
| nonTnonB_total | 6.8% |
| Tconv memPD1_mem | 6.8% |
| CD8 RO_total | 6.8% |
| CD8 RO CD56_CD3 | 6.8% |
| CD3pos_total | 6.8% |
| myeloid_CD3neg | 6.5% |
| naive_Bcells | 6.5% |
| CD14+16+mono_myeloid | 6.5% |
| CD14+16+mono_total | 6.5% |
| Tconv memCD56_Tconv | 6.5% |
| NKCD56hi_total | 6.5% |
| CD8 RO CXCR3_CD3 | 6.5% |
| CD8  RO Ki67_CD3 | 6.5% |
| CD8 ncytotox RO CCR4_CD8ntox | 6.2% |
| CD4neg_total | 6.2% |
| CD8 RO PD1_CD8 | 6.2% |
| Tconv memPD1_Tconv | 6.2% |
| Tconv memCCR4_Tconv | 6.2% |
| Tconv memCCR4_CD3 | 6.2% |
| intB7_CD8RO | 6.0% |
| Tconv memintB7_CD3 | 6.0% |
| Tconv memCCR4_mem | 6.0% |
| CD8 RO CCR5_CD8 | 6.0% |
| CD8 RA naive_total | 6.0% |
| CD8 RO_CD8 | 6.0% |
| Tconv memPD1_total | 6.0% |
| CD8 RO_CD3 | 6.0% |
| Treg naive_total | 6.0% |
| Tconv memKi67_Tconv | 6.0% |
| Tconv memCD56_mem | 6.0% |
| Tconv memCD27_mem | 6.0% |
| Tconv memCCR5_mem | 6.0% |
| Tconv memCCR5_CD3 | 6.0% |
| CD8 RO PD1_total | 6.0% |
| CD8 RO CD27_CD8 | 5.8% |
| CD8 RO Ki67_total | 5.8% |
| CD8 RO CXCR3_total | 5.8% |
| NKCD16_total | 5.8% |
| Tconv memCCR5_Tconv | 5.8% |
| CD14mono_myeloid | 5.8% |
| NKCD56hi_CD3neg | 5.8% |
| Treg naive_CD3 | 5.8% |
| NK Ki67_nonTnonB | 5.8% |
| Tconv memPD1_CD3 | 5.5% |
| memory_Bcells | 5.5% |
| Tconv memintB7_Tconv | 5.5% |
| Tconv memCCR6_mem | 5.5% |
| CD8 RO CD56_total | 5.2% |
| Tconv naive_total | 5.2% |
| Bcells CD27negIgDneg_total | 5.2% |
| CD8 RO intB7_total | 5.2% |
| CD8 RO TIGIT_CD3 | 5.2% |
| CD8 RO TIGIT_CD8 | 5.0% |
| Tconv memKi67_CD3 | 5.0% |
| Tconv memCCR4_total | 4.8% |
| myeloid_total | 4.8% |
| CD14+16+mono_CD3neg | 4.5% |
| NK Ki67_CD3neg | 4.5% |
| Bcells Ki67_CD3neg | 4.2% |

### RandomForest_Permutation_Top10%

**Base Method**: Raw feature selection frequencies across all bootstrap samples

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Tconv memKi67_total | 65.0% |
| Tconv memintB7_total | 62.7% |
| Tconv memCD27_total | 59.8% |
| Tconv memCCR6_total | 58.5% |
| Tconv memCD56_total | 57.2% |
| Tconv memPD1_total | 55.8% |
| Tconv memDR_total | 53.5% |
| Tconv naive_total | 50.5% |
| Tconv memCXCR3_total | 49.5% |
| Tconv memTIGIT_total | 45.0% |
| Tconv memCCR5_total | 39.8% |
| CD4 Treg_total | 36.5% |
| CD3pos_total | 25.8% |
| CD4 Tconv mem_total | 23.5% |
| Tconv memCCR4_total | 18.2% |
| CD4 Tconv_total | 17.8% |
| Bcells CD27posIgDneg_total | 9.0% |
| CD8 RO DR_CD3 | 9.0% |
| Tconv memDR_Tconv | 9.0% |
| Tconv memCXCR3_mem | 8.8% |
| CD3hi_CD4neg | 8.5% |
| Tconv memCXCR3_Tconv | 8.5% |
| CD4 Tconv_CD3 | 8.2% |
| CD8 RO DR_CD8 | 8.2% |
| Bcells naive_CD3neg | 8.0% |
| NKCD16_NK | 8.0% |
| Tconv naive_Tconv | 8.0% |
| Tconv memTIGIT_mem | 7.8% |
| CD8 RO CXCR3_CD8 | 7.8% |
| CCR6_CD8RO | 7.8% |
| CD8pos_CD3 | 7.8% |
| CD4 Treg_CD4 | 7.8% |
| CD8 RO CCR6_CD8 | 7.5% |
| Treg memory_CD4 | 7.5% |
| Treg memory_total | 7.5% |
| Bcells memory_total | 7.5% |
| Tconv memCCR6_Tconv | 7.5% |
| CCR5_CD8RO | 7.5% |
| Tconv naive_CD3 | 7.5% |
| CD8 RO TIGIT_total | 7.5% |
| NK_CD3neg | 7.5% |
| CD4neg_CD3 | 7.5% |
| CD8 RA_CD8 | 7.2% |
| CD56_CD8RO | 7.2% |
| Tconv memTIGIT_Tconv | 7.2% |
| CD27IgD_Bcells | 7.2% |
| Bcells_total | 7.0% |
| CD27_CD8RO | 7.0% |
| CD3neg_total | 7.0% |
| CD8 RO CCR5_total | 7.0% |
| Ki67_CD8RO | 6.8% |
| Tconv memDR_mem | 6.8% |
| Tconv mem_CD3 | 6.8% |
| CD8 RO CCR5_CD3 | 6.5% |
| CD8 RA_CD3 | 6.5% |
| Tconv memDR_CD3 | 6.5% |
| CD3hi_total | 6.5% |
| Tconv memCCR6_CD3 | 6.5% |
| CD8 RO DR_total | 6.5% |
| Tconv memKi67_mem | 6.5% |
| NK_total | 6.5% |
| CD8 RO CCR4_total | 6.5% |
| Tconv memintB7_mem | 6.5% |
| CD8pos_total | 6.5% |
| CD8 RO intB7_CD3 | 6.5% |
| Treg naive_CD4 | 6.2% |
| CD8 ncytotox RO CCR4_CD3 | 6.2% |
| NKCD16_CD3neg | 6.2% |
| CD16mono_myeloid | 6.2% |
| Bcells naive_total | 6.2% |
| CD16+mono_total | 6.0% |
| CD8 RO_total | 6.0% |
| CD8 RA CCR7 naive_CD8 | 6.0% |
| NK Ki67_total | 6.0% |
| nonTnonB_CD3neg | 6.0% |
| Tconv memCD56_Tconv | 6.0% |
| Tconv memPD1_mem | 6.0% |
| Tconv memCD27_Tconv | 6.0% |
| Bcells_CD3neg | 6.0% |
| NK_nonTnonB | 6.0% |
| CD14mono_total | 6.0% |
| CD8 RO CCR6_CD3 | 5.8% |
| CD16mono_CD3neg | 5.8% |
| CD27negIgDneg_Bcells | 5.8% |
| Tconv memCD56_CD3 | 5.8% |
| CD8 RO PD1_CD3 | 5.8% |
| CD8 RO CD56_CD3 | 5.8% |
| CD8 ncytotox RO CCR4_CD8ntox | 5.8% |
| CD8 RA_total | 5.8% |
| CD14mono_CD3neg | 5.8% |
| CD14+16+mono_total | 5.8% |
| nonTnonB_total | 5.8% |
| NKCD56hi_NK | 5.8% |
| Tconv mem_Tconv | 5.8% |
| CCR4_CD8RO | 5.8% |
| CD8 RO_CD3 | 5.8% |
| DR_CD8RO | 5.8% |
| Tconv memCCR4_mem | 5.5% |
| TIGIT_CD8RO | 5.5% |
| NKCD16_nonTnonB | 5.5% |
| CD3hi_CD3 | 5.5% |
| PD1_CD8RO | 5.5% |
| Tconv memCCR5_mem | 5.5% |
| CD8 RO CCR5_CD8 | 5.5% |
| Tconv memTIGIT_CD3 | 5.5% |
| CXCR3_CD8RO | 5.5% |
| CD8 RO CD27_total | 5.5% |
| NKCD56hi_nonTnonB | 5.5% |
| Ki67_Bcells | 5.5% |
| Treg memory_CD3 | 5.5% |
| CD8 RO intB7_CD8 | 5.5% |
| CD8 RO CD27_CD3 | 5.5% |
| CD8 RO CCR6_total | 5.5% |
| CD8 RA naive_CD3 | 5.2% |
| CD8 RO Ki67_CD8 | 5.2% |
| CD8 RO CD56_CD8 | 5.2% |
| CD8 RA naive_total | 5.2% |
| Tconv memCD27_mem | 5.2% |
| Bcells memory_CD3neg | 5.2% |
| CD8 RO CXCR3_CD3 | 5.2% |
| CD8  RO Ki67_CD3 | 5.2% |
| CD8 RO PD1_total | 5.2% |
| CD4 Treg _CD3 | 5.0% |
| CD8 RO_CD8 | 5.0% |
| Tconv memCXCR3_CD3 | 5.0% |
| Tconv memCD56_mem | 5.0% |
| myeloid_CD3neg | 5.0% |
| CD8 RO CXCR3_total | 5.0% |
| naive_Bcells | 5.0% |
| Tconv memCCR6_mem | 5.0% |
| NK Ki67_NK | 5.0% |
| Treg naive_total | 5.0% |
| CD8 RO CD27_CD8 | 4.8% |
| Bcells Ki67_total | 4.8% |
| CD8 RO TIGIT_CD3 | 4.8% |
| Tconv memCCR5_CD3 | 4.8% |
| CD8 RO PD1_CD8 | 4.8% |
| NKCD56hi_total | 4.8% |
| Tconv memCD27_CD3 | 4.8% |
| Tconv memCCR5_Tconv | 4.5% |
| CD4neg_total | 4.5% |
| CD14+16+mono_myeloid | 4.5% |
| Tconv memintB7_CD3 | 4.5% |
| CD8 RO Ki67_total | 4.5% |
| CD8 RO CD56_total | 4.5% |
| Treg naive_CD3 | 4.5% |
| CD8 RO intB7_total | 4.5% |
| CD8 RO TIGIT_CD8 | 4.2% |
| intB7_CD8RO | 4.2% |
| Tconv memPD1_CD3 | 4.2% |
| NKCD16_total | 4.2% |
| NK Ki67_nonTnonB | 4.2% |
| Tconv memCCR4_Tconv | 4.2% |
| CD14mono_myeloid | 4.2% |
| Tconv memPD1_Tconv | 4.2% |
| Tconv memCCR4_CD3 | 4.2% |
| Tconv memintB7_Tconv | 4.2% |
| Bcells CD27negIgDneg_total | 4.0% |
| myeloid_total | 4.0% |
| NKCD56hi_CD3neg | 4.0% |
| memory_Bcells | 3.8% |
| CD14+16+mono_CD3neg | 3.5% |
| Tconv memKi67_Tconv | 3.5% |
| Tconv memKi67_CD3 | 3.5% |
| NK Ki67_CD3neg | 3.5% |
| Bcells Ki67_CD3neg | 2.8% |

### Ridge_Strict

**Base Method**: Raw feature selection frequencies across all bootstrap samples

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| DR_CD8RO | 95.0% |
| CD8 RO DR_CD8 | 90.0% |
| CD16mono_myeloid | 84.0% |
| CD27IgD_Bcells | 79.2% |
| CD3hi_total | 76.0% |
| CD3hi_CD3 | 74.0% |
| Tconv memDR_total | 72.8% |
| Ki67_Bcells | 72.0% |
| CD8 RO intB7_total | 70.2% |
| CD8 RO intB7_CD8 | 69.5% |
| Bcells CD27posIgDneg_total | 68.2% |
| NKCD56hi_total | 68.0% |
| Tconv memKi67_mem | 67.8% |
| CD8 RO CD56_CD8 | 66.2% |
| CD8 RA CCR7 naive_CD8 | 64.5% |
| CD14mono_myeloid | 64.5% |
| Tconv memCCR5_mem | 64.0% |
| Tconv memPD1_mem | 63.7% |
| memory_Bcells | 63.0% |
| CD8 RA_total | 62.5% |
| CXCR3_CD8RO | 62.5% |
| Tconv memKi67_CD3 | 61.5% |
| CD8 RA_CD3 | 61.0% |
| CD8 RO CCR6_CD8 | 60.8% |
| CD16mono_CD3neg | 60.2% |
| Bcells Ki67_total | 58.8% |
| TIGIT_CD8RO | 58.5% |
| CD8 ncytotox RO CCR4_CD8ntox | 58.2% |
| CCR4_CD8RO | 57.5% |
| Bcells CD27negIgDneg_total | 57.2% |
| Bcells memory_total | 56.0% |
| CD8pos_CD3 | 55.8% |
| Tconv memCCR4_mem | 54.8% |
| intB7_CD8RO | 54.5% |
| CD14+16+mono_myeloid | 53.8% |
| CD8 RO TIGIT_CD3 | 53.8% |
| CD8 RO CCR5_total | 52.8% |
| Tconv memDR_mem | 52.2% |
| Tconv memKi67_Tconv | 52.0% |
| Tconv mem_Tconv | 51.7% |
| CD3hi_CD4neg | 51.0% |
| CD8 RA naive_total | 50.7% |
| Tconv memintB7_CD3 | 50.2% |
| CD27negIgDneg_Bcells | 50.0% |
| NKCD56hi_NK | 50.0% |
| CD8 RA naive_CD3 | 49.8% |
| Tconv memCD27_mem | 49.8% |
| NKCD16_NK | 49.2% |
| CCR5_CD8RO | 48.8% |
| Tconv memDR_CD3 | 48.5% |
| CD8 RO PD1_CD3 | 48.2% |
| Tconv memKi67_total | 48.0% |
| Tconv memCD56_total | 48.0% |
| CD8 RO CXCR3_CD8 | 48.0% |
| Tconv memCCR5_total | 47.5% |
| CD8 RO DR_CD3 | 47.5% |
| CD4neg_total | 47.2% |
| Tconv memCCR6_mem | 47.0% |
| CCR6_CD8RO | 46.5% |
| CD8 RO DR_total | 46.2% |
| CD56_CD8RO | 46.2% |
| CD8 RO PD1_total | 46.0% |
| NK Ki67_NK | 45.8% |
| Treg naive_CD4 | 45.8% |
| NK Ki67_total | 45.0% |
| CD8 RO CD56_CD3 | 44.8% |
| CD16+mono_total | 44.8% |
| Tconv memintB7_mem | 44.8% |
| Tconv memCCR6_Tconv | 44.8% |
| Tconv memDR_Tconv | 44.5% |
| Bcells Ki67_CD3neg | 44.0% |
| Tconv memCXCR3_total | 43.8% |
| PD1_CD8RO | 43.5% |
| CD8 RO CCR4_total | 43.5% |
| Treg naive_total | 43.5% |
| CD4neg_CD3 | 43.5% |
| Ki67_CD8RO | 43.2% |
| Treg memory_total | 43.0% |
| Tconv memintB7_Tconv | 42.8% |
| NKCD56hi_CD3neg | 42.0% |
| Tconv memCCR5_Tconv | 42.0% |
| CD27_CD8RO | 41.2% |
| Tconv naive_Tconv | 41.0% |
| CD8 RO Ki67_CD8 | 40.8% |
| CD14+16+mono_CD3neg | 40.5% |
| Tconv memCXCR3_mem | 40.5% |
| Bcells memory_CD3neg | 39.8% |
| Tconv memTIGIT_mem | 39.5% |
| Tconv mem_CD3 | 39.5% |
| naive_Bcells | 39.2% |
| NKCD56hi_nonTnonB | 38.8% |
| Tconv memCCR6_CD3 | 38.5% |
| Tconv memCCR6_total | 38.0% |
| CD8 RO intB7_CD3 | 37.8% |
| CD8 RO CCR5_CD3 | 37.8% |
| CD8 RO TIGIT_CD8 | 37.5% |
| CD8 RO CD56_total | 37.5% |
| Tconv memPD1_CD3 | 37.2% |
| Treg naive_CD3 | 37.0% |
| NK Ki67_nonTnonB | 37.0% |
| CD4 Treg_total | 36.5% |
| Bcells naive_CD3neg | 36.2% |
| CD8 RO PD1_CD8 | 36.0% |
| CD8 RO CXCR3_CD3 | 36.0% |
| Tconv memTIGIT_Tconv | 35.2% |
| Tconv memCCR5_CD3 | 34.5% |
| CD14+16+mono_total | 34.0% |
| NK Ki67_CD3neg | 33.8% |
| Tconv memintB7_total | 33.8% |
| CD8 RO Ki67_total | 33.2% |
| CD8 RO CD27_CD3 | 33.0% |
| Tconv memPD1_total | 33.0% |
| Bcells naive_total | 32.8% |
| CD8 RO CD27_CD8 | 32.8% |
| Tconv memPD1_Tconv | 31.5% |
| CD8 RO CCR6_CD3 | 31.0% |
| Tconv memCXCR3_Tconv | 30.2% |
| Tconv memTIGIT_total | 30.2% |
| CD8 RO_CD3 | 29.8% |
| Tconv memCXCR3_CD3 | 29.5% |
| CD8 RO CXCR3_total | 29.2% |
| CD8 RO CCR5_CD8 | 29.2% |
| Tconv memCCR4_CD3 | 28.7% |
| CD8 RO CCR6_total | 27.8% |
| Tconv memCD27_Tconv | 27.8% |
| CD8 ncytotox RO CCR4_CD3 | 27.3% |
| Tconv memCD56_CD3 | 26.5% |
| Tconv memCD56_mem | 26.5% |
| Bcells_total | 25.8% |
| Tconv memCCR4_Tconv | 25.2% |
| CD8 RA_CD8 | 25.2% |
| CD8 RO TIGIT_total | 24.8% |
| Tconv memTIGIT_CD3 | 24.8% |
| Treg memory_CD3 | 23.8% |
| Tconv memCD27_total | 23.5% |
| CD14mono_CD3neg | 23.0% |
| NK_total | 22.2% |
| Tconv memCD56_Tconv | 22.0% |
| Tconv naive_CD3 | 22.0% |
| Treg memory_CD4 | 21.2% |
| Tconv naive_total | 21.0% |
| NKCD16_total | 20.2% |
| Tconv memCCR4_total | 20.0% |
| CD8  RO Ki67_CD3 | 19.8% |
| CD8 RO_CD8 | 19.2% |
| CD8pos_total | 19.0% |
| CD4 Treg_CD4 | 19.0% |
| CD4 Treg _CD3 | 19.0% |
| Tconv memCD27_CD3 | 19.0% |
| CD8 RO CD27_total | 15.8% |
| NKCD16_nonTnonB | 15.0% |
| CD4 Tconv_CD3 | 14.8% |
| CD4 Tconv mem_total | 13.2% |
| Bcells_CD3neg | 12.2% |
| NK_nonTnonB | 11.5% |
| nonTnonB_CD3neg | 11.5% |
| myeloid_total | 10.8% |
| CD14mono_total | 10.2% |
| CD8 RO_total | 10.0% |
| NKCD16_CD3neg | 9.5% |
| CD4 Tconv_total | 8.0% |
| NK_CD3neg | 7.8% |
| CD3pos_total | 5.8% |
| CD3neg_total | 5.8% |
| myeloid_CD3neg | 1.5% |
| nonTnonB_total | 1.0% |

### SVM_RBF_Permutation_AboveMean

**Base Method**: Raw feature selection frequencies across all bootstrap samples

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CCR4_CD8RO | 44.5% |
| CD16mono_myeloid | 42.2% |
| CD27IgD_Bcells | 41.8% |
| DR_CD8RO | 41.5% |
| CD8 RO DR_CD8 | 40.5% |
| memory_Bcells | 40.0% |
| Bcells CD27posIgDneg_total | 39.8% |
| naive_Bcells | 39.5% |
| CD16mono_CD3neg | 38.2% |
| CD3hi_CD4neg | 38.0% |
| CD16+mono_total | 37.8% |
| CD3hi_total | 37.8% |
| Tconv memPD1_mem | 37.0% |
| Tconv memKi67_mem | 37.0% |
| Tconv memCCR4_mem | 36.8% |
| TIGIT_CD8RO | 36.8% |
| CD8 RA_total | 36.5% |
| CD8 ncytotox RO CCR4_CD8ntox | 36.2% |
| CD8 RO TIGIT_CD8 | 35.2% |
| Tconv memKi67_CD3 | 35.2% |
| Bcells Ki67_total | 35.2% |
| Tconv memCCR5_mem | 35.0% |
| Bcells CD27negIgDneg_total | 35.0% |
| CD27negIgDneg_Bcells | 34.8% |
| NKCD56hi_CD3neg | 34.2% |
| Tconv memTIGIT_mem | 34.0% |
| CD3hi_CD3 | 33.8% |
| Bcells memory_total | 33.8% |
| Tconv memDR_total | 33.8% |
| CD8 RA_CD3 | 33.8% |
| Treg memory_total | 33.8% |
| CD8 RA naive_total | 33.5% |
| Bcells Ki67_CD3neg | 33.2% |
| Tconv memDR_mem | 33.2% |
| Tconv memintB7_CD3 | 33.0% |
| NKCD56hi_nonTnonB | 32.5% |
| NKCD56hi_total | 32.5% |
| Tconv memCD56_total | 32.2% |
| CD4 Treg_total | 32.0% |
| Tconv memCCR5_Tconv | 32.0% |
| NK Ki67_nonTnonB | 32.0% |
| Tconv memCCR6_mem | 31.8% |
| Tconv memCCR6_CD3 | 31.8% |
| Tconv memKi67_total | 31.5% |
| Bcells naive_total | 31.5% |
| CD8 RO DR_total | 31.2% |
| intB7_CD8RO | 31.2% |
| Tconv memCD27_CD3 | 31.2% |
| NK Ki67_total | 31.2% |
| Tconv memDR_CD3 | 31.0% |
| NK Ki67_CD3neg | 30.8% |
| CCR5_CD8RO | 30.8% |
| CD8 RO DR_CD3 | 30.8% |
| Tconv memCXCR3_mem | 30.5% |
| CD8 RO CXCR3_total | 30.5% |
| CD14+16+mono_myeloid | 30.2% |
| CXCR3_CD8RO | 30.2% |
| Bcells_total | 30.2% |
| CD8 RO PD1_CD3 | 30.2% |
| Tconv memintB7_total | 30.2% |
| CCR6_CD8RO | 30.0% |
| CD8 RA naive_CD3 | 30.0% |
| CD8 RO intB7_CD3 | 29.8% |
| CD56_CD8RO | 29.8% |
| Tconv memCCR4_CD3 | 29.8% |
| Treg naive_CD3 | 29.5% |
| Tconv memPD1_CD3 | 29.5% |
| CD14+16+mono_CD3neg | 29.5% |
| Ki67_Bcells | 29.5% |
| Tconv mem_CD3 | 29.5% |
| CD8 RO PD1_CD8 | 29.5% |
| Treg naive_CD4 | 29.5% |
| CD8 RO PD1_total | 29.5% |
| Tconv memintB7_mem | 29.5% |
| NKCD16_NK | 29.2% |
| Tconv memCCR4_total | 29.2% |
| Tconv memintB7_Tconv | 29.2% |
| CD8 RO intB7_CD8 | 29.2% |
| NK Ki67_NK | 29.2% |
| Tconv memKi67_Tconv | 29.2% |
| Tconv memCCR5_CD3 | 29.2% |
| Bcells naive_CD3neg | 29.0% |
| CD8 RO CCR5_CD8 | 29.0% |
| Tconv memCXCR3_CD3 | 29.0% |
| Tconv memCCR6_Tconv | 29.0% |
| Tconv memPD1_Tconv | 29.0% |
| NKCD56hi_NK | 28.7% |
| CD4neg_total | 28.7% |
| Tconv memTIGIT_Tconv | 28.5% |
| CD8pos_total | 28.5% |
| CD8 RO CXCR3_CD8 | 28.5% |
| Tconv memCXCR3_Tconv | 28.5% |
| Tconv memCXCR3_total | 28.5% |
| CD8 RO CD27_total | 28.2% |
| CD8 RO Ki67_total | 28.2% |
| Tconv memTIGIT_CD3 | 28.2% |
| CD8 RO intB7_total | 28.0% |
| CD8 RO CXCR3_CD3 | 28.0% |
| CD4 Tconv mem_total | 27.8% |
| Tconv memCCR5_total | 27.8% |
| Ki67_CD8RO | 27.5% |
| CD8 RO CD27_CD8 | 27.5% |
| PD1_CD8RO | 27.3% |
| CD8 RO CD56_total | 27.3% |
| CD14mono_myeloid | 27.3% |
| Tconv memCD27_mem | 27.3% |
| CD8 RO TIGIT_CD3 | 27.0% |
| Tconv memPD1_total | 27.0% |
| CD8 RO CD56_CD8 | 27.0% |
| CD8 RO TIGIT_total | 27.0% |
| CD14+16+mono_total | 26.8% |
| Bcells memory_CD3neg | 26.8% |
| Tconv memCD56_Tconv | 26.5% |
| CD8 RO CCR5_CD3 | 26.5% |
| Tconv memCD56_mem | 26.5% |
| Tconv memCD56_CD3 | 26.2% |
| CD8 RA_CD8 | 26.2% |
| CD8 RO_total | 26.2% |
| CD8 RO_CD8 | 26.0% |
| CD8 RO Ki67_CD8 | 26.0% |
| nonTnonB_CD3neg | 26.0% |
| Treg naive_total | 25.8% |
| Tconv memCCR6_total | 25.8% |
| CD27_CD8RO | 25.5% |
| Bcells_CD3neg | 25.5% |
| Tconv memCD27_total | 25.5% |
| NK_CD3neg | 25.2% |
| CD8 RO CCR6_CD8 | 25.2% |
| NKCD16_nonTnonB | 25.2% |
| Tconv memCD27_Tconv | 25.2% |
| CD8 RO CCR4_total | 25.0% |
| CD8 RO CCR6_total | 25.0% |
| NKCD16_CD3neg | 25.0% |
| Tconv memDR_Tconv | 25.0% |
| NK_nonTnonB | 25.0% |
| CD8  RO Ki67_CD3 | 24.8% |
| CD8 RO CCR5_total | 24.5% |
| CD4neg_CD3 | 24.2% |
| CD8 RO CD56_CD3 | 24.2% |
| CD8 ncytotox RO CCR4_CD3 | 24.2% |
| Treg memory_CD3 | 24.2% |
| Tconv memTIGIT_total | 23.8% |
| CD8 RA CCR7 naive_CD8 | 23.5% |
| CD8 RO CD27_CD3 | 23.2% |
| CD4 Treg _CD3 | 23.2% |
| CD8pos_CD3 | 23.2% |
| CD4 Treg_CD4 | 23.0% |
| NK_total | 23.0% |
| CD8 RO CCR6_CD3 | 22.5% |
| myeloid_CD3neg | 22.2% |
| NKCD16_total | 22.0% |
| Tconv memCCR4_Tconv | 21.8% |
| Tconv mem_Tconv | 21.8% |
| Treg memory_CD4 | 21.0% |
| Tconv naive_Tconv | 21.0% |
| CD14mono_CD3neg | 20.8% |
| CD8 RO_CD3 | 20.5% |
| CD3pos_total | 20.0% |
| CD3neg_total | 20.0% |
| myeloid_total | 19.8% |
| CD4 Tconv_CD3 | 19.0% |
| nonTnonB_total | 18.2% |
| CD14mono_total | 18.2% |
| Tconv naive_total | 18.0% |
| Tconv naive_CD3 | 17.0% |
| CD4 Tconv_total | 16.0% |

### SVM_RBF_Permutation_Top10%

**Base Method**: Raw feature selection frequencies across all bootstrap samples

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD4 Treg_total | 43.2% |
| Tconv memCXCR3_total | 43.2% |
| Tconv memKi67_total | 43.2% |
| Tconv memDR_total | 42.8% |
| Tconv memCD56_total | 40.5% |
| Tconv memintB7_total | 39.0% |
| Tconv memPD1_total | 38.5% |
| Tconv memCD27_total | 38.0% |
| Tconv memTIGIT_total | 37.5% |
| Tconv naive_total | 36.8% |
| CD3pos_total | 32.2% |
| Tconv memCCR5_total | 30.8% |
| CD4 Tconv mem_total | 30.5% |
| Tconv memCCR6_total | 30.2% |
| Tconv memCCR4_total | 29.8% |
| CD4 Tconv_total | 28.7% |
| DR_CD8RO | 23.5% |
| CD8 RO DR_CD8 | 22.2% |
| CCR4_CD8RO | 20.2% |
| Bcells CD27posIgDneg_total | 18.8% |
| CD16mono_myeloid | 18.8% |
| CD3hi_total | 16.0% |
| CD16mono_CD3neg | 16.0% |
| Tconv memDR_mem | 14.5% |
| Tconv memPD1_mem | 14.2% |
| CD16+mono_total | 13.2% |
| CD8 RO DR_total | 13.0% |
| NKCD56hi_total | 13.0% |
| Treg memory_total | 12.2% |
| CD3hi_CD4neg | 12.2% |
| CD27IgD_Bcells | 12.2% |
| CD8 ncytotox RO CCR4_CD8ntox | 12.0% |
| Bcells Ki67_total | 12.0% |
| Tconv memCCR4_mem | 11.8% |
| CD8 RA_total | 11.8% |
| Tconv memTIGIT_mem | 11.8% |
| Bcells CD27negIgDneg_total | 11.5% |
| CD8 RA naive_total | 11.5% |
| CD8 RO DR_CD3 | 11.5% |
| Bcells memory_total | 11.2% |
| CD3hi_CD3 | 11.2% |
| intB7_CD8RO | 10.5% |
| NKCD56hi_CD3neg | 10.0% |
| CD27negIgDneg_Bcells | 9.5% |
| CD8 RO TIGIT_CD8 | 9.5% |
| NKCD56hi_nonTnonB | 9.2% |
| Tconv memKi67_mem | 9.2% |
| Tconv memCXCR3_mem | 9.2% |
| memory_Bcells | 9.0% |
| NKCD56hi_NK | 8.5% |
| CD8 RO Ki67_total | 8.5% |
| Tconv memCCR6_CD3 | 8.5% |
| Bcells Ki67_CD3neg | 8.5% |
| NKCD16_NK | 8.2% |
| CXCR3_CD8RO | 8.2% |
| Tconv memKi67_CD3 | 8.0% |
| CD8 RA_CD3 | 8.0% |
| CD8 RA naive_CD3 | 8.0% |
| TIGIT_CD8RO | 7.8% |
| CD56_CD8RO | 7.8% |
| Tconv memCCR6_mem | 7.8% |
| Tconv memDR_CD3 | 7.8% |
| CD14mono_myeloid | 7.8% |
| Tconv memCCR5_mem | 7.8% |
| CD8 RO CXCR3_CD8 | 7.8% |
| naive_Bcells | 7.5% |
| Treg naive_total | 7.5% |
| CD14+16+mono_total | 7.5% |
| NK Ki67_nonTnonB | 7.2% |
| CD14+16+mono_myeloid | 7.0% |
| Ki67_Bcells | 7.0% |
| CD8 RO intB7_total | 7.0% |
| Treg naive_CD4 | 6.8% |
| CD8 RO CXCR3_total | 6.8% |
| CD8 RO CD56_total | 6.8% |
| CD8 RO intB7_CD8 | 6.8% |
| Treg naive_CD3 | 6.8% |
| CD4neg_total | 6.5% |
| CD8 RO PD1_total | 6.5% |
| CD8 RO PD1_CD8 | 6.5% |
| Tconv mem_CD3 | 6.5% |
| CCR5_CD8RO | 6.5% |
| CD8 RO Ki67_CD8 | 6.2% |
| CD8 RO CCR5_CD8 | 6.2% |
| CD8 RO intB7_CD3 | 6.2% |
| Ki67_CD8RO | 6.2% |
| CD8  RO Ki67_CD3 | 6.0% |
| Tconv memintB7_Tconv | 6.0% |
| Tconv memCXCR3_Tconv | 6.0% |
| CD4 Treg _CD3 | 5.8% |
| Tconv memCCR4_CD3 | 5.8% |
| Tconv memCXCR3_CD3 | 5.8% |
| Tconv memCCR6_Tconv | 5.8% |
| CCR6_CD8RO | 5.8% |
| Treg memory_CD3 | 5.8% |
| NK Ki67_total | 5.5% |
| CD8 RO PD1_CD3 | 5.5% |
| Tconv memDR_Tconv | 5.5% |
| Tconv memCD27_CD3 | 5.5% |
| Bcells naive_total | 5.2% |
| CD8 RO TIGIT_total | 5.2% |
| Tconv memintB7_CD3 | 5.2% |
| CD8 RO CCR4_total | 5.2% |
| CD8 RO CD56_CD8 | 5.2% |
| Bcells memory_CD3neg | 5.2% |
| Tconv memintB7_mem | 5.0% |
| PD1_CD8RO | 5.0% |
| CD8 RO CD27_CD8 | 5.0% |
| Bcells naive_CD3neg | 4.8% |
| Tconv memTIGIT_Tconv | 4.8% |
| CD14+16+mono_CD3neg | 4.8% |
| NK_total | 4.8% |
| CD8 RO CCR6_CD8 | 4.8% |
| Tconv memCCR5_Tconv | 4.8% |
| Tconv memKi67_Tconv | 4.8% |
| CD8 RO CD56_CD3 | 4.8% |
| CD8pos_total | 4.5% |
| CD8 RO CD27_total | 4.5% |
| CD8 RO CCR6_total | 4.2% |
| CD27_CD8RO | 4.2% |
| Treg memory_CD4 | 4.2% |
| CD4neg_CD3 | 4.2% |
| Bcells_total | 4.2% |
| Tconv memCD56_mem | 4.2% |
| CD8 RO TIGIT_CD3 | 4.0% |
| CD8 RO_CD8 | 4.0% |
| Tconv memCD27_mem | 4.0% |
| Tconv memCCR5_CD3 | 4.0% |
| Tconv mem_Tconv | 3.8% |
| CD8 RO CXCR3_CD3 | 3.8% |
| Tconv memCD56_Tconv | 3.8% |
| Tconv memPD1_Tconv | 3.5% |
| CD8pos_CD3 | 3.5% |
| CD8 RO CCR5_total | 3.5% |
| CD8 RA_CD8 | 3.5% |
| NK Ki67_NK | 3.5% |
| CD8 RO CD27_CD3 | 3.5% |
| CD4 Treg_CD4 | 3.5% |
| Tconv memPD1_CD3 | 3.5% |
| NK Ki67_CD3neg | 3.2% |
| CD8 RO CCR5_CD3 | 3.2% |
| CD8 RO CCR6_CD3 | 3.2% |
| CD8 RO_total | 3.2% |
| CD4 Tconv_CD3 | 3.2% |
| CD8 RA CCR7 naive_CD8 | 3.2% |
| NKCD16_nonTnonB | 3.0% |
| Tconv memTIGIT_CD3 | 3.0% |
| Tconv memCD27_Tconv | 3.0% |
| Tconv naive_Tconv | 2.8% |
| NK_nonTnonB | 2.8% |
| CD3neg_total | 2.8% |
| Tconv memCD56_CD3 | 2.8% |
| NK_CD3neg | 2.5% |
| nonTnonB_total | 2.2% |
| NKCD16_total | 2.2% |
| Tconv memCCR4_Tconv | 2.0% |
| NKCD16_CD3neg | 2.0% |
| CD8 ncytotox RO CCR4_CD3 | 2.0% |
| Tconv naive_CD3 | 1.8% |
| CD8 RO_CD3 | 1.8% |
| CD14mono_CD3neg | 1.2% |
| nonTnonB_CD3neg | 1.2% |
| CD14mono_total | 1.2% |
| Bcells_CD3neg | 1.2% |
| myeloid_CD3neg | 1.0% |
| myeloid_total | 0.8% |

### XGB_Importance

**Base Method**: Raw feature selection frequencies across all bootstrap samples

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Bcells CD27posIgDneg_total | 78.8% |
| CD8 RO DR_CD3 | 61.5% |
| CD27IgD_Bcells | 59.8% |
| CD16mono_myeloid | 59.8% |
| CD16mono_CD3neg | 48.0% |
| Tconv naive_total | 41.5% |
| Tconv memDR_mem | 40.5% |
| CD4 Treg_CD4 | 38.5% |
| Ki67_Bcells | 38.5% |
| Tconv memPD1_total | 35.8% |
| CD8  RO Ki67_CD3 | 31.8% |
| CD3hi_total | 30.2% |
| NKCD56hi_total | 29.2% |
| CD16+mono_total | 27.0% |
| CD8 RO PD1_CD3 | 26.5% |
| CD3pos_total | 25.8% |
| naive_Bcells | 25.8% |
| Tconv memDR_CD3 | 25.2% |
| CD8pos_CD3 | 24.2% |
| Tconv mem_Tconv | 24.2% |
| CD8 RA naive_CD3 | 24.0% |
| Tconv naive_CD3 | 24.0% |
| NKCD16_NK | 23.5% |
| CD4 Tconv mem_total | 23.5% |
| CD8 RO DR_CD8 | 23.5% |
| nonTnonB_CD3neg | 23.5% |
| CD4 Tconv_total | 23.0% |
| Tconv memCXCR3_total | 22.2% |
| Tconv memKi67_total | 22.0% |
| Tconv memDR_total | 21.5% |
| CD8 RO CD56_CD3 | 21.5% |
| Tconv memCCR4_total | 21.5% |
| memory_Bcells | 21.2% |
| CD8 RA CCR7 naive_CD8 | 21.0% |
| Tconv memDR_Tconv | 20.2% |
| CD8 RO DR_total | 20.0% |
| CD56_CD8RO | 19.8% |
| Tconv memCD27_Tconv | 19.5% |
| NK_total | 19.2% |
| Bcells_total | 19.2% |
| CCR5_CD8RO | 19.2% |
| Tconv memTIGIT_total | 19.0% |
| Tconv memCXCR3_CD3 | 19.0% |
| DR_CD8RO | 18.8% |
| NK Ki67_total | 18.8% |
| Bcells CD27negIgDneg_total | 18.5% |
| Tconv memCCR6_mem | 18.5% |
| Tconv memPD1_mem | 18.5% |
| Tconv memCD56_total | 18.5% |
| CD8 RO CD56_total | 18.2% |
| Treg memory_CD4 | 18.2% |
| CD14+16+mono_myeloid | 17.2% |
| NK Ki67_NK | 17.0% |
| Bcells Ki67_total | 16.8% |
| CD8 RO CCR5_total | 16.5% |
| CD8 RA_CD3 | 16.5% |
| intB7_CD8RO | 16.2% |
| Tconv memTIGIT_mem | 16.2% |
| Bcells memory_total | 16.2% |
| CD3hi_CD3 | 16.0% |
| Tconv memCD27_mem | 15.8% |
| CD4 Treg_total | 15.8% |
| CD8 RA_total | 15.8% |
| CD8 RO CD56_CD8 | 15.5% |
| CD8pos_total | 15.5% |
| CD8 RO CCR5_CD3 | 15.2% |
| NKCD56hi_NK | 15.2% |
| Tconv memCCR5_mem | 15.0% |
| NKCD56hi_nonTnonB | 15.0% |
| Tconv memCD27_CD3 | 14.8% |
| Tconv memCCR4_mem | 14.8% |
| Treg naive_total | 14.8% |
| CD3hi_CD4neg | 14.8% |
| Tconv memKi67_mem | 14.5% |
| CD27_CD8RO | 14.2% |
| Tconv memCXCR3_Tconv | 14.0% |
| TIGIT_CD8RO | 14.0% |
| CD8 RO CXCR3_CD3 | 13.8% |
| Tconv memCCR5_total | 13.8% |
| Tconv memCXCR3_mem | 13.8% |
| CD8 RO PD1_CD8 | 13.8% |
| CD14mono_total | 13.5% |
| myeloid_total | 13.2% |
| Tconv memCCR6_total | 13.2% |
| CD4neg_CD3 | 13.2% |
| CD14+16+mono_total | 13.2% |
| Tconv memCCR6_Tconv | 13.0% |
| CD4 Treg _CD3 | 12.8% |
| Tconv memCCR6_CD3 | 12.8% |
| CD8 RO CCR5_CD8 | 12.8% |
| CD27negIgDneg_Bcells | 12.5% |
| NK_CD3neg | 12.5% |
| Tconv memCCR4_Tconv | 12.5% |
| CD8 RO CXCR3_CD8 | 12.5% |
| Bcells memory_CD3neg | 12.0% |
| Tconv mem_CD3 | 11.8% |
| Tconv memintB7_mem | 11.8% |
| Bcells naive_CD3neg | 11.5% |
| CD8 RO CCR4_total | 11.5% |
| CD8 RO CD27_CD8 | 11.5% |
| CCR6_CD8RO | 11.5% |
| CD8 RO Ki67_total | 11.2% |
| nonTnonB_total | 11.2% |
| Tconv memTIGIT_CD3 | 11.2% |
| Tconv memPD1_CD3 | 11.2% |
| CD14mono_myeloid | 11.2% |
| CD8 RO CCR6_CD3 | 11.2% |
| CD8 RA naive_total | 11.0% |
| CD8 RO CXCR3_total | 10.8% |
| CD8 RO CCR6_total | 10.5% |
| CD4 Tconv_CD3 | 10.5% |
| CD4neg_total | 10.2% |
| CD8 RO TIGIT_total | 10.2% |
| CD8 RO_total | 10.0% |
| Bcells naive_total | 10.0% |
| Treg memory_CD3 | 9.8% |
| CD8 RA_CD8 | 9.8% |
| CD8 RO intB7_CD8 | 9.8% |
| Treg memory_total | 9.8% |
| Ki67_CD8RO | 9.5% |
| Treg naive_CD4 | 9.5% |
| Tconv memCD56_mem | 9.5% |
| CD8 ncytotox RO CCR4_CD8ntox | 9.2% |
| CD8 RO TIGIT_CD3 | 9.2% |
| Tconv memTIGIT_Tconv | 9.2% |
| Tconv memintB7_total | 9.2% |
| Tconv memCCR4_CD3 | 9.0% |
| Tconv memintB7_Tconv | 9.0% |
| Bcells Ki67_CD3neg | 9.0% |
| CD8 RO TIGIT_CD8 | 9.0% |
| Tconv memCD56_Tconv | 8.8% |
| Tconv memintB7_CD3 | 8.8% |
| CD14mono_CD3neg | 8.8% |
| Tconv memCD56_CD3 | 8.5% |
| CD8 RO intB7_total | 8.5% |
| CD8 RO_CD3 | 8.5% |
| NKCD56hi_CD3neg | 8.5% |
| NKCD16_total | 8.2% |
| CD8 RO PD1_total | 8.2% |
| Tconv memCCR5_CD3 | 8.2% |
| CD8 RO Ki67_CD8 | 7.8% |
| CD8 RO CCR6_CD8 | 7.8% |
| Treg naive_CD3 | 7.5% |
| Tconv memCD27_total | 7.2% |
| CCR4_CD8RO | 7.2% |
| PD1_CD8RO | 7.0% |
| NK Ki67_CD3neg | 6.8% |
| Tconv memKi67_CD3 | 6.5% |
| CXCR3_CD8RO | 6.5% |
| NK Ki67_nonTnonB | 6.2% |
| CD14+16+mono_CD3neg | 5.8% |
| CD8 RO intB7_CD3 | 5.8% |
| NK_nonTnonB | 5.5% |
| CD8 ncytotox RO CCR4_CD3 | 5.0% |
| Tconv memPD1_Tconv | 4.8% |
| Tconv naive_Tconv | 4.2% |
| myeloid_CD3neg | 4.0% |
| Tconv memCCR5_Tconv | 3.5% |
| CD8 RO CD27_CD3 | 3.5% |
| Tconv memKi67_Tconv | 3.5% |
| CD8 RO_CD8 | 2.8% |
| Bcells_CD3neg | 2.2% |
| CD8 RO CD27_total | 2.2% |
| NKCD16_nonTnonB | 1.0% |
| NKCD16_CD3neg | 0.8% |

### XGBoost_Permutation_AboveMean

**Base Method**: Raw feature selection frequencies across all bootstrap samples

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Bcells CD27posIgDneg_total | 31.2% |
| CD16mono_myeloid | 19.8% |
| CD8 RO DR_CD3 | 14.2% |
| Tconv naive_total | 7.8% |
| Ki67_Bcells | 7.2% |
| CD27IgD_Bcells | 7.0% |
| CD16mono_CD3neg | 6.0% |
| Tconv memPD1_total | 5.5% |
| CD8  RO Ki67_CD3 | 4.5% |
| Tconv memDR_mem | 4.0% |
| CD4 Treg_CD4 | 3.8% |
| Tconv mem_Tconv | 3.2% |
| NKCD56hi_nonTnonB | 3.2% |
| CD8 RO CD56_CD3 | 2.8% |
| Treg memory_CD4 | 2.8% |
| Tconv memDR_Tconv | 2.5% |
| CD8pos_CD3 | 2.5% |
| Tconv memKi67_mem | 2.2% |
| Tconv memCCR6_total | 2.2% |
| Tconv memCCR4_total | 2.2% |
| CD3hi_total | 2.2% |
| CD8 RA CCR7 naive_CD8 | 2.2% |
| NKCD16_NK | 2.2% |
| CD8 RA_CD3 | 2.0% |
| Treg naive_total | 2.0% |
| TIGIT_CD8RO | 2.0% |
| CD3hi_CD3 | 2.0% |
| Tconv naive_CD3 | 2.0% |
| DR_CD8RO | 2.0% |
| CD8 RO CCR5_total | 1.8% |
| CD8 RO Ki67_CD8 | 1.8% |
| myeloid_total | 1.8% |
| NKCD56hi_total | 1.8% |
| Tconv memKi67_total | 1.8% |
| CD8 RO CXCR3_total | 1.8% |
| Bcells memory_total | 1.8% |
| CD8 RO CCR4_total | 1.8% |
| Treg memory_CD3 | 1.8% |
| CCR5_CD8RO | 1.8% |
| CD8 RO CCR5_CD3 | 1.8% |
| Tconv memDR_CD3 | 1.8% |
| intB7_CD8RO | 1.8% |
| memory_Bcells | 1.8% |
| Tconv memTIGIT_total | 1.8% |
| Tconv memCD27_Tconv | 1.8% |
| CD3hi_CD4neg | 1.5% |
| CD14+16+mono_total | 1.5% |
| myeloid_CD3neg | 1.5% |
| CD4 Tconv_CD3 | 1.5% |
| Tconv memCCR6_Tconv | 1.5% |
| NKCD56hi_NK | 1.5% |
| CD8 RO PD1_CD8 | 1.5% |
| Tconv memCCR5_mem | 1.5% |
| CD8 RO DR_CD8 | 1.5% |
| nonTnonB_CD3neg | 1.5% |
| CD27_CD8RO | 1.5% |
| CD8 RA_CD8 | 1.5% |
| CD8 ncytotox RO CCR4_CD8ntox | 1.5% |
| Tconv memintB7_Tconv | 1.5% |
| Tconv memCD56_total | 1.5% |
| CD3pos_total | 1.5% |
| CD4 Treg_total | 1.5% |
| CD8 RO PD1_CD3 | 1.5% |
| Tconv memKi67_CD3 | 1.5% |
| Tconv memCCR5_CD3 | 1.5% |
| CD8 RO_total | 1.2% |
| CD8 RO CD27_CD3 | 1.2% |
| CD56_CD8RO | 1.2% |
| Tconv memCCR6_mem | 1.2% |
| Tconv memCXCR3_mem | 1.2% |
| CD4 Tconv_total | 1.2% |
| CD8 ncytotox RO CCR4_CD3 | 1.2% |
| Tconv memKi67_Tconv | 1.2% |
| Tconv memCCR5_Tconv | 1.2% |
| Tconv memPD1_mem | 1.2% |
| Tconv memCD27_CD3 | 1.2% |
| NK_nonTnonB | 1.2% |
| NKCD16_nonTnonB | 1.2% |
| Tconv memTIGIT_CD3 | 1.2% |
| NK Ki67_nonTnonB | 1.2% |
| CD8 RO CXCR3_CD8 | 1.2% |
| CD8 RO intB7_CD8 | 1.2% |
| CD8 RO_CD8 | 1.2% |
| CD8 RO CCR5_CD8 | 1.2% |
| CXCR3_CD8RO | 1.2% |
| CD14+16+mono_myeloid | 1.2% |
| CD8 RO CD27_CD8 | 1.2% |
| CD8 RO CD56_CD8 | 1.2% |
| CD8 RO CD27_total | 1.2% |
| CD8 RO_CD3 | 1.2% |
| Tconv naive_Tconv | 1.2% |
| PD1_CD8RO | 1.2% |
| Treg naive_CD4 | 1.2% |
| Tconv memintB7_CD3 | 1.2% |
| NK Ki67_total | 1.2% |
| CD8 RO CCR6_total | 1.2% |
| NKCD16_total | 1.2% |
| Tconv memCCR6_CD3 | 1.2% |
| Tconv memintB7_total | 1.2% |
| CD8 RO CXCR3_CD3 | 1.2% |
| Ki67_CD8RO | 1.0% |
| Tconv memCCR4_Tconv | 1.0% |
| Tconv memPD1_Tconv | 1.0% |
| CD14mono_CD3neg | 1.0% |
| Tconv memTIGIT_Tconv | 1.0% |
| Bcells naive_CD3neg | 1.0% |
| CCR4_CD8RO | 1.0% |
| Tconv memCD56_mem | 1.0% |
| Tconv memTIGIT_mem | 1.0% |
| Tconv memCD27_mem | 1.0% |
| NKCD56hi_CD3neg | 1.0% |
| NK Ki67_CD3neg | 1.0% |
| CD27negIgDneg_Bcells | 1.0% |
| Tconv memCCR4_CD3 | 1.0% |
| CD14mono_myeloid | 1.0% |
| NKCD16_CD3neg | 1.0% |
| Tconv mem_CD3 | 1.0% |
| Tconv memCD56_Tconv | 1.0% |
| CD8 RO PD1_total | 1.0% |
| CD8 RO intB7_total | 1.0% |
| naive_Bcells | 1.0% |
| CD8 RO TIGIT_total | 1.0% |
| CD8pos_total | 1.0% |
| CD4 Tconv mem_total | 1.0% |
| CD8 RO TIGIT_CD8 | 1.0% |
| Bcells memory_CD3neg | 1.0% |
| CD4neg_total | 1.0% |
| Treg memory_total | 1.0% |
| NK_total | 1.0% |
| Tconv memCD27_total | 1.0% |
| CD3neg_total | 1.0% |
| CD8 RA_total | 1.0% |
| Tconv memPD1_CD3 | 1.0% |
| Treg naive_CD3 | 1.0% |
| Tconv memCCR5_total | 1.0% |
| Tconv memCCR4_mem | 1.0% |
| CD8 RO CCR6_CD3 | 1.0% |
| NK Ki67_NK | 1.0% |
| nonTnonB_total | 1.0% |
| Tconv memCXCR3_CD3 | 1.0% |
| Bcells_CD3neg | 1.0% |
| Tconv memCXCR3_Tconv | 0.8% |
| CCR6_CD8RO | 0.8% |
| CD4 Treg _CD3 | 0.8% |
| Tconv memCD56_CD3 | 0.8% |
| CD4neg_CD3 | 0.8% |
| Bcells Ki67_total | 0.8% |
| CD8 RO CD56_total | 0.8% |
| Bcells Ki67_CD3neg | 0.8% |
| CD8 RO Ki67_total | 0.8% |
| CD16+mono_total | 0.8% |
| CD8 RO intB7_CD3 | 0.8% |
| CD8 RO CCR6_CD8 | 0.8% |
| Tconv memintB7_mem | 0.8% |
| Tconv memCXCR3_total | 0.8% |
| CD8 RA naive_CD3 | 0.8% |
| CD8 RA naive_total | 0.8% |
| CD8 RO DR_total | 0.8% |
| Bcells naive_total | 0.8% |
| Bcells_total | 0.8% |
| NK_CD3neg | 0.8% |
| Bcells CD27negIgDneg_total | 0.5% |
| Tconv memDR_total | 0.5% |
| CD14+16+mono_CD3neg | 0.5% |
| CD14mono_total | 0.5% |
| CD8 RO TIGIT_CD3 | 0.5% |

### XGBoost_Permutation_Top10%

**Base Method**: Raw feature selection frequencies across all bootstrap samples

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Tconv memKi67_total | 96.0% |
| Tconv memintB7_total | 95.0% |
| Tconv memPD1_total | 94.0% |
| Tconv memCD56_total | 92.8% |
| Tconv memCD27_total | 92.0% |
| Tconv memDR_total | 90.5% |
| Tconv naive_total | 90.2% |
| Tconv memCXCR3_total | 86.0% |
| CD4 Treg_total | 81.0% |
| Tconv memTIGIT_total | 80.8% |
| CD3pos_total | 63.0% |
| Tconv memCCR6_total | 53.2% |
| CD4 Tconv mem_total | 48.0% |
| CD4 Tconv_total | 40.8% |
| Bcells CD27posIgDneg_total | 34.5% |
| Tconv memCCR4_total | 33.5% |
| Tconv memCCR5_total | 32.0% |
| CD16mono_myeloid | 22.5% |
| CD8 RO DR_CD3 | 18.5% |
| Ki67_Bcells | 12.0% |
| CD27IgD_Bcells | 10.0% |
| CD16mono_CD3neg | 9.2% |
| Tconv memDR_mem | 7.8% |
| CD8  RO Ki67_CD3 | 6.2% |
| CD4 Treg_CD4 | 6.2% |
| Tconv mem_Tconv | 5.5% |
| Tconv memDR_CD3 | 5.0% |
| CD8 RO CD56_CD3 | 5.0% |
| Treg memory_CD4 | 5.0% |
| Tconv memDR_Tconv | 4.8% |
| NKCD16_NK | 4.8% |
| CD8 RO PD1_CD3 | 4.8% |
| Treg naive_total | 4.5% |
| CD8pos_CD3 | 4.2% |
| DR_CD8RO | 4.2% |
| CD8 RA CCR7 naive_CD8 | 4.2% |
| CD3hi_total | 4.2% |
| Tconv memCCR6_Tconv | 4.0% |
| NKCD56hi_nonTnonB | 4.0% |
| Tconv naive_CD3 | 3.8% |
| CD4neg_total | 3.8% |
| naive_Bcells | 3.8% |
| CD8 RO DR_CD8 | 3.8% |
| CD3hi_CD3 | 3.5% |
| Tconv memCCR5_mem | 3.5% |
| TIGIT_CD8RO | 3.5% |
| Tconv memCD27_Tconv | 3.5% |
| intB7_CD8RO | 3.2% |
| CCR5_CD8RO | 3.2% |
| nonTnonB_CD3neg | 3.2% |
| CD8 RO DR_total | 3.2% |
| NKCD56hi_total | 3.0% |
| memory_Bcells | 3.0% |
| CD8 RA naive_CD3 | 3.0% |
| Tconv memintB7_CD3 | 3.0% |
| CD14+16+mono_myeloid | 3.0% |
| Tconv memKi67_mem | 2.8% |
| NK Ki67_total | 2.8% |
| Bcells memory_total | 2.8% |
| Treg naive_CD4 | 2.8% |
| CD8 RO intB7_CD8 | 2.8% |
| NK_total | 2.8% |
| CD8 RA_CD3 | 2.8% |
| CD8 RO CCR5_CD3 | 2.8% |
| CD8pos_total | 2.8% |
| CD14mono_myeloid | 2.8% |
| Ki67_CD8RO | 2.8% |
| Tconv memCCR4_Tconv | 2.8% |
| Tconv memCD27_CD3 | 2.5% |
| CD8 RO Ki67_total | 2.5% |
| Bcells naive_total | 2.5% |
| Tconv memCXCR3_Tconv | 2.5% |
| Bcells CD27negIgDneg_total | 2.5% |
| myeloid_total | 2.5% |
| Tconv memPD1_mem | 2.5% |
| CD4 Treg _CD3 | 2.5% |
| CD8 RO CD27_CD8 | 2.5% |
| CD8 RO CCR4_total | 2.5% |
| CD3hi_CD4neg | 2.5% |
| Tconv memCCR6_CD3 | 2.2% |
| CD8 RO CD56_CD8 | 2.2% |
| Tconv memTIGIT_Tconv | 2.2% |
| CD8 RO CD56_total | 2.2% |
| CD8 RO CXCR3_total | 2.2% |
| Tconv memKi67_CD3 | 2.2% |
| CD16+mono_total | 2.0% |
| CD8 RO CXCR3_CD3 | 2.0% |
| CD8 RO CCR6_CD3 | 2.0% |
| Bcells_total | 2.0% |
| CD8 RO TIGIT_total | 2.0% |
| PD1_CD8RO | 2.0% |
| NK_CD3neg | 2.0% |
| CD56_CD8RO | 2.0% |
| Tconv memKi67_Tconv | 2.0% |
| CD8 RA_total | 2.0% |
| Tconv memCD56_Tconv | 2.0% |
| Tconv memCXCR3_CD3 | 2.0% |
| Tconv memCCR6_mem | 2.0% |
| Tconv memCD56_mem | 2.0% |
| Bcells naive_CD3neg | 2.0% |
| CD8 RO intB7_total | 2.0% |
| Treg memory_CD3 | 1.8% |
| Tconv memCCR4_CD3 | 1.8% |
| Bcells Ki67_total | 1.8% |
| CD8 RO Ki67_CD8 | 1.8% |
| CD8 ncytotox RO CCR4_CD3 | 1.8% |
| CD8 RO CCR5_CD8 | 1.8% |
| CD8 RO PD1_CD8 | 1.8% |
| CD8 RO TIGIT_CD8 | 1.8% |
| Tconv memintB7_mem | 1.8% |
| CD14+16+mono_total | 1.8% |
| NK Ki67_NK | 1.8% |
| nonTnonB_total | 1.8% |
| CD8 RA_CD8 | 1.8% |
| CD4 Tconv_CD3 | 1.8% |
| Tconv memTIGIT_mem | 1.8% |
| CCR4_CD8RO | 1.8% |
| Tconv memTIGIT_CD3 | 1.8% |
| CD8 RO CCR6_total | 1.5% |
| NK Ki67_nonTnonB | 1.5% |
| CD27_CD8RO | 1.5% |
| CCR6_CD8RO | 1.5% |
| CD8 ncytotox RO CCR4_CD8ntox | 1.5% |
| CD8 RO_total | 1.5% |
| CD8 RO CCR5_total | 1.5% |
| Tconv memCXCR3_mem | 1.5% |
| Tconv memCCR4_mem | 1.5% |
| Tconv memPD1_CD3 | 1.5% |
| CD27negIgDneg_Bcells | 1.5% |
| CD8 RA naive_total | 1.2% |
| Tconv memPD1_Tconv | 1.2% |
| CD8 RO_CD3 | 1.2% |
| NKCD56hi_NK | 1.2% |
| Treg naive_CD3 | 1.2% |
| Tconv memintB7_Tconv | 1.2% |
| Treg memory_total | 1.2% |
| Tconv memCD56_CD3 | 1.2% |
| myeloid_CD3neg | 1.2% |
| CD14mono_CD3neg | 1.2% |
| CD8 RO intB7_CD3 | 1.2% |
| CD8 RO TIGIT_CD3 | 1.2% |
| CD8 RO CXCR3_CD8 | 1.2% |
| Tconv memCD27_mem | 1.0% |
| CD14+16+mono_CD3neg | 1.0% |
| Tconv memCCR5_CD3 | 1.0% |
| CD4neg_CD3 | 1.0% |
| Bcells memory_CD3neg | 1.0% |
| CXCR3_CD8RO | 0.8% |
| CD14mono_total | 0.8% |
| Tconv mem_CD3 | 0.8% |
| CD8 RO CD27_CD3 | 0.8% |
| Tconv naive_Tconv | 0.8% |
| NKCD16_total | 0.8% |
| NKCD16_nonTnonB | 0.8% |
| CD3neg_total | 0.8% |
| NKCD56hi_CD3neg | 0.8% |
| CD8 RO PD1_total | 0.5% |
| Tconv memCCR5_Tconv | 0.5% |
| CD8 RO_CD8 | 0.5% |
| Bcells Ki67_CD3neg | 0.5% |
| NK_nonTnonB | 0.2% |
| CD8 RO CD27_total | 0.2% |
| CD8 RO CCR6_CD8 | 0.2% |

### mRMR (Top 10%)

**Base Method**: Raw feature selection frequencies across all bootstrap samples

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD16mono_myeloid | 57.0% |
| CD8 RO DR_CD8 | 45.8% |
| Treg memory_CD4 | 45.8% |
| CD8 RO DR_CD3 | 44.2% |
| CD4 Tconv_total | 40.8% |
| CD4 Treg_CD4 | 38.0% |
| Treg memory_CD3 | 36.2% |
| DR_CD8RO | 34.8% |
| Tconv memDR_Tconv | 32.5% |
| Tconv mem_Tconv | 32.5% |
| Tconv naive_total | 31.8% |
| Tconv naive_CD3 | 31.0% |
| CD14mono_myeloid | 31.0% |
| CD27IgD_Bcells | 28.7% |
| CD4 Treg _CD3 | 27.8% |
| Tconv memDR_CD3 | 27.8% |
| CD16mono_CD3neg | 27.3% |
| CD3neg_total | 26.5% |
| CD3pos_total | 26.5% |
| CD3hi_total | 26.0% |
| CD14+16+mono_myeloid | 25.2% |
| NKCD56hi_total | 24.5% |
| CD8pos_CD3 | 24.2% |
| Bcells CD27posIgDneg_total | 23.2% |
| Tconv naive_Tconv | 22.2% |
| CD8 RO CD56_CD3 | 18.8% |
| NKCD56hi_NK | 17.8% |
| Tconv memDR_mem | 16.2% |
| Ki67_Bcells | 16.2% |
| CD4 Tconv_CD3 | 16.2% |
| Tconv memCD27_Tconv | 15.0% |
| NKCD16_NK | 14.8% |
| CD8 RO PD1_CD3 | 14.5% |
| Bcells memory_CD3neg | 13.8% |
| nonTnonB_total | 13.8% |
| NK Ki67_total | 13.0% |
| CD8 RA_CD3 | 13.0% |
| CD27negIgDneg_Bcells | 12.8% |
| CD4neg_CD3 | 12.8% |
| Tconv memCCR6_total | 12.2% |
| Bcells CD27negIgDneg_total | 11.8% |
| CD8 RO CD56_CD8 | 11.2% |
| memory_Bcells | 11.0% |
| intB7_CD8RO | 10.8% |
| CD8 RO CXCR3_CD3 | 10.5% |
| CD14+16+mono_CD3neg | 9.8% |
| CD8 RO_CD3 | 9.5% |
| NK Ki67_NK | 9.2% |
| CD14+16+mono_total | 9.2% |
| Tconv memCXCR3_Tconv | 9.2% |
| CD8 RO DR_total | 9.0% |
| Tconv memTIGIT_mem | 9.0% |
| Treg naive_total | 9.0% |
| Tconv mem_CD3 | 8.5% |
| CD27_CD8RO | 8.2% |
| CCR4_CD8RO | 8.0% |
| CD56_CD8RO | 8.0% |
| Tconv memintB7_Tconv | 8.0% |
| CD8 RO TIGIT_CD3 | 7.8% |
| Tconv memCCR4_total | 7.8% |
| Tconv memCCR4_mem | 7.5% |
| CD14mono_total | 7.2% |
| Bcells Ki67_CD3neg | 7.2% |
| Tconv memCD56_total | 7.2% |
| naive_Bcells | 7.2% |
| Tconv memPD1_mem | 7.0% |
| Tconv memCXCR3_CD3 | 7.0% |
| CD14mono_CD3neg | 6.8% |
| Tconv memKi67_total | 6.5% |
| CD8 RA naive_CD3 | 6.5% |
| Bcells naive_CD3neg | 6.2% |
| Tconv memCCR4_Tconv | 6.2% |
| CD16+mono_total | 6.2% |
| Tconv memCXCR3_mem | 6.2% |
| Bcells memory_total | 6.0% |
| Tconv memCCR6_mem | 6.0% |
| CCR5_CD8RO | 6.0% |
| NK_total | 6.0% |
| CD8 RO CD27_CD3 | 5.8% |
| CD8 RA CCR7 naive_CD8 | 5.8% |
| Tconv memCCR5_total | 5.5% |
| CD8  RO Ki67_CD3 | 5.5% |
| Tconv memCD27_mem | 5.5% |
| CD8 RO CXCR3_CD8 | 5.5% |
| Tconv memintB7_CD3 | 5.2% |
| Tconv memintB7_mem | 5.2% |
| Bcells Ki67_total | 5.2% |
| Bcells naive_total | 5.0% |
| Tconv memPD1_total | 5.0% |
| CD3hi_CD4neg | 5.0% |
| CD8 RA naive_total | 5.0% |
| CD8 RO intB7_CD8 | 4.8% |
| Tconv memKi67_mem | 4.8% |
| CD8 RO CD56_total | 4.8% |
| CCR6_CD8RO | 4.8% |
| CD8 ncytotox RO CCR4_CD3 | 4.5% |
| Treg naive_CD3 | 4.2% |
| NK Ki67_nonTnonB | 4.2% |
| CD8 RO CCR6_CD8 | 4.2% |
| Tconv memCD27_total | 4.2% |
| CD8 RO PD1_CD8 | 4.2% |
| Tconv memintB7_total | 4.2% |
| CD4 Tconv mem_total | 4.0% |
| NKCD56hi_CD3neg | 4.0% |
| CD8 RO Ki67_CD8 | 4.0% |
| NKCD16_total | 4.0% |
| CD3hi_CD3 | 3.8% |
| Tconv memTIGIT_Tconv | 3.8% |
| Tconv memCCR5_mem | 3.8% |
| nonTnonB_CD3neg | 3.8% |
| NKCD56hi_nonTnonB | 3.8% |
| CD8 RA_total | 3.5% |
| CD8 RO intB7_total | 3.5% |
| CD8 RO CCR5_total | 3.5% |
| NK Ki67_CD3neg | 3.5% |
| Treg naive_CD4 | 3.5% |
| Tconv memCD56_mem | 3.5% |
| Tconv memCD27_CD3 | 3.2% |
| Bcells_CD3neg | 3.0% |
| Tconv memCCR6_Tconv | 3.0% |
| CD8 RO CCR6_total | 3.0% |
| NKCD16_CD3neg | 2.8% |
| myeloid_total | 2.8% |
| Ki67_CD8RO | 2.8% |
| CD4neg_total | 2.5% |
| Tconv memCCR6_CD3 | 2.5% |
| CXCR3_CD8RO | 2.5% |
| TIGIT_CD8RO | 2.5% |
| Tconv memDR_total | 2.5% |
| CD8pos_total | 2.2% |
| CD8 RO intB7_CD3 | 2.2% |
| CD8 RO CCR6_CD3 | 2.2% |
| Bcells_total | 2.2% |
| Tconv memTIGIT_total | 2.2% |
| PD1_CD8RO | 2.2% |
| CD8 RO CXCR3_total | 2.2% |
| CD8 RO_CD8 | 2.0% |
| CD8 RO CCR5_CD8 | 2.0% |
| Tconv memPD1_Tconv | 2.0% |
| Treg memory_total | 2.0% |
| CD8 ncytotox RO CCR4_CD8ntox | 1.8% |
| Tconv memKi67_CD3 | 1.8% |
| Tconv memCCR4_CD3 | 1.8% |
| CD8 RA_CD8 | 1.5% |
| CD8 RO CD27_CD8 | 1.5% |
| CD8 RO TIGIT_CD8 | 1.5% |
| Tconv memCD56_Tconv | 1.5% |
| NK_CD3neg | 1.5% |
| Tconv memCXCR3_total | 1.5% |
| CD8 RO TIGIT_total | 1.5% |
| CD4 Treg_total | 1.5% |
| Tconv memCD56_CD3 | 1.5% |
| Tconv memPD1_CD3 | 1.2% |
| NKCD16_nonTnonB | 1.2% |
| Tconv memTIGIT_CD3 | 1.2% |
| CD8 RO Ki67_total | 1.2% |
| NK_nonTnonB | 1.2% |
| Tconv memKi67_Tconv | 1.2% |
| CD8 RO CD27_total | 1.0% |
| Tconv memCCR5_Tconv | 1.0% |
| myeloid_CD3neg | 1.0% |
| CD8 RO CCR4_total | 0.8% |
| CD8 RO_total | 0.8% |
| CD8 RO PD1_total | 0.8% |
| CD8 RO CCR5_CD3 | 0.8% |
| Tconv memCCR5_CD3 | 0.2% |

