# Biomarker Discovery: Main Summary Report

---
- **Methodology**: Nested Cross-Validation (40 outer folds) with stratified bootstrapped inner stability (10 resamples)
- **Key Finding**: Performance metrics reported here are unbiased estimates of generalization performance.
- **Best Unbiased ROC-AUC**: 0.7387

## Top 10 Performing Model Combinations (Mean Unbiased Nested CV Performance)

|    | signature_method                          | classifier   |   roc_auc_mean |   roc_auc_std | roc_auc_ci   |   auprc_mean |   auprc_std | auprc_ci    |   accuracy_mean |   accuracy_std |   precision_mean |   precision_std |   recall_mean |   recall_std |   specificity_mean |   specificity_std |   f1_score_mean |   f1_score_std | f1_score_ci   |
|---:|:------------------------------------------|:-------------|---------------:|--------------:|:-------------|-------------:|------------:|:------------|----------------:|---------------:|-----------------:|----------------:|--------------:|-------------:|-------------------:|------------------:|----------------:|---------------:|:--------------|
|  0 | LogisticRegression_Permutation_Top10%_t80 | RandomForest |       0.738657 |      0.123079 | 0.699-0.778  |     0.671335 |    0.14898  | 0.624-0.719 |        0.66     |      0.0987673 |         0.592321 |        0.25384  |      0.4625   |     0.231087 |           0.791667 |         0.138246  |        0.496099 |       0.201858 | 0.432-0.561   |
|  1 | XGBoost_Permutation_Top10%_t80            | RandomForest |       0.73588  |      0.119647 | 0.698-0.774  |     0.67609  |    0.132946 | 0.634-0.719 |        0.675    |      0.0980581 |         0.637262 |        0.178699 |      0.4875   |     0.211451 |           0.8      |         0.135966  |        0.529133 |       0.16454  | 0.477-0.582   |
|  2 | RFE (RandomForest)_t40                    | SVM_RBF      |       0.733796 |      0.104982 | 0.700-0.767  |     0.714351 |    0.102537 | 0.682-0.747 |        0.698333 |      0.0840397 |         0.709881 |        0.215218 |      0.441667 |     0.175208 |           0.869444 |         0.0970848 |        0.524805 |       0.163095 | 0.473-0.577   |
|  3 | RFE (RandomForest)_t50                    | SVM_RBF      |       0.730556 |      0.108788 | 0.696-0.765  |     0.714021 |    0.106547 | 0.680-0.748 |        0.696667 |      0.0866601 |         0.698631 |        0.212902 |      0.445833 |     0.178581 |           0.863889 |         0.0957716 |        0.525487 |       0.167001 | 0.472-0.579   |
|  4 | XGBoost_Permutation_Top10%_t70            | RandomForest |       0.726157 |      0.133537 | 0.683-0.769  |     0.666662 |    0.137487 | 0.623-0.711 |        0.656667 |      0.104104  |         0.594653 |        0.202883 |      0.4625   |     0.240155 |           0.786111 |         0.12678   |        0.494822 |       0.193405 | 0.433-0.557   |
|  5 | All Features (Baseline)_t70               | SVM_RBF      |       0.725463 |      0.108215 | 0.691-0.760  |     0.706605 |    0.104105 | 0.673-0.740 |        0.695    |      0.0825346 |         0.712083 |        0.193594 |      0.425    |     0.184707 |           0.875    |         0.0841602 |        0.50974  |       0.167661 | 0.456-0.563   |
|  6 | RFE (RandomForest)_t60                    | SVM_RBF      |       0.724074 |      0.106653 | 0.690-0.758  |     0.707181 |    0.106728 | 0.673-0.741 |        0.703333 |      0.0905192 |         0.694821 |        0.200943 |      0.466667 |     0.196841 |           0.861111 |         0.0898453 |        0.539011 |       0.177271 | 0.482-0.596   |
|  7 | RF_Importance_t50                         | SVM_RBF      |       0.723611 |      0.11503  | 0.687-0.760  |     0.693329 |    0.120842 | 0.655-0.732 |        0.693333 |      0.0987673 |         0.677173 |        0.187681 |      0.508333 |     0.184707 |           0.816667 |         0.127185  |        0.559052 |       0.155079 | 0.509-0.609   |
|  8 | XGBoost_Permutation_Top10%_t40            | RandomForest |       0.723611 |      0.131491 | 0.682-0.766  |     0.661032 |    0.138646 | 0.617-0.705 |        0.663333 |      0.111912  |         0.627133 |        0.213876 |      0.466667 |     0.220721 |           0.794444 |         0.136779  |        0.509944 |       0.178052 | 0.453-0.567   |
|  9 | RandomForest_Permutation_Top10%_t60       | RandomForest |       0.721991 |      0.110982 | 0.686-0.757  |     0.657281 |    0.135343 | 0.614-0.701 |        0.645    |      0.112356  |         0.584554 |        0.227822 |      0.4375   |     0.219061 |           0.783333 |         0.148752  |        0.47881  |       0.188608 | 0.418-0.539   |

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
| ElasticNet_Lenient_t40 | 40 | 92 | 2.3 |
| ElasticNet_Lenient_t50 | 39 | 73 | 1.9 |
| ElasticNet_Lenient_t60 | 39 | 55 | 1.4 |
| ElasticNet_Lenient_t70 | 34 | 35 | 1.0 |
| ElasticNet_Lenient_t80 | 28 | 23 | 0.8 |
| ElasticNet_RFE_t40 | 40 | 79 | 2.0 |
| ElasticNet_RFE_t50 | 39 | 55 | 1.4 |
| ElasticNet_RFE_t60 | 37 | 37 | 1.0 |
| ElasticNet_RFE_t70 | 31 | 25 | 0.8 |
| ElasticNet_RFE_t80 | 22 | 13 | 0.6 |
| ElasticNet_Strict_t40 | 39 | 51 | 1.3 |
| ElasticNet_Strict_t50 | 35 | 25 | 0.7 |
| ElasticNet_Strict_t60 | 21 | 15 | 0.7 |
| ElasticNet_Strict_t70 | 17 | 12 | 0.7 |
| ElasticNet_Strict_t80 | 8 | 6 | 0.8 |
| FDR (p < 0.01)_t40 | 28 | 32 | 1.1 |
| FDR (p < 0.01)_t50 | 24 | 23 | 1.0 |
| FDR (p < 0.01)_t60 | 14 | 12 | 0.9 |
| FDR (p < 0.01)_t70 | 8 | 7 | 0.9 |
| FDR (p < 0.01)_t80 | 3 | 2 | 0.7 |
| FDR (p < 0.05)_t40 | 40 | 86 | 2.1 |
| FDR (p < 0.05)_t50 | 37 | 66 | 1.8 |
| FDR (p < 0.05)_t60 | 36 | 52 | 1.4 |
| FDR (p < 0.05)_t70 | 31 | 39 | 1.3 |
| FDR (p < 0.05)_t80 | 21 | 27 | 1.3 |
| FDR (p < 0.1)_t40 | 40 | 115 | 2.9 |
| FDR (p < 0.1)_t50 | 40 | 89 | 2.2 |
| FDR (p < 0.1)_t60 | 38 | 80 | 2.1 |
| FDR (p < 0.1)_t70 | 37 | 61 | 1.6 |
| FDR (p < 0.1)_t80 | 34 | 48 | 1.4 |
| LASSO_Lenient_t40 | 40 | 78 | 1.9 |
| LASSO_Lenient_t50 | 39 | 58 | 1.5 |
| LASSO_Lenient_t60 | 36 | 35 | 1.0 |
| LASSO_Lenient_t70 | 29 | 22 | 0.8 |
| LASSO_Lenient_t80 | 17 | 11 | 0.6 |
| LASSO_RFE_t40 | 40 | 63 | 1.6 |
| LASSO_RFE_t50 | 39 | 41 | 1.1 |
| LASSO_RFE_t60 | 33 | 24 | 0.7 |
| LASSO_RFE_t70 | 21 | 14 | 0.7 |
| LASSO_RFE_t80 | 15 | 11 | 0.7 |
| LASSO_Strict_t40 | 36 | 31 | 0.9 |
| LASSO_Strict_t50 | 25 | 16 | 0.6 |
| LASSO_Strict_t60 | 15 | 11 | 0.7 |
| LASSO_Strict_t70 | 12 | 8 | 0.7 |
| LASSO_Strict_t80 | 3 | 4 | 1.3 |
| LogisticRegression_Permutation_Top10%_t40 | 40 | 16 | 0.4 |
| LogisticRegression_Permutation_Top10%_t50 | 40 | 16 | 0.4 |
| LogisticRegression_Permutation_Top10%_t60 | 40 | 16 | 0.4 |
| LogisticRegression_Permutation_Top10%_t70 | 40 | 16 | 0.4 |
| LogisticRegression_Permutation_Top10%_t80 | 40 | 16 | 0.4 |
| Mutual Information (Top 10%)_t40 | 40 | 94 | 2.4 |
| Mutual Information (Top 10%)_t50 | 40 | 62 | 1.6 |
| Mutual Information (Top 10%)_t60 | 37 | 32 | 0.9 |
| Mutual Information (Top 10%)_t70 | 29 | 17 | 0.6 |
| Mutual Information (Top 10%)_t80 | 11 | 5 | 0.5 |
| NaiveBayes_Permutation_AboveMean_t40 | 40 | 160 | 4.0 |
| NaiveBayes_Permutation_AboveMean_t50 | 40 | 130 | 3.2 |
| NaiveBayes_Permutation_AboveMean_t60 | 40 | 81 | 2.0 |
| NaiveBayes_Permutation_AboveMean_t70 | 40 | 51 | 1.3 |
| NaiveBayes_Permutation_AboveMean_t80 | 40 | 41 | 1.0 |
| NaiveBayes_Permutation_Top10%_t40 | 40 | 68 | 1.7 |
| NaiveBayes_Permutation_Top10%_t50 | 40 | 54 | 1.4 |
| NaiveBayes_Permutation_Top10%_t60 | 40 | 41 | 1.0 |
| NaiveBayes_Permutation_Top10%_t70 | 39 | 30 | 0.8 |
| NaiveBayes_Permutation_Top10%_t80 | 27 | 17 | 0.6 |
| RFE (RandomForest)_t40 | 40 | 166 | 4.2 |
| RFE (RandomForest)_t50 | 40 | 166 | 4.2 |
| RFE (RandomForest)_t60 | 40 | 166 | 4.2 |
| RFE (RandomForest)_t70 | 40 | 162 | 4.0 |
| RFE (RandomForest)_t80 | 40 | 153 | 3.8 |
| RF_Importance_t40 | 40 | 163 | 4.1 |
| RF_Importance_t50 | 40 | 143 | 3.6 |
| RF_Importance_t60 | 40 | 110 | 2.8 |
| RF_Importance_t70 | 40 | 85 | 2.1 |
| RF_Importance_t80 | 40 | 55 | 1.4 |
| RandomForest_Permutation_Top10%_t40 | 40 | 16 | 0.4 |
| RandomForest_Permutation_Top10%_t50 | 40 | 16 | 0.4 |
| RandomForest_Permutation_Top10%_t60 | 40 | 16 | 0.4 |
| RandomForest_Permutation_Top10%_t70 | 40 | 16 | 0.4 |
| RandomForest_Permutation_Top10%_t80 | 40 | 16 | 0.4 |
| Ridge_Strict_t40 | 40 | 165 | 4.1 |
| Ridge_Strict_t50 | 40 | 160 | 4.0 |
| Ridge_Strict_t60 | 40 | 156 | 3.9 |
| Ridge_Strict_t70 | 40 | 141 | 3.5 |
| Ridge_Strict_t80 | 40 | 130 | 3.2 |
| SVM_RBF_Permutation_AboveMean_t40 | 25 | 165 | 6.6 |
| SVM_RBF_Permutation_AboveMean_t50 | 19 | 143 | 7.5 |
| SVM_RBF_Permutation_AboveMean_t60 | 11 | 48 | 4.4 |
| SVM_RBF_Permutation_AboveMean_t70 | 3 | 11 | 3.7 |
| SVM_RBF_Permutation_AboveMean_t80 | 1 | 1 | 1.0 |
| SVM_RBF_Permutation_Top10%_t40 | 40 | 28 | 0.7 |
| SVM_RBF_Permutation_Top10%_t50 | 40 | 18 | 0.5 |
| SVM_RBF_Permutation_Top10%_t60 | 39 | 17 | 0.4 |
| SVM_RBF_Permutation_Top10%_t70 | 31 | 16 | 0.5 |
| SVM_RBF_Permutation_Top10%_t80 | 23 | 16 | 0.7 |
| XGB_Importance_t40 | 40 | 97 | 2.4 |
| XGB_Importance_t50 | 40 | 64 | 1.6 |
| XGB_Importance_t60 | 40 | 40 | 1.0 |
| XGB_Importance_t70 | 39 | 23 | 0.6 |
| XGB_Importance_t80 | 31 | 15 | 0.5 |
| XGBoost_Permutation_AboveMean_t40 | 14 | 5 | 0.4 |
| XGBoost_Permutation_AboveMean_t50 | 8 | 5 | 0.6 |
| XGBoost_Permutation_AboveMean_t60 | 4 | 3 | 0.8 |
| XGBoost_Permutation_AboveMean_t70 | 2 | 2 | 1.0 |
| XGBoost_Permutation_AboveMean_t80 | 1 | 1 | 1.0 |
| XGBoost_Permutation_Top10%_t40 | 40 | 23 | 0.6 |
| XGBoost_Permutation_Top10%_t50 | 40 | 21 | 0.5 |
| XGBoost_Permutation_Top10%_t60 | 40 | 19 | 0.5 |
| XGBoost_Permutation_Top10%_t70 | 40 | 18 | 0.5 |
| XGBoost_Permutation_Top10%_t80 | 40 | 16 | 0.4 |
| mRMR (Top 10%)_t40 | 40 | 71 | 1.8 |
| mRMR (Top 10%)_t50 | 40 | 53 | 1.3 |
| mRMR (Top 10%)_t60 | 40 | 43 | 1.1 |
| mRMR (Top 10%)_t70 | 39 | 37 | 0.9 |
| mRMR (Top 10%)_t80 | 33 | 26 | 0.8 |

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
| ElasticNet_Lenient | 40 | 92 | 2.3 |
| ElasticNet_RFE | 40 | 79 | 2.0 |
| ElasticNet_Strict | 39 | 51 | 1.3 |
| FDR (p < 0.01) | 28 | 32 | 1.1 |
| FDR (p < 0.05) | 40 | 86 | 2.1 |
| FDR (p < 0.1) | 40 | 115 | 2.9 |
| LASSO_Lenient | 40 | 78 | 1.9 |
| LASSO_RFE | 40 | 63 | 1.6 |
| LASSO_Strict | 36 | 31 | 0.9 |
| LogisticRegression_Permutation_Top10% | 40 | 16 | 0.4 |
| Mutual Information (Top 10%) | 40 | 94 | 2.4 |
| NaiveBayes_Permutation_AboveMean | 40 | 160 | 4.0 |
| NaiveBayes_Permutation_Top10% | 40 | 68 | 1.7 |
| RFE (RandomForest) | 40 | 166 | 4.2 |
| RF_Importance | 40 | 163 | 4.1 |
| RandomForest_Permutation_Top10% | 40 | 16 | 0.4 |
| Ridge_Strict | 40 | 165 | 4.1 |
| SVM_RBF_Permutation_AboveMean | 25 | 165 | 6.6 |
| SVM_RBF_Permutation_Top10% | 40 | 28 | 0.7 |
| XGB_Importance | 40 | 97 | 2.4 |
| XGBoost_Permutation_AboveMean | 14 | 5 | 0.4 |
| XGBoost_Permutation_Top10% | 40 | 23 | 0.6 |
| mRMR (Top 10%) | 40 | 71 | 1.8 |

**Total signatures at 40% threshold**: 902

#### Threshold 50%

| Base Method | Signatures Found | Total Features | Avg Features/Signature |
|-------------|------------------|----------------|------------------------|
| All Features (Baseline) | 40 | 166 | 4.2 |
| ElasticNet_Lenient | 39 | 73 | 1.9 |
| ElasticNet_RFE | 39 | 55 | 1.4 |
| ElasticNet_Strict | 35 | 25 | 0.7 |
| FDR (p < 0.01) | 24 | 23 | 1.0 |
| FDR (p < 0.05) | 37 | 66 | 1.8 |
| FDR (p < 0.1) | 40 | 89 | 2.2 |
| LASSO_Lenient | 39 | 58 | 1.5 |
| LASSO_RFE | 39 | 41 | 1.1 |
| LASSO_Strict | 25 | 16 | 0.6 |
| LogisticRegression_Permutation_Top10% | 40 | 16 | 0.4 |
| Mutual Information (Top 10%) | 40 | 62 | 1.6 |
| NaiveBayes_Permutation_AboveMean | 40 | 130 | 3.2 |
| NaiveBayes_Permutation_Top10% | 40 | 54 | 1.4 |
| RFE (RandomForest) | 40 | 166 | 4.2 |
| RF_Importance | 40 | 143 | 3.6 |
| RandomForest_Permutation_Top10% | 40 | 16 | 0.4 |
| Ridge_Strict | 40 | 160 | 4.0 |
| SVM_RBF_Permutation_AboveMean | 19 | 143 | 7.5 |
| SVM_RBF_Permutation_Top10% | 40 | 18 | 0.5 |
| XGB_Importance | 40 | 64 | 1.6 |
| XGBoost_Permutation_AboveMean | 8 | 5 | 0.6 |
| XGBoost_Permutation_Top10% | 40 | 21 | 0.5 |
| mRMR (Top 10%) | 40 | 53 | 1.3 |

**Total signatures at 50% threshold**: 864

#### Threshold 60%

| Base Method | Signatures Found | Total Features | Avg Features/Signature |
|-------------|------------------|----------------|------------------------|
| All Features (Baseline) | 40 | 166 | 4.2 |
| ElasticNet_Lenient | 39 | 55 | 1.4 |
| ElasticNet_RFE | 37 | 37 | 1.0 |
| ElasticNet_Strict | 21 | 15 | 0.7 |
| FDR (p < 0.01) | 14 | 12 | 0.9 |
| FDR (p < 0.05) | 36 | 52 | 1.4 |
| FDR (p < 0.1) | 38 | 80 | 2.1 |
| LASSO_Lenient | 36 | 35 | 1.0 |
| LASSO_RFE | 33 | 24 | 0.7 |
| LASSO_Strict | 15 | 11 | 0.7 |
| LogisticRegression_Permutation_Top10% | 40 | 16 | 0.4 |
| Mutual Information (Top 10%) | 37 | 32 | 0.9 |
| NaiveBayes_Permutation_AboveMean | 40 | 81 | 2.0 |
| NaiveBayes_Permutation_Top10% | 40 | 41 | 1.0 |
| RFE (RandomForest) | 40 | 166 | 4.2 |
| RF_Importance | 40 | 110 | 2.8 |
| RandomForest_Permutation_Top10% | 40 | 16 | 0.4 |
| Ridge_Strict | 40 | 156 | 3.9 |
| SVM_RBF_Permutation_AboveMean | 11 | 48 | 4.4 |
| SVM_RBF_Permutation_Top10% | 39 | 17 | 0.4 |
| XGB_Importance | 40 | 40 | 1.0 |
| XGBoost_Permutation_AboveMean | 4 | 3 | 0.8 |
| XGBoost_Permutation_Top10% | 40 | 19 | 0.5 |
| mRMR (Top 10%) | 40 | 43 | 1.1 |

**Total signatures at 60% threshold**: 800

#### Threshold 70%

| Base Method | Signatures Found | Total Features | Avg Features/Signature |
|-------------|------------------|----------------|------------------------|
| All Features (Baseline) | 40 | 166 | 4.2 |
| ElasticNet_Lenient | 34 | 35 | 1.0 |
| ElasticNet_RFE | 31 | 25 | 0.8 |
| ElasticNet_Strict | 17 | 12 | 0.7 |
| FDR (p < 0.01) | 8 | 7 | 0.9 |
| FDR (p < 0.05) | 31 | 39 | 1.3 |
| FDR (p < 0.1) | 37 | 61 | 1.6 |
| LASSO_Lenient | 29 | 22 | 0.8 |
| LASSO_RFE | 21 | 14 | 0.7 |
| LASSO_Strict | 12 | 8 | 0.7 |
| LogisticRegression_Permutation_Top10% | 40 | 16 | 0.4 |
| Mutual Information (Top 10%) | 29 | 17 | 0.6 |
| NaiveBayes_Permutation_AboveMean | 40 | 51 | 1.3 |
| NaiveBayes_Permutation_Top10% | 39 | 30 | 0.8 |
| RFE (RandomForest) | 40 | 162 | 4.0 |
| RF_Importance | 40 | 85 | 2.1 |
| RandomForest_Permutation_Top10% | 40 | 16 | 0.4 |
| Ridge_Strict | 40 | 141 | 3.5 |
| SVM_RBF_Permutation_AboveMean | 3 | 11 | 3.7 |
| SVM_RBF_Permutation_Top10% | 31 | 16 | 0.5 |
| XGB_Importance | 39 | 23 | 0.6 |
| XGBoost_Permutation_AboveMean | 2 | 2 | 1.0 |
| XGBoost_Permutation_Top10% | 40 | 18 | 0.5 |
| mRMR (Top 10%) | 39 | 37 | 0.9 |

**Total signatures at 70% threshold**: 722

#### Threshold 80%

| Base Method | Signatures Found | Total Features | Avg Features/Signature |
|-------------|------------------|----------------|------------------------|
| All Features (Baseline) | 40 | 166 | 4.2 |
| ElasticNet_Lenient | 28 | 23 | 0.8 |
| ElasticNet_RFE | 22 | 13 | 0.6 |
| ElasticNet_Strict | 8 | 6 | 0.8 |
| FDR (p < 0.01) | 3 | 2 | 0.7 |
| FDR (p < 0.05) | 21 | 27 | 1.3 |
| FDR (p < 0.1) | 34 | 48 | 1.4 |
| LASSO_Lenient | 17 | 11 | 0.6 |
| LASSO_RFE | 15 | 11 | 0.7 |
| LASSO_Strict | 3 | 4 | 1.3 |
| LogisticRegression_Permutation_Top10% | 40 | 16 | 0.4 |
| Mutual Information (Top 10%) | 11 | 5 | 0.5 |
| NaiveBayes_Permutation_AboveMean | 40 | 41 | 1.0 |
| NaiveBayes_Permutation_Top10% | 27 | 17 | 0.6 |
| RFE (RandomForest) | 40 | 153 | 3.8 |
| RF_Importance | 40 | 55 | 1.4 |
| RandomForest_Permutation_Top10% | 40 | 16 | 0.4 |
| Ridge_Strict | 40 | 130 | 3.2 |
| SVM_RBF_Permutation_AboveMean | 1 | 1 | 1.0 |
| SVM_RBF_Permutation_Top10% | 23 | 16 | 0.7 |
| XGB_Importance | 31 | 15 | 0.5 |
| XGBoost_Permutation_AboveMean | 1 | 1 | 1.0 |
| XGBoost_Permutation_Top10% | 40 | 16 | 0.4 |
| mRMR (Top 10%) | 33 | 26 | 0.8 |

**Total signatures at 80% threshold**: 598


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
| CD14mono_myeloid | 62.5% |
| CD16mono_myeloid | 62.5% |
| CCR4_CD8RO | 60.0% |
| CD27IgD_Bcells | 57.5% |
| NKCD56hi_nonTnonB | 57.5% |
| CD3hi_CD4neg | 47.5% |
| Tconv memPD1_mem | 47.5% |
| CD8pos_CD3 | 42.5% |
| CD8 RA_CD3 | 37.5% |
| NKCD56hi_total | 37.5% |
| CD14+16+mono_myeloid | 35.0% |
| CD4 Treg_CD4 | 32.5% |
| Bcells CD27negIgDneg_total | 30.0% |
| Tconv memKi67_mem | 25.0% |
| CD8 RA_total | 25.0% |
| DR_CD8RO | 25.0% |
| Tconv memCCR6_Tconv | 25.0% |
| Tconv memKi67_total | 22.5% |
| CD27negIgDneg_Bcells | 22.5% |
| CD8 RO CCR5_CD8 | 22.5% |
| CD8 RO TIGIT_CD3 | 20.0% |
| CD16mono_CD3neg | 20.0% |
| Tconv memCCR6_mem | 20.0% |
| CD8 RO CCR5_CD3 | 20.0% |
| CD8 RO CXCR3_CD3 | 17.5% |
| CD8 RO CXCR3_CD8 | 17.5% |
| Tconv memCXCR3_CD3 | 17.5% |
| CD8 RA CCR7 naive_CD8 | 17.5% |
| TIGIT_CD8RO | 17.5% |
| Treg memory_CD3 | 17.5% |
| Tconv naive_total | 17.5% |
| Tconv memCCR6_CD3 | 15.0% |
| Bcells memory_total | 15.0% |
| Treg memory_CD4 | 15.0% |
| CD8 RA naive_CD3 | 12.5% |
| Tconv memCXCR3_Tconv | 12.5% |
| Bcells Ki67_CD3neg | 12.5% |
| Bcells CD27posIgDneg_total | 12.5% |
| CD3hi_total | 12.5% |
| Ki67_Bcells | 12.5% |
| CD4 Tconv_total | 12.5% |
| Tconv memCD56_total | 12.5% |
| Tconv memTIGIT_Tconv | 10.0% |
| NKCD56hi_NK | 10.0% |
| CD4 Treg _CD3 | 10.0% |
| CD4neg_CD3 | 10.0% |
| Tconv naive_CD3 | 10.0% |
| Treg naive_CD4 | 10.0% |
| NKCD56hi_CD3neg | 10.0% |
| CD8 RO CD27_CD3 | 10.0% |
| NK Ki67_NK | 7.5% |
| CCR5_CD8RO | 7.5% |
| Tconv memCXCR3_mem | 7.5% |
| Treg naive_total | 7.5% |
| CD8 RO DR_CD8 | 7.5% |
| Bcells Ki67_total | 7.5% |
| Tconv memCCR4_mem | 5.0% |
| CD8 RO CCR6_CD8 | 5.0% |
| Tconv memCD27_mem | 5.0% |
| CD4 Tconv_CD3 | 5.0% |
| CD3pos_total | 5.0% |
| Tconv memCCR4_Tconv | 5.0% |
| NK_total | 5.0% |
| CD3neg_total | 5.0% |
| NK Ki67_nonTnonB | 5.0% |
| Bcells_total | 5.0% |
| Tconv memKi67_CD3 | 5.0% |
| Ki67_CD8RO | 5.0% |
| Treg memory_total | 5.0% |
| Tconv memCXCR3_total | 2.5% |
| Tconv memDR_CD3 | 2.5% |
| CD8 RO_CD8 | 2.5% |
| CD8 RO CD56_CD8 | 2.5% |
| memory_Bcells | 2.5% |
| CD8 RO_CD3 | 2.5% |
| Tconv memDR_mem | 2.5% |
| CD8 RO intB7_CD8 | 2.5% |
| Tconv memCCR5_mem | 2.5% |
| Tconv memDR_total | 2.5% |
| CD27_CD8RO | 2.5% |
| CD8 RO CCR5_total | 2.5% |
| Tconv mem_Tconv | 2.5% |
| CD8 RA naive_total | 2.5% |
| CD8pos_total | 2.5% |
| CD8 RO CCR6_CD3 | 2.5% |
| CD8 RO DR_CD3 | 2.5% |
| CD8 RO CCR6_total | 2.5% |
| NKCD16_total | 2.5% |
| CD8 RO PD1_total | 2.5% |
| CD8 RO intB7_CD3 | 2.5% |
| Tconv memintB7_Tconv | 2.5% |
| CCR6_CD8RO | 2.5% |

**Total features selected by ElasticNet_Lenient_t40**: 92

#### ElasticNet_Lenient_t50

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD27IgD_Bcells | 48.7% |
| CD14mono_myeloid | 48.7% |
| CCR4_CD8RO | 48.7% |
| CD16mono_myeloid | 43.6% |
| NKCD56hi_nonTnonB | 35.9% |
| CD8pos_CD3 | 35.9% |
| Tconv memPD1_mem | 33.3% |
| CD3hi_CD4neg | 30.8% |
| NKCD56hi_total | 28.2% |
| CD14+16+mono_myeloid | 25.6% |
| Tconv memKi67_total | 20.5% |
| Bcells CD27negIgDneg_total | 20.5% |
| CD8 RO CCR5_CD3 | 17.9% |
| CD8 RO CCR5_CD8 | 17.9% |
| CD8 RA_CD3 | 17.9% |
| Tconv memCCR6_Tconv | 15.4% |
| Tconv memKi67_mem | 15.4% |
| CD27negIgDneg_Bcells | 15.4% |
| Tconv memCXCR3_Tconv | 12.8% |
| CD8 RA CCR7 naive_CD8 | 12.8% |
| Tconv memCXCR3_CD3 | 12.8% |
| CD4 Treg_CD4 | 12.8% |
| Tconv naive_total | 12.8% |
| CD8 RO CXCR3_CD3 | 12.8% |
| DR_CD8RO | 12.8% |
| CD16mono_CD3neg | 12.8% |
| Tconv memCCR6_CD3 | 12.8% |
| CD8 RA_total | 10.3% |
| CD4 Tconv_total | 10.3% |
| Tconv memCCR6_mem | 10.3% |
| CD3hi_total | 7.7% |
| Bcells Ki67_CD3neg | 7.7% |
| Treg naive_CD4 | 7.7% |
| CD8 RO CD27_CD3 | 7.7% |
| CD8 RO CXCR3_CD8 | 7.7% |
| Treg memory_CD4 | 7.7% |
| NKCD56hi_NK | 5.1% |
| CD8 RO TIGIT_CD3 | 5.1% |
| Ki67_Bcells | 5.1% |
| CD8 RO DR_CD8 | 5.1% |
| Tconv memKi67_CD3 | 5.1% |
| NK Ki67_NK | 5.1% |
| CD8 RA naive_CD3 | 5.1% |
| Bcells memory_total | 5.1% |
| TIGIT_CD8RO | 5.1% |
| NK_total | 5.1% |
| CD4neg_CD3 | 5.1% |
| NKCD56hi_CD3neg | 5.1% |
| Tconv memCCR4_mem | 5.1% |
| Tconv memCD56_total | 2.6% |
| Ki67_CD8RO | 2.6% |
| CD8 RO CCR6_CD8 | 2.6% |
| Tconv naive_CD3 | 2.6% |
| Tconv memCD27_mem | 2.6% |
| CD8 RO_CD3 | 2.6% |
| CD3pos_total | 2.6% |
| CD3neg_total | 2.6% |
| CD8 RO CCR5_total | 2.6% |
| CD8 RO intB7_CD8 | 2.6% |
| Tconv memCXCR3_mem | 2.6% |
| Tconv memTIGIT_Tconv | 2.6% |
| Treg memory_CD3 | 2.6% |
| Treg naive_total | 2.6% |
| CD8pos_total | 2.6% |
| Bcells CD27posIgDneg_total | 2.6% |
| CD8 RO CCR6_CD3 | 2.6% |
| CD8 RO DR_CD3 | 2.6% |
| NKCD16_total | 2.6% |
| CD8 RO PD1_total | 2.6% |
| CD8 RO intB7_CD3 | 2.6% |
| Tconv memintB7_Tconv | 2.6% |
| CCR5_CD8RO | 2.6% |
| Tconv memCCR4_Tconv | 2.6% |

**Total features selected by ElasticNet_Lenient_t50**: 73

#### ElasticNet_Lenient_t60

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD14mono_myeloid | 41.0% |
| CCR4_CD8RO | 35.9% |
| CD27IgD_Bcells | 25.6% |
| CD16mono_myeloid | 25.6% |
| CD8pos_CD3 | 23.1% |
| Tconv memPD1_mem | 20.5% |
| NKCD56hi_nonTnonB | 20.5% |
| CD14+16+mono_myeloid | 20.5% |
| Tconv memKi67_total | 17.9% |
| CD3hi_CD4neg | 15.4% |
| CD8 RO CCR5_CD3 | 12.8% |
| Tconv memCXCR3_Tconv | 12.8% |
| CD8 RO CCR5_CD8 | 12.8% |
| Tconv memCCR6_CD3 | 12.8% |
| NKCD56hi_total | 12.8% |
| CD8 RA_CD3 | 10.3% |
| CD8 RO CXCR3_CD3 | 7.7% |
| Treg naive_CD4 | 7.7% |
| CD16mono_CD3neg | 7.7% |
| CD8 RA CCR7 naive_CD8 | 7.7% |
| Treg memory_CD4 | 7.7% |
| Tconv naive_total | 7.7% |
| Bcells Ki67_CD3neg | 7.7% |
| Tconv memKi67_mem | 7.7% |
| Bcells CD27negIgDneg_total | 5.1% |
| DR_CD8RO | 5.1% |
| CD8 RO DR_CD8 | 5.1% |
| CD8 RA_total | 5.1% |
| Tconv memCCR6_Tconv | 5.1% |
| NK Ki67_NK | 5.1% |
| NKCD56hi_CD3neg | 5.1% |
| CD27negIgDneg_Bcells | 5.1% |
| CD3hi_total | 5.1% |
| Tconv memCCR4_mem | 5.1% |
| CD8 RO CCR6_CD8 | 2.6% |
| CD4neg_CD3 | 2.6% |
| Tconv memCXCR3_mem | 2.6% |
| Treg memory_CD3 | 2.6% |
| Ki67_CD8RO | 2.6% |
| Tconv memCXCR3_CD3 | 2.6% |
| CD8 RO CCR5_total | 2.6% |
| Bcells CD27posIgDneg_total | 2.6% |
| CD8 RO TIGIT_CD3 | 2.6% |
| CD8 RO CXCR3_CD8 | 2.6% |
| Tconv memCCR6_mem | 2.6% |
| NKCD56hi_NK | 2.6% |
| CD8 RO CCR6_CD3 | 2.6% |
| CD8 RO DR_CD3 | 2.6% |
| CD4 Treg_CD4 | 2.6% |
| NK_total | 2.6% |
| NKCD16_total | 2.6% |
| CD8 RO PD1_total | 2.6% |
| CCR5_CD8RO | 2.6% |
| Bcells memory_total | 2.6% |
| CD8 RO CD27_CD3 | 2.6% |

**Total features selected by ElasticNet_Lenient_t60**: 55

#### ElasticNet_Lenient_t70

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CCR4_CD8RO | 32.4% |
| CD14mono_myeloid | 26.5% |
| CD27IgD_Bcells | 26.5% |
| Tconv memPD1_mem | 17.6% |
| CD8pos_CD3 | 14.7% |
| CD8 RO CCR5_CD3 | 14.7% |
| CD14+16+mono_myeloid | 11.8% |
| NKCD56hi_total | 8.8% |
| CD16mono_myeloid | 8.8% |
| CD3hi_CD4neg | 8.8% |
| CD8 RO CCR5_CD8 | 8.8% |
| NKCD56hi_nonTnonB | 8.8% |
| CD8 RO DR_CD8 | 5.9% |
| Tconv memKi67_total | 5.9% |
| Bcells Ki67_CD3neg | 5.9% |
| Treg memory_CD3 | 2.9% |
| CD8 RO CXCR3_CD3 | 2.9% |
| CD8 RA_total | 2.9% |
| Tconv naive_total | 2.9% |
| CD8 RA_CD3 | 2.9% |
| Treg memory_CD4 | 2.9% |
| Ki67_CD8RO | 2.9% |
| Bcells CD27posIgDneg_total | 2.9% |
| Tconv memCCR6_mem | 2.9% |
| Tconv memCCR6_CD3 | 2.9% |
| Tconv memCCR6_Tconv | 2.9% |
| CD8 RO TIGIT_CD3 | 2.9% |
| CD16mono_CD3neg | 2.9% |
| Tconv memCXCR3_Tconv | 2.9% |
| Treg naive_CD4 | 2.9% |
| NKCD56hi_NK | 2.9% |
| CD8 RO CCR6_CD3 | 2.9% |
| CD4 Treg_CD4 | 2.9% |
| NK_total | 2.9% |
| CD8 RO PD1_total | 2.9% |

**Total features selected by ElasticNet_Lenient_t70**: 35

#### ElasticNet_Lenient_t80

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CCR4_CD8RO | 28.6% |
| CD27IgD_Bcells | 25.0% |
| CD14mono_myeloid | 21.4% |
| CD8 RO CCR5_CD3 | 10.7% |
| CD8pos_CD3 | 10.7% |
| Tconv memPD1_mem | 10.7% |
| CD14+16+mono_myeloid | 10.7% |
| NKCD56hi_total | 7.1% |
| Tconv naive_total | 3.6% |
| Treg memory_CD3 | 3.6% |
| CD8 RO DR_CD8 | 3.6% |
| CD8 RA_CD3 | 3.6% |
| Tconv memCCR6_CD3 | 3.6% |
| Tconv memCCR6_mem | 3.6% |
| Treg memory_CD4 | 3.6% |
| Tconv memKi67_total | 3.6% |
| CD8 RO CCR5_CD8 | 3.6% |
| NKCD56hi_nonTnonB | 3.6% |
| Tconv memCXCR3_Tconv | 3.6% |
| NKCD56hi_NK | 3.6% |
| CD8 RO CCR6_CD3 | 3.6% |
| CD4 Treg_CD4 | 3.6% |
| NK_total | 3.6% |

**Total features selected by ElasticNet_Lenient_t80**: 23

#### ElasticNet_RFE_t40

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD16mono_myeloid | 60.0% |
| CD14mono_myeloid | 57.5% |
| CD27IgD_Bcells | 52.5% |
| CCR4_CD8RO | 45.0% |
| CD8pos_CD3 | 40.0% |
| NKCD56hi_nonTnonB | 37.5% |
| Tconv memPD1_mem | 37.5% |
| NKCD56hi_total | 32.5% |
| CD3hi_CD4neg | 32.5% |
| CD4 Treg_CD4 | 30.0% |
| CD8 RA_CD3 | 27.5% |
| Tconv memKi67_total | 22.5% |
| CD8 RO CCR5_CD8 | 20.0% |
| CD14+16+mono_myeloid | 20.0% |
| CD8 RO CCR5_CD3 | 17.5% |
| Tconv memCCR6_Tconv | 17.5% |
| Tconv naive_total | 17.5% |
| Treg memory_CD4 | 15.0% |
| CD8 RO CXCR3_CD8 | 15.0% |
| Tconv memKi67_mem | 15.0% |
| CD16mono_CD3neg | 15.0% |
| CD8 RO CXCR3_CD3 | 12.5% |
| CD4 Tconv_total | 12.5% |
| Tconv memCCR6_CD3 | 12.5% |
| Tconv memCCR6_mem | 12.5% |
| DR_CD8RO | 12.5% |
| Bcells CD27negIgDneg_total | 12.5% |
| Tconv memCXCR3_Tconv | 12.5% |
| CD8 RA_total | 10.0% |
| CD3hi_total | 10.0% |
| Tconv memCXCR3_CD3 | 10.0% |
| CD8 RO TIGIT_CD3 | 10.0% |
| Treg memory_CD3 | 10.0% |
| CD8 RA CCR7 naive_CD8 | 10.0% |
| CD27negIgDneg_Bcells | 10.0% |
| Treg naive_CD4 | 7.5% |
| Bcells CD27posIgDneg_total | 7.5% |
| CD4 Treg _CD3 | 7.5% |
| CD8 RA naive_CD3 | 7.5% |
| CD8 RO DR_CD8 | 7.5% |
| CD3pos_total | 5.0% |
| Tconv memCCR4_mem | 5.0% |
| Tconv memCD56_total | 5.0% |
| CD8 RO CD27_CD3 | 5.0% |
| NK Ki67_NK | 5.0% |
| Tconv memKi67_CD3 | 5.0% |
| Tconv naive_CD3 | 5.0% |
| CCR5_CD8RO | 5.0% |
| Bcells Ki67_CD3neg | 5.0% |
| CD4neg_CD3 | 5.0% |
| CD3neg_total | 5.0% |
| Bcells memory_total | 5.0% |
| Tconv memCXCR3_mem | 5.0% |
| NKCD56hi_CD3neg | 5.0% |
| Tconv memCXCR3_total | 2.5% |
| CD8 RO CCR6_CD8 | 2.5% |
| Tconv memCD27_mem | 2.5% |
| Ki67_CD8RO | 2.5% |
| Bcells Ki67_total | 2.5% |
| CD8 RO CD56_CD8 | 2.5% |
| Bcells_total | 2.5% |
| CD8 RO_CD3 | 2.5% |
| Tconv memDR_total | 2.5% |
| CD8 RO CCR5_total | 2.5% |
| Tconv memCCR5_mem | 2.5% |
| Tconv memTIGIT_Tconv | 2.5% |
| CD4 Tconv_CD3 | 2.5% |
| CD8pos_total | 2.5% |
| NKCD56hi_NK | 2.5% |
| TIGIT_CD8RO | 2.5% |
| Treg memory_total | 2.5% |
| CD8 RO CCR6_CD3 | 2.5% |
| CD8 RO DR_CD3 | 2.5% |
| NKCD16_total | 2.5% |
| NK_total | 2.5% |
| CD8 RO PD1_total | 2.5% |
| CD8 RO intB7_CD3 | 2.5% |
| Tconv memintB7_Tconv | 2.5% |
| Tconv memCCR4_Tconv | 2.5% |

**Total features selected by ElasticNet_RFE_t40**: 79

#### ElasticNet_RFE_t50

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD14mono_myeloid | 43.6% |
| CD27IgD_Bcells | 43.6% |
| CD16mono_myeloid | 38.5% |
| CD8pos_CD3 | 33.3% |
| CCR4_CD8RO | 33.3% |
| NKCD56hi_nonTnonB | 20.5% |
| NKCD56hi_total | 20.5% |
| Tconv memPD1_mem | 17.9% |
| CD8 RO CCR5_CD3 | 17.9% |
| Tconv memKi67_total | 15.4% |
| CD3hi_CD4neg | 15.4% |
| Tconv naive_total | 12.8% |
| Tconv memCXCR3_Tconv | 12.8% |
| CD8 RO CXCR3_CD3 | 12.8% |
| CD14+16+mono_myeloid | 12.8% |
| CD16mono_CD3neg | 12.8% |
| CD8 RA_CD3 | 10.3% |
| Tconv memCCR6_CD3 | 10.3% |
| CD8 RO CCR5_CD8 | 10.3% |
| CD4 Treg_CD4 | 7.7% |
| Treg memory_CD4 | 7.7% |
| Tconv memKi67_mem | 7.7% |
| CD4neg_CD3 | 5.1% |
| CD8 RO TIGIT_CD3 | 5.1% |
| Tconv memCXCR3_CD3 | 5.1% |
| CD27negIgDneg_Bcells | 5.1% |
| Tconv memCCR4_mem | 5.1% |
| NK Ki67_NK | 5.1% |
| CD4 Tconv_total | 5.1% |
| Tconv memCD27_mem | 2.6% |
| CD8 RO CCR6_CD8 | 2.6% |
| NKCD56hi_CD3neg | 2.6% |
| CD8 RO DR_CD8 | 2.6% |
| CD8 RO_CD3 | 2.6% |
| CD3pos_total | 2.6% |
| Treg memory_CD3 | 2.6% |
| Tconv memCXCR3_mem | 2.6% |
| Bcells CD27negIgDneg_total | 2.6% |
| Ki67_CD8RO | 2.6% |
| Bcells CD27posIgDneg_total | 2.6% |
| CD8 RO CCR5_total | 2.6% |
| Tconv memCCR6_Tconv | 2.6% |
| Tconv memCCR6_mem | 2.6% |
| Treg naive_CD4 | 2.6% |
| DR_CD8RO | 2.6% |
| CD8 RA CCR7 naive_CD8 | 2.6% |
| NKCD56hi_NK | 2.6% |
| CD8 RO CCR6_CD3 | 2.6% |
| CD8 RO DR_CD3 | 2.6% |
| NK_total | 2.6% |
| CD8 RO CXCR3_CD8 | 2.6% |
| CD8 RO PD1_total | 2.6% |
| CCR5_CD8RO | 2.6% |
| Bcells Ki67_CD3neg | 2.6% |
| CD8 RA_total | 2.6% |

**Total features selected by ElasticNet_RFE_t50**: 55

#### ElasticNet_RFE_t60

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD8pos_CD3 | 24.3% |
| CD27IgD_Bcells | 24.3% |
| CD16mono_myeloid | 24.3% |
| CCR4_CD8RO | 24.3% |
| CD14mono_myeloid | 24.3% |
| CD8 RO CCR5_CD3 | 13.5% |
| NKCD56hi_nonTnonB | 13.5% |
| Tconv memCXCR3_Tconv | 10.8% |
| Tconv memPD1_mem | 10.8% |
| CD14+16+mono_myeloid | 8.1% |
| NKCD56hi_total | 8.1% |
| Tconv naive_total | 8.1% |
| Tconv memKi67_total | 8.1% |
| Tconv memCCR6_CD3 | 5.4% |
| Treg memory_CD4 | 5.4% |
| CD16mono_CD3neg | 5.4% |
| CD8 RA_CD3 | 5.4% |
| CD3hi_CD4neg | 5.4% |
| CD8 RO CCR5_CD8 | 5.4% |
| CD8 RO CCR6_CD8 | 2.7% |
| CD4neg_CD3 | 2.7% |
| Treg memory_CD3 | 2.7% |
| CD8 RO DR_CD8 | 2.7% |
| NKCD56hi_CD3neg | 2.7% |
| Ki67_CD8RO | 2.7% |
| Tconv memCCR6_mem | 2.7% |
| Bcells CD27posIgDneg_total | 2.7% |
| Tconv memKi67_mem | 2.7% |
| Tconv memCCR4_mem | 2.7% |
| Tconv memCCR6_Tconv | 2.7% |
| CD8 RO CCR6_CD3 | 2.7% |
| CD4 Treg_CD4 | 2.7% |
| CD8 RO PD1_total | 2.7% |
| CD27negIgDneg_Bcells | 2.7% |
| CCR5_CD8RO | 2.7% |
| Bcells Ki67_CD3neg | 2.7% |
| CD8 RA_total | 2.7% |

**Total features selected by ElasticNet_RFE_t60**: 37

#### ElasticNet_RFE_t70

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD27IgD_Bcells | 25.8% |
| CCR4_CD8RO | 22.6% |
| CD8pos_CD3 | 16.1% |
| CD8 RO CCR5_CD3 | 16.1% |
| CD14mono_myeloid | 16.1% |
| Tconv memPD1_mem | 9.7% |
| NKCD56hi_total | 6.5% |
| CD8 RO CCR5_CD8 | 6.5% |
| CD16mono_myeloid | 6.5% |
| CD14+16+mono_myeloid | 6.5% |
| Tconv naive_total | 3.2% |
| CD8 RO DR_CD8 | 3.2% |
| Ki67_CD8RO | 3.2% |
| Bcells CD27posIgDneg_total | 3.2% |
| Treg memory_CD3 | 3.2% |
| Tconv memCCR6_mem | 3.2% |
| Treg memory_CD4 | 3.2% |
| Tconv memCCR6_CD3 | 3.2% |
| CD16mono_CD3neg | 3.2% |
| NKCD56hi_nonTnonB | 3.2% |
| Tconv memCXCR3_Tconv | 3.2% |
| CD3hi_CD4neg | 3.2% |
| CD8 RO CCR6_CD3 | 3.2% |
| CD4 Treg_CD4 | 3.2% |
| CD8 RO PD1_total | 3.2% |

**Total features selected by ElasticNet_RFE_t70**: 25

#### ElasticNet_RFE_t80

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD27IgD_Bcells | 22.7% |
| CD14mono_myeloid | 22.7% |
| CD8pos_CD3 | 13.6% |
| CCR4_CD8RO | 13.6% |
| CD8 RO CCR5_CD3 | 13.6% |
| Tconv memPD1_mem | 9.1% |
| Tconv naive_total | 4.5% |
| CD8 RO DR_CD8 | 4.5% |
| NKCD56hi_total | 4.5% |
| CD8 RO CCR5_CD8 | 4.5% |
| Treg memory_CD4 | 4.5% |
| NKCD56hi_nonTnonB | 4.5% |
| CD14+16+mono_myeloid | 4.5% |

**Total features selected by ElasticNet_RFE_t80**: 13

#### ElasticNet_Strict_t40

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CCR4_CD8RO | 33.3% |
| CD27IgD_Bcells | 25.6% |
| CD14mono_myeloid | 25.6% |
| Tconv memPD1_mem | 25.6% |
| CD16mono_myeloid | 23.1% |
| CD8pos_CD3 | 20.5% |
| CD8 RO CCR5_CD3 | 15.4% |
| Tconv memKi67_total | 12.8% |
| NKCD56hi_nonTnonB | 12.8% |
| CD14+16+mono_myeloid | 12.8% |
| CD8 RO CCR5_CD8 | 10.3% |
| CD3hi_CD4neg | 10.3% |
| Tconv memCCR6_CD3 | 10.3% |
| CD8 RA_CD3 | 7.7% |
| Tconv memKi67_mem | 7.7% |
| NKCD56hi_NK | 7.7% |
| CD8 RO CXCR3_CD3 | 7.7% |
| Tconv naive_total | 5.1% |
| NKCD56hi_total | 5.1% |
| CD8 RA CCR7 naive_CD8 | 5.1% |
| Tconv memCCR6_mem | 5.1% |
| Bcells CD27negIgDneg_total | 5.1% |
| CD8 RO DR_CD8 | 5.1% |
| Bcells CD27posIgDneg_total | 5.1% |
| Tconv memCXCR3_Tconv | 5.1% |
| CD8 RA_total | 5.1% |
| CD4 Tconv_total | 5.1% |
| CD8 RA naive_CD3 | 5.1% |
| CD8 RO CXCR3_CD8 | 5.1% |
| CD8 RO CCR6_CD8 | 2.6% |
| Tconv memCD27_mem | 2.6% |
| Tconv memDR_CD3 | 2.6% |
| Ki67_CD8RO | 2.6% |
| CD16mono_CD3neg | 2.6% |
| Treg memory_CD3 | 2.6% |
| CD8 RO TIGIT_CD3 | 2.6% |
| CD8 RO CCR5_total | 2.6% |
| Tconv memCXCR3_CD3 | 2.6% |
| CD4neg_CD3 | 2.6% |
| CD27negIgDneg_Bcells | 2.6% |
| Tconv memCCR6_Tconv | 2.6% |
| DR_CD8RO | 2.6% |
| CCR5_CD8RO | 2.6% |
| Tconv naive_CD3 | 2.6% |
| Treg memory_CD4 | 2.6% |
| CD8 RO CCR6_CD3 | 2.6% |
| CD4 Treg_CD4 | 2.6% |
| NK Ki67_NK | 2.6% |
| Bcells memory_total | 2.6% |
| Tconv memintB7_Tconv | 2.6% |
| Bcells Ki67_CD3neg | 2.6% |

**Total features selected by ElasticNet_Strict_t40**: 51

#### ElasticNet_Strict_t50

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CCR4_CD8RO | 25.7% |
| CD14mono_myeloid | 20.0% |
| CD27IgD_Bcells | 20.0% |
| CD16mono_myeloid | 14.3% |
| CD8pos_CD3 | 11.4% |
| Tconv memCCR6_CD3 | 11.4% |
| Tconv memPD1_mem | 8.6% |
| CD8 RO CCR5_CD8 | 8.6% |
| CD8 RO CCR5_CD3 | 8.6% |
| CD14+16+mono_myeloid | 8.6% |
| NKCD56hi_total | 5.7% |
| Tconv memKi67_total | 5.7% |
| CD3hi_CD4neg | 5.7% |
| NKCD56hi_nonTnonB | 5.7% |
| CD8 RO CXCR3_CD3 | 2.9% |
| Ki67_CD8RO | 2.9% |
| Tconv memCXCR3_Tconv | 2.9% |
| CD8 RO TIGIT_CD3 | 2.9% |
| CD8 RA_CD3 | 2.9% |
| Tconv memKi67_mem | 2.9% |
| Bcells CD27negIgDneg_total | 2.9% |
| NKCD56hi_NK | 2.9% |
| Tconv naive_total | 2.9% |
| Bcells Ki67_CD3neg | 2.9% |
| CD8 RO DR_CD8 | 2.9% |

**Total features selected by ElasticNet_Strict_t50**: 25

#### ElasticNet_Strict_t60

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD27IgD_Bcells | 23.8% |
| CD14mono_myeloid | 19.0% |
| CCR4_CD8RO | 19.0% |
| Tconv memPD1_mem | 14.3% |
| CD8pos_CD3 | 14.3% |
| NKCD56hi_total | 9.5% |
| CD8 RO CCR5_CD3 | 9.5% |
| CD16mono_myeloid | 9.5% |
| Tconv memCCR6_CD3 | 9.5% |
| CD14+16+mono_myeloid | 9.5% |
| CD8 RO CCR5_CD8 | 4.8% |
| NKCD56hi_nonTnonB | 4.8% |
| Bcells Ki67_CD3neg | 4.8% |
| Tconv memKi67_total | 4.8% |
| CD8 RO DR_CD8 | 4.8% |

**Total features selected by ElasticNet_Strict_t60**: 15

#### ElasticNet_Strict_t70

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD27IgD_Bcells | 29.4% |
| CD14mono_myeloid | 23.5% |
| CD8pos_CD3 | 17.6% |
| CCR4_CD8RO | 11.8% |
| CD14+16+mono_myeloid | 11.8% |
| NKCD56hi_total | 5.9% |
| CD8 RO CCR5_CD8 | 5.9% |
| CD16mono_myeloid | 5.9% |
| Tconv memPD1_mem | 5.9% |
| NKCD56hi_nonTnonB | 5.9% |
| Tconv memKi67_total | 5.9% |
| CD8 RO DR_CD8 | 5.9% |

**Total features selected by ElasticNet_Strict_t70**: 12

#### ElasticNet_Strict_t80

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD8pos_CD3 | 25.0% |
| CD27IgD_Bcells | 25.0% |
| CD8 RO CCR5_CD8 | 12.5% |
| CD14+16+mono_myeloid | 12.5% |
| CCR4_CD8RO | 12.5% |
| CD14mono_myeloid | 12.5% |

**Total features selected by ElasticNet_Strict_t80**: 6

#### FDR (p < 0.01)_t40

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD4 Treg_CD4 | 57.1% |
| CD8 RO CCR5_CD3 | 57.1% |
| CD8pos_CD3 | 50.0% |
| Tconv naive_total | 42.9% |
| Treg memory_CD4 | 42.9% |
| CD4 Tconv_CD3 | 35.7% |
| CD8 RO CXCR3_CD3 | 32.1% |
| Bcells CD27posIgDneg_total | 21.4% |
| CD8 RO CCR5_total | 17.9% |
| CD8 RA_CD3 | 17.9% |
| Tconv naive_CD3 | 17.9% |
| CD4 Tconv_total | 17.9% |
| Tconv memCCR5_Tconv | 17.9% |
| CD8 RO_CD3 | 10.7% |
| Tconv memCXCR3_Tconv | 10.7% |
| CD8 RO CCR5_CD8 | 10.7% |
| CD8 RO DR_CD3 | 10.7% |
| CD14mono_myeloid | 7.1% |
| Treg memory_CD3 | 7.1% |
| Tconv mem_Tconv | 7.1% |
| CD16mono_CD3neg | 7.1% |
| Tconv naive_Tconv | 7.1% |
| CD27IgD_Bcells | 7.1% |
| CD16mono_myeloid | 7.1% |
| Tconv memCCR6_Tconv | 7.1% |
| CD4 Treg _CD3 | 7.1% |
| CD8 RO CD56_CD3 | 3.6% |
| CD8 RO CD27_CD3 | 3.6% |
| Tconv memCCR5_mem | 3.6% |
| Tconv memCCR5_CD3 | 3.6% |
| CD3pos_total | 3.6% |
| CD3neg_total | 3.6% |

**Total features selected by FDR (p < 0.01)_t40**: 32

#### FDR (p < 0.01)_t50

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Tconv naive_total | 41.7% |
| CD8 RO CCR5_CD3 | 41.7% |
| CD4 Treg_CD4 | 25.0% |
| CD8pos_CD3 | 25.0% |
| CD8 RO CXCR3_CD3 | 20.8% |
| Treg memory_CD4 | 16.7% |
| CD4 Tconv_CD3 | 16.7% |
| CD8 RA_CD3 | 16.7% |
| Bcells CD27posIgDneg_total | 12.5% |
| CD8 RO DR_CD3 | 12.5% |
| CD8 RO_CD3 | 8.3% |
| Tconv naive_CD3 | 8.3% |
| CD8 RO CD56_CD3 | 4.2% |
| Tconv memCCR5_CD3 | 4.2% |
| CD8 RO CD27_CD3 | 4.2% |
| Tconv memCCR5_Tconv | 4.2% |
| CD8 RO CCR5_total | 4.2% |
| CD4 Tconv_total | 4.2% |
| Tconv memCCR6_Tconv | 4.2% |
| CD16mono_CD3neg | 4.2% |
| CD27IgD_Bcells | 4.2% |
| Treg memory_CD3 | 4.2% |
| CD14mono_myeloid | 4.2% |

**Total features selected by FDR (p < 0.01)_t50**: 23

#### FDR (p < 0.01)_t60

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Tconv naive_total | 42.9% |
| CD4 Treg_CD4 | 28.6% |
| CD8 RO CCR5_CD3 | 28.6% |
| CD8pos_CD3 | 28.6% |
| CD4 Tconv_CD3 | 21.4% |
| Treg memory_CD4 | 21.4% |
| CD8 RA_CD3 | 21.4% |
| CD8 RO_CD3 | 7.1% |
| CD8 RO CCR5_total | 7.1% |
| CD8 RO DR_CD3 | 7.1% |
| CD14mono_myeloid | 7.1% |
| Tconv naive_CD3 | 7.1% |

**Total features selected by FDR (p < 0.01)_t60**: 12

#### FDR (p < 0.01)_t70

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD8pos_CD3 | 50.0% |
| CD8 RA_CD3 | 25.0% |
| Tconv naive_total | 25.0% |
| CD8 RO CCR5_CD3 | 25.0% |
| CD4 Treg_CD4 | 12.5% |
| CD4 Tconv_CD3 | 12.5% |
| CD14mono_myeloid | 12.5% |

**Total features selected by FDR (p < 0.01)_t70**: 7

#### FDR (p < 0.01)_t80

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD8pos_CD3 | 66.7% |
| CD8 RO CCR5_CD3 | 33.3% |

**Total features selected by FDR (p < 0.01)_t80**: 2

#### FDR (p < 0.05)_t40

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD4 Treg_CD4 | 90.0% |
| Treg memory_CD4 | 82.5% |
| Tconv naive_total | 80.0% |
| CD8pos_CD3 | 75.0% |
| CD8 RO CCR5_CD3 | 75.0% |
| CD4 Tconv_CD3 | 65.0% |
| Bcells CD27posIgDneg_total | 65.0% |
| CD4 Tconv_total | 62.5% |
| Tconv naive_CD3 | 57.5% |
| CD8 RO CXCR3_CD3 | 50.0% |
| CD27IgD_Bcells | 47.5% |
| CD8 RO CCR5_total | 45.0% |
| Tconv memCCR5_Tconv | 45.0% |
| Tconv memCXCR3_Tconv | 42.5% |
| Tconv mem_Tconv | 42.5% |
| CD8 RO CCR5_CD8 | 42.5% |
| CD16mono_myeloid | 42.5% |
| Tconv naive_Tconv | 42.5% |
| CD8 RO_CD3 | 42.5% |
| Treg memory_CD3 | 40.0% |
| CD8 RO CD56_CD3 | 40.0% |
| CD16mono_CD3neg | 40.0% |
| CD8 RO CCR6_CD3 | 35.0% |
| CD8 RA_CD3 | 35.0% |
| CD8 RO DR_CD3 | 35.0% |
| Tconv memCCR5_mem | 35.0% |
| CD4 Treg _CD3 | 32.5% |
| CD4neg_CD3 | 32.5% |
| CD14mono_myeloid | 30.0% |
| Tconv memCCR5_CD3 | 27.5% |
| CD8 RO CD27_CD3 | 25.0% |
| Tconv memCXCR3_CD3 | 22.5% |
| CCR5_CD8RO | 22.5% |
| Tconv memCXCR3_mem | 22.5% |
| CD8 RO TIGIT_CD3 | 22.5% |
| CD8 RO intB7_CD3 | 20.0% |
| Tconv memCCR6_Tconv | 20.0% |
| CD3neg_total | 17.5% |
| Tconv memintB7_Tconv | 17.5% |
| CD3pos_total | 17.5% |
| CD8 RO CXCR3_total | 17.5% |
| Tconv memCCR4_Tconv | 15.0% |
| Tconv memCD27_Tconv | 15.0% |
| Tconv memKi67_total | 12.5% |
| CD8  RO Ki67_CD3 | 12.5% |
| CD8 RO CXCR3_CD8 | 12.5% |
| CD8pos_total | 10.0% |
| NKCD56hi_total | 10.0% |
| CD8 RO DR_total | 7.5% |
| CXCR3_CD8RO | 7.5% |
| CCR4_CD8RO | 7.5% |
| CD8 RO CD56_total | 7.5% |
| Tconv memCD27_mem | 7.5% |
| nonTnonB_total | 7.5% |
| Tconv memCD56_Tconv | 7.5% |
| Tconv memTIGIT_Tconv | 7.5% |
| CD8 RO PD1_CD3 | 5.0% |
| CD16+mono_total | 5.0% |
| NKCD56hi_nonTnonB | 5.0% |
| Tconv memCCR6_CD3 | 5.0% |
| Tconv memPD1_total | 5.0% |
| CD8 ncytotox RO CCR4_CD3 | 5.0% |
| CD8 RO DR_CD8 | 5.0% |
| CD27negIgDneg_Bcells | 5.0% |
| CD14mono_total | 5.0% |
| Bcells memory_CD3neg | 5.0% |
| CD8 RA CCR7 naive_CD8 | 2.5% |
| CD8 RO CD27_total | 2.5% |
| Tconv memCD27_total | 2.5% |
| Tconv memDR_Tconv | 2.5% |
| Tconv memCCR5_total | 2.5% |
| NKCD56hi_CD3neg | 2.5% |
| NK Ki67_total | 2.5% |
| Tconv memCCR4_mem | 2.5% |
| Tconv memPD1_Tconv | 2.5% |
| CD8 RA_total | 2.5% |
| Treg memory_total | 2.5% |
| Tconv memCXCR3_total | 2.5% |
| NK Ki67_NK | 2.5% |
| CD8 RO Ki67_CD8 | 2.5% |
| CD8 RO CD56_CD8 | 2.5% |
| CD8 RO TIGIT_total | 2.5% |
| CD8 RO intB7_total | 2.5% |
| CD8 RO CCR6_total | 2.5% |
| Tconv memPD1_mem | 2.5% |
| Bcells memory_total | 2.5% |

**Total features selected by FDR (p < 0.05)_t40**: 86

#### FDR (p < 0.05)_t50

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD4 Treg_CD4 | 89.2% |
| Treg memory_CD4 | 83.8% |
| Tconv naive_total | 78.4% |
| CD8 RO CCR5_CD3 | 67.6% |
| CD4 Tconv_total | 59.5% |
| CD8pos_CD3 | 56.8% |
| CD4 Tconv_CD3 | 54.1% |
| Bcells CD27posIgDneg_total | 45.9% |
| CD8 RO CXCR3_CD3 | 40.5% |
| Tconv naive_CD3 | 40.5% |
| CD27IgD_Bcells | 40.5% |
| Tconv memCXCR3_Tconv | 37.8% |
| Tconv memCCR5_Tconv | 35.1% |
| CD16mono_CD3neg | 32.4% |
| CD8 RO CCR5_CD8 | 29.7% |
| CD8 RO CD56_CD3 | 29.7% |
| CD16mono_myeloid | 29.7% |
| CD8 RO CCR5_total | 29.7% |
| CD8 RA_CD3 | 29.7% |
| CD8 RO_CD3 | 27.0% |
| CD8 RO DR_CD3 | 27.0% |
| CD8 RO CD27_CD3 | 24.3% |
| CD4neg_CD3 | 24.3% |
| Tconv mem_Tconv | 21.6% |
| Tconv memCCR5_mem | 21.6% |
| Tconv naive_Tconv | 21.6% |
| Treg memory_CD3 | 21.6% |
| CD14mono_myeloid | 18.9% |
| CD4 Treg _CD3 | 18.9% |
| CD8 RO CCR6_CD3 | 18.9% |
| CD8 RO TIGIT_CD3 | 18.9% |
| Tconv memCCR5_CD3 | 16.2% |
| Tconv memCXCR3_mem | 16.2% |
| Tconv memCXCR3_CD3 | 16.2% |
| Tconv memCCR6_Tconv | 13.5% |
| CD8pos_total | 10.8% |
| CD8 RO CXCR3_total | 10.8% |
| CCR5_CD8RO | 10.8% |
| CD3neg_total | 10.8% |
| Tconv memCCR4_Tconv | 10.8% |
| CD3pos_total | 10.8% |
| Tconv memintB7_Tconv | 8.1% |
| NKCD56hi_total | 8.1% |
| Tconv memCCR6_CD3 | 5.4% |
| CXCR3_CD8RO | 5.4% |
| CD8 RO intB7_CD3 | 5.4% |
| CD16+mono_total | 5.4% |
| CCR4_CD8RO | 5.4% |
| Tconv memCD27_Tconv | 5.4% |
| CD8 RO DR_total | 5.4% |
| CD8 RO CXCR3_CD8 | 5.4% |
| nonTnonB_total | 2.7% |
| CD8 RA CCR7 naive_CD8 | 2.7% |
| Tconv memKi67_total | 2.7% |
| NK Ki67_total | 2.7% |
| Tconv memCCR4_mem | 2.7% |
| CD8  RO Ki67_CD3 | 2.7% |
| CD27negIgDneg_Bcells | 2.7% |
| NKCD56hi_CD3neg | 2.7% |
| CD8 ncytotox RO CCR4_CD3 | 2.7% |
| Tconv memCD27_mem | 2.7% |
| CD8 RO CCR6_total | 2.7% |
| Bcells memory_total | 2.7% |
| Bcells memory_CD3neg | 2.7% |
| CD8 RO PD1_CD3 | 2.7% |
| CD8 RO DR_CD8 | 2.7% |

**Total features selected by FDR (p < 0.05)_t50**: 66

#### FDR (p < 0.05)_t60

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Tconv naive_total | 69.4% |
| CD8 RO CCR5_CD3 | 61.1% |
| CD4 Treg_CD4 | 58.3% |
| Treg memory_CD4 | 47.2% |
| CD4 Tconv_total | 41.7% |
| CD8 RO CXCR3_CD3 | 38.9% |
| CD4 Tconv_CD3 | 38.9% |
| Tconv naive_CD3 | 36.1% |
| CD8pos_CD3 | 36.1% |
| Bcells CD27posIgDneg_total | 33.3% |
| CD27IgD_Bcells | 30.6% |
| CD16mono_myeloid | 25.0% |
| Tconv memCCR5_Tconv | 25.0% |
| CD8 RO_CD3 | 25.0% |
| CD8 RO DR_CD3 | 19.4% |
| CD8 RA_CD3 | 19.4% |
| Tconv memCXCR3_Tconv | 19.4% |
| CD8 RO CCR5_total | 19.4% |
| CD16mono_CD3neg | 19.4% |
| CD4neg_CD3 | 16.7% |
| Tconv memCCR5_mem | 16.7% |
| Treg memory_CD3 | 13.9% |
| CD8 RO TIGIT_CD3 | 13.9% |
| CD8 RO CD27_CD3 | 13.9% |
| CD8 RO CCR6_CD3 | 13.9% |
| CD4 Treg _CD3 | 13.9% |
| Tconv mem_Tconv | 13.9% |
| Tconv naive_Tconv | 13.9% |
| CD14mono_myeloid | 11.1% |
| Tconv memCCR5_CD3 | 11.1% |
| Tconv memCCR6_Tconv | 8.3% |
| Tconv memCXCR3_CD3 | 8.3% |
| CD8 RO CD56_CD3 | 8.3% |
| CD8 RO CCR5_CD8 | 8.3% |
| CCR5_CD8RO | 5.6% |
| CD8 RO intB7_CD3 | 5.6% |
| CD3pos_total | 5.6% |
| CCR4_CD8RO | 5.6% |
| CD3neg_total | 5.6% |
| CD8pos_total | 2.8% |
| Tconv memCCR4_mem | 2.8% |
| Tconv memKi67_total | 2.8% |
| Tconv memCXCR3_mem | 2.8% |
| NKCD56hi_total | 2.8% |
| Tconv memCCR6_CD3 | 2.8% |
| CD8 RO CXCR3_CD8 | 2.8% |
| CD8 RO CXCR3_total | 2.8% |
| Tconv memCD27_mem | 2.8% |
| Bcells memory_CD3neg | 2.8% |
| Tconv memCD27_Tconv | 2.8% |
| Tconv memCCR4_Tconv | 2.8% |
| CD8 RO DR_CD8 | 2.8% |

**Total features selected by FDR (p < 0.05)_t60**: 52

#### FDR (p < 0.05)_t70

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD8 RO CCR5_CD3 | 54.8% |
| Tconv naive_total | 51.6% |
| CD4 Treg_CD4 | 38.7% |
| CD4 Tconv_CD3 | 32.3% |
| Treg memory_CD4 | 32.3% |
| Tconv naive_CD3 | 29.0% |
| CD8pos_CD3 | 25.8% |
| CD27IgD_Bcells | 22.6% |
| CD8 RO CXCR3_CD3 | 19.4% |
| CD8 RO_CD3 | 19.4% |
| CD4 Tconv_total | 19.4% |
| Tconv memCCR5_Tconv | 16.1% |
| Bcells CD27posIgDneg_total | 16.1% |
| CD4neg_CD3 | 12.9% |
| CD8 RO CD27_CD3 | 9.7% |
| CD16mono_CD3neg | 9.7% |
| Tconv memCCR5_mem | 9.7% |
| CD8 RA_CD3 | 9.7% |
| Tconv memCXCR3_Tconv | 9.7% |
| Treg memory_CD3 | 9.7% |
| CD8 RO DR_CD3 | 9.7% |
| CD8 RO CCR6_CD3 | 6.5% |
| Tconv naive_Tconv | 6.5% |
| CD8 RO CD56_CD3 | 6.5% |
| CD8 RO CCR5_total | 6.5% |
| CD4 Treg _CD3 | 6.5% |
| Tconv mem_Tconv | 6.5% |
| Tconv memCCR6_Tconv | 6.5% |
| CCR4_CD8RO | 3.2% |
| CD8 RO intB7_CD3 | 3.2% |
| CD8 RO TIGIT_CD3 | 3.2% |
| CD8 RO CCR5_CD8 | 3.2% |
| NKCD56hi_total | 3.2% |
| CD16mono_myeloid | 3.2% |
| CCR5_CD8RO | 3.2% |
| CD3pos_total | 3.2% |
| CD3neg_total | 3.2% |
| CD14mono_myeloid | 3.2% |
| CD8 RO DR_CD8 | 3.2% |

**Total features selected by FDR (p < 0.05)_t70**: 39

#### FDR (p < 0.05)_t80

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Tconv naive_total | 42.9% |
| CD8 RO CCR5_CD3 | 42.9% |
| CD4 Treg_CD4 | 33.3% |
| CD8pos_CD3 | 28.6% |
| Treg memory_CD4 | 28.6% |
| CD4 Tconv_CD3 | 23.8% |
| CD8 RO_CD3 | 19.0% |
| CD27IgD_Bcells | 19.0% |
| Tconv naive_CD3 | 14.3% |
| CD8 RO CXCR3_CD3 | 14.3% |
| CD8 RA_CD3 | 9.5% |
| CD8 RO CCR5_total | 9.5% |
| Tconv memCCR6_Tconv | 9.5% |
| CD16mono_CD3neg | 9.5% |
| CD4neg_CD3 | 9.5% |
| Treg memory_CD3 | 9.5% |
| CD8 RO CD56_CD3 | 9.5% |
| CD8 RO CCR6_CD3 | 4.8% |
| CD8 RO CD27_CD3 | 4.8% |
| Tconv memCXCR3_Tconv | 4.8% |
| CD4 Tconv_total | 4.8% |
| CD8 RO CCR5_CD8 | 4.8% |
| Bcells CD27posIgDneg_total | 4.8% |
| CCR5_CD8RO | 4.8% |
| CD4 Treg _CD3 | 4.8% |
| CD8 RO DR_CD3 | 4.8% |
| CD14mono_myeloid | 4.8% |

**Total features selected by FDR (p < 0.05)_t80**: 27

#### FDR (p < 0.1)_t40

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD8 RO CCR5_CD3 | 100.0% |
| CD4 Treg_CD4 | 97.5% |
| Treg memory_CD4 | 97.5% |
| Tconv naive_total | 95.0% |
| CD4 Tconv_total | 90.0% |
| CD8pos_CD3 | 87.5% |
| Bcells CD27posIgDneg_total | 87.5% |
| CD27IgD_Bcells | 87.5% |
| CD8 RO CXCR3_CD3 | 85.0% |
| CD4 Tconv_CD3 | 82.5% |
| Treg memory_CD3 | 72.5% |
| CD8 RO CD56_CD3 | 72.5% |
| CD16mono_myeloid | 67.5% |
| CD8 RO CCR5_total | 67.5% |
| Tconv naive_CD3 | 67.5% |
| CD4 Treg _CD3 | 65.0% |
| CD8 RO CCR5_CD8 | 65.0% |
| CD16mono_CD3neg | 65.0% |
| Tconv mem_Tconv | 62.5% |
| CD8 RO DR_CD3 | 60.0% |
| Tconv naive_Tconv | 60.0% |
| Tconv memCCR5_Tconv | 57.5% |
| Tconv memCCR6_Tconv | 57.5% |
| CD4neg_CD3 | 55.0% |
| Tconv memCXCR3_Tconv | 55.0% |
| CD8 RO_CD3 | 55.0% |
| CD8 RA_CD3 | 55.0% |
| Tconv memCCR5_mem | 52.5% |
| CD14mono_myeloid | 52.5% |
| CD8 RO CCR6_CD3 | 50.0% |
| Tconv memCCR5_CD3 | 47.5% |
| CD8 RO CD27_CD3 | 45.0% |
| Tconv memKi67_total | 42.5% |
| CCR5_CD8RO | 42.5% |
| Tconv memCXCR3_mem | 40.0% |
| CD3pos_total | 40.0% |
| CD3neg_total | 40.0% |
| CD8 RO intB7_CD3 | 35.0% |
| Tconv memCXCR3_CD3 | 35.0% |
| Tconv memCD27_mem | 35.0% |
| Tconv memCD27_Tconv | 32.5% |
| CD8 RO TIGIT_CD3 | 32.5% |
| Tconv memintB7_Tconv | 30.0% |
| CD8 RO CXCR3_CD8 | 27.5% |
| CCR4_CD8RO | 25.0% |
| CD8 RO CXCR3_total | 25.0% |
| Tconv memCCR4_Tconv | 25.0% |
| CD8  RO Ki67_CD3 | 25.0% |
| CD8 RO CD56_total | 22.5% |
| CXCR3_CD8RO | 22.5% |
| Tconv memPD1_total | 22.5% |
| CD8 RO DR_total | 20.0% |
| CD8 RO PD1_CD3 | 20.0% |
| NKCD56hi_total | 20.0% |
| Tconv memCD56_Tconv | 20.0% |
| CD16+mono_total | 15.0% |
| Tconv memCCR6_CD3 | 15.0% |
| Tconv memDR_Tconv | 15.0% |
| Tconv memTIGIT_Tconv | 15.0% |
| CD27negIgDneg_Bcells | 12.5% |
| Tconv memCCR4_mem | 12.5% |
| CD8pos_total | 12.5% |
| CD8 RO TIGIT_total | 12.5% |
| CD8 RO_total | 12.5% |
| CD8 RO CCR6_total | 12.5% |
| Tconv memPD1_mem | 12.5% |
| Bcells memory_CD3neg | 12.5% |
| nonTnonB_total | 12.5% |
| CD8 RO CD27_total | 10.0% |
| CD8 RA_total | 10.0% |
| CD8 RO CD56_CD8 | 10.0% |
| CD8 ncytotox RO CCR4_CD3 | 10.0% |
| NKCD56hi_CD3neg | 10.0% |
| Tconv memCCR4_total | 10.0% |
| Tconv memCD27_total | 10.0% |
| NKCD56hi_nonTnonB | 10.0% |
| Tconv memCD56_CD3 | 10.0% |
| CD8 RA CCR7 naive_CD8 | 7.5% |
| NK Ki67_total | 7.5% |
| Tconv memCCR5_total | 7.5% |
| Tconv memTIGIT_total | 7.5% |
| CD8 RO DR_CD8 | 7.5% |
| Tconv memCCR6_mem | 7.5% |
| Tconv memintB7_CD3 | 7.5% |
| CD14mono_total | 7.5% |
| Bcells memory_total | 5.0% |
| CD8 RA naive_CD3 | 5.0% |
| CD4neg_total | 5.0% |
| Bcells CD27negIgDneg_total | 5.0% |
| Tconv memCXCR3_total | 5.0% |
| Treg memory_total | 5.0% |
| nonTnonB_CD3neg | 5.0% |
| CD8 RO CCR6_CD8 | 5.0% |
| Bcells_CD3neg | 5.0% |
| CD8 RO_CD8 | 2.5% |
| Tconv memDR_total | 2.5% |
| CD8 RA_CD8 | 2.5% |
| PD1_CD8RO | 2.5% |
| CD3hi_CD3 | 2.5% |
| CD8 ncytotox RO CCR4_CD8ntox | 2.5% |
| Tconv memCD56_mem | 2.5% |
| Tconv memCD56_total | 2.5% |
| CD8 RO Ki67_CD8 | 2.5% |
| CD8 RO PD1_total | 2.5% |
| CD8 RO CCR4_total | 2.5% |
| Tconv memPD1_Tconv | 2.5% |
| NK Ki67_NK | 2.5% |
| Tconv memintB7_mem | 2.5% |
| CD8 RO intB7_total | 2.5% |
| Tconv memKi67_mem | 2.5% |
| Treg naive_CD4 | 2.5% |
| CD14+16+mono_myeloid | 2.5% |
| CD14mono_CD3neg | 2.5% |
| myeloid_total | 2.5% |
| CD27_CD8RO | 2.5% |

**Total features selected by FDR (p < 0.1)_t40**: 115

#### FDR (p < 0.1)_t50

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD8 RO CCR5_CD3 | 95.0% |
| CD4 Treg_CD4 | 95.0% |
| Tconv naive_total | 92.5% |
| Treg memory_CD4 | 90.0% |
| CD8pos_CD3 | 80.0% |
| Bcells CD27posIgDneg_total | 77.5% |
| CD4 Tconv_total | 77.5% |
| CD4 Tconv_CD3 | 72.5% |
| CD8 RO CXCR3_CD3 | 67.5% |
| CD27IgD_Bcells | 67.5% |
| Tconv naive_CD3 | 62.5% |
| CD8 RO CD56_CD3 | 60.0% |
| Treg memory_CD3 | 55.0% |
| CD8 RO CCR5_total | 55.0% |
| Tconv mem_Tconv | 55.0% |
| Tconv memCCR5_Tconv | 55.0% |
| Tconv naive_Tconv | 52.5% |
| CD8 RO CCR5_CD8 | 50.0% |
| CD16mono_CD3neg | 50.0% |
| Tconv memCXCR3_Tconv | 50.0% |
| Tconv memCCR5_mem | 47.5% |
| CD8 RO DR_CD3 | 47.5% |
| CD16mono_myeloid | 45.0% |
| CD8 RO_CD3 | 45.0% |
| CD4 Treg _CD3 | 45.0% |
| CD4neg_CD3 | 42.5% |
| CD8 RA_CD3 | 40.0% |
| CD8 RO CCR6_CD3 | 40.0% |
| CD14mono_myeloid | 37.5% |
| Tconv memCCR6_Tconv | 35.0% |
| Tconv memCXCR3_CD3 | 32.5% |
| Tconv memCXCR3_mem | 32.5% |
| Tconv memCCR5_CD3 | 30.0% |
| CD8 RO CD27_CD3 | 30.0% |
| CD8 RO TIGIT_CD3 | 30.0% |
| CCR5_CD8RO | 27.5% |
| CD3neg_total | 27.5% |
| CD3pos_total | 27.5% |
| CD8 RO intB7_CD3 | 25.0% |
| CD8 RO CXCR3_CD8 | 20.0% |
| Tconv memCD27_Tconv | 20.0% |
| CD8  RO Ki67_CD3 | 20.0% |
| CD8 RO CXCR3_total | 17.5% |
| Tconv memCD27_mem | 17.5% |
| NKCD56hi_total | 17.5% |
| Tconv memCCR4_Tconv | 17.5% |
| Tconv memCD56_Tconv | 15.0% |
| CXCR3_CD8RO | 15.0% |
| Tconv memKi67_total | 15.0% |
| Tconv memintB7_Tconv | 15.0% |
| CCR4_CD8RO | 12.5% |
| CD8 RO PD1_CD3 | 12.5% |
| CD8pos_total | 12.5% |
| CD8 RO DR_total | 12.5% |
| Tconv memCCR6_CD3 | 12.5% |
| NKCD56hi_nonTnonB | 10.0% |
| Tconv memPD1_total | 10.0% |
| Tconv memTIGIT_Tconv | 10.0% |
| Bcells memory_CD3neg | 10.0% |
| CD8 RO CCR6_total | 7.5% |
| CD8 RO CD27_total | 7.5% |
| CD27negIgDneg_Bcells | 7.5% |
| CD16+mono_total | 7.5% |
| Tconv memCCR4_mem | 7.5% |
| CD8 RA_total | 7.5% |
| NKCD56hi_CD3neg | 7.5% |
| Tconv memCD27_total | 5.0% |
| Tconv memDR_Tconv | 5.0% |
| nonTnonB_total | 5.0% |
| Bcells_CD3neg | 5.0% |
| CD8 ncytotox RO CCR4_CD3 | 5.0% |
| CD8 RO CD56_CD8 | 5.0% |
| CD8 RO_total | 5.0% |
| CD8 RO DR_CD8 | 5.0% |
| Tconv memCCR5_total | 5.0% |
| CD8 RO CD56_total | 5.0% |
| CD14mono_total | 5.0% |
| CD8 RA CCR7 naive_CD8 | 2.5% |
| NK Ki67_total | 2.5% |
| Tconv memCCR6_mem | 2.5% |
| Tconv memCXCR3_total | 2.5% |
| CD4neg_total | 2.5% |
| Tconv memPD1_mem | 2.5% |
| Tconv memKi67_mem | 2.5% |
| CD8 RO intB7_total | 2.5% |
| nonTnonB_CD3neg | 2.5% |
| Tconv memintB7_mem | 2.5% |
| Bcells memory_total | 2.5% |
| CD27_CD8RO | 2.5% |

**Total features selected by FDR (p < 0.1)_t50**: 89

#### FDR (p < 0.1)_t60

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD4 Treg_CD4 | 94.7% |
| Treg memory_CD4 | 86.8% |
| Tconv naive_total | 84.2% |
| CD8 RO CCR5_CD3 | 78.9% |
| CD8pos_CD3 | 71.1% |
| CD4 Tconv_total | 65.8% |
| CD4 Tconv_CD3 | 63.2% |
| CD8 RO CXCR3_CD3 | 63.2% |
| Bcells CD27posIgDneg_total | 57.9% |
| CD27IgD_Bcells | 55.3% |
| Tconv naive_CD3 | 52.6% |
| Tconv naive_Tconv | 47.4% |
| Tconv mem_Tconv | 47.4% |
| Tconv memCCR5_Tconv | 44.7% |
| CD8 RO CD56_CD3 | 42.1% |
| CD8 RO DR_CD3 | 42.1% |
| Tconv memCXCR3_Tconv | 42.1% |
| CD8 RO CCR5_total | 42.1% |
| CD8 RO_CD3 | 39.5% |
| CD8 RA_CD3 | 39.5% |
| CD16mono_myeloid | 36.8% |
| Tconv memCCR5_mem | 34.2% |
| CD16mono_CD3neg | 31.6% |
| Treg memory_CD3 | 31.6% |
| CD4neg_CD3 | 31.6% |
| CD8 RO CCR6_CD3 | 28.9% |
| CD14mono_myeloid | 28.9% |
| CD8 RO CCR5_CD8 | 28.9% |
| Tconv memCCR5_CD3 | 26.3% |
| CD8 RO CD27_CD3 | 26.3% |
| CD4 Treg _CD3 | 23.7% |
| CD8 RO TIGIT_CD3 | 21.1% |
| Tconv memCCR6_Tconv | 21.1% |
| CD8 RO intB7_CD3 | 21.1% |
| Tconv memCXCR3_CD3 | 21.1% |
| Tconv memCXCR3_mem | 18.4% |
| CCR5_CD8RO | 15.8% |
| CD8 RO CXCR3_total | 13.2% |
| Tconv memKi67_total | 13.2% |
| CD3pos_total | 13.2% |
| Tconv memCCR4_Tconv | 13.2% |
| CD3neg_total | 13.2% |
| NKCD56hi_CD3neg | 7.9% |
| CXCR3_CD8RO | 7.9% |
| CD8  RO Ki67_CD3 | 7.9% |
| CD8 RA_total | 7.9% |
| Tconv memCD27_mem | 7.9% |
| CCR4_CD8RO | 7.9% |
| NKCD56hi_nonTnonB | 7.9% |
| NKCD56hi_total | 7.9% |
| CD16+mono_total | 7.9% |
| CD8pos_total | 5.3% |
| CD8 RO DR_total | 5.3% |
| CD27negIgDneg_Bcells | 5.3% |
| nonTnonB_total | 5.3% |
| Tconv memintB7_Tconv | 5.3% |
| Tconv memCCR4_mem | 5.3% |
| Tconv memCD56_Tconv | 5.3% |
| Tconv memCCR6_CD3 | 5.3% |
| CD8 RO PD1_CD3 | 5.3% |
| Tconv memCD27_Tconv | 5.3% |
| Bcells memory_CD3neg | 5.3% |
| Tconv memTIGIT_Tconv | 5.3% |
| NK Ki67_total | 2.6% |
| CD8 ncytotox RO CCR4_CD3 | 2.6% |
| CD8 RO_total | 2.6% |
| CD8 RO CCR6_total | 2.6% |
| CD8 RO CD27_total | 2.6% |
| CD8 RO CD56_CD8 | 2.6% |
| Tconv memCCR6_mem | 2.6% |
| Tconv memCCR5_total | 2.6% |
| CD8 RO CXCR3_CD8 | 2.6% |
| Bcells_CD3neg | 2.6% |
| nonTnonB_CD3neg | 2.6% |
| Tconv memPD1_mem | 2.6% |
| Bcells memory_total | 2.6% |
| CD14mono_total | 2.6% |
| CD27_CD8RO | 2.6% |
| Tconv memDR_Tconv | 2.6% |
| CD8 RO DR_CD8 | 2.6% |

**Total features selected by FDR (p < 0.1)_t60**: 80

#### FDR (p < 0.1)_t70

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Tconv naive_total | 75.7% |
| CD4 Treg_CD4 | 75.7% |
| CD8 RO CCR5_CD3 | 70.3% |
| Treg memory_CD4 | 62.2% |
| CD8pos_CD3 | 54.1% |
| CD8 RO CXCR3_CD3 | 51.4% |
| CD4 Tconv_total | 51.4% |
| CD27IgD_Bcells | 51.4% |
| CD4 Tconv_CD3 | 48.6% |
| Bcells CD27posIgDneg_total | 43.2% |
| Tconv naive_CD3 | 40.5% |
| CD8 RO_CD3 | 27.0% |
| CD8 RO CD56_CD3 | 27.0% |
| Tconv mem_Tconv | 27.0% |
| Tconv memCXCR3_Tconv | 27.0% |
| CD8 RO CCR5_total | 27.0% |
| Tconv memCCR5_Tconv | 27.0% |
| CD8 RA_CD3 | 24.3% |
| CD14mono_myeloid | 24.3% |
| CD4neg_CD3 | 24.3% |
| Tconv naive_Tconv | 24.3% |
| CD8 RO DR_CD3 | 24.3% |
| CD16mono_myeloid | 21.6% |
| CD16mono_CD3neg | 21.6% |
| CD8 RO CD27_CD3 | 21.6% |
| CD8 RO CCR5_CD8 | 21.6% |
| Tconv memCCR5_mem | 21.6% |
| CD8 RO CCR6_CD3 | 18.9% |
| Treg memory_CD3 | 18.9% |
| CD8 RO TIGIT_CD3 | 16.2% |
| CD4 Treg _CD3 | 16.2% |
| Tconv memCXCR3_CD3 | 13.5% |
| Tconv memKi67_total | 10.8% |
| Tconv memCCR5_CD3 | 10.8% |
| Tconv memCCR4_Tconv | 10.8% |
| Tconv memCXCR3_mem | 8.1% |
| Tconv memCCR6_Tconv | 8.1% |
| CD8 RO intB7_CD3 | 5.4% |
| CCR4_CD8RO | 5.4% |
| CD27negIgDneg_Bcells | 5.4% |
| CD8 RO CXCR3_total | 5.4% |
| NKCD56hi_total | 5.4% |
| CCR5_CD8RO | 5.4% |
| CD3pos_total | 5.4% |
| CD3neg_total | 5.4% |
| NKCD56hi_nonTnonB | 5.4% |
| CD8 RO CCR6_total | 2.7% |
| CD8 RA_total | 2.7% |
| CD8pos_total | 2.7% |
| CD8 RO CXCR3_CD8 | 2.7% |
| CD16+mono_total | 2.7% |
| Tconv memCCR6_CD3 | 2.7% |
| CD8 ncytotox RO CCR4_CD3 | 2.7% |
| Tconv memCCR6_mem | 2.7% |
| Tconv memCD27_mem | 2.7% |
| Tconv memintB7_Tconv | 2.7% |
| Tconv memCD56_Tconv | 2.7% |
| Tconv memCD27_Tconv | 2.7% |
| CD27_CD8RO | 2.7% |
| CD8 RO DR_total | 2.7% |
| CD8 RO DR_CD8 | 2.7% |

**Total features selected by FDR (p < 0.1)_t70**: 61

#### FDR (p < 0.1)_t80

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Tconv naive_total | 67.6% |
| CD4 Treg_CD4 | 61.8% |
| CD8 RO CCR5_CD3 | 55.9% |
| CD8pos_CD3 | 52.9% |
| Treg memory_CD4 | 47.1% |
| CD4 Tconv_CD3 | 44.1% |
| CD4 Tconv_total | 35.3% |
| CD8 RO CXCR3_CD3 | 32.4% |
| Bcells CD27posIgDneg_total | 29.4% |
| CD27IgD_Bcells | 26.5% |
| Tconv naive_CD3 | 20.6% |
| CD16mono_myeloid | 17.6% |
| Tconv memCCR5_Tconv | 17.6% |
| CD8 RO CD56_CD3 | 17.6% |
| CD8 RO_CD3 | 17.6% |
| CD4neg_CD3 | 17.6% |
| CD14mono_myeloid | 17.6% |
| Tconv memCCR5_mem | 14.7% |
| CD8 RO DR_CD3 | 14.7% |
| Tconv memCXCR3_Tconv | 14.7% |
| CD8 RA_CD3 | 14.7% |
| Treg memory_CD3 | 14.7% |
| CD16mono_CD3neg | 11.8% |
| CD8 RO CD27_CD3 | 11.8% |
| CD8 RO CCR5_CD8 | 8.8% |
| CD8 RO CCR5_total | 8.8% |
| CD8 RO CCR6_CD3 | 8.8% |
| Tconv memCCR6_Tconv | 8.8% |
| Tconv naive_Tconv | 5.9% |
| CD8 RO TIGIT_CD3 | 5.9% |
| Tconv memKi67_total | 5.9% |
| Tconv mem_Tconv | 5.9% |
| CD8 RO intB7_CD3 | 2.9% |
| CD8pos_total | 2.9% |
| CD8 RO CXCR3_total | 2.9% |
| Tconv memCXCR3_CD3 | 2.9% |
| NKCD56hi_total | 2.9% |
| Tconv memCCR5_CD3 | 2.9% |
| CCR4_CD8RO | 2.9% |
| CCR5_CD8RO | 2.9% |
| NKCD56hi_nonTnonB | 2.9% |
| Tconv memCCR6_CD3 | 2.9% |
| Tconv memCD27_Tconv | 2.9% |
| Tconv memCCR4_Tconv | 2.9% |
| CD4 Treg _CD3 | 2.9% |
| CD3pos_total | 2.9% |
| CD3neg_total | 2.9% |
| CD8 RO DR_CD8 | 2.9% |

**Total features selected by FDR (p < 0.1)_t80**: 48

#### LASSO_Lenient_t40

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD14mono_myeloid | 52.5% |
| CD27IgD_Bcells | 50.0% |
| CCR4_CD8RO | 50.0% |
| NKCD56hi_nonTnonB | 47.5% |
| CD16mono_myeloid | 47.5% |
| Tconv memPD1_mem | 37.5% |
| CD3hi_CD4neg | 37.5% |
| NKCD56hi_total | 32.5% |
| CD8pos_CD3 | 27.5% |
| CD14+16+mono_myeloid | 27.5% |
| Bcells CD27negIgDneg_total | 25.0% |
| Tconv memKi67_mem | 22.5% |
| Tconv memKi67_total | 22.5% |
| CD8 RA_CD3 | 20.0% |
| CD8 RO CCR5_CD3 | 20.0% |
| CD8 RO CCR5_CD8 | 20.0% |
| CD8 RA_total | 17.5% |
| DR_CD8RO | 17.5% |
| CD27negIgDneg_Bcells | 17.5% |
| CD4 Tconv_total | 15.0% |
| Tconv naive_total | 15.0% |
| Tconv memCCR6_mem | 15.0% |
| Tconv memCCR6_CD3 | 15.0% |
| CD8 RA CCR7 naive_CD8 | 12.5% |
| CD8 RO CXCR3_CD3 | 12.5% |
| Ki67_Bcells | 12.5% |
| Tconv memCXCR3_Tconv | 12.5% |
| CD8 RO CXCR3_CD8 | 12.5% |
| Treg naive_CD4 | 12.5% |
| Bcells CD27posIgDneg_total | 10.0% |
| CD16mono_CD3neg | 10.0% |
| CD4 Treg_CD4 | 10.0% |
| Tconv memCCR6_Tconv | 10.0% |
| Tconv memCCR4_mem | 10.0% |
| CD3hi_total | 10.0% |
| NKCD56hi_NK | 7.5% |
| CD8 RO TIGIT_CD3 | 7.5% |
| Bcells Ki67_CD3neg | 7.5% |
| TIGIT_CD8RO | 7.5% |
| CCR5_CD8RO | 7.5% |
| CD8 RA naive_CD3 | 7.5% |
| CD8 RO DR_CD8 | 7.5% |
| Tconv memCXCR3_CD3 | 7.5% |
| Tconv naive_CD3 | 7.5% |
| CD4neg_CD3 | 7.5% |
| CD8 RO CD27_CD3 | 7.5% |
| Bcells memory_total | 5.0% |
| Treg memory_CD4 | 5.0% |
| Tconv memCD56_total | 5.0% |
| Treg memory_total | 5.0% |
| Treg naive_total | 5.0% |
| NK Ki67_NK | 5.0% |
| Bcells Ki67_total | 5.0% |
| Tconv memCXCR3_total | 2.5% |
| Tconv memCD27_mem | 2.5% |
| Ki67_CD8RO | 2.5% |
| CD8 RO CCR6_CD8 | 2.5% |
| CD4 Tconv_CD3 | 2.5% |
| Tconv memTIGIT_Tconv | 2.5% |
| Tconv memDR_total | 2.5% |
| CD27_CD8RO | 2.5% |
| Treg memory_CD3 | 2.5% |
| CD8 RO CCR5_total | 2.5% |
| NKCD56hi_CD3neg | 2.5% |
| CD8 RO intB7_CD8 | 2.5% |
| Tconv memCXCR3_mem | 2.5% |
| Tconv memCCR5_mem | 2.5% |
| Tconv memKi67_CD3 | 2.5% |
| CD8pos_total | 2.5% |
| CD8 RO CCR6_CD3 | 2.5% |
| NK_total | 2.5% |
| CD8 RO DR_CD3 | 2.5% |
| CD8 RO intB7_CD3 | 2.5% |
| CD8 RO PD1_total | 2.5% |
| Bcells_total | 2.5% |
| Tconv memintB7_Tconv | 2.5% |
| Tconv memDR_CD3 | 2.5% |
| CD8 RO CD56_CD3 | 2.5% |

**Total features selected by LASSO_Lenient_t40**: 78

#### LASSO_Lenient_t50

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD14mono_myeloid | 43.6% |
| CD27IgD_Bcells | 38.5% |
| CCR4_CD8RO | 35.9% |
| CD16mono_myeloid | 30.8% |
| Tconv memPD1_mem | 28.2% |
| CD8pos_CD3 | 23.1% |
| CD3hi_CD4neg | 23.1% |
| NKCD56hi_nonTnonB | 23.1% |
| CD14+16+mono_myeloid | 23.1% |
| NKCD56hi_total | 17.9% |
| CD8 RO CCR5_CD3 | 17.9% |
| Tconv memKi67_total | 15.4% |
| Tconv memCXCR3_Tconv | 12.8% |
| CD8 RA_CD3 | 12.8% |
| Bcells CD27negIgDneg_total | 12.8% |
| Tconv memCCR6_CD3 | 12.8% |
| CD8 RO CCR5_CD8 | 12.8% |
| Tconv naive_total | 10.3% |
| CD8 RA CCR7 naive_CD8 | 10.3% |
| Bcells Ki67_CD3neg | 7.7% |
| CD16mono_CD3neg | 7.7% |
| CD27negIgDneg_Bcells | 7.7% |
| Tconv memKi67_mem | 7.7% |
| CD8 RA_total | 5.1% |
| DR_CD8RO | 5.1% |
| Treg naive_CD4 | 5.1% |
| CD4 Treg_CD4 | 5.1% |
| CD3hi_total | 5.1% |
| CD8 RO CD27_CD3 | 5.1% |
| CD4neg_CD3 | 5.1% |
| CD8 RO CXCR3_CD3 | 5.1% |
| NKCD56hi_NK | 5.1% |
| CD4 Tconv_total | 5.1% |
| CD8 RO TIGIT_CD3 | 5.1% |
| Tconv memCCR6_mem | 5.1% |
| CD8 RO DR_CD8 | 5.1% |
| Tconv memCD27_mem | 2.6% |
| CD8 RO CCR6_CD8 | 2.6% |
| Treg memory_CD3 | 2.6% |
| Treg naive_total | 2.6% |
| Ki67_CD8RO | 2.6% |
| Tconv memCXCR3_mem | 2.6% |
| Tconv memCXCR3_CD3 | 2.6% |
| Bcells CD27posIgDneg_total | 2.6% |
| CD8 RO intB7_CD8 | 2.6% |
| CD8 RO CCR5_total | 2.6% |
| CD8 RO CXCR3_CD8 | 2.6% |
| Tconv memCCR4_mem | 2.6% |
| CD8 RO CCR6_CD3 | 2.6% |
| CD8 RO DR_CD3 | 2.6% |
| NK_total | 2.6% |
| NK Ki67_NK | 2.6% |
| Bcells memory_total | 2.6% |
| CD8 RO PD1_total | 2.6% |
| TIGIT_CD8RO | 2.6% |
| Tconv memintB7_Tconv | 2.6% |
| CD8 RA naive_CD3 | 2.6% |
| CCR5_CD8RO | 2.6% |

**Total features selected by LASSO_Lenient_t50**: 58

#### LASSO_Lenient_t60

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD14mono_myeloid | 33.3% |
| CCR4_CD8RO | 30.6% |
| CD27IgD_Bcells | 27.8% |
| CD16mono_myeloid | 19.4% |
| Tconv memPD1_mem | 16.7% |
| CD8 RO CCR5_CD3 | 16.7% |
| CD8pos_CD3 | 13.9% |
| CD14+16+mono_myeloid | 13.9% |
| CD3hi_CD4neg | 11.1% |
| Tconv memCCR6_CD3 | 8.3% |
| NKCD56hi_total | 8.3% |
| NKCD56hi_nonTnonB | 8.3% |
| Tconv memCXCR3_Tconv | 8.3% |
| Tconv memKi67_total | 8.3% |
| Bcells Ki67_CD3neg | 5.6% |
| CD8 RO CCR5_CD8 | 5.6% |
| CD8 RO DR_CD8 | 5.6% |
| Treg naive_CD4 | 5.6% |
| CD8 RO CXCR3_CD3 | 5.6% |
| CD8 RA_CD3 | 5.6% |
| Tconv memCD27_mem | 2.8% |
| Tconv naive_total | 2.8% |
| Bcells CD27posIgDneg_total | 2.8% |
| CD8 RO TIGIT_CD3 | 2.8% |
| Bcells CD27negIgDneg_total | 2.8% |
| CD8 RO CXCR3_CD8 | 2.8% |
| Tconv memCXCR3_CD3 | 2.8% |
| CD8 RA CCR7 naive_CD8 | 2.8% |
| NKCD56hi_NK | 2.8% |
| CD8 RO DR_CD3 | 2.8% |
| CD8 RO CCR6_CD3 | 2.8% |
| NK_total | 2.8% |
| CD8 RO PD1_total | 2.8% |
| Tconv memintB7_Tconv | 2.8% |
| CCR5_CD8RO | 2.8% |

**Total features selected by LASSO_Lenient_t60**: 35

#### LASSO_Lenient_t70

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD27IgD_Bcells | 27.6% |
| CD14mono_myeloid | 27.6% |
| CCR4_CD8RO | 24.1% |
| Tconv memPD1_mem | 13.8% |
| CD8 RO CCR5_CD3 | 13.8% |
| CD8pos_CD3 | 10.3% |
| NKCD56hi_total | 10.3% |
| NKCD56hi_nonTnonB | 6.9% |
| CD16mono_myeloid | 6.9% |
| CD8 RO CCR5_CD8 | 6.9% |
| CD14+16+mono_myeloid | 6.9% |
| Tconv memCD27_mem | 3.4% |
| CD8 RO CXCR3_CD3 | 3.4% |
| CD8 RO DR_CD8 | 3.4% |
| CD8 RA_CD3 | 3.4% |
| CD3hi_CD4neg | 3.4% |
| CD8 RO TIGIT_CD3 | 3.4% |
| Tconv memCXCR3_Tconv | 3.4% |
| CD8 RO CCR6_CD3 | 3.4% |
| NK_total | 3.4% |
| Tconv memKi67_total | 3.4% |
| Bcells Ki67_CD3neg | 3.4% |

**Total features selected by LASSO_Lenient_t70**: 22

#### LASSO_Lenient_t80

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD27IgD_Bcells | 29.4% |
| CD14mono_myeloid | 23.5% |
| CD8pos_CD3 | 17.6% |
| Tconv memPD1_mem | 17.6% |
| CCR4_CD8RO | 17.6% |
| CD14+16+mono_myeloid | 11.8% |
| CD8 RO CCR5_CD3 | 11.8% |
| NKCD56hi_total | 5.9% |
| CD8 RO CCR5_CD8 | 5.9% |
| NKCD56hi_nonTnonB | 5.9% |
| Tconv memCXCR3_Tconv | 5.9% |

**Total features selected by LASSO_Lenient_t80**: 11

#### LASSO_RFE_t40

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD27IgD_Bcells | 50.0% |
| CD14mono_myeloid | 45.0% |
| CCR4_CD8RO | 45.0% |
| CD16mono_myeloid | 42.5% |
| NKCD56hi_nonTnonB | 27.5% |
| CD3hi_CD4neg | 25.0% |
| NKCD56hi_total | 25.0% |
| CD8pos_CD3 | 22.5% |
| Tconv memPD1_mem | 22.5% |
| CD8 RO CCR5_CD3 | 20.0% |
| Tconv memKi67_total | 17.5% |
| CD8 RO CCR5_CD8 | 17.5% |
| CD14+16+mono_myeloid | 17.5% |
| Tconv naive_total | 15.0% |
| CD8 RA_CD3 | 15.0% |
| Tconv memKi67_mem | 12.5% |
| Tconv memCCR6_CD3 | 12.5% |
| CD8 RO CXCR3_CD8 | 12.5% |
| Tconv memCXCR3_Tconv | 10.0% |
| CD4 Tconv_total | 10.0% |
| CD8 RO CXCR3_CD3 | 10.0% |
| Treg naive_CD4 | 10.0% |
| CD16mono_CD3neg | 10.0% |
| CD4 Treg_CD4 | 10.0% |
| CD27negIgDneg_Bcells | 10.0% |
| CD8 RO TIGIT_CD3 | 7.5% |
| Tconv memCCR6_Tconv | 7.5% |
| CD8 RO CD27_CD3 | 7.5% |
| CD3hi_total | 7.5% |
| CD8 RO DR_CD8 | 7.5% |
| CD4neg_CD3 | 7.5% |
| Tconv memCCR4_mem | 7.5% |
| Tconv memCCR6_mem | 7.5% |
| Tconv memCXCR3_CD3 | 5.0% |
| CD8 RA naive_CD3 | 5.0% |
| Tconv naive_CD3 | 5.0% |
| NKCD56hi_NK | 5.0% |
| Ki67_Bcells | 5.0% |
| Bcells CD27posIgDneg_total | 5.0% |
| Bcells CD27negIgDneg_total | 5.0% |
| Bcells memory_total | 5.0% |
| Treg memory_CD4 | 5.0% |
| CD8 RA_total | 5.0% |
| CD8 RA CCR7 naive_CD8 | 5.0% |
| Tconv memCXCR3_total | 2.5% |
| Tconv memCD27_mem | 2.5% |
| CD8 RO CCR6_CD8 | 2.5% |
| DR_CD8RO | 2.5% |
| CD4 Tconv_CD3 | 2.5% |
| Treg memory_CD3 | 2.5% |
| Tconv memDR_total | 2.5% |
| CD8 RO CCR5_total | 2.5% |
| Tconv memCCR5_mem | 2.5% |
| CD8pos_total | 2.5% |
| Treg memory_total | 2.5% |
| CD8 RO CCR6_CD3 | 2.5% |
| CD8 RO DR_CD3 | 2.5% |
| NK_total | 2.5% |
| CD8 RO PD1_total | 2.5% |
| Bcells_total | 2.5% |
| Tconv memintB7_Tconv | 2.5% |
| CCR5_CD8RO | 2.5% |
| CD8 RO CD56_CD3 | 2.5% |

**Total features selected by LASSO_RFE_t40**: 63

#### LASSO_RFE_t50

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD27IgD_Bcells | 35.9% |
| CD14mono_myeloid | 33.3% |
| CCR4_CD8RO | 30.8% |
| CD16mono_myeloid | 25.6% |
| CD8 RO CCR5_CD3 | 17.9% |
| CD8pos_CD3 | 15.4% |
| Tconv memPD1_mem | 15.4% |
| Tconv memKi67_total | 12.8% |
| CD3hi_CD4neg | 12.8% |
| CD14+16+mono_myeloid | 12.8% |
| Tconv memCCR6_CD3 | 12.8% |
| NKCD56hi_nonTnonB | 10.3% |
| Tconv naive_total | 10.3% |
| NKCD56hi_total | 10.3% |
| CD8 RO CCR5_CD8 | 10.3% |
| CD16mono_CD3neg | 7.7% |
| CD8 RA_CD3 | 7.7% |
| Tconv memCXCR3_Tconv | 7.7% |
| CD3hi_total | 5.1% |
| Treg naive_CD4 | 5.1% |
| CD8 RA CCR7 naive_CD8 | 5.1% |
| CD8 RO DR_CD8 | 5.1% |
| CD8 RO CXCR3_CD3 | 5.1% |
| CD8 RO TIGIT_CD3 | 5.1% |
| Tconv memCD27_mem | 2.6% |
| CD8 RO CCR6_CD8 | 2.6% |
| CD4neg_CD3 | 2.6% |
| CD4 Tconv_total | 2.6% |
| Treg memory_CD3 | 2.6% |
| Bcells CD27posIgDneg_total | 2.6% |
| Tconv memCXCR3_CD3 | 2.6% |
| Tconv memCCR4_mem | 2.6% |
| CD8 RO CCR5_total | 2.6% |
| CD8 RO CXCR3_CD8 | 2.6% |
| Bcells CD27negIgDneg_total | 2.6% |
| CD8 RO CCR6_CD3 | 2.6% |
| CD4 Treg_CD4 | 2.6% |
| NK_total | 2.6% |
| CD8 RO PD1_total | 2.6% |
| Tconv memintB7_Tconv | 2.6% |
| CD27negIgDneg_Bcells | 2.6% |

**Total features selected by LASSO_RFE_t50**: 41

#### LASSO_RFE_t60

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD14mono_myeloid | 30.3% |
| CD27IgD_Bcells | 27.3% |
| CCR4_CD8RO | 27.3% |
| CD8 RO CCR5_CD3 | 18.2% |
| CD16mono_myeloid | 15.2% |
| CD8pos_CD3 | 12.1% |
| Tconv memPD1_mem | 9.1% |
| NKCD56hi_total | 9.1% |
| CD14+16+mono_myeloid | 9.1% |
| NKCD56hi_nonTnonB | 6.1% |
| Tconv memCCR6_CD3 | 6.1% |
| CD8 RO CCR5_CD8 | 6.1% |
| Tconv memCXCR3_Tconv | 6.1% |
| Tconv memCD27_mem | 3.0% |
| CD8 RO CXCR3_CD3 | 3.0% |
| CD8 RO DR_CD8 | 3.0% |
| Tconv memCXCR3_CD3 | 3.0% |
| CD8 RA_CD3 | 3.0% |
| Tconv naive_total | 3.0% |
| CD8 RO TIGIT_CD3 | 3.0% |
| Bcells CD27posIgDneg_total | 3.0% |
| NK_total | 3.0% |
| CD8 RO PD1_total | 3.0% |
| Tconv memKi67_total | 3.0% |

**Total features selected by LASSO_RFE_t60**: 24

#### LASSO_RFE_t70

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD27IgD_Bcells | 28.6% |
| CCR4_CD8RO | 19.0% |
| CD14mono_myeloid | 19.0% |
| CD8 RO CCR5_CD3 | 19.0% |
| CD8pos_CD3 | 14.3% |
| NKCD56hi_total | 9.5% |
| Tconv memPD1_mem | 9.5% |
| Tconv memCD27_mem | 4.8% |
| CD8 RO CXCR3_CD3 | 4.8% |
| CD8 RO CCR5_CD8 | 4.8% |
| NKCD56hi_nonTnonB | 4.8% |
| Tconv memCXCR3_Tconv | 4.8% |
| CD14+16+mono_myeloid | 4.8% |
| NK_total | 4.8% |

**Total features selected by LASSO_RFE_t70**: 14

#### LASSO_RFE_t80

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD27IgD_Bcells | 26.7% |
| CD14mono_myeloid | 20.0% |
| CD8pos_CD3 | 20.0% |
| CD8 RO CCR5_CD3 | 13.3% |
| NKCD56hi_total | 6.7% |
| NKCD56hi_nonTnonB | 6.7% |
| CD8 RO CCR5_CD8 | 6.7% |
| Tconv memCXCR3_Tconv | 6.7% |
| CD14+16+mono_myeloid | 6.7% |
| CCR4_CD8RO | 6.7% |
| Tconv memPD1_mem | 6.7% |

**Total features selected by LASSO_RFE_t80**: 11

#### LASSO_Strict_t40

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CCR4_CD8RO | 30.6% |
| CD27IgD_Bcells | 27.8% |
| CD14mono_myeloid | 27.8% |
| CD16mono_myeloid | 22.2% |
| Tconv memPD1_mem | 22.2% |
| CD8pos_CD3 | 13.9% |
| CD8 RO CCR5_CD3 | 11.1% |
| CD14+16+mono_myeloid | 11.1% |
| CD8 RO CCR5_CD8 | 8.3% |
| CD3hi_CD4neg | 8.3% |
| Tconv memCCR6_CD3 | 8.3% |
| NKCD56hi_nonTnonB | 8.3% |
| NKCD56hi_total | 5.6% |
| CD8 RO DR_CD8 | 5.6% |
| Tconv memKi67_total | 5.6% |
| CD8 RO CXCR3_CD3 | 5.6% |
| Tconv memKi67_mem | 5.6% |
| CD8 RA_CD3 | 5.6% |
| Bcells CD27negIgDneg_total | 5.6% |
| CD8 RA_total | 2.8% |
| Tconv memCXCR3_Tconv | 2.8% |
| CD8 RO CCR6_CD8 | 2.8% |
| Bcells CD27posIgDneg_total | 2.8% |
| Tconv memCCR6_mem | 2.8% |
| CCR5_CD8RO | 2.8% |
| DR_CD8RO | 2.8% |
| NKCD56hi_NK | 2.8% |
| Tconv naive_total | 2.8% |
| NK Ki67_NK | 2.8% |
| Tconv memintB7_Tconv | 2.8% |
| Bcells Ki67_CD3neg | 2.8% |

**Total features selected by LASSO_Strict_t40**: 31

#### LASSO_Strict_t50

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CCR4_CD8RO | 28.0% |
| CD27IgD_Bcells | 24.0% |
| CD14mono_myeloid | 16.0% |
| CD16mono_myeloid | 16.0% |
| CD14+16+mono_myeloid | 12.0% |
| CD8pos_CD3 | 12.0% |
| CD8 RO CCR5_CD3 | 8.0% |
| NKCD56hi_total | 8.0% |
| CD8 RO CCR5_CD8 | 8.0% |
| Tconv memKi67_total | 8.0% |
| Tconv memPD1_mem | 8.0% |
| Tconv memCXCR3_Tconv | 4.0% |
| NKCD56hi_nonTnonB | 4.0% |
| Tconv naive_total | 4.0% |
| Bcells Ki67_CD3neg | 4.0% |
| CD8 RO DR_CD8 | 4.0% |

**Total features selected by LASSO_Strict_t50**: 16

#### LASSO_Strict_t60

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD8pos_CD3 | 20.0% |
| CD27IgD_Bcells | 20.0% |
| CCR4_CD8RO | 13.3% |
| Tconv memPD1_mem | 13.3% |
| CD14+16+mono_myeloid | 13.3% |
| CD14mono_myeloid | 13.3% |
| NKCD56hi_total | 6.7% |
| CD8 RO CCR5_CD8 | 6.7% |
| CD16mono_myeloid | 6.7% |
| NKCD56hi_nonTnonB | 6.7% |
| Bcells Ki67_CD3neg | 6.7% |

**Total features selected by LASSO_Strict_t60**: 11

#### LASSO_Strict_t70

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD8pos_CD3 | 16.7% |
| Tconv memPD1_mem | 16.7% |
| CD14mono_myeloid | 16.7% |
| CD14+16+mono_myeloid | 16.7% |
| CD27IgD_Bcells | 16.7% |
| CD16mono_myeloid | 8.3% |
| CD8 RO CCR5_CD8 | 8.3% |
| CCR4_CD8RO | 8.3% |

**Total features selected by LASSO_Strict_t70**: 8

#### LASSO_Strict_t80

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD8pos_CD3 | 33.3% |
| CD14+16+mono_myeloid | 33.3% |
| CD14mono_myeloid | 33.3% |
| CCR4_CD8RO | 33.3% |

**Total features selected by LASSO_Strict_t80**: 4

#### LogisticRegression_Permutation_Top10%_t40

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

**Total features selected by LogisticRegression_Permutation_Top10%_t40**: 16

#### LogisticRegression_Permutation_Top10%_t50

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

**Total features selected by LogisticRegression_Permutation_Top10%_t50**: 16

#### LogisticRegression_Permutation_Top10%_t60

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

**Total features selected by LogisticRegression_Permutation_Top10%_t60**: 16

#### LogisticRegression_Permutation_Top10%_t70

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

**Total features selected by LogisticRegression_Permutation_Top10%_t70**: 16

#### LogisticRegression_Permutation_Top10%_t80

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD3pos_total | 100.0% |
| CD4 Tconv_total | 100.0% |
| CD4 Tconv mem_total | 100.0% |
| Tconv memCCR4_total | 100.0% |
| Tconv memCD56_total | 100.0% |
| Tconv memCD27_total | 100.0% |
| Tconv memDR_total | 100.0% |
| Tconv memCXCR3_total | 100.0% |
| Tconv memPD1_total | 100.0% |
| Tconv memTIGIT_total | 100.0% |
| Tconv memintB7_total | 100.0% |
| Tconv memKi67_total | 100.0% |
| Tconv naive_total | 100.0% |
| CD4 Treg_total | 100.0% |
| Tconv memCCR5_total | 97.5% |
| Tconv memCCR6_total | 85.0% |

**Total features selected by LogisticRegression_Permutation_Top10%_t80**: 16

#### Mutual Information (Top 10%)_t40

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD8pos_CD3 | 65.0% |
| Treg memory_CD4 | 47.5% |
| CD4 Treg_CD4 | 47.5% |
| nonTnonB_total | 40.0% |
| CD8 RO CCR5_CD3 | 37.5% |
| Tconv naive_total | 35.0% |
| CD4 Tconv_total | 32.5% |
| CD8 RO_CD3 | 27.5% |
| CD8 RO TIGIT_CD3 | 25.0% |
| CD4 Treg _CD3 | 22.5% |
| Tconv naive_CD3 | 22.5% |
| TIGIT_CD8RO | 22.5% |
| CD8 RO CD27_CD3 | 20.0% |
| CD8pos_total | 20.0% |
| NK Ki67_nonTnonB | 20.0% |
| CD8 RO CCR6_CD3 | 20.0% |
| CD16mono_CD3neg | 17.5% |
| CD27IgD_Bcells | 17.5% |
| CD16mono_myeloid | 15.0% |
| Tconv memPD1_mem | 15.0% |
| Bcells_CD3neg | 15.0% |
| Treg naive_CD4 | 15.0% |
| CD8 RA_CD3 | 15.0% |
| CD3pos_total | 12.5% |
| CD3neg_total | 12.5% |
| CD8 RO DR_total | 12.5% |
| nonTnonB_CD3neg | 12.5% |
| DR_CD8RO | 12.5% |
| Bcells CD27posIgDneg_total | 12.5% |
| CD8 RO CCR5_total | 12.5% |
| Tconv memCCR5_CD3 | 12.5% |
| intB7_CD8RO | 10.0% |
| PD1_CD8RO | 10.0% |
| Tconv memCXCR3_Tconv | 10.0% |
| Ki67_CD8RO | 10.0% |
| CD8  RO Ki67_CD3 | 10.0% |
| Tconv memTIGIT_CD3 | 10.0% |
| CD8 RA naive_CD3 | 10.0% |
| CD8 RO CCR5_CD8 | 10.0% |
| NK Ki67_total | 7.5% |
| Treg memory_total | 7.5% |
| CD8 ncytotox RO CCR4_CD8ntox | 7.5% |
| Ki67_Bcells | 7.5% |
| NKCD16_CD3neg | 7.5% |
| Treg memory_CD3 | 7.5% |
| Tconv memCD27_total | 7.5% |
| CD4neg_CD3 | 7.5% |
| CD14mono_total | 7.5% |
| CD14mono_myeloid | 5.0% |
| Bcells memory_total | 5.0% |
| NK Ki67_NK | 5.0% |
| Tconv naive_Tconv | 5.0% |
| Tconv memCCR6_mem | 5.0% |
| CD27_CD8RO | 5.0% |
| Tconv memDR_CD3 | 5.0% |
| CD8 RO DR_CD8 | 5.0% |
| CCR5_CD8RO | 5.0% |
| Bcells_total | 5.0% |
| Tconv memCCR5_mem | 5.0% |
| Tconv memKi67_CD3 | 5.0% |
| Tconv memintB7_CD3 | 5.0% |
| CD14mono_CD3neg | 5.0% |
| Tconv memCCR6_CD3 | 5.0% |
| Tconv memTIGIT_total | 2.5% |
| NK_CD3neg | 2.5% |
| CD8 RO DR_CD3 | 2.5% |
| CD4 Tconv_CD3 | 2.5% |
| Tconv memCCR4_total | 2.5% |
| NK_total | 2.5% |
| CD8 RO intB7_CD3 | 2.5% |
| CD8 RO CD56_CD3 | 2.5% |
| Tconv memTIGIT_mem | 2.5% |
| CD8 RO intB7_CD8 | 2.5% |
| Tconv memCCR5_total | 2.5% |
| CD8 RO CD56_CD8 | 2.5% |
| Tconv memCD27_mem | 2.5% |
| Bcells Ki67_CD3neg | 2.5% |
| NKCD16_NK | 2.5% |
| Tconv memCD56_total | 2.5% |
| Tconv memKi67_mem | 2.5% |
| Tconv memintB7_Tconv | 2.5% |
| NKCD56hi_total | 2.5% |
| Tconv memKi67_total | 2.5% |
| Tconv memCD56_Tconv | 2.5% |
| CD3hi_total | 2.5% |
| NK_nonTnonB | 2.5% |
| CD8 ncytotox RO CCR4_CD3 | 2.5% |
| CD8 RO CCR4_total | 2.5% |
| Tconv memTIGIT_Tconv | 2.5% |
| Tconv memCD27_CD3 | 2.5% |
| Tconv memPD1_CD3 | 2.5% |
| CD4 Tconv mem_total | 2.5% |
| CD8 RO CXCR3_CD3 | 2.5% |
| Tconv mem_CD3 | 2.5% |

**Total features selected by Mutual Information (Top 10%)_t40**: 94

#### Mutual Information (Top 10%)_t50

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD8pos_CD3 | 52.5% |
| Treg memory_CD4 | 32.5% |
| nonTnonB_total | 32.5% |
| Tconv naive_total | 25.0% |
| CD4 Treg_CD4 | 25.0% |
| CD8 RO CCR5_CD3 | 22.5% |
| CD4 Tconv_total | 22.5% |
| TIGIT_CD8RO | 17.5% |
| CD8 RO_CD3 | 12.5% |
| nonTnonB_CD3neg | 10.0% |
| CD8 RO TIGIT_CD3 | 10.0% |
| DR_CD8RO | 10.0% |
| CD8pos_total | 10.0% |
| CD8 RO CCR6_CD3 | 10.0% |
| Treg naive_CD4 | 10.0% |
| Tconv naive_CD3 | 10.0% |
| NK Ki67_nonTnonB | 10.0% |
| CD8  RO Ki67_CD3 | 7.5% |
| CD8 RO CD27_CD3 | 7.5% |
| CD27IgD_Bcells | 7.5% |
| CD8 RO CCR5_total | 7.5% |
| PD1_CD8RO | 7.5% |
| CD8 RA_CD3 | 7.5% |
| CD8 RO DR_total | 7.5% |
| CD4 Treg _CD3 | 7.5% |
| CD3neg_total | 5.0% |
| Tconv memCCR6_mem | 5.0% |
| CD8 RO CCR5_CD8 | 5.0% |
| Bcells_CD3neg | 5.0% |
| CD8 RA naive_CD3 | 5.0% |
| CD3pos_total | 5.0% |
| intB7_CD8RO | 5.0% |
| CD14mono_total | 5.0% |
| Treg memory_total | 5.0% |
| Treg memory_CD3 | 5.0% |
| Tconv memPD1_mem | 5.0% |
| NKCD16_CD3neg | 2.5% |
| CD8 RO DR_CD3 | 2.5% |
| Tconv memCD27_total | 2.5% |
| CD14mono_CD3neg | 2.5% |
| Tconv memCCR5_CD3 | 2.5% |
| NK_CD3neg | 2.5% |
| Bcells Ki67_CD3neg | 2.5% |
| NK_total | 2.5% |
| Tconv memTIGIT_CD3 | 2.5% |
| Ki67_CD8RO | 2.5% |
| Tconv memKi67_mem | 2.5% |
| CD8 RO CD56_CD8 | 2.5% |
| Tconv memCCR5_mem | 2.5% |
| Tconv memCXCR3_Tconv | 2.5% |
| Tconv memCD56_Tconv | 2.5% |
| CD4neg_CD3 | 2.5% |
| CD3hi_total | 2.5% |
| Tconv memKi67_total | 2.5% |
| Tconv memKi67_CD3 | 2.5% |
| CD16mono_CD3neg | 2.5% |
| NK Ki67_NK | 2.5% |
| Ki67_Bcells | 2.5% |
| Tconv memintB7_CD3 | 2.5% |
| CD27_CD8RO | 2.5% |
| Bcells CD27posIgDneg_total | 2.5% |
| CD8 RO CXCR3_CD3 | 2.5% |

**Total features selected by Mutual Information (Top 10%)_t50**: 62

#### Mutual Information (Top 10%)_t60

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD8pos_CD3 | 43.2% |
| Treg memory_CD4 | 24.3% |
| CD8 RO CCR5_CD3 | 21.6% |
| CD4 Tconv_total | 18.9% |
| CD4 Treg_CD4 | 13.5% |
| Tconv naive_total | 13.5% |
| nonTnonB_total | 13.5% |
| TIGIT_CD8RO | 10.8% |
| Tconv naive_CD3 | 10.8% |
| CD8 RO_CD3 | 8.1% |
| CD27IgD_Bcells | 8.1% |
| Treg naive_CD4 | 8.1% |
| CD8 RA_CD3 | 5.4% |
| CD8pos_total | 5.4% |
| CD8 RO CCR5_total | 5.4% |
| CD8 RO CCR6_CD3 | 5.4% |
| CD14mono_total | 5.4% |
| CD8 RO TIGIT_CD3 | 5.4% |
| CD8 RA naive_CD3 | 2.7% |
| NKCD16_CD3neg | 2.7% |
| Treg memory_CD3 | 2.7% |
| CD8 RO DR_total | 2.7% |
| Tconv memCCR5_mem | 2.7% |
| CD8  RO Ki67_CD3 | 2.7% |
| CD8 RO CD56_CD8 | 2.7% |
| PD1_CD8RO | 2.7% |
| CD4 Treg _CD3 | 2.7% |
| CD8 RO CD27_CD3 | 2.7% |
| Tconv memKi67_CD3 | 2.7% |
| NK Ki67_NK | 2.7% |
| Bcells CD27posIgDneg_total | 2.7% |
| NK Ki67_nonTnonB | 2.7% |

**Total features selected by Mutual Information (Top 10%)_t60**: 32

#### Mutual Information (Top 10%)_t70

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD8pos_CD3 | 37.9% |
| CD8 RO CCR5_CD3 | 13.8% |
| TIGIT_CD8RO | 13.8% |
| CD8 RO_CD3 | 10.3% |
| Treg memory_CD4 | 10.3% |
| Tconv naive_total | 10.3% |
| nonTnonB_total | 6.9% |
| Treg naive_CD4 | 6.9% |
| CD4 Tconv_total | 6.9% |
| CD8 RA naive_CD3 | 3.4% |
| Treg memory_CD3 | 3.4% |
| CD8 RO DR_total | 3.4% |
| CD8 RO CCR6_CD3 | 3.4% |
| PD1_CD8RO | 3.4% |
| Tconv naive_CD3 | 3.4% |
| CD4 Treg_CD4 | 3.4% |
| Bcells CD27posIgDneg_total | 3.4% |

**Total features selected by Mutual Information (Top 10%)_t70**: 17

#### Mutual Information (Top 10%)_t80

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD8pos_CD3 | 45.5% |
| TIGIT_CD8RO | 27.3% |
| CD8 RO CCR5_CD3 | 18.2% |
| Treg naive_CD4 | 9.1% |
| Bcells CD27posIgDneg_total | 9.1% |

**Total features selected by Mutual Information (Top 10%)_t80**: 5

#### NaiveBayes_Permutation_AboveMean_t40

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Bcells memory_total | 90.0% |
| Bcells CD27posIgDneg_total | 90.0% |
| CD8 RO CCR5_CD3 | 85.0% |
| Bcells memory_CD3neg | 85.0% |
| CD3hi_total | 82.5% |
| Ki67_CD8RO | 82.5% |
| CD8 RO Ki67_CD8 | 80.0% |
| CD8 RO Ki67_total | 80.0% |
| CD8  RO Ki67_CD3 | 75.0% |
| NK Ki67_NK | 75.0% |
| CD8 RO DR_total | 75.0% |
| CD8 RO DR_CD3 | 75.0% |
| NKCD56hi_NK | 72.5% |
| NKCD16_NK | 70.0% |
| Tconv memCD56_Tconv | 70.0% |
| Tconv memCXCR3_total | 65.0% |
| CD27negIgDneg_Bcells | 65.0% |
| CD8 RO CD56_CD3 | 65.0% |
| CD16mono_myeloid | 62.5% |
| CD8 RO CCR6_CD3 | 62.5% |
| CD14+16+mono_total | 60.0% |
| Tconv memCD56_mem | 60.0% |
| DR_CD8RO | 57.5% |
| Tconv memCXCR3_Tconv | 57.5% |
| NK Ki67_total | 52.5% |
| CD27IgD_Bcells | 52.5% |
| CD8 RO CD56_total | 50.0% |
| Bcells_total | 50.0% |
| CD8 RO intB7_CD3 | 50.0% |
| CD8 RO CXCR3_CD3 | 50.0% |
| CD14+16+mono_CD3neg | 47.5% |
| Tconv memCD56_CD3 | 47.5% |
| CD8 RA naive_CD3 | 45.0% |
| Tconv memCD56_total | 45.0% |
| Tconv memCXCR3_CD3 | 45.0% |
| NKCD16_total | 45.0% |
| CD14mono_myeloid | 42.5% |
| NK_total | 42.5% |
| CD8 RO CCR5_total | 40.0% |
| NKCD56hi_total | 40.0% |
| Bcells naive_total | 37.5% |
| CD8 RO CCR6_total | 37.5% |
| Tconv memCCR5_total | 37.5% |
| Treg naive_total | 37.5% |
| Tconv memCCR5_Tconv | 37.5% |
| CD3hi_CD4neg | 35.0% |
| Bcells CD27negIgDneg_total | 32.5% |
| Ki67_Bcells | 32.5% |
| NK Ki67_CD3neg | 32.5% |
| CD14+16+mono_myeloid | 30.0% |
| CD8 RA_CD3 | 30.0% |
| Tconv memTIGIT_total | 30.0% |
| Tconv memCD27_mem | 30.0% |
| CD3hi_CD3 | 27.5% |
| Bcells naive_CD3neg | 27.5% |
| Tconv memCXCR3_mem | 27.5% |
| Tconv memPD1_mem | 27.5% |
| Tconv memKi67_total | 27.5% |
| CD8 RO_CD3 | 25.0% |
| CD8 RO intB7_total | 25.0% |
| NK Ki67_nonTnonB | 25.0% |
| Tconv naive_total | 25.0% |
| CD8 RA naive_total | 22.5% |
| Bcells Ki67_CD3neg | 22.5% |
| nonTnonB_CD3neg | 22.5% |
| CD8 RO DR_CD8 | 20.0% |
| Tconv memintB7_Tconv | 20.0% |
| Bcells_CD3neg | 20.0% |
| CD16+mono_total | 20.0% |
| CD4 Treg_CD4 | 20.0% |
| Tconv memCCR5_CD3 | 20.0% |
| CD27_CD8RO | 20.0% |
| CD8 RO CXCR3_total | 20.0% |
| Treg memory_CD4 | 20.0% |
| CD8 RO CCR4_total | 17.5% |
| CD8 ncytotox RO CCR4_CD3 | 17.5% |
| Tconv memCCR6_CD3 | 17.5% |
| CD4 Tconv_total | 17.5% |
| Tconv memCCR6_mem | 15.0% |
| CD16mono_CD3neg | 15.0% |
| CD3pos_total | 15.0% |
| Bcells Ki67_total | 15.0% |
| CD3neg_total | 15.0% |
| CD8 RO CD27_CD3 | 15.0% |
| Treg naive_CD3 | 15.0% |
| Tconv memintB7_CD3 | 15.0% |
| Tconv memTIGIT_Tconv | 15.0% |
| Tconv memintB7_total | 15.0% |
| CXCR3_CD8RO | 15.0% |
| CD8pos_CD3 | 15.0% |
| CD8 RO CCR5_CD8 | 15.0% |
| Tconv memCCR6_Tconv | 15.0% |
| CD4 Treg_total | 12.5% |
| Tconv memDR_total | 12.5% |
| Tconv memCCR4_total | 12.5% |
| CD8 RO PD1_CD3 | 12.5% |
| CD8 RA_total | 12.5% |
| CD4neg_CD3 | 12.5% |
| CCR4_CD8RO | 12.5% |
| CD8 RO PD1_CD8 | 12.5% |
| CD8 RO CD56_CD8 | 12.5% |
| CD8 ncytotox RO CCR4_CD8ntox | 10.0% |
| Tconv memintB7_mem | 10.0% |
| Tconv memCD27_total | 10.0% |
| NKCD56hi_CD3neg | 10.0% |
| Tconv memCCR4_mem | 10.0% |
| CD8 RO TIGIT_CD3 | 10.0% |
| Tconv memCD27_CD3 | 10.0% |
| intB7_CD8RO | 10.0% |
| TIGIT_CD8RO | 10.0% |
| CD8 RO PD1_total | 10.0% |
| Tconv memCCR5_mem | 10.0% |
| Tconv memCCR4_CD3 | 7.5% |
| Tconv memKi67_Tconv | 7.5% |
| Tconv memDR_mem | 7.5% |
| Tconv memPD1_total | 7.5% |
| Treg memory_CD3 | 7.5% |
| CD4 Treg _CD3 | 7.5% |
| CD8pos_total | 7.5% |
| CD4 Tconv_CD3 | 7.5% |
| Tconv memKi67_CD3 | 7.5% |
| NKCD16_nonTnonB | 7.5% |
| Tconv memCD27_Tconv | 7.5% |
| CD56_CD8RO | 7.5% |
| Tconv memTIGIT_mem | 7.5% |
| CD8 RO intB7_CD8 | 7.5% |
| myeloid_CD3neg | 7.5% |
| naive_Bcells | 7.5% |
| NK_nonTnonB | 7.5% |
| Tconv memTIGIT_CD3 | 5.0% |
| CD4neg_total | 5.0% |
| Treg naive_CD4 | 5.0% |
| CD8 RO CXCR3_CD8 | 5.0% |
| Tconv memCCR6_total | 5.0% |
| CD8 RA CCR7 naive_CD8 | 5.0% |
| NKCD56hi_nonTnonB | 5.0% |
| Tconv memKi67_mem | 5.0% |
| CD14mono_CD3neg | 5.0% |
| Tconv memCCR4_Tconv | 5.0% |
| nonTnonB_total | 5.0% |
| Tconv naive_Tconv | 5.0% |
| memory_Bcells | 5.0% |
| CD8 RO CCR6_CD8 | 5.0% |
| CD8 RO TIGIT_CD8 | 5.0% |
| CD4 Tconv mem_total | 5.0% |
| Treg memory_total | 5.0% |
| Tconv memPD1_CD3 | 5.0% |
| Tconv mem_Tconv | 5.0% |
| CCR6_CD8RO | 5.0% |
| Tconv memDR_Tconv | 5.0% |
| CD8 RO_total | 2.5% |
| CD14mono_total | 2.5% |
| Tconv memDR_CD3 | 2.5% |
| Tconv naive_CD3 | 2.5% |
| NK_CD3neg | 2.5% |
| NKCD16_CD3neg | 2.5% |
| PD1_CD8RO | 2.5% |
| CD8 RO TIGIT_total | 2.5% |
| CD8 RO CD27_total | 2.5% |
| Tconv mem_CD3 | 2.5% |

**Total features selected by NaiveBayes_Permutation_AboveMean_t40**: 160

#### NaiveBayes_Permutation_AboveMean_t50

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Bcells CD27posIgDneg_total | 82.5% |
| CD3hi_total | 72.5% |
| Bcells memory_total | 72.5% |
| NKCD56hi_NK | 70.0% |
| CD8  RO Ki67_CD3 | 70.0% |
| CD8 RO DR_total | 67.5% |
| CD8 RO CCR5_CD3 | 67.5% |
| NK Ki67_NK | 65.0% |
| CD8 RO DR_CD3 | 65.0% |
| CD8 RO Ki67_total | 62.5% |
| CD8 RO Ki67_CD8 | 60.0% |
| Bcells memory_CD3neg | 60.0% |
| Ki67_CD8RO | 57.5% |
| Tconv memCXCR3_total | 57.5% |
| CD27negIgDneg_Bcells | 55.0% |
| Tconv memCD56_Tconv | 55.0% |
| CD8 RO CCR6_CD3 | 50.0% |
| NKCD16_NK | 50.0% |
| CD8 RO CD56_CD3 | 50.0% |
| CD16mono_myeloid | 45.0% |
| Tconv memCXCR3_Tconv | 45.0% |
| DR_CD8RO | 42.5% |
| CD14+16+mono_total | 40.0% |
| Tconv memCD56_mem | 37.5% |
| Tconv memCD56_CD3 | 37.5% |
| CD8 RO CXCR3_CD3 | 35.0% |
| CD8 RO CD56_total | 35.0% |
| NK Ki67_total | 35.0% |
| CD14+16+mono_CD3neg | 32.5% |
| CD8 RO intB7_CD3 | 32.5% |
| Bcells_total | 32.5% |
| CD8 RA naive_CD3 | 32.5% |
| CD27IgD_Bcells | 30.0% |
| Tconv memCXCR3_CD3 | 27.5% |
| Tconv memCD56_total | 27.5% |
| Tconv memCCR5_total | 25.0% |
| CD14mono_myeloid | 25.0% |
| CD8 RO CCR5_total | 22.5% |
| Bcells naive_total | 22.5% |
| NKCD56hi_total | 22.5% |
| CD14+16+mono_myeloid | 20.0% |
| Bcells CD27negIgDneg_total | 20.0% |
| Treg naive_total | 20.0% |
| NK Ki67_CD3neg | 17.5% |
| NKCD16_total | 17.5% |
| Tconv memTIGIT_total | 15.0% |
| CD8 RO CCR6_total | 15.0% |
| Tconv memCCR5_Tconv | 15.0% |
| CD8 RA_CD3 | 15.0% |
| Tconv memCD27_mem | 15.0% |
| CD8 RO intB7_total | 15.0% |
| Tconv memKi67_total | 15.0% |
| Tconv memCXCR3_mem | 15.0% |
| Bcells naive_CD3neg | 12.5% |
| NK_total | 12.5% |
| Tconv memPD1_mem | 12.5% |
| Bcells Ki67_CD3neg | 10.0% |
| NK Ki67_nonTnonB | 10.0% |
| CD3hi_CD4neg | 10.0% |
| CD8 ncytotox RO CCR4_CD3 | 10.0% |
| CD8 RO DR_CD8 | 10.0% |
| CD16mono_CD3neg | 7.5% |
| Tconv memCCR6_mem | 7.5% |
| CD8 RO CXCR3_total | 7.5% |
| Tconv memCCR6_Tconv | 7.5% |
| CD4 Tconv_total | 7.5% |
| Tconv memintB7_CD3 | 7.5% |
| Ki67_Bcells | 7.5% |
| CD3hi_CD3 | 7.5% |
| Tconv naive_total | 7.5% |
| CD8 RO PD1_CD8 | 7.5% |
| Tconv memKi67_CD3 | 7.5% |
| CD8 RO_CD3 | 5.0% |
| CD8 RO CCR5_CD8 | 5.0% |
| Tconv memTIGIT_mem | 5.0% |
| CD27_CD8RO | 5.0% |
| Treg memory_CD3 | 5.0% |
| CD8 RO TIGIT_CD3 | 5.0% |
| Tconv memCCR4_mem | 5.0% |
| CD8 ncytotox RO CCR4_CD8ntox | 5.0% |
| CXCR3_CD8RO | 5.0% |
| Treg naive_CD3 | 5.0% |
| Bcells_CD3neg | 5.0% |
| nonTnonB_CD3neg | 5.0% |
| CD8 RA_total | 5.0% |
| Treg memory_CD4 | 5.0% |
| CD4 Treg_CD4 | 5.0% |
| Tconv memCCR6_CD3 | 5.0% |
| CD8 RO CCR4_total | 5.0% |
| Tconv memKi67_Tconv | 5.0% |
| Tconv memTIGIT_Tconv | 5.0% |
| Tconv memDR_mem | 5.0% |
| NKCD16_nonTnonB | 2.5% |
| CD8 RO CD27_CD3 | 2.5% |
| CD4neg_CD3 | 2.5% |
| CD8 RO intB7_CD8 | 2.5% |
| Tconv memCCR4_Tconv | 2.5% |
| CD4 Treg _CD3 | 2.5% |
| naive_Bcells | 2.5% |
| Tconv naive_CD3 | 2.5% |
| NKCD16_CD3neg | 2.5% |
| CD8pos_CD3 | 2.5% |
| NK_CD3neg | 2.5% |
| Tconv memCCR4_CD3 | 2.5% |
| NK_nonTnonB | 2.5% |
| CD4 Tconv mem_total | 2.5% |
| Tconv memintB7_mem | 2.5% |
| nonTnonB_total | 2.5% |
| Tconv memTIGIT_CD3 | 2.5% |
| CD8 RO CXCR3_CD8 | 2.5% |
| CD4 Treg_total | 2.5% |
| Treg memory_total | 2.5% |
| TIGIT_CD8RO | 2.5% |
| Tconv memintB7_total | 2.5% |
| Tconv memKi67_mem | 2.5% |
| memory_Bcells | 2.5% |
| Tconv mem_CD3 | 2.5% |
| Tconv memCCR6_total | 2.5% |
| CD8 RA naive_total | 2.5% |
| Tconv memintB7_Tconv | 2.5% |
| CD4 Tconv_CD3 | 2.5% |
| CD56_CD8RO | 2.5% |
| CD8 RO PD1_CD3 | 2.5% |
| CCR4_CD8RO | 2.5% |
| CCR6_CD8RO | 2.5% |
| Treg naive_CD4 | 2.5% |
| Bcells Ki67_total | 2.5% |
| Tconv memCD27_total | 2.5% |
| Tconv memPD1_CD3 | 2.5% |
| Tconv memCCR4_total | 2.5% |

**Total features selected by NaiveBayes_Permutation_AboveMean_t50**: 130

#### NaiveBayes_Permutation_AboveMean_t60

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Bcells CD27posIgDneg_total | 75.0% |
| Bcells memory_total | 67.5% |
| CD3hi_total | 65.0% |
| CD8  RO Ki67_CD3 | 60.0% |
| CD8 RO DR_CD3 | 60.0% |
| NKCD56hi_NK | 60.0% |
| CD8 RO DR_total | 57.5% |
| CD8 RO Ki67_total | 52.5% |
| Bcells memory_CD3neg | 50.0% |
| CD8 RO Ki67_CD8 | 45.0% |
| NK Ki67_NK | 40.0% |
| CD8 RO CCR5_CD3 | 40.0% |
| NKCD16_NK | 37.5% |
| Tconv memCXCR3_total | 37.5% |
| Tconv memCD56_Tconv | 37.5% |
| CD27negIgDneg_Bcells | 35.0% |
| Ki67_CD8RO | 32.5% |
| CD16mono_myeloid | 32.5% |
| CD8 RO CCR6_CD3 | 30.0% |
| CD14+16+mono_total | 27.5% |
| CD8 RO CD56_CD3 | 25.0% |
| Bcells_total | 22.5% |
| CD8 RO CD56_total | 22.5% |
| Tconv memCD56_mem | 20.0% |
| CD27IgD_Bcells | 17.5% |
| NK Ki67_total | 17.5% |
| Tconv memCXCR3_Tconv | 17.5% |
| CD8 RO intB7_CD3 | 17.5% |
| CD14+16+mono_CD3neg | 15.0% |
| Tconv memCD56_CD3 | 15.0% |
| CD8 RO CCR5_total | 15.0% |
| CD8 RO CCR6_total | 12.5% |
| DR_CD8RO | 12.5% |
| CD8 RA naive_CD3 | 12.5% |
| CD14+16+mono_myeloid | 12.5% |
| Bcells naive_total | 10.0% |
| CD8 RO CXCR3_CD3 | 10.0% |
| Tconv memCXCR3_CD3 | 10.0% |
| CD8 RA_CD3 | 10.0% |
| Tconv memKi67_total | 10.0% |
| Tconv memCCR5_total | 7.5% |
| Bcells CD27negIgDneg_total | 7.5% |
| Tconv memCCR5_Tconv | 7.5% |
| Treg naive_total | 7.5% |
| CD27_CD8RO | 5.0% |
| CD8 RO DR_CD8 | 5.0% |
| Tconv memCXCR3_mem | 5.0% |
| NKCD56hi_total | 5.0% |
| Tconv memCD56_total | 5.0% |
| CD14mono_myeloid | 5.0% |
| CD16mono_CD3neg | 5.0% |
| Tconv memCCR6_Tconv | 5.0% |
| CD8 RO CXCR3_total | 5.0% |
| Bcells naive_CD3neg | 5.0% |
| Treg memory_CD3 | 2.5% |
| NKCD16_total | 2.5% |
| NK_total | 2.5% |
| Tconv memCD27_mem | 2.5% |
| NK Ki67_nonTnonB | 2.5% |
| CD8 RO intB7_CD8 | 2.5% |
| Tconv memCCR4_mem | 2.5% |
| CD8 RA_total | 2.5% |
| Tconv memKi67_Tconv | 2.5% |
| Tconv memTIGIT_mem | 2.5% |
| Tconv naive_total | 2.5% |
| Tconv memintB7_total | 2.5% |
| CXCR3_CD8RO | 2.5% |
| Bcells_CD3neg | 2.5% |
| nonTnonB_CD3neg | 2.5% |
| Tconv memKi67_mem | 2.5% |
| CD8 RO intB7_total | 2.5% |
| CD8 RO CXCR3_CD8 | 2.5% |
| Treg memory_total | 2.5% |
| Tconv memCCR6_mem | 2.5% |
| CD8 RO PD1_CD8 | 2.5% |
| CD3hi_CD4neg | 2.5% |
| NK Ki67_CD3neg | 2.5% |
| CD8 RO_CD3 | 2.5% |
| CD3hi_CD3 | 2.5% |
| Bcells Ki67_CD3neg | 2.5% |
| Tconv memCD27_total | 2.5% |

**Total features selected by NaiveBayes_Permutation_AboveMean_t60**: 81

#### NaiveBayes_Permutation_AboveMean_t70

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Bcells CD27posIgDneg_total | 65.0% |
| CD8  RO Ki67_CD3 | 50.0% |
| CD3hi_total | 47.5% |
| CD8 RO DR_CD3 | 47.5% |
| Bcells memory_total | 47.5% |
| CD8 RO DR_total | 45.0% |
| CD8 RO Ki67_total | 42.5% |
| CD8 RO Ki67_CD8 | 37.5% |
| Bcells memory_CD3neg | 37.5% |
| NKCD56hi_NK | 35.0% |
| CD8 RO CCR6_CD3 | 30.0% |
| CD8 RO CCR5_CD3 | 30.0% |
| CD27negIgDneg_Bcells | 22.5% |
| NKCD16_NK | 22.5% |
| CD8 RO CD56_CD3 | 20.0% |
| CD14+16+mono_total | 20.0% |
| Tconv memCD56_Tconv | 17.5% |
| NK Ki67_NK | 17.5% |
| CD8 RO CD56_total | 15.0% |
| CD8 RO intB7_CD3 | 15.0% |
| Bcells_total | 15.0% |
| CD14+16+mono_myeloid | 12.5% |
| CD8 RO CCR6_total | 12.5% |
| Ki67_CD8RO | 12.5% |
| NK Ki67_total | 12.5% |
| CD16mono_myeloid | 12.5% |
| Tconv memCD56_mem | 12.5% |
| Tconv memCXCR3_Tconv | 10.0% |
| Tconv memCD56_CD3 | 10.0% |
| CD8 RO CXCR3_CD3 | 10.0% |
| CD8 RO CCR5_total | 10.0% |
| Tconv memCXCR3_total | 10.0% |
| CD14+16+mono_CD3neg | 10.0% |
| CD8 RA_CD3 | 7.5% |
| CD27IgD_Bcells | 5.0% |
| Bcells naive_total | 5.0% |
| Tconv memCXCR3_CD3 | 5.0% |
| DR_CD8RO | 5.0% |
| CD8 RO DR_CD8 | 5.0% |
| Tconv memCD27_mem | 2.5% |
| Bcells CD27negIgDneg_total | 2.5% |
| CD8 RA naive_CD3 | 2.5% |
| Tconv memCCR6_Tconv | 2.5% |
| Tconv memKi67_total | 2.5% |
| Tconv memCCR5_total | 2.5% |
| Tconv memKi67_mem | 2.5% |
| Bcells naive_CD3neg | 2.5% |
| Tconv memCD56_total | 2.5% |
| CD3hi_CD4neg | 2.5% |
| CD14mono_myeloid | 2.5% |
| CD8 RO_CD3 | 2.5% |

**Total features selected by NaiveBayes_Permutation_AboveMean_t70**: 51

#### NaiveBayes_Permutation_AboveMean_t80

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Bcells CD27posIgDneg_total | 47.5% |
| CD8  RO Ki67_CD3 | 32.5% |
| CD8 RO Ki67_CD8 | 30.0% |
| CD8 RO DR_CD3 | 30.0% |
| Bcells memory_total | 27.5% |
| CD8 RO DR_total | 27.5% |
| CD8 RO Ki67_total | 25.0% |
| CD8 RO CCR5_CD3 | 25.0% |
| CD3hi_total | 20.0% |
| Bcells memory_CD3neg | 17.5% |
| CD14+16+mono_total | 15.0% |
| NKCD56hi_NK | 15.0% |
| CD8 RO CCR6_CD3 | 12.5% |
| NKCD16_NK | 12.5% |
| CD8 RO CD56_CD3 | 12.5% |
| CD16mono_myeloid | 10.0% |
| CD8 RO CD56_total | 10.0% |
| Tconv memCD56_mem | 10.0% |
| Tconv memCD56_Tconv | 10.0% |
| NK Ki67_NK | 7.5% |
| Tconv memCD56_CD3 | 7.5% |
| CD14+16+mono_CD3neg | 7.5% |
| CD14+16+mono_myeloid | 7.5% |
| NK Ki67_total | 5.0% |
| CD27negIgDneg_Bcells | 5.0% |
| Tconv memCXCR3_total | 5.0% |
| CD8 RO CXCR3_CD3 | 5.0% |
| Bcells naive_total | 5.0% |
| CD8 RO intB7_CD3 | 5.0% |
| Ki67_CD8RO | 5.0% |
| Bcells_total | 5.0% |
| CD8 RO CCR6_total | 2.5% |
| CD8 RA_CD3 | 2.5% |
| Tconv memCD27_mem | 2.5% |
| Tconv memCCR5_total | 2.5% |
| CD27IgD_Bcells | 2.5% |
| Tconv memCXCR3_Tconv | 2.5% |
| CD8 RO CCR5_total | 2.5% |
| Bcells naive_CD3neg | 2.5% |
| CD14mono_myeloid | 2.5% |
| CD8 RO DR_CD8 | 2.5% |

**Total features selected by NaiveBayes_Permutation_AboveMean_t80**: 41

#### NaiveBayes_Permutation_Top10%_t40

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Bcells memory_total | 75.0% |
| Bcells CD27posIgDneg_total | 72.5% |
| CD3hi_total | 67.5% |
| CD8 RO DR_total | 67.5% |
| CD8  RO Ki67_CD3 | 65.0% |
| CD8 RO DR_CD3 | 65.0% |
| NKCD56hi_NK | 65.0% |
| CD8 RO Ki67_total | 62.5% |
| Bcells memory_CD3neg | 57.5% |
| Tconv memCD56_Tconv | 55.0% |
| CD8 RO Ki67_CD8 | 50.0% |
| NKCD16_NK | 47.5% |
| CD8 RO CCR5_CD3 | 45.0% |
| NK Ki67_NK | 42.5% |
| Tconv memCXCR3_total | 37.5% |
| Ki67_CD8RO | 37.5% |
| CD27negIgDneg_Bcells | 37.5% |
| CD14+16+mono_total | 35.0% |
| CD8 RO CCR6_CD3 | 30.0% |
| CD8 RO CD56_CD3 | 30.0% |
| Tconv memCD56_mem | 25.0% |
| NK Ki67_total | 25.0% |
| CD8 RO CD56_total | 22.5% |
| Tconv memCXCR3_Tconv | 22.5% |
| CD16mono_myeloid | 22.5% |
| Tconv memCD56_CD3 | 22.5% |
| Bcells_total | 22.5% |
| CD8 RO intB7_CD3 | 20.0% |
| CD27IgD_Bcells | 12.5% |
| Bcells naive_total | 12.5% |
| CD8 RO CXCR3_CD3 | 12.5% |
| CD14+16+mono_CD3neg | 12.5% |
| NKCD16_total | 10.0% |
| DR_CD8RO | 10.0% |
| CD14+16+mono_myeloid | 10.0% |
| CD8 RO CCR5_total | 7.5% |
| Bcells naive_CD3neg | 7.5% |
| Tconv memKi67_total | 7.5% |
| Tconv memCXCR3_CD3 | 7.5% |
| NKCD56hi_total | 7.5% |
| CD8 RO CCR6_total | 5.0% |
| Tconv memCD56_total | 5.0% |
| Tconv memTIGIT_total | 5.0% |
| NK_total | 5.0% |
| CD14mono_myeloid | 5.0% |
| CD8 RA naive_CD3 | 5.0% |
| CD8 RA_CD3 | 5.0% |
| Tconv memCCR5_Tconv | 5.0% |
| CD8 RA_total | 5.0% |
| Bcells CD27negIgDneg_total | 5.0% |
| CD8 RO_CD3 | 2.5% |
| Tconv memCCR5_CD3 | 2.5% |
| CD8 RO CCR5_CD8 | 2.5% |
| CD8 RO intB7_total | 2.5% |
| Treg naive_total | 2.5% |
| Tconv naive_total | 2.5% |
| Tconv memCD27_mem | 2.5% |
| Tconv memintB7_CD3 | 2.5% |
| CD27_CD8RO | 2.5% |
| Tconv memCCR5_total | 2.5% |
| Bcells_CD3neg | 2.5% |
| nonTnonB_CD3neg | 2.5% |
| NK Ki67_CD3neg | 2.5% |
| CD8 RO CCR4_total | 2.5% |
| NK Ki67_nonTnonB | 2.5% |
| CD3hi_CD3 | 2.5% |
| CD8 RO DR_CD8 | 2.5% |
| Tconv memCD27_total | 2.5% |

**Total features selected by NaiveBayes_Permutation_Top10%_t40**: 68

#### NaiveBayes_Permutation_Top10%_t50

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Bcells CD27posIgDneg_total | 70.0% |
| Bcells memory_total | 57.5% |
| CD8 RO DR_total | 57.5% |
| CD8  RO Ki67_CD3 | 57.5% |
| CD8 RO DR_CD3 | 57.5% |
| CD3hi_total | 50.0% |
| NKCD56hi_NK | 47.5% |
| CD8 RO Ki67_total | 45.0% |
| Tconv memCD56_Tconv | 37.5% |
| CD8 RO Ki67_CD8 | 35.0% |
| Bcells memory_CD3neg | 30.0% |
| NKCD16_NK | 30.0% |
| NK Ki67_NK | 27.5% |
| CD8 RO CCR5_CD3 | 25.0% |
| CD14+16+mono_total | 22.5% |
| CD27negIgDneg_Bcells | 22.5% |
| Tconv memCXCR3_total | 20.0% |
| CD8 RO CD56_CD3 | 20.0% |
| Ki67_CD8RO | 17.5% |
| CD8 RO CCR6_CD3 | 17.5% |
| CD8 RO CD56_total | 15.0% |
| Tconv memCD56_mem | 15.0% |
| NK Ki67_total | 12.5% |
| Tconv memCXCR3_Tconv | 12.5% |
| Tconv memCD56_CD3 | 12.5% |
| CD8 RO CXCR3_CD3 | 12.5% |
| CD8 RO intB7_CD3 | 10.0% |
| CD16mono_myeloid | 10.0% |
| Bcells_total | 10.0% |
| CD14+16+mono_myeloid | 7.5% |
| CD14+16+mono_CD3neg | 7.5% |
| Bcells naive_CD3neg | 5.0% |
| CD8 RA naive_CD3 | 5.0% |
| Tconv memCXCR3_CD3 | 5.0% |
| Bcells naive_total | 5.0% |
| NKCD16_total | 2.5% |
| CD8 RO CCR6_total | 2.5% |
| CD8 RO_CD3 | 2.5% |
| NK_total | 2.5% |
| Tconv naive_total | 2.5% |
| Treg naive_total | 2.5% |
| Tconv memCD27_mem | 2.5% |
| CD8 RA_total | 2.5% |
| Bcells CD27negIgDneg_total | 2.5% |
| Tconv memKi67_total | 2.5% |
| CD27IgD_Bcells | 2.5% |
| Tconv memCCR5_total | 2.5% |
| CD27_CD8RO | 2.5% |
| Bcells_CD3neg | 2.5% |
| DR_CD8RO | 2.5% |
| CD8 RO CCR5_total | 2.5% |
| CD14mono_myeloid | 2.5% |
| CD8 RO DR_CD8 | 2.5% |
| Tconv memCD56_total | 2.5% |

**Total features selected by NaiveBayes_Permutation_Top10%_t50**: 54

#### NaiveBayes_Permutation_Top10%_t60

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Bcells CD27posIgDneg_total | 52.5% |
| CD8 RO DR_total | 47.5% |
| CD8 RO DR_CD3 | 45.0% |
| Bcells memory_total | 40.0% |
| CD8  RO Ki67_CD3 | 40.0% |
| NKCD56hi_NK | 32.5% |
| CD8 RO Ki67_total | 30.0% |
| CD8 RO Ki67_CD8 | 30.0% |
| CD3hi_total | 25.0% |
| Bcells memory_CD3neg | 20.0% |
| NKCD16_NK | 17.5% |
| Tconv memCD56_Tconv | 17.5% |
| CD27negIgDneg_Bcells | 15.0% |
| CD8 RO CCR5_CD3 | 15.0% |
| Ki67_CD8RO | 15.0% |
| NK Ki67_NK | 12.5% |
| CD14+16+mono_total | 12.5% |
| Tconv memCD56_CD3 | 10.0% |
| CD14+16+mono_myeloid | 7.5% |
| Tconv memCD56_mem | 7.5% |
| NK Ki67_total | 7.5% |
| CD8 RO CXCR3_CD3 | 7.5% |
| CD8 RO CD56_total | 7.5% |
| CD8 RO CCR6_CD3 | 5.0% |
| Tconv memCXCR3_Tconv | 5.0% |
| Tconv memCXCR3_total | 5.0% |
| Bcells naive_total | 5.0% |
| CD8 RO CD56_CD3 | 5.0% |
| CD14+16+mono_CD3neg | 5.0% |
| CD16mono_myeloid | 5.0% |
| CD8 RO_CD3 | 2.5% |
| NKCD16_total | 2.5% |
| NK_total | 2.5% |
| CD8 RA naive_CD3 | 2.5% |
| Bcells naive_CD3neg | 2.5% |
| Treg naive_total | 2.5% |
| CD27IgD_Bcells | 2.5% |
| CD27_CD8RO | 2.5% |
| CD8 RO CCR5_total | 2.5% |
| CD14mono_myeloid | 2.5% |
| CD8 RO DR_CD8 | 2.5% |

**Total features selected by NaiveBayes_Permutation_Top10%_t60**: 41

#### NaiveBayes_Permutation_Top10%_t70

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Bcells CD27posIgDneg_total | 41.0% |
| CD8 RO DR_CD3 | 38.5% |
| CD8  RO Ki67_CD3 | 30.8% |
| Bcells memory_total | 30.8% |
| CD8 RO Ki67_CD8 | 28.2% |
| CD8 RO DR_total | 28.2% |
| NKCD56hi_NK | 20.5% |
| CD8 RO Ki67_total | 20.5% |
| Bcells memory_CD3neg | 15.4% |
| CD8 RO CCR5_CD3 | 12.8% |
| CD14+16+mono_total | 10.3% |
| Tconv memCD56_Tconv | 10.3% |
| CD27negIgDneg_Bcells | 7.7% |
| CD3hi_total | 7.7% |
| NKCD16_NK | 7.7% |
| CD14+16+mono_myeloid | 5.1% |
| CD14+16+mono_CD3neg | 5.1% |
| Tconv memCD56_mem | 5.1% |
| CD8 RO CXCR3_CD3 | 5.1% |
| CD8 RO CCR6_CD3 | 2.6% |
| CD8 RO CD56_total | 2.6% |
| CD8 RA naive_CD3 | 2.6% |
| Tconv memCXCR3_Tconv | 2.6% |
| Bcells naive_total | 2.6% |
| Tconv memCD56_CD3 | 2.6% |
| CD8 RO CCR5_total | 2.6% |
| NK Ki67_total | 2.6% |
| CD14mono_myeloid | 2.6% |
| Ki67_CD8RO | 2.6% |
| CD8 RO DR_CD8 | 2.6% |

**Total features selected by NaiveBayes_Permutation_Top10%_t70**: 30

#### NaiveBayes_Permutation_Top10%_t80

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Bcells CD27posIgDneg_total | 37.0% |
| Bcells memory_total | 29.6% |
| CD8 RO Ki67_CD8 | 29.6% |
| CD8  RO Ki67_CD3 | 22.2% |
| CD8 RO DR_CD3 | 18.5% |
| CD8 RO DR_total | 14.8% |
| CD8 RO CCR5_CD3 | 11.1% |
| NKCD56hi_NK | 11.1% |
| CD8 RO Ki67_total | 11.1% |
| Tconv memCD56_Tconv | 7.4% |
| Tconv memCD56_mem | 7.4% |
| CD14+16+mono_total | 7.4% |
| CD14+16+mono_myeloid | 7.4% |
| Tconv memCD56_CD3 | 3.7% |
| CD8 RO CCR5_total | 3.7% |
| NK Ki67_total | 3.7% |
| CD8 RO DR_CD8 | 3.7% |

**Total features selected by NaiveBayes_Permutation_Top10%_t80**: 17

#### RFE (RandomForest)_t40

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Tconv memCCR6_CD3 | 100.0% |
| Tconv naive_total | 100.0% |
| Bcells CD27posIgDneg_total | 100.0% |
| CD4 Tconv_CD3 | 100.0% |
| NKCD16_NK | 100.0% |
| CD8 RO CD27_CD8 | 100.0% |
| Tconv memCXCR3_Tconv | 100.0% |
| Tconv memCCR6_mem | 100.0% |
| Tconv memCD27_mem | 100.0% |
| Tconv memCD56_mem | 100.0% |
| Tconv memCCR5_mem | 100.0% |
| Tconv memCCR4_mem | 100.0% |
| CD8 RO CD56_CD8 | 100.0% |
| CD8 RO CXCR3_CD8 | 100.0% |
| CD8 RO_CD8 | 100.0% |
| CD8 ncytotox RO CCR4_CD8ntox | 100.0% |
| Tconv memTIGIT_mem | 100.0% |
| CD3hi_CD4neg | 100.0% |
| Tconv memPD1_mem | 100.0% |
| Tconv memKi67_mem | 100.0% |
| Tconv memDR_mem | 100.0% |
| Tconv memCXCR3_mem | 100.0% |
| CD8 RO CCR5_CD8 | 100.0% |
| CD8 RO CCR5_CD3 | 100.0% |
| CD8 RO_CD3 | 100.0% |
| CD8 RO CD27_CD3 | 100.0% |
| CD4 Treg_CD4 | 100.0% |
| CD8 RO TIGIT_CD3 | 100.0% |
| CD8 RO PD1_CD3 | 100.0% |
| CD8 RO intB7_CD3 | 100.0% |
| Tconv mem_Tconv | 100.0% |
| Treg memory_CD4 | 100.0% |
| CD8 RO CCR6_CD3 | 100.0% |
| CD3hi_CD3 | 100.0% |
| CD4 Treg _CD3 | 100.0% |
| CD8 RA_CD3 | 100.0% |
| CD8pos_CD3 | 100.0% |
| Tconv naive_CD3 | 100.0% |
| CD27negIgDneg_Bcells | 100.0% |
| Ki67_Bcells | 100.0% |
| memory_Bcells | 100.0% |
| naive_Bcells | 100.0% |
| Tconv memPD1_Tconv | 100.0% |
| CD16mono_myeloid | 100.0% |
| CD14+16+mono_myeloid | 100.0% |
| CD27IgD_Bcells | 100.0% |
| NK Ki67_nonTnonB | 100.0% |
| CD16mono_CD3neg | 100.0% |
| myeloid_CD3neg | 100.0% |
| CD14mono_CD3neg | 100.0% |
| NK Ki67_CD3neg | 100.0% |
| Bcells Ki67_CD3neg | 100.0% |
| Bcells_CD3neg | 100.0% |
| NK_nonTnonB | 100.0% |
| nonTnonB_CD3neg | 100.0% |
| NK_CD3neg | 100.0% |
| NKCD56hi_CD3neg | 100.0% |
| TIGIT_CD8RO | 100.0% |
| DR_CD8RO | 100.0% |
| PD1_CD8RO | 100.0% |
| Ki67_CD8RO | 100.0% |
| intB7_CD8RO | 100.0% |
| CD27_CD8RO | 100.0% |
| CD56_CD8RO | 100.0% |
| CXCR3_CD8RO | 100.0% |
| CCR6_CD8RO | 100.0% |
| CCR4_CD8RO | 100.0% |
| CCR5_CD8RO | 100.0% |
| CD8 RO PD1_CD8 | 100.0% |
| CD8 RO DR_CD8 | 100.0% |
| CD14+16+mono_CD3neg | 100.0% |
| Bcells memory_CD3neg | 100.0% |
| NKCD56hi_NK | 100.0% |
| NK Ki67_NK | 100.0% |
| CD14mono_myeloid | 100.0% |
| NKCD56hi_nonTnonB | 100.0% |
| NKCD16_nonTnonB | 100.0% |
| CD8 RO CCR5_total | 97.5% |
| CD16+mono_total | 97.5% |
| Bcells naive_CD3neg | 97.5% |
| CD8 RO intB7_CD8 | 97.5% |
| NKCD16_CD3neg | 97.5% |
| Tconv memKi67_Tconv | 97.5% |
| Tconv memTIGIT_Tconv | 97.5% |
| CD8 RO CCR6_CD8 | 97.5% |
| CD8 RO Ki67_CD8 | 97.5% |
| Treg memory_CD3 | 97.5% |
| CD4neg_CD3 | 97.5% |
| CD8 RO CD56_CD3 | 97.5% |
| CD8 RO CXCR3_CD3 | 97.5% |
| Treg naive_CD4 | 97.5% |
| CD8 RO DR_CD3 | 97.5% |
| Tconv memintB7_mem | 97.5% |
| CD8 RA_CD8 | 97.5% |
| Tconv memCCR5_Tconv | 97.5% |
| Tconv naive_Tconv | 97.5% |
| Tconv memCD56_Tconv | 97.5% |
| Tconv memCD27_Tconv | 97.5% |
| Tconv memCCR6_Tconv | 97.5% |
| Tconv memCCR4_Tconv | 97.5% |
| CD8 RA naive_CD3 | 97.5% |
| CD8 RA CCR7 naive_CD8 | 97.5% |
| CD8 RO TIGIT_CD8 | 97.5% |
| Tconv memDR_Tconv | 95.0% |
| Treg naive_CD3 | 95.0% |
| Tconv memCXCR3_CD3 | 95.0% |
| CD8  RO Ki67_CD3 | 95.0% |
| Tconv memintB7_Tconv | 95.0% |
| NKCD56hi_total | 95.0% |
| CD3neg_total | 92.5% |
| Tconv memCCR5_CD3 | 92.5% |
| Bcells CD27negIgDneg_total | 92.5% |
| CD4 Tconv_total | 92.5% |
| CD8 ncytotox RO CCR4_CD3 | 90.0% |
| Bcells Ki67_total | 87.5% |
| Tconv memPD1_CD3 | 87.5% |
| Tconv memKi67_CD3 | 87.5% |
| Bcells memory_total | 87.5% |
| Tconv mem_CD3 | 87.5% |
| Tconv memPD1_total | 87.5% |
| CD3hi_total | 85.0% |
| Tconv memDR_CD3 | 85.0% |
| CD3pos_total | 82.5% |
| CD14+16+mono_total | 82.5% |
| CD8 RO CD56_total | 80.0% |
| CD14mono_total | 80.0% |
| Tconv memTIGIT_CD3 | 80.0% |
| Bcells_total | 80.0% |
| Tconv memintB7_CD3 | 77.5% |
| CD8 RO CXCR3_total | 77.5% |
| Tconv memCD56_CD3 | 77.5% |
| Tconv memCD27_CD3 | 77.5% |
| NK_total | 75.0% |
| Tconv memKi67_total | 75.0% |
| nonTnonB_total | 75.0% |
| NK Ki67_total | 70.0% |
| CD8pos_total | 67.5% |
| Treg memory_total | 67.5% |
| Tconv memCXCR3_total | 65.0% |
| CD8 RO DR_total | 65.0% |
| Tconv memCD27_total | 62.5% |
| Tconv memCCR4_total | 62.5% |
| Tconv memDR_total | 62.5% |
| Tconv memCCR4_CD3 | 62.5% |
| Bcells naive_total | 60.0% |
| myeloid_total | 60.0% |
| CD8 RO CCR6_total | 60.0% |
| CD4 Tconv mem_total | 60.0% |
| CD4 Treg_total | 60.0% |
| CD8 RO TIGIT_total | 57.5% |
| NKCD16_total | 57.5% |
| CD8 RA_total | 57.5% |
| Tconv memCCR6_total | 57.5% |
| Tconv memCD56_total | 55.0% |
| CD8 RO CD27_total | 52.5% |
| CD8 RO CCR4_total | 52.5% |
| Tconv memCCR5_total | 52.5% |
| CD8 RO PD1_total | 50.0% |
| CD8 RO Ki67_total | 50.0% |
| Tconv memTIGIT_total | 42.5% |
| CD4neg_total | 40.0% |
| CD8 RA naive_total | 40.0% |
| CD8 RO_total | 37.5% |
| CD8 RO intB7_total | 37.5% |
| Treg naive_total | 35.0% |
| Tconv memintB7_total | 32.5% |

**Total features selected by RFE (RandomForest)_t40**: 166

#### RFE (RandomForest)_t50

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Bcells CD27posIgDneg_total | 100.0% |
| CD14+16+mono_myeloid | 100.0% |
| CD16mono_myeloid | 100.0% |
| NKCD56hi_NK | 100.0% |
| NK Ki67_NK | 100.0% |
| naive_Bcells | 100.0% |
| CD8 RO PD1_CD8 | 100.0% |
| CCR4_CD8RO | 100.0% |
| CCR6_CD8RO | 100.0% |
| CCR5_CD8RO | 100.0% |
| CD27_CD8RO | 100.0% |
| CD56_CD8RO | 100.0% |
| DR_CD8RO | 100.0% |
| CXCR3_CD8RO | 100.0% |
| nonTnonB_CD3neg | 100.0% |
| TIGIT_CD8RO | 100.0% |
| intB7_CD8RO | 100.0% |
| Bcells_CD3neg | 100.0% |
| CD14mono_CD3neg | 100.0% |
| CD16mono_CD3neg | 100.0% |
| CD14+16+mono_CD3neg | 100.0% |
| NKCD56hi_CD3neg | 100.0% |
| NKCD16_NK | 100.0% |
| NKCD56hi_nonTnonB | 100.0% |
| Bcells memory_CD3neg | 100.0% |
| Bcells Ki67_CD3neg | 100.0% |
| CD8 ncytotox RO CCR4_CD8ntox | 100.0% |
| CD8 RO CD56_CD8 | 100.0% |
| CD3hi_CD4neg | 100.0% |
| Tconv memPD1_mem | 100.0% |
| Tconv memCXCR3_Tconv | 100.0% |
| Tconv memCCR4_mem | 100.0% |
| Tconv memCD27_mem | 100.0% |
| CD4 Treg_CD4 | 100.0% |
| CD8 RO CCR5_CD3 | 100.0% |
| CD8 RO CD27_CD3 | 100.0% |
| Treg memory_CD4 | 100.0% |
| CD8pos_CD3 | 100.0% |
| CD14mono_myeloid | 100.0% |
| NK_nonTnonB | 100.0% |
| CD27negIgDneg_Bcells | 100.0% |
| Ki67_Bcells | 100.0% |
| CD27IgD_Bcells | 100.0% |
| Tconv naive_total | 97.5% |
| Tconv memPD1_Tconv | 97.5% |
| NK Ki67_CD3neg | 97.5% |
| Bcells naive_CD3neg | 97.5% |
| memory_Bcells | 97.5% |
| CD8 RO Ki67_CD8 | 97.5% |
| Ki67_CD8RO | 97.5% |
| CD8 RO CXCR3_CD3 | 97.5% |
| Tconv naive_CD3 | 97.5% |
| CD8 RA_CD3 | 97.5% |
| CD8 RO_CD3 | 97.5% |
| Tconv memCCR6_mem | 97.5% |
| Tconv memCXCR3_mem | 97.5% |
| Tconv memCCR5_mem | 97.5% |
| Tconv naive_Tconv | 97.5% |
| CD8 RO CCR5_CD8 | 97.5% |
| CD8 RO CCR6_CD8 | 97.5% |
| CD8 RA CCR7 naive_CD8 | 97.5% |
| CD8 RO DR_CD8 | 97.5% |
| Tconv memDR_mem | 97.5% |
| CD8 RO CCR6_CD3 | 97.5% |
| CD8 RO TIGIT_CD3 | 97.5% |
| CD8 RO PD1_CD3 | 97.5% |
| Tconv mem_Tconv | 97.5% |
| Tconv memCCR5_Tconv | 97.5% |
| CD8 RO CXCR3_CD8 | 97.5% |
| PD1_CD8RO | 97.5% |
| Treg naive_CD4 | 95.0% |
| Tconv memCD56_Tconv | 95.0% |
| CD8 RO DR_CD3 | 95.0% |
| CD4 Tconv_CD3 | 95.0% |
| CD4neg_CD3 | 95.0% |
| NKCD16_CD3neg | 95.0% |
| CD8 RO TIGIT_CD8 | 95.0% |
| NKCD16_nonTnonB | 95.0% |
| myeloid_CD3neg | 95.0% |
| NK Ki67_nonTnonB | 95.0% |
| Tconv memCCR6_Tconv | 95.0% |
| CD8 RO CD27_CD8 | 95.0% |
| Tconv memTIGIT_mem | 95.0% |
| Tconv memKi67_mem | 95.0% |
| Tconv memintB7_mem | 95.0% |
| CD4 Treg _CD3 | 95.0% |
| CD8 RO CD56_CD3 | 95.0% |
| Tconv memCD27_Tconv | 92.5% |
| NK_CD3neg | 92.5% |
| CD8 RO intB7_CD3 | 92.5% |
| CD3hi_CD3 | 92.5% |
| Tconv memKi67_Tconv | 92.5% |
| CD8 RA naive_CD3 | 92.5% |
| Treg memory_CD3 | 92.5% |
| Tconv memCD56_mem | 92.5% |
| CD8 RO_CD8 | 92.5% |
| CD8 RA_CD8 | 92.5% |
| CD8 RO intB7_CD8 | 92.5% |
| Tconv memintB7_Tconv | 90.0% |
| Tconv memCXCR3_CD3 | 90.0% |
| NKCD56hi_total | 90.0% |
| CD8  RO Ki67_CD3 | 90.0% |
| Tconv memTIGIT_Tconv | 90.0% |
| CD8 RO CCR5_total | 87.5% |
| Treg naive_CD3 | 87.5% |
| Tconv memDR_Tconv | 87.5% |
| Tconv memCCR5_CD3 | 85.0% |
| CD4 Tconv_total | 82.5% |
| Tconv memCCR6_CD3 | 82.5% |
| CD16+mono_total | 82.5% |
| Tconv memCCR4_Tconv | 80.0% |
| Bcells CD27negIgDneg_total | 75.0% |
| Tconv memKi67_CD3 | 75.0% |
| Tconv memPD1_CD3 | 75.0% |
| CD3neg_total | 72.5% |
| CD8 ncytotox RO CCR4_CD3 | 72.5% |
| CD3hi_total | 72.5% |
| Bcells memory_total | 72.5% |
| Bcells Ki67_total | 72.5% |
| Tconv mem_CD3 | 70.0% |
| Tconv memDR_CD3 | 67.5% |
| Tconv memKi67_total | 67.5% |
| Bcells_total | 65.0% |
| CD14mono_total | 60.0% |
| Tconv memCD27_CD3 | 60.0% |
| Tconv memPD1_total | 60.0% |
| Tconv memCD56_CD3 | 60.0% |
| CD14+16+mono_total | 60.0% |
| CD8 RO CXCR3_total | 57.5% |
| Tconv memTIGIT_CD3 | 57.5% |
| Tconv memintB7_CD3 | 57.5% |
| CD8 RO DR_total | 57.5% |
| CD8 RO CD56_total | 55.0% |
| CD8pos_total | 52.5% |
| nonTnonB_total | 52.5% |
| NK Ki67_total | 52.5% |
| Tconv memCCR4_CD3 | 50.0% |
| CD4 Treg_total | 50.0% |
| Tconv memCCR4_total | 47.5% |
| NK_total | 47.5% |
| Treg memory_total | 47.5% |
| CD3pos_total | 47.5% |
| Tconv memCXCR3_total | 45.0% |
| CD8 RO Ki67_total | 42.5% |
| Tconv memDR_total | 42.5% |
| CD4 Tconv mem_total | 42.5% |
| Tconv memCD56_total | 40.0% |
| Tconv memCD27_total | 40.0% |
| CD8 RA_total | 40.0% |
| CD8 RO PD1_total | 37.5% |
| NKCD16_total | 37.5% |
| Tconv memCCR5_total | 35.0% |
| CD8 RO CCR6_total | 35.0% |
| myeloid_total | 32.5% |
| Bcells naive_total | 32.5% |
| Tconv memCCR6_total | 30.0% |
| CD8 RO CCR4_total | 30.0% |
| CD4neg_total | 27.5% |
| CD8 RA naive_total | 25.0% |
| CD8 RO TIGIT_total | 22.5% |
| CD8 RO CD27_total | 22.5% |
| Treg naive_total | 20.0% |
| Tconv memintB7_total | 20.0% |
| Tconv memTIGIT_total | 20.0% |
| CD8 RO_total | 17.5% |
| CD8 RO intB7_total | 7.5% |

**Total features selected by RFE (RandomForest)_t50**: 166

#### RFE (RandomForest)_t60

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Bcells CD27posIgDneg_total | 100.0% |
| CD27IgD_Bcells | 100.0% |
| CD27negIgDneg_Bcells | 100.0% |
| CD16mono_myeloid | 100.0% |
| CD4 Treg_CD4 | 100.0% |
| CD8pos_CD3 | 100.0% |
| CXCR3_CD8RO | 100.0% |
| intB7_CD8RO | 100.0% |
| CD16mono_CD3neg | 100.0% |
| naive_Bcells | 100.0% |
| CD8 RO CCR5_CD3 | 97.5% |
| Treg memory_CD4 | 97.5% |
| CCR4_CD8RO | 97.5% |
| CD8 RO CCR5_CD8 | 97.5% |
| Tconv memCXCR3_mem | 97.5% |
| Tconv memPD1_mem | 97.5% |
| CCR5_CD8RO | 97.5% |
| DR_CD8RO | 97.5% |
| NKCD56hi_nonTnonB | 97.5% |
| NKCD16_NK | 97.5% |
| CD8 RO Ki67_CD8 | 97.5% |
| Bcells memory_CD3neg | 97.5% |
| CD14+16+mono_myeloid | 97.5% |
| CD8 RO_CD3 | 95.0% |
| CD56_CD8RO | 95.0% |
| Tconv memCXCR3_Tconv | 95.0% |
| Tconv memKi67_mem | 95.0% |
| CD8 RA CCR7 naive_CD8 | 95.0% |
| CD8 ncytotox RO CCR4_CD8ntox | 95.0% |
| CD27_CD8RO | 95.0% |
| CD3hi_CD4neg | 95.0% |
| CD8 RO CD56_CD8 | 95.0% |
| Tconv mem_Tconv | 95.0% |
| Tconv naive_total | 95.0% |
| Tconv naive_CD3 | 95.0% |
| PD1_CD8RO | 95.0% |
| NKCD56hi_CD3neg | 95.0% |
| Bcells Ki67_CD3neg | 95.0% |
| CD14mono_myeloid | 95.0% |
| NKCD56hi_NK | 95.0% |
| Ki67_Bcells | 95.0% |
| TIGIT_CD8RO | 95.0% |
| CD8 RO PD1_CD3 | 92.5% |
| CD8 RO CD27_CD3 | 92.5% |
| CD4 Tconv_CD3 | 92.5% |
| CD8 RO CXCR3_CD3 | 92.5% |
| NK_nonTnonB | 92.5% |
| nonTnonB_CD3neg | 92.5% |
| CD14mono_CD3neg | 92.5% |
| NKCD16_CD3neg | 92.5% |
| Ki67_CD8RO | 92.5% |
| Tconv memCCR6_Tconv | 92.5% |
| Tconv memCCR5_mem | 92.5% |
| Bcells_CD3neg | 92.5% |
| memory_Bcells | 90.0% |
| myeloid_CD3neg | 90.0% |
| CD8 RO CXCR3_CD8 | 90.0% |
| CD8 RO PD1_CD8 | 90.0% |
| CCR6_CD8RO | 90.0% |
| NK Ki67_CD3neg | 90.0% |
| NKCD16_nonTnonB | 90.0% |
| CD8 RO CD27_CD8 | 90.0% |
| CD8 RO TIGIT_CD8 | 90.0% |
| Tconv memCD27_mem | 90.0% |
| Tconv memCCR6_mem | 90.0% |
| Tconv memCCR5_Tconv | 90.0% |
| CD8 RO DR_CD3 | 90.0% |
| CD8 RO CD56_CD3 | 90.0% |
| CD8 RO DR_CD8 | 90.0% |
| CD8 RO CCR6_CD8 | 90.0% |
| NK Ki67_nonTnonB | 90.0% |
| CD4 Treg _CD3 | 87.5% |
| NK Ki67_NK | 87.5% |
| CD8 RO TIGIT_CD3 | 87.5% |
| Bcells naive_CD3neg | 87.5% |
| CD8 RA_CD3 | 87.5% |
| CD14+16+mono_CD3neg | 87.5% |
| Tconv memTIGIT_mem | 85.0% |
| Tconv memintB7_Tconv | 85.0% |
| NK_CD3neg | 85.0% |
| CD8 RO intB7_CD8 | 85.0% |
| CD8 RO CCR6_CD3 | 85.0% |
| Tconv naive_Tconv | 85.0% |
| CD8 RA naive_CD3 | 85.0% |
| Treg memory_CD3 | 82.5% |
| Tconv memCD56_Tconv | 82.5% |
| Tconv memCCR4_mem | 82.5% |
| Tconv memCD56_mem | 82.5% |
| CD8 RO_CD8 | 82.5% |
| CD8 RA_CD8 | 82.5% |
| Tconv memCXCR3_CD3 | 80.0% |
| CD4neg_CD3 | 80.0% |
| Tconv memPD1_Tconv | 80.0% |
| CD8 RO intB7_CD3 | 80.0% |
| Treg naive_CD4 | 80.0% |
| Tconv memintB7_mem | 80.0% |
| Tconv memDR_mem | 77.5% |
| Tconv memCD27_Tconv | 75.0% |
| CD8  RO Ki67_CD3 | 75.0% |
| Tconv memKi67_Tconv | 75.0% |
| CD3hi_CD3 | 72.5% |
| Tconv memCCR5_CD3 | 72.5% |
| Tconv memTIGIT_Tconv | 72.5% |
| CD8 ncytotox RO CCR4_CD3 | 70.0% |
| Tconv memCCR6_CD3 | 70.0% |
| Tconv memDR_Tconv | 70.0% |
| CD4 Tconv_total | 67.5% |
| NKCD56hi_total | 67.5% |
| Treg naive_CD3 | 62.5% |
| Tconv memCCR4_Tconv | 60.0% |
| CD8 RO CCR5_total | 60.0% |
| CD16+mono_total | 60.0% |
| CD3hi_total | 57.5% |
| Bcells memory_total | 57.5% |
| CD3neg_total | 55.0% |
| Tconv memKi67_CD3 | 55.0% |
| Bcells CD27negIgDneg_total | 52.5% |
| Bcells Ki67_total | 52.5% |
| Tconv memPD1_CD3 | 50.0% |
| Tconv memKi67_total | 50.0% |
| Tconv memCD56_CD3 | 47.5% |
| Tconv mem_CD3 | 45.0% |
| Bcells_total | 42.5% |
| CD14mono_total | 42.5% |
| Tconv memPD1_total | 42.5% |
| CD8 RO CXCR3_total | 42.5% |
| CD3pos_total | 40.0% |
| Tconv memTIGIT_CD3 | 40.0% |
| Tconv memDR_CD3 | 40.0% |
| Tconv memintB7_CD3 | 35.0% |
| NK Ki67_total | 32.5% |
| Treg memory_total | 32.5% |
| CD8 RO CD56_total | 32.5% |
| myeloid_total | 30.0% |
| nonTnonB_total | 30.0% |
| CD4 Treg_total | 30.0% |
| Tconv memCD27_CD3 | 30.0% |
| CD14+16+mono_total | 27.5% |
| CD8pos_total | 27.5% |
| CD8 RO DR_total | 25.0% |
| CD8 RA_total | 22.5% |
| Tconv memCXCR3_total | 22.5% |
| Tconv memDR_total | 22.5% |
| Tconv memCCR4_total | 20.0% |
| NK_total | 20.0% |
| Tconv memCCR4_CD3 | 20.0% |
| CD8 RO CCR6_total | 17.5% |
| CD4 Tconv mem_total | 17.5% |
| Tconv memCD56_total | 15.0% |
| CD8 RO PD1_total | 15.0% |
| Bcells naive_total | 15.0% |
| Tconv memCCR6_total | 15.0% |
| CD8 RO Ki67_total | 12.5% |
| Tconv memTIGIT_total | 12.5% |
| NKCD16_total | 12.5% |
| Tconv memCD27_total | 12.5% |
| CD8 RO TIGIT_total | 10.0% |
| CD8 RA naive_total | 10.0% |
| Tconv memCCR5_total | 10.0% |
| CD8 RO CD27_total | 7.5% |
| CD8 RO intB7_total | 7.5% |
| CD8 RO_total | 7.5% |
| Tconv memintB7_total | 7.5% |
| Treg naive_total | 7.5% |
| CD4neg_total | 5.0% |
| CD8 RO CCR4_total | 5.0% |

**Total features selected by RFE (RandomForest)_t60**: 166

#### RFE (RandomForest)_t70

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD8pos_CD3 | 100.0% |
| CD16mono_myeloid | 100.0% |
| CD27IgD_Bcells | 100.0% |
| CD16mono_CD3neg | 100.0% |
| CD4 Treg_CD4 | 97.5% |
| Treg memory_CD4 | 95.0% |
| CD8 RO CCR5_CD3 | 95.0% |
| Tconv memPD1_mem | 92.5% |
| CXCR3_CD8RO | 92.5% |
| CD8 RO CCR5_CD8 | 92.5% |
| Bcells CD27posIgDneg_total | 90.0% |
| NKCD56hi_nonTnonB | 90.0% |
| CCR5_CD8RO | 90.0% |
| CD8 RO Ki67_CD8 | 90.0% |
| CD14mono_myeloid | 90.0% |
| CD14+16+mono_myeloid | 90.0% |
| CD8 RO CD27_CD3 | 87.5% |
| Tconv naive_total | 87.5% |
| NKCD56hi_NK | 87.5% |
| Tconv memCXCR3_Tconv | 87.5% |
| Tconv memCXCR3_mem | 87.5% |
| CD27negIgDneg_Bcells | 87.5% |
| Bcells memory_CD3neg | 87.5% |
| NK Ki67_NK | 85.0% |
| CD8 RO CXCR3_CD3 | 85.0% |
| CD8 RO_CD3 | 85.0% |
| Ki67_Bcells | 85.0% |
| CD14mono_CD3neg | 85.0% |
| nonTnonB_CD3neg | 85.0% |
| TIGIT_CD8RO | 85.0% |
| NKCD56hi_CD3neg | 85.0% |
| CD8 RO CD56_CD8 | 85.0% |
| CD8 ncytotox RO CCR4_CD8ntox | 85.0% |
| CD4 Tconv_CD3 | 82.5% |
| naive_Bcells | 82.5% |
| Bcells_CD3neg | 82.5% |
| CD27_CD8RO | 82.5% |
| CD56_CD8RO | 82.5% |
| intB7_CD8RO | 82.5% |
| Tconv memCD27_mem | 82.5% |
| Bcells Ki67_CD3neg | 82.5% |
| Tconv memCCR5_mem | 82.5% |
| CD8 RO CXCR3_CD8 | 82.5% |
| PD1_CD8RO | 82.5% |
| CD3hi_CD4neg | 80.0% |
| CCR4_CD8RO | 80.0% |
| CD8 RO CD27_CD8 | 80.0% |
| Tconv memCCR6_mem | 80.0% |
| memory_Bcells | 80.0% |
| Tconv memKi67_mem | 80.0% |
| CD4 Treg _CD3 | 77.5% |
| Tconv naive_CD3 | 77.5% |
| Tconv memintB7_Tconv | 77.5% |
| DR_CD8RO | 77.5% |
| NKCD16_NK | 77.5% |
| CD14+16+mono_CD3neg | 77.5% |
| NKCD16_nonTnonB | 77.5% |
| CD8 RO CD56_CD3 | 77.5% |
| CCR6_CD8RO | 77.5% |
| CD8 RO DR_CD8 | 75.0% |
| NK Ki67_nonTnonB | 75.0% |
| NKCD16_CD3neg | 75.0% |
| CD8 RO PD1_CD8 | 75.0% |
| CD8 RO DR_CD3 | 75.0% |
| CD8 RA_CD3 | 75.0% |
| NK_nonTnonB | 75.0% |
| CD8 RO TIGIT_CD3 | 75.0% |
| Tconv memCCR5_Tconv | 75.0% |
| NK_CD3neg | 72.5% |
| myeloid_CD3neg | 72.5% |
| Tconv naive_Tconv | 72.5% |
| Ki67_CD8RO | 72.5% |
| NK Ki67_CD3neg | 72.5% |
| Treg memory_CD3 | 70.0% |
| CD8 RO TIGIT_CD8 | 70.0% |
| Tconv memDR_mem | 70.0% |
| Tconv memCCR6_Tconv | 70.0% |
| CD8 RO CCR6_CD3 | 70.0% |
| Tconv mem_Tconv | 70.0% |
| CD8 RO CCR6_CD8 | 70.0% |
| Tconv memCD56_mem | 70.0% |
| CD8 RA CCR7 naive_CD8 | 70.0% |
| CD8 RO PD1_CD3 | 67.5% |
| Bcells naive_CD3neg | 65.0% |
| Tconv memTIGIT_mem | 65.0% |
| Treg naive_CD4 | 65.0% |
| Tconv memCD27_Tconv | 65.0% |
| CD8 RA_CD8 | 65.0% |
| Tconv memintB7_mem | 62.5% |
| Tconv memCD56_Tconv | 62.5% |
| CD8 RO intB7_CD8 | 62.5% |
| CD8 RO_CD8 | 60.0% |
| Tconv memCXCR3_CD3 | 60.0% |
| CD4neg_CD3 | 60.0% |
| CD3hi_CD3 | 57.5% |
| Tconv memCCR4_mem | 57.5% |
| CD8 RA naive_CD3 | 57.5% |
| CD8 RO intB7_CD3 | 55.0% |
| CD8  RO Ki67_CD3 | 52.5% |
| CD4 Tconv_total | 50.0% |
| CD8 ncytotox RO CCR4_CD3 | 50.0% |
| NKCD56hi_total | 50.0% |
| Tconv memCCR6_CD3 | 50.0% |
| Tconv memDR_Tconv | 50.0% |
| Tconv memPD1_Tconv | 50.0% |
| Tconv memKi67_Tconv | 47.5% |
| Tconv memCCR4_Tconv | 45.0% |
| CD8 RO CCR5_total | 42.5% |
| Tconv memCCR5_CD3 | 42.5% |
| Tconv memTIGIT_Tconv | 42.5% |
| CD3hi_total | 40.0% |
| CD16+mono_total | 40.0% |
| Tconv memPD1_CD3 | 35.0% |
| Bcells memory_total | 35.0% |
| CD3neg_total | 32.5% |
| Treg naive_CD3 | 32.5% |
| Tconv memPD1_total | 30.0% |
| Tconv memKi67_total | 30.0% |
| Tconv mem_CD3 | 27.5% |
| Tconv memKi67_CD3 | 27.5% |
| Bcells Ki67_total | 25.0% |
| CD8 RO CD56_total | 25.0% |
| CD3pos_total | 25.0% |
| Bcells_total | 25.0% |
| CD14mono_total | 22.5% |
| Tconv memDR_CD3 | 22.5% |
| Tconv memintB7_CD3 | 22.5% |
| Tconv memCD56_CD3 | 22.5% |
| Bcells CD27negIgDneg_total | 20.0% |
| Tconv memCD27_CD3 | 20.0% |
| CD8 RO CXCR3_total | 20.0% |
| Tconv memCCR4_CD3 | 17.5% |
| CD8pos_total | 17.5% |
| Tconv memTIGIT_CD3 | 17.5% |
| nonTnonB_total | 15.0% |
| CD8 RO DR_total | 15.0% |
| Tconv memCXCR3_total | 15.0% |
| CD14+16+mono_total | 15.0% |
| myeloid_total | 12.5% |
| NK_total | 12.5% |
| CD4 Treg_total | 12.5% |
| NK Ki67_total | 12.5% |
| Bcells naive_total | 10.0% |
| Treg memory_total | 10.0% |
| Tconv memTIGIT_total | 7.5% |
| Tconv memDR_total | 7.5% |
| CD8 RO CCR6_total | 7.5% |
| Tconv memCD56_total | 5.0% |
| CD8 RA naive_total | 5.0% |
| Tconv memCCR4_total | 5.0% |
| CD4 Tconv mem_total | 5.0% |
| CD8 RO Ki67_total | 5.0% |
| Tconv memCCR6_total | 5.0% |
| NKCD16_total | 5.0% |
| CD8 RO TIGIT_total | 5.0% |
| Tconv memCCR5_total | 2.5% |
| Treg naive_total | 2.5% |
| CD4neg_total | 2.5% |
| CD8 RO PD1_total | 2.5% |
| CD8 RO_total | 2.5% |
| CD8 RA_total | 2.5% |
| Tconv memCD27_total | 2.5% |

**Total features selected by RFE (RandomForest)_t70**: 162

#### RFE (RandomForest)_t80

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD16mono_CD3neg | 100.0% |
| CD27IgD_Bcells | 100.0% |
| CD16mono_myeloid | 95.0% |
| CD8pos_CD3 | 90.0% |
| CD4 Treg_CD4 | 87.5% |
| Treg memory_CD4 | 85.0% |
| Tconv memPD1_mem | 82.5% |
| CD8 RO CCR5_CD8 | 82.5% |
| CD8 RO CCR5_CD3 | 80.0% |
| CD14mono_myeloid | 80.0% |
| Tconv memCXCR3_Tconv | 77.5% |
| CCR5_CD8RO | 77.5% |
| Bcells CD27posIgDneg_total | 75.0% |
| Tconv naive_total | 75.0% |
| Tconv memCXCR3_mem | 70.0% |
| Bcells memory_CD3neg | 70.0% |
| nonTnonB_CD3neg | 70.0% |
| CXCR3_CD8RO | 70.0% |
| CD4 Tconv_CD3 | 70.0% |
| naive_Bcells | 70.0% |
| CD27negIgDneg_Bcells | 70.0% |
| CD8 RO CD56_CD8 | 70.0% |
| CD14+16+mono_myeloid | 67.5% |
| CCR4_CD8RO | 67.5% |
| CD8 RO CXCR3_CD8 | 67.5% |
| CD8 ncytotox RO CCR4_CD8ntox | 65.0% |
| CD3hi_CD4neg | 65.0% |
| CD8 RO CD27_CD3 | 65.0% |
| Bcells_CD3neg | 65.0% |
| Tconv naive_Tconv | 65.0% |
| PD1_CD8RO | 62.5% |
| TIGIT_CD8RO | 62.5% |
| NKCD56hi_nonTnonB | 62.5% |
| NKCD56hi_NK | 62.5% |
| CD8 RO Ki67_CD8 | 60.0% |
| intB7_CD8RO | 60.0% |
| CD8 RO TIGIT_CD3 | 60.0% |
| CD4 Treg _CD3 | 60.0% |
| CD8 RO CXCR3_CD3 | 60.0% |
| CD27_CD8RO | 60.0% |
| CD8 RO CD56_CD3 | 57.5% |
| Tconv memCCR6_mem | 57.5% |
| Tconv memCCR6_Tconv | 57.5% |
| NK_nonTnonB | 57.5% |
| NKCD56hi_CD3neg | 57.5% |
| NKCD16_nonTnonB | 57.5% |
| CD8 RO PD1_CD8 | 57.5% |
| CD14mono_CD3neg | 57.5% |
| memory_Bcells | 57.5% |
| Tconv memCCR5_mem | 57.5% |
| Treg memory_CD3 | 57.5% |
| CD8 RO_CD3 | 57.5% |
| CD8 RA_CD3 | 55.0% |
| Bcells Ki67_CD3neg | 55.0% |
| Ki67_Bcells | 55.0% |
| CD56_CD8RO | 55.0% |
| Tconv memCD27_mem | 55.0% |
| Tconv memKi67_mem | 55.0% |
| CCR6_CD8RO | 52.5% |
| DR_CD8RO | 52.5% |
| CD8 RA CCR7 naive_CD8 | 52.5% |
| CD8 RO DR_CD3 | 52.5% |
| Tconv memCCR5_Tconv | 52.5% |
| CD8 RO CD27_CD8 | 50.0% |
| Tconv naive_CD3 | 50.0% |
| myeloid_CD3neg | 50.0% |
| CD14+16+mono_CD3neg | 50.0% |
| CD8 RO TIGIT_CD8 | 47.5% |
| NK Ki67_nonTnonB | 47.5% |
| NK_CD3neg | 47.5% |
| Ki67_CD8RO | 47.5% |
| NK Ki67_NK | 47.5% |
| CD8 RO intB7_CD8 | 47.5% |
| CD8 RO CCR6_CD8 | 45.0% |
| Tconv memTIGIT_mem | 45.0% |
| NKCD16_CD3neg | 45.0% |
| CD8 RO PD1_CD3 | 45.0% |
| Tconv mem_Tconv | 42.5% |
| CD8  RO Ki67_CD3 | 42.5% |
| Tconv memDR_mem | 42.5% |
| CD8 RO CCR6_CD3 | 42.5% |
| NK Ki67_CD3neg | 42.5% |
| Tconv memintB7_Tconv | 40.0% |
| CD8 RO DR_CD8 | 40.0% |
| NKCD16_NK | 40.0% |
| Tconv memintB7_mem | 37.5% |
| Tconv memCD56_mem | 37.5% |
| CD8 RA naive_CD3 | 37.5% |
| Treg naive_CD4 | 37.5% |
| Tconv memCCR4_mem | 37.5% |
| CD3hi_CD3 | 37.5% |
| Bcells naive_CD3neg | 35.0% |
| Tconv memCD56_Tconv | 35.0% |
| Tconv memCD27_Tconv | 35.0% |
| CD4neg_CD3 | 35.0% |
| Tconv memPD1_Tconv | 32.5% |
| CD8 RO_CD8 | 32.5% |
| CD8 RA_CD8 | 32.5% |
| Tconv memCXCR3_CD3 | 32.5% |
| CD4 Tconv_total | 30.0% |
| CD8 RO CCR5_total | 27.5% |
| Tconv memCCR4_Tconv | 27.5% |
| Tconv memTIGIT_Tconv | 25.0% |
| CD8 RO intB7_CD3 | 25.0% |
| NKCD56hi_total | 22.5% |
| Tconv memCCR6_CD3 | 22.5% |
| Tconv memDR_Tconv | 22.5% |
| CD16+mono_total | 22.5% |
| Tconv memKi67_Tconv | 20.0% |
| CD8 ncytotox RO CCR4_CD3 | 20.0% |
| CD3hi_total | 20.0% |
| Tconv memPD1_CD3 | 17.5% |
| CD8 RO CXCR3_total | 17.5% |
| CD3neg_total | 15.0% |
| Bcells Ki67_total | 15.0% |
| Tconv memKi67_total | 15.0% |
| Bcells memory_total | 15.0% |
| Tconv memCCR5_CD3 | 15.0% |
| Bcells_total | 15.0% |
| Tconv memKi67_CD3 | 12.5% |
| Treg naive_CD3 | 12.5% |
| CD3pos_total | 10.0% |
| Bcells CD27negIgDneg_total | 10.0% |
| Tconv memCCR4_CD3 | 10.0% |
| Tconv memDR_CD3 | 10.0% |
| Tconv memPD1_total | 7.5% |
| Tconv memTIGIT_CD3 | 7.5% |
| Tconv memCD56_CD3 | 7.5% |
| CD8 RO CD56_total | 7.5% |
| myeloid_total | 7.5% |
| CD8 RO CCR6_total | 5.0% |
| Tconv memCXCR3_total | 5.0% |
| Tconv memDR_total | 5.0% |
| CD14mono_total | 5.0% |
| CD14+16+mono_total | 5.0% |
| CD4 Tconv mem_total | 5.0% |
| nonTnonB_total | 5.0% |
| CD8pos_total | 2.5% |
| Tconv memCCR6_total | 2.5% |
| Tconv memCCR5_total | 2.5% |
| Treg memory_total | 2.5% |
| CD4 Treg_total | 2.5% |
| CD8 RO PD1_total | 2.5% |
| NKCD16_total | 2.5% |
| CD8 RO_total | 2.5% |
| Tconv memCD56_total | 2.5% |
| Tconv mem_CD3 | 2.5% |
| NK Ki67_total | 2.5% |
| CD8 RO TIGIT_total | 2.5% |
| Tconv memintB7_CD3 | 2.5% |
| Tconv memCD27_total | 2.5% |
| Tconv memCD27_CD3 | 2.5% |
| Tconv memTIGIT_total | 2.5% |

**Total features selected by RFE (RandomForest)_t80**: 153

#### RF_Importance_t40

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD27IgD_Bcells | 100.0% |
| CD4 Treg_CD4 | 100.0% |
| CD8 RO CCR5_CD3 | 100.0% |
| Tconv naive_total | 100.0% |
| Bcells CD27posIgDneg_total | 100.0% |
| CD8pos_CD3 | 97.5% |
| Treg memory_CD4 | 97.5% |
| CD16mono_CD3neg | 97.5% |
| CD8 RO CCR5_total | 92.5% |
| CD4 Tconv_CD3 | 92.5% |
| CD16mono_myeloid | 90.0% |
| CD8 RO CCR5_CD8 | 87.5% |
| Tconv memCXCR3_Tconv | 85.0% |
| CD8 RO_CD3 | 82.5% |
| CD4 Treg _CD3 | 82.5% |
| Tconv memCCR6_Tconv | 77.5% |
| Treg memory_CD3 | 77.5% |
| CD8 RO CD27_CD3 | 75.0% |
| CD4 Tconv_total | 75.0% |
| CD8 RO CXCR3_CD3 | 75.0% |
| CCR5_CD8RO | 75.0% |
| CD14mono_myeloid | 72.5% |
| Tconv naive_CD3 | 72.5% |
| Tconv mem_Tconv | 70.0% |
| CD8 RO CD56_CD3 | 70.0% |
| CD8 RA_CD3 | 65.0% |
| CD8 RO DR_CD3 | 65.0% |
| Tconv memCXCR3_mem | 62.5% |
| Tconv memKi67_total | 62.5% |
| Tconv memCD27_mem | 62.5% |
| CCR4_CD8RO | 62.5% |
| Tconv naive_Tconv | 62.5% |
| CD8 RO CCR6_CD3 | 60.0% |
| CD8 RO TIGIT_CD3 | 60.0% |
| Tconv memCCR5_mem | 57.5% |
| CXCR3_CD8RO | 57.5% |
| Tconv memPD1_total | 57.5% |
| Tconv memCCR5_Tconv | 57.5% |
| CD4neg_CD3 | 55.0% |
| Tconv memCXCR3_CD3 | 55.0% |
| CD8 RO CXCR3_CD8 | 55.0% |
| CD16+mono_total | 55.0% |
| CD3neg_total | 52.5% |
| NKCD56hi_total | 52.5% |
| CD8 RO CXCR3_total | 50.0% |
| Tconv memCCR5_CD3 | 50.0% |
| CD8 RO PD1_CD3 | 50.0% |
| CD8 RA naive_CD3 | 50.0% |
| Bcells memory_CD3neg | 47.5% |
| Tconv memCCR4_total | 47.5% |
| CD3pos_total | 47.5% |
| nonTnonB_CD3neg | 47.5% |
| NKCD56hi_nonTnonB | 45.0% |
| nonTnonB_total | 45.0% |
| Bcells_CD3neg | 45.0% |
| CD8 RO CD56_CD8 | 45.0% |
| CD8  RO Ki67_CD3 | 45.0% |
| Treg naive_CD4 | 42.5% |
| Tconv memKi67_mem | 42.5% |
| CD8 RO intB7_CD3 | 42.5% |
| CD8 RO CD56_total | 42.5% |
| CD27negIgDneg_Bcells | 40.0% |
| Tconv memPD1_mem | 40.0% |
| NKCD56hi_CD3neg | 37.5% |
| Bcells Ki67_total | 35.0% |
| Tconv memDR_total | 35.0% |
| CD8 RO DR_total | 35.0% |
| Tconv memintB7_Tconv | 35.0% |
| CD3hi_total | 35.0% |
| Tconv memCD27_Tconv | 32.5% |
| CD3hi_CD3 | 32.5% |
| Tconv memCCR6_mem | 32.5% |
| Tconv memCCR4_mem | 32.5% |
| Ki67_CD8RO | 30.0% |
| Tconv memTIGIT_mem | 30.0% |
| CD4 Tconv mem_total | 30.0% |
| Tconv memPD1_CD3 | 27.5% |
| Tconv memCXCR3_total | 27.5% |
| Treg naive_CD3 | 27.5% |
| CD8pos_total | 27.5% |
| Tconv memCD27_total | 27.5% |
| Bcells Ki67_CD3neg | 25.0% |
| CD14+16+mono_myeloid | 25.0% |
| Tconv memCCR6_CD3 | 25.0% |
| CD8 RO Ki67_CD8 | 25.0% |
| Bcells CD27negIgDneg_total | 22.5% |
| CD3hi_CD4neg | 22.5% |
| CD4 Treg_total | 22.5% |
| Tconv memCCR4_Tconv | 22.5% |
| Bcells memory_total | 22.5% |
| Tconv memTIGIT_total | 22.5% |
| Tconv memCD56_CD3 | 20.0% |
| CD8 RA CCR7 naive_CD8 | 20.0% |
| Tconv memCD56_total | 20.0% |
| Tconv memCCR6_total | 20.0% |
| NKCD56hi_NK | 20.0% |
| Bcells_total | 20.0% |
| CD14mono_total | 20.0% |
| CD14+16+mono_total | 20.0% |
| Tconv memKi67_CD3 | 20.0% |
| CD8 RO TIGIT_total | 17.5% |
| Tconv memCD56_mem | 17.5% |
| Treg memory_total | 17.5% |
| Ki67_Bcells | 17.5% |
| CD8 RO CD27_CD8 | 17.5% |
| NK Ki67_total | 17.5% |
| Tconv memCCR5_total | 17.5% |
| NK_CD3neg | 17.5% |
| CD8 RO CCR6_total | 17.5% |
| CD8 RO DR_CD8 | 17.5% |
| Tconv memintB7_CD3 | 15.0% |
| CD27_CD8RO | 15.0% |
| CD8 ncytotox RO CCR4_CD3 | 15.0% |
| CD56_CD8RO | 15.0% |
| Tconv memDR_mem | 15.0% |
| DR_CD8RO | 15.0% |
| NK Ki67_NK | 15.0% |
| Treg naive_total | 15.0% |
| Tconv memDR_Tconv | 15.0% |
| Tconv memDR_CD3 | 12.5% |
| PD1_CD8RO | 12.5% |
| Tconv memPD1_Tconv | 12.5% |
| NK Ki67_nonTnonB | 12.5% |
| CD8 ncytotox RO CCR4_CD8ntox | 12.5% |
| TIGIT_CD8RO | 12.5% |
| CD8 RO TIGIT_CD8 | 12.5% |
| Tconv memTIGIT_Tconv | 12.5% |
| CD8 RO CD27_total | 12.5% |
| intB7_CD8RO | 12.5% |
| CD8 RO CCR4_total | 12.5% |
| CD8 RA_total | 12.5% |
| CCR6_CD8RO | 10.0% |
| CD8 RO PD1_total | 10.0% |
| Tconv mem_CD3 | 10.0% |
| Tconv memCD56_Tconv | 10.0% |
| CD8 RO Ki67_total | 10.0% |
| Tconv memCD27_CD3 | 10.0% |
| naive_Bcells | 10.0% |
| NK_total | 10.0% |
| NKCD16_CD3neg | 7.5% |
| NKCD16_NK | 7.5% |
| CD14+16+mono_CD3neg | 7.5% |
| NKCD16_total | 7.5% |
| CD14mono_CD3neg | 7.5% |
| CD8 RO_CD8 | 7.5% |
| CD4neg_total | 7.5% |
| Tconv memintB7_total | 5.0% |
| myeloid_total | 5.0% |
| CD8 RO CCR6_CD8 | 5.0% |
| Tconv memKi67_Tconv | 5.0% |
| CD8 RO intB7_CD8 | 5.0% |
| CD8 RO_total | 5.0% |
| CD8 RA naive_total | 5.0% |
| memory_Bcells | 5.0% |
| Tconv memintB7_mem | 2.5% |
| NK Ki67_CD3neg | 2.5% |
| CD8 RO PD1_CD8 | 2.5% |
| NKCD16_nonTnonB | 2.5% |
| NK_nonTnonB | 2.5% |
| CD8 RA_CD8 | 2.5% |
| myeloid_CD3neg | 2.5% |
| Bcells naive_total | 2.5% |
| Tconv memCCR4_CD3 | 2.5% |

**Total features selected by RF_Importance_t40**: 163

#### RF_Importance_t50

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD8 RO CCR5_CD3 | 97.5% |
| CD4 Treg_CD4 | 97.5% |
| CD8pos_CD3 | 95.0% |
| Treg memory_CD4 | 95.0% |
| CD27IgD_Bcells | 92.5% |
| Tconv naive_total | 92.5% |
| Bcells CD27posIgDneg_total | 92.5% |
| CD16mono_CD3neg | 87.5% |
| CD4 Tconv_CD3 | 85.0% |
| Tconv memCXCR3_Tconv | 75.0% |
| CD8 RO CCR5_CD8 | 75.0% |
| CD16mono_myeloid | 75.0% |
| CD8 RO CCR5_total | 75.0% |
| CD4 Treg _CD3 | 72.5% |
| CD8 RO_CD3 | 72.5% |
| CD8 RO CXCR3_CD3 | 70.0% |
| Treg memory_CD3 | 65.0% |
| CD4 Tconv_total | 62.5% |
| CCR5_CD8RO | 62.5% |
| CD8 RO CD56_CD3 | 60.0% |
| Tconv naive_Tconv | 55.0% |
| Tconv naive_CD3 | 55.0% |
| Tconv memCXCR3_mem | 52.5% |
| Tconv memKi67_total | 52.5% |
| CD8 RO CD27_CD3 | 50.0% |
| CD14mono_myeloid | 50.0% |
| Tconv memCCR6_Tconv | 50.0% |
| Tconv memCCR5_mem | 47.5% |
| Tconv mem_Tconv | 45.0% |
| CD8 RA_CD3 | 45.0% |
| CD8 RO DR_CD3 | 45.0% |
| CD8 RO TIGIT_CD3 | 42.5% |
| CD4neg_CD3 | 40.0% |
| CXCR3_CD8RO | 40.0% |
| Tconv memPD1_total | 40.0% |
| CD8 RO CXCR3_total | 37.5% |
| CD8 RO CCR6_CD3 | 37.5% |
| CD8 RO CXCR3_CD8 | 37.5% |
| Tconv memCD27_mem | 37.5% |
| Tconv memCXCR3_CD3 | 37.5% |
| CD16+mono_total | 37.5% |
| Tconv memCCR5_Tconv | 37.5% |
| Tconv memPD1_mem | 35.0% |
| NKCD56hi_total | 32.5% |
| CD3neg_total | 30.0% |
| CD8 RA naive_CD3 | 30.0% |
| Tconv memCCR5_CD3 | 30.0% |
| CD3pos_total | 30.0% |
| CCR4_CD8RO | 27.5% |
| Bcells memory_CD3neg | 27.5% |
| Tconv memKi67_mem | 27.5% |
| CD8  RO Ki67_CD3 | 27.5% |
| Bcells_CD3neg | 27.5% |
| NKCD56hi_nonTnonB | 27.5% |
| CD3hi_total | 25.0% |
| nonTnonB_total | 25.0% |
| Tconv memCCR4_mem | 25.0% |
| CD27negIgDneg_Bcells | 25.0% |
| CD8 RO PD1_CD3 | 25.0% |
| CD8 RO CD56_CD8 | 25.0% |
| CD8 RO intB7_CD3 | 25.0% |
| NKCD56hi_CD3neg | 22.5% |
| Tconv memintB7_Tconv | 22.5% |
| Tconv memCCR6_mem | 20.0% |
| Tconv memDR_total | 20.0% |
| Tconv memCCR4_total | 20.0% |
| CD8 RO CD56_total | 20.0% |
| Tconv memTIGIT_total | 17.5% |
| Tconv memPD1_CD3 | 17.5% |
| CD4 Tconv mem_total | 17.5% |
| nonTnonB_CD3neg | 17.5% |
| Tconv memCD27_total | 17.5% |
| Tconv memCXCR3_total | 17.5% |
| Bcells CD27negIgDneg_total | 17.5% |
| Bcells_total | 15.0% |
| CD14+16+mono_myeloid | 15.0% |
| Bcells memory_total | 15.0% |
| CD8pos_total | 15.0% |
| Tconv memCD56_mem | 15.0% |
| Treg naive_CD4 | 12.5% |
| Tconv memTIGIT_mem | 12.5% |
| CD8 RO DR_CD8 | 12.5% |
| Tconv memCD27_Tconv | 12.5% |
| CD8 RO DR_total | 12.5% |
| CD4 Treg_total | 10.0% |
| intB7_CD8RO | 10.0% |
| CD14+16+mono_total | 10.0% |
| Bcells Ki67_CD3neg | 10.0% |
| Ki67_CD8RO | 10.0% |
| Treg naive_total | 10.0% |
| Tconv memTIGIT_Tconv | 10.0% |
| CD8 RO Ki67_CD8 | 10.0% |
| Tconv memCCR6_CD3 | 10.0% |
| CD8 RA CCR7 naive_CD8 | 7.5% |
| NK_CD3neg | 7.5% |
| CD3hi_CD4neg | 7.5% |
| Tconv memKi67_CD3 | 7.5% |
| CD8 RO CCR6_total | 7.5% |
| Tconv memCCR6_total | 7.5% |
| CD3hi_CD3 | 7.5% |
| Bcells Ki67_total | 7.5% |
| CD14mono_total | 7.5% |
| Tconv memPD1_Tconv | 7.5% |
| Tconv memCCR4_Tconv | 7.5% |
| CD27_CD8RO | 7.5% |
| DR_CD8RO | 7.5% |
| Tconv memDR_mem | 7.5% |
| Tconv memDR_CD3 | 5.0% |
| Tconv memCD56_total | 5.0% |
| CD56_CD8RO | 5.0% |
| Ki67_Bcells | 5.0% |
| CD8 RO TIGIT_total | 5.0% |
| Tconv memCD56_CD3 | 5.0% |
| Tconv memCD56_Tconv | 5.0% |
| TIGIT_CD8RO | 5.0% |
| Tconv memCD27_CD3 | 5.0% |
| Tconv memCCR5_total | 5.0% |
| CD8 RO PD1_total | 5.0% |
| NKCD56hi_NK | 5.0% |
| CCR6_CD8RO | 5.0% |
| CD8 ncytotox RO CCR4_CD3 | 5.0% |
| CD8 RA_total | 5.0% |
| CD8 RO CCR6_CD8 | 2.5% |
| NK_total | 2.5% |
| NK Ki67_total | 2.5% |
| Treg memory_total | 2.5% |
| CD4neg_total | 2.5% |
| CD8 RO CD27_CD8 | 2.5% |
| CD8 RO_CD8 | 2.5% |
| CD8 RO CCR4_total | 2.5% |
| CD8 RA_CD8 | 2.5% |
| CD8 RO CD27_total | 2.5% |
| CD8 RO PD1_CD8 | 2.5% |
| NK Ki67_nonTnonB | 2.5% |
| Treg naive_CD3 | 2.5% |
| Tconv memDR_Tconv | 2.5% |
| PD1_CD8RO | 2.5% |
| CD8 RO TIGIT_CD8 | 2.5% |
| CD8 RO Ki67_total | 2.5% |
| NK Ki67_NK | 2.5% |
| naive_Bcells | 2.5% |
| myeloid_CD3neg | 2.5% |
| CD14mono_CD3neg | 2.5% |

**Total features selected by RF_Importance_t50**: 143

#### RF_Importance_t60

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD8 RO CCR5_CD3 | 90.0% |
| CD8pos_CD3 | 87.5% |
| CD4 Treg_CD4 | 87.5% |
| Bcells CD27posIgDneg_total | 87.5% |
| Treg memory_CD4 | 82.5% |
| Tconv naive_total | 80.0% |
| CD4 Tconv_CD3 | 77.5% |
| CD27IgD_Bcells | 75.0% |
| CD16mono_CD3neg | 72.5% |
| CD16mono_myeloid | 62.5% |
| CD8 RO CCR5_total | 62.5% |
| CD8 RO CXCR3_CD3 | 62.5% |
| CD4 Treg _CD3 | 60.0% |
| CD8 RO CCR5_CD8 | 52.5% |
| Tconv memCXCR3_Tconv | 52.5% |
| Treg memory_CD3 | 50.0% |
| CD4 Tconv_total | 47.5% |
| CD8 RO_CD3 | 45.0% |
| CD14mono_myeloid | 40.0% |
| Tconv naive_CD3 | 40.0% |
| Tconv memCCR6_Tconv | 37.5% |
| CD8 RO CD56_CD3 | 37.5% |
| Tconv memKi67_total | 37.5% |
| Tconv memCCR5_mem | 37.5% |
| CD8 RA_CD3 | 35.0% |
| CD8 RO TIGIT_CD3 | 35.0% |
| Tconv naive_Tconv | 35.0% |
| CD8 RO CCR6_CD3 | 30.0% |
| CD8 RO DR_CD3 | 30.0% |
| CCR5_CD8RO | 27.5% |
| CD4neg_CD3 | 27.5% |
| Tconv memCXCR3_mem | 25.0% |
| CD8 RO CD27_CD3 | 25.0% |
| Tconv memCCR5_Tconv | 22.5% |
| Tconv mem_Tconv | 22.5% |
| CXCR3_CD8RO | 22.5% |
| Tconv memPD1_total | 22.5% |
| Tconv memPD1_mem | 20.0% |
| Tconv memCXCR3_CD3 | 20.0% |
| Tconv memCCR5_CD3 | 20.0% |
| CD8 RO CXCR3_total | 17.5% |
| CD8  RO Ki67_CD3 | 17.5% |
| CD8 RO CD56_CD8 | 17.5% |
| Tconv memCD27_mem | 17.5% |
| NKCD56hi_total | 17.5% |
| CD16+mono_total | 17.5% |
| CCR4_CD8RO | 17.5% |
| Bcells memory_CD3neg | 17.5% |
| CD8 RA naive_CD3 | 15.0% |
| Tconv memCCR4_mem | 15.0% |
| CD3neg_total | 12.5% |
| CD27negIgDneg_Bcells | 12.5% |
| NKCD56hi_nonTnonB | 12.5% |
| Tconv memCCR4_total | 12.5% |
| CD3pos_total | 12.5% |
| NKCD56hi_CD3neg | 12.5% |
| CD8 RO CD56_total | 12.5% |
| Tconv memintB7_Tconv | 12.5% |
| Bcells_CD3neg | 12.5% |
| CD8 RO PD1_CD3 | 10.0% |
| nonTnonB_total | 10.0% |
| Tconv memPD1_CD3 | 10.0% |
| Tconv memCCR6_mem | 10.0% |
| CD8 RO CXCR3_CD8 | 10.0% |
| Treg naive_CD4 | 7.5% |
| Tconv memDR_total | 7.5% |
| Bcells CD27negIgDneg_total | 7.5% |
| Bcells memory_total | 7.5% |
| Bcells_total | 7.5% |
| CD8pos_total | 7.5% |
| nonTnonB_CD3neg | 7.5% |
| CD8 RO intB7_CD3 | 7.5% |
| Tconv memKi67_mem | 7.5% |
| Bcells Ki67_CD3neg | 7.5% |
| CD4 Treg_total | 7.5% |
| Tconv memTIGIT_total | 5.0% |
| Tconv memCD27_total | 5.0% |
| Tconv memTIGIT_mem | 5.0% |
| CD14+16+mono_myeloid | 5.0% |
| CD4 Tconv mem_total | 5.0% |
| Tconv memCD27_Tconv | 5.0% |
| CD14+16+mono_total | 5.0% |
| TIGIT_CD8RO | 5.0% |
| Tconv memCXCR3_total | 5.0% |
| Tconv memCCR6_CD3 | 5.0% |
| CD3hi_total | 5.0% |
| Tconv memCD56_mem | 5.0% |
| Tconv memDR_CD3 | 5.0% |
| Tconv memTIGIT_Tconv | 5.0% |
| CD8 RO CCR6_CD8 | 2.5% |
| CD3hi_CD3 | 2.5% |
| NK Ki67_total | 2.5% |
| CD8 RO DR_total | 2.5% |
| CD8 RO_CD8 | 2.5% |
| Treg memory_total | 2.5% |
| CD8 ncytotox RO CCR4_CD3 | 2.5% |
| Tconv memCCR4_Tconv | 2.5% |
| NK Ki67_nonTnonB | 2.5% |
| NK Ki67_NK | 2.5% |
| CD8 RA_total | 2.5% |
| Tconv memCD56_total | 2.5% |
| Ki67_CD8RO | 2.5% |
| CD8 RO Ki67_CD8 | 2.5% |
| intB7_CD8RO | 2.5% |
| myeloid_CD3neg | 2.5% |
| CD14mono_total | 2.5% |
| Tconv memCD56_Tconv | 2.5% |
| CD27_CD8RO | 2.5% |
| CD8 RO CCR6_total | 2.5% |
| Tconv memCD27_CD3 | 2.5% |

**Total features selected by RF_Importance_t60**: 110

#### RF_Importance_t70

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD8 RO CCR5_CD3 | 80.0% |
| CD4 Treg_CD4 | 77.5% |
| CD8pos_CD3 | 75.0% |
| Tconv naive_total | 70.0% |
| Bcells CD27posIgDneg_total | 62.5% |
| CD27IgD_Bcells | 62.5% |
| Treg memory_CD4 | 60.0% |
| CD4 Tconv_CD3 | 55.0% |
| CD16mono_CD3neg | 47.5% |
| CD8 RO CCR5_total | 45.0% |
| CD8 RO CXCR3_CD3 | 45.0% |
| CD16mono_myeloid | 45.0% |
| Treg memory_CD3 | 37.5% |
| CD8 RO_CD3 | 35.0% |
| CD8 RO CCR5_CD8 | 35.0% |
| CD4 Tconv_total | 32.5% |
| Tconv memCXCR3_Tconv | 27.5% |
| CD4 Treg _CD3 | 25.0% |
| Tconv naive_CD3 | 25.0% |
| Tconv memKi67_total | 25.0% |
| Tconv memCCR5_mem | 22.5% |
| CD8 RA_CD3 | 22.5% |
| CD4neg_CD3 | 20.0% |
| Tconv memCCR6_Tconv | 17.5% |
| CCR5_CD8RO | 17.5% |
| CD8 RO TIGIT_CD3 | 17.5% |
| CD8 RO CD56_CD3 | 17.5% |
| CD8 RO CCR6_CD3 | 15.0% |
| CD8 RO DR_CD3 | 15.0% |
| CD14mono_myeloid | 15.0% |
| CD8 RO CD27_CD3 | 15.0% |
| Tconv memPD1_mem | 12.5% |
| Tconv memCXCR3_mem | 12.5% |
| Tconv naive_Tconv | 12.5% |
| NKCD56hi_CD3neg | 10.0% |
| NKCD56hi_total | 10.0% |
| Tconv memCXCR3_CD3 | 10.0% |
| Tconv memCCR5_CD3 | 10.0% |
| CXCR3_CD8RO | 10.0% |
| Tconv memPD1_CD3 | 7.5% |
| CCR4_CD8RO | 7.5% |
| CD3neg_total | 7.5% |
| CD27negIgDneg_Bcells | 7.5% |
| Tconv mem_Tconv | 7.5% |
| CD3pos_total | 7.5% |
| Tconv memCD27_mem | 7.5% |
| CD8 RA naive_CD3 | 7.5% |
| Bcells_CD3neg | 7.5% |
| CD8  RO Ki67_CD3 | 5.0% |
| Tconv memPD1_total | 5.0% |
| NKCD56hi_nonTnonB | 5.0% |
| Tconv memTIGIT_total | 5.0% |
| CD8 RO CD56_CD8 | 5.0% |
| Tconv memCCR5_Tconv | 5.0% |
| nonTnonB_total | 5.0% |
| CD8 RO PD1_CD3 | 5.0% |
| CD16+mono_total | 5.0% |
| Tconv memCCR6_CD3 | 5.0% |
| CD8 RO CXCR3_total | 5.0% |
| Bcells memory_CD3neg | 2.5% |
| Treg memory_total | 2.5% |
| CD8 RO CXCR3_CD8 | 2.5% |
| CD8 RO DR_total | 2.5% |
| Tconv memTIGIT_mem | 2.5% |
| nonTnonB_CD3neg | 2.5% |
| Ki67_CD8RO | 2.5% |
| CD8pos_total | 2.5% |
| Tconv memTIGIT_Tconv | 2.5% |
| CD14+16+mono_total | 2.5% |
| Tconv memCCR4_mem | 2.5% |
| CD4 Treg_total | 2.5% |
| CD14+16+mono_myeloid | 2.5% |
| Tconv memCD56_total | 2.5% |
| Bcells CD27negIgDneg_total | 2.5% |
| intB7_CD8RO | 2.5% |
| Tconv memDR_total | 2.5% |
| Tconv memCD27_Tconv | 2.5% |
| TIGIT_CD8RO | 2.5% |
| Bcells_total | 2.5% |
| myeloid_CD3neg | 2.5% |
| Treg naive_CD4 | 2.5% |
| Tconv memintB7_Tconv | 2.5% |
| Tconv memCCR4_total | 2.5% |
| CD14mono_total | 2.5% |
| Bcells memory_total | 2.5% |

**Total features selected by RF_Importance_t70**: 85

#### RF_Importance_t80

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD8 RO CCR5_CD3 | 60.0% |
| Tconv naive_total | 60.0% |
| CD4 Treg_CD4 | 50.0% |
| CD8pos_CD3 | 50.0% |
| CD27IgD_Bcells | 42.5% |
| Bcells CD27posIgDneg_total | 37.5% |
| Treg memory_CD4 | 35.0% |
| CD16mono_CD3neg | 30.0% |
| CD8 RO CXCR3_CD3 | 27.5% |
| CD16mono_myeloid | 20.0% |
| Tconv memCXCR3_Tconv | 20.0% |
| CD4 Tconv_CD3 | 20.0% |
| CD8 RO CCR5_total | 15.0% |
| Treg memory_CD3 | 15.0% |
| CD8 RO CCR5_CD8 | 15.0% |
| CD14mono_myeloid | 12.5% |
| CD4 Treg _CD3 | 12.5% |
| CD8 RO_CD3 | 12.5% |
| Tconv naive_CD3 | 12.5% |
| CD4 Tconv_total | 10.0% |
| CD8 RA_CD3 | 10.0% |
| CD4neg_CD3 | 7.5% |
| CD8 RO CCR6_CD3 | 7.5% |
| CD8 RO TIGIT_CD3 | 7.5% |
| CD8 RO CD27_CD3 | 7.5% |
| CCR5_CD8RO | 7.5% |
| CD8 RO CD56_CD3 | 7.5% |
| CD3pos_total | 7.5% |
| CD8 RO DR_CD3 | 5.0% |
| Tconv memCCR6_Tconv | 5.0% |
| Tconv memPD1_total | 5.0% |
| Tconv memCXCR3_CD3 | 5.0% |
| Tconv memPD1_mem | 5.0% |
| Tconv memKi67_total | 5.0% |
| Tconv naive_Tconv | 5.0% |
| CD8 RA naive_CD3 | 5.0% |
| Tconv memCCR5_CD3 | 5.0% |
| Tconv memCXCR3_mem | 5.0% |
| CD8  RO Ki67_CD3 | 5.0% |
| CD16+mono_total | 5.0% |
| Tconv memCCR5_mem | 5.0% |
| CXCR3_CD8RO | 5.0% |
| CD8 RO PD1_CD3 | 5.0% |
| CD8 RO CD56_CD8 | 2.5% |
| Tconv memTIGIT_total | 2.5% |
| CD8 RO CXCR3_total | 2.5% |
| Bcells memory_CD3neg | 2.5% |
| Tconv mem_Tconv | 2.5% |
| CD8 RO CXCR3_CD8 | 2.5% |
| Tconv memTIGIT_Tconv | 2.5% |
| CD4 Treg_total | 2.5% |
| Tconv memCD27_mem | 2.5% |
| Tconv memCD27_Tconv | 2.5% |
| CD3neg_total | 2.5% |
| Bcells memory_total | 2.5% |

**Total features selected by RF_Importance_t80**: 55

#### RandomForest_Permutation_Top10%_t40

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD3pos_total | 100.0% |
| Tconv memCXCR3_total | 100.0% |
| Tconv memCD56_total | 100.0% |
| Tconv memCD27_total | 100.0% |
| Tconv memDR_total | 100.0% |
| Tconv memPD1_total | 100.0% |
| Tconv memKi67_total | 100.0% |
| Tconv memintB7_total | 100.0% |
| Tconv naive_total | 100.0% |
| CD4 Treg_total | 100.0% |
| Tconv memTIGIT_total | 100.0% |
| CD4 Tconv mem_total | 97.5% |
| Tconv memCCR4_total | 95.0% |
| CD4 Tconv_total | 92.5% |
| Tconv memCCR6_total | 90.0% |
| Tconv memCCR5_total | 85.0% |

**Total features selected by RandomForest_Permutation_Top10%_t40**: 16

#### RandomForest_Permutation_Top10%_t50

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Tconv memDR_total | 100.0% |
| Tconv memCXCR3_total | 100.0% |
| Tconv memCD56_total | 100.0% |
| Tconv memCD27_total | 100.0% |
| Tconv memTIGIT_total | 100.0% |
| Tconv memPD1_total | 100.0% |
| Tconv memKi67_total | 100.0% |
| Tconv memintB7_total | 100.0% |
| Tconv naive_total | 100.0% |
| CD4 Treg_total | 100.0% |
| CD3pos_total | 97.5% |
| CD4 Tconv mem_total | 92.5% |
| Tconv memCCR6_total | 82.5% |
| CD4 Tconv_total | 80.0% |
| Tconv memCCR4_total | 80.0% |
| Tconv memCCR5_total | 62.5% |

**Total features selected by RandomForest_Permutation_Top10%_t50**: 16

#### RandomForest_Permutation_Top10%_t60

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Tconv memCD27_total | 100.0% |
| Tconv memDR_total | 100.0% |
| Tconv memCXCR3_total | 100.0% |
| Tconv memCD56_total | 100.0% |
| Tconv memintB7_total | 100.0% |
| Tconv naive_total | 100.0% |
| Tconv memPD1_total | 100.0% |
| Tconv memKi67_total | 100.0% |
| CD4 Treg_total | 97.5% |
| Tconv memTIGIT_total | 97.5% |
| CD3pos_total | 92.5% |
| CD4 Tconv mem_total | 82.5% |
| Tconv memCCR6_total | 60.0% |
| CD4 Tconv_total | 55.0% |
| Tconv memCCR4_total | 55.0% |
| Tconv memCCR5_total | 42.5% |

**Total features selected by RandomForest_Permutation_Top10%_t60**: 16

#### RandomForest_Permutation_Top10%_t70

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Tconv memCD56_total | 100.0% |
| Tconv memCD27_total | 100.0% |
| Tconv memKi67_total | 100.0% |
| Tconv memDR_total | 97.5% |
| Tconv memintB7_total | 97.5% |
| Tconv memPD1_total | 97.5% |
| Tconv naive_total | 97.5% |
| Tconv memCXCR3_total | 95.0% |
| CD4 Treg_total | 95.0% |
| Tconv memTIGIT_total | 85.0% |
| CD3pos_total | 62.5% |
| CD4 Tconv mem_total | 62.5% |
| Tconv memCCR6_total | 37.5% |
| Tconv memCCR4_total | 35.0% |
| CD4 Tconv_total | 27.5% |
| Tconv memCCR5_total | 20.0% |

**Total features selected by RandomForest_Permutation_Top10%_t70**: 16

#### RandomForest_Permutation_Top10%_t80

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Tconv memKi67_total | 100.0% |
| Tconv naive_total | 97.5% |
| Tconv memCD56_total | 95.0% |
| Tconv memCD27_total | 95.0% |
| Tconv memPD1_total | 92.5% |
| Tconv memintB7_total | 92.5% |
| Tconv memCXCR3_total | 92.5% |
| Tconv memDR_total | 90.0% |
| CD4 Treg_total | 75.0% |
| Tconv memTIGIT_total | 60.0% |
| CD3pos_total | 40.0% |
| CD4 Tconv mem_total | 35.0% |
| Tconv memCCR6_total | 12.5% |
| CD4 Tconv_total | 12.5% |
| Tconv memCCR4_total | 7.5% |
| Tconv memCCR5_total | 2.5% |

**Total features selected by RandomForest_Permutation_Top10%_t80**: 16

#### Ridge_Strict_t40

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD27negIgDneg_Bcells | 100.0% |
| Tconv memKi67_Tconv | 97.5% |
| CD3hi_total | 97.5% |
| CCR4_CD8RO | 97.5% |
| Tconv memPD1_mem | 95.0% |
| CD3hi_CD4neg | 95.0% |
| DR_CD8RO | 95.0% |
| CD14mono_myeloid | 95.0% |
| NKCD56hi_nonTnonB | 95.0% |
| CD27IgD_Bcells | 95.0% |
| CD8 ncytotox RO CCR4_CD8ntox | 92.5% |
| Tconv memKi67_CD3 | 92.5% |
| CD16mono_myeloid | 92.5% |
| Tconv memCCR6_mem | 92.5% |
| Ki67_CD8RO | 90.0% |
| NKCD56hi_CD3neg | 87.5% |
| CD14+16+mono_myeloid | 87.5% |
| Tconv memCXCR3_total | 87.5% |
| Bcells CD27negIgDneg_total | 87.5% |
| Tconv memCD27_mem | 85.0% |
| Tconv memKi67_total | 85.0% |
| CD8 RO intB7_CD8 | 85.0% |
| Tconv memKi67_mem | 85.0% |
| NKCD56hi_total | 85.0% |
| Bcells CD27posIgDneg_total | 85.0% |
| CD3hi_CD3 | 85.0% |
| CD8 RO DR_CD8 | 85.0% |
| CD8pos_CD3 | 82.5% |
| CD8 RA_CD3 | 82.5% |
| intB7_CD8RO | 82.5% |
| CD8 RO CCR6_CD8 | 82.5% |
| Tconv memTIGIT_mem | 80.0% |
| memory_Bcells | 80.0% |
| Treg naive_total | 80.0% |
| CD8 RA naive_total | 80.0% |
| CD8 RO CCR6_CD3 | 77.5% |
| Tconv memCCR6_CD3 | 77.5% |
| TIGIT_CD8RO | 77.5% |
| CD8 RO CXCR3_CD8 | 77.5% |
| CD8 RA_total | 77.5% |
| Tconv memCCR4_mem | 75.0% |
| CD8 RO TIGIT_CD3 | 75.0% |
| Treg memory_total | 75.0% |
| Tconv memTIGIT_Tconv | 75.0% |
| Tconv memPD1_Tconv | 75.0% |
| CD4neg_total | 75.0% |
| Tconv memPD1_CD3 | 75.0% |
| Tconv memTIGIT_CD3 | 75.0% |
| CD16+mono_total | 75.0% |
| CCR6_CD8RO | 75.0% |
| CD14+16+mono_CD3neg | 75.0% |
| CD8 RO Ki67_CD8 | 72.5% |
| CD16mono_CD3neg | 72.5% |
| Bcells Ki67_total | 72.5% |
| CD8 RA CCR7 naive_CD8 | 72.5% |
| CCR5_CD8RO | 70.0% |
| Tconv memCCR6_total | 70.0% |
| CD8 RO CXCR3_CD3 | 70.0% |
| CD8 RO CCR6_total | 70.0% |
| Tconv memCXCR3_Tconv | 70.0% |
| CD14+16+mono_total | 70.0% |
| CD8 RO TIGIT_CD8 | 67.5% |
| CD8 RO CD56_CD8 | 67.5% |
| CD8 RA naive_CD3 | 65.0% |
| CD27_CD8RO | 65.0% |
| NK Ki67_NK | 65.0% |
| Tconv memCXCR3_CD3 | 65.0% |
| CXCR3_CD8RO | 65.0% |
| Bcells memory_total | 65.0% |
| CD8 RO CCR5_CD8 | 65.0% |
| Bcells memory_CD3neg | 62.5% |
| Ki67_Bcells | 62.5% |
| CD56_CD8RO | 62.5% |
| Tconv memDR_mem | 60.0% |
| NKCD56hi_NK | 60.0% |
| Bcells Ki67_CD3neg | 60.0% |
| NK Ki67_nonTnonB | 60.0% |
| CD8 RO CCR4_total | 60.0% |
| CD4neg_CD3 | 60.0% |
| CD8 RO PD1_total | 60.0% |
| Tconv memCCR6_Tconv | 57.5% |
| NKCD16_NK | 57.5% |
| Tconv memintB7_mem | 57.5% |
| Tconv memTIGIT_total | 57.5% |
| Tconv memintB7_total | 57.5% |
| NK Ki67_total | 57.5% |
| naive_Bcells | 57.5% |
| Tconv memDR_CD3 | 57.5% |
| Treg naive_CD3 | 57.5% |
| CD8 RO Ki67_total | 57.5% |
| CD8 RO_CD3 | 55.0% |
| CD8 RO CD27_CD3 | 55.0% |
| Tconv memCD56_total | 55.0% |
| CD8 RO PD1_CD8 | 55.0% |
| CD8 RO CCR5_CD3 | 52.5% |
| CD8 RO CCR5_total | 52.5% |
| Tconv memCCR5_total | 52.5% |
| NK Ki67_CD3neg | 50.0% |
| CD8 RO CXCR3_total | 50.0% |
| Tconv naive_total | 50.0% |
| CD4 Treg_total | 50.0% |
| Tconv memCD27_total | 50.0% |
| Treg naive_CD4 | 47.5% |
| Tconv memCCR5_mem | 45.0% |
| Tconv mem_Tconv | 45.0% |
| Bcells_total | 45.0% |
| CD8 RO PD1_CD3 | 45.0% |
| Tconv memPD1_total | 42.5% |
| Tconv memintB7_CD3 | 42.5% |
| Tconv memintB7_Tconv | 42.5% |
| CD8pos_total | 42.5% |
| PD1_CD8RO | 42.5% |
| CD8 RO intB7_total | 42.5% |
| CD4 Tconv_CD3 | 42.5% |
| Treg memory_CD4 | 40.0% |
| CD4 Tconv_total | 40.0% |
| nonTnonB_CD3neg | 40.0% |
| Tconv naive_CD3 | 40.0% |
| Tconv memDR_Tconv | 37.5% |
| Tconv memDR_total | 37.5% |
| Treg memory_CD3 | 37.5% |
| CD8 RO CD56_total | 37.5% |
| Bcells naive_CD3neg | 35.0% |
| Tconv memCXCR3_mem | 35.0% |
| CD4 Treg_CD4 | 32.5% |
| Bcells_CD3neg | 32.5% |
| CD8 RO CD27_CD8 | 32.5% |
| Bcells naive_total | 32.5% |
| CD8  RO Ki67_CD3 | 30.0% |
| CD8 RO intB7_CD3 | 30.0% |
| CD4 Treg _CD3 | 30.0% |
| CD8 ncytotox RO CCR4_CD3 | 27.5% |
| Tconv memCCR5_CD3 | 27.5% |
| Tconv memCD27_CD3 | 27.5% |
| Tconv naive_Tconv | 25.0% |
| CD3pos_total | 22.5% |
| CD8 RO CD56_CD3 | 22.5% |
| Tconv memCD56_mem | 22.5% |
| CD3neg_total | 22.5% |
| Tconv memCCR5_Tconv | 22.5% |
| NK_total | 20.0% |
| CD8 RA_CD8 | 20.0% |
| Tconv memCD56_CD3 | 20.0% |
| Tconv mem_CD3 | 20.0% |
| CD14mono_CD3neg | 20.0% |
| Tconv memCD27_Tconv | 20.0% |
| Tconv memCD56_Tconv | 17.5% |
| CD8 RO TIGIT_total | 17.5% |
| CD8 RO CD27_total | 17.5% |
| CD8 RO DR_CD3 | 17.5% |
| Tconv memCCR4_Tconv | 17.5% |
| NKCD16_total | 17.5% |
| Tconv memCCR4_total | 15.0% |
| CD8 RO DR_total | 12.5% |
| myeloid_CD3neg | 12.5% |
| CD8 RO_CD8 | 12.5% |
| Tconv memCCR4_CD3 | 12.5% |
| CD4 Tconv mem_total | 10.0% |
| myeloid_total | 5.0% |
| NKCD16_CD3neg | 5.0% |
| CD14mono_total | 5.0% |
| CD8 RO_total | 5.0% |
| NK_CD3neg | 2.5% |
| NK_nonTnonB | 2.5% |
| NKCD16_nonTnonB | 2.5% |

**Total features selected by Ridge_Strict_t40**: 165

#### Ridge_Strict_t50

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD3hi_total | 97.5% |
| CCR4_CD8RO | 97.5% |
| CD14mono_myeloid | 92.5% |
| NKCD56hi_nonTnonB | 92.5% |
| Tconv memKi67_Tconv | 92.5% |
| Tconv memPD1_mem | 90.0% |
| DR_CD8RO | 90.0% |
| CD27IgD_Bcells | 90.0% |
| CD3hi_CD4neg | 87.5% |
| CD8 ncytotox RO CCR4_CD8ntox | 87.5% |
| CD27negIgDneg_Bcells | 87.5% |
| CD16mono_myeloid | 85.0% |
| Tconv memKi67_CD3 | 85.0% |
| Ki67_CD8RO | 77.5% |
| CD8 RO DR_CD8 | 77.5% |
| Tconv memKi67_total | 77.5% |
| CD14+16+mono_myeloid | 75.0% |
| Tconv memCXCR3_total | 75.0% |
| CD8 RA_CD3 | 72.5% |
| Tconv memCCR6_mem | 72.5% |
| CD3hi_CD3 | 72.5% |
| CD8pos_CD3 | 70.0% |
| Tconv memTIGIT_CD3 | 70.0% |
| Bcells CD27posIgDneg_total | 70.0% |
| intB7_CD8RO | 70.0% |
| Treg naive_total | 70.0% |
| NKCD56hi_CD3neg | 70.0% |
| CD8 RO CXCR3_CD8 | 67.5% |
| Tconv memKi67_mem | 67.5% |
| Tconv memTIGIT_mem | 67.5% |
| TIGIT_CD8RO | 67.5% |
| NKCD56hi_total | 67.5% |
| CD8 RA_total | 65.0% |
| Bcells CD27negIgDneg_total | 65.0% |
| CD8 RA CCR7 naive_CD8 | 65.0% |
| CD14+16+mono_CD3neg | 60.0% |
| CD8 RO TIGIT_CD3 | 60.0% |
| Tconv memTIGIT_Tconv | 60.0% |
| Tconv memCCR4_mem | 60.0% |
| Treg memory_total | 60.0% |
| Tconv memCD27_mem | 60.0% |
| CD8 RO CCR6_CD8 | 60.0% |
| CD16+mono_total | 60.0% |
| CD8 RO CCR5_CD8 | 57.5% |
| CD8 RO Ki67_CD8 | 57.5% |
| CD8 RO intB7_CD8 | 55.0% |
| CD8 RO CXCR3_CD3 | 55.0% |
| CD8 RA naive_total | 55.0% |
| Tconv memCCR6_CD3 | 55.0% |
| Bcells Ki67_total | 55.0% |
| Tconv memPD1_CD3 | 55.0% |
| memory_Bcells | 55.0% |
| Ki67_Bcells | 52.5% |
| Tconv memPD1_Tconv | 52.5% |
| Bcells memory_total | 52.5% |
| CD8 RO CCR6_CD3 | 52.5% |
| Tconv memCXCR3_Tconv | 52.5% |
| CD14+16+mono_total | 52.5% |
| CD8 RO CCR6_total | 50.0% |
| CD8 RO Ki67_total | 50.0% |
| CCR6_CD8RO | 50.0% |
| CD27_CD8RO | 47.5% |
| CCR5_CD8RO | 47.5% |
| Treg naive_CD3 | 47.5% |
| CD8 RO CCR4_total | 45.0% |
| Tconv memTIGIT_total | 45.0% |
| Tconv memCXCR3_CD3 | 45.0% |
| Bcells Ki67_CD3neg | 45.0% |
| CD8 RO CXCR3_total | 45.0% |
| CD4neg_total | 45.0% |
| CD16mono_CD3neg | 45.0% |
| NK Ki67_nonTnonB | 45.0% |
| Tconv memCCR6_Tconv | 45.0% |
| Tconv memintB7_total | 42.5% |
| CXCR3_CD8RO | 42.5% |
| Bcells memory_CD3neg | 40.0% |
| CD8 RO_CD3 | 40.0% |
| CD8 RA naive_CD3 | 40.0% |
| Tconv memintB7_mem | 40.0% |
| CD56_CD8RO | 40.0% |
| Tconv naive_total | 40.0% |
| CD8 RO TIGIT_CD8 | 37.5% |
| NKCD56hi_NK | 37.5% |
| CD8 RO CD56_CD8 | 37.5% |
| CD4neg_CD3 | 37.5% |
| Tconv memCCR6_total | 37.5% |
| CD8 RO CCR5_total | 37.5% |
| CD8 RO CCR5_CD3 | 37.5% |
| Tconv memDR_mem | 35.0% |
| CD8 RO CD27_CD3 | 35.0% |
| Treg naive_CD4 | 35.0% |
| NKCD16_NK | 35.0% |
| Treg memory_CD3 | 35.0% |
| CD8 RO PD1_total | 32.5% |
| NK Ki67_NK | 32.5% |
| Tconv memCCR5_mem | 32.5% |
| Tconv memCCR5_total | 32.5% |
| Tconv memCD56_total | 32.5% |
| CD8 RO PD1_CD8 | 30.0% |
| Tconv memDR_CD3 | 30.0% |
| Bcells_total | 30.0% |
| CD4 Treg_total | 30.0% |
| Tconv memintB7_CD3 | 30.0% |
| Tconv memPD1_total | 30.0% |
| naive_Bcells | 27.5% |
| PD1_CD8RO | 27.5% |
| Treg memory_CD4 | 27.5% |
| Tconv memintB7_Tconv | 25.0% |
| Bcells_CD3neg | 25.0% |
| NK Ki67_total | 25.0% |
| CD8 RO PD1_CD3 | 25.0% |
| Tconv memDR_Tconv | 25.0% |
| CD8 RO intB7_total | 25.0% |
| CD4 Tconv_total | 25.0% |
| Tconv memCD27_total | 25.0% |
| CD4 Tconv_CD3 | 25.0% |
| Tconv memDR_total | 25.0% |
| nonTnonB_CD3neg | 22.5% |
| Tconv mem_Tconv | 22.5% |
| NK Ki67_CD3neg | 22.5% |
| CD8  RO Ki67_CD3 | 20.0% |
| CD8pos_total | 20.0% |
| Tconv memCXCR3_mem | 20.0% |
| Bcells naive_CD3neg | 20.0% |
| CD4 Treg _CD3 | 20.0% |
| CD8 RO CD27_CD8 | 20.0% |
| Bcells naive_total | 17.5% |
| CD8 ncytotox RO CCR4_CD3 | 17.5% |
| CD4 Treg_CD4 | 17.5% |
| CD8 RO CD56_total | 15.0% |
| CD8 RO CD56_CD3 | 15.0% |
| Tconv naive_CD3 | 15.0% |
| Tconv memCCR5_Tconv | 15.0% |
| Tconv mem_CD3 | 15.0% |
| Tconv memCCR5_CD3 | 12.5% |
| Tconv memCD56_mem | 12.5% |
| NK_total | 12.5% |
| Tconv memCD27_CD3 | 12.5% |
| Tconv memCCR4_Tconv | 12.5% |
| CD8 RO DR_CD3 | 12.5% |
| NKCD16_total | 12.5% |
| myeloid_CD3neg | 10.0% |
| CD8 RO CD27_total | 10.0% |
| Tconv memCD56_CD3 | 10.0% |
| CD8 RO TIGIT_total | 10.0% |
| Tconv memCD27_Tconv | 10.0% |
| CD8 RA_CD8 | 10.0% |
| Tconv memCD56_Tconv | 10.0% |
| CD8 RO intB7_CD3 | 10.0% |
| CD3neg_total | 7.5% |
| CD3pos_total | 7.5% |
| CD14mono_CD3neg | 5.0% |
| CD8 RO_CD8 | 5.0% |
| Tconv naive_Tconv | 5.0% |
| CD4 Tconv mem_total | 5.0% |
| Tconv memCCR4_total | 5.0% |
| CD8 RO DR_total | 5.0% |
| CD14mono_total | 2.5% |
| myeloid_total | 2.5% |
| Tconv memCCR4_CD3 | 2.5% |

**Total features selected by Ridge_Strict_t50**: 160

#### Ridge_Strict_t60

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CCR4_CD8RO | 95.0% |
| CD3hi_total | 90.0% |
| CD14mono_myeloid | 85.0% |
| NKCD56hi_nonTnonB | 82.5% |
| CD27negIgDneg_Bcells | 80.0% |
| Tconv memKi67_Tconv | 80.0% |
| CD8 ncytotox RO CCR4_CD8ntox | 80.0% |
| DR_CD8RO | 80.0% |
| CD3hi_CD4neg | 77.5% |
| Tconv memPD1_mem | 75.0% |
| CD16mono_myeloid | 75.0% |
| CD27IgD_Bcells | 72.5% |
| Tconv memKi67_CD3 | 70.0% |
| CD8pos_CD3 | 65.0% |
| CD8 RO CXCR3_CD8 | 65.0% |
| Tconv memKi67_total | 65.0% |
| CD8 RO DR_CD8 | 62.5% |
| CD3hi_CD3 | 62.5% |
| Bcells CD27negIgDneg_total | 62.5% |
| Tconv memCCR6_mem | 60.0% |
| Tconv memTIGIT_mem | 57.5% |
| Bcells CD27posIgDneg_total | 57.5% |
| CD8 RA_CD3 | 55.0% |
| Tconv memTIGIT_Tconv | 52.5% |
| CD14+16+mono_myeloid | 52.5% |
| CD8 RA CCR7 naive_CD8 | 52.5% |
| Ki67_CD8RO | 52.5% |
| Tconv memCXCR3_total | 52.5% |
| intB7_CD8RO | 50.0% |
| Tconv memCD27_mem | 50.0% |
| TIGIT_CD8RO | 50.0% |
| NKCD56hi_total | 50.0% |
| NKCD56hi_CD3neg | 50.0% |
| CD8 RA_total | 50.0% |
| Tconv memKi67_mem | 47.5% |
| Tconv memTIGIT_CD3 | 45.0% |
| Tconv memPD1_CD3 | 45.0% |
| CD16+mono_total | 45.0% |
| CD8 RO CCR5_CD8 | 45.0% |
| CD8 RO CCR6_CD8 | 45.0% |
| Tconv memPD1_Tconv | 45.0% |
| CD8 RO CXCR3_CD3 | 42.5% |
| Tconv memCCR4_mem | 40.0% |
| CD8 RO TIGIT_CD3 | 37.5% |
| CD14+16+mono_CD3neg | 37.5% |
| Treg naive_total | 37.5% |
| CD8 RO Ki67_total | 37.5% |
| CD8 RO intB7_CD8 | 37.5% |
| memory_Bcells | 35.0% |
| Ki67_Bcells | 35.0% |
| CD8 RO Ki67_CD8 | 35.0% |
| CCR5_CD8RO | 35.0% |
| CD14+16+mono_total | 35.0% |
| Treg naive_CD3 | 35.0% |
| Tconv memCXCR3_Tconv | 35.0% |
| CD8 RO CCR5_CD3 | 35.0% |
| Bcells Ki67_CD3neg | 35.0% |
| CD8 RA naive_total | 32.5% |
| CD8 RO CCR5_total | 32.5% |
| Treg memory_total | 32.5% |
| CD8 RO CCR6_CD3 | 32.5% |
| CCR6_CD8RO | 30.0% |
| Bcells memory_total | 30.0% |
| NK Ki67_nonTnonB | 30.0% |
| Tconv memCCR6_CD3 | 30.0% |
| Tconv memCXCR3_CD3 | 30.0% |
| Bcells Ki67_total | 30.0% |
| CD56_CD8RO | 30.0% |
| Tconv memCCR6_total | 27.5% |
| CD27_CD8RO | 27.5% |
| CD8 RO CCR6_total | 27.5% |
| Tconv memCCR6_Tconv | 27.5% |
| Tconv memTIGIT_total | 27.5% |
| CD8 RO CXCR3_total | 27.5% |
| Tconv memintB7_mem | 27.5% |
| CXCR3_CD8RO | 27.5% |
| NKCD16_NK | 25.0% |
| CD8 RO CD56_CD8 | 25.0% |
| CD8 RO_CD3 | 25.0% |
| NKCD56hi_NK | 25.0% |
| CD16mono_CD3neg | 25.0% |
| CD8 RO PD1_total | 25.0% |
| CD8 RO CCR4_total | 25.0% |
| CD8 RO CD27_CD3 | 22.5% |
| Tconv memCCR5_total | 22.5% |
| NK Ki67_NK | 22.5% |
| CD4neg_CD3 | 22.5% |
| Tconv memintB7_total | 22.5% |
| Bcells memory_CD3neg | 22.5% |
| Tconv memCD56_total | 20.0% |
| CD8 RO TIGIT_CD8 | 20.0% |
| Treg memory_CD3 | 20.0% |
| Treg naive_CD4 | 20.0% |
| CD8 RO PD1_CD3 | 20.0% |
| CD8 RA naive_CD3 | 20.0% |
| Tconv naive_total | 20.0% |
| Tconv memDR_mem | 20.0% |
| CD4neg_total | 20.0% |
| CD8 RO PD1_CD8 | 20.0% |
| Bcells_total | 20.0% |
| Tconv memDR_CD3 | 20.0% |
| CD8 RO intB7_total | 17.5% |
| CD4 Tconv_CD3 | 17.5% |
| Treg memory_CD4 | 17.5% |
| Bcells naive_CD3neg | 17.5% |
| Tconv memDR_total | 15.0% |
| Tconv memintB7_CD3 | 15.0% |
| Tconv memCD27_total | 15.0% |
| Tconv memCCR5_mem | 15.0% |
| PD1_CD8RO | 15.0% |
| CD8  RO Ki67_CD3 | 15.0% |
| Tconv memintB7_Tconv | 15.0% |
| CD8pos_total | 15.0% |
| Tconv memPD1_total | 15.0% |
| CD4 Tconv_total | 15.0% |
| NK Ki67_total | 12.5% |
| nonTnonB_CD3neg | 12.5% |
| CD4 Treg_CD4 | 12.5% |
| Tconv memCXCR3_mem | 12.5% |
| CD4 Treg_total | 10.0% |
| Tconv mem_Tconv | 10.0% |
| Tconv memDR_Tconv | 10.0% |
| Bcells_CD3neg | 10.0% |
| myeloid_CD3neg | 10.0% |
| Bcells naive_total | 10.0% |
| Tconv naive_CD3 | 10.0% |
| NK_total | 10.0% |
| Tconv memCCR5_CD3 | 10.0% |
| Tconv memCD27_CD3 | 10.0% |
| CD8 RO CD56_CD3 | 7.5% |
| Tconv memCD27_Tconv | 7.5% |
| naive_Bcells | 7.5% |
| NKCD16_total | 7.5% |
| CD8 RO TIGIT_total | 7.5% |
| CD8 ncytotox RO CCR4_CD3 | 7.5% |
| CD8 RO DR_CD3 | 7.5% |
| Tconv memCCR4_Tconv | 7.5% |
| CD8 RO CD27_CD8 | 7.5% |
| CD14mono_CD3neg | 5.0% |
| Tconv memCCR5_Tconv | 5.0% |
| CD3neg_total | 5.0% |
| CD3pos_total | 5.0% |
| CD4 Treg _CD3 | 5.0% |
| Tconv mem_CD3 | 5.0% |
| NK Ki67_CD3neg | 5.0% |
| Tconv naive_Tconv | 5.0% |
| Tconv memCCR4_total | 5.0% |
| CD8 RO CD56_total | 2.5% |
| CD8 RO_CD8 | 2.5% |
| CD8 RA_CD8 | 2.5% |
| CD8 RO CD27_total | 2.5% |
| CD8 RO intB7_CD3 | 2.5% |
| CD14mono_total | 2.5% |
| Tconv memCD56_Tconv | 2.5% |
| CD8 RO DR_total | 2.5% |
| Tconv memCCR4_CD3 | 2.5% |

**Total features selected by Ridge_Strict_t60**: 156

#### Ridge_Strict_t70

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CCR4_CD8RO | 77.5% |
| DR_CD8RO | 75.0% |
| CD3hi_total | 75.0% |
| CD8 ncytotox RO CCR4_CD8ntox | 72.5% |
| CD14mono_myeloid | 70.0% |
| NKCD56hi_nonTnonB | 70.0% |
| Tconv memKi67_Tconv | 67.5% |
| Tconv memKi67_CD3 | 65.0% |
| CD3hi_CD4neg | 65.0% |
| CD27negIgDneg_Bcells | 65.0% |
| Tconv memPD1_mem | 62.5% |
| CD16mono_myeloid | 60.0% |
| CD8 RO CXCR3_CD8 | 57.5% |
| CD27IgD_Bcells | 50.0% |
| Bcells CD27negIgDneg_total | 50.0% |
| Bcells CD27posIgDneg_total | 47.5% |
| CD8 RA_CD3 | 47.5% |
| Tconv memKi67_total | 47.5% |
| CD8 RA_total | 45.0% |
| CD8pos_CD3 | 45.0% |
| CD14+16+mono_myeloid | 45.0% |
| Tconv memCCR6_mem | 42.5% |
| TIGIT_CD8RO | 40.0% |
| CD8 RO DR_CD8 | 37.5% |
| NKCD56hi_total | 35.0% |
| CD8 RA CCR7 naive_CD8 | 35.0% |
| NKCD56hi_CD3neg | 35.0% |
| Tconv memTIGIT_mem | 35.0% |
| CD8 RO CCR5_CD8 | 35.0% |
| Tconv memPD1_Tconv | 35.0% |
| intB7_CD8RO | 35.0% |
| Tconv memCXCR3_total | 32.5% |
| CD3hi_CD3 | 32.5% |
| Tconv memCCR4_mem | 32.5% |
| CD16+mono_total | 30.0% |
| CD8 RO CCR6_CD8 | 30.0% |
| Tconv memKi67_mem | 30.0% |
| Treg naive_total | 27.5% |
| Tconv memTIGIT_Tconv | 27.5% |
| Tconv memCD27_mem | 27.5% |
| CD8 RO CCR5_CD3 | 27.5% |
| CD14+16+mono_CD3neg | 25.0% |
| CD8 RO TIGIT_CD3 | 25.0% |
| Tconv memTIGIT_CD3 | 25.0% |
| CD8 RO CXCR3_CD3 | 25.0% |
| Ki67_CD8RO | 25.0% |
| Treg naive_CD3 | 22.5% |
| memory_Bcells | 22.5% |
| Tconv memCXCR3_CD3 | 22.5% |
| Tconv memPD1_CD3 | 22.5% |
| CD8 RO CCR6_CD3 | 22.5% |
| Tconv memCCR6_CD3 | 22.5% |
| CXCR3_CD8RO | 22.5% |
| CD8 RO CCR5_total | 22.5% |
| Bcells memory_total | 22.5% |
| Tconv memCCR6_Tconv | 22.5% |
| Tconv memTIGIT_total | 20.0% |
| CD8 RO Ki67_CD8 | 20.0% |
| Tconv memCXCR3_Tconv | 20.0% |
| CD8 RO Ki67_total | 20.0% |
| CCR6_CD8RO | 20.0% |
| Tconv memintB7_mem | 20.0% |
| Ki67_Bcells | 20.0% |
| Treg memory_total | 17.5% |
| CD8 RO CCR4_total | 17.5% |
| CD8 RO intB7_CD8 | 17.5% |
| NK Ki67_nonTnonB | 17.5% |
| Bcells memory_CD3neg | 17.5% |
| CCR5_CD8RO | 17.5% |
| Tconv memCCR6_total | 17.5% |
| Bcells Ki67_CD3neg | 17.5% |
| CD8 RA naive_total | 17.5% |
| CD8 RO CCR6_total | 17.5% |
| NKCD16_NK | 17.5% |
| Bcells Ki67_total | 15.0% |
| CD8 RO CD27_CD3 | 15.0% |
| Treg memory_CD4 | 15.0% |
| CD8 RO CXCR3_total | 15.0% |
| CD8 RO_CD3 | 15.0% |
| CD56_CD8RO | 15.0% |
| CD8 RO PD1_CD8 | 12.5% |
| CD8 RO CD56_CD8 | 12.5% |
| CD8pos_total | 12.5% |
| CD8 RO PD1_total | 12.5% |
| CD16mono_CD3neg | 12.5% |
| CD14+16+mono_total | 12.5% |
| Tconv memCXCR3_mem | 12.5% |
| NKCD56hi_NK | 12.5% |
| Bcells naive_CD3neg | 10.0% |
| Tconv naive_total | 10.0% |
| CD8 RO TIGIT_CD8 | 10.0% |
| Tconv memCCR5_mem | 10.0% |
| Tconv memCD27_total | 10.0% |
| CD8 RA naive_CD3 | 10.0% |
| Bcells_total | 10.0% |
| Treg naive_CD4 | 10.0% |
| Tconv mem_Tconv | 10.0% |
| CD4neg_CD3 | 10.0% |
| CD4neg_total | 10.0% |
| PD1_CD8RO | 10.0% |
| NK Ki67_NK | 10.0% |
| CD4 Tconv_CD3 | 10.0% |
| CD4 Treg_total | 7.5% |
| Bcells_CD3neg | 7.5% |
| nonTnonB_CD3neg | 7.5% |
| Tconv memDR_Tconv | 7.5% |
| CD4 Tconv_total | 7.5% |
| naive_Bcells | 7.5% |
| CD4 Treg_CD4 | 7.5% |
| CD8 RO DR_CD3 | 7.5% |
| Tconv naive_CD3 | 7.5% |
| Tconv memDR_mem | 7.5% |
| Tconv memCCR5_total | 7.5% |
| Tconv memCCR5_Tconv | 5.0% |
| CD8  RO Ki67_CD3 | 5.0% |
| CD8 ncytotox RO CCR4_CD3 | 5.0% |
| Tconv memPD1_total | 5.0% |
| CD27_CD8RO | 5.0% |
| Tconv naive_Tconv | 5.0% |
| Tconv memDR_CD3 | 5.0% |
| Tconv memCCR4_Tconv | 5.0% |
| Tconv memCCR5_CD3 | 5.0% |
| Tconv memCCR4_total | 5.0% |
| Tconv memintB7_total | 5.0% |
| NKCD16_total | 5.0% |
| NK Ki67_total | 5.0% |
| myeloid_CD3neg | 5.0% |
| Treg memory_CD3 | 5.0% |
| Tconv memCD56_total | 5.0% |
| Tconv memCD27_Tconv | 5.0% |
| Bcells naive_total | 5.0% |
| CD4 Treg _CD3 | 5.0% |
| Tconv memintB7_Tconv | 5.0% |
| CD8 RO PD1_CD3 | 5.0% |
| NK_total | 2.5% |
| CD8 RA_CD8 | 2.5% |
| CD8 RO intB7_CD3 | 2.5% |
| Tconv mem_CD3 | 2.5% |
| CD8 RO intB7_total | 2.5% |
| Tconv memintB7_CD3 | 2.5% |
| Tconv memCCR4_CD3 | 2.5% |

**Total features selected by Ridge_Strict_t70**: 141

#### Ridge_Strict_t80

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CCR4_CD8RO | 72.5% |
| DR_CD8RO | 65.0% |
| Tconv memKi67_Tconv | 62.5% |
| CD14mono_myeloid | 57.5% |
| CD8 ncytotox RO CCR4_CD8ntox | 57.5% |
| CD3hi_total | 57.5% |
| CD3hi_CD4neg | 52.5% |
| Tconv memPD1_mem | 52.5% |
| Tconv memKi67_CD3 | 50.0% |
| NKCD56hi_nonTnonB | 45.0% |
| CD8 RO CXCR3_CD8 | 45.0% |
| CD27IgD_Bcells | 42.5% |
| CD27negIgDneg_Bcells | 40.0% |
| CD16mono_myeloid | 37.5% |
| Tconv memKi67_total | 35.0% |
| CD8pos_CD3 | 32.5% |
| CD14+16+mono_myeloid | 30.0% |
| NKCD56hi_total | 30.0% |
| Tconv memCCR6_mem | 25.0% |
| CD8 RA_total | 25.0% |
| Tconv memKi67_mem | 25.0% |
| CD8 RA_CD3 | 25.0% |
| CD8 RO DR_CD8 | 25.0% |
| CD8 RO TIGIT_CD3 | 22.5% |
| CD8 RO CCR5_CD3 | 22.5% |
| NKCD56hi_CD3neg | 22.5% |
| Bcells CD27posIgDneg_total | 22.5% |
| Tconv memCXCR3_total | 20.0% |
| Tconv memPD1_Tconv | 20.0% |
| CD3hi_CD3 | 20.0% |
| Tconv memCCR6_CD3 | 20.0% |
| CD8 RA CCR7 naive_CD8 | 20.0% |
| Tconv memCD27_mem | 20.0% |
| CD8 RO CXCR3_CD3 | 20.0% |
| CD8 RO CCR6_CD8 | 17.5% |
| Treg naive_total | 17.5% |
| Bcells CD27negIgDneg_total | 17.5% |
| Ki67_CD8RO | 17.5% |
| Tconv memTIGIT_mem | 17.5% |
| TIGIT_CD8RO | 17.5% |
| CD8 RO CCR5_total | 15.0% |
| CD8 RO CCR5_CD8 | 15.0% |
| CD8 RO intB7_CD8 | 15.0% |
| Ki67_Bcells | 15.0% |
| CXCR3_CD8RO | 15.0% |
| memory_Bcells | 15.0% |
| CD14+16+mono_CD3neg | 15.0% |
| Tconv memTIGIT_Tconv | 15.0% |
| Tconv memPD1_CD3 | 15.0% |
| Tconv memTIGIT_CD3 | 15.0% |
| Tconv memCCR6_Tconv | 15.0% |
| CCR5_CD8RO | 12.5% |
| CD8 RO CD27_CD3 | 12.5% |
| NK Ki67_nonTnonB | 12.5% |
| CD8 RO Ki67_total | 12.5% |
| Tconv memCCR6_total | 12.5% |
| CD8 RO PD1_total | 12.5% |
| CD8 RO Ki67_CD8 | 10.0% |
| NKCD16_NK | 10.0% |
| Tconv memCXCR3_CD3 | 10.0% |
| CD8pos_total | 10.0% |
| Tconv memCXCR3_Tconv | 10.0% |
| CD8 RO_CD3 | 10.0% |
| Tconv memCXCR3_mem | 10.0% |
| CCR6_CD8RO | 10.0% |
| NKCD56hi_NK | 10.0% |
| CD56_CD8RO | 10.0% |
| Tconv memCCR4_mem | 10.0% |
| CD16+mono_total | 10.0% |
| intB7_CD8RO | 10.0% |
| Bcells Ki67_CD3neg | 7.5% |
| CD8 RO CCR4_total | 7.5% |
| CD8 RO PD1_CD8 | 7.5% |
| Bcells_total | 7.5% |
| Treg memory_total | 7.5% |
| Bcells memory_total | 7.5% |
| CD8 RO CXCR3_total | 7.5% |
| CD4neg_total | 7.5% |
| naive_Bcells | 5.0% |
| Bcells_CD3neg | 5.0% |
| CD8 RO CD56_CD8 | 5.0% |
| nonTnonB_CD3neg | 5.0% |
| CD8 RA naive_CD3 | 5.0% |
| CD8 RO PD1_CD3 | 5.0% |
| Tconv mem_Tconv | 5.0% |
| Treg naive_CD3 | 5.0% |
| Tconv memTIGIT_total | 5.0% |
| Tconv memCD27_total | 5.0% |
| PD1_CD8RO | 5.0% |
| Bcells memory_CD3neg | 5.0% |
| Tconv naive_Tconv | 5.0% |
| NK Ki67_NK | 5.0% |
| CD8 RO DR_CD3 | 5.0% |
| Tconv memDR_CD3 | 5.0% |
| CD8 RO CCR6_CD3 | 5.0% |
| CD27_CD8RO | 5.0% |
| CD4 Tconv_CD3 | 5.0% |
| Tconv naive_CD3 | 5.0% |
| Treg memory_CD4 | 5.0% |
| Treg naive_CD4 | 5.0% |
| Tconv memintB7_mem | 5.0% |
| Tconv memCCR5_total | 5.0% |
| CD4neg_CD3 | 5.0% |
| NKCD16_total | 5.0% |
| CD4 Treg_total | 2.5% |
| CD8 RO TIGIT_CD8 | 2.5% |
| CD4 Tconv_total | 2.5% |
| Tconv memDR_mem | 2.5% |
| CD8 RA_CD8 | 2.5% |
| Tconv naive_total | 2.5% |
| Bcells naive_CD3neg | 2.5% |
| NK_total | 2.5% |
| Tconv memCCR4_total | 2.5% |
| CD14+16+mono_total | 2.5% |
| Tconv memPD1_total | 2.5% |
| Tconv mem_CD3 | 2.5% |
| Tconv memCD27_Tconv | 2.5% |
| Tconv memintB7_total | 2.5% |
| CD16mono_CD3neg | 2.5% |
| CD8 RO CCR6_total | 2.5% |
| Bcells naive_total | 2.5% |
| Tconv memintB7_CD3 | 2.5% |
| Tconv memintB7_Tconv | 2.5% |
| CD8 RA naive_total | 2.5% |
| Bcells Ki67_total | 2.5% |
| Tconv memCCR5_CD3 | 2.5% |
| Tconv memCCR5_Tconv | 2.5% |
| Tconv memCCR5_mem | 2.5% |
| Tconv memCCR4_CD3 | 2.5% |
| Tconv memCCR4_Tconv | 2.5% |

**Total features selected by Ridge_Strict_t80**: 130

#### SVM_RBF_Permutation_AboveMean_t40

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CCR4_CD8RO | 80.0% |
| CD8 ncytotox RO CCR4_CD8ntox | 52.0% |
| CD3hi_total | 48.0% |
| Tconv memPD1_mem | 48.0% |
| CD3hi_CD4neg | 48.0% |
| TIGIT_CD8RO | 44.0% |
| CD27IgD_Bcells | 44.0% |
| CD8 RO DR_CD8 | 40.0% |
| CD8 RO intB7_CD3 | 40.0% |
| Tconv memCCR4_mem | 40.0% |
| DR_CD8RO | 40.0% |
| Bcells Ki67_total | 36.0% |
| Tconv memKi67_total | 36.0% |
| CD16mono_myeloid | 36.0% |
| Tconv memCCR6_mem | 36.0% |
| Treg memory_total | 36.0% |
| Tconv memCXCR3_Tconv | 36.0% |
| Tconv memKi67_CD3 | 36.0% |
| CD8 RO intB7_total | 36.0% |
| CD3pos_total | 32.0% |
| Tconv mem_CD3 | 32.0% |
| CD8 RO Ki67_CD8 | 32.0% |
| CD8 RO CXCR3_CD8 | 32.0% |
| NKCD16_CD3neg | 32.0% |
| CD3neg_total | 32.0% |
| CD8 RO CD56_CD8 | 32.0% |
| Tconv memCCR6_CD3 | 32.0% |
| Tconv memPD1_Tconv | 32.0% |
| Tconv memPD1_CD3 | 32.0% |
| Treg naive_CD3 | 32.0% |
| Tconv memCXCR3_mem | 32.0% |
| Tconv memCCR5_total | 32.0% |
| Treg naive_total | 32.0% |
| CD14+16+mono_CD3neg | 28.0% |
| intB7_CD8RO | 28.0% |
| Tconv memCD56_total | 28.0% |
| Tconv memTIGIT_mem | 28.0% |
| CD14+16+mono_myeloid | 28.0% |
| Tconv memCCR5_CD3 | 28.0% |
| NKCD16_nonTnonB | 28.0% |
| CD4 Treg_total | 28.0% |
| CD3hi_CD3 | 28.0% |
| nonTnonB_total | 28.0% |
| NK_CD3neg | 28.0% |
| CD8 RA CCR7 naive_CD8 | 28.0% |
| Bcells CD27posIgDneg_total | 28.0% |
| Tconv memPD1_total | 28.0% |
| CD8 RO intB7_CD8 | 28.0% |
| NK_nonTnonB | 28.0% |
| Tconv memKi67_Tconv | 28.0% |
| CD8 RO DR_CD3 | 28.0% |
| Tconv memDR_total | 28.0% |
| memory_Bcells | 28.0% |
| Bcells CD27negIgDneg_total | 28.0% |
| CD8 RO CCR6_CD8 | 28.0% |
| Tconv memCD27_CD3 | 24.0% |
| CXCR3_CD8RO | 24.0% |
| Tconv memKi67_mem | 24.0% |
| CD8 RO CCR4_total | 24.0% |
| CD27_CD8RO | 24.0% |
| CD8 ncytotox RO CCR4_CD3 | 24.0% |
| CCR6_CD8RO | 24.0% |
| NKCD16_total | 24.0% |
| Tconv memTIGIT_total | 24.0% |
| NK_total | 24.0% |
| Bcells memory_CD3neg | 24.0% |
| Tconv memCCR4_CD3 | 24.0% |
| Bcells memory_total | 24.0% |
| CD8 RA_CD3 | 24.0% |
| CD8 RO CD27_CD3 | 24.0% |
| CD8 RA naive_CD3 | 24.0% |
| Tconv memCXCR3_CD3 | 24.0% |
| NK Ki67_CD3neg | 24.0% |
| CD14+16+mono_total | 24.0% |
| CD8 RO TIGIT_CD8 | 24.0% |
| NK Ki67_total | 24.0% |
| Tconv memCCR5_Tconv | 24.0% |
| NKCD16_NK | 24.0% |
| CD8 RO PD1_total | 24.0% |
| Bcells_total | 24.0% |
| Tconv memCXCR3_total | 24.0% |
| Tconv memintB7_mem | 24.0% |
| Tconv memTIGIT_CD3 | 20.0% |
| CD16mono_CD3neg | 20.0% |
| CD4 Tconv mem_total | 20.0% |
| Tconv memCD56_Tconv | 20.0% |
| Tconv memCD56_mem | 20.0% |
| Tconv memCCR4_total | 20.0% |
| Tconv memCD56_CD3 | 20.0% |
| Tconv memCCR5_mem | 20.0% |
| CD8 RO CCR5_CD8 | 20.0% |
| CD14mono_myeloid | 20.0% |
| CD8 RO CD56_CD3 | 20.0% |
| CD8 RO DR_total | 20.0% |
| Bcells naive_total | 20.0% |
| CD8 RO CXCR3_CD3 | 20.0% |
| Bcells Ki67_CD3neg | 20.0% |
| Tconv memCD27_Tconv | 20.0% |
| CD56_CD8RO | 20.0% |
| CD8 RO PD1_CD3 | 20.0% |
| Treg naive_CD4 | 20.0% |
| CD8 RO CCR5_CD3 | 20.0% |
| CD8  RO Ki67_CD3 | 20.0% |
| Tconv memCCR6_total | 20.0% |
| NK Ki67_nonTnonB | 20.0% |
| CD8 RO CD56_total | 20.0% |
| CD8 RO CCR6_CD3 | 20.0% |
| NKCD56hi_CD3neg | 20.0% |
| Ki67_CD8RO | 20.0% |
| CD8 RA_total | 20.0% |
| CD4 Tconv_total | 20.0% |
| Tconv memCD27_total | 16.0% |
| CD14mono_CD3neg | 16.0% |
| CD4neg_total | 16.0% |
| Tconv memDR_CD3 | 16.0% |
| CD27negIgDneg_Bcells | 16.0% |
| naive_Bcells | 16.0% |
| CD16+mono_total | 16.0% |
| myeloid_total | 16.0% |
| CD8 RO CD27_total | 16.0% |
| CD8 RO_total | 16.0% |
| Tconv memTIGIT_Tconv | 16.0% |
| PD1_CD8RO | 16.0% |
| NK Ki67_NK | 16.0% |
| CD8 RO CD27_CD8 | 16.0% |
| nonTnonB_CD3neg | 16.0% |
| CD8 RO_CD3 | 16.0% |
| CD8 RO TIGIT_CD3 | 16.0% |
| CD8 RO CCR5_total | 16.0% |
| Tconv naive_total | 16.0% |
| Bcells_CD3neg | 16.0% |
| Tconv memDR_mem | 16.0% |
| CD8 RO Ki67_total | 16.0% |
| Tconv memCCR6_Tconv | 16.0% |
| CD8 RO PD1_CD8 | 12.0% |
| myeloid_CD3neg | 12.0% |
| NKCD56hi_NK | 12.0% |
| CD14mono_total | 12.0% |
| CD8 RO TIGIT_total | 12.0% |
| Bcells naive_CD3neg | 12.0% |
| Tconv memintB7_total | 12.0% |
| Tconv memintB7_CD3 | 12.0% |
| Tconv memDR_Tconv | 12.0% |
| NKCD56hi_total | 12.0% |
| Ki67_Bcells | 12.0% |
| CD8 RA naive_total | 12.0% |
| CD4neg_CD3 | 12.0% |
| Tconv memintB7_Tconv | 12.0% |
| CD8 RO CXCR3_total | 12.0% |
| CD8 RO_CD8 | 12.0% |
| CD4 Treg_CD4 | 8.0% |
| CD8pos_total | 8.0% |
| CCR5_CD8RO | 8.0% |
| NKCD56hi_nonTnonB | 8.0% |
| CD8pos_CD3 | 8.0% |
| Tconv memCD27_mem | 8.0% |
| Tconv memCCR4_Tconv | 8.0% |
| CD8 RA_CD8 | 8.0% |
| CD8 RO CCR6_total | 8.0% |
| Tconv naive_Tconv | 8.0% |
| CD4 Tconv_CD3 | 4.0% |
| Treg memory_CD4 | 4.0% |
| Treg memory_CD3 | 4.0% |
| CD4 Treg _CD3 | 4.0% |
| Tconv mem_Tconv | 4.0% |

**Total features selected by SVM_RBF_Permutation_AboveMean_t40**: 165

#### SVM_RBF_Permutation_AboveMean_t50

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CCR4_CD8RO | 52.6% |
| CD8 RO DR_CD8 | 36.8% |
| Tconv memPD1_mem | 36.8% |
| DR_CD8RO | 36.8% |
| CD3hi_CD4neg | 31.6% |
| Tconv memCCR6_mem | 31.6% |
| CD8 ncytotox RO CCR4_CD8ntox | 31.6% |
| CD3hi_total | 31.6% |
| CD8 RO CCR4_total | 26.3% |
| CD27IgD_Bcells | 26.3% |
| Bcells memory_total | 26.3% |
| Ki67_CD8RO | 26.3% |
| memory_Bcells | 26.3% |
| CD3pos_total | 21.1% |
| Treg naive_CD3 | 21.1% |
| CD3hi_CD3 | 21.1% |
| CD3neg_total | 21.1% |
| Tconv memDR_CD3 | 21.1% |
| Bcells CD27negIgDneg_total | 21.1% |
| CD14mono_myeloid | 21.1% |
| Tconv memCCR4_mem | 21.1% |
| CD8 RO CD27_CD3 | 15.8% |
| Tconv memPD1_CD3 | 15.8% |
| Tconv memTIGIT_CD3 | 15.8% |
| CD8 RO DR_CD3 | 15.8% |
| CD8  RO Ki67_CD3 | 15.8% |
| CD8 ncytotox RO CCR4_CD3 | 15.8% |
| CD8 RO CCR6_CD3 | 15.8% |
| CD8 RO intB7_total | 15.8% |
| Tconv memCCR5_mem | 15.8% |
| Bcells CD27posIgDneg_total | 15.8% |
| Tconv memCD27_CD3 | 15.8% |
| Treg memory_total | 15.8% |
| CD8 RO TIGIT_CD8 | 15.8% |
| Tconv memKi67_total | 15.8% |
| CD14+16+mono_myeloid | 15.8% |
| CD8 RO DR_total | 15.8% |
| NK_CD3neg | 15.8% |
| Tconv memCCR4_CD3 | 15.8% |
| CD8 RO intB7_CD3 | 15.8% |
| Tconv memPD1_total | 15.8% |
| CD8 RA naive_CD3 | 15.8% |
| CD8 RO Ki67_total | 15.8% |
| Tconv memCCR6_CD3 | 15.8% |
| NKCD16_total | 10.5% |
| CD16mono_CD3neg | 10.5% |
| NKCD16_nonTnonB | 10.5% |
| CD8 RO CD56_CD3 | 10.5% |
| NK_nonTnonB | 10.5% |
| NK_total | 10.5% |
| NK Ki67_CD3neg | 10.5% |
| Tconv memintB7_total | 10.5% |
| Tconv memDR_total | 10.5% |
| Tconv naive_total | 10.5% |
| CD8 RA_total | 10.5% |
| CD8pos_CD3 | 10.5% |
| Tconv memKi67_mem | 10.5% |
| Tconv memCXCR3_mem | 10.5% |
| CD8 RO Ki67_CD8 | 10.5% |
| Bcells_total | 10.5% |
| nonTnonB_total | 10.5% |
| Tconv memCXCR3_CD3 | 10.5% |
| CD8 RA_CD3 | 10.5% |
| NK Ki67_nonTnonB | 10.5% |
| Tconv memCCR4_total | 10.5% |
| Tconv memKi67_CD3 | 10.5% |
| Tconv memintB7_Tconv | 10.5% |
| CD8 RO CD27_CD8 | 10.5% |
| CD14+16+mono_CD3neg | 10.5% |
| Tconv memTIGIT_mem | 10.5% |
| Bcells memory_CD3neg | 10.5% |
| CD8 RO_CD3 | 10.5% |
| Bcells Ki67_total | 10.5% |
| Tconv memCCR5_Tconv | 10.5% |
| Tconv memCD27_mem | 10.5% |
| Tconv memCXCR3_Tconv | 10.5% |
| NKCD16_NK | 10.5% |
| TIGIT_CD8RO | 10.5% |
| NKCD16_CD3neg | 10.5% |
| Tconv memCCR6_Tconv | 10.5% |
| CD8 RO CD56_total | 10.5% |
| Tconv memKi67_Tconv | 10.5% |
| CD8 RA CCR7 naive_CD8 | 10.5% |
| NKCD56hi_total | 10.5% |
| Bcells_CD3neg | 10.5% |
| myeloid_total | 10.5% |
| CD8 RO CD27_total | 10.5% |
| CD8 RO CD56_CD8 | 5.3% |
| CCR5_CD8RO | 5.3% |
| Tconv memCD56_total | 5.3% |
| myeloid_CD3neg | 5.3% |
| Tconv memPD1_Tconv | 5.3% |
| Tconv memintB7_CD3 | 5.3% |
| CD8 RO CXCR3_CD3 | 5.3% |
| Tconv memCXCR3_total | 5.3% |
| Tconv memCD27_total | 5.3% |
| Tconv memCCR6_total | 5.3% |
| CD8 RO CXCR3_total | 5.3% |
| CD4 Treg_total | 5.3% |
| Tconv memCCR5_total | 5.3% |
| CD8 RO CCR5_CD8 | 5.3% |
| Treg memory_CD3 | 5.3% |
| CD4neg_CD3 | 5.3% |
| CD8 RO PD1_total | 5.3% |
| Tconv memCD56_mem | 5.3% |
| Tconv memCD56_CD3 | 5.3% |
| CD4 Treg _CD3 | 5.3% |
| nonTnonB_CD3neg | 5.3% |
| CD8 RO_total | 5.3% |
| Tconv memTIGIT_total | 5.3% |
| CD14+16+mono_total | 5.3% |
| CD8 RO CCR5_total | 5.3% |
| NK Ki67_NK | 5.3% |
| Tconv memCD56_Tconv | 5.3% |
| CD4 Treg_CD4 | 5.3% |
| Tconv memCCR4_Tconv | 5.3% |
| Treg memory_CD4 | 5.3% |
| Tconv memCCR5_CD3 | 5.3% |
| CCR6_CD8RO | 5.3% |
| CD8 RA naive_total | 5.3% |
| CD8 RO PD1_CD8 | 5.3% |
| NKCD56hi_CD3neg | 5.3% |
| NKCD56hi_nonTnonB | 5.3% |
| NKCD56hi_NK | 5.3% |
| CD16mono_myeloid | 5.3% |
| Bcells naive_total | 5.3% |
| CD8 RO TIGIT_CD3 | 5.3% |
| Bcells naive_CD3neg | 5.3% |
| CD14mono_total | 5.3% |
| Treg naive_total | 5.3% |
| Tconv memCD27_Tconv | 5.3% |
| CD4 Tconv_total | 5.3% |
| CD16+mono_total | 5.3% |
| CD4neg_total | 5.3% |
| Tconv memTIGIT_Tconv | 5.3% |
| CD56_CD8RO | 5.3% |
| CD8 RO CCR6_CD8 | 5.3% |
| naive_Bcells | 5.3% |
| intB7_CD8RO | 5.3% |
| PD1_CD8RO | 5.3% |
| CD8 RO CCR6_total | 5.3% |
| Ki67_Bcells | 5.3% |
| CD8 RO intB7_CD8 | 5.3% |

**Total features selected by SVM_RBF_Permutation_AboveMean_t50**: 143

#### SVM_RBF_Permutation_AboveMean_t60

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CCR4_CD8RO | 63.6% |
| CD8 RO DR_CD8 | 45.5% |
| DR_CD8RO | 45.5% |
| Tconv memPD1_mem | 36.4% |
| CD8 ncytotox RO CCR4_CD8ntox | 36.4% |
| Bcells memory_total | 27.3% |
| CD3hi_CD4neg | 18.2% |
| Bcells CD27negIgDneg_total | 18.2% |
| Tconv memCCR6_mem | 18.2% |
| Tconv memDR_CD3 | 18.2% |
| NK_nonTnonB | 9.1% |
| CD3hi_CD3 | 9.1% |
| CCR5_CD8RO | 9.1% |
| CD8 RO TIGIT_CD8 | 9.1% |
| CD8 ncytotox RO CCR4_CD3 | 9.1% |
| CD8 RO CD56_CD8 | 9.1% |
| Tconv memCXCR3_Tconv | 9.1% |
| Tconv memCXCR3_total | 9.1% |
| CD8 RA_total | 9.1% |
| CD8 RO CCR4_total | 9.1% |
| Treg memory_CD3 | 9.1% |
| CD4 Treg _CD3 | 9.1% |
| CD8 RA naive_total | 9.1% |
| Ki67_CD8RO | 9.1% |
| CD8 RA CCR7 naive_CD8 | 9.1% |
| NKCD56hi_nonTnonB | 9.1% |
| NK Ki67_nonTnonB | 9.1% |
| NKCD56hi_NK | 9.1% |
| Tconv memCD27_CD3 | 9.1% |
| Tconv memCCR6_CD3 | 9.1% |
| CD16mono_myeloid | 9.1% |
| CD27IgD_Bcells | 9.1% |
| myeloid_total | 9.1% |
| Tconv memCCR6_Tconv | 9.1% |
| CD16mono_CD3neg | 9.1% |
| Tconv memTIGIT_CD3 | 9.1% |
| CD8 RA naive_CD3 | 9.1% |
| Treg naive_total | 9.1% |
| Tconv memCD27_Tconv | 9.1% |
| Bcells Ki67_total | 9.1% |
| CD3pos_total | 9.1% |
| CD3neg_total | 9.1% |
| Tconv memTIGIT_mem | 9.1% |
| memory_Bcells | 9.1% |
| Tconv memintB7_total | 9.1% |
| CD14mono_myeloid | 9.1% |
| CD8 RO intB7_CD8 | 9.1% |
| CD8 RO CCR6_CD3 | 9.1% |

**Total features selected by SVM_RBF_Permutation_AboveMean_t60**: 48

#### SVM_RBF_Permutation_AboveMean_t70

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CCR4_CD8RO | 100.0% |
| Bcells memory_total | 33.3% |
| Bcells CD27negIgDneg_total | 33.3% |
| CD8 RO DR_CD8 | 33.3% |
| Tconv memCCR6_CD3 | 33.3% |
| CD16mono_myeloid | 33.3% |
| Tconv memCCR6_Tconv | 33.3% |
| CD8 ncytotox RO CCR4_CD8ntox | 33.3% |
| CD3pos_total | 33.3% |
| CD3neg_total | 33.3% |
| memory_Bcells | 33.3% |

**Total features selected by SVM_RBF_Permutation_AboveMean_t70**: 11

#### SVM_RBF_Permutation_AboveMean_t80

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Bcells CD27negIgDneg_total | 100.0% |

**Total features selected by SVM_RBF_Permutation_AboveMean_t80**: 1

#### SVM_RBF_Permutation_Top10%_t40

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Tconv memCD27_total | 100.0% |
| Tconv memCD56_total | 100.0% |
| Tconv memKi67_total | 100.0% |
| Tconv memintB7_total | 100.0% |
| Tconv naive_total | 97.5% |
| CD4 Treg_total | 97.5% |
| Tconv memDR_total | 97.5% |
| CD3pos_total | 97.5% |
| Tconv memCCR4_total | 97.5% |
| Tconv memPD1_total | 95.0% |
| Tconv memCXCR3_total | 95.0% |
| CD4 Tconv mem_total | 95.0% |
| Tconv memCCR5_total | 92.5% |
| Tconv memTIGIT_total | 92.5% |
| CD4 Tconv_total | 92.5% |
| Tconv memCCR6_total | 87.5% |
| CCR4_CD8RO | 22.5% |
| CD3hi_CD4neg | 5.0% |
| Tconv memPD1_mem | 2.5% |
| CD8 RO intB7_total | 2.5% |
| CD8 RO DR_CD8 | 2.5% |
| CD27IgD_Bcells | 2.5% |
| CD8 ncytotox RO CCR4_CD8ntox | 2.5% |
| Tconv memCCR6_CD3 | 2.5% |
| CD3hi_total | 2.5% |
| Tconv memCCR4_mem | 2.5% |
| Bcells CD27negIgDneg_total | 2.5% |
| CD14mono_myeloid | 2.5% |

**Total features selected by SVM_RBF_Permutation_Top10%_t40**: 28

#### SVM_RBF_Permutation_Top10%_t50

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Tconv memKi67_total | 92.5% |
| Tconv memCD27_total | 90.0% |
| Tconv memCD56_total | 87.5% |
| Tconv memCXCR3_total | 87.5% |
| Tconv memPD1_total | 85.0% |
| CD4 Treg_total | 85.0% |
| Tconv memintB7_total | 82.5% |
| Tconv memCCR4_total | 82.5% |
| Tconv memDR_total | 82.5% |
| Tconv naive_total | 82.5% |
| CD4 Tconv mem_total | 77.5% |
| CD3pos_total | 77.5% |
| Tconv memTIGIT_total | 77.5% |
| Tconv memCCR5_total | 77.5% |
| Tconv memCCR6_total | 75.0% |
| CD4 Tconv_total | 75.0% |
| CCR4_CD8RO | 10.0% |
| CD3hi_total | 2.5% |

**Total features selected by SVM_RBF_Permutation_Top10%_t50**: 18

#### SVM_RBF_Permutation_Top10%_t60

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Tconv memKi67_total | 79.5% |
| Tconv memCXCR3_total | 79.5% |
| Tconv memPD1_total | 71.8% |
| CD4 Treg_total | 71.8% |
| Tconv memDR_total | 71.8% |
| Tconv naive_total | 69.2% |
| Tconv memCD56_total | 69.2% |
| Tconv memCD27_total | 66.7% |
| Tconv memTIGIT_total | 66.7% |
| CD3pos_total | 64.1% |
| Tconv memCCR5_total | 64.1% |
| Tconv memintB7_total | 61.5% |
| Tconv memCCR4_total | 61.5% |
| CD4 Tconv mem_total | 59.0% |
| Tconv memCCR6_total | 56.4% |
| CD4 Tconv_total | 56.4% |
| CCR4_CD8RO | 2.6% |

**Total features selected by SVM_RBF_Permutation_Top10%_t60**: 17

#### SVM_RBF_Permutation_Top10%_t70

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Tconv memKi67_total | 80.6% |
| Tconv memCXCR3_total | 71.0% |
| Tconv memCD56_total | 71.0% |
| Tconv memintB7_total | 67.7% |
| Tconv memCD27_total | 64.5% |
| CD3pos_total | 64.5% |
| Tconv naive_total | 64.5% |
| CD4 Treg_total | 64.5% |
| Tconv memPD1_total | 61.3% |
| Tconv memDR_total | 61.3% |
| Tconv memTIGIT_total | 61.3% |
| Tconv memCCR5_total | 51.6% |
| CD4 Tconv_total | 48.4% |
| Tconv memCCR4_total | 48.4% |
| CD4 Tconv mem_total | 48.4% |
| Tconv memCCR6_total | 41.9% |

**Total features selected by SVM_RBF_Permutation_Top10%_t70**: 16

#### SVM_RBF_Permutation_Top10%_t80

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Tconv memCXCR3_total | 82.6% |
| Tconv memintB7_total | 65.2% |
| CD3pos_total | 60.9% |
| Tconv memCD56_total | 60.9% |
| CD4 Treg_total | 60.9% |
| Tconv memDR_total | 56.5% |
| Tconv memKi67_total | 56.5% |
| Tconv naive_total | 56.5% |
| Tconv memPD1_total | 56.5% |
| CD4 Tconv mem_total | 56.5% |
| Tconv memCD27_total | 52.2% |
| Tconv memCCR5_total | 47.8% |
| Tconv memTIGIT_total | 47.8% |
| Tconv memCCR6_total | 43.5% |
| Tconv memCCR4_total | 43.5% |
| CD4 Tconv_total | 39.1% |

**Total features selected by SVM_RBF_Permutation_Top10%_t80**: 16

#### XGB_Importance_t40

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Tconv naive_total | 85.0% |
| CD16mono_CD3neg | 85.0% |
| CD8 RO CCR5_CD3 | 67.5% |
| Bcells CD27posIgDneg_total | 65.0% |
| CD4 Treg_CD4 | 62.5% |
| NKCD56hi_total | 55.0% |
| Tconv memPD1_total | 55.0% |
| CD8pos_CD3 | 55.0% |
| CD27IgD_Bcells | 55.0% |
| CD16mono_myeloid | 52.5% |
| Tconv memKi67_total | 37.5% |
| CCR5_CD8RO | 30.0% |
| CD8 RO CXCR3_CD3 | 30.0% |
| CD4 Tconv mem_total | 27.5% |
| CD8 RO CD56_CD3 | 27.5% |
| CD14mono_myeloid | 25.0% |
| CD3pos_total | 25.0% |
| CD4 Tconv_total | 22.5% |
| CD8 RO CCR5_total | 22.5% |
| Tconv memKi67_mem | 22.5% |
| Tconv memDR_total | 20.0% |
| CD8 RA_CD3 | 20.0% |
| Tconv memTIGIT_mem | 20.0% |
| Tconv memPD1_mem | 17.5% |
| Tconv memCCR4_total | 17.5% |
| Treg memory_CD4 | 17.5% |
| CD8 RO DR_CD3 | 17.5% |
| CD14+16+mono_myeloid | 17.5% |
| CD8pos_total | 17.5% |
| CCR4_CD8RO | 15.0% |
| CD8 RO CCR5_CD8 | 15.0% |
| CD8  RO Ki67_CD3 | 15.0% |
| CD3hi_total | 15.0% |
| CD8 RO DR_total | 15.0% |
| Ki67_Bcells | 15.0% |
| Tconv memCXCR3_Tconv | 12.5% |
| CD27negIgDneg_Bcells | 12.5% |
| Tconv memCCR6_mem | 12.5% |
| CD8 RO DR_CD8 | 12.5% |
| Tconv memCCR4_mem | 10.0% |
| NK_total | 10.0% |
| nonTnonB_CD3neg | 10.0% |
| CD16+mono_total | 7.5% |
| CD4 Treg _CD3 | 7.5% |
| CD8 RO CCR6_CD8 | 7.5% |
| NKCD56hi_CD3neg | 7.5% |
| Tconv memCCR6_CD3 | 7.5% |
| Tconv memCCR5_mem | 7.5% |
| Treg naive_total | 7.5% |
| Tconv memCXCR3_total | 7.5% |
| Bcells memory_CD3neg | 7.5% |
| Tconv memCD27_mem | 7.5% |
| CD3hi_CD4neg | 7.5% |
| Treg memory_CD3 | 7.5% |
| Tconv memCD56_total | 7.5% |
| Treg naive_CD4 | 7.5% |
| CD8 RO CD56_total | 7.5% |
| NKCD16_NK | 5.0% |
| Bcells memory_total | 5.0% |
| CD8 RA CCR7 naive_CD8 | 5.0% |
| Tconv memCD27_total | 5.0% |
| NKCD56hi_NK | 5.0% |
| CD8 RO_CD3 | 5.0% |
| NK Ki67_NK | 5.0% |
| NK Ki67_total | 5.0% |
| CD8 RO CD56_CD8 | 5.0% |
| CD14+16+mono_total | 5.0% |
| Bcells_total | 5.0% |
| NKCD56hi_nonTnonB | 5.0% |
| CD4 Tconv_CD3 | 5.0% |
| Bcells CD27negIgDneg_total | 5.0% |
| CD8 RO CD27_CD3 | 5.0% |
| CD8 RA naive_CD3 | 5.0% |
| Tconv memDR_mem | 5.0% |
| CD8 RO TIGIT_CD3 | 5.0% |
| Ki67_CD8RO | 5.0% |
| Tconv memCCR6_Tconv | 5.0% |
| Tconv memCCR5_total | 5.0% |
| Tconv memCCR5_CD3 | 2.5% |
| Tconv memCXCR3_CD3 | 2.5% |
| Tconv mem_Tconv | 2.5% |
| CD8 RO CXCR3_total | 2.5% |
| Tconv memintB7_CD3 | 2.5% |
| CD8 RO CCR6_CD3 | 2.5% |
| Treg naive_CD3 | 2.5% |
| Tconv memCD56_mem | 2.5% |
| DR_CD8RO | 2.5% |
| CD4neg_total | 2.5% |
| Treg memory_total | 2.5% |
| Bcells Ki67_total | 2.5% |
| myeloid_CD3neg | 2.5% |
| Tconv memCXCR3_mem | 2.5% |
| CD56_CD8RO | 2.5% |
| CD8 ncytotox RO CCR4_CD8ntox | 2.5% |
| Tconv memCCR6_total | 2.5% |
| CD14mono_total | 2.5% |
| Tconv memCD27_Tconv | 2.5% |

**Total features selected by XGB_Importance_t40**: 97

#### XGB_Importance_t50

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Tconv naive_total | 72.5% |
| CD16mono_CD3neg | 72.5% |
| Bcells CD27posIgDneg_total | 50.0% |
| CD4 Treg_CD4 | 45.0% |
| CD8pos_CD3 | 45.0% |
| CD27IgD_Bcells | 42.5% |
| CD8 RO CCR5_CD3 | 37.5% |
| NKCD56hi_total | 37.5% |
| CD16mono_myeloid | 35.0% |
| Tconv memPD1_total | 35.0% |
| CD8 RO CXCR3_CD3 | 22.5% |
| Tconv memKi67_total | 17.5% |
| CD4 Tconv mem_total | 15.0% |
| CD8 RO CD56_CD3 | 12.5% |
| CD8  RO Ki67_CD3 | 12.5% |
| Tconv memPD1_mem | 12.5% |
| Tconv memKi67_mem | 12.5% |
| Tconv memTIGIT_mem | 10.0% |
| CD8 RO CCR5_CD8 | 10.0% |
| Tconv memDR_total | 10.0% |
| CD14mono_myeloid | 10.0% |
| CD8 RA_CD3 | 10.0% |
| CD3pos_total | 10.0% |
| CCR5_CD8RO | 10.0% |
| Tconv memCCR4_mem | 7.5% |
| CD8 RO DR_CD3 | 7.5% |
| NKCD56hi_CD3neg | 7.5% |
| Tconv memCXCR3_Tconv | 7.5% |
| CCR4_CD8RO | 7.5% |
| CD16+mono_total | 7.5% |
| CD8 RO DR_total | 7.5% |
| CD8 RO DR_CD8 | 7.5% |
| Treg memory_CD4 | 7.5% |
| Tconv memCCR6_mem | 7.5% |
| CD14+16+mono_myeloid | 7.5% |
| CD8 RO CCR5_total | 7.5% |
| NKCD56hi_nonTnonB | 5.0% |
| CD3hi_CD4neg | 5.0% |
| CD8pos_total | 5.0% |
| CD8 RO CCR6_CD8 | 5.0% |
| NKCD56hi_NK | 5.0% |
| CD3hi_total | 5.0% |
| Tconv memCXCR3_total | 5.0% |
| Tconv memCCR6_Tconv | 5.0% |
| Ki67_Bcells | 5.0% |
| CD27negIgDneg_Bcells | 5.0% |
| nonTnonB_CD3neg | 5.0% |
| NK Ki67_NK | 5.0% |
| Tconv mem_Tconv | 2.5% |
| Tconv memCCR6_CD3 | 2.5% |
| Tconv memCXCR3_CD3 | 2.5% |
| CD8 RA CCR7 naive_CD8 | 2.5% |
| Treg naive_total | 2.5% |
| Treg memory_CD3 | 2.5% |
| NK Ki67_total | 2.5% |
| CD14+16+mono_total | 2.5% |
| Bcells_total | 2.5% |
| Treg memory_total | 2.5% |
| CD4 Treg _CD3 | 2.5% |
| Tconv memCCR4_total | 2.5% |
| Ki67_CD8RO | 2.5% |
| NK_total | 2.5% |
| CD4 Tconv_total | 2.5% |
| Tconv memCCR6_total | 2.5% |

**Total features selected by XGB_Importance_t50**: 64

#### XGB_Importance_t60

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD16mono_CD3neg | 62.5% |
| Tconv naive_total | 57.5% |
| CD8pos_CD3 | 42.5% |
| Bcells CD27posIgDneg_total | 40.0% |
| Tconv memPD1_total | 30.0% |
| CD4 Treg_CD4 | 27.5% |
| CD27IgD_Bcells | 25.0% |
| CD8 RO CCR5_CD3 | 22.5% |
| NKCD56hi_total | 17.5% |
| CD16mono_myeloid | 17.5% |
| Tconv memKi67_total | 15.0% |
| Tconv memPD1_mem | 10.0% |
| CD14mono_myeloid | 7.5% |
| CD8 RO CD56_CD3 | 7.5% |
| Tconv memCXCR3_Tconv | 5.0% |
| Tconv memTIGIT_mem | 5.0% |
| CD8  RO Ki67_CD3 | 5.0% |
| CD8 RO CXCR3_CD3 | 5.0% |
| CD8 RO CCR5_CD8 | 5.0% |
| CD8 RO CCR5_total | 5.0% |
| CD8 RO DR_CD8 | 5.0% |
| Treg memory_CD4 | 5.0% |
| CD8 RO DR_total | 5.0% |
| CD8 RO CCR6_CD8 | 5.0% |
| Treg naive_total | 2.5% |
| CD8 RA_CD3 | 2.5% |
| CCR4_CD8RO | 2.5% |
| CD8 RO DR_CD3 | 2.5% |
| Tconv memDR_total | 2.5% |
| Tconv memCCR4_mem | 2.5% |
| Ki67_Bcells | 2.5% |
| CD8pos_total | 2.5% |
| CD16+mono_total | 2.5% |
| NKCD56hi_CD3neg | 2.5% |
| CD14+16+mono_myeloid | 2.5% |
| Tconv memCCR6_mem | 2.5% |
| CD4 Treg _CD3 | 2.5% |
| Treg memory_total | 2.5% |
| Tconv memKi67_mem | 2.5% |
| CD4 Tconv_total | 2.5% |

**Total features selected by XGB_Importance_t60**: 40

#### XGB_Importance_t70

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Tconv naive_total | 48.7% |
| CD16mono_CD3neg | 46.2% |
| CD8pos_CD3 | 23.1% |
| CD27IgD_Bcells | 23.1% |
| CD4 Treg_CD4 | 17.9% |
| Bcells CD27posIgDneg_total | 17.9% |
| CD8 RO CCR5_CD3 | 12.8% |
| CD16mono_myeloid | 10.3% |
| NKCD56hi_total | 7.7% |
| Tconv memPD1_total | 7.7% |
| Tconv memPD1_mem | 7.7% |
| Tconv memKi67_total | 7.7% |
| CD14mono_myeloid | 5.1% |
| Tconv memTIGIT_mem | 5.1% |
| Treg naive_total | 2.6% |
| CD8 RO CCR6_CD8 | 2.6% |
| CD8 RO CD56_CD3 | 2.6% |
| CD8  RO Ki67_CD3 | 2.6% |
| CD14+16+mono_myeloid | 2.6% |
| NKCD56hi_CD3neg | 2.6% |
| Treg memory_CD4 | 2.6% |
| CD8 RO DR_CD8 | 2.6% |
| CD4 Tconv_total | 2.6% |

**Total features selected by XGB_Importance_t70**: 23

#### XGB_Importance_t80

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD16mono_CD3neg | 38.7% |
| Tconv naive_total | 35.5% |
| CD8pos_CD3 | 19.4% |
| CD8 RO CCR5_CD3 | 12.9% |
| CD4 Treg_CD4 | 12.9% |
| CD14mono_myeloid | 6.5% |
| CD16mono_myeloid | 6.5% |
| Treg naive_total | 3.2% |
| Bcells CD27posIgDneg_total | 3.2% |
| CD8  RO Ki67_CD3 | 3.2% |
| Tconv memKi67_total | 3.2% |
| Tconv memTIGIT_mem | 3.2% |
| Tconv memPD1_mem | 3.2% |
| CD27IgD_Bcells | 3.2% |
| Tconv memPD1_total | 3.2% |

**Total features selected by XGB_Importance_t80**: 15

#### XGBoost_Permutation_AboveMean_t40

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Tconv naive_total | 42.9% |
| CD16mono_CD3neg | 21.4% |
| CD8pos_CD3 | 14.3% |
| CD8 RO CCR5_CD3 | 14.3% |
| CD8  RO Ki67_CD3 | 7.1% |

**Total features selected by XGBoost_Permutation_AboveMean_t40**: 5

#### XGBoost_Permutation_AboveMean_t50

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Tconv naive_total | 37.5% |
| CD8 RO CCR5_CD3 | 25.0% |
| CD8pos_CD3 | 12.5% |
| CD8  RO Ki67_CD3 | 12.5% |
| CD16mono_CD3neg | 12.5% |

**Total features selected by XGBoost_Permutation_AboveMean_t50**: 5

#### XGBoost_Permutation_AboveMean_t60

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD8 RO CCR5_CD3 | 50.0% |
| CD8pos_CD3 | 25.0% |
| Tconv naive_total | 25.0% |

**Total features selected by XGBoost_Permutation_AboveMean_t60**: 3

#### XGBoost_Permutation_AboveMean_t70

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD8pos_CD3 | 50.0% |
| Tconv naive_total | 50.0% |

**Total features selected by XGBoost_Permutation_AboveMean_t70**: 2

#### XGBoost_Permutation_AboveMean_t80

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD8pos_CD3 | 100.0% |

**Total features selected by XGBoost_Permutation_AboveMean_t80**: 1

#### XGBoost_Permutation_Top10%_t40

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Tconv memCCR4_total | 100.0% |
| CD4 Tconv mem_total | 100.0% |
| CD3pos_total | 100.0% |
| Tconv memCD27_total | 100.0% |
| Tconv memCXCR3_total | 100.0% |
| Tconv memCD56_total | 100.0% |
| Tconv memintB7_total | 100.0% |
| Tconv memTIGIT_total | 100.0% |
| Tconv memKi67_total | 100.0% |
| Tconv memPD1_total | 100.0% |
| Tconv memDR_total | 100.0% |
| CD4 Tconv_total | 100.0% |
| Tconv naive_total | 100.0% |
| CD4 Treg_total | 100.0% |
| Tconv memCCR6_total | 85.0% |
| Tconv memCCR5_total | 72.5% |
| CD16mono_CD3neg | 10.0% |
| CD4 Treg_CD4 | 7.5% |
| CD8 RO CCR5_CD3 | 7.5% |
| CD8pos_CD3 | 5.0% |
| CD8  RO Ki67_CD3 | 2.5% |
| CD27IgD_Bcells | 2.5% |
| Bcells CD27posIgDneg_total | 2.5% |

**Total features selected by XGBoost_Permutation_Top10%_t40**: 23

#### XGBoost_Permutation_Top10%_t50

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD3pos_total | 100.0% |
| Tconv memCXCR3_total | 100.0% |
| Tconv memCD27_total | 100.0% |
| Tconv memintB7_total | 100.0% |
| Tconv memCD56_total | 100.0% |
| Tconv memDR_total | 100.0% |
| Tconv memTIGIT_total | 100.0% |
| Tconv memKi67_total | 100.0% |
| Tconv memPD1_total | 100.0% |
| Tconv naive_total | 100.0% |
| CD4 Treg_total | 100.0% |
| CD4 Tconv mem_total | 97.5% |
| Tconv memCCR4_total | 95.0% |
| CD4 Tconv_total | 95.0% |
| Tconv memCCR5_total | 57.5% |
| Tconv memCCR6_total | 50.0% |
| CD8 RO CCR5_CD3 | 7.5% |
| CD8  RO Ki67_CD3 | 2.5% |
| CD8pos_CD3 | 2.5% |
| CD16mono_CD3neg | 2.5% |
| CD4 Treg_CD4 | 2.5% |

**Total features selected by XGBoost_Permutation_Top10%_t50**: 21

#### XGBoost_Permutation_Top10%_t60

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD3pos_total | 100.0% |
| Tconv memCXCR3_total | 100.0% |
| Tconv memCD27_total | 100.0% |
| Tconv naive_total | 100.0% |
| CD4 Treg_total | 100.0% |
| Tconv memCD56_total | 100.0% |
| Tconv memintB7_total | 100.0% |
| Tconv memKi67_total | 100.0% |
| Tconv memPD1_total | 100.0% |
| Tconv memDR_total | 100.0% |
| Tconv memTIGIT_total | 100.0% |
| CD4 Tconv mem_total | 97.5% |
| Tconv memCCR4_total | 95.0% |
| CD4 Tconv_total | 77.5% |
| Tconv memCCR5_total | 40.0% |
| Tconv memCCR6_total | 20.0% |
| CD8 RO CCR5_CD3 | 5.0% |
| CD8pos_CD3 | 2.5% |
| CD8  RO Ki67_CD3 | 2.5% |

**Total features selected by XGBoost_Permutation_Top10%_t60**: 19

#### XGBoost_Permutation_Top10%_t70

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Tconv memCD27_total | 100.0% |
| CD3pos_total | 100.0% |
| Tconv memTIGIT_total | 100.0% |
| Tconv naive_total | 100.0% |
| Tconv memCXCR3_total | 100.0% |
| Tconv memCD56_total | 100.0% |
| Tconv memintB7_total | 100.0% |
| Tconv memKi67_total | 100.0% |
| Tconv memPD1_total | 100.0% |
| Tconv memDR_total | 100.0% |
| CD4 Treg_total | 100.0% |
| CD4 Tconv mem_total | 97.5% |
| Tconv memCCR4_total | 82.5% |
| CD4 Tconv_total | 52.5% |
| Tconv memCCR6_total | 10.0% |
| Tconv memCCR5_total | 7.5% |
| CD8pos_CD3 | 2.5% |
| CD8 RO CCR5_CD3 | 2.5% |

**Total features selected by XGBoost_Permutation_Top10%_t70**: 18

#### XGBoost_Permutation_Top10%_t80

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Tconv memCD27_total | 100.0% |
| Tconv memintB7_total | 100.0% |
| Tconv memCD56_total | 100.0% |
| Tconv memCXCR3_total | 100.0% |
| Tconv memKi67_total | 100.0% |
| CD4 Treg_total | 100.0% |
| Tconv naive_total | 100.0% |
| Tconv memPD1_total | 100.0% |
| CD3pos_total | 97.5% |
| Tconv memDR_total | 97.5% |
| Tconv memTIGIT_total | 95.0% |
| CD4 Tconv mem_total | 90.0% |
| Tconv memCCR4_total | 47.5% |
| CD4 Tconv_total | 20.0% |
| CD8pos_CD3 | 2.5% |
| Tconv memCCR6_total | 2.5% |

**Total features selected by XGBoost_Permutation_Top10%_t80**: 16

#### mRMR (Top 10%)_t40

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD4 Treg_CD4 | 80.0% |
| CD16mono_myeloid | 75.0% |
| CD4 Tconv_total | 75.0% |
| CD8pos_CD3 | 62.5% |
| CD14mono_myeloid | 55.0% |
| CD27IgD_Bcells | 55.0% |
| Treg memory_CD4 | 55.0% |
| Tconv naive_total | 52.5% |
| CD8 RO CCR5_CD3 | 52.5% |
| Tconv naive_CD3 | 50.0% |
| CD16mono_CD3neg | 45.0% |
| CD4 Tconv_CD3 | 45.0% |
| CD4 Treg _CD3 | 42.5% |
| CD8 RA_CD3 | 40.0% |
| CD8 RO CCR5_CD8 | 35.0% |
| Treg memory_CD3 | 35.0% |
| NKCD56hi_total | 35.0% |
| CCR4_CD8RO | 27.5% |
| Tconv memCCR6_Tconv | 20.0% |
| Tconv memCXCR3_Tconv | 20.0% |
| CD8 RO CXCR3_CD3 | 20.0% |
| Tconv memPD1_mem | 20.0% |
| CD3pos_total | 17.5% |
| Tconv memCCR5_Tconv | 17.5% |
| Tconv memKi67_total | 15.0% |
| CCR5_CD8RO | 15.0% |
| CD3neg_total | 15.0% |
| Bcells CD27posIgDneg_total | 15.0% |
| CD4neg_CD3 | 15.0% |
| Bcells CD27negIgDneg_total | 12.5% |
| Tconv memCCR6_CD3 | 12.5% |
| CD8 RO DR_CD3 | 12.5% |
| CD8 RO CD56_CD3 | 12.5% |
| CD8 RO TIGIT_CD3 | 10.0% |
| Tconv mem_Tconv | 10.0% |
| CD8 RO CD27_CD3 | 10.0% |
| Tconv memCCR6_mem | 10.0% |
| CD8 RO_CD3 | 10.0% |
| Treg naive_CD4 | 7.5% |
| NKCD56hi_nonTnonB | 7.5% |
| CD14+16+mono_myeloid | 7.5% |
| Tconv memCCR5_mem | 7.5% |
| CD27negIgDneg_Bcells | 7.5% |
| CD8 RO CCR6_CD3 | 7.5% |
| CD8 RO CCR5_total | 7.5% |
| CD8 RO DR_CD8 | 7.5% |
| CD8 RA naive_CD3 | 7.5% |
| Tconv memintB7_Tconv | 5.0% |
| Tconv memCCR4_mem | 5.0% |
| CD8 RO CXCR3_CD8 | 5.0% |
| DR_CD8RO | 5.0% |
| CD3hi_CD4neg | 5.0% |
| Tconv naive_Tconv | 5.0% |
| Tconv memCXCR3_CD3 | 5.0% |
| Tconv memCD27_mem | 5.0% |
| CCR6_CD8RO | 2.5% |
| CD8 RO CCR6_CD8 | 2.5% |
| CD8 RO CD56_CD8 | 2.5% |
| Bcells Ki67_total | 2.5% |
| NKCD56hi_NK | 2.5% |
| CD8 RO intB7_CD3 | 2.5% |
| CD8 RO CXCR3_total | 2.5% |
| CD8 RA_total | 2.5% |
| Tconv memCD27_total | 2.5% |
| Tconv memCD27_Tconv | 2.5% |
| CD8 RO PD1_total | 2.5% |
| CD8 RO PD1_CD3 | 2.5% |
| Bcells_total | 2.5% |
| CXCR3_CD8RO | 2.5% |
| Tconv memDR_total | 2.5% |
| CD27_CD8RO | 2.5% |

**Total features selected by mRMR (Top 10%)_t40**: 71

#### mRMR (Top 10%)_t50

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD4 Treg_CD4 | 65.0% |
| CD16mono_myeloid | 57.5% |
| CD4 Tconv_total | 57.5% |
| CD8 RO CCR5_CD3 | 52.5% |
| Treg memory_CD4 | 47.5% |
| CD14mono_myeloid | 42.5% |
| CD8pos_CD3 | 40.0% |
| Tconv naive_total | 40.0% |
| CD16mono_CD3neg | 32.5% |
| CD27IgD_Bcells | 32.5% |
| CD8 RA_CD3 | 22.5% |
| NKCD56hi_total | 22.5% |
| CD4 Tconv_CD3 | 22.5% |
| Tconv naive_CD3 | 22.5% |
| Treg memory_CD3 | 22.5% |
| CD8 RO CCR5_CD8 | 22.5% |
| CCR4_CD8RO | 20.0% |
| CD4 Treg _CD3 | 20.0% |
| Tconv memCXCR3_Tconv | 17.5% |
| CD8 RO CD56_CD3 | 12.5% |
| CD8 RO CXCR3_CD3 | 12.5% |
| Tconv memPD1_mem | 12.5% |
| Tconv memCCR6_Tconv | 12.5% |
| Bcells CD27posIgDneg_total | 10.0% |
| CD8 RO CD27_CD3 | 10.0% |
| CD4neg_CD3 | 7.5% |
| CD8 RO DR_CD3 | 7.5% |
| CD8 RO CCR6_CD3 | 7.5% |
| CD3pos_total | 7.5% |
| CD3neg_total | 7.5% |
| Tconv memCCR6_mem | 7.5% |
| CD8 RA naive_CD3 | 7.5% |
| Tconv memKi67_total | 5.0% |
| Tconv memCCR6_CD3 | 5.0% |
| Tconv memCCR5_mem | 5.0% |
| Tconv memCCR5_Tconv | 5.0% |
| Tconv memCXCR3_CD3 | 5.0% |
| CD8 RO DR_CD8 | 5.0% |
| CD8 RO CCR5_total | 5.0% |
| Tconv mem_Tconv | 5.0% |
| Tconv memCCR4_mem | 5.0% |
| NKCD56hi_nonTnonB | 5.0% |
| Bcells CD27negIgDneg_total | 5.0% |
| Tconv memintB7_Tconv | 5.0% |
| CD8 RO CCR6_CD8 | 2.5% |
| CD8 RO_CD3 | 2.5% |
| CCR5_CD8RO | 2.5% |
| CD8 RO CXCR3_CD8 | 2.5% |
| CD8 RO TIGIT_CD3 | 2.5% |
| CD14+16+mono_myeloid | 2.5% |
| CD8 RO PD1_CD3 | 2.5% |
| CXCR3_CD8RO | 2.5% |
| CD27negIgDneg_Bcells | 2.5% |

**Total features selected by mRMR (Top 10%)_t50**: 53

#### mRMR (Top 10%)_t60

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Treg memory_CD4 | 42.5% |
| CD4 Treg_CD4 | 40.0% |
| CD14mono_myeloid | 40.0% |
| CD8 RO CCR5_CD3 | 32.5% |
| CD4 Tconv_total | 32.5% |
| CD16mono_myeloid | 30.0% |
| CD8pos_CD3 | 27.5% |
| CD27IgD_Bcells | 27.5% |
| Tconv naive_total | 27.5% |
| CD16mono_CD3neg | 20.0% |
| CD4 Tconv_CD3 | 15.0% |
| Tconv naive_CD3 | 15.0% |
| CCR4_CD8RO | 15.0% |
| NKCD56hi_total | 12.5% |
| CD8 RA_CD3 | 12.5% |
| CD8 RO CCR5_CD8 | 12.5% |
| CD4 Treg _CD3 | 10.0% |
| Tconv memCCR6_Tconv | 10.0% |
| Tconv memCXCR3_Tconv | 10.0% |
| Treg memory_CD3 | 10.0% |
| CD8 RO CD27_CD3 | 7.5% |
| CD4neg_CD3 | 7.5% |
| CD8 RO CXCR3_CD3 | 7.5% |
| Bcells CD27posIgDneg_total | 7.5% |
| CD8 RO DR_CD3 | 5.0% |
| CD8 RO CD56_CD3 | 5.0% |
| CD8 RO DR_CD8 | 5.0% |
| Tconv memPD1_mem | 5.0% |
| CD3neg_total | 5.0% |
| CD3pos_total | 5.0% |
| CD8 RO CCR6_CD8 | 2.5% |
| CD8 RO_CD3 | 2.5% |
| Tconv memCCR5_Tconv | 2.5% |
| Tconv memKi67_total | 2.5% |
| Tconv mem_Tconv | 2.5% |
| CD8 RO CCR5_total | 2.5% |
| CCR5_CD8RO | 2.5% |
| NKCD56hi_nonTnonB | 2.5% |
| Tconv memCCR6_mem | 2.5% |
| CD8 RO TIGIT_CD3 | 2.5% |
| Tconv memintB7_Tconv | 2.5% |
| CD8 RA naive_CD3 | 2.5% |
| CD8 RO CCR6_CD3 | 2.5% |

**Total features selected by mRMR (Top 10%)_t60**: 43

#### mRMR (Top 10%)_t70

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD4 Treg_CD4 | 30.8% |
| CD14mono_myeloid | 30.8% |
| CD8 RO CCR5_CD3 | 25.6% |
| Treg memory_CD4 | 23.1% |
| CD27IgD_Bcells | 23.1% |
| CD16mono_myeloid | 20.5% |
| CD4 Tconv_total | 20.5% |
| CD8pos_CD3 | 20.5% |
| Tconv naive_total | 17.9% |
| CD8 RA_CD3 | 10.3% |
| CD4 Tconv_CD3 | 10.3% |
| CD16mono_CD3neg | 10.3% |
| CD8 RO CXCR3_CD3 | 7.7% |
| Tconv memCXCR3_Tconv | 7.7% |
| CD8 RO CCR5_CD8 | 7.7% |
| CCR4_CD8RO | 7.7% |
| CD8 RO CD27_CD3 | 5.1% |
| Bcells CD27posIgDneg_total | 5.1% |
| Tconv naive_CD3 | 5.1% |
| CD4neg_CD3 | 5.1% |
| CD8 RO DR_CD8 | 5.1% |
| Tconv memCCR6_Tconv | 5.1% |
| CD4 Treg _CD3 | 5.1% |
| NKCD56hi_total | 5.1% |
| Tconv memPD1_mem | 5.1% |
| CD3pos_total | 2.6% |
| CD8 RO_CD3 | 2.6% |
| Tconv memCCR5_Tconv | 2.6% |
| CD8 RO CCR6_CD8 | 2.6% |
| CCR5_CD8RO | 2.6% |
| CD8 RO CCR5_total | 2.6% |
| CD3neg_total | 2.6% |
| Tconv memCCR6_mem | 2.6% |
| CD8 RA naive_CD3 | 2.6% |
| Treg memory_CD3 | 2.6% |
| CD8 RO CCR6_CD3 | 2.6% |
| CD8 RO DR_CD3 | 2.6% |

**Total features selected by mRMR (Top 10%)_t70**: 37

#### mRMR (Top 10%)_t80

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD14mono_myeloid | 27.3% |
| CD8 RO CCR5_CD3 | 24.2% |
| CD4 Treg_CD4 | 21.2% |
| CD16mono_myeloid | 18.2% |
| CD8pos_CD3 | 15.2% |
| Treg memory_CD4 | 15.2% |
| Tconv naive_total | 15.2% |
| CD27IgD_Bcells | 12.1% |
| CD4 Tconv_CD3 | 9.1% |
| CD8 RO CD27_CD3 | 6.1% |
| Tconv memCXCR3_Tconv | 6.1% |
| CD4 Tconv_total | 6.1% |
| CD8 RO CXCR3_CD3 | 6.1% |
| CCR4_CD8RO | 6.1% |
| CD8 RO CCR5_CD8 | 6.1% |
| CD8 RA_CD3 | 6.1% |
| CD8 RO DR_CD8 | 3.0% |
| CD8 RO CCR5_total | 3.0% |
| Tconv memCCR6_Tconv | 3.0% |
| NKCD56hi_total | 3.0% |
| Bcells CD27posIgDneg_total | 3.0% |
| Treg memory_CD3 | 3.0% |
| CD8 RO CCR6_CD3 | 3.0% |
| CD8 RO DR_CD3 | 3.0% |
| Tconv memPD1_mem | 3.0% |
| CD16mono_CD3neg | 3.0% |

**Total features selected by mRMR (Top 10%)_t80**: 26

## Overall Stable Features by Threshold

### Threshold 40%

`Tconv naive_total`

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
| CD14mono_myeloid | 46.5% |
| CCR4_CD8RO | 44.2% |
| CD27IgD_Bcells | 42.0% |
| CD16mono_myeloid | 40.2% |
| NKCD56hi_nonTnonB | 38.5% |
| CD8pos_CD3 | 36.2% |
| Tconv memPD1_mem | 36.0% |
| CD3hi_CD4neg | 34.2% |
| NKCD56hi_total | 32.5% |
| CD14+16+mono_myeloid | 31.8% |
| CD8 RA_CD3 | 27.0% |
| CD4 Treg_CD4 | 26.5% |
| CD16mono_CD3neg | 24.2% |
| Bcells CD27negIgDneg_total | 23.5% |
| CD27negIgDneg_Bcells | 23.2% |
| Tconv memKi67_total | 22.2% |
| DR_CD8RO | 22.0% |
| Tconv memKi67_mem | 22.0% |
| Tconv naive_total | 22.0% |
| Tconv memCCR6_mem | 21.8% |
| CD8 RO CCR5_CD8 | 21.5% |
| Treg memory_CD4 | 21.5% |
| CD8 RO CCR5_CD3 | 21.2% |
| Bcells memory_total | 21.0% |
| CD4 Tconv_total | 20.0% |
| Tconv memCCR6_Tconv | 19.8% |
| CD8 RO TIGIT_CD3 | 19.5% |
| Treg memory_CD3 | 18.5% |
| CD8 RA_total | 18.5% |
| CD3hi_total | 18.2% |
| CD8 RA CCR7 naive_CD8 | 18.0% |
| Bcells CD27posIgDneg_total | 17.8% |
| TIGIT_CD8RO | 17.0% |
| CD4 Treg _CD3 | 16.0% |
| CD8 RO CXCR3_CD3 | 16.0% |
| Bcells Ki67_total | 15.8% |
| Treg naive_total | 15.8% |
| Tconv memCCR6_CD3 | 15.5% |
| intB7_CD8RO | 15.5% |
| CD8 RO CXCR3_CD8 | 15.5% |
| Tconv memCD27_mem | 15.5% |
| Bcells Ki67_CD3neg | 15.5% |
| CCR5_CD8RO | 15.2% |
| Tconv naive_CD3 | 15.0% |
| Treg naive_CD4 | 14.5% |
| CD8 RA naive_CD3 | 14.2% |
| Tconv memTIGIT_Tconv | 14.0% |
| CD4 Tconv_CD3 | 13.8% |
| Treg memory_total | 13.5% |
| Ki67_Bcells | 13.5% |
| NK_total | 13.5% |
| Tconv memCXCR3_CD3 | 12.5% |
| NK Ki67_nonTnonB | 12.2% |
| Tconv memintB7_Tconv | 12.2% |
| Tconv memCCR4_mem | 12.0% |
| CD4neg_CD3 | 12.0% |
| Tconv memKi67_CD3 | 11.8% |
| Tconv memDR_mem | 11.8% |
| CD8 RO DR_CD8 | 11.5% |
| NKCD56hi_NK | 11.2% |
| CD8 RO CD27_CD3 | 11.2% |
| Tconv memCXCR3_Tconv | 11.2% |
| Tconv memCD56_total | 11.0% |
| NK Ki67_NK | 11.0% |
| NKCD56hi_CD3neg | 10.8% |
| CD8 RO CCR6_CD8 | 10.5% |
| CD3pos_total | 10.2% |
| CCR6_CD8RO | 10.2% |
| CD3neg_total | 10.2% |
| memory_Bcells | 9.8% |
| CD8 RO Ki67_CD8 | 9.2% |
| Bcells_total | 9.0% |
| Tconv memTIGIT_mem | 9.0% |
| NK Ki67_total | 9.0% |
| Tconv mem_Tconv | 8.8% |
| CD8 RO CCR6_CD3 | 8.2% |
| CD27_CD8RO | 8.2% |
| NKCD16_total | 8.0% |
| CD8 RO CD56_CD8 | 8.0% |
| Ki67_CD8RO | 8.0% |
| CD8 RO PD1_total | 8.0% |
| NKCD16_NK | 7.8% |
| CD8 RO intB7_CD8 | 7.5% |
| Tconv memintB7_mem | 7.5% |
| CD8 RO PD1_CD3 | 7.5% |
| Tconv memintB7_CD3 | 7.2% |
| Tconv memCXCR3_mem | 7.0% |
| CD4 Treg_total | 7.0% |
| Tconv memCXCR3_total | 6.8% |
| CD8 RO CD56_CD3 | 6.8% |
| Tconv memDR_CD3 | 6.5% |
| Treg naive_CD3 | 6.2% |
| CD16+mono_total | 6.2% |
| Tconv memCCR5_mem | 6.2% |
| CD56_CD8RO | 6.0% |
| CD8 RA naive_total | 6.0% |
| CD8 RO TIGIT_CD8 | 5.8% |
| CD8 RO PD1_CD8 | 5.8% |
| CD8 RO CCR5_total | 5.8% |
| Tconv memDR_total | 5.8% |
| Bcells memory_CD3neg | 5.5% |
| Tconv memCCR6_total | 5.5% |
| CXCR3_CD8RO | 5.2% |
| Tconv memintB7_total | 5.2% |
| Tconv memCCR4_Tconv | 5.2% |
| Tconv memKi67_Tconv | 5.0% |
| naive_Bcells | 5.0% |
| Tconv memCD27_Tconv | 5.0% |
| CD8 RO Ki67_total | 5.0% |
| Tconv memTIGIT_CD3 | 5.0% |
| Bcells naive_total | 5.0% |
| CD8 RO_CD3 | 5.0% |
| myeloid_CD3neg | 4.8% |
| CD8 RO CXCR3_total | 4.8% |
| CD8 ncytotox RO CCR4_CD8ntox | 4.8% |
| Bcells naive_CD3neg | 4.8% |
| CD8pos_total | 4.5% |
| Tconv memPD1_CD3 | 4.5% |
| CD8 RO CCR6_total | 4.2% |
| CD8 RO DR_CD3 | 4.2% |
| Tconv memCD27_total | 4.2% |
| CD8 RO intB7_CD3 | 4.0% |
| NK Ki67_CD3neg | 3.8% |
| CD8 RO CD56_total | 3.8% |
| CD14+16+mono_CD3neg | 3.8% |
| Bcells_CD3neg | 3.5% |
| Tconv memCCR5_CD3 | 3.5% |
| CD4neg_total | 3.5% |
| PD1_CD8RO | 3.5% |
| CD8 RO CD27_total | 3.2% |
| Tconv memCD56_Tconv | 3.0% |
| Tconv memCD56_mem | 3.0% |
| Tconv memDR_Tconv | 3.0% |
| nonTnonB_CD3neg | 3.0% |
| CD14+16+mono_total | 3.0% |
| Tconv memCCR5_total | 2.8% |
| Tconv memCCR5_Tconv | 2.8% |
| CD8 RO_CD8 | 2.8% |
| CD3hi_CD3 | 2.8% |
| Tconv memCCR4_total | 2.5% |
| Tconv memPD1_total | 2.5% |
| CD8 RO CCR4_total | 2.2% |
| CD8 RO TIGIT_total | 2.2% |
| Tconv memCD56_CD3 | 2.2% |
| Tconv memCD27_CD3 | 2.0% |
| CD8 RO intB7_total | 1.8% |
| CD8 RO DR_total | 1.8% |
| NK_nonTnonB | 1.5% |
| CD8 RA_CD8 | 1.5% |
| NKCD16_nonTnonB | 1.5% |
| Tconv mem_CD3 | 1.5% |
| NKCD16_CD3neg | 1.2% |
| Tconv naive_Tconv | 1.2% |
| Tconv memTIGIT_total | 1.2% |
| CD8 RO_total | 1.2% |
| CD8 RO CD27_CD8 | 1.2% |
| CD8  RO Ki67_CD3 | 1.0% |
| CD8 ncytotox RO CCR4_CD3 | 1.0% |
| NK_CD3neg | 1.0% |
| Tconv memPD1_Tconv | 1.0% |
| CD4 Tconv mem_total | 0.8% |
| Tconv memCCR4_CD3 | 0.8% |
| CD14mono_CD3neg | 0.5% |
| CD14mono_total | 0.2% |
| nonTnonB_total | 0.2% |

### ElasticNet_RFE

**Base Method**: Raw feature selection frequencies across all bootstrap samples

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD14mono_myeloid | 41.5% |
| CD27IgD_Bcells | 38.8% |
| CD16mono_myeloid | 38.0% |
| CCR4_CD8RO | 35.2% |
| CD8pos_CD3 | 34.8% |
| NKCD56hi_nonTnonB | 30.2% |
| Tconv memPD1_mem | 28.7% |
| NKCD56hi_total | 27.5% |
| CD14+16+mono_myeloid | 24.8% |
| CD4 Treg_CD4 | 24.8% |
| CD3hi_CD4neg | 24.2% |
| CD16mono_CD3neg | 22.5% |
| CD8 RA_CD3 | 22.2% |
| Tconv naive_total | 21.8% |
| CD8 RO CCR5_CD3 | 20.8% |
| Treg memory_CD4 | 20.5% |
| CD4 Tconv_total | 18.8% |
| Tconv memKi67_total | 18.8% |
| CD8 RO CCR5_CD8 | 18.5% |
| CD27negIgDneg_Bcells | 17.8% |
| Tconv memKi67_mem | 17.0% |
| Bcells CD27posIgDneg_total | 17.0% |
| Tconv memCCR6_Tconv | 16.2% |
| Treg memory_CD3 | 15.8% |
| Tconv memCCR6_mem | 15.0% |
| DR_CD8RO | 15.0% |
| CD8 RO TIGIT_CD3 | 14.8% |
| CD4 Treg _CD3 | 14.5% |
| Bcells CD27negIgDneg_total | 14.5% |
| CD8 RO CXCR3_CD3 | 14.2% |
| Bcells memory_total | 14.0% |
| CCR5_CD8RO | 13.2% |
| CD3hi_total | 13.2% |
| CD8 RA_total | 13.2% |
| CD4 Tconv_CD3 | 13.2% |
| CD8 RO CXCR3_CD8 | 13.2% |
| CD8 RA CCR7 naive_CD8 | 12.8% |
| CD8 RA naive_CD3 | 12.2% |
| Tconv memCCR6_CD3 | 12.0% |
| Tconv naive_CD3 | 11.8% |
| Bcells Ki67_total | 11.2% |
| Tconv memCD27_mem | 11.0% |
| TIGIT_CD8RO | 11.0% |
| CD4neg_CD3 | 11.0% |
| intB7_CD8RO | 10.8% |
| Treg naive_CD4 | 10.2% |
| Treg naive_total | 10.2% |
| Tconv memCXCR3_CD3 | 10.2% |
| Tconv memCXCR3_Tconv | 10.0% |
| Tconv memCCR4_mem | 10.0% |
| CD8 RO DR_CD8 | 10.0% |
| Bcells Ki67_CD3neg | 9.2% |
| Tconv memTIGIT_Tconv | 9.0% |
| NK_total | 9.0% |
| Tconv memintB7_Tconv | 9.0% |
| Ki67_Bcells | 8.8% |
| Tconv memKi67_CD3 | 8.8% |
| CD3neg_total | 8.5% |
| Tconv memCD56_total | 8.5% |
| CD3pos_total | 8.2% |
| Treg memory_total | 8.2% |
| NKCD56hi_CD3neg | 7.8% |
| CD8 RO CD27_CD3 | 7.8% |
| NK Ki67_NK | 7.5% |
| NK Ki67_nonTnonB | 7.2% |
| Tconv mem_Tconv | 7.2% |
| CD8 RO CCR6_CD8 | 7.0% |
| NKCD56hi_NK | 6.8% |
| CCR6_CD8RO | 6.8% |
| memory_Bcells | 6.8% |
| CD8 RO CCR6_CD3 | 6.8% |
| CD8 RO CD56_CD8 | 6.8% |
| CD8 RO PD1_CD3 | 6.5% |
| NK Ki67_total | 6.5% |
| Tconv memTIGIT_mem | 6.5% |
| Bcells_total | 6.2% |
| NKCD16_total | 6.0% |
| CD27_CD8RO | 6.0% |
| CD8 RO Ki67_CD8 | 6.0% |
| Ki67_CD8RO | 6.0% |
| CD8 RO PD1_total | 6.0% |
| Tconv memCXCR3_mem | 6.0% |
| Tconv memCXCR3_total | 5.8% |
| Tconv memintB7_CD3 | 5.5% |
| Tconv memDR_mem | 5.5% |
| Tconv memintB7_mem | 5.2% |
| CD8 RO CCR5_total | 5.2% |
| Tconv memCCR5_mem | 5.0% |
| CD8 RO CD56_CD3 | 5.0% |
| NKCD16_NK | 5.0% |
| Tconv memDR_total | 5.0% |
| CD8 RO_CD3 | 4.8% |
| Tconv memDR_CD3 | 4.8% |
| CD4 Treg_total | 4.5% |
| CD16+mono_total | 4.5% |
| Tconv memCCR6_total | 4.5% |
| CD56_CD8RO | 4.5% |
| Tconv memCCR4_Tconv | 4.2% |
| Tconv memCD27_total | 4.0% |
| CD8 RO intB7_CD8 | 4.0% |
| naive_Bcells | 4.0% |
| CD8 RO DR_CD3 | 3.8% |
| CD8 RA naive_total | 3.8% |
| Tconv memCD27_Tconv | 3.8% |
| CD8 RO Ki67_total | 3.8% |
| CD8pos_total | 3.8% |
| CD8 RO PD1_CD8 | 3.8% |
| CD8 RO CXCR3_total | 3.8% |
| Tconv memintB7_total | 3.8% |
| myeloid_CD3neg | 3.8% |
| CXCR3_CD8RO | 3.5% |
| CD8 RO TIGIT_CD8 | 3.5% |
| Tconv memPD1_CD3 | 3.5% |
| CD8 ncytotox RO CCR4_CD8ntox | 3.2% |
| Bcells naive_CD3neg | 3.2% |
| Treg naive_CD3 | 3.2% |
| Tconv memTIGIT_CD3 | 3.0% |
| Bcells memory_CD3neg | 3.0% |
| CD8 RO CD56_total | 2.8% |
| Bcells_CD3neg | 2.8% |
| Tconv memCCR5_CD3 | 2.5% |
| Bcells naive_total | 2.5% |
| Tconv memPD1_total | 2.5% |
| Tconv memCCR5_Tconv | 2.5% |
| Tconv memKi67_Tconv | 2.5% |
| CD8 RO CCR6_total | 2.5% |
| Tconv memCCR4_total | 2.2% |
| Tconv memCCR5_total | 2.2% |
| CD8 RO intB7_CD3 | 2.2% |
| PD1_CD8RO | 2.0% |
| nonTnonB_CD3neg | 2.0% |
| CD14+16+mono_total | 1.8% |
| Tconv memCD27_CD3 | 1.8% |
| Tconv memCD56_Tconv | 1.8% |
| NK Ki67_CD3neg | 1.8% |
| CD4neg_total | 1.8% |
| CD8 RO CD27_total | 1.8% |
| CD14+16+mono_CD3neg | 1.8% |
| CD8 RO TIGIT_total | 1.5% |
| Tconv memDR_Tconv | 1.5% |
| CD8 RO CCR4_total | 1.2% |
| NK_nonTnonB | 1.2% |
| Tconv mem_CD3 | 1.2% |
| CD3hi_CD3 | 1.2% |
| Tconv memCD56_CD3 | 1.2% |
| NKCD16_CD3neg | 1.2% |
| CD8 RO_CD8 | 1.2% |
| CD8 RO DR_total | 1.2% |
| CD8 RO intB7_total | 1.0% |
| CD8 RO_total | 1.0% |
| Tconv naive_Tconv | 1.0% |
| NKCD16_nonTnonB | 1.0% |
| CD8 ncytotox RO CCR4_CD3 | 1.0% |
| CD4 Tconv mem_total | 0.8% |
| Tconv memCD56_mem | 0.8% |
| Tconv memCCR4_CD3 | 0.8% |
| CD8 RA_CD8 | 0.8% |
| NK_CD3neg | 0.8% |
| CD14mono_CD3neg | 0.5% |
| Tconv memTIGIT_total | 0.5% |
| CD8  RO Ki67_CD3 | 0.5% |
| Tconv memPD1_Tconv | 0.5% |
| CD8 RO CD27_CD8 | 0.5% |
| CD14mono_total | 0.2% |
| nonTnonB_total | 0.2% |

### ElasticNet_Strict

**Base Method**: Raw feature selection frequencies across all bootstrap samples

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CCR4_CD8RO | 27.0% |
| CD14mono_myeloid | 25.8% |
| CD27IgD_Bcells | 24.8% |
| CD16mono_myeloid | 22.8% |
| NKCD56hi_nonTnonB | 20.2% |
| Tconv memPD1_mem | 18.8% |
| CD8pos_CD3 | 18.5% |
| CD14+16+mono_myeloid | 17.2% |
| CD3hi_CD4neg | 17.0% |
| Tconv memKi67_total | 13.8% |
| NKCD56hi_total | 12.5% |
| CD4 Treg_CD4 | 12.0% |
| Tconv memKi67_mem | 12.0% |
| CD8 RO CCR5_CD3 | 11.5% |
| CD8 RO CCR5_CD8 | 11.2% |
| DR_CD8RO | 11.2% |
| Bcells CD27negIgDneg_total | 10.5% |
| CD8 RA_CD3 | 10.5% |
| CD16mono_CD3neg | 10.2% |
| Tconv naive_total | 9.8% |
| CD8 RO TIGIT_CD3 | 9.8% |
| CD8 RA_total | 9.2% |
| Tconv memCCR6_CD3 | 8.5% |
| Tconv memCCR6_mem | 8.2% |
| CD4 Tconv_total | 8.2% |
| Tconv memCCR6_Tconv | 7.5% |
| Treg memory_CD4 | 7.2% |
| CD8 RO CXCR3_CD8 | 7.2% |
| CD8 RA CCR7 naive_CD8 | 7.2% |
| Treg memory_CD3 | 7.0% |
| CD8 RO CXCR3_CD3 | 6.8% |
| CD27negIgDneg_Bcells | 6.8% |
| Bcells Ki67_CD3neg | 6.8% |
| Treg naive_CD4 | 6.8% |
| CCR5_CD8RO | 6.8% |
| CD8 RO DR_CD8 | 6.5% |
| Bcells CD27posIgDneg_total | 6.2% |
| Bcells memory_total | 6.2% |
| Bcells Ki67_total | 6.2% |
| Tconv naive_CD3 | 5.8% |
| TIGIT_CD8RO | 5.5% |
| intB7_CD8RO | 5.2% |
| Tconv memKi67_CD3 | 5.2% |
| CD4 Tconv_CD3 | 5.2% |
| Tconv memDR_mem | 5.0% |
| CD8 RA naive_CD3 | 5.0% |
| Tconv memintB7_Tconv | 5.0% |
| CD3hi_total | 5.0% |
| Treg memory_total | 5.0% |
| CD4 Treg _CD3 | 5.0% |
| Ki67_Bcells | 5.0% |
| Tconv memCD27_mem | 4.8% |
| Tconv memCXCR3_Tconv | 4.8% |
| CD8 RO CD27_CD3 | 4.5% |
| Tconv memTIGIT_Tconv | 4.5% |
| CD4neg_CD3 | 4.5% |
| Tconv memCXCR3_CD3 | 4.2% |
| CD8 RO CCR6_CD8 | 4.2% |
| NKCD56hi_NK | 4.2% |
| Tconv memCCR4_mem | 4.0% |
| Treg naive_total | 4.0% |
| NK Ki67_nonTnonB | 4.0% |
| CD8 RO intB7_CD8 | 3.8% |
| Tconv memTIGIT_mem | 3.8% |
| Tconv memCD56_total | 3.2% |
| CD8 RO CCR6_CD3 | 3.2% |
| Tconv memCXCR3_mem | 3.0% |
| CD27_CD8RO | 3.0% |
| CCR6_CD8RO | 3.0% |
| Bcells_total | 2.8% |
| Tconv memDR_CD3 | 2.8% |
| Tconv memDR_total | 2.8% |
| Tconv memCXCR3_total | 2.8% |
| memory_Bcells | 2.8% |
| Tconv memCCR5_mem | 2.5% |
| NK_total | 2.5% |
| Tconv memintB7_mem | 2.5% |
| CD8 RO CD56_CD8 | 2.5% |
| CD56_CD8RO | 2.5% |
| NKCD56hi_CD3neg | 2.5% |
| CD8 RO CCR5_total | 2.5% |
| Ki67_CD8RO | 2.5% |
| NK Ki67_total | 2.2% |
| CXCR3_CD8RO | 2.2% |
| Tconv memCCR5_CD3 | 2.2% |
| CD8 RO PD1_CD3 | 2.2% |
| CD8 RA naive_total | 2.0% |
| CD8 RO Ki67_CD8 | 2.0% |
| CD4 Treg_total | 2.0% |
| CD8 RO PD1_total | 2.0% |
| NK Ki67_NK | 2.0% |
| NKCD16_NK | 2.0% |
| CD8 RO DR_CD3 | 2.0% |
| CD8 RO Ki67_total | 1.8% |
| CD3pos_total | 1.8% |
| CD8 ncytotox RO CCR4_CD8ntox | 1.8% |
| Treg naive_CD3 | 1.8% |
| CD8 RO intB7_CD3 | 1.5% |
| Tconv mem_Tconv | 1.5% |
| Tconv memKi67_Tconv | 1.5% |
| CD8 RO TIGIT_CD8 | 1.5% |
| CD8 RO PD1_CD8 | 1.5% |
| Tconv memCCR4_Tconv | 1.5% |
| Tconv memCD27_Tconv | 1.5% |
| CD3neg_total | 1.5% |
| Tconv memintB7_CD3 | 1.5% |
| Tconv memCCR6_total | 1.2% |
| myeloid_CD3neg | 1.2% |
| Bcells naive_CD3neg | 1.2% |
| Tconv memCCR4_total | 1.0% |
| CD16+mono_total | 1.0% |
| Tconv memPD1_CD3 | 1.0% |
| Tconv memDR_Tconv | 1.0% |
| Bcells naive_total | 1.0% |
| Tconv memTIGIT_CD3 | 1.0% |
| CD8pos_total | 1.0% |
| CD8 RO CCR4_total | 1.0% |
| CD8 RO CXCR3_total | 1.0% |
| Bcells memory_CD3neg | 1.0% |
| NKCD16_total | 1.0% |
| CD8 RO CD56_CD3 | 1.0% |
| Tconv memCD27_total | 1.0% |
| CD14+16+mono_CD3neg | 1.0% |
| CD14+16+mono_total | 1.0% |
| Tconv memintB7_total | 1.0% |
| nonTnonB_CD3neg | 0.8% |
| Tconv memCCR5_total | 0.8% |
| CD4neg_total | 0.8% |
| naive_Bcells | 0.8% |
| CD3hi_CD3 | 0.8% |
| CD8 RO CD56_total | 0.8% |
| CD8 RO_CD8 | 0.5% |
| Tconv memPD1_total | 0.5% |
| PD1_CD8RO | 0.5% |
| CD8 RO CCR6_total | 0.5% |
| CD8  RO Ki67_CD3 | 0.5% |
| Tconv memCCR5_Tconv | 0.5% |
| CD8 RO CD27_CD8 | 0.5% |
| NK Ki67_CD3neg | 0.5% |
| CD8 RO_CD3 | 0.5% |
| CD4 Tconv mem_total | 0.2% |
| CD14mono_CD3neg | 0.2% |
| NK_nonTnonB | 0.2% |
| CD8 RA_CD8 | 0.2% |
| CD8 RO intB7_total | 0.2% |
| CD8 RO TIGIT_total | 0.2% |
| Tconv mem_CD3 | 0.2% |
| Bcells_CD3neg | 0.2% |
| Tconv memCD56_Tconv | 0.2% |
| CD8 RO_total | 0.2% |
| Tconv memTIGIT_total | 0.2% |
| Tconv memCCR4_CD3 | 0.2% |
| NKCD16_nonTnonB | 0.2% |
| CD8 RO CD27_total | 0.2% |

### FDR (p < 0.01)

**Base Method**: Raw feature selection frequencies across all bootstrap samples

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD8 RO CCR5_CD3 | 29.0% |
| CD4 Treg_CD4 | 28.7% |
| Tconv naive_total | 27.8% |
| CD8pos_CD3 | 26.0% |
| Treg memory_CD4 | 25.5% |
| CD4 Tconv_CD3 | 20.8% |
| CD8 RO CXCR3_CD3 | 18.2% |
| CD8 RO CCR5_total | 16.0% |
| Bcells CD27posIgDneg_total | 15.8% |
| CD4 Tconv_total | 15.8% |
| Tconv naive_CD3 | 15.2% |
| CD8 RO CCR5_CD8 | 14.5% |
| Tconv memCCR5_Tconv | 14.0% |
| CD4 Treg _CD3 | 12.5% |
| CD27IgD_Bcells | 12.2% |
| Tconv memCXCR3_Tconv | 12.2% |
| Treg memory_CD3 | 12.0% |
| CD16mono_myeloid | 11.5% |
| CD8 RO_CD3 | 11.5% |
| CD16mono_CD3neg | 11.0% |
| CD8 RO DR_CD3 | 10.5% |
| Tconv mem_Tconv | 10.0% |
| Tconv memCCR5_mem | 10.0% |
| CD8 RA_CD3 | 10.0% |
| CD8 RO CD56_CD3 | 10.0% |
| Tconv naive_Tconv | 9.5% |
| CD14mono_myeloid | 9.2% |
| Tconv memCCR5_CD3 | 8.8% |
| CD8 RO CD27_CD3 | 8.5% |
| CD4neg_CD3 | 8.5% |
| CCR5_CD8RO | 7.5% |
| Tconv memCCR6_Tconv | 7.5% |
| CD8 RO CCR6_CD3 | 7.5% |
| CD8 RO TIGIT_CD3 | 7.0% |
| Tconv memCXCR3_CD3 | 5.8% |
| CD3pos_total | 5.0% |
| CD3neg_total | 5.0% |
| Tconv memintB7_Tconv | 5.0% |
| Tconv memCD27_Tconv | 4.8% |
| Tconv memCXCR3_mem | 4.5% |
| Tconv memKi67_total | 4.5% |
| CD8 RO CXCR3_CD8 | 4.5% |
| CD8 RO intB7_CD3 | 4.0% |
| Tconv memCCR4_Tconv | 4.0% |
| CD8 RO CD56_total | 3.8% |
| CD16+mono_total | 3.5% |
| CD8 RO CXCR3_total | 3.5% |
| CD8pos_total | 3.2% |
| CXCR3_CD8RO | 3.0% |
| CD8 RO PD1_CD3 | 3.0% |
| NKCD56hi_total | 2.5% |
| Tconv memDR_Tconv | 2.5% |
| CD8  RO Ki67_CD3 | 2.5% |
| CCR4_CD8RO | 2.2% |
| CD14mono_total | 2.2% |
| Tconv memCD27_mem | 2.0% |
| CD8 RO DR_total | 2.0% |
| Tconv memCCR5_total | 2.0% |
| Tconv memTIGIT_Tconv | 2.0% |
| nonTnonB_total | 1.8% |
| Tconv memCCR6_CD3 | 1.8% |
| Tconv memCCR6_mem | 1.8% |
| Tconv memKi67_mem | 1.5% |
| CD8 RO CD56_CD8 | 1.5% |
| CD27negIgDneg_Bcells | 1.5% |
| Treg memory_total | 1.5% |
| Tconv memCD56_Tconv | 1.5% |
| Tconv memCCR4_mem | 1.2% |
| Tconv memCD27_total | 1.2% |
| NKCD56hi_nonTnonB | 1.2% |
| CD4neg_total | 1.2% |
| Tconv memPD1_total | 1.2% |
| Bcells memory_CD3neg | 1.2% |
| NKCD56hi_CD3neg | 1.0% |
| Tconv memPD1_mem | 1.0% |
| NK Ki67_total | 1.0% |
| CD8 RO CCR6_total | 1.0% |
| Tconv memCCR4_total | 1.0% |
| CD8 RO DR_CD8 | 1.0% |
| Tconv memintB7_CD3 | 1.0% |
| CD8 RO TIGIT_total | 1.0% |
| CD4 Treg_total | 1.0% |
| Tconv memPD1_Tconv | 1.0% |
| Tconv memCXCR3_total | 1.0% |
| Treg naive_CD4 | 0.8% |
| CD8 RO intB7_total | 0.8% |
| CD8 RO CD27_total | 0.8% |
| CD8 RO_total | 0.8% |
| CD8 RA naive_CD3 | 0.8% |
| CD8 ncytotox RO CCR4_CD3 | 0.8% |
| Treg naive_CD3 | 0.8% |
| Bcells memory_total | 0.8% |
| CD8 RA_total | 0.8% |
| CD8 RO_CD8 | 0.5% |
| NK Ki67_NK | 0.5% |
| myeloid_total | 0.5% |
| Tconv memKi67_CD3 | 0.5% |
| Tconv memTIGIT_total | 0.5% |
| Bcells Ki67_CD3neg | 0.5% |
| CD8 RA_CD8 | 0.5% |
| CD8 RO Ki67_total | 0.2% |
| CD3hi_CD3 | 0.2% |
| Bcells_CD3neg | 0.2% |
| CD56_CD8RO | 0.2% |
| Tconv memDR_CD3 | 0.2% |
| CD8 RO CCR4_total | 0.2% |
| NK Ki67_nonTnonB | 0.2% |
| NKCD56hi_NK | 0.2% |
| Tconv memDR_total | 0.2% |
| Ki67_Bcells | 0.2% |
| CD8 RO CCR6_CD8 | 0.2% |
| CD8 RO PD1_total | 0.2% |
| CD8 RA CCR7 naive_CD8 | 0.2% |
| nonTnonB_CD3neg | 0.2% |
| CD14+16+mono_myeloid | 0.2% |
| PD1_CD8RO | 0.2% |
| Ki67_CD8RO | 0.2% |
| CD8 RO TIGIT_CD8 | 0.2% |
| CD27_CD8RO | 0.2% |
| CD8 RO PD1_CD8 | 0.2% |
| Tconv memintB7_total | 0.2% |
| Tconv memPD1_CD3 | 0.2% |
| Tconv memintB7_mem | 0.2% |
| intB7_CD8RO | 0.2% |
| CD14+16+mono_CD3neg | 0.2% |
| CD8 RO intB7_CD8 | 0.2% |
| Tconv memKi67_Tconv | 0.2% |
| Tconv mem_CD3 | 0.2% |
| CD3hi_CD4neg | 0.2% |
| CD4 Tconv mem_total | 0.2% |
| NK_total | 0.2% |
| NKCD16_total | 0.2% |
| NK_CD3neg | 0.2% |
| NKCD16_CD3neg | 0.2% |
| NK_nonTnonB | 0.2% |
| NKCD16_nonTnonB | 0.2% |
| Tconv memCCR6_total | 0.2% |

### FDR (p < 0.05)

**Base Method**: Raw feature selection frequencies across all bootstrap samples

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Tconv naive_total | 58.2% |
| CD4 Treg_CD4 | 58.0% |
| CD8 RO CCR5_CD3 | 55.2% |
| Treg memory_CD4 | 54.5% |
| CD8pos_CD3 | 47.8% |
| CD4 Tconv_CD3 | 46.0% |
| CD4 Tconv_total | 42.8% |
| Bcells CD27posIgDneg_total | 41.5% |
| Tconv naive_CD3 | 40.8% |
| CD8 RO CXCR3_CD3 | 40.0% |
| CD27IgD_Bcells | 38.5% |
| CD8 RO CCR5_total | 34.5% |
| Tconv memCCR5_Tconv | 33.0% |
| CD8 RO CCR5_CD8 | 33.0% |
| CD16mono_myeloid | 32.0% |
| CD8 RO_CD3 | 32.0% |
| Tconv memCXCR3_Tconv | 31.2% |
| Treg memory_CD3 | 31.0% |
| CD8 RO CD56_CD3 | 30.8% |
| CD8 RO DR_CD3 | 30.2% |
| Tconv mem_Tconv | 30.0% |
| CD16mono_CD3neg | 30.0% |
| Tconv naive_Tconv | 29.8% |
| CD4 Treg _CD3 | 29.2% |
| CD4neg_CD3 | 28.7% |
| CD8 RA_CD3 | 27.5% |
| Tconv memCCR5_mem | 26.8% |
| CD14mono_myeloid | 26.8% |
| CD8 RO CCR6_CD3 | 25.0% |
| Tconv memCCR6_Tconv | 23.5% |
| CD8 RO CD27_CD3 | 23.2% |
| Tconv memCXCR3_CD3 | 22.0% |
| CD8 RO TIGIT_CD3 | 21.5% |
| CCR5_CD8RO | 21.5% |
| Tconv memCCR5_CD3 | 21.0% |
| Tconv memCXCR3_mem | 19.8% |
| CD8 RO intB7_CD3 | 19.2% |
| CD3pos_total | 19.0% |
| CD3neg_total | 19.0% |
| Tconv memintB7_Tconv | 17.5% |
| CD8 RO CXCR3_total | 17.2% |
| Tconv memCD27_Tconv | 16.0% |
| CD8 RO CXCR3_CD8 | 15.8% |
| Tconv memCCR4_Tconv | 15.0% |
| CCR4_CD8RO | 14.0% |
| Tconv memKi67_total | 14.0% |
| Tconv memCD27_mem | 13.8% |
| NKCD56hi_total | 13.2% |
| CD8 RO CD56_total | 13.0% |
| CXCR3_CD8RO | 12.8% |
| CD27negIgDneg_Bcells | 11.0% |
| CD8 RO PD1_CD3 | 10.0% |
| CD8  RO Ki67_CD3 | 10.0% |
| Tconv memCCR6_CD3 | 9.5% |
| CD16+mono_total | 9.5% |
| Bcells memory_CD3neg | 9.2% |
| CD8pos_total | 8.8% |
| CD8 RO DR_total | 8.8% |
| Tconv memTIGIT_Tconv | 8.2% |
| Tconv memCD56_Tconv | 8.2% |
| nonTnonB_total | 8.0% |
| NKCD56hi_CD3neg | 8.0% |
| NKCD56hi_nonTnonB | 7.8% |
| Tconv memPD1_total | 7.8% |
| Tconv memCCR4_mem | 7.5% |
| Tconv memDR_Tconv | 7.5% |
| Tconv memCD27_total | 7.2% |
| NK Ki67_total | 7.2% |
| Tconv memCCR5_total | 7.0% |
| CD8 ncytotox RO CCR4_CD3 | 7.0% |
| Tconv memPD1_mem | 7.0% |
| CD8 RO CD56_CD8 | 6.8% |
| Tconv memCXCR3_total | 6.5% |
| CD8 RO_total | 6.5% |
| CD8 RO CCR6_total | 6.5% |
| Treg naive_CD4 | 6.5% |
| CD8 RO CD27_total | 6.2% |
| Treg memory_total | 6.2% |
| CD14mono_total | 6.0% |
| Tconv memKi67_mem | 5.8% |
| CD8 RO TIGIT_total | 5.5% |
| Tconv memCCR4_total | 5.5% |
| CD8 RA_total | 5.2% |
| Tconv memintB7_CD3 | 5.2% |
| CD4neg_total | 5.2% |
| Tconv memCCR6_mem | 5.0% |
| CD8 RO DR_CD8 | 4.8% |
| Bcells CD27negIgDneg_total | 4.8% |
| CD4 Treg_total | 4.5% |
| NK Ki67_NK | 4.5% |
| Ki67_CD8RO | 4.2% |
| CD8 RA naive_CD3 | 4.0% |
| Tconv memKi67_Tconv | 4.0% |
| CD8 RO intB7_total | 4.0% |
| Treg naive_CD3 | 4.0% |
| CD27_CD8RO | 4.0% |
| CD8 RA CCR7 naive_CD8 | 4.0% |
| CD56_CD8RO | 4.0% |
| CD8 RO Ki67_CD8 | 3.8% |
| Tconv mem_CD3 | 3.8% |
| Tconv memTIGIT_total | 3.5% |
| Bcells memory_total | 3.5% |
| Tconv memCD56_CD3 | 3.5% |
| CD8 RO PD1_total | 3.5% |
| Tconv memintB7_mem | 3.2% |
| nonTnonB_CD3neg | 3.0% |
| Bcells_CD3neg | 3.0% |
| CD14mono_CD3neg | 3.0% |
| CD3hi_CD3 | 3.0% |
| Tconv memDR_total | 2.8% |
| CD8 RO Ki67_total | 2.8% |
| myeloid_CD3neg | 2.8% |
| NK Ki67_nonTnonB | 2.8% |
| CD8 RO CCR6_CD8 | 2.8% |
| CD8 RO CCR4_total | 2.8% |
| CD8 RO TIGIT_CD8 | 2.8% |
| CD8 RO PD1_CD8 | 2.5% |
| myeloid_total | 2.5% |
| CD14+16+mono_total | 2.5% |
| CD3hi_CD4neg | 2.5% |
| PD1_CD8RO | 2.5% |
| Tconv memDR_CD3 | 2.5% |
| Tconv memKi67_CD3 | 2.2% |
| Tconv memPD1_Tconv | 2.2% |
| Tconv memTIGIT_mem | 2.2% |
| Tconv memCD56_mem | 2.2% |
| CD8 RO_CD8 | 2.0% |
| CD4 Tconv mem_total | 2.0% |
| Bcells Ki67_CD3neg | 2.0% |
| naive_Bcells | 2.0% |
| Tconv memCCR4_CD3 | 2.0% |
| CD14+16+mono_myeloid | 1.8% |
| Bcells Ki67_total | 1.8% |
| Tconv memDR_mem | 1.8% |
| TIGIT_CD8RO | 1.8% |
| Treg naive_total | 1.8% |
| Tconv memCCR6_total | 1.8% |
| DR_CD8RO | 1.8% |
| NKCD16_nonTnonB | 1.8% |
| Ki67_Bcells | 1.8% |
| CD8 RA_CD8 | 1.8% |
| Tconv memPD1_CD3 | 1.5% |
| NK_total | 1.5% |
| Tconv memTIGIT_CD3 | 1.5% |
| NKCD56hi_NK | 1.5% |
| NKCD16_NK | 1.5% |
| NK Ki67_CD3neg | 1.5% |
| NK_nonTnonB | 1.5% |
| NKCD16_total | 1.5% |
| CD8 RO intB7_CD8 | 1.5% |
| CD3hi_total | 1.5% |
| CD8 ncytotox RO CCR4_CD8ntox | 1.2% |
| Tconv memintB7_total | 1.2% |
| Tconv memCD27_CD3 | 1.2% |
| CD14+16+mono_CD3neg | 1.2% |
| Tconv memCD56_total | 1.0% |
| NKCD16_CD3neg | 1.0% |
| NK_CD3neg | 1.0% |
| CD8 RA naive_total | 1.0% |
| CD8 RO CD27_CD8 | 1.0% |
| intB7_CD8RO | 1.0% |
| CCR6_CD8RO | 0.8% |
| Bcells_total | 0.8% |
| Bcells naive_CD3neg | 0.8% |
| memory_Bcells | 0.8% |
| Bcells naive_total | 0.2% |

### FDR (p < 0.1)

**Base Method**: Raw feature selection frequencies across all bootstrap samples

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD4 Treg_CD4 | 73.5% |
| Tconv naive_total | 73.0% |
| CD8 RO CCR5_CD3 | 72.8% |
| Treg memory_CD4 | 69.0% |
| CD8pos_CD3 | 65.5% |
| CD4 Tconv_total | 61.3% |
| CD4 Tconv_CD3 | 61.3% |
| CD8 RO CXCR3_CD3 | 59.2% |
| Bcells CD27posIgDneg_total | 58.5% |
| CD27IgD_Bcells | 58.0% |
| Tconv naive_CD3 | 51.0% |
| CD8 RO CCR5_total | 48.5% |
| CD8 RO CD56_CD3 | 48.2% |
| Treg memory_CD3 | 46.8% |
| Tconv memCCR5_Tconv | 46.0% |
| CD16mono_myeloid | 46.0% |
| Tconv mem_Tconv | 45.2% |
| Tconv memCXCR3_Tconv | 45.2% |
| CD8 RO DR_CD3 | 45.0% |
| CD8 RO_CD3 | 44.8% |
| CD8 RO CCR5_CD8 | 44.2% |
| CD16mono_CD3neg | 44.0% |
| Tconv naive_Tconv | 43.8% |
| CD4neg_CD3 | 43.0% |
| CD14mono_myeloid | 43.0% |
| CD4 Treg _CD3 | 42.5% |
| CD8 RA_CD3 | 40.8% |
| Tconv memCCR5_mem | 40.2% |
| Tconv memCCR6_Tconv | 38.5% |
| CD8 RO CCR6_CD3 | 37.8% |
| CD8 RO CD27_CD3 | 35.2% |
| Tconv memCCR5_CD3 | 34.8% |
| CCR5_CD8RO | 33.2% |
| Tconv memCXCR3_CD3 | 31.0% |
| CD3pos_total | 31.0% |
| Tconv memCXCR3_mem | 31.0% |
| CD8 RO TIGIT_CD3 | 31.0% |
| CD3neg_total | 31.0% |
| CD8 RO intB7_CD3 | 29.5% |
| Tconv memKi67_total | 26.8% |
| CD8 RO CXCR3_total | 26.0% |
| Tconv memCD27_Tconv | 25.8% |
| Tconv memCD27_mem | 24.8% |
| Tconv memintB7_Tconv | 24.8% |
| CD8 RO CXCR3_CD8 | 24.2% |
| Tconv memCCR4_Tconv | 23.0% |
| CCR4_CD8RO | 23.0% |
| NKCD56hi_total | 22.8% |
| CD8 RO CD56_total | 21.8% |
| CXCR3_CD8RO | 21.8% |
| CD27negIgDneg_Bcells | 18.5% |
| CD8  RO Ki67_CD3 | 18.5% |
| CD8 RO PD1_CD3 | 18.2% |
| Tconv memPD1_total | 17.8% |
| CD16+mono_total | 16.5% |
| Bcells memory_CD3neg | 16.5% |
| Tconv memCCR6_CD3 | 16.5% |
| Tconv memCD56_Tconv | 16.5% |
| Tconv memCD27_total | 16.2% |
| CD8 RO DR_total | 15.5% |
| Tconv memCCR4_total | 15.2% |
| Tconv memCCR4_mem | 15.0% |
| NKCD56hi_nonTnonB | 15.0% |
| nonTnonB_total | 14.8% |
| Tconv memTIGIT_Tconv | 14.2% |
| CD8 RO CD56_CD8 | 14.2% |
| Treg naive_CD4 | 14.0% |
| Tconv memPD1_mem | 14.0% |
| CD14mono_total | 14.0% |
| Tconv memCCR5_total | 13.8% |
| Tconv memDR_Tconv | 13.8% |
| Tconv memCXCR3_total | 13.0% |
| NKCD56hi_CD3neg | 13.0% |
| CD8 RO CCR6_total | 12.5% |
| Tconv memKi67_mem | 12.2% |
| CD8pos_total | 12.2% |
| CD8 RO_total | 12.0% |
| CD8 RO CD27_total | 11.8% |
| CD8 RO TIGIT_total | 11.5% |
| NK Ki67_total | 11.5% |
| Tconv memCCR6_mem | 10.8% |
| CD8 RA_total | 10.8% |
| Tconv memintB7_CD3 | 10.8% |
| CD8 ncytotox RO CCR4_CD3 | 10.2% |
| CD8 RO DR_CD8 | 9.8% |
| Treg memory_total | 9.5% |
| Bcells_CD3neg | 9.5% |
| CD27_CD8RO | 9.5% |
| nonTnonB_CD3neg | 9.5% |
| Treg naive_CD3 | 9.2% |
| Bcells CD27negIgDneg_total | 9.0% |
| Tconv memDR_total | 9.0% |
| CD4neg_total | 9.0% |
| NK Ki67_NK | 8.8% |
| Tconv memTIGIT_total | 8.5% |
| CD8 RA naive_CD3 | 8.2% |
| Tconv memKi67_Tconv | 8.2% |
| Tconv memintB7_mem | 8.2% |
| Tconv mem_CD3 | 8.2% |
| Tconv memCD56_CD3 | 8.0% |
| CD8 RA CCR7 naive_CD8 | 8.0% |
| CD8 RO intB7_total | 7.5% |
| CD56_CD8RO | 7.5% |
| CD4 Treg_total | 7.5% |
| Ki67_CD8RO | 7.0% |
| CD3hi_CD3 | 7.0% |
| CD14+16+mono_total | 6.8% |
| CD8 RO CCR6_CD8 | 6.8% |
| CD4 Tconv mem_total | 6.5% |
| CD8 RO Ki67_CD8 | 6.5% |
| Bcells memory_total | 6.2% |
| CD8 RO PD1_total | 6.2% |
| Tconv memCD56_total | 6.0% |
| CD8 RO_CD8 | 6.0% |
| myeloid_CD3neg | 6.0% |
| myeloid_total | 5.8% |
| Tconv memTIGIT_mem | 5.8% |
| Tconv memKi67_CD3 | 5.8% |
| CD8 ncytotox RO CCR4_CD8ntox | 5.5% |
| CD8 RA_CD8 | 5.5% |
| CD8 RO TIGIT_CD8 | 5.5% |
| CD14+16+mono_myeloid | 5.5% |
| CD3hi_CD4neg | 5.5% |
| NK Ki67_nonTnonB | 5.5% |
| PD1_CD8RO | 5.5% |
| Ki67_Bcells | 5.2% |
| CD14mono_CD3neg | 5.2% |
| NKCD56hi_NK | 5.2% |
| Treg naive_total | 5.2% |
| NK Ki67_CD3neg | 5.0% |
| NK_total | 5.0% |
| CD8 RO Ki67_total | 5.0% |
| CD8 RO CCR4_total | 5.0% |
| Tconv memDR_mem | 4.8% |
| CD8 RO PD1_CD8 | 4.8% |
| NKCD16_total | 4.8% |
| naive_Bcells | 4.8% |
| Tconv memCD56_mem | 4.8% |
| Tconv memDR_CD3 | 4.5% |
| Tconv memCCR4_CD3 | 4.2% |
| CD8 RO intB7_CD8 | 4.2% |
| Bcells Ki67_CD3neg | 4.0% |
| DR_CD8RO | 4.0% |
| Tconv memPD1_Tconv | 4.0% |
| TIGIT_CD8RO | 4.0% |
| Bcells Ki67_total | 3.8% |
| NK_nonTnonB | 3.8% |
| NKCD16_nonTnonB | 3.5% |
| Tconv memPD1_CD3 | 3.5% |
| Tconv memCCR6_total | 3.5% |
| Tconv memTIGIT_CD3 | 3.2% |
| NKCD16_NK | 3.0% |
| Tconv memCD27_CD3 | 3.0% |
| Bcells naive_CD3neg | 3.0% |
| CD3hi_total | 3.0% |
| Bcells_total | 2.8% |
| CD8 RA naive_total | 2.8% |
| CD14+16+mono_CD3neg | 2.8% |
| CD8 RO CD27_CD8 | 2.8% |
| CCR6_CD8RO | 2.5% |
| Tconv memintB7_total | 2.5% |
| NKCD16_CD3neg | 2.0% |
| NK_CD3neg | 2.0% |
| intB7_CD8RO | 2.0% |
| memory_Bcells | 1.5% |
| Bcells naive_total | 1.5% |

### LASSO_Lenient

**Base Method**: Raw feature selection frequencies across all bootstrap samples

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD14mono_myeloid | 40.8% |
| CD27IgD_Bcells | 39.0% |
| CCR4_CD8RO | 37.8% |
| CD16mono_myeloid | 35.2% |
| NKCD56hi_nonTnonB | 32.5% |
| Tconv memPD1_mem | 32.0% |
| CD3hi_CD4neg | 30.2% |
| CD8pos_CD3 | 28.7% |
| CD14+16+mono_myeloid | 28.0% |
| NKCD56hi_total | 26.8% |
| CD8 RA_CD3 | 21.8% |
| Bcells CD27negIgDneg_total | 20.8% |
| DR_CD8RO | 19.8% |
| CD27negIgDneg_Bcells | 19.5% |
| Tconv memKi67_total | 19.2% |
| CD16mono_CD3neg | 19.2% |
| CD8 RO CCR5_CD3 | 19.0% |
| CD4 Treg_CD4 | 17.8% |
| CD8 RO CCR5_CD8 | 17.5% |
| Tconv memCCR6_mem | 17.5% |
| Tconv memKi67_mem | 17.2% |
| Tconv naive_total | 16.8% |
| Bcells memory_total | 16.0% |
| CD4 Tconv_total | 16.0% |
| CD8 RO TIGIT_CD3 | 16.0% |
| Treg naive_total | 15.5% |
| Bcells CD27posIgDneg_total | 15.2% |
| CD8 RA CCR7 naive_CD8 | 14.5% |
| Tconv memCCR6_Tconv | 14.5% |
| Bcells Ki67_total | 14.2% |
| CD8 RA_total | 14.2% |
| Tconv memCD27_mem | 13.5% |
| CD3hi_total | 13.5% |
| Treg naive_CD4 | 13.2% |
| Bcells Ki67_CD3neg | 13.0% |
| Tconv memCCR6_CD3 | 13.0% |
| Ki67_Bcells | 12.8% |
| CD8 RO CXCR3_CD8 | 12.5% |
| CCR5_CD8RO | 12.2% |
| TIGIT_CD8RO | 12.2% |
| intB7_CD8RO | 11.8% |
| CD8 RO CXCR3_CD3 | 11.8% |
| NK_total | 11.5% |
| CD8 RA naive_CD3 | 11.5% |
| Tconv naive_CD3 | 11.0% |
| CD4 Tconv_CD3 | 10.5% |
| Treg memory_total | 10.5% |
| Treg memory_CD3 | 10.5% |
| Tconv memTIGIT_Tconv | 10.5% |
| Tconv memintB7_Tconv | 10.2% |
| CD8 RO DR_CD8 | 10.2% |
| Tconv memCCR4_mem | 10.0% |
| CD4neg_CD3 | 10.0% |
| Tconv memCD56_total | 10.0% |
| Tconv memCXCR3_Tconv | 9.8% |
| Treg memory_CD4 | 9.5% |
| NK Ki67_nonTnonB | 9.2% |
| CD8 RO CCR6_CD8 | 9.2% |
| Tconv memDR_mem | 9.2% |
| NK Ki67_NK | 8.8% |
| NKCD56hi_NK | 8.8% |
| CD8 RO CD27_CD3 | 8.5% |
| Tconv memKi67_CD3 | 8.2% |
| CD3pos_total | 8.0% |
| Tconv memTIGIT_mem | 7.5% |
| memory_Bcells | 7.5% |
| Tconv memCXCR3_CD3 | 7.5% |
| CD4 Treg _CD3 | 7.5% |
| Bcells_total | 7.2% |
| CD3neg_total | 7.0% |
| CCR6_CD8RO | 7.0% |
| CD27_CD8RO | 6.8% |
| CD8 RO intB7_CD8 | 6.8% |
| CD8 RO CCR6_CD3 | 6.8% |
| NKCD16_NK | 6.8% |
| Ki67_CD8RO | 6.2% |
| Tconv memintB7_mem | 6.0% |
| NK Ki67_total | 6.0% |
| Tconv memDR_CD3 | 6.0% |
| CD8 RO Ki67_CD8 | 6.0% |
| CD16+mono_total | 6.0% |
| CD8 RO CD56_CD8 | 5.8% |
| Tconv memCXCR3_total | 5.8% |
| CD8 RO PD1_total | 5.8% |
| CD8 RO CD56_CD3 | 5.2% |
| NKCD56hi_CD3neg | 5.2% |
| Tconv memDR_total | 5.2% |
| Tconv memCXCR3_mem | 5.0% |
| CD56_CD8RO | 5.0% |
| Tconv memCCR5_mem | 5.0% |
| CD8 RO PD1_CD3 | 4.8% |
| Tconv memTIGIT_CD3 | 4.8% |
| Tconv memintB7_CD3 | 4.8% |
| Tconv mem_Tconv | 4.5% |
| CD4 Treg_total | 4.5% |
| Tconv memCCR6_total | 4.5% |
| CD8 RA naive_total | 4.5% |
| CD8 RO Ki67_total | 4.2% |
| CD8 RO PD1_CD8 | 4.0% |
| Tconv memintB7_total | 4.0% |
| Bcells naive_total | 4.0% |
| CD8 RO DR_CD3 | 4.0% |
| CD8 RO intB7_CD3 | 3.8% |
| Tconv memCCR4_Tconv | 3.8% |
| CD8 RO CCR5_total | 3.8% |
| CXCR3_CD8RO | 3.8% |
| Bcells naive_CD3neg | 3.5% |
| Tconv memDR_Tconv | 3.2% |
| Bcells memory_CD3neg | 3.2% |
| CD4neg_total | 3.2% |
| CD8 RO TIGIT_CD8 | 3.2% |
| Tconv memCD27_Tconv | 3.2% |
| CD8pos_total | 3.0% |
| naive_Bcells | 3.0% |
| Tconv memKi67_Tconv | 3.0% |
| Tconv memCCR5_CD3 | 3.0% |
| NK Ki67_CD3neg | 2.8% |
| myeloid_CD3neg | 2.8% |
| CD8 RO CXCR3_total | 2.8% |
| Tconv memPD1_CD3 | 2.5% |
| PD1_CD8RO | 2.5% |
| CD8 RO_CD8 | 2.5% |
| CD3hi_CD3 | 2.2% |
| Treg naive_CD3 | 2.2% |
| CD8 RO CD27_total | 2.2% |
| Tconv memCCR5_total | 2.2% |
| Tconv memCD27_total | 2.2% |
| CD8 ncytotox RO CCR4_CD8ntox | 2.2% |
| Tconv memCD56_CD3 | 2.0% |
| Tconv memCD56_mem | 2.0% |
| CD14+16+mono_total | 2.0% |
| CD8 RO CCR4_total | 2.0% |
| CD14+16+mono_CD3neg | 2.0% |
| CD8 RO_CD3 | 2.0% |
| Bcells_CD3neg | 1.8% |
| NKCD16_total | 1.8% |
| Tconv memCD56_Tconv | 1.8% |
| CD8 RO CD56_total | 1.8% |
| Tconv memCCR4_total | 1.5% |
| nonTnonB_CD3neg | 1.5% |
| CD8 RO CCR6_total | 1.5% |
| CD8 RA_CD8 | 1.2% |
| CD8 RO intB7_total | 1.2% |
| CD8 RO DR_total | 1.2% |
| CD8 RO TIGIT_total | 1.2% |
| NK_nonTnonB | 1.2% |
| Tconv memCD27_CD3 | 1.0% |
| Tconv memPD1_Tconv | 1.0% |
| Tconv memCCR5_Tconv | 1.0% |
| CD8 RO CD27_CD8 | 1.0% |
| CD8 RO_total | 1.0% |
| Tconv memPD1_total | 1.0% |
| NKCD16_CD3neg | 1.0% |
| Tconv memTIGIT_total | 1.0% |
| CD4 Tconv mem_total | 0.8% |
| NK_CD3neg | 0.8% |
| CD8  RO Ki67_CD3 | 0.8% |
| Tconv memCCR4_CD3 | 0.5% |
| Tconv mem_CD3 | 0.5% |
| CD14mono_CD3neg | 0.2% |
| NKCD16_nonTnonB | 0.2% |
| nonTnonB_total | 0.2% |
| CD8 ncytotox RO CCR4_CD3 | 0.2% |

### LASSO_RFE

**Base Method**: Raw feature selection frequencies across all bootstrap samples

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD27IgD_Bcells | 37.2% |
| CD14mono_myeloid | 36.5% |
| CD16mono_myeloid | 32.2% |
| CCR4_CD8RO | 31.2% |
| CD8pos_CD3 | 26.8% |
| NKCD56hi_nonTnonB | 25.5% |
| Tconv memPD1_mem | 24.8% |
| NKCD56hi_total | 23.5% |
| CD3hi_CD4neg | 22.5% |
| CD14+16+mono_myeloid | 20.0% |
| CD8 RO CCR5_CD3 | 19.0% |
| CD8 RA_CD3 | 18.5% |
| CD16mono_CD3neg | 18.0% |
| CD4 Treg_CD4 | 16.8% |
| Tconv naive_total | 16.2% |
| Tconv memKi67_total | 16.2% |
| CD8 RO CCR5_CD8 | 15.8% |
| CD4 Tconv_total | 14.8% |
| CD27negIgDneg_Bcells | 14.5% |
| Bcells CD27negIgDneg_total | 14.0% |
| DR_CD8RO | 14.0% |
| CD8 RO TIGIT_CD3 | 13.5% |
| Bcells CD27posIgDneg_total | 13.0% |
| Tconv memCCR6_mem | 12.8% |
| Bcells memory_total | 12.8% |
| Tconv memKi67_mem | 12.5% |
| Tconv memCCR6_Tconv | 12.2% |
| Tconv memCCR6_CD3 | 11.5% |
| CD8 RA_total | 11.2% |
| Treg naive_CD4 | 11.2% |
| Tconv memCD27_mem | 11.2% |
| CD8 RO CXCR3_CD3 | 11.2% |
| CD8 RO CXCR3_CD8 | 10.8% |
| CCR5_CD8RO | 10.5% |
| Bcells Ki67_total | 10.5% |
| CD3hi_total | 10.2% |
| CD8 RA CCR7 naive_CD8 | 10.2% |
| CD4 Tconv_CD3 | 9.8% |
| Treg memory_CD3 | 9.8% |
| Tconv naive_CD3 | 9.8% |
| CD8 RA naive_CD3 | 9.5% |
| Treg memory_CD4 | 9.5% |
| Treg naive_total | 9.2% |
| NK_total | 9.0% |
| Ki67_Bcells | 9.0% |
| CD8 RO DR_CD8 | 9.0% |
| Tconv memCCR4_mem | 8.8% |
| CD4neg_CD3 | 8.5% |
| Treg memory_total | 8.2% |
| Tconv memCXCR3_Tconv | 8.2% |
| TIGIT_CD8RO | 7.8% |
| intB7_CD8RO | 7.8% |
| Bcells Ki67_CD3neg | 7.8% |
| Tconv memintB7_Tconv | 7.5% |
| Tconv memCD56_total | 7.5% |
| Tconv memTIGIT_Tconv | 7.0% |
| CD4 Treg _CD3 | 7.0% |
| CD3pos_total | 6.8% |
| CD8 RO CD27_CD3 | 6.8% |
| CD8 RO CCR6_CD8 | 6.0% |
| Bcells_total | 6.0% |
| CD3neg_total | 6.0% |
| Tconv memKi67_CD3 | 5.8% |
| CD8 RO CCR6_CD3 | 5.8% |
| NK Ki67_nonTnonB | 5.8% |
| memory_Bcells | 5.8% |
| Tconv memTIGIT_mem | 5.8% |
| NK Ki67_NK | 5.5% |
| Tconv memCXCR3_CD3 | 5.2% |
| NKCD56hi_NK | 5.2% |
| NKCD16_NK | 5.0% |
| CCR6_CD8RO | 4.8% |
| CD27_CD8RO | 4.8% |
| Tconv memCCR5_mem | 4.8% |
| CD8 RO intB7_CD8 | 4.8% |
| CD8 RO PD1_total | 4.8% |
| Tconv memCXCR3_mem | 4.2% |
| Tconv memDR_CD3 | 4.2% |
| Tconv memintB7_mem | 4.2% |
| Tconv memCCR6_total | 4.2% |
| Tconv memDR_mem | 4.2% |
| Tconv memCXCR3_total | 4.2% |
| Tconv mem_Tconv | 4.2% |
| CD8 RO PD1_CD3 | 4.2% |
| CD8 RO CD56_CD3 | 4.0% |
| NK Ki67_total | 4.0% |
| CD8 RO Ki67_CD8 | 3.8% |
| CD8 RO CCR5_total | 3.8% |
| CD16+mono_total | 3.8% |
| Tconv memDR_total | 3.8% |
| CD8 RO CD56_CD8 | 3.5% |
| Ki67_CD8RO | 3.5% |
| NKCD56hi_CD3neg | 3.5% |
| CD56_CD8RO | 3.5% |
| Tconv memintB7_CD3 | 3.2% |
| CD8 RO DR_CD3 | 3.2% |
| Tconv memintB7_total | 3.2% |
| CD4 Treg_total | 3.0% |
| CXCR3_CD8RO | 3.0% |
| CD8 RO Ki67_total | 3.0% |
| Bcells memory_CD3neg | 2.8% |
| Tconv memCD27_Tconv | 2.8% |
| Tconv memCCR4_Tconv | 2.8% |
| Tconv memTIGIT_CD3 | 2.5% |
| CD8 RO TIGIT_CD8 | 2.5% |
| CD8pos_total | 2.5% |
| CD8 RO intB7_CD3 | 2.5% |
| CD8 RO CXCR3_total | 2.5% |
| CD8 RA naive_total | 2.2% |
| Tconv memCD27_total | 2.2% |
| naive_Bcells | 2.2% |
| Treg naive_CD3 | 2.0% |
| Tconv memDR_Tconv | 2.0% |
| Bcells naive_total | 2.0% |
| Tconv memPD1_CD3 | 2.0% |
| Tconv memCCR5_CD3 | 2.0% |
| CD8 RO_CD3 | 1.8% |
| CD8 RO PD1_CD8 | 1.8% |
| myeloid_CD3neg | 1.8% |
| PD1_CD8RO | 1.5% |
| CD8 RO CD27_total | 1.5% |
| CD3hi_CD3 | 1.5% |
| CD4neg_total | 1.5% |
| NK Ki67_CD3neg | 1.5% |
| Tconv memCCR5_total | 1.5% |
| CD14+16+mono_CD3neg | 1.2% |
| CD8 RO CD56_total | 1.2% |
| Tconv memCCR4_total | 1.2% |
| Tconv memCD56_Tconv | 1.2% |
| Bcells naive_CD3neg | 1.2% |
| CD8 ncytotox RO CCR4_CD8ntox | 1.2% |
| CD8 RO_CD8 | 1.2% |
| NKCD16_total | 1.2% |
| Bcells_CD3neg | 1.0% |
| Tconv memCD56_mem | 1.0% |
| CD8 RA_CD8 | 1.0% |
| Tconv memPD1_total | 1.0% |
| Tconv memCD27_CD3 | 1.0% |
| NK_nonTnonB | 1.0% |
| CD14+16+mono_total | 1.0% |
| Tconv memCD56_CD3 | 1.0% |
| Tconv memKi67_Tconv | 1.0% |
| nonTnonB_CD3neg | 1.0% |
| CD8 RO CCR6_total | 1.0% |
| CD4 Tconv mem_total | 0.8% |
| CD8 RO intB7_total | 0.8% |
| CD8 RO DR_total | 0.8% |
| Tconv memCCR5_Tconv | 0.8% |
| CD8 RO CCR4_total | 0.8% |
| CD8 RO_total | 0.8% |
| CD8 RO CD27_CD8 | 0.8% |
| NKCD16_CD3neg | 0.8% |
| CD8 RO TIGIT_total | 0.8% |
| Tconv memTIGIT_total | 0.5% |
| Tconv memCCR4_CD3 | 0.5% |
| CD8  RO Ki67_CD3 | 0.5% |
| Tconv mem_CD3 | 0.5% |
| Tconv memPD1_Tconv | 0.5% |
| NK_CD3neg | 0.5% |
| CD14mono_CD3neg | 0.2% |
| nonTnonB_total | 0.2% |
| CD8 ncytotox RO CCR4_CD3 | 0.2% |

### LASSO_Strict

**Base Method**: Raw feature selection frequencies across all bootstrap samples

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CCR4_CD8RO | 23.5% |
| CD27IgD_Bcells | 20.8% |
| CD14mono_myeloid | 20.0% |
| CD16mono_myeloid | 19.5% |
| NKCD56hi_nonTnonB | 17.0% |
| CD8pos_CD3 | 16.0% |
| Tconv memPD1_mem | 16.0% |
| CD14+16+mono_myeloid | 15.5% |
| CD3hi_CD4neg | 13.2% |
| Tconv memKi67_total | 10.5% |
| NKCD56hi_total | 10.0% |
| CD8 RO CCR5_CD3 | 9.8% |
| CD8 RO CCR5_CD8 | 9.8% |
| Tconv naive_total | 8.8% |
| Tconv memKi67_mem | 8.8% |
| CD4 Treg_CD4 | 8.8% |
| CD8 RO TIGIT_CD3 | 8.8% |
| Bcells CD27negIgDneg_total | 8.5% |
| CD8 RA_CD3 | 8.2% |
| DR_CD8RO | 8.2% |
| CD16mono_CD3neg | 8.0% |
| CD8 RA_total | 7.8% |
| Tconv memCCR6_mem | 7.2% |
| Tconv memCCR6_Tconv | 6.5% |
| Tconv memCCR6_CD3 | 6.2% |
| CD8 RO CXCR3_CD8 | 5.5% |
| Treg naive_CD4 | 5.5% |
| CD8 RO CXCR3_CD3 | 5.5% |
| CD8 RO DR_CD8 | 5.5% |
| Treg memory_CD3 | 5.2% |
| Treg memory_CD4 | 5.2% |
| CD4 Tconv_total | 5.2% |
| Bcells Ki67_CD3neg | 5.2% |
| CCR5_CD8RO | 5.0% |
| CD8 RA naive_CD3 | 5.0% |
| Bcells CD27posIgDneg_total | 4.8% |
| CD27negIgDneg_Bcells | 4.8% |
| CD8 RA CCR7 naive_CD8 | 4.8% |
| Tconv naive_CD3 | 4.8% |
| Bcells memory_total | 4.8% |
| Ki67_Bcells | 4.8% |
| Bcells Ki67_total | 4.5% |
| TIGIT_CD8RO | 4.5% |
| Tconv memintB7_Tconv | 4.2% |
| CD3hi_total | 4.2% |
| Tconv memCXCR3_Tconv | 4.2% |
| intB7_CD8RO | 4.0% |
| Treg memory_total | 4.0% |
| CD8 RO CCR6_CD8 | 3.8% |
| CD4 Treg _CD3 | 3.8% |
| CD4 Tconv_CD3 | 3.8% |
| CD8 RO CD27_CD3 | 3.5% |
| Tconv memKi67_CD3 | 3.5% |
| NKCD56hi_NK | 3.5% |
| NK_total | 3.5% |
| Tconv memCD27_mem | 3.2% |
| Tconv memCXCR3_mem | 3.2% |
| Tconv memTIGIT_Tconv | 3.0% |
| CD4neg_CD3 | 3.0% |
| Tconv memDR_mem | 3.0% |
| CD8 RO intB7_CD8 | 3.0% |
| NK Ki67_nonTnonB | 2.8% |
| Treg naive_total | 2.8% |
| Tconv memCCR4_mem | 2.8% |
| NK Ki67_NK | 2.5% |
| CD8 RO CCR6_CD3 | 2.5% |
| Tconv memCD56_total | 2.5% |
| Tconv memCXCR3_CD3 | 2.2% |
| Tconv memTIGIT_mem | 2.2% |
| Bcells_total | 2.2% |
| memory_Bcells | 2.2% |
| CD27_CD8RO | 2.2% |
| NKCD56hi_CD3neg | 2.0% |
| NK Ki67_total | 2.0% |
| Tconv memintB7_CD3 | 2.0% |
| Tconv memintB7_mem | 2.0% |
| Tconv memDR_CD3 | 2.0% |
| Ki67_CD8RO | 2.0% |
| NKCD16_NK | 2.0% |
| CCR6_CD8RO | 2.0% |
| Tconv memDR_total | 2.0% |
| CD8 RO CD56_CD8 | 1.8% |
| CD8 RO CCR5_total | 1.8% |
| CD4 Treg_total | 1.8% |
| Tconv memCCR5_mem | 1.5% |
| CD3pos_total | 1.5% |
| Tconv memCCR4_Tconv | 1.5% |
| Tconv memCXCR3_total | 1.5% |
| CD8 RA naive_total | 1.5% |
| Tconv mem_Tconv | 1.5% |
| CD8 RO CD56_CD3 | 1.5% |
| Tconv memKi67_Tconv | 1.5% |
| CD8 RO intB7_CD3 | 1.2% |
| Tconv memCCR5_CD3 | 1.2% |
| CD8 RO PD1_CD8 | 1.2% |
| CXCR3_CD8RO | 1.2% |
| CD8 RO PD1_total | 1.2% |
| Tconv memTIGIT_CD3 | 1.2% |
| CD56_CD8RO | 1.2% |
| CD8 RO CXCR3_total | 1.2% |
| Treg naive_CD3 | 1.2% |
| CD8 RO DR_CD3 | 1.2% |
| CD8 RO Ki67_total | 1.2% |
| myeloid_CD3neg | 1.0% |
| Tconv memCCR5_total | 1.0% |
| CD8 RO Ki67_CD8 | 1.0% |
| naive_Bcells | 1.0% |
| CD4neg_total | 1.0% |
| Tconv memCCR6_total | 1.0% |
| Tconv memCD27_Tconv | 1.0% |
| CD8 RO PD1_CD3 | 1.0% |
| Bcells naive_CD3neg | 1.0% |
| CD8 ncytotox RO CCR4_CD8ntox | 1.0% |
| Tconv memintB7_total | 1.0% |
| CD8 RO_CD8 | 0.8% |
| Tconv memCCR4_total | 0.8% |
| Bcells naive_total | 0.8% |
| nonTnonB_CD3neg | 0.8% |
| CD8 RO TIGIT_CD8 | 0.8% |
| Tconv memDR_Tconv | 0.8% |
| Bcells memory_CD3neg | 0.8% |
| CD3neg_total | 0.8% |
| CD8pos_total | 0.8% |
| CD16+mono_total | 0.8% |
| Tconv memCD27_total | 0.8% |
| PD1_CD8RO | 0.8% |
| Tconv memPD1_CD3 | 0.8% |
| CD4 Tconv mem_total | 0.5% |
| NK_nonTnonB | 0.5% |
| CD8 RO intB7_total | 0.5% |
| CD8 RO CCR4_total | 0.5% |
| Tconv memCCR5_Tconv | 0.5% |
| CD8 RO CD27_total | 0.5% |
| Bcells_CD3neg | 0.5% |
| Tconv mem_CD3 | 0.5% |
| CD14+16+mono_CD3neg | 0.5% |
| Tconv memPD1_total | 0.5% |
| CD3hi_CD3 | 0.5% |
| CD8 RO CD56_total | 0.5% |
| Tconv memCD56_CD3 | 0.2% |
| CD8 RO CD27_CD8 | 0.2% |
| NK_CD3neg | 0.2% |
| NK Ki67_CD3neg | 0.2% |
| CD14+16+mono_total | 0.2% |
| Tconv memCD56_mem | 0.2% |
| Tconv memPD1_Tconv | 0.2% |
| CD8  RO Ki67_CD3 | 0.2% |
| NKCD16_total | 0.2% |

### LogisticRegression_Permutation_AboveMean

**Base Method**: Raw feature selection frequencies across all bootstrap samples

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CCR4_CD8RO | 5.3% |
| Bcells CD27posIgDneg_total | 2.5% |
| DR_CD8RO | 2.2% |
| Bcells CD27negIgDneg_total | 2.2% |
| CD3hi_CD4neg | 1.9% |
| CD8 RO DR_CD8 | 1.9% |
| CD3hi_total | 1.6% |
| CD8 RO CXCR3_CD8 | 1.2% |
| Tconv memCD56_total | 1.2% |
| Tconv memCXCR3_total | 1.2% |
| NK Ki67_NK | 1.2% |
| CD8 RO CXCR3_total | 0.9% |
| Tconv memCXCR3_Tconv | 0.9% |
| Bcells memory_CD3neg | 0.9% |
| CD8 RO CXCR3_CD3 | 0.9% |
| CD4neg_total | 0.9% |
| Bcells memory_total | 0.9% |
| Bcells_total | 0.9% |
| CD8 RO CD27_total | 0.9% |
| CD8 RO_CD3 | 0.9% |
| CD3hi_CD3 | 0.9% |
| Treg memory_CD4 | 0.9% |
| CD8 RO Ki67_CD8 | 0.9% |
| NK_total | 0.6% |
| CD4 Tconv_total | 0.6% |
| Tconv memCCR5_total | 0.6% |
| Tconv memKi67_total | 0.6% |
| CD8 RA_total | 0.6% |
| CD8 RO TIGIT_total | 0.6% |
| Ki67_CD8RO | 0.6% |
| Tconv memCD56_Tconv | 0.6% |
| CD16+mono_total | 0.6% |
| CD4 Treg _CD3 | 0.6% |
| Tconv memPD1_Tconv | 0.6% |
| CD14mono_total | 0.6% |
| Tconv memCXCR3_CD3 | 0.6% |
| NKCD16_total | 0.6% |
| CD8 RO Ki67_total | 0.6% |
| CD8 RA naive_total | 0.6% |
| CD14+16+mono_total | 0.6% |
| Bcells naive_total | 0.6% |
| CD8 RO_total | 0.6% |
| CD14+16+mono_myeloid | 0.6% |
| CD8 RO CCR4_total | 0.6% |
| CD8 RO CCR5_CD3 | 0.6% |
| Tconv naive_CD3 | 0.6% |
| Bcells naive_CD3neg | 0.6% |
| NK_nonTnonB | 0.6% |
| Tconv memPD1_CD3 | 0.6% |
| nonTnonB_CD3neg | 0.6% |
| NKCD16_CD3neg | 0.6% |
| CD14+16+mono_CD3neg | 0.6% |
| CD8 RO CCR6_total | 0.6% |
| TIGIT_CD8RO | 0.6% |
| PD1_CD8RO | 0.6% |
| CD8pos_CD3 | 0.6% |
| CD27_CD8RO | 0.6% |
| Tconv memCXCR3_mem | 0.6% |
| CD8 RO TIGIT_CD8 | 0.6% |
| Bcells_CD3neg | 0.6% |
| Tconv memPD1_mem | 0.6% |
| CD8 RA_CD8 | 0.6% |
| CD8  RO Ki67_CD3 | 0.6% |
| CD4 Treg_CD4 | 0.6% |
| CD8 RO CD27_CD8 | 0.6% |
| CXCR3_CD8RO | 0.6% |
| CD8 RO CD27_CD3 | 0.6% |
| CD4neg_CD3 | 0.6% |
| naive_Bcells | 0.6% |
| memory_Bcells | 0.6% |
| Treg memory_CD3 | 0.6% |
| CD27IgD_Bcells | 0.6% |
| NKCD16_NK | 0.6% |
| NKCD16_nonTnonB | 0.6% |
| CD8 RO intB7_total | 0.6% |
| CD4 Treg_total | 0.6% |
| CD16mono_CD3neg | 0.6% |
| CD14mono_CD3neg | 0.6% |
| Tconv mem_Tconv | 0.6% |
| NK_CD3neg | 0.6% |
| nonTnonB_total | 0.3% |
| Tconv memDR_total | 0.3% |
| Tconv memintB7_total | 0.3% |
| CD8 ncytotox RO CCR4_CD3 | 0.3% |
| Tconv memCD27_CD3 | 0.3% |
| NKCD56hi_NK | 0.3% |
| NKCD56hi_nonTnonB | 0.3% |
| CD8 RA naive_CD3 | 0.3% |
| Tconv memTIGIT_CD3 | 0.3% |
| Tconv memDR_CD3 | 0.3% |
| CD8 RO DR_CD3 | 0.3% |
| Tconv memCCR5_CD3 | 0.3% |
| Treg memory_total | 0.3% |
| Tconv memCCR4_CD3 | 0.3% |
| Tconv mem_CD3 | 0.3% |
| Treg naive_total | 0.3% |
| Tconv memPD1_total | 0.3% |
| Tconv memTIGIT_total | 0.3% |
| CD8 RO DR_total | 0.3% |
| Tconv naive_total | 0.3% |
| NK Ki67_total | 0.3% |
| myeloid_total | 0.3% |
| Tconv memCD56_CD3 | 0.3% |
| NK Ki67_nonTnonB | 0.3% |
| Treg naive_CD3 | 0.3% |
| Ki67_Bcells | 0.3% |
| NKCD56hi_total | 0.3% |
| CD16mono_myeloid | 0.3% |
| Tconv memCCR4_mem | 0.3% |
| Tconv naive_Tconv | 0.3% |
| Tconv memCCR5_mem | 0.3% |
| Tconv memCD56_mem | 0.3% |
| CD8 RA CCR7 naive_CD8 | 0.3% |
| NK Ki67_CD3neg | 0.3% |
| CD8 RO_CD8 | 0.3% |
| CD8 RO intB7_CD8 | 0.3% |
| Treg naive_CD4 | 0.3% |
| Tconv memCCR5_Tconv | 0.3% |
| Tconv memCCR6_Tconv | 0.3% |
| CD8 RO CD56_CD3 | 0.3% |
| Tconv memCD27_Tconv | 0.3% |
| CD8 RO PD1_CD8 | 0.3% |
| CCR5_CD8RO | 0.3% |
| myeloid_CD3neg | 0.3% |
| CD8pos_total | 0.3% |
| CD56_CD8RO | 0.3% |
| intB7_CD8RO | 0.3% |
| NKCD56hi_CD3neg | 0.3% |
| CD8 RO intB7_CD3 | 0.3% |
| Tconv memDR_mem | 0.3% |
| CD8 RA_CD3 | 0.3% |
| Tconv memDR_Tconv | 0.3% |
| CD8 RO CD56_CD8 | 0.3% |
| Tconv memKi67_mem | 0.3% |
| CD4 Tconv_CD3 | 0.3% |
| CD8 RO TIGIT_CD3 | 0.3% |
| CD8 RO CCR5_CD8 | 0.3% |
| CD14mono_myeloid | 0.3% |
| CD4 Tconv mem_total | 0.3% |
| Tconv memCD27_total | 0.3% |

### LogisticRegression_Permutation_Top10%

**Base Method**: Raw feature selection frequencies across all bootstrap samples

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Tconv memCXCR3_total | 99.8% |
| Tconv memDR_total | 99.5% |
| Tconv memPD1_total | 99.5% |
| Tconv memKi67_total | 99.2% |
| Tconv naive_total | 99.2% |
| Tconv memCD27_total | 99.2% |
| Tconv memintB7_total | 99.2% |
| Tconv memCD56_total | 99.2% |
| Tconv memTIGIT_total | 98.5% |
| CD3pos_total | 98.2% |
| CD4 Tconv mem_total | 98.2% |
| CD4 Treg_total | 98.2% |
| Tconv memCCR4_total | 98.0% |
| CD4 Tconv_total | 96.8% |
| Tconv memCCR5_total | 95.8% |
| Tconv memCCR6_total | 88.8% |
| CCR4_CD8RO | 4.2% |
| Bcells CD27negIgDneg_total | 1.8% |
| Bcells CD27posIgDneg_total | 1.8% |
| DR_CD8RO | 1.5% |
| CD3hi_CD4neg | 1.2% |
| CD8 RO DR_CD8 | 1.2% |
| CD3hi_total | 1.2% |
| CD4neg_total | 0.8% |
| NK Ki67_NK | 0.8% |
| CD8 RA_total | 0.5% |
| CD8 RO Ki67_CD8 | 0.5% |
| CD8 RO CD27_total | 0.5% |
| CD8 RO intB7_total | 0.5% |
| CD56_CD8RO | 0.5% |
| CD8 RO CCR6_total | 0.5% |
| CD8 RO TIGIT_total | 0.5% |
| CD8 RO CXCR3_total | 0.5% |
| NK_total | 0.5% |
| CD8 RO CXCR3_CD8 | 0.5% |
| Ki67_CD8RO | 0.5% |
| CD3hi_CD3 | 0.5% |
| Bcells memory_total | 0.5% |
| CD8 RO CXCR3_CD3 | 0.5% |
| CD27_CD8RO | 0.5% |
| CD8pos_total | 0.2% |
| CD8 RO DR_total | 0.2% |
| CD8 RA_CD8 | 0.2% |
| NK_nonTnonB | 0.2% |
| nonTnonB_total | 0.2% |
| CD8 RO Ki67_total | 0.2% |
| naive_Bcells | 0.2% |
| Bcells naive_CD3neg | 0.2% |
| CD8 RO_total | 0.2% |
| NKCD16_nonTnonB | 0.2% |
| CD4neg_CD3 | 0.2% |
| CD8 RO CCR4_total | 0.2% |
| CD14mono_total | 0.2% |
| Bcells memory_CD3neg | 0.2% |
| CD8 RO CD56_CD8 | 0.2% |
| CD8 RO CD27_CD8 | 0.2% |
| CD8pos_CD3 | 0.2% |
| CD4 Tconv_CD3 | 0.2% |
| Tconv memPD1_mem | 0.2% |
| Tconv memPD1_Tconv | 0.2% |
| Tconv memPD1_CD3 | 0.2% |
| memory_Bcells | 0.2% |
| CD8 RO_CD3 | 0.2% |
| CD8 RO TIGIT_CD3 | 0.2% |
| TIGIT_CD8RO | 0.2% |
| Bcells_total | 0.2% |
| Treg memory_CD4 | 0.2% |
| Tconv mem_Tconv | 0.2% |
| CD8 RO CCR5_CD3 | 0.2% |
| CD8 RO CCR5_CD8 | 0.2% |
| PD1_CD8RO | 0.2% |
| CD14+16+mono_total | 0.2% |
| CD8 RO TIGIT_CD8 | 0.2% |
| CD14mono_myeloid | 0.2% |
| CD16mono_CD3neg | 0.2% |
| CD16+mono_total | 0.2% |
| Tconv memCXCR3_Tconv | 0.2% |
| NKCD16_NK | 0.2% |
| CD8 RA naive_total | 0.2% |
| CD27IgD_Bcells | 0.2% |
| CD14+16+mono_myeloid | 0.2% |
| CD14+16+mono_CD3neg | 0.2% |

### Mutual Information (Top 10%)

**Base Method**: Raw feature selection frequencies across all bootstrap samples

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD8pos_CD3 | 48.0% |
| Treg memory_CD4 | 35.2% |
| CD4 Treg_CD4 | 35.2% |
| CD8 RO CCR5_CD3 | 34.5% |
| nonTnonB_total | 33.2% |
| Tconv naive_total | 28.7% |
| CD4 Tconv_total | 26.5% |
| TIGIT_CD8RO | 26.2% |
| Tconv naive_CD3 | 22.5% |
| CD8 RO_CD3 | 22.2% |
| NK Ki67_nonTnonB | 22.2% |
| CD8pos_total | 21.8% |
| DR_CD8RO | 21.5% |
| CD16mono_CD3neg | 21.2% |
| CD8 RO CCR6_CD3 | 21.2% |
| Bcells CD27posIgDneg_total | 20.5% |
| nonTnonB_CD3neg | 20.5% |
| CD8 RA naive_CD3 | 20.2% |
| CD27IgD_Bcells | 20.2% |
| Treg naive_CD4 | 20.2% |
| CD8 RO TIGIT_CD3 | 20.0% |
| CD16mono_myeloid | 20.0% |
| Tconv memPD1_mem | 19.5% |
| CD4 Treg _CD3 | 19.2% |
| CD8 RA_CD3 | 19.2% |
| Bcells_CD3neg | 19.0% |
| PD1_CD8RO | 19.0% |
| CD8 RO CD27_CD3 | 18.5% |
| CD8 RO DR_total | 17.8% |
| CD8 RO CCR5_total | 17.8% |
| CD3neg_total | 17.5% |
| CD3pos_total | 17.5% |
| CD8 RO CCR5_CD8 | 17.0% |
| CD14mono_total | 17.0% |
| CD8 ncytotox RO CCR4_CD8ntox | 16.8% |
| CD8  RO Ki67_CD3 | 16.5% |
| Treg memory_CD3 | 15.2% |
| Ki67_CD8RO | 15.0% |
| Treg memory_total | 14.2% |
| CD4 Tconv mem_total | 14.0% |
| Tconv mem_Tconv | 13.8% |
| Tconv memCCR5_CD3 | 13.5% |
| CD8 RO CD56_CD3 | 13.2% |
| CD8 RO CXCR3_CD3 | 12.8% |
| Tconv memTIGIT_CD3 | 12.5% |
| intB7_CD8RO | 12.5% |
| Tconv naive_Tconv | 12.0% |
| Tconv memCXCR3_Tconv | 11.8% |
| NK Ki67_NK | 11.8% |
| CD14mono_CD3neg | 11.8% |
| Tconv memCD27_total | 11.8% |
| Tconv memCCR6_mem | 11.8% |
| CD4 Tconv_CD3 | 11.5% |
| Ki67_Bcells | 11.5% |
| CD27_CD8RO | 11.2% |
| CCR5_CD8RO | 11.2% |
| Tconv mem_CD3 | 11.2% |
| CD4neg_CD3 | 11.0% |
| NKCD16_CD3neg | 11.0% |
| Bcells memory_CD3neg | 11.0% |
| Bcells_total | 11.0% |
| CD4 Treg_total | 10.8% |
| Tconv memCCR5_total | 10.0% |
| Tconv memKi67_total | 10.0% |
| CD8 RO DR_CD3 | 10.0% |
| NK Ki67_total | 9.8% |
| Tconv memCCR5_mem | 9.5% |
| Tconv memDR_CD3 | 9.5% |
| Tconv memintB7_CD3 | 9.2% |
| Tconv memintB7_Tconv | 9.2% |
| NK_total | 9.2% |
| Tconv memCCR6_CD3 | 9.0% |
| Tconv memCD56_total | 9.0% |
| naive_Bcells | 8.8% |
| CD8 RO DR_CD8 | 8.8% |
| Tconv memCD27_CD3 | 8.8% |
| NK_CD3neg | 8.5% |
| NKCD16_NK | 8.5% |
| NKCD16_total | 8.2% |
| Tconv memTIGIT_mem | 8.2% |
| CD8 RO CCR4_total | 8.0% |
| CD8 RO CD56_CD8 | 8.0% |
| NKCD56hi_NK | 8.0% |
| CD14mono_myeloid | 8.0% |
| CD8 RA CCR7 naive_CD8 | 8.0% |
| Tconv memKi67_CD3 | 8.0% |
| Tconv memKi67_Tconv | 7.2% |
| Tconv memPD1_CD3 | 7.2% |
| Bcells memory_total | 7.2% |
| myeloid_CD3neg | 7.2% |
| CD8 RO Ki67_CD8 | 7.0% |
| Tconv memKi67_mem | 7.0% |
| Tconv memCCR6_Tconv | 6.8% |
| CD8 ncytotox RO CCR4_CD3 | 6.8% |
| Treg naive_total | 6.8% |
| NKCD56hi_CD3neg | 6.8% |
| CD16+mono_total | 6.8% |
| CD8 RO_total | 6.5% |
| Tconv memCCR5_Tconv | 6.5% |
| NKCD56hi_nonTnonB | 6.5% |
| CD8 RO CXCR3_total | 6.2% |
| CD8 RA naive_total | 6.2% |
| NKCD56hi_total | 6.2% |
| NKCD16_nonTnonB | 6.0% |
| Bcells Ki67_CD3neg | 6.0% |
| CD8 RO Ki67_total | 6.0% |
| CD8 RA_total | 6.0% |
| Tconv memCD56_Tconv | 5.8% |
| NK_nonTnonB | 5.8% |
| NK Ki67_CD3neg | 5.8% |
| CD3hi_total | 5.5% |
| CD8 RA_CD8 | 5.5% |
| Tconv memCCR4_total | 5.5% |
| Tconv memCD56_mem | 5.5% |
| Tconv memCXCR3_CD3 | 5.2% |
| CD56_CD8RO | 5.2% |
| CD8 RO CD56_total | 5.2% |
| CD14+16+mono_myeloid | 5.0% |
| CD3hi_CD4neg | 5.0% |
| Tconv memintB7_mem | 5.0% |
| CD8 RO CD27_CD8 | 4.8% |
| Bcells Ki67_total | 4.8% |
| Tconv memCD27_mem | 4.8% |
| Tconv memTIGIT_Tconv | 4.5% |
| Tconv memCXCR3_mem | 4.5% |
| Tconv memTIGIT_total | 4.2% |
| Tconv memPD1_total | 4.2% |
| Tconv memCXCR3_total | 4.2% |
| CD8 RO TIGIT_CD8 | 4.2% |
| Tconv memDR_mem | 4.0% |
| Tconv memDR_total | 4.0% |
| CD8 RO CXCR3_CD8 | 4.0% |
| Bcells naive_total | 4.0% |
| CD8 RO intB7_CD3 | 4.0% |
| CD8 RO intB7_CD8 | 3.8% |
| Bcells CD27negIgDneg_total | 3.8% |
| CD27negIgDneg_Bcells | 3.5% |
| CD14+16+mono_CD3neg | 3.5% |
| CXCR3_CD8RO | 3.5% |
| Treg naive_CD3 | 3.5% |
| Tconv memCCR4_Tconv | 3.2% |
| CD8 RO_CD8 | 3.2% |
| CD3hi_CD3 | 3.2% |
| CD8 RO PD1_CD3 | 3.2% |
| CCR4_CD8RO | 3.2% |
| Tconv memintB7_total | 3.0% |
| CCR6_CD8RO | 3.0% |
| CD8 RO PD1_CD8 | 3.0% |
| Tconv memPD1_Tconv | 3.0% |
| CD8 RO TIGIT_total | 3.0% |
| Bcells naive_CD3neg | 3.0% |
| myeloid_total | 2.8% |
| CD14+16+mono_total | 2.8% |
| memory_Bcells | 2.5% |
| Tconv memCCR4_mem | 2.5% |
| CD8 RO CD27_total | 2.5% |
| Tconv memCD56_CD3 | 2.5% |
| Tconv memCCR6_total | 2.2% |
| Tconv memCCR4_CD3 | 2.2% |
| CD8 RO intB7_total | 2.2% |
| Tconv memCD27_Tconv | 2.0% |
| CD8 RO CCR6_CD8 | 1.8% |
| CD8 RO PD1_total | 1.5% |
| CD8 RO CCR6_total | 1.5% |
| CD4neg_total | 1.0% |
| Tconv memDR_Tconv | 0.5% |

### NaiveBayes_Permutation_AboveMean

**Base Method**: Raw feature selection frequencies across all bootstrap samples

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Bcells CD27posIgDneg_total | 68.5% |
| Bcells memory_total | 63.0% |
| CD8 RO Ki67_CD8 | 58.2% |
| CD8  RO Ki67_CD3 | 58.0% |
| CD3hi_total | 57.8% |
| CD8 RO CCR5_CD3 | 55.0% |
| Bcells memory_CD3neg | 55.0% |
| CD8 RO Ki67_total | 54.8% |
| CD8 RO DR_total | 54.5% |
| CD8 RO DR_CD3 | 53.8% |
| NKCD56hi_NK | 52.8% |
| NK Ki67_NK | 48.0% |
| Ki67_CD8RO | 47.5% |
| Tconv memCD56_Tconv | 46.0% |
| CD27negIgDneg_Bcells | 45.5% |
| CD14+16+mono_total | 45.2% |
| CD8 RO CCR6_CD3 | 45.0% |
| NKCD16_NK | 45.0% |
| CD16mono_myeloid | 43.0% |
| Tconv memCXCR3_total | 42.5% |
| Tconv memCD56_mem | 42.5% |
| CD8 RO CD56_CD3 | 42.0% |
| Bcells_total | 39.0% |
| CD14+16+mono_CD3neg | 38.8% |
| Tconv memCXCR3_Tconv | 38.5% |
| NK Ki67_total | 38.5% |
| CD8 RO CD56_total | 38.2% |
| DR_CD8RO | 38.0% |
| Tconv memCD56_CD3 | 38.0% |
| CD27IgD_Bcells | 37.5% |
| CD8 RO CXCR3_CD3 | 37.0% |
| CD8 RA naive_CD3 | 34.8% |
| CD8 RO intB7_CD3 | 34.2% |
| CD8 RO CCR5_total | 32.2% |
| CD14mono_myeloid | 32.0% |
| Tconv memCD56_total | 31.8% |
| Tconv memCCR5_total | 31.8% |
| CD14+16+mono_myeloid | 31.8% |
| Tconv memCXCR3_CD3 | 31.5% |
| NKCD16_total | 31.5% |
| Treg naive_total | 31.2% |
| CD8 RO CCR6_total | 31.0% |
| Bcells naive_total | 30.8% |
| Bcells CD27negIgDneg_total | 30.2% |
| NK_total | 30.2% |
| Tconv memCCR5_Tconv | 29.8% |
| NKCD56hi_total | 29.5% |
| CD8 RA_CD3 | 29.5% |
| Tconv memKi67_total | 28.5% |
| CD3hi_CD4neg | 28.2% |
| Bcells naive_CD3neg | 27.5% |
| NK Ki67_CD3neg | 27.0% |
| CD3hi_CD3 | 26.0% |
| Tconv naive_total | 26.0% |
| Tconv memCD27_mem | 25.0% |
| Tconv memTIGIT_total | 25.0% |
| CD8 RO DR_CD8 | 24.8% |
| CD27_CD8RO | 24.5% |
| Tconv memCXCR3_mem | 24.2% |
| CD8 RO CXCR3_total | 24.0% |
| nonTnonB_CD3neg | 24.0% |
| Treg memory_CD4 | 24.0% |
| NK Ki67_nonTnonB | 24.0% |
| Ki67_Bcells | 23.5% |
| CD8 RO intB7_total | 23.5% |
| Tconv memPD1_mem | 23.2% |
| CD8 RA naive_total | 23.0% |
| Bcells_CD3neg | 23.0% |
| Tconv memintB7_CD3 | 23.0% |
| CD4 Treg_CD4 | 22.8% |
| Bcells Ki67_CD3neg | 22.8% |
| Tconv memCCR6_Tconv | 22.8% |
| CD8 RO_CD3 | 22.0% |
| Tconv memCCR5_CD3 | 21.5% |
| Treg naive_CD3 | 21.5% |
| CD16mono_CD3neg | 21.2% |
| CCR4_CD8RO | 21.2% |
| CD8pos_CD3 | 21.0% |
| CD8 RO CD56_CD8 | 20.8% |
| CD8 RO PD1_CD3 | 20.2% |
| CD16+mono_total | 20.2% |
| Bcells Ki67_total | 20.2% |
| Tconv memCCR6_mem | 20.2% |
| CD4neg_CD3 | 20.2% |
| Tconv memCCR4_mem | 20.2% |
| CD4 Tconv_total | 20.2% |
| Tconv memCCR6_CD3 | 20.2% |
| Tconv memCCR5_mem | 20.2% |
| CD8 RO PD1_CD8 | 20.0% |
| CD8 RA_total | 20.0% |
| Tconv memintB7_total | 19.8% |
| CD4 Treg_total | 19.8% |
| CD8 RO CCR4_total | 19.8% |
| CD8 ncytotox RO CCR4_CD3 | 19.2% |
| CD8 RO CD27_CD3 | 19.2% |
| CD4 Treg _CD3 | 19.2% |
| Tconv memCCR4_total | 19.0% |
| Tconv memintB7_mem | 19.0% |
| Tconv memintB7_Tconv | 18.8% |
| intB7_CD8RO | 18.8% |
| CD56_CD8RO | 18.8% |
| NKCD56hi_nonTnonB | 18.5% |
| Treg memory_CD3 | 18.5% |
| Treg memory_total | 18.5% |
| CD8 RO TIGIT_CD3 | 18.2% |
| Treg naive_CD4 | 18.2% |
| CD8 RO PD1_total | 18.2% |
| Tconv memCD27_total | 18.2% |
| Tconv memDR_total | 18.2% |
| CXCR3_CD8RO | 18.2% |
| Tconv memKi67_mem | 18.0% |
| Tconv memKi67_CD3 | 17.8% |
| CD8 RO CCR5_CD8 | 17.8% |
| NKCD56hi_CD3neg | 17.8% |
| CCR6_CD8RO | 17.5% |
| naive_Bcells | 17.5% |
| CD4 Tconv mem_total | 17.2% |
| CD8 RO CXCR3_CD8 | 17.2% |
| Tconv memTIGIT_Tconv | 17.2% |
| Tconv memCD27_Tconv | 17.2% |
| CD8 RO intB7_CD8 | 17.2% |
| Tconv memCCR4_CD3 | 17.0% |
| CD3neg_total | 17.0% |
| CD3pos_total | 17.0% |
| TIGIT_CD8RO | 16.8% |
| Tconv memTIGIT_CD3 | 16.5% |
| Tconv memDR_mem | 16.5% |
| Tconv memCCR6_total | 16.5% |
| CD8 ncytotox RO CCR4_CD8ntox | 16.2% |
| NK_nonTnonB | 16.2% |
| NKCD16_nonTnonB | 16.2% |
| CD8 RO CCR6_CD8 | 16.0% |
| NKCD16_CD3neg | 15.8% |
| Tconv memCD27_CD3 | 15.8% |
| Tconv memPD1_total | 15.5% |
| CD4 Tconv_CD3 | 15.5% |
| Tconv naive_CD3 | 15.5% |
| memory_Bcells | 15.5% |
| CD8pos_total | 15.5% |
| nonTnonB_total | 15.5% |
| CD8 RA CCR7 naive_CD8 | 15.2% |
| NK_CD3neg | 15.2% |
| PD1_CD8RO | 15.0% |
| CD8 RO TIGIT_CD8 | 15.0% |
| Tconv memCCR4_Tconv | 14.8% |
| Tconv naive_Tconv | 14.5% |
| Tconv mem_Tconv | 14.5% |
| Tconv memTIGIT_mem | 14.5% |
| Tconv memKi67_Tconv | 14.2% |
| Tconv mem_CD3 | 14.2% |
| CCR5_CD8RO | 14.0% |
| Tconv memPD1_CD3 | 14.0% |
| CD8 RO TIGIT_total | 13.8% |
| myeloid_CD3neg | 13.5% |
| CD14mono_CD3neg | 13.2% |
| CD8 RO CD27_CD8 | 13.2% |
| CD4neg_total | 13.2% |
| CD14mono_total | 13.0% |
| CD8 RO_total | 13.0% |
| Tconv memPD1_Tconv | 13.0% |
| Tconv memDR_CD3 | 12.8% |
| CD8 RA_CD8 | 12.5% |
| CD8 RO CD27_total | 12.5% |
| CD8 RO_CD8 | 12.0% |
| myeloid_total | 10.8% |
| Tconv memDR_Tconv | 10.0% |

### NaiveBayes_Permutation_Top10%

**Base Method**: Raw feature selection frequencies across all bootstrap samples

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Bcells CD27posIgDneg_total | 54.0% |
| Bcells memory_total | 49.8% |
| CD8 RO Ki67_CD8 | 45.8% |
| CD8  RO Ki67_CD3 | 45.8% |
| CD8 RO DR_CD3 | 45.0% |
| CD8 RO DR_total | 44.2% |
| CD8 RO Ki67_total | 40.2% |
| NKCD56hi_NK | 39.2% |
| CD3hi_total | 38.8% |
| Bcells memory_CD3neg | 38.0% |
| CD8 RO CCR5_CD3 | 34.8% |
| Tconv memCD56_Tconv | 34.8% |
| NK Ki67_NK | 31.8% |
| NKCD16_NK | 30.5% |
| Ki67_CD8RO | 28.7% |
| CD14+16+mono_total | 28.2% |
| CD27negIgDneg_Bcells | 27.3% |
| CD8 RO CD56_CD3 | 26.0% |
| Tconv memCXCR3_total | 26.0% |
| Tconv memCD56_mem | 23.8% |
| CD8 RO CCR6_CD3 | 23.8% |
| Tconv memCXCR3_Tconv | 22.5% |
| Tconv memCD56_CD3 | 22.2% |
| CD8 RO CD56_total | 22.2% |
| NK Ki67_total | 21.5% |
| Bcells_total | 20.5% |
| CD16mono_myeloid | 20.5% |
| CD8 RO CXCR3_CD3 | 20.5% |
| CD14+16+mono_CD3neg | 19.5% |
| Tconv memCD56_total | 16.5% |
| CD8 RO intB7_CD3 | 16.2% |
| CD14+16+mono_myeloid | 16.2% |
| Bcells naive_total | 16.0% |
| DR_CD8RO | 15.5% |
| Tconv memCCR5_total | 15.0% |
| CD8 RO CCR5_total | 14.5% |
| CD27IgD_Bcells | 14.0% |
| NK_total | 13.2% |
| CD8 RA naive_CD3 | 13.0% |
| Tconv memCXCR3_CD3 | 13.0% |
| Tconv memKi67_total | 12.8% |
| NKCD16_total | 12.8% |
| Tconv memCCR5_Tconv | 12.5% |
| NKCD56hi_total | 12.0% |
| Treg naive_total | 11.8% |
| Bcells naive_CD3neg | 11.8% |
| CD8 RO CCR6_total | 11.2% |
| CD27_CD8RO | 11.0% |
| CD14mono_myeloid | 11.0% |
| Bcells CD27negIgDneg_total | 10.0% |
| Treg memory_CD4 | 10.0% |
| CD8 RA_CD3 | 9.8% |
| NK Ki67_CD3neg | 9.8% |
| NK Ki67_nonTnonB | 9.5% |
| CD3hi_CD3 | 9.2% |
| Tconv memTIGIT_total | 8.8% |
| CD8 RO DR_CD8 | 8.8% |
| Tconv naive_total | 8.5% |
| Tconv memCD27_mem | 8.5% |
| CD4 Treg_CD4 | 8.2% |
| nonTnonB_CD3neg | 8.0% |
| CD8 RO intB7_total | 8.0% |
| CD3hi_CD4neg | 7.8% |
| Tconv memCCR5_CD3 | 7.8% |
| Bcells_CD3neg | 7.5% |
| CD8 RO CXCR3_total | 7.2% |
| CD8 RO_CD3 | 7.2% |
| CD8 ncytotox RO CCR4_CD3 | 7.0% |
| CD8 RO CCR4_total | 7.0% |
| CD8 RA_total | 6.5% |
| Bcells Ki67_CD3neg | 6.0% |
| Tconv memCCR6_Tconv | 5.8% |
| Tconv memintB7_CD3 | 5.5% |
| Ki67_Bcells | 5.2% |
| CD4neg_CD3 | 5.2% |
| Tconv memPD1_mem | 4.8% |
| CD8 RO CD27_CD3 | 4.8% |
| CD8pos_CD3 | 4.5% |
| Tconv memintB7_mem | 4.2% |
| CD8 RA naive_total | 4.2% |
| CD16+mono_total | 4.2% |
| CD8 RO CD56_CD8 | 4.2% |
| NKCD56hi_nonTnonB | 4.2% |
| Tconv memCD27_total | 4.2% |
| Tconv memCXCR3_mem | 4.0% |
| Tconv memCCR5_mem | 4.0% |
| Tconv memCCR6_CD3 | 4.0% |
| CD8 RO CCR5_CD8 | 4.0% |
| CD56_CD8RO | 4.0% |
| Treg naive_CD3 | 4.0% |
| Tconv memintB7_total | 4.0% |
| Tconv memCCR6_mem | 3.8% |
| intB7_CD8RO | 3.5% |
| CD4 Tconv_total | 3.5% |
| CD4 Treg_total | 3.5% |
| Treg memory_CD3 | 3.2% |
| Treg memory_total | 3.2% |
| Tconv memintB7_Tconv | 3.2% |
| Bcells Ki67_total | 3.2% |
| Treg naive_CD4 | 3.2% |
| CD16mono_CD3neg | 3.0% |
| CD8 RO PD1_CD8 | 3.0% |
| CCR4_CD8RO | 3.0% |
| Tconv naive_CD3 | 2.8% |
| CD8pos_total | 2.8% |
| CD8 RO PD1_CD3 | 2.8% |
| CD8 RO TIGIT_CD3 | 2.5% |
| Tconv memPD1_total | 2.5% |
| CD8 RO PD1_total | 2.5% |
| CD3neg_total | 2.5% |
| Tconv memTIGIT_Tconv | 2.5% |
| CD8 RO intB7_CD8 | 2.5% |
| Tconv memCCR4_mem | 2.5% |
| CD3pos_total | 2.5% |
| NKCD16_nonTnonB | 2.5% |
| NK_nonTnonB | 2.5% |
| Tconv memKi67_CD3 | 2.2% |
| Tconv memKi67_mem | 2.2% |
| NKCD56hi_CD3neg | 2.2% |
| Tconv memDR_total | 2.2% |
| CD4 Treg _CD3 | 2.2% |
| Tconv memTIGIT_CD3 | 2.0% |
| Tconv memCCR4_total | 2.0% |
| CCR6_CD8RO | 2.0% |
| Tconv memCCR6_total | 2.0% |
| CD4 Tconv_CD3 | 2.0% |
| Tconv memCD27_CD3 | 1.8% |
| CD8 RO CXCR3_CD8 | 1.8% |
| Tconv memDR_mem | 1.8% |
| nonTnonB_total | 1.5% |
| CD8 RO CD27_total | 1.5% |
| naive_Bcells | 1.5% |
| CD4neg_total | 1.5% |
| CCR5_CD8RO | 1.5% |
| CD8 RO_total | 1.5% |
| NKCD16_CD3neg | 1.5% |
| Tconv memCCR4_CD3 | 1.5% |
| NK_CD3neg | 1.5% |
| Tconv memCD27_Tconv | 1.2% |
| CD8 RO CCR6_CD8 | 1.2% |
| Tconv mem_Tconv | 1.2% |
| Tconv memTIGIT_mem | 1.2% |
| Tconv memKi67_Tconv | 1.2% |
| TIGIT_CD8RO | 1.0% |
| CD8 ncytotox RO CCR4_CD8ntox | 1.0% |
| CD14mono_total | 1.0% |
| Tconv naive_Tconv | 1.0% |
| Tconv memCCR4_Tconv | 1.0% |
| CD8 RA CCR7 naive_CD8 | 1.0% |
| PD1_CD8RO | 1.0% |
| CD4 Tconv mem_total | 0.8% |
| CD8 RO TIGIT_total | 0.8% |
| CXCR3_CD8RO | 0.8% |
| memory_Bcells | 0.8% |
| Tconv memPD1_CD3 | 0.8% |
| CD8 RO CD27_CD8 | 0.5% |
| myeloid_CD3neg | 0.5% |
| CD14mono_CD3neg | 0.5% |
| Tconv memDR_Tconv | 0.5% |
| Tconv mem_CD3 | 0.5% |
| myeloid_total | 0.5% |
| CD8 RA_CD8 | 0.2% |
| CD8 RO_CD8 | 0.2% |
| CD8 RO TIGIT_CD8 | 0.2% |
| Tconv memPD1_Tconv | 0.2% |
| Tconv memDR_CD3 | 0.2% |

### RFE (RandomForest)

**Base Method**: Raw feature selection frequencies across all bootstrap samples

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD16mono_myeloid | 92.8% |
| CD27IgD_Bcells | 92.8% |
| CD16mono_CD3neg | 91.0% |
| CD8pos_CD3 | 89.2% |
| CD4 Treg_CD4 | 88.2% |
| Treg memory_CD4 | 87.8% |
| CD8 RO CCR5_CD3 | 87.0% |
| CD14mono_myeloid | 86.0% |
| CD8 RO CCR5_CD8 | 85.2% |
| CCR5_CD8RO | 85.0% |
| Tconv memPD1_mem | 83.5% |
| Bcells CD27posIgDneg_total | 83.0% |
| Tconv memCXCR3_Tconv | 82.8% |
| Bcells memory_CD3neg | 81.5% |
| CD27negIgDneg_Bcells | 81.2% |
| CXCR3_CD8RO | 81.2% |
| NKCD56hi_nonTnonB | 81.2% |
| Tconv naive_total | 81.2% |
| CD4 Tconv_CD3 | 80.8% |
| CCR4_CD8RO | 80.8% |
| Tconv memCXCR3_mem | 80.8% |
| CD14+16+mono_myeloid | 80.2% |
| naive_Bcells | 80.0% |
| CD8 RO CD56_CD8 | 79.8% |
| CD8 RO CXCR3_CD3 | 79.5% |
| NKCD56hi_NK | 79.5% |
| Bcells_CD3neg | 79.5% |
| CD3hi_CD4neg | 79.5% |
| NKCD56hi_CD3neg | 79.2% |
| CD27_CD8RO | 79.2% |
| CD8 RO CXCR3_CD8 | 79.2% |
| CD8 ncytotox RO CCR4_CD8ntox | 79.2% |
| nonTnonB_CD3neg | 79.0% |
| CD8 RO Ki67_CD8 | 79.0% |
| CD8 RO CD27_CD3 | 78.8% |
| PD1_CD8RO | 78.5% |
| TIGIT_CD8RO | 78.5% |
| Tconv memCD27_mem | 78.2% |
| Bcells Ki67_CD3neg | 78.2% |
| intB7_CD8RO | 78.0% |
| CD8 RO_CD3 | 77.5% |
| Ki67_Bcells | 77.2% |
| CD56_CD8RO | 77.0% |
| CD14mono_CD3neg | 77.0% |
| Tconv memCCR6_mem | 77.0% |
| CD8 RO PD1_CD8 | 76.8% |
| Tconv memCCR6_Tconv | 76.5% |
| NK_nonTnonB | 76.5% |
| memory_Bcells | 76.5% |
| Tconv naive_Tconv | 76.5% |
| DR_CD8RO | 76.5% |
| CCR6_CD8RO | 76.5% |
| Tconv memCCR5_mem | 76.2% |
| CD8 RO CD56_CD3 | 76.2% |
| Tconv memKi67_mem | 76.2% |
| CD8 RO TIGIT_CD3 | 76.0% |
| CD4 Treg _CD3 | 75.8% |
| CD8 RO CD27_CD8 | 75.5% |
| NK Ki67_NK | 75.5% |
| NKCD16_nonTnonB | 75.2% |
| NKCD16_NK | 75.2% |
| CD14+16+mono_CD3neg | 75.0% |
| NK Ki67_nonTnonB | 75.0% |
| Ki67_CD8RO | 74.8% |
| Tconv naive_CD3 | 74.8% |
| CD8 RA CCR7 naive_CD8 | 74.8% |
| CD8 RA_CD3 | 74.8% |
| Tconv memCCR5_Tconv | 74.2% |
| NKCD16_CD3neg | 74.0% |
| Treg memory_CD3 | 73.8% |
| CD8 RO DR_CD3 | 73.0% |
| Tconv mem_Tconv | 73.0% |
| NK_CD3neg | 72.8% |
| myeloid_CD3neg | 72.8% |
| CD8 RO PD1_CD3 | 72.8% |
| CD8 RO DR_CD8 | 72.8% |
| CD8 RO CCR6_CD3 | 72.5% |
| CD8 RO CCR6_CD8 | 72.5% |
| NK Ki67_CD3neg | 72.0% |
| CD8 RO TIGIT_CD8 | 72.0% |
| Tconv memTIGIT_mem | 71.8% |
| CD8 RO intB7_CD8 | 71.0% |
| Tconv memCD56_mem | 71.0% |
| Tconv memCCR4_mem | 70.8% |
| Tconv memintB7_Tconv | 70.8% |
| Tconv memDR_mem | 70.5% |
| Bcells naive_CD3neg | 70.2% |
| Tconv memCD56_Tconv | 69.5% |
| Treg naive_CD4 | 69.5% |
| CD8 RA_CD8 | 69.0% |
| Tconv memintB7_mem | 68.8% |
| Tconv memCD27_Tconv | 68.8% |
| CD8 RA naive_CD3 | 68.5% |
| CD8 RO_CD8 | 68.5% |
| CD4neg_CD3 | 68.5% |
| CD3hi_CD3 | 68.2% |
| Tconv memCXCR3_CD3 | 67.5% |
| Tconv memPD1_Tconv | 67.5% |
| CD8  RO Ki67_CD3 | 66.8% |
| CD8 RO intB7_CD3 | 66.0% |
| Tconv memKi67_Tconv | 64.5% |
| Tconv memTIGIT_Tconv | 64.2% |
| Tconv memCCR6_CD3 | 64.0% |
| NKCD56hi_total | 63.5% |
| CD8 RO CCR5_total | 63.0% |
| Tconv memDR_Tconv | 62.7% |
| CD4 Tconv_total | 62.3% |
| Tconv memCCR4_Tconv | 62.0% |
| Tconv memCCR5_CD3 | 61.3% |
| CD8 ncytotox RO CCR4_CD3 | 61.0% |
| CD16+mono_total | 60.8% |
| Treg naive_CD3 | 58.8% |
| CD3hi_total | 57.5% |
| CD3neg_total | 57.0% |
| Tconv memPD1_CD3 | 57.0% |
| Bcells memory_total | 56.0% |
| Tconv memKi67_CD3 | 56.0% |
| Bcells Ki67_total | 55.8% |
| Bcells CD27negIgDneg_total | 54.2% |
| Tconv mem_CD3 | 52.8% |
| Bcells_total | 52.5% |
| Tconv memPD1_total | 52.2% |
| Tconv memKi67_total | 52.2% |
| Tconv memDR_CD3 | 51.7% |
| Tconv memCD56_CD3 | 51.0% |
| CD8 RO CXCR3_total | 50.2% |
| CD3pos_total | 50.0% |
| Tconv memTIGIT_CD3 | 49.2% |
| CD14mono_total | 49.0% |
| Tconv memintB7_CD3 | 49.0% |
| CD8 RO CD56_total | 48.5% |
| CD14+16+mono_total | 48.5% |
| Tconv memCD27_CD3 | 48.2% |
| nonTnonB_total | 47.2% |
| NK Ki67_total | 46.0% |
| Treg memory_total | 45.0% |
| NK_total | 44.2% |
| CD8 RO DR_total | 44.2% |
| CD8pos_total | 44.2% |
| Tconv memCCR4_CD3 | 44.0% |
| CD4 Treg_total | 43.2% |
| Tconv memCXCR3_total | 42.8% |
| myeloid_total | 42.2% |
| Tconv memDR_total | 42.0% |
| CD4 Tconv mem_total | 41.0% |
| Bcells naive_total | 40.8% |
| Tconv memCCR4_total | 40.8% |
| CD8 RO CCR6_total | 39.8% |
| NKCD16_total | 39.8% |
| CD8 RO Ki67_total | 39.2% |
| Tconv memCD27_total | 39.2% |
| CD8 RA_total | 38.0% |
| Tconv memCD56_total | 37.8% |
| CD8 RO PD1_total | 37.8% |
| Tconv memCCR6_total | 37.2% |
| CD8 RO TIGIT_total | 36.8% |
| CD8 RO CCR4_total | 35.5% |
| CD8 RO CD27_total | 34.8% |
| Tconv memCCR5_total | 34.5% |
| Tconv memTIGIT_total | 34.2% |
| CD8 RA naive_total | 32.8% |
| CD4neg_total | 32.0% |
| Treg naive_total | 30.8% |
| CD8 RO_total | 30.5% |
| CD8 RO intB7_total | 28.5% |
| Tconv memintB7_total | 27.8% |

### RF_Importance

**Base Method**: Raw feature selection frequencies across all bootstrap samples

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD8 RO CCR5_CD3 | 78.0% |
| Tconv naive_total | 75.0% |
| CD4 Treg_CD4 | 74.2% |
| CD8pos_CD3 | 73.5% |
| CD27IgD_Bcells | 70.2% |
| Bcells CD27posIgDneg_total | 70.2% |
| Treg memory_CD4 | 68.5% |
| CD16mono_CD3neg | 66.0% |
| CD4 Tconv_CD3 | 63.7% |
| CD16mono_myeloid | 60.2% |
| CD8 RO CCR5_total | 60.0% |
| CD8 RO CXCR3_CD3 | 57.2% |
| CD8 RO CCR5_CD8 | 56.8% |
| Tconv memCXCR3_Tconv | 56.0% |
| CD4 Treg _CD3 | 54.2% |
| Treg memory_CD3 | 54.2% |
| CD8 RO_CD3 | 53.8% |
| CD4 Tconv_total | 51.5% |
| Tconv naive_CD3 | 50.5% |
| CD8 RO CD56_CD3 | 49.2% |
| CCR5_CD8RO | 47.2% |
| CD8 RO CD27_CD3 | 46.8% |
| Tconv memCCR6_Tconv | 46.8% |
| CD14mono_myeloid | 46.0% |
| CD8 RA_CD3 | 45.5% |
| Tconv naive_Tconv | 45.0% |
| Tconv memCXCR3_mem | 44.8% |
| Tconv memKi67_total | 44.0% |
| CD8 RO TIGIT_CD3 | 43.8% |
| Tconv memCCR5_mem | 43.2% |
| Tconv mem_Tconv | 43.2% |
| CD8 RO DR_CD3 | 43.0% |
| CD8 RO CCR6_CD3 | 42.0% |
| Tconv memCD27_mem | 40.5% |
| CD4neg_CD3 | 40.5% |
| Tconv memCXCR3_CD3 | 40.2% |
| Tconv memCCR5_Tconv | 40.0% |
| CXCR3_CD8RO | 39.8% |
| CD8 RO CXCR3_total | 39.5% |
| Tconv memPD1_total | 39.2% |
| CD16+mono_total | 38.8% |
| NKCD56hi_total | 38.5% |
| Tconv memCCR5_CD3 | 37.2% |
| CCR4_CD8RO | 36.8% |
| Bcells memory_CD3neg | 36.8% |
| CD8 RA naive_CD3 | 36.5% |
| CD3pos_total | 36.5% |
| Tconv memPD1_mem | 36.5% |
| CD8 RO CXCR3_CD8 | 36.2% |
| CD3neg_total | 35.2% |
| CD8  RO Ki67_CD3 | 35.2% |
| NKCD56hi_nonTnonB | 34.8% |
| CD8 RO CD56_CD8 | 34.5% |
| Tconv memCCR4_total | 34.5% |
| CD8 RO PD1_CD3 | 32.8% |
| NKCD56hi_CD3neg | 31.8% |
| Treg naive_CD4 | 31.8% |
| nonTnonB_total | 31.8% |
| CD8 RO CD56_total | 31.5% |
| Tconv memKi67_mem | 31.5% |
| CD27negIgDneg_Bcells | 30.8% |
| Bcells_CD3neg | 30.5% |
| nonTnonB_CD3neg | 30.5% |
| CD3hi_total | 30.2% |
| CD8 RO intB7_CD3 | 30.2% |
| Tconv memCD27_Tconv | 30.0% |
| Tconv memCCR6_mem | 29.8% |
| Tconv memintB7_Tconv | 29.8% |
| Tconv memCCR4_mem | 29.2% |
| Tconv memDR_total | 28.7% |
| CD3hi_CD3 | 28.5% |
| Tconv memCD27_total | 28.5% |
| Tconv memPD1_CD3 | 28.2% |
| CD4 Treg_total | 27.5% |
| CD4 Tconv mem_total | 27.5% |
| Tconv memCXCR3_total | 27.5% |
| Tconv memCCR6_CD3 | 27.3% |
| Bcells CD27negIgDneg_total | 27.0% |
| CD8pos_total | 27.0% |
| CD8 RO DR_total | 26.8% |
| CD14+16+mono_myeloid | 26.5% |
| Tconv memTIGIT_mem | 26.5% |
| Bcells memory_total | 25.8% |
| Tconv memTIGIT_total | 25.8% |
| Ki67_CD8RO | 25.5% |
| Bcells Ki67_total | 25.5% |
| Bcells Ki67_CD3neg | 25.2% |
| CD8 RO Ki67_CD8 | 25.0% |
| Tconv memCCR5_total | 24.2% |
| Treg naive_CD3 | 23.8% |
| CD3hi_CD4neg | 23.8% |
| Bcells_total | 23.5% |
| CD14mono_total | 23.5% |
| Tconv memKi67_CD3 | 23.5% |
| TIGIT_CD8RO | 23.2% |
| DR_CD8RO | 23.2% |
| Tconv memCD56_Tconv | 23.0% |
| NK_CD3neg | 23.0% |
| CD27_CD8RO | 22.8% |
| Tconv memCD56_total | 22.8% |
| Tconv memCD56_mem | 22.2% |
| intB7_CD8RO | 22.0% |
| Tconv memCCR4_Tconv | 22.0% |
| CD8 RA CCR7 naive_CD8 | 22.0% |
| CD14+16+mono_total | 21.5% |
| Ki67_Bcells | 21.5% |
| NKCD56hi_NK | 21.2% |
| CD8 ncytotox RO CCR4_CD8ntox | 21.2% |
| NK Ki67_total | 21.0% |
| Treg memory_total | 20.8% |
| Tconv mem_CD3 | 20.5% |
| Tconv memDR_CD3 | 20.5% |
| Tconv memCCR6_total | 20.2% |
| Treg naive_total | 20.2% |
| CD8 RO CCR6_total | 20.2% |
| Tconv memintB7_CD3 | 20.2% |
| CD8 RO DR_CD8 | 20.2% |
| CD8 RO CD27_CD8 | 20.0% |
| Tconv memCD27_CD3 | 20.0% |
| CD8 RA_total | 19.5% |
| Tconv memPD1_Tconv | 19.2% |
| CD56_CD8RO | 19.2% |
| NK Ki67_nonTnonB | 19.0% |
| NKCD16_CD3neg | 18.8% |
| NK Ki67_NK | 18.5% |
| CD8 RO TIGIT_CD8 | 18.2% |
| CD8 RO CD27_total | 18.2% |
| NKCD16_total | 18.0% |
| Tconv memDR_Tconv | 17.8% |
| CD8 RO TIGIT_total | 17.8% |
| CD8 RO PD1_total | 17.8% |
| Tconv memTIGIT_Tconv | 17.5% |
| NK_total | 17.5% |
| CD4neg_total | 17.2% |
| CCR6_CD8RO | 17.2% |
| NKCD16_NK | 17.2% |
| naive_Bcells | 17.2% |
| myeloid_CD3neg | 17.0% |
| PD1_CD8RO | 17.0% |
| CD8 ncytotox RO CCR4_CD3 | 16.8% |
| CD8 RO PD1_CD8 | 16.8% |
| Tconv memDR_mem | 16.5% |
| Tconv memCD56_CD3 | 16.2% |
| CD8 RO intB7_CD8 | 16.0% |
| CD8 RO CCR4_total | 15.8% |
| CD8 RO Ki67_total | 15.5% |
| CD14+16+mono_CD3neg | 15.2% |
| CD8 RO CCR6_CD8 | 15.2% |
| NK_nonTnonB | 15.0% |
| Tconv memKi67_Tconv | 15.0% |
| Tconv memintB7_total | 15.0% |
| CD8 RA naive_total | 14.8% |
| CD8 RA_CD8 | 14.8% |
| Tconv memintB7_mem | 14.8% |
| NKCD16_nonTnonB | 14.8% |
| CD8 RO_total | 14.5% |
| CD14mono_CD3neg | 14.5% |
| myeloid_total | 13.8% |
| CD8 RO_CD8 | 13.5% |
| NK Ki67_CD3neg | 12.2% |
| memory_Bcells | 11.8% |
| Bcells naive_CD3neg | 10.5% |
| Tconv memCCR4_CD3 | 10.0% |
| CD8 RO intB7_total | 9.2% |
| Bcells naive_total | 9.0% |
| Tconv memTIGIT_CD3 | 8.2% |

### RandomForest_Permutation_AboveMean

**Base Method**: Raw feature selection frequencies across all bootstrap samples

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD8pos_CD3 | 5.5% |
| CD4 Treg_CD4 | 5.2% |
| CD4 Tconv_CD3 | 5.0% |
| CD4neg_CD3 | 5.0% |
| CD4 Treg _CD3 | 4.8% |
| Tconv memPD1_total | 4.8% |
| Bcells CD27posIgDneg_total | 4.8% |
| Tconv naive_total | 4.5% |
| Tconv memCCR6_Tconv | 4.5% |
| CD16mono_CD3neg | 4.2% |
| Tconv memCCR5_Tconv | 4.2% |
| CD8 RO CCR5_total | 4.2% |
| CD8 RO CD27_CD3 | 4.0% |
| CD27IgD_Bcells | 4.0% |
| CD16+mono_total | 4.0% |
| Tconv naive_Tconv | 4.0% |
| Tconv memKi67_CD3 | 3.8% |
| Tconv memCCR5_mem | 3.8% |
| CD8 RO CCR5_CD3 | 3.8% |
| Tconv memKi67_total | 3.8% |
| CD16mono_myeloid | 3.8% |
| CD8 RO_CD3 | 3.5% |
| CCR4_CD8RO | 3.5% |
| Tconv memKi67_mem | 3.5% |
| Tconv memCXCR3_Tconv | 3.5% |
| CD8 RO intB7_CD3 | 3.5% |
| nonTnonB_total | 3.5% |
| Treg memory_CD4 | 3.5% |
| Bcells_total | 3.5% |
| CD4 Tconv_total | 3.2% |
| NKCD16_CD3neg | 3.2% |
| Tconv memCCR5_CD3 | 3.2% |
| NKCD56hi_total | 3.2% |
| CD8 RO CD56_total | 3.2% |
| Tconv memDR_total | 3.2% |
| Treg memory_CD3 | 3.2% |
| CD3neg_total | 3.2% |
| nonTnonB_CD3neg | 3.2% |
| CXCR3_CD8RO | 3.2% |
| NKCD56hi_nonTnonB | 3.2% |
| CD8 RO CD56_CD3 | 3.2% |
| CD8 RO CXCR3_CD8 | 3.2% |
| Tconv memCD56_mem | 3.0% |
| Treg memory_total | 3.0% |
| Tconv memPD1_Tconv | 3.0% |
| Tconv memCXCR3_CD3 | 3.0% |
| CD8 RA_total | 3.0% |
| Tconv memCXCR3_mem | 3.0% |
| CD4neg_total | 3.0% |
| Bcells CD27negIgDneg_total | 3.0% |
| CD8 RO_total | 3.0% |
| Tconv memCD27_mem | 2.8% |
| CD8 RO CCR5_CD8 | 2.8% |
| Bcells Ki67_total | 2.8% |
| CD8 RO CXCR3_CD3 | 2.8% |
| CD14+16+mono_myeloid | 2.8% |
| CD27negIgDneg_Bcells | 2.8% |
| CD8 RA naive_CD3 | 2.8% |
| CD27_CD8RO | 2.8% |
| CD8 RO PD1_CD3 | 2.8% |
| CCR5_CD8RO | 2.8% |
| CD3hi_CD3 | 2.8% |
| Tconv memCCR6_CD3 | 2.8% |
| Tconv memCCR4_total | 2.8% |
| CD8 RO TIGIT_CD3 | 2.8% |
| CD8 RO CD56_CD8 | 2.8% |
| Tconv memintB7_Tconv | 2.8% |
| Treg naive_CD3 | 2.8% |
| PD1_CD8RO | 2.8% |
| Tconv memCCR5_total | 2.8% |
| Tconv memCCR6_total | 2.8% |
| intB7_CD8RO | 2.8% |
| TIGIT_CD8RO | 2.8% |
| Tconv naive_CD3 | 2.8% |
| CD14mono_myeloid | 2.5% |
| Tconv memTIGIT_total | 2.5% |
| CD8 RO Ki67_total | 2.5% |
| CD8 RO DR_CD3 | 2.5% |
| CD8 RO CCR6_CD3 | 2.5% |
| Tconv memCD56_Tconv | 2.5% |
| Tconv mem_Tconv | 2.5% |
| Bcells naive_CD3neg | 2.5% |
| myeloid_CD3neg | 2.5% |
| Tconv memCD27_total | 2.5% |
| Tconv memDR_mem | 2.5% |
| CD3pos_total | 2.5% |
| Tconv memCXCR3_total | 2.5% |
| CD8 RO PD1_total | 2.2% |
| DR_CD8RO | 2.2% |
| NK_CD3neg | 2.2% |
| CD8 ncytotox RO CCR4_CD8ntox | 2.2% |
| Treg naive_CD4 | 2.2% |
| CD8 RO CD27_total | 2.2% |
| Tconv memPD1_mem | 2.2% |
| Tconv memintB7_mem | 2.2% |
| Tconv memPD1_CD3 | 2.2% |
| Tconv memCCR4_mem | 2.2% |
| CD14mono_CD3neg | 2.2% |
| Tconv mem_CD3 | 2.2% |
| Tconv memKi67_Tconv | 2.2% |
| CD8 RO TIGIT_CD8 | 2.2% |
| NK_total | 2.2% |
| myeloid_total | 2.2% |
| Tconv memCCR4_Tconv | 2.2% |
| CD8 RO CXCR3_total | 2.2% |
| CD8 RA_CD3 | 2.0% |
| NKCD56hi_CD3neg | 2.0% |
| Tconv memCD56_CD3 | 2.0% |
| NK Ki67_nonTnonB | 2.0% |
| CD4 Tconv mem_total | 2.0% |
| Tconv memCD27_Tconv | 2.0% |
| CD8 RA CCR7 naive_CD8 | 2.0% |
| Tconv memCD27_CD3 | 2.0% |
| CD8 RO DR_total | 2.0% |
| naive_Bcells | 2.0% |
| Ki67_Bcells | 2.0% |
| CD8 RO CCR6_CD8 | 2.0% |
| CD8 RO DR_CD8 | 2.0% |
| memory_Bcells | 2.0% |
| CD3hi_total | 2.0% |
| CD8  RO Ki67_CD3 | 2.0% |
| CD14mono_total | 2.0% |
| Tconv memCD56_total | 2.0% |
| Ki67_CD8RO | 2.0% |
| NKCD56hi_NK | 1.8% |
| CD4 Treg_total | 1.8% |
| Bcells_CD3neg | 1.8% |
| NK Ki67_CD3neg | 1.8% |
| Tconv memintB7_CD3 | 1.8% |
| CD14+16+mono_CD3neg | 1.8% |
| CD8 RO CD27_CD8 | 1.8% |
| CD8 RO intB7_CD8 | 1.8% |
| CD8 RO CCR6_total | 1.8% |
| Tconv memDR_CD3 | 1.8% |
| CD8pos_total | 1.8% |
| CD8 RO Ki67_CD8 | 1.8% |
| CD8 RO_CD8 | 1.8% |
| CD3hi_CD4neg | 1.8% |
| Bcells memory_CD3neg | 1.8% |
| CD8 RO CCR4_total | 1.8% |
| Bcells memory_total | 1.5% |
| Bcells naive_total | 1.5% |
| Tconv memCCR4_CD3 | 1.5% |
| CCR6_CD8RO | 1.5% |
| CD14+16+mono_total | 1.5% |
| Tconv memTIGIT_CD3 | 1.5% |
| NK Ki67_total | 1.5% |
| Tconv memTIGIT_mem | 1.2% |
| Tconv memintB7_total | 1.2% |
| CD8 ncytotox RO CCR4_CD3 | 1.2% |
| Tconv memTIGIT_Tconv | 1.2% |
| Tconv memCCR6_mem | 1.2% |
| CD56_CD8RO | 1.2% |
| CD8 RO PD1_CD8 | 1.2% |
| Treg naive_total | 1.2% |
| NKCD16_NK | 1.2% |
| CD8 RA naive_total | 1.2% |
| Bcells Ki67_CD3neg | 1.2% |
| CD8 RO intB7_total | 1.2% |
| NK Ki67_NK | 1.2% |
| NK_nonTnonB | 1.0% |
| CD8 RA_CD8 | 1.0% |
| NKCD16_total | 0.8% |
| Tconv memDR_Tconv | 0.8% |
| NKCD16_nonTnonB | 0.8% |
| CD8 RO TIGIT_total | 0.5% |

### RandomForest_Permutation_Top10%

**Base Method**: Raw feature selection frequencies across all bootstrap samples

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Tconv memintB7_total | 92.5% |
| Tconv memCD27_total | 92.5% |
| Tconv memKi67_total | 92.5% |
| Tconv memCD56_total | 92.0% |
| Tconv naive_total | 90.8% |
| Tconv memPD1_total | 90.5% |
| Tconv memDR_total | 89.5% |
| Tconv memCXCR3_total | 87.5% |
| CD4 Treg_total | 83.2% |
| Tconv memTIGIT_total | 77.8% |
| CD3pos_total | 71.0% |
| CD4 Tconv mem_total | 68.0% |
| Tconv memCCR6_total | 58.5% |
| Tconv memCCR4_total | 57.2% |
| CD4 Tconv_total | 56.8% |
| Tconv memCCR5_total | 50.7% |
| CD8pos_CD3 | 5.5% |
| CD4 Treg_CD4 | 5.2% |
| Bcells CD27posIgDneg_total | 4.8% |
| CD4neg_CD3 | 4.8% |
| CD4 Treg _CD3 | 4.5% |
| Tconv memCCR5_Tconv | 4.2% |
| CD4 Tconv_CD3 | 4.2% |
| CD16mono_CD3neg | 4.2% |
| Tconv memCCR6_Tconv | 4.2% |
| Tconv naive_Tconv | 4.0% |
| CD27IgD_Bcells | 4.0% |
| CD8 RO CCR5_total | 4.0% |
| CD8 RO CD27_CD3 | 4.0% |
| Tconv memKi67_mem | 3.8% |
| CD16+mono_total | 3.8% |
| CD8 RO_CD3 | 3.5% |
| CD8 RO CCR5_CD3 | 3.5% |
| CD8 RO CD56_total | 3.5% |
| CCR4_CD8RO | 3.5% |
| nonTnonB_total | 3.5% |
| CD16mono_myeloid | 3.5% |
| Treg memory_CD4 | 3.5% |
| CXCR3_CD8RO | 3.2% |
| Tconv memCXCR3_Tconv | 3.2% |
| NKCD56hi_nonTnonB | 3.2% |
| CD8 RO intB7_CD3 | 3.2% |
| Tconv memCCR5_mem | 3.2% |
| CD8 RO CD56_CD3 | 3.2% |
| CD8 RO CXCR3_CD8 | 3.0% |
| Treg memory_CD3 | 3.0% |
| CD8 RO_total | 3.0% |
| CD3neg_total | 3.0% |
| NKCD16_CD3neg | 3.0% |
| Tconv memKi67_CD3 | 3.0% |
| Bcells_total | 3.0% |
| NKCD56hi_total | 3.0% |
| CD8 RA naive_CD3 | 2.8% |
| CD8 RO CXCR3_CD3 | 2.8% |
| Treg memory_total | 2.8% |
| Tconv memCXCR3_mem | 2.8% |
| Bcells CD27negIgDneg_total | 2.8% |
| intB7_CD8RO | 2.8% |
| Tconv memCCR5_CD3 | 2.8% |
| Tconv naive_CD3 | 2.8% |
| CD4neg_total | 2.8% |
| Tconv memCD27_mem | 2.8% |
| Tconv memintB7_Tconv | 2.8% |
| Tconv memCD56_mem | 2.8% |
| CD8 RO CD56_CD8 | 2.8% |
| CD8 RO TIGIT_CD3 | 2.8% |
| CCR5_CD8RO | 2.8% |
| nonTnonB_CD3neg | 2.8% |
| myeloid_CD3neg | 2.5% |
| CD8 RO Ki67_total | 2.5% |
| CD8 RO CCR6_CD3 | 2.5% |
| CD3hi_CD3 | 2.5% |
| CD8 RO TIGIT_CD8 | 2.5% |
| CD8 RA_total | 2.5% |
| CD8 RO PD1_CD3 | 2.5% |
| CD14mono_myeloid | 2.5% |
| CD27_CD8RO | 2.5% |
| PD1_CD8RO | 2.5% |
| Tconv memCXCR3_CD3 | 2.5% |
| CD8 ncytotox RO CCR4_CD8ntox | 2.5% |
| Tconv memPD1_mem | 2.2% |
| CD14mono_CD3neg | 2.2% |
| DR_CD8RO | 2.2% |
| Bcells naive_CD3neg | 2.2% |
| Tconv memDR_mem | 2.2% |
| Tconv memCCR4_mem | 2.2% |
| CD8 RO DR_CD3 | 2.2% |
| TIGIT_CD8RO | 2.2% |
| CD14+16+mono_myeloid | 2.2% |
| CD8 RA_CD3 | 2.2% |
| CD8 RO CXCR3_total | 2.2% |
| Tconv memCCR6_CD3 | 2.2% |
| Treg naive_CD3 | 2.2% |
| CD27negIgDneg_Bcells | 2.2% |
| CD8 RO CD27_total | 2.2% |
| CD8 RO CCR5_CD8 | 2.2% |
| Tconv memCD27_Tconv | 2.0% |
| NKCD56hi_CD3neg | 2.0% |
| Tconv memPD1_CD3 | 2.0% |
| CD8 RO DR_CD8 | 2.0% |
| NK Ki67_nonTnonB | 2.0% |
| CD8 RA CCR7 naive_CD8 | 2.0% |
| Bcells Ki67_total | 2.0% |
| NK_CD3neg | 2.0% |
| NK_total | 2.0% |
| CD8 RO DR_total | 2.0% |
| Tconv memCCR4_Tconv | 2.0% |
| CD8 RO PD1_total | 2.0% |
| Tconv memCD56_Tconv | 2.0% |
| myeloid_total | 2.0% |
| Tconv memPD1_Tconv | 2.0% |
| Tconv memintB7_mem | 1.8% |
| NKCD56hi_NK | 1.8% |
| Tconv memCD56_CD3 | 1.8% |
| CD8 RO CD27_CD8 | 1.8% |
| Ki67_Bcells | 1.8% |
| CD8 RO intB7_CD8 | 1.8% |
| Treg naive_CD4 | 1.8% |
| CD8 RO CCR6_total | 1.8% |
| CD14mono_total | 1.8% |
| Tconv memCD27_CD3 | 1.8% |
| Ki67_CD8RO | 1.8% |
| Tconv memCCR6_mem | 1.8% |
| Tconv memDR_CD3 | 1.8% |
| CD8  RO Ki67_CD3 | 1.8% |
| CD3hi_total | 1.5% |
| Tconv memCCR4_CD3 | 1.5% |
| CD8 RO CCR6_CD8 | 1.5% |
| CD14+16+mono_CD3neg | 1.5% |
| Bcells_CD3neg | 1.5% |
| NK Ki67_total | 1.5% |
| Tconv memTIGIT_Tconv | 1.5% |
| Tconv mem_CD3 | 1.5% |
| Tconv memKi67_Tconv | 1.5% |
| Tconv mem_Tconv | 1.5% |
| NK Ki67_CD3neg | 1.5% |
| CD8 RO CCR4_total | 1.5% |
| Tconv memTIGIT_CD3 | 1.5% |
| CD8 RO Ki67_CD8 | 1.5% |
| Bcells memory_total | 1.5% |
| CD8pos_total | 1.5% |
| memory_Bcells | 1.5% |
| naive_Bcells | 1.5% |
| Bcells memory_CD3neg | 1.5% |
| CD3hi_CD4neg | 1.5% |
| Tconv memTIGIT_mem | 1.2% |
| CD8 RO intB7_total | 1.2% |
| NK Ki67_NK | 1.2% |
| Tconv memintB7_CD3 | 1.2% |
| CCR6_CD8RO | 1.2% |
| CD8 RO_CD8 | 1.2% |
| Bcells Ki67_CD3neg | 1.2% |
| CD8 RO PD1_CD8 | 1.2% |
| CD56_CD8RO | 1.2% |
| CD8 ncytotox RO CCR4_CD3 | 1.0% |
| Bcells naive_total | 1.0% |
| Tconv memDR_Tconv | 1.0% |
| CD8 RA naive_total | 1.0% |
| CD8 RA_CD8 | 1.0% |
| Treg naive_total | 1.0% |
| NKCD16_nonTnonB | 0.8% |
| CD14+16+mono_total | 0.8% |
| NKCD16_NK | 0.8% |
| NK_nonTnonB | 0.8% |
| CD8 RO TIGIT_total | 0.5% |
| NKCD16_total | 0.5% |

### Ridge_Strict

**Base Method**: Raw feature selection frequencies across all bootstrap samples

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CCR4_CD8RO | 82.5% |
| CD3hi_total | 75.2% |
| DR_CD8RO | 75.0% |
| CD14mono_myeloid | 74.2% |
| Tconv memKi67_Tconv | 74.2% |
| CD8 ncytotox RO CCR4_CD8ntox | 73.0% |
| NKCD56hi_nonTnonB | 72.0% |
| CD3hi_CD4neg | 71.0% |
| Tconv memPD1_mem | 71.0% |
| CD27negIgDneg_Bcells | 71.0% |
| Tconv memKi67_CD3 | 70.2% |
| CD27IgD_Bcells | 69.0% |
| CD16mono_myeloid | 66.5% |
| Tconv memKi67_total | 63.2% |
| CD8 RO CXCR3_CD8 | 62.7% |
| CD14+16+mono_myeloid | 61.0% |
| Tconv memCCR6_mem | 60.8% |
| CD8pos_CD3 | 60.0% |
| CD8 RO DR_CD8 | 59.0% |
| CD8 RA_CD3 | 58.2% |
| NKCD56hi_total | 57.8% |
| CD3hi_CD3 | 57.8% |
| CD8 RA_total | 57.8% |
| Bcells CD27negIgDneg_total | 57.8% |
| Ki67_CD8RO | 57.2% |
| NKCD56hi_CD3neg | 57.2% |
| Bcells CD27posIgDneg_total | 57.2% |
| Tconv memKi67_mem | 57.0% |
| Tconv memCXCR3_total | 56.8% |
| TIGIT_CD8RO | 55.5% |
| Tconv memTIGIT_mem | 55.0% |
| CD8 RO CCR6_CD8 | 54.8% |
| Tconv memCD27_mem | 54.5% |
| CD8 RA CCR7 naive_CD8 | 54.2% |
| intB7_CD8RO | 53.2% |
| Treg naive_total | 52.2% |
| Tconv memPD1_Tconv | 51.7% |
| Tconv memTIGIT_CD3 | 51.5% |
| Tconv memTIGIT_Tconv | 51.5% |
| Tconv memCCR6_CD3 | 51.2% |
| CD8 RO TIGIT_CD3 | 51.0% |
| CD8 RO CXCR3_CD3 | 50.7% |
| CD16+mono_total | 50.5% |
| Tconv memCCR4_mem | 50.5% |
| CD14+16+mono_CD3neg | 49.8% |
| CD8 RO intB7_CD8 | 49.8% |
| CD8 RO CCR5_CD8 | 49.5% |
| memory_Bcells | 49.2% |
| Tconv memPD1_CD3 | 48.5% |
| Treg memory_total | 48.0% |
| Ki67_Bcells | 48.0% |
| CD8 RO CCR6_CD3 | 47.8% |
| CD8 RA naive_total | 47.5% |
| CCR5_CD8RO | 47.2% |
| CD8 RO Ki67_CD8 | 47.2% |
| CCR6_CD8RO | 47.2% |
| Tconv memCXCR3_Tconv | 47.2% |
| Bcells memory_total | 46.0% |
| Tconv memCXCR3_CD3 | 46.0% |
| Bcells Ki67_total | 45.8% |
| CXCR3_CD8RO | 45.8% |
| Tconv memCCR6_Tconv | 45.5% |
| Tconv memCCR6_total | 45.5% |
| CD4neg_total | 45.2% |
| Treg naive_CD3 | 45.2% |
| CD8 RO CCR6_total | 45.0% |
| Bcells Ki67_CD3neg | 45.0% |
| CD8 RO Ki67_total | 44.8% |
| CD14+16+mono_total | 44.0% |
| CD56_CD8RO | 44.0% |
| CD27_CD8RO | 44.0% |
| CD8 RO CCR4_total | 43.5% |
| CD8 RO CCR5_CD3 | 43.2% |
| NK Ki67_nonTnonB | 43.2% |
| CD16mono_CD3neg | 43.0% |
| Tconv memintB7_mem | 42.8% |
| CD8 RA naive_CD3 | 42.8% |
| CD8 RO CCR5_total | 42.8% |
| CD8 RO CD56_CD8 | 42.5% |
| CD8 RO TIGIT_CD8 | 42.5% |
| NKCD56hi_NK | 42.2% |
| CD4neg_CD3 | 42.2% |
| CD8 RO PD1_total | 41.8% |
| NK Ki67_NK | 41.8% |
| Tconv memTIGIT_total | 41.5% |
| Bcells memory_CD3neg | 41.2% |
| Tconv memDR_mem | 40.8% |
| NKCD16_NK | 40.8% |
| Tconv memintB7_total | 40.5% |
| Treg naive_CD4 | 39.5% |
| CD8 RO PD1_CD8 | 39.5% |
| CD8 RO_CD3 | 38.8% |
| Tconv memCD56_total | 38.2% |
| CD8 RO CD27_CD3 | 38.2% |
| Tconv memCCR5_total | 38.0% |
| naive_Bcells | 37.2% |
| Tconv memDR_CD3 | 37.0% |
| CD8 RO CXCR3_total | 37.0% |
| CD4 Treg_total | 36.5% |
| Tconv naive_total | 36.2% |
| Treg memory_CD4 | 36.2% |
| NK Ki67_total | 35.8% |
| Treg memory_CD3 | 35.2% |
| CD8 RO PD1_CD3 | 35.2% |
| Bcells_total | 34.8% |
| Tconv memintB7_Tconv | 34.8% |
| PD1_CD8RO | 34.8% |
| Tconv memintB7_CD3 | 34.8% |
| Tconv memCCR5_mem | 34.5% |
| NK Ki67_CD3neg | 34.2% |
| Tconv memCD27_total | 34.2% |
| Tconv memPD1_total | 34.2% |
| Tconv mem_Tconv | 33.8% |
| Tconv memCXCR3_mem | 33.0% |
| CD8 RO intB7_total | 32.8% |
| nonTnonB_CD3neg | 32.5% |
| CD4 Tconv_total | 32.2% |
| Bcells_CD3neg | 31.8% |
| CD4 Tconv_CD3 | 31.5% |
| CD8pos_total | 31.0% |
| Tconv memDR_total | 31.0% |
| CD4 Treg_CD4 | 31.0% |
| Tconv memDR_Tconv | 30.8% |
| Bcells naive_CD3neg | 30.5% |
| Tconv naive_CD3 | 30.2% |
| Bcells naive_total | 29.5% |
| CD8 RO CD56_total | 29.0% |
| CD4 Treg _CD3 | 28.7% |
| CD8 ncytotox RO CCR4_CD3 | 27.8% |
| Tconv memCCR5_CD3 | 27.5% |
| CD8 RO CD27_CD8 | 27.3% |
| CD8  RO Ki67_CD3 | 26.8% |
| Tconv naive_Tconv | 25.8% |
| CD3neg_total | 25.5% |
| CD3pos_total | 25.5% |
| Tconv memCCR5_Tconv | 25.0% |
| CD8 RO intB7_CD3 | 24.5% |
| Tconv memCCR4_Tconv | 24.5% |
| Tconv memCD27_CD3 | 24.2% |
| CD8 RO TIGIT_total | 24.2% |
| Tconv memCD27_Tconv | 24.0% |
| CD8 RO CD56_CD3 | 23.8% |
| Tconv memCD56_mem | 23.8% |
| NK_total | 23.0% |
| NKCD16_total | 22.2% |
| Tconv memCD56_CD3 | 22.0% |
| Tconv memCD56_Tconv | 21.8% |
| CD8 RO DR_CD3 | 21.0% |
| Tconv mem_CD3 | 20.2% |
| Tconv memCCR4_CD3 | 20.0% |
| CD14mono_CD3neg | 19.8% |
| CD8 RA_CD8 | 19.2% |
| CD8 RO CD27_total | 19.0% |
| Tconv memCCR4_total | 17.5% |
| CD8 RO DR_total | 17.0% |
| myeloid_CD3neg | 16.2% |
| CD4 Tconv mem_total | 15.2% |
| CD8 RO_CD8 | 14.2% |
| NKCD16_nonTnonB | 13.8% |
| NK_nonTnonB | 13.5% |
| CD8 RO_total | 12.2% |
| CD14mono_total | 12.0% |
| NKCD16_CD3neg | 11.0% |
| NK_CD3neg | 8.8% |
| myeloid_total | 7.0% |
| nonTnonB_total | 4.8% |

### SVM_RBF_Permutation_AboveMean

**Base Method**: Raw feature selection frequencies across all bootstrap samples

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CCR4_CD8RO | 35.5% |
| Tconv memPD1_mem | 28.9% |
| CD8 ncytotox RO CCR4_CD8ntox | 27.9% |
| DR_CD8RO | 27.1% |
| CD3hi_total | 27.1% |
| CD3hi_CD4neg | 27.1% |
| CD27IgD_Bcells | 26.1% |
| CD8 RO DR_CD8 | 26.1% |
| Tconv memCCR6_mem | 25.5% |
| Treg memory_total | 24.5% |
| CD16mono_myeloid | 24.5% |
| TIGIT_CD8RO | 24.2% |
| Bcells memory_total | 24.2% |
| CD8 RO intB7_CD3 | 24.2% |
| CD16mono_CD3neg | 23.9% |
| CD3neg_total | 23.7% |
| CD3hi_CD3 | 23.7% |
| Tconv memCCR4_mem | 23.7% |
| CD3pos_total | 23.7% |
| Bcells CD27negIgDneg_total | 23.4% |
| NKCD16_CD3neg | 23.4% |
| Tconv memCCR6_CD3 | 23.2% |
| Tconv memKi67_total | 22.9% |
| CD8 RO PD1_CD3 | 22.9% |
| CD8 RO intB7_total | 22.6% |
| CD4 Treg_total | 22.6% |
| NK_CD3neg | 22.6% |
| memory_Bcells | 22.6% |
| CD8 RO PD1_total | 22.4% |
| Tconv memPD1_CD3 | 22.4% |
| CD8 RA CCR7 naive_CD8 | 22.4% |
| Tconv memTIGIT_mem | 22.4% |
| NKCD16_nonTnonB | 22.1% |
| NK_nonTnonB | 22.1% |
| Tconv memKi67_Tconv | 22.1% |
| CD8 RO CCR4_total | 22.1% |
| Bcells Ki67_total | 22.1% |
| Tconv memDR_CD3 | 21.8% |
| Tconv memCXCR3_Tconv | 21.8% |
| Tconv memCXCR3_total | 21.8% |
| CD8 RO intB7_CD8 | 21.8% |
| Ki67_CD8RO | 21.6% |
| CD8 RO DR_CD3 | 21.6% |
| intB7_CD8RO | 21.6% |
| Tconv memKi67_CD3 | 21.6% |
| CD14+16+mono_total | 21.6% |
| Bcells memory_CD3neg | 21.3% |
| Tconv memCD27_CD3 | 21.3% |
| Tconv memCCR4_total | 21.3% |
| Bcells CD27posIgDneg_total | 21.3% |
| Tconv memKi67_mem | 21.3% |
| Tconv memPD1_Tconv | 21.3% |
| CD8 RA_total | 21.3% |
| nonTnonB_total | 21.3% |
| CD8 RO CCR6_CD8 | 21.1% |
| Tconv memPD1_total | 21.1% |
| CD16+mono_total | 21.1% |
| CD8 RO Ki67_CD8 | 21.1% |
| CD8 ncytotox RO CCR4_CD3 | 21.1% |
| CD8 RO TIGIT_CD8 | 21.1% |
| CD14+16+mono_myeloid | 21.1% |
| Tconv memCD27_total | 20.8% |
| CD14+16+mono_CD3neg | 20.8% |
| CD8 RA naive_total | 20.8% |
| Tconv memTIGIT_CD3 | 20.8% |
| Tconv memCXCR3_mem | 20.5% |
| Tconv mem_CD3 | 20.5% |
| CD8 RO PD1_CD8 | 20.5% |
| Tconv memCCR5_total | 20.3% |
| myeloid_total | 20.3% |
| CCR6_CD8RO | 20.3% |
| Treg naive_total | 20.3% |
| CD14mono_myeloid | 20.3% |
| Tconv memCXCR3_CD3 | 20.3% |
| NK Ki67_CD3neg | 20.3% |
| NKCD16_NK | 20.3% |
| CD8 RO CXCR3_CD8 | 20.3% |
| Tconv memCCR6_total | 20.3% |
| CD8 RO CD56_CD8 | 20.0% |
| Tconv memDR_total | 20.0% |
| Tconv memDR_mem | 20.0% |
| Bcells Ki67_CD3neg | 20.0% |
| Tconv memCCR4_CD3 | 20.0% |
| Bcells_total | 20.0% |
| Tconv memCD56_mem | 19.7% |
| Tconv memintB7_mem | 19.7% |
| CD56_CD8RO | 19.7% |
| CD8 RA naive_CD3 | 19.7% |
| CD4neg_total | 19.7% |
| CD8  RO Ki67_CD3 | 19.7% |
| NKCD56hi_CD3neg | 19.7% |
| CD4 Tconv mem_total | 19.5% |
| CD8 RO DR_total | 19.5% |
| CD4 Tconv_total | 19.5% |
| Tconv memintB7_total | 19.5% |
| Tconv memCD27_mem | 19.5% |
| NK_total | 19.5% |
| NKCD16_total | 19.5% |
| Tconv memCD56_total | 19.2% |
| CD8 RO CD56_total | 19.2% |
| CXCR3_CD8RO | 19.2% |
| Bcells naive_total | 19.2% |
| CD8 RO Ki67_total | 19.2% |
| CD8 RO CD27_CD8 | 19.2% |
| NKCD56hi_NK | 18.9% |
| CD8 RO TIGIT_CD3 | 18.9% |
| CD8 RO CD27_CD3 | 18.9% |
| myeloid_CD3neg | 18.9% |
| CD8 RO CD27_total | 18.9% |
| Treg naive_CD3 | 18.9% |
| Tconv memCD27_Tconv | 18.9% |
| CD14mono_total | 18.9% |
| Tconv memDR_Tconv | 18.7% |
| Tconv memTIGIT_total | 18.7% |
| CD14mono_CD3neg | 18.7% |
| CD8 RO CXCR3_CD3 | 18.7% |
| Ki67_Bcells | 18.7% |
| CD8 RO CCR6_total | 18.7% |
| CD8 RO_CD8 | 18.4% |
| CD8 RO CCR6_CD3 | 18.4% |
| naive_Bcells | 18.4% |
| NK Ki67_nonTnonB | 18.4% |
| Bcells_CD3neg | 18.4% |
| NKCD56hi_nonTnonB | 18.4% |
| NK Ki67_total | 18.4% |
| Tconv memCD56_CD3 | 18.4% |
| CD8 RO CXCR3_total | 18.4% |
| Tconv memTIGIT_Tconv | 18.4% |
| PD1_CD8RO | 18.4% |
| CD27negIgDneg_Bcells | 18.2% |
| Tconv memCCR6_Tconv | 18.2% |
| nonTnonB_CD3neg | 18.2% |
| Bcells naive_CD3neg | 18.2% |
| CD8 RA_CD8 | 18.2% |
| CD8 RO TIGIT_total | 18.2% |
| NK Ki67_NK | 18.2% |
| NKCD56hi_total | 17.9% |
| Tconv naive_total | 17.9% |
| CD8 RA_CD3 | 17.9% |
| CD4neg_CD3 | 17.6% |
| CD4 Treg _CD3 | 17.6% |
| Tconv memintB7_CD3 | 17.6% |
| CD8 RO_total | 17.6% |
| CD8 RO_CD3 | 17.4% |
| Tconv memintB7_Tconv | 17.4% |
| CD8 RO CCR5_total | 17.4% |
| Tconv memCD56_Tconv | 17.1% |
| Tconv memCCR5_Tconv | 17.1% |
| CD27_CD8RO | 17.1% |
| CD8 RO CCR5_CD3 | 17.1% |
| Tconv memCCR5_CD3 | 16.8% |
| Treg memory_CD3 | 16.6% |
| Tconv memCCR5_mem | 16.3% |
| Treg naive_CD4 | 16.1% |
| Tconv memCCR4_Tconv | 16.1% |
| CD8pos_total | 16.1% |
| CD8 RO CCR5_CD8 | 15.8% |
| CCR5_CD8RO | 15.5% |
| Tconv mem_Tconv | 15.3% |
| CD8 RO CD56_CD3 | 15.3% |
| CD8pos_CD3 | 15.0% |
| Treg memory_CD4 | 15.0% |
| CD4 Treg_CD4 | 15.0% |
| Tconv naive_Tconv | 14.7% |
| CD4 Tconv_CD3 | 13.7% |
| Tconv naive_CD3 | 12.6% |

### SVM_RBF_Permutation_Top10%

**Base Method**: Raw feature selection frequencies across all bootstrap samples

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Tconv memCXCR3_total | 69.5% |
| Tconv memKi67_total | 69.2% |
| Tconv memCD56_total | 67.5% |
| CD4 Treg_total | 66.2% |
| Tconv naive_total | 66.2% |
| Tconv memCD27_total | 66.2% |
| Tconv memPD1_total | 66.0% |
| Tconv memDR_total | 65.8% |
| Tconv memintB7_total | 65.8% |
| CD3pos_total | 64.8% |
| Tconv memTIGIT_total | 63.0% |
| CD4 Tconv mem_total | 62.7% |
| Tconv memCCR5_total | 62.3% |
| Tconv memCCR4_total | 62.0% |
| CD4 Tconv_total | 59.2% |
| Tconv memCCR6_total | 58.0% |
| CCR4_CD8RO | 21.5% |
| CD3hi_total | 13.0% |
| CD8 ncytotox RO CCR4_CD8ntox | 11.2% |
| Tconv memPD1_mem | 10.5% |
| DR_CD8RO | 10.0% |
| CD3hi_CD4neg | 8.5% |
| CD8 RO DR_CD8 | 8.2% |
| Bcells CD27negIgDneg_total | 7.8% |
| Treg memory_total | 7.8% |
| Tconv memCCR6_mem | 7.5% |
| Treg naive_total | 7.5% |
| CD8 RA_total | 7.5% |
| CD8 RA naive_total | 7.0% |
| CD27IgD_Bcells | 7.0% |
| Tconv memCCR4_mem | 6.8% |
| Tconv memCXCR3_Tconv | 6.5% |
| CD16mono_myeloid | 6.5% |
| CD8 RO intB7_total | 6.5% |
| Bcells memory_total | 6.2% |
| Bcells CD27posIgDneg_total | 6.0% |
| Tconv memCXCR3_CD3 | 6.0% |
| CD8 RA_CD3 | 6.0% |
| CD4neg_total | 6.0% |
| CD8 RO DR_CD3 | 6.0% |
| Tconv memCCR6_CD3 | 6.0% |
| CD3neg_total | 5.8% |
| Ki67_CD8RO | 5.8% |
| nonTnonB_total | 5.5% |
| CD8 RO CCR4_total | 5.5% |
| CD8 RO PD1_total | 5.2% |
| CD8 RO Ki67_total | 5.2% |
| CD16mono_CD3neg | 5.2% |
| NK_total | 5.0% |
| Tconv memCD27_mem | 5.0% |
| CD8 RA naive_CD3 | 4.8% |
| CD8 RO CD56_total | 4.8% |
| CD8 RO Ki67_CD8 | 4.8% |
| CD8pos_CD3 | 4.8% |
| intB7_CD8RO | 4.5% |
| CD27negIgDneg_Bcells | 4.5% |
| CD8 RO CCR5_total | 4.5% |
| CD8 RO intB7_CD3 | 4.5% |
| TIGIT_CD8RO | 4.5% |
| CD8 RO DR_total | 4.2% |
| CD8 RO TIGIT_CD3 | 4.2% |
| CD8 RO CXCR3_CD3 | 4.2% |
| Tconv memKi67_mem | 4.2% |
| CD8 RO CD56_CD8 | 4.2% |
| CD8pos_total | 4.0% |
| Bcells memory_CD3neg | 4.0% |
| Tconv memKi67_CD3 | 4.0% |
| CD8 RO PD1_CD3 | 4.0% |
| CCR6_CD8RO | 4.0% |
| NKCD56hi_total | 3.8% |
| CD8 RO CXCR3_total | 3.8% |
| CD8 RO intB7_CD8 | 3.8% |
| CD8 ncytotox RO CCR4_CD3 | 3.8% |
| Tconv memCD56_mem | 3.8% |
| NKCD56hi_nonTnonB | 3.8% |
| CD8 RO CCR6_total | 3.5% |
| CD8 RO TIGIT_total | 3.5% |
| CD8 RO_CD3 | 3.5% |
| CD8 RO CD27_CD3 | 3.5% |
| Tconv memCCR6_Tconv | 3.5% |
| CD14mono_myeloid | 3.5% |
| CD8 RO CCR6_CD8 | 3.2% |
| CCR5_CD8RO | 3.2% |
| Tconv memCD56_CD3 | 3.2% |
| CD8 RO CCR5_CD3 | 3.2% |
| CD14+16+mono_total | 3.2% |
| CD56_CD8RO | 3.2% |
| Tconv memCD56_Tconv | 3.2% |
| Tconv memCXCR3_mem | 3.2% |
| CD8 RO CD27_total | 3.2% |
| CD3hi_CD3 | 3.0% |
| CXCR3_CD8RO | 3.0% |
| NKCD56hi_CD3neg | 3.0% |
| CD16+mono_total | 3.0% |
| Tconv memTIGIT_mem | 3.0% |
| CD14+16+mono_myeloid | 3.0% |
| Bcells naive_total | 3.0% |
| CD8 RO TIGIT_CD8 | 3.0% |
| CD8 RA CCR7 naive_CD8 | 3.0% |
| Bcells Ki67_CD3neg | 3.0% |
| Tconv memintB7_CD3 | 3.0% |
| Tconv memintB7_mem | 3.0% |
| Tconv memDR_mem | 2.8% |
| Tconv memCCR5_mem | 2.8% |
| Bcells Ki67_total | 2.8% |
| CD8 RO CD56_CD3 | 2.8% |
| Tconv memCD27_CD3 | 2.8% |
| CD8 RO PD1_CD8 | 2.8% |
| Treg memory_CD4 | 2.8% |
| CD8  RO Ki67_CD3 | 2.5% |
| Tconv memCCR5_CD3 | 2.5% |
| NKCD16_CD3neg | 2.5% |
| NK Ki67_CD3neg | 2.5% |
| CD4 Treg _CD3 | 2.5% |
| PD1_CD8RO | 2.5% |
| CD4 Tconv_CD3 | 2.5% |
| Tconv memPD1_Tconv | 2.5% |
| Tconv memintB7_Tconv | 2.5% |
| NK_CD3neg | 2.2% |
| CD8 RO CD27_CD8 | 2.2% |
| Tconv memDR_CD3 | 2.2% |
| Tconv memPD1_CD3 | 2.2% |
| myeloid_total | 2.2% |
| Tconv memCCR5_Tconv | 2.2% |
| CD8 RA_CD8 | 2.2% |
| NKCD56hi_NK | 2.2% |
| Tconv memKi67_Tconv | 2.2% |
| NK Ki67_NK | 2.0% |
| CD4 Treg_CD4 | 2.0% |
| NKCD16_total | 2.0% |
| Treg naive_CD3 | 2.0% |
| CD8 RO CCR6_CD3 | 2.0% |
| Treg memory_CD3 | 2.0% |
| Tconv naive_Tconv | 2.0% |
| naive_Bcells | 2.0% |
| Bcells naive_CD3neg | 2.0% |
| CD8 RO_CD8 | 2.0% |
| Tconv memTIGIT_Tconv | 1.8% |
| CD14mono_total | 1.8% |
| memory_Bcells | 1.8% |
| NK Ki67_total | 1.8% |
| Tconv mem_Tconv | 1.8% |
| Bcells_total | 1.8% |
| CD8 RO CXCR3_CD8 | 1.8% |
| NK_nonTnonB | 1.8% |
| CD14+16+mono_CD3neg | 1.8% |
| CD8 RO_total | 1.8% |
| NK Ki67_nonTnonB | 1.5% |
| NKCD16_nonTnonB | 1.5% |
| Tconv memCCR4_CD3 | 1.5% |
| CD27_CD8RO | 1.5% |
| Tconv memTIGIT_CD3 | 1.5% |
| Tconv mem_CD3 | 1.5% |
| NKCD16_NK | 1.5% |
| CD8 RO CCR5_CD8 | 1.2% |
| nonTnonB_CD3neg | 1.2% |
| Bcells_CD3neg | 1.2% |
| Ki67_Bcells | 1.2% |
| Tconv naive_CD3 | 1.2% |
| Tconv memDR_Tconv | 1.0% |
| Tconv memCD27_Tconv | 1.0% |
| Treg naive_CD4 | 1.0% |
| CD4neg_CD3 | 0.8% |
| CD14mono_CD3neg | 0.8% |
| Tconv memCCR4_Tconv | 0.8% |
| myeloid_CD3neg | 0.8% |

### XGB_Importance

**Base Method**: Raw feature selection frequencies across all bootstrap samples

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD16mono_CD3neg | 61.3% |
| Tconv naive_total | 58.5% |
| CD8pos_CD3 | 46.0% |
| Bcells CD27posIgDneg_total | 45.8% |
| CD4 Treg_CD4 | 44.2% |
| CD8 RO CCR5_CD3 | 42.5% |
| CD27IgD_Bcells | 40.0% |
| Tconv memPD1_total | 37.2% |
| NKCD56hi_total | 36.5% |
| CD16mono_myeloid | 34.5% |
| Tconv memKi67_total | 29.0% |
| CD8 RO CXCR3_CD3 | 25.5% |
| CD4 Tconv mem_total | 25.2% |
| Tconv memTIGIT_mem | 24.0% |
| CD4 Tconv_total | 23.8% |
| CD14mono_myeloid | 23.5% |
| CD3pos_total | 23.5% |
| Tconv memPD1_mem | 22.8% |
| Tconv memKi67_mem | 21.5% |
| CD8 RO CCR5_total | 20.8% |
| Tconv memCCR4_total | 20.8% |
| CD8  RO Ki67_CD3 | 20.2% |
| CCR5_CD8RO | 20.2% |
| Tconv memDR_total | 19.8% |
| CD8 RO CCR5_CD8 | 19.8% |
| CD8 RO CD56_CD3 | 19.5% |
| CD8 RA_CD3 | 18.8% |
| CD8 RO DR_total | 18.8% |
| CD8 RO DR_CD3 | 18.5% |
| CD8pos_total | 18.2% |
| Tconv memCXCR3_Tconv | 18.0% |
| CD16+mono_total | 17.8% |
| CD3hi_total | 17.8% |
| CD14+16+mono_myeloid | 17.5% |
| CD27negIgDneg_Bcells | 16.8% |
| Ki67_Bcells | 16.8% |
| NK_total | 16.5% |
| CD4 Treg _CD3 | 16.2% |
| Treg memory_CD4 | 16.0% |
| Tconv memCCR6_mem | 16.0% |
| CCR4_CD8RO | 16.0% |
| Tconv memCD56_total | 15.5% |
| Bcells_total | 15.2% |
| CD8 RO DR_CD8 | 15.2% |
| Tconv memCCR4_mem | 15.0% |
| NKCD56hi_CD3neg | 14.5% |
| Tconv memCCR6_total | 14.2% |
| Bcells memory_total | 14.2% |
| Treg naive_total | 14.0% |
| CD8 RA naive_CD3 | 14.0% |
| Tconv memCXCR3_total | 13.8% |
| NKCD56hi_nonTnonB | 13.8% |
| CD4 Tconv_CD3 | 13.2% |
| nonTnonB_CD3neg | 13.2% |
| CD8 RO CD56_total | 13.0% |
| NK Ki67_NK | 13.0% |
| Bcells memory_CD3neg | 12.5% |
| CD8 RO CCR6_CD8 | 12.2% |
| CD8 RO CD56_CD8 | 12.0% |
| Treg naive_CD4 | 12.0% |
| CD3hi_CD4neg | 12.0% |
| CD8 RO_CD3 | 12.0% |
| CD8 RO PD1_CD3 | 11.8% |
| Tconv memCCR6_Tconv | 11.8% |
| Treg memory_CD3 | 11.8% |
| CD4 Treg_total | 11.8% |
| CD14+16+mono_total | 11.8% |
| CD8 RO CCR6_CD3 | 11.5% |
| Tconv memCD27_mem | 11.5% |
| Ki67_CD8RO | 11.5% |
| NK Ki67_total | 11.5% |
| Bcells CD27negIgDneg_total | 11.5% |
| Tconv memCCR5_mem | 11.5% |
| Bcells Ki67_total | 11.0% |
| Tconv memCCR6_CD3 | 10.5% |
| Tconv memDR_CD3 | 10.5% |
| NKCD56hi_NK | 10.5% |
| CD27_CD8RO | 10.5% |
| Tconv memCCR5_total | 10.5% |
| CD8 RO CXCR3_total | 10.2% |
| Tconv memDR_mem | 10.2% |
| CD8 RA CCR7 naive_CD8 | 9.8% |
| Tconv memintB7_mem | 9.8% |
| Tconv memCD27_Tconv | 9.5% |
| TIGIT_CD8RO | 9.5% |
| NKCD16_NK | 9.5% |
| myeloid_CD3neg | 9.2% |
| nonTnonB_total | 9.0% |
| CD8 ncytotox RO CCR4_CD8ntox | 9.0% |
| DR_CD8RO | 9.0% |
| Tconv memCXCR3_CD3 | 8.8% |
| Tconv memCD56_mem | 8.5% |
| CD8 RO Ki67_total | 8.5% |
| Tconv memCD27_total | 8.5% |
| CD4neg_total | 8.5% |
| CD8 RA naive_total | 8.5% |
| CD8 RO CD27_CD3 | 8.5% |
| intB7_CD8RO | 8.5% |
| Tconv memPD1_CD3 | 8.2% |
| Tconv mem_Tconv | 8.2% |
| Tconv memintB7_CD3 | 8.2% |
| CD8 RO CCR4_total | 8.0% |
| Tconv memTIGIT_total | 8.0% |
| Tconv memCD27_CD3 | 8.0% |
| CD8 RO Ki67_CD8 | 7.5% |
| CD8 RO intB7_CD8 | 7.5% |
| myeloid_total | 7.5% |
| Tconv memintB7_total | 7.2% |
| Treg naive_CD3 | 7.2% |
| Tconv memCCR5_Tconv | 7.0% |
| CXCR3_CD8RO | 7.0% |
| NK_CD3neg | 7.0% |
| CD4neg_CD3 | 7.0% |
| Tconv memCXCR3_mem | 6.8% |
| Tconv memCD56_Tconv | 6.8% |
| CD56_CD8RO | 6.8% |
| CD8 RO TIGIT_CD3 | 6.5% |
| Tconv mem_CD3 | 6.2% |
| CD8 RO TIGIT_CD8 | 6.2% |
| CD8 RA_total | 6.0% |
| Tconv naive_CD3 | 6.0% |
| Tconv memCD56_CD3 | 5.8% |
| Treg memory_total | 5.5% |
| Tconv memintB7_Tconv | 5.2% |
| Tconv memKi67_CD3 | 5.2% |
| Tconv memCCR5_CD3 | 5.2% |
| NK Ki67_CD3neg | 5.2% |
| Bcells naive_total | 5.2% |
| naive_Bcells | 5.2% |
| CD14mono_total | 5.2% |
| CD8 RO PD1_total | 5.2% |
| NK Ki67_nonTnonB | 5.0% |
| Tconv memCCR4_CD3 | 5.0% |
| CD14mono_CD3neg | 4.8% |
| CD8 RO CXCR3_CD8 | 4.8% |
| CD8 RO CD27_CD8 | 4.5% |
| Tconv memTIGIT_CD3 | 4.5% |
| CD8 ncytotox RO CCR4_CD3 | 4.5% |
| Tconv memCCR4_Tconv | 4.5% |
| CD8 RO intB7_total | 4.2% |
| CD8 RO_total | 4.0% |
| CD8 RA_CD8 | 4.0% |
| CD8 RO CCR6_total | 4.0% |
| CCR6_CD8RO | 4.0% |
| Tconv memDR_Tconv | 3.8% |
| CD3hi_CD3 | 3.8% |
| memory_Bcells | 3.5% |
| PD1_CD8RO | 3.5% |
| CD14+16+mono_CD3neg | 3.2% |
| Tconv memPD1_Tconv | 3.2% |
| Tconv memTIGIT_Tconv | 3.2% |
| CD8 RO PD1_CD8 | 3.0% |
| Bcells Ki67_CD3neg | 3.0% |
| CD8 RO intB7_CD3 | 3.0% |
| NK_nonTnonB | 2.8% |
| Tconv memKi67_Tconv | 2.8% |
| Bcells naive_CD3neg | 2.5% |
| CD8 RO TIGIT_total | 2.2% |
| CD8 RO CD27_total | 2.0% |
| NKCD16_nonTnonB | 1.5% |
| CD8 RO_CD8 | 0.8% |
| NKCD16_CD3neg | 0.5% |
| Tconv naive_Tconv | 0.5% |

### XGBoost_Permutation_AboveMean

**Base Method**: Raw feature selection frequencies across all bootstrap samples

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Tconv naive_total | 15.8% |
| CD8pos_CD3 | 12.8% |
| CD16mono_CD3neg | 11.8% |
| CD4 Treg_CD4 | 10.5% |
| CD8 RO CCR5_CD3 | 9.0% |
| CD27IgD_Bcells | 6.2% |
| CD16mono_myeloid | 4.8% |
| Bcells CD27posIgDneg_total | 4.2% |
| NKCD56hi_total | 3.5% |
| CD8 RO CXCR3_CD3 | 2.8% |
| CD8  RO Ki67_CD3 | 2.5% |
| CCR5_CD8RO | 2.2% |
| CD8 RO DR_CD8 | 2.2% |
| CD8 RA_CD3 | 2.0% |
| CD8 RO CD56_CD3 | 2.0% |
| CD4 Treg _CD3 | 2.0% |
| Treg memory_CD4 | 2.0% |
| Tconv memKi67_total | 2.0% |
| CD8 RO CCR5_CD8 | 1.8% |
| CD8 RO DR_CD3 | 1.8% |
| CD27negIgDneg_Bcells | 1.8% |
| Tconv memPD1_total | 1.8% |
| CCR4_CD8RO | 1.5% |
| Tconv memTIGIT_mem | 1.5% |
| Tconv memCCR4_total | 1.5% |
| CD8 RO TIGIT_CD3 | 1.2% |
| Tconv memCXCR3_Tconv | 1.2% |
| CD8 RO CD27_CD3 | 1.2% |
| Bcells Ki67_total | 1.2% |
| Tconv memPD1_mem | 1.2% |
| CD14mono_myeloid | 1.2% |
| Ki67_CD8RO | 1.2% |
| Tconv memCCR6_mem | 1.0% |
| Tconv memKi67_mem | 1.0% |
| DR_CD8RO | 1.0% |
| CD8 RO CCR5_total | 1.0% |
| NKCD56hi_CD3neg | 1.0% |
| CD3hi_CD4neg | 1.0% |
| CD8 RO CD56_CD8 | 1.0% |
| CD14+16+mono_myeloid | 1.0% |
| CD8pos_total | 1.0% |
| Ki67_Bcells | 1.0% |
| Tconv memCCR5_Tconv | 1.0% |
| CD8 RO DR_total | 1.0% |
| Tconv memCCR4_mem | 1.0% |
| Treg naive_CD4 | 1.0% |
| CD3pos_total | 0.8% |
| Tconv memCCR5_mem | 0.8% |
| NK Ki67_NK | 0.8% |
| CD8 RO CCR6_CD8 | 0.8% |
| CD8 RO PD1_CD3 | 0.8% |
| Treg naive_total | 0.8% |
| CD4 Tconv mem_total | 0.8% |
| CD8 RA naive_CD3 | 0.8% |
| Tconv memintB7_mem | 0.8% |
| Tconv memTIGIT_total | 0.8% |
| CD4 Tconv_total | 0.8% |
| CD27_CD8RO | 0.8% |
| Tconv memCCR6_Tconv | 0.8% |
| nonTnonB_total | 0.8% |
| NK Ki67_total | 0.8% |
| CD4 Tconv_CD3 | 0.8% |
| Tconv memCD56_mem | 0.8% |
| CD14+16+mono_total | 0.8% |
| CD16+mono_total | 0.8% |
| CD8 RO CCR4_total | 0.8% |
| CD8 RO Ki67_CD8 | 0.5% |
| CD8 RO TIGIT_CD8 | 0.5% |
| Tconv memCD27_Tconv | 0.5% |
| Tconv mem_Tconv | 0.5% |
| Bcells CD27negIgDneg_total | 0.5% |
| Tconv memPD1_CD3 | 0.5% |
| Tconv memKi67_Tconv | 0.5% |
| Tconv memCD56_CD3 | 0.5% |
| CD8 RO Ki67_total | 0.5% |
| Tconv memintB7_CD3 | 0.5% |
| Tconv memCCR4_Tconv | 0.5% |
| Tconv memCD27_mem | 0.5% |
| CD4neg_total | 0.5% |
| CD8 RO intB7_CD8 | 0.5% |
| NKCD16_nonTnonB | 0.5% |
| Treg memory_total | 0.5% |
| CD8 RO CXCR3_CD8 | 0.5% |
| Tconv memCCR6_CD3 | 0.5% |
| Bcells_total | 0.5% |
| Tconv memCXCR3_total | 0.5% |
| Treg memory_CD3 | 0.5% |
| CD8 RO_CD3 | 0.5% |
| Tconv memDR_Tconv | 0.5% |
| CD8 RO CD56_total | 0.5% |
| Tconv memCCR6_total | 0.5% |
| CD8 RA CCR7 naive_CD8 | 0.5% |
| Tconv memKi67_CD3 | 0.5% |
| Tconv memDR_total | 0.5% |
| nonTnonB_CD3neg | 0.5% |
| NKCD56hi_NK | 0.5% |
| intB7_CD8RO | 0.5% |
| Tconv memCD27_CD3 | 0.5% |
| Bcells memory_total | 0.5% |
| Tconv memCXCR3_mem | 0.5% |
| Treg naive_CD3 | 0.2% |
| CD4 Treg_total | 0.2% |
| Tconv memintB7_total | 0.2% |
| CD8 RO intB7_total | 0.2% |
| Tconv memCD27_total | 0.2% |
| Tconv memCCR5_total | 0.2% |
| Tconv memCD56_total | 0.2% |
| CD8 RO_total | 0.2% |
| CD8 RA_total | 0.2% |
| TIGIT_CD8RO | 0.2% |
| memory_Bcells | 0.2% |
| NK_CD3neg | 0.2% |
| NKCD16_CD3neg | 0.2% |
| CD14mono_CD3neg | 0.2% |
| CD8 RA naive_total | 0.2% |
| CD8 RO CD27_total | 0.2% |
| CD8 RO CCR6_total | 0.2% |
| CD8 RO PD1_total | 0.2% |
| CD8 RO CXCR3_total | 0.2% |
| CD14mono_total | 0.2% |
| myeloid_total | 0.2% |
| NKCD16_total | 0.2% |
| naive_Bcells | 0.2% |
| CD8 RO TIGIT_total | 0.2% |
| CD3neg_total | 0.2% |
| Tconv memPD1_Tconv | 0.2% |
| CD8 ncytotox RO CCR4_CD3 | 0.2% |
| Tconv memDR_CD3 | 0.2% |
| Tconv memTIGIT_CD3 | 0.2% |
| Tconv memCCR5_CD3 | 0.2% |
| CD4neg_CD3 | 0.2% |
| Tconv mem_CD3 | 0.2% |
| Tconv memCCR4_CD3 | 0.2% |
| Bcells Ki67_CD3neg | 0.2% |
| NK Ki67_CD3neg | 0.2% |
| Bcells naive_total | 0.2% |
| Tconv memTIGIT_Tconv | 0.2% |
| Tconv memDR_mem | 0.2% |
| CD8 RA_CD8 | 0.2% |
| Tconv memCD56_Tconv | 0.2% |
| Tconv memintB7_Tconv | 0.2% |
| Bcells_CD3neg | 0.2% |
| Bcells naive_CD3neg | 0.2% |
| NK_nonTnonB | 0.2% |
| NKCD16_NK | 0.2% |
| CD8 RO intB7_CD3 | 0.2% |
| CCR6_CD8RO | 0.2% |
| CD8 RO_CD8 | 0.2% |
| CD14+16+mono_CD3neg | 0.2% |
| PD1_CD8RO | 0.2% |
| CXCR3_CD8RO | 0.2% |
| CD8 RO PD1_CD8 | 0.2% |
| CD8 RO CD27_CD8 | 0.2% |
| Bcells memory_CD3neg | 0.2% |
| CD56_CD8RO | 0.2% |
| CD8 RO CCR6_CD3 | 0.2% |
| Tconv memCXCR3_CD3 | 0.2% |

### XGBoost_Permutation_Top10%

**Base Method**: Raw feature selection frequencies across all bootstrap samples

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Tconv memintB7_total | 99.8% |
| Tconv memKi67_total | 99.2% |
| Tconv memCXCR3_total | 98.8% |
| Tconv memPD1_total | 98.5% |
| Tconv naive_total | 98.5% |
| Tconv memCD27_total | 98.5% |
| Tconv memCD56_total | 98.0% |
| Tconv memDR_total | 96.2% |
| Tconv memTIGIT_total | 94.0% |
| CD4 Treg_total | 93.2% |
| CD3pos_total | 92.2% |
| CD4 Tconv mem_total | 88.8% |
| Tconv memCCR4_total | 74.5% |
| CD4 Tconv_total | 65.0% |
| Tconv memCCR6_total | 46.8% |
| Tconv memCCR5_total | 46.2% |
| CD16mono_CD3neg | 14.2% |
| CD8pos_CD3 | 13.2% |
| CD4 Treg_CD4 | 12.2% |
| CD8 RO CCR5_CD3 | 10.8% |
| CD27IgD_Bcells | 8.2% |
| CD16mono_myeloid | 7.2% |
| Bcells CD27posIgDneg_total | 6.2% |
| NKCD56hi_total | 5.0% |
| CD8 RO CXCR3_CD3 | 4.2% |
| CD8  RO Ki67_CD3 | 3.5% |
| CD8 RO DR_CD3 | 3.5% |
| CD4 Treg _CD3 | 3.0% |
| CCR5_CD8RO | 2.8% |
| CD14+16+mono_myeloid | 2.8% |
| Tconv memTIGIT_mem | 2.8% |
| CD8pos_total | 2.5% |
| Treg naive_total | 2.5% |
| Treg memory_CD4 | 2.5% |
| CD8 RO DR_total | 2.5% |
| CD8 RO CD56_CD3 | 2.2% |
| CD8 RO DR_CD8 | 2.2% |
| Treg memory_total | 2.2% |
| Tconv memPD1_mem | 2.0% |
| CD8 RO CCR5_CD8 | 2.0% |
| CD8 RA_CD3 | 2.0% |
| CD27negIgDneg_Bcells | 2.0% |
| Tconv memCXCR3_Tconv | 1.8% |
| CD8 RO CCR5_total | 1.8% |
| Tconv memCD56_mem | 1.8% |
| CD4neg_total | 1.8% |
| CD3hi_total | 1.8% |
| Bcells_total | 1.8% |
| CD14mono_myeloid | 1.8% |
| CCR4_CD8RO | 1.8% |
| Tconv memPD1_CD3 | 1.5% |
| CD8 RO CCR6_CD8 | 1.5% |
| Bcells Ki67_total | 1.5% |
| Ki67_Bcells | 1.5% |
| NKCD56hi_CD3neg | 1.5% |
| CD3hi_CD4neg | 1.5% |
| Tconv memCCR5_mem | 1.5% |
| Tconv memKi67_mem | 1.5% |
| Treg naive_CD4 | 1.5% |
| Tconv memCD27_Tconv | 1.2% |
| CD8 RA naive_CD3 | 1.2% |
| Tconv memCCR4_mem | 1.2% |
| DR_CD8RO | 1.2% |
| Ki67_CD8RO | 1.2% |
| CD8 RO CD56_total | 1.2% |
| NK Ki67_total | 1.2% |
| CD8 RO intB7_total | 1.2% |
| Tconv memCCR6_mem | 1.2% |
| CD8 RO CD27_CD3 | 1.2% |
| CD4 Tconv_CD3 | 1.2% |
| CD8 RA_total | 1.2% |
| nonTnonB_CD3neg | 1.2% |
| NK Ki67_NK | 1.2% |
| CD8 RO TIGIT_CD3 | 1.2% |
| Tconv memCCR6_CD3 | 1.2% |
| NKCD56hi_NK | 1.0% |
| CD8 RO intB7_CD8 | 1.0% |
| CD8 RO CD56_CD8 | 1.0% |
| nonTnonB_total | 1.0% |
| CD27_CD8RO | 1.0% |
| Tconv memCCR6_Tconv | 1.0% |
| Bcells CD27negIgDneg_total | 1.0% |
| NKCD56hi_nonTnonB | 1.0% |
| CD14+16+mono_total | 1.0% |
| Tconv memCCR5_Tconv | 1.0% |
| CD8 RO Ki67_CD8 | 1.0% |
| Bcells memory_total | 1.0% |
| CD8 RO TIGIT_total | 1.0% |
| CXCR3_CD8RO | 1.0% |
| CD8 RA CCR7 naive_CD8 | 0.8% |
| NK_total | 0.8% |
| CD8 RO PD1_CD3 | 0.8% |
| Tconv memintB7_mem | 0.8% |
| CD8 RO TIGIT_CD8 | 0.8% |
| Tconv memCD56_CD3 | 0.8% |
| Tconv memDR_CD3 | 0.8% |
| Tconv memKi67_CD3 | 0.8% |
| CD16+mono_total | 0.8% |
| Tconv memCXCR3_CD3 | 0.8% |
| CD8 RO CCR6_CD3 | 0.8% |
| CD8 RO CCR4_total | 0.8% |
| Tconv memCD27_CD3 | 0.5% |
| myeloid_CD3neg | 0.5% |
| Tconv memCCR4_Tconv | 0.5% |
| Tconv memintB7_CD3 | 0.5% |
| Tconv memKi67_Tconv | 0.5% |
| CD8 RA_CD8 | 0.5% |
| CD8 RO PD1_total | 0.5% |
| CD8 RO CCR6_total | 0.5% |
| CD8 RO_CD3 | 0.5% |
| CD8 ncytotox RO CCR4_CD3 | 0.5% |
| CD8 RO Ki67_total | 0.5% |
| CD4neg_CD3 | 0.5% |
| Tconv naive_CD3 | 0.5% |
| Tconv memCCR4_CD3 | 0.5% |
| NK Ki67_CD3neg | 0.5% |
| NKCD16_NK | 0.5% |
| Bcells memory_CD3neg | 0.5% |
| Tconv memCD27_mem | 0.5% |
| CD14mono_CD3neg | 0.5% |
| intB7_CD8RO | 0.5% |
| CD8 RO CXCR3_total | 0.5% |
| Tconv memCXCR3_mem | 0.5% |
| CD8 RO CD27_CD8 | 0.2% |
| Treg naive_CD3 | 0.2% |
| Tconv memintB7_Tconv | 0.2% |
| CD8 ncytotox RO CCR4_CD8ntox | 0.2% |
| Tconv mem_Tconv | 0.2% |
| Tconv mem_CD3 | 0.2% |
| NKCD16_nonTnonB | 0.2% |
| CCR6_CD8RO | 0.2% |
| Bcells naive_total | 0.2% |
| CD56_CD8RO | 0.2% |
| CD8 RO intB7_CD3 | 0.2% |
| PD1_CD8RO | 0.2% |
| CD3hi_CD3 | 0.2% |
| Tconv memDR_mem | 0.2% |
| CD8 RO CXCR3_CD8 | 0.2% |
| CD8 RA naive_total | 0.2% |
| Treg memory_CD3 | 0.2% |
| Tconv memCD56_Tconv | 0.2% |
| CD8 RO_total | 0.2% |
| Tconv memTIGIT_Tconv | 0.2% |
| Tconv memCCR5_CD3 | 0.2% |
| Tconv memDR_Tconv | 0.2% |
| memory_Bcells | 0.2% |

### mRMR (Top 10%)

**Base Method**: Raw feature selection frequencies across all bootstrap samples

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD4 Treg_CD4 | 52.2% |
| CD16mono_myeloid | 48.0% |
| CD8 RO CCR5_CD3 | 45.8% |
| CD4 Tconv_total | 45.5% |
| CD14mono_myeloid | 45.0% |
| Treg memory_CD4 | 44.2% |
| CD8pos_CD3 | 43.8% |
| CD27IgD_Bcells | 41.2% |
| Tconv naive_total | 41.0% |
| CD16mono_CD3neg | 35.0% |
| CD4 Tconv_CD3 | 34.5% |
| Tconv naive_CD3 | 32.5% |
| CD4 Treg _CD3 | 31.5% |
| NKCD56hi_total | 31.2% |
| CD8 RA_CD3 | 31.0% |
| CD8 RO CCR5_CD8 | 29.5% |
| Treg memory_CD3 | 27.5% |
| CCR4_CD8RO | 26.8% |
| Tconv memCCR6_Tconv | 22.2% |
| Tconv memCXCR3_Tconv | 20.8% |
| Tconv memPD1_mem | 19.8% |
| CCR5_CD8RO | 19.5% |
| CD8 RO CXCR3_CD3 | 19.2% |
| CD3pos_total | 18.8% |
| CD3neg_total | 17.8% |
| Tconv memKi67_total | 17.0% |
| Bcells CD27posIgDneg_total | 16.5% |
| CD8 RO DR_CD3 | 16.2% |
| CD4neg_CD3 | 16.0% |
| CD8 RO CD56_CD3 | 15.5% |
| Tconv mem_Tconv | 15.5% |
| CD8 RA naive_CD3 | 15.2% |
| Treg naive_CD4 | 15.2% |
| Tconv memCCR6_mem | 14.5% |
| CD8 RO CD27_CD3 | 14.5% |
| NKCD56hi_nonTnonB | 14.2% |
| Bcells CD27negIgDneg_total | 14.2% |
| CD8 RO TIGIT_CD3 | 14.0% |
| CD3hi_CD4neg | 13.8% |
| CD8 RO CCR6_CD3 | 13.5% |
| CD8 RO_CD3 | 13.2% |
| CD27negIgDneg_Bcells | 12.5% |
| Tconv memCCR6_CD3 | 12.2% |
| Tconv memCCR5_Tconv | 12.0% |
| Tconv memCD27_mem | 11.5% |
| CD8 RO DR_CD8 | 11.5% |
| Tconv memCXCR3_CD3 | 11.0% |
| Tconv memintB7_Tconv | 10.5% |
| CD14+16+mono_myeloid | 10.5% |
| Tconv naive_Tconv | 10.2% |
| CD8 RO CCR5_total | 10.2% |
| Tconv memKi67_mem | 9.8% |
| DR_CD8RO | 9.2% |
| CD8 RO CXCR3_CD8 | 9.2% |
| Tconv memCCR4_mem | 9.0% |
| Tconv memCCR5_mem | 8.8% |
| Bcells Ki67_total | 8.8% |
| CD3hi_total | 8.8% |
| CD8 RO intB7_CD3 | 8.2% |
| NK Ki67_total | 8.2% |
| CD27_CD8RO | 8.0% |
| Tconv memCD56_total | 7.8% |
| Tconv memCXCR3_mem | 7.8% |
| NKCD56hi_CD3neg | 7.2% |
| CD16+mono_total | 7.2% |
| NKCD56hi_NK | 7.2% |
| Treg naive_CD3 | 7.0% |
| Tconv memDR_total | 7.0% |
| CXCR3_CD8RO | 7.0% |
| CD8 RO PD1_CD3 | 6.8% |
| Tconv memCCR5_CD3 | 6.8% |
| CD8 RO CD56_total | 6.5% |
| CD8 RO CCR6_CD8 | 6.2% |
| CD8 RA_total | 6.2% |
| Tconv memCCR4_Tconv | 6.0% |
| NK_total | 6.0% |
| CD8 RO CD56_CD8 | 6.0% |
| Tconv memCD27_Tconv | 6.0% |
| Bcells memory_CD3neg | 5.8% |
| Tconv memKi67_CD3 | 5.8% |
| Tconv memDR_mem | 5.2% |
| Tconv memPD1_total | 5.2% |
| Tconv memCCR4_total | 5.2% |
| NK Ki67_NK | 5.0% |
| Tconv memTIGIT_Tconv | 5.0% |
| NK Ki67_nonTnonB | 4.8% |
| CD56_CD8RO | 4.8% |
| Treg memory_total | 4.5% |
| PD1_CD8RO | 4.5% |
| Tconv memCD27_total | 4.5% |
| naive_Bcells | 4.2% |
| Tconv memintB7_mem | 4.0% |
| nonTnonB_total | 4.0% |
| CCR6_CD8RO | 4.0% |
| CD8 RA CCR7 naive_CD8 | 4.0% |
| Ki67_Bcells | 3.8% |
| myeloid_CD3neg | 3.8% |
| intB7_CD8RO | 3.8% |
| CD8 ncytotox RO CCR4_CD8ntox | 3.8% |
| Bcells_total | 3.5% |
| CD8 RO PD1_CD8 | 3.5% |
| CD4 Treg_total | 3.5% |
| CD14mono_total | 3.2% |
| CD8 RO TIGIT_CD8 | 3.2% |
| CD8 RO Ki67_CD8 | 3.2% |
| memory_Bcells | 3.2% |
| Tconv memTIGIT_mem | 3.0% |
| CD8  RO Ki67_CD3 | 3.0% |
| CD14+16+mono_total | 3.0% |
| CD8pos_total | 3.0% |
| NKCD16_NK | 3.0% |
| Tconv memCD56_mem | 3.0% |
| Tconv memCCR6_total | 3.0% |
| Bcells Ki67_CD3neg | 3.0% |
| Bcells memory_total | 2.8% |
| NKCD16_total | 2.5% |
| Ki67_CD8RO | 2.5% |
| Treg naive_total | 2.5% |
| Tconv memPD1_CD3 | 2.2% |
| CD8 RO intB7_CD8 | 2.2% |
| NK_nonTnonB | 2.2% |
| Tconv memPD1_Tconv | 2.0% |
| CD14+16+mono_CD3neg | 2.0% |
| Tconv memTIGIT_CD3 | 2.0% |
| CD8 RO PD1_total | 2.0% |
| CD8 RO CD27_total | 2.0% |
| Tconv memDR_CD3 | 2.0% |
| Tconv memintB7_CD3 | 2.0% |
| CD8 RO_CD8 | 2.0% |
| CD4neg_total | 2.0% |
| Tconv memCD56_Tconv | 1.8% |
| Tconv memintB7_total | 1.8% |
| CD3hi_CD3 | 1.8% |
| Bcells naive_total | 1.8% |
| CD8 RO DR_total | 1.8% |
| Bcells naive_CD3neg | 1.8% |
| CD14mono_CD3neg | 1.8% |
| CD8 RO CXCR3_total | 1.8% |
| Tconv memDR_Tconv | 1.8% |
| Tconv memTIGIT_total | 1.8% |
| Bcells_CD3neg | 1.5% |
| CD8 RO TIGIT_total | 1.5% |
| CD8 RO CCR6_total | 1.5% |
| Tconv memCCR5_total | 1.5% |
| CD4 Tconv mem_total | 1.5% |
| TIGIT_CD8RO | 1.5% |
| CD8 RO CCR4_total | 1.5% |
| CD8 RO Ki67_total | 1.5% |
| Tconv memCCR4_CD3 | 1.2% |
| CD8 RA_CD8 | 1.2% |
| NKCD16_nonTnonB | 1.2% |
| CD8 RO_total | 1.2% |
| CD8 RO CD27_CD8 | 1.2% |
| Tconv memCXCR3_total | 1.0% |
| CD8 RA naive_total | 1.0% |
| NK Ki67_CD3neg | 1.0% |
| Tconv memKi67_Tconv | 0.8% |
| myeloid_total | 0.8% |
| CD8 ncytotox RO CCR4_CD3 | 0.8% |
| NKCD16_CD3neg | 0.5% |
| Tconv memCD27_CD3 | 0.5% |
| Tconv mem_CD3 | 0.5% |
| NK_CD3neg | 0.5% |
| Tconv memCD56_CD3 | 0.2% |
| CD8 RO intB7_total | 0.2% |

