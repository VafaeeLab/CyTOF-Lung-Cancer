# Biomarker Discovery: Main Summary Report

---
- **Methodology**: Nested Cross-Validation (40 outer folds) with stratified bootstrapped inner stability (10 resamples)
- **Key Finding**: Performance metrics reported here are unbiased estimates of generalization performance.
- **Best Unbiased ROC-AUC**: 0.7974

## Top 10 Performing Model Combinations (Mean Unbiased Nested CV Performance)

|    | signature_method            | classifier   |   roc_auc_mean |   roc_auc_std | roc_auc_ci   |   auprc_mean |   auprc_std | auprc_ci    |   accuracy_mean |   accuracy_std |   precision_mean |   precision_std |   recall_mean |   recall_std |   specificity_mean |   specificity_std |   f1_score_mean |   f1_score_std | f1_score_ci   |
|---:|:----------------------------|:-------------|---------------:|--------------:|:-------------|-------------:|------------:|:------------|----------------:|---------------:|-----------------:|----------------:|--------------:|-------------:|-------------------:|------------------:|----------------:|---------------:|:--------------|
|  0 | Ridge_Strict_t40            | XGBoost      |       0.797396 |      0.208813 | 0.731-0.864  |     0.864211 |    0.141683 | 0.819-0.910 |        0.6875   |       0.205243 |         0.726726 |        0.247957 |       0.71875 |     0.284129 |           0.65625  |          0.324228 |        0.696953 |       0.229514 | 0.624-0.770   |
|  1 | RF_Importance_t40           | XGBoost      |       0.767188 |      0.198142 | 0.704-0.831  |     0.844821 |    0.140029 | 0.800-0.890 |        0.646429 |       0.179038 |         0.67994  |        0.229852 |       0.6875  |     0.287284 |           0.604167 |          0.302383 |        0.657105 |       0.220658 | 0.587-0.728   |
|  2 | Ridge_Strict_t70            | XGBoost      |       0.764583 |      0.214969 | 0.696-0.833  |     0.835893 |    0.153472 | 0.787-0.885 |        0.670982 |       0.208832 |         0.699405 |        0.243095 |       0.7125  |     0.28051  |           0.627083 |          0.301343 |        0.685332 |       0.230906 | 0.611-0.759   |
|  3 | Ridge_Strict_t50            | XGBoost      |       0.7625   |      0.214793 | 0.694-0.831  |     0.839167 |    0.153807 | 0.790-0.888 |        0.663393 |       0.19883  |         0.711012 |        0.25275  |       0.7125  |     0.297155 |           0.6125   |          0.339971 |        0.677    |       0.226477 | 0.605-0.749   |
|  4 | RF_Importance_t50           | XGBoost      |       0.76224  |      0.206278 | 0.696-0.828  |     0.842217 |    0.135875 | 0.799-0.886 |        0.676339 |       0.174458 |         0.732976 |        0.242545 |       0.7     |     0.284199 |           0.658333 |          0.311691 |        0.681338 |       0.212204 | 0.613-0.749   |
|  5 | All Features (Baseline)_t40 | XGBoost      |       0.754687 |      0.204205 | 0.689-0.820  |     0.834777 |    0.146283 | 0.788-0.882 |        0.637054 |       0.178131 |         0.689524 |        0.243648 |       0.66875 |     0.27958  |           0.608333 |          0.32914  |        0.647918 |       0.212407 | 0.580-0.716   |
|  6 | Ridge_Strict_t60            | XGBoost      |       0.753906 |      0.231073 | 0.680-0.828  |     0.828527 |    0.16917  | 0.774-0.883 |        0.650446 |       0.206152 |         0.679821 |        0.2395   |       0.7     |     0.278503 |           0.597917 |          0.303052 |        0.668883 |       0.227249 | 0.596-0.742   |
|  7 | RFE (RandomForest)_t40      | XGBoost      |       0.739062 |      0.219454 | 0.669-0.809  |     0.818214 |    0.155948 | 0.768-0.868 |        0.664286 |       0.177755 |         0.69869  |        0.227808 |       0.7     |     0.272688 |           0.629167 |          0.292322 |        0.675696 |       0.212818 | 0.608-0.744   |
|  8 | RF_Importance_t60           | XGBoost      |       0.730469 |      0.209375 | 0.664-0.797  |     0.816994 |    0.149897 | 0.769-0.865 |        0.655804 |       0.189457 |         0.69006  |        0.235079 |       0.70625 |     0.270846 |           0.602083 |          0.31094  |        0.675207 |       0.214967 | 0.606-0.744   |
|  9 | Ridge_Strict_t80            | XGBoost      |       0.730469 |      0.225473 | 0.658-0.803  |     0.81061  |    0.159394 | 0.760-0.862 |        0.627232 |       0.185805 |         0.637083 |        0.233653 |       0.675   |     0.272688 |           0.575    |          0.272035 |        0.641806 |       0.229996 | 0.568-0.715   |

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
| ElasticNet_Lenient_t40 | 40 | 87 | 2.2 |
| ElasticNet_Lenient_t50 | 40 | 53 | 1.3 |
| ElasticNet_Lenient_t60 | 37 | 38 | 1.0 |
| ElasticNet_Lenient_t70 | 31 | 24 | 0.8 |
| ElasticNet_Lenient_t80 | 19 | 13 | 0.7 |
| ElasticNet_RFE_t40 | 38 | 35 | 0.9 |
| ElasticNet_RFE_t50 | 30 | 18 | 0.6 |
| ElasticNet_RFE_t60 | 10 | 7 | 0.7 |
| ElasticNet_RFE_t70 | 4 | 4 | 1.0 |
| ElasticNet_RFE_t80 | 3 | 3 | 1.0 |
| ElasticNet_Strict_t40 | 39 | 32 | 0.8 |
| ElasticNet_Strict_t50 | 28 | 21 | 0.8 |
| ElasticNet_Strict_t60 | 19 | 15 | 0.8 |
| ElasticNet_Strict_t70 | 11 | 10 | 0.9 |
| ElasticNet_Strict_t80 | 5 | 5 | 1.0 |
| FDR (p < 0.01)_t40 | 6 | 12 | 2.0 |
| FDR (p < 0.01)_t50 | 3 | 6 | 2.0 |
| FDR (p < 0.01)_t60 | 1 | 3 | 3.0 |
| FDR (p < 0.01)_t70 | 1 | 3 | 3.0 |
| FDR (p < 0.01)_t80 | 1 | 3 | 3.0 |
| FDR (p < 0.05)_t40 | 33 | 86 | 2.6 |
| FDR (p < 0.05)_t50 | 30 | 53 | 1.8 |
| FDR (p < 0.05)_t60 | 24 | 39 | 1.6 |
| FDR (p < 0.05)_t70 | 15 | 27 | 1.8 |
| FDR (p < 0.05)_t80 | 9 | 17 | 1.9 |
| FDR (p < 0.1)_t40 | 36 | 122 | 3.4 |
| FDR (p < 0.1)_t50 | 35 | 103 | 2.9 |
| FDR (p < 0.1)_t60 | 31 | 78 | 2.5 |
| FDR (p < 0.1)_t70 | 28 | 57 | 2.0 |
| FDR (p < 0.1)_t80 | 22 | 40 | 1.8 |
| LASSO_Lenient_t40 | 40 | 57 | 1.4 |
| LASSO_Lenient_t50 | 35 | 29 | 0.8 |
| LASSO_Lenient_t60 | 30 | 22 | 0.7 |
| LASSO_Lenient_t70 | 19 | 18 | 0.9 |
| LASSO_Lenient_t80 | 10 | 10 | 1.0 |
| LASSO_RFE_t40 | 38 | 26 | 0.7 |
| LASSO_RFE_t50 | 16 | 11 | 0.7 |
| LASSO_RFE_t60 | 8 | 7 | 0.9 |
| LASSO_RFE_t70 | 4 | 3 | 0.8 |
| LASSO_RFE_t80 | 1 | 1 | 1.0 |
| LASSO_Strict_t40 | 31 | 21 | 0.7 |
| LASSO_Strict_t50 | 22 | 17 | 0.8 |
| LASSO_Strict_t60 | 12 | 11 | 0.9 |
| LASSO_Strict_t70 | 6 | 6 | 1.0 |
| LASSO_Strict_t80 | 2 | 2 | 1.0 |
| LogisticRegression_Permutation_Top10%_t40 | 40 | 16 | 0.4 |
| LogisticRegression_Permutation_Top10%_t50 | 40 | 16 | 0.4 |
| LogisticRegression_Permutation_Top10%_t60 | 40 | 16 | 0.4 |
| LogisticRegression_Permutation_Top10%_t70 | 40 | 16 | 0.4 |
| LogisticRegression_Permutation_Top10%_t80 | 40 | 16 | 0.4 |
| Mutual Information (Top 10%)_t40 | 40 | 87 | 2.2 |
| Mutual Information (Top 10%)_t50 | 40 | 65 | 1.6 |
| Mutual Information (Top 10%)_t60 | 40 | 41 | 1.0 |
| Mutual Information (Top 10%)_t70 | 30 | 27 | 0.9 |
| Mutual Information (Top 10%)_t80 | 21 | 16 | 0.8 |
| NaiveBayes_Permutation_AboveMean_t40 | 40 | 139 | 3.5 |
| NaiveBayes_Permutation_AboveMean_t50 | 40 | 77 | 1.9 |
| NaiveBayes_Permutation_AboveMean_t60 | 38 | 42 | 1.1 |
| NaiveBayes_Permutation_AboveMean_t70 | 29 | 18 | 0.6 |
| NaiveBayes_Permutation_AboveMean_t80 | 11 | 7 | 0.6 |
| NaiveBayes_Permutation_Top10%_t40 | 40 | 58 | 1.4 |
| NaiveBayes_Permutation_Top10%_t50 | 40 | 39 | 1.0 |
| NaiveBayes_Permutation_Top10%_t60 | 40 | 30 | 0.8 |
| NaiveBayes_Permutation_Top10%_t70 | 37 | 19 | 0.5 |
| NaiveBayes_Permutation_Top10%_t80 | 24 | 14 | 0.6 |
| RFE (RandomForest)_t40 | 40 | 151 | 3.8 |
| RFE (RandomForest)_t50 | 40 | 133 | 3.3 |
| RFE (RandomForest)_t60 | 40 | 113 | 2.8 |
| RFE (RandomForest)_t70 | 40 | 81 | 2.0 |
| RFE (RandomForest)_t80 | 25 | 42 | 1.7 |
| RF_Importance_t40 | 40 | 165 | 4.1 |
| RF_Importance_t50 | 40 | 154 | 3.9 |
| RF_Importance_t60 | 40 | 119 | 3.0 |
| RF_Importance_t70 | 40 | 86 | 2.1 |
| RF_Importance_t80 | 40 | 59 | 1.5 |
| RandomForest_Permutation_Top10%_t40 | 40 | 16 | 0.4 |
| RandomForest_Permutation_Top10%_t50 | 40 | 16 | 0.4 |
| RandomForest_Permutation_Top10%_t60 | 40 | 16 | 0.4 |
| RandomForest_Permutation_Top10%_t70 | 40 | 16 | 0.4 |
| RandomForest_Permutation_Top10%_t80 | 40 | 16 | 0.4 |
| Ridge_Strict_t40 | 40 | 162 | 4.0 |
| Ridge_Strict_t50 | 40 | 159 | 4.0 |
| Ridge_Strict_t60 | 40 | 154 | 3.9 |
| Ridge_Strict_t70 | 40 | 149 | 3.7 |
| Ridge_Strict_t80 | 40 | 133 | 3.3 |
| SVM_RBF_Permutation_Top10%_t40 | 40 | 16 | 0.4 |
| SVM_RBF_Permutation_Top10%_t50 | 40 | 16 | 0.4 |
| SVM_RBF_Permutation_Top10%_t60 | 40 | 16 | 0.4 |
| SVM_RBF_Permutation_Top10%_t70 | 40 | 16 | 0.4 |
| SVM_RBF_Permutation_Top10%_t80 | 40 | 16 | 0.4 |
| XGB_Importance_t40 | 39 | 39 | 1.0 |
| XGB_Importance_t50 | 33 | 22 | 0.7 |
| XGB_Importance_t60 | 20 | 11 | 0.6 |
| XGB_Importance_t70 | 11 | 7 | 0.6 |
| XGB_Importance_t80 | 5 | 3 | 0.6 |
| XGBoost_Permutation_AboveMean_t40 | 16 | 10 | 0.6 |
| XGBoost_Permutation_AboveMean_t50 | 6 | 3 | 0.5 |
| XGBoost_Permutation_AboveMean_t60 | 3 | 2 | 0.7 |
| XGBoost_Permutation_AboveMean_t70 | 2 | 2 | 1.0 |
| XGBoost_Permutation_AboveMean_t80 | 1 | 1 | 1.0 |
| XGBoost_Permutation_Top10%_t40 | 40 | 25 | 0.6 |
| XGBoost_Permutation_Top10%_t50 | 40 | 19 | 0.5 |
| XGBoost_Permutation_Top10%_t60 | 40 | 18 | 0.5 |
| XGBoost_Permutation_Top10%_t70 | 40 | 18 | 0.5 |
| XGBoost_Permutation_Top10%_t80 | 40 | 16 | 0.4 |
| mRMR (Top 10%)_t40 | 40 | 83 | 2.1 |
| mRMR (Top 10%)_t50 | 40 | 60 | 1.5 |
| mRMR (Top 10%)_t60 | 40 | 40 | 1.0 |
| mRMR (Top 10%)_t70 | 34 | 29 | 0.9 |
| mRMR (Top 10%)_t80 | 30 | 26 | 0.9 |

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
| ElasticNet_Lenient | 40 | 87 | 2.2 |
| ElasticNet_RFE | 38 | 35 | 0.9 |
| ElasticNet_Strict | 39 | 32 | 0.8 |
| FDR (p < 0.01) | 6 | 12 | 2.0 |
| FDR (p < 0.05) | 33 | 86 | 2.6 |
| FDR (p < 0.1) | 36 | 122 | 3.4 |
| LASSO_Lenient | 40 | 57 | 1.4 |
| LASSO_RFE | 38 | 26 | 0.7 |
| LASSO_Strict | 31 | 21 | 0.7 |
| LogisticRegression_Permutation_Top10% | 40 | 16 | 0.4 |
| Mutual Information (Top 10%) | 40 | 87 | 2.2 |
| NaiveBayes_Permutation_AboveMean | 40 | 139 | 3.5 |
| NaiveBayes_Permutation_Top10% | 40 | 58 | 1.4 |
| RFE (RandomForest) | 40 | 151 | 3.8 |
| RF_Importance | 40 | 165 | 4.1 |
| RandomForest_Permutation_Top10% | 40 | 16 | 0.4 |
| Ridge_Strict | 40 | 162 | 4.0 |
| SVM_RBF_Permutation_Top10% | 40 | 16 | 0.4 |
| XGB_Importance | 39 | 39 | 1.0 |
| XGBoost_Permutation_AboveMean | 16 | 10 | 0.6 |
| XGBoost_Permutation_Top10% | 40 | 25 | 0.6 |
| mRMR (Top 10%) | 40 | 83 | 2.1 |

**Total signatures at 40% threshold**: 836

#### Threshold 50%

| Base Method | Signatures Found | Total Features | Avg Features/Signature |
|-------------|------------------|----------------|------------------------|
| All Features (Baseline) | 40 | 166 | 4.2 |
| ElasticNet_Lenient | 40 | 53 | 1.3 |
| ElasticNet_RFE | 30 | 18 | 0.6 |
| ElasticNet_Strict | 28 | 21 | 0.8 |
| FDR (p < 0.01) | 3 | 6 | 2.0 |
| FDR (p < 0.05) | 30 | 53 | 1.8 |
| FDR (p < 0.1) | 35 | 103 | 2.9 |
| LASSO_Lenient | 35 | 29 | 0.8 |
| LASSO_RFE | 16 | 11 | 0.7 |
| LASSO_Strict | 22 | 17 | 0.8 |
| LogisticRegression_Permutation_Top10% | 40 | 16 | 0.4 |
| Mutual Information (Top 10%) | 40 | 65 | 1.6 |
| NaiveBayes_Permutation_AboveMean | 40 | 77 | 1.9 |
| NaiveBayes_Permutation_Top10% | 40 | 39 | 1.0 |
| RFE (RandomForest) | 40 | 133 | 3.3 |
| RF_Importance | 40 | 154 | 3.9 |
| RandomForest_Permutation_Top10% | 40 | 16 | 0.4 |
| Ridge_Strict | 40 | 159 | 4.0 |
| SVM_RBF_Permutation_Top10% | 40 | 16 | 0.4 |
| XGB_Importance | 33 | 22 | 0.7 |
| XGBoost_Permutation_AboveMean | 6 | 3 | 0.5 |
| XGBoost_Permutation_Top10% | 40 | 19 | 0.5 |
| mRMR (Top 10%) | 40 | 60 | 1.5 |

**Total signatures at 50% threshold**: 758

#### Threshold 60%

| Base Method | Signatures Found | Total Features | Avg Features/Signature |
|-------------|------------------|----------------|------------------------|
| All Features (Baseline) | 40 | 166 | 4.2 |
| ElasticNet_Lenient | 37 | 38 | 1.0 |
| ElasticNet_RFE | 10 | 7 | 0.7 |
| ElasticNet_Strict | 19 | 15 | 0.8 |
| FDR (p < 0.01) | 1 | 3 | 3.0 |
| FDR (p < 0.05) | 24 | 39 | 1.6 |
| FDR (p < 0.1) | 31 | 78 | 2.5 |
| LASSO_Lenient | 30 | 22 | 0.7 |
| LASSO_RFE | 8 | 7 | 0.9 |
| LASSO_Strict | 12 | 11 | 0.9 |
| LogisticRegression_Permutation_Top10% | 40 | 16 | 0.4 |
| Mutual Information (Top 10%) | 40 | 41 | 1.0 |
| NaiveBayes_Permutation_AboveMean | 38 | 42 | 1.1 |
| NaiveBayes_Permutation_Top10% | 40 | 30 | 0.8 |
| RFE (RandomForest) | 40 | 113 | 2.8 |
| RF_Importance | 40 | 119 | 3.0 |
| RandomForest_Permutation_Top10% | 40 | 16 | 0.4 |
| Ridge_Strict | 40 | 154 | 3.9 |
| SVM_RBF_Permutation_Top10% | 40 | 16 | 0.4 |
| XGB_Importance | 20 | 11 | 0.6 |
| XGBoost_Permutation_AboveMean | 3 | 2 | 0.7 |
| XGBoost_Permutation_Top10% | 40 | 18 | 0.5 |
| mRMR (Top 10%) | 40 | 40 | 1.0 |

**Total signatures at 60% threshold**: 673

#### Threshold 70%

| Base Method | Signatures Found | Total Features | Avg Features/Signature |
|-------------|------------------|----------------|------------------------|
| All Features (Baseline) | 40 | 166 | 4.2 |
| ElasticNet_Lenient | 31 | 24 | 0.8 |
| ElasticNet_RFE | 4 | 4 | 1.0 |
| ElasticNet_Strict | 11 | 10 | 0.9 |
| FDR (p < 0.01) | 1 | 3 | 3.0 |
| FDR (p < 0.05) | 15 | 27 | 1.8 |
| FDR (p < 0.1) | 28 | 57 | 2.0 |
| LASSO_Lenient | 19 | 18 | 0.9 |
| LASSO_RFE | 4 | 3 | 0.8 |
| LASSO_Strict | 6 | 6 | 1.0 |
| LogisticRegression_Permutation_Top10% | 40 | 16 | 0.4 |
| Mutual Information (Top 10%) | 30 | 27 | 0.9 |
| NaiveBayes_Permutation_AboveMean | 29 | 18 | 0.6 |
| NaiveBayes_Permutation_Top10% | 37 | 19 | 0.5 |
| RFE (RandomForest) | 40 | 81 | 2.0 |
| RF_Importance | 40 | 86 | 2.1 |
| RandomForest_Permutation_Top10% | 40 | 16 | 0.4 |
| Ridge_Strict | 40 | 149 | 3.7 |
| SVM_RBF_Permutation_Top10% | 40 | 16 | 0.4 |
| XGB_Importance | 11 | 7 | 0.6 |
| XGBoost_Permutation_AboveMean | 2 | 2 | 1.0 |
| XGBoost_Permutation_Top10% | 40 | 18 | 0.5 |
| mRMR (Top 10%) | 34 | 29 | 0.9 |

**Total signatures at 70% threshold**: 582

#### Threshold 80%

| Base Method | Signatures Found | Total Features | Avg Features/Signature |
|-------------|------------------|----------------|------------------------|
| All Features (Baseline) | 40 | 166 | 4.2 |
| ElasticNet_Lenient | 19 | 13 | 0.7 |
| ElasticNet_RFE | 3 | 3 | 1.0 |
| ElasticNet_Strict | 5 | 5 | 1.0 |
| FDR (p < 0.01) | 1 | 3 | 3.0 |
| FDR (p < 0.05) | 9 | 17 | 1.9 |
| FDR (p < 0.1) | 22 | 40 | 1.8 |
| LASSO_Lenient | 10 | 10 | 1.0 |
| LASSO_RFE | 1 | 1 | 1.0 |
| LASSO_Strict | 2 | 2 | 1.0 |
| LogisticRegression_Permutation_Top10% | 40 | 16 | 0.4 |
| Mutual Information (Top 10%) | 21 | 16 | 0.8 |
| NaiveBayes_Permutation_AboveMean | 11 | 7 | 0.6 |
| NaiveBayes_Permutation_Top10% | 24 | 14 | 0.6 |
| RFE (RandomForest) | 25 | 42 | 1.7 |
| RF_Importance | 40 | 59 | 1.5 |
| RandomForest_Permutation_Top10% | 40 | 16 | 0.4 |
| Ridge_Strict | 40 | 133 | 3.3 |
| SVM_RBF_Permutation_Top10% | 40 | 16 | 0.4 |
| XGB_Importance | 5 | 3 | 0.6 |
| XGBoost_Permutation_AboveMean | 1 | 1 | 1.0 |
| XGBoost_Permutation_Top10% | 40 | 16 | 0.4 |
| mRMR (Top 10%) | 30 | 26 | 0.9 |

**Total signatures at 80% threshold**: 469


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
| Bcells CD27posIgDneg_total | 75.0% |
| CD8 RO DR_CD8 | 67.5% |
| CD14+16+mono_CD3neg | 55.0% |
| DR_CD8RO | 47.5% |
| NKCD16_NK | 45.0% |
| Tconv memDR_total | 45.0% |
| Tconv memCXCR3_mem | 32.5% |
| Tconv memCCR5_mem | 30.0% |
| CD27negIgDneg_Bcells | 30.0% |
| CD8 RO DR_CD3 | 25.0% |
| NK Ki67_NK | 22.5% |
| Tconv memDR_mem | 22.5% |
| NK Ki67_nonTnonB | 22.5% |
| Tconv memDR_CD3 | 22.5% |
| CD14+16+mono_total | 20.0% |
| NKCD56hi_total | 17.5% |
| NKCD16_nonTnonB | 17.5% |
| CD8 RO CD56_total | 17.5% |
| CD8 RO CD56_CD3 | 17.5% |
| CD8 RO CD56_CD8 | 15.0% |
| CD8 RO CCR5_CD3 | 15.0% |
| Treg naive_CD4 | 15.0% |
| NKCD56hi_NK | 15.0% |
| CD56_CD8RO | 12.5% |
| CD8 RA naive_CD3 | 12.5% |
| CD8 RA_CD3 | 12.5% |
| Bcells_total | 12.5% |
| Tconv memTIGIT_mem | 12.5% |
| Tconv memKi67_mem | 12.5% |
| CD8 RO CCR5_total | 10.0% |
| CD8 RO CXCR3_CD3 | 10.0% |
| Tconv memCCR6_mem | 10.0% |
| Treg memory_CD3 | 10.0% |
| nonTnonB_CD3neg | 10.0% |
| Tconv memCCR4_CD3 | 7.5% |
| Tconv memKi67_total | 7.5% |
| CD14+16+mono_myeloid | 7.5% |
| myeloid_CD3neg | 7.5% |
| Tconv memDR_Tconv | 7.5% |
| CD3hi_CD4neg | 7.5% |
| Bcells_CD3neg | 7.5% |
| NK Ki67_CD3neg | 7.5% |
| Ki67_Bcells | 7.5% |
| Bcells memory_CD3neg | 7.5% |
| Treg memory_total | 7.5% |
| CD8 RO CCR6_CD3 | 5.0% |
| naive_Bcells | 5.0% |
| Bcells Ki67_total | 5.0% |
| CD16mono_myeloid | 5.0% |
| Bcells memory_total | 5.0% |
| Tconv memCD27_Tconv | 5.0% |
| Tconv memCD56_mem | 5.0% |
| Bcells naive_total | 5.0% |
| CD8 RO CCR6_CD8 | 5.0% |
| CCR6_CD8RO | 5.0% |
| CD3hi_total | 5.0% |
| CD8 RA naive_total | 5.0% |
| Tconv memCD27_CD3 | 5.0% |
| Tconv mem_CD3 | 5.0% |
| NKCD16_total | 2.5% |
| NK_total | 2.5% |
| Treg memory_CD4 | 2.5% |
| NKCD16_CD3neg | 2.5% |
| CD27IgD_Bcells | 2.5% |
| NK_CD3neg | 2.5% |
| Tconv memCXCR3_total | 2.5% |
| CD16mono_CD3neg | 2.5% |
| CCR5_CD8RO | 2.5% |
| Tconv naive_Tconv | 2.5% |
| Tconv mem_Tconv | 2.5% |
| CXCR3_CD8RO | 2.5% |
| CD8 RO intB7_total | 2.5% |
| CD8 RO TIGIT_CD8 | 2.5% |
| memory_Bcells | 2.5% |
| Tconv memCCR4_Tconv | 2.5% |
| Treg naive_CD3 | 2.5% |
| Tconv memCD27_mem | 2.5% |
| CD8 RO intB7_CD3 | 2.5% |
| CD8pos_CD3 | 2.5% |
| NK_nonTnonB | 2.5% |
| Tconv memPD1_total | 2.5% |
| CD8 RO DR_total | 2.5% |
| Tconv memCCR4_mem | 2.5% |
| CD8 RO Ki67_total | 2.5% |
| CD4 Treg _CD3 | 2.5% |
| CD4neg_total | 2.5% |
| NK Ki67_total | 2.5% |

**Total features selected by ElasticNet_Lenient_t40**: 87

#### ElasticNet_Lenient_t50

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD8 RO DR_CD8 | 55.0% |
| Bcells CD27posIgDneg_total | 52.5% |
| CD14+16+mono_CD3neg | 42.5% |
| NKCD16_NK | 35.0% |
| DR_CD8RO | 30.0% |
| Tconv memDR_total | 25.0% |
| Tconv memCCR5_mem | 22.5% |
| Tconv memDR_mem | 20.0% |
| Tconv memCXCR3_mem | 17.5% |
| CD27negIgDneg_Bcells | 17.5% |
| NK Ki67_nonTnonB | 17.5% |
| CD8 RO DR_CD3 | 15.0% |
| NK Ki67_NK | 12.5% |
| CD8 RO CCR5_CD3 | 12.5% |
| NKCD56hi_NK | 12.5% |
| Treg naive_CD4 | 12.5% |
| NKCD56hi_total | 12.5% |
| CD8 RO CD56_CD8 | 12.5% |
| CD14+16+mono_total | 10.0% |
| NKCD16_nonTnonB | 10.0% |
| CD8 RA_CD3 | 10.0% |
| nonTnonB_CD3neg | 7.5% |
| Treg memory_CD3 | 7.5% |
| Bcells_total | 5.0% |
| Tconv memDR_CD3 | 5.0% |
| CD8 RO CD56_CD3 | 5.0% |
| CD8 RA naive_CD3 | 5.0% |
| Ki67_Bcells | 5.0% |
| myeloid_CD3neg | 5.0% |
| Tconv memTIGIT_mem | 5.0% |
| CD8 RO CCR5_total | 5.0% |
| Tconv memKi67_mem | 5.0% |
| CD8 RO CXCR3_CD3 | 5.0% |
| Tconv memKi67_total | 2.5% |
| NKCD16_total | 2.5% |
| NK_total | 2.5% |
| naive_Bcells | 2.5% |
| CD8 RO CCR6_CD8 | 2.5% |
| CD56_CD8RO | 2.5% |
| CCR6_CD8RO | 2.5% |
| CD27IgD_Bcells | 2.5% |
| CD3hi_CD4neg | 2.5% |
| Tconv memCCR4_Tconv | 2.5% |
| CD8 RO intB7_CD3 | 2.5% |
| Tconv memCD56_mem | 2.5% |
| CD8 RO CCR6_CD3 | 2.5% |
| Treg naive_CD3 | 2.5% |
| CD8 RO CD56_total | 2.5% |
| Bcells_CD3neg | 2.5% |
| Tconv memCCR6_mem | 2.5% |
| Bcells memory_CD3neg | 2.5% |
| Tconv memDR_Tconv | 2.5% |
| NK Ki67_CD3neg | 2.5% |

**Total features selected by ElasticNet_Lenient_t50**: 53

#### ElasticNet_Lenient_t60

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD8 RO DR_CD8 | 37.8% |
| CD14+16+mono_CD3neg | 35.1% |
| Bcells CD27posIgDneg_total | 35.1% |
| NKCD16_NK | 18.9% |
| Tconv memCCR5_mem | 18.9% |
| DR_CD8RO | 16.2% |
| Tconv memDR_total | 13.5% |
| Tconv memDR_mem | 13.5% |
| NK Ki67_nonTnonB | 13.5% |
| CD8 RO CCR5_CD3 | 10.8% |
| CD14+16+mono_total | 8.1% |
| NKCD16_nonTnonB | 8.1% |
| Tconv memCXCR3_mem | 8.1% |
| CD8 RO DR_CD3 | 8.1% |
| Treg memory_CD3 | 5.4% |
| CD27negIgDneg_Bcells | 5.4% |
| Tconv memTIGIT_mem | 5.4% |
| Treg naive_CD4 | 5.4% |
| CD8 RA_CD3 | 5.4% |
| NK Ki67_NK | 5.4% |
| CD8 RO CD56_CD8 | 5.4% |
| NKCD56hi_NK | 5.4% |
| NKCD16_total | 2.7% |
| NK_total | 2.7% |
| Tconv memKi67_total | 2.7% |
| CD3hi_CD4neg | 2.7% |
| Ki67_Bcells | 2.7% |
| CD56_CD8RO | 2.7% |
| Tconv memKi67_mem | 2.7% |
| myeloid_CD3neg | 2.7% |
| CD8 RO CCR6_CD3 | 2.7% |
| CD8 RO intB7_CD3 | 2.7% |
| CD8 RO CXCR3_CD3 | 2.7% |
| CD8 RO CD56_CD3 | 2.7% |
| nonTnonB_CD3neg | 2.7% |
| CD8 RO CD56_total | 2.7% |
| NKCD56hi_total | 2.7% |
| CD8 RA naive_CD3 | 2.7% |

**Total features selected by ElasticNet_Lenient_t60**: 38

#### ElasticNet_Lenient_t70

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Bcells CD27posIgDneg_total | 29.0% |
| CD14+16+mono_CD3neg | 29.0% |
| CD8 RO DR_CD8 | 25.8% |
| NKCD16_NK | 12.9% |
| Tconv memDR_total | 9.7% |
| CD8 RO DR_CD3 | 9.7% |
| DR_CD8RO | 9.7% |
| Tconv memCXCR3_mem | 9.7% |
| CD8 RO CCR5_CD3 | 9.7% |
| NK Ki67_NK | 6.5% |
| Tconv memCCR5_mem | 6.5% |
| Tconv memDR_mem | 6.5% |
| CD27negIgDneg_Bcells | 6.5% |
| CD14+16+mono_total | 6.5% |
| CD8 RO CD56_CD8 | 3.2% |
| Tconv memKi67_total | 3.2% |
| CD8 RO CD56_CD3 | 3.2% |
| CD56_CD8RO | 3.2% |
| CD8 RO CXCR3_CD3 | 3.2% |
| CD8 RA_CD3 | 3.2% |
| Treg naive_CD4 | 3.2% |
| Tconv memTIGIT_mem | 3.2% |
| CD8 RA naive_CD3 | 3.2% |
| NK Ki67_nonTnonB | 3.2% |

**Total features selected by ElasticNet_Lenient_t70**: 24

#### ElasticNet_Lenient_t80

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD14+16+mono_CD3neg | 26.3% |
| CD8 RO DR_CD8 | 26.3% |
| Bcells CD27posIgDneg_total | 26.3% |
| CD8 RO CCR5_CD3 | 10.5% |
| Tconv memCCR5_mem | 10.5% |
| DR_CD8RO | 10.5% |
| NKCD16_NK | 10.5% |
| NK Ki67_NK | 5.3% |
| CD8 RO DR_CD3 | 5.3% |
| Tconv memDR_total | 5.3% |
| Treg naive_CD4 | 5.3% |
| CD27negIgDneg_Bcells | 5.3% |
| Tconv memDR_mem | 5.3% |

**Total features selected by ElasticNet_Lenient_t80**: 13

#### ElasticNet_RFE_t40

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD14+16+mono_CD3neg | 31.6% |
| CD8 RO DR_CD8 | 28.9% |
| Bcells CD27posIgDneg_total | 26.3% |
| Tconv memDR_mem | 18.4% |
| NKCD16_NK | 15.8% |
| CD27negIgDneg_Bcells | 13.2% |
| DR_CD8RO | 13.2% |
| Tconv memCCR5_mem | 13.2% |
| CD8 RO DR_CD3 | 13.2% |
| Tconv memDR_total | 13.2% |
| CD8 RO CCR5_CD3 | 10.5% |
| NK Ki67_nonTnonB | 7.9% |
| Bcells_total | 5.3% |
| Bcells naive_total | 5.3% |
| NK Ki67_NK | 5.3% |
| Tconv memCXCR3_mem | 5.3% |
| Treg naive_CD4 | 5.3% |
| CD14+16+mono_total | 5.3% |
| CD8 RO CD56_CD8 | 5.3% |
| Tconv memKi67_total | 2.6% |
| CD27IgD_Bcells | 2.6% |
| NKCD16_total | 2.6% |
| myeloid_CD3neg | 2.6% |
| Tconv memKi67_mem | 2.6% |
| CD3hi_CD4neg | 2.6% |
| Tconv memDR_CD3 | 2.6% |
| Tconv memDR_Tconv | 2.6% |
| CD8 RO CXCR3_CD3 | 2.6% |
| CD8 RO intB7_CD3 | 2.6% |
| Ki67_Bcells | 2.6% |
| NKCD56hi_NK | 2.6% |
| Bcells_CD3neg | 2.6% |
| CD8 RO CCR5_total | 2.6% |
| Tconv memCCR6_mem | 2.6% |
| Bcells memory_CD3neg | 2.6% |

**Total features selected by ElasticNet_RFE_t40**: 35

#### ElasticNet_RFE_t50

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD14+16+mono_CD3neg | 26.7% |
| CD8 RO DR_CD8 | 23.3% |
| CD8 RO CCR5_CD3 | 10.0% |
| Tconv memCCR5_mem | 10.0% |
| CD27negIgDneg_Bcells | 10.0% |
| NKCD16_NK | 10.0% |
| Bcells CD27posIgDneg_total | 10.0% |
| Tconv memDR_total | 10.0% |
| CD8 RO DR_CD3 | 6.7% |
| Tconv memDR_mem | 6.7% |
| DR_CD8RO | 3.3% |
| CD27IgD_Bcells | 3.3% |
| NK Ki67_NK | 3.3% |
| Bcells_total | 3.3% |
| CD8 RO CXCR3_CD3 | 3.3% |
| NKCD56hi_NK | 3.3% |
| CD14+16+mono_total | 3.3% |
| NK Ki67_nonTnonB | 3.3% |

**Total features selected by ElasticNet_RFE_t50**: 18

#### ElasticNet_RFE_t60

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD14+16+mono_CD3neg | 30.0% |
| CD8 RO DR_CD8 | 20.0% |
| Bcells CD27posIgDneg_total | 20.0% |
| NK Ki67_NK | 10.0% |
| Tconv memDR_total | 10.0% |
| Tconv memCCR5_mem | 10.0% |
| Tconv memDR_mem | 10.0% |

**Total features selected by ElasticNet_RFE_t60**: 7

#### ElasticNet_RFE_t70

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD14+16+mono_CD3neg | 25.0% |
| CD8 RO DR_CD8 | 25.0% |
| Tconv memDR_total | 25.0% |
| Bcells CD27posIgDneg_total | 25.0% |

**Total features selected by ElasticNet_RFE_t70**: 4

#### ElasticNet_RFE_t80

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD14+16+mono_CD3neg | 33.3% |
| Tconv memDR_total | 33.3% |
| Bcells CD27posIgDneg_total | 33.3% |

**Total features selected by ElasticNet_RFE_t80**: 3

#### ElasticNet_Strict_t40

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD8 RO DR_CD8 | 35.9% |
| Bcells CD27posIgDneg_total | 35.9% |
| DR_CD8RO | 28.2% |
| CD14+16+mono_CD3neg | 17.9% |
| Tconv memCCR5_mem | 15.4% |
| CD8 RO DR_CD3 | 15.4% |
| NKCD16_NK | 12.8% |
| Tconv memDR_mem | 10.3% |
| Tconv memDR_total | 10.3% |
| NK Ki67_NK | 7.7% |
| Tconv memCXCR3_mem | 7.7% |
| CD8 RO CD56_CD8 | 7.7% |
| CD27negIgDneg_Bcells | 7.7% |
| CD8 RA_CD3 | 7.7% |
| CD8 RO CD56_total | 5.1% |
| naive_Bcells | 5.1% |
| CD8 RO CCR5_CD3 | 5.1% |
| CD27IgD_Bcells | 2.6% |
| CD56_CD8RO | 2.6% |
| Bcells memory_total | 2.6% |
| CCR5_CD8RO | 2.6% |
| Tconv memDR_Tconv | 2.6% |
| CD8 RO CXCR3_CD3 | 2.6% |
| Tconv memDR_CD3 | 2.6% |
| Treg naive_CD4 | 2.6% |
| NKCD56hi_NK | 2.6% |
| NKCD16_nonTnonB | 2.6% |
| Tconv memTIGIT_mem | 2.6% |
| NKCD56hi_total | 2.6% |
| Tconv memCCR6_mem | 2.6% |
| CD14+16+mono_total | 2.6% |
| NK Ki67_nonTnonB | 2.6% |

**Total features selected by ElasticNet_Strict_t40**: 32

#### ElasticNet_Strict_t50

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD8 RO DR_CD8 | 32.1% |
| Bcells CD27posIgDneg_total | 28.6% |
| DR_CD8RO | 14.3% |
| CD14+16+mono_CD3neg | 14.3% |
| NKCD16_NK | 14.3% |
| Tconv memDR_total | 10.7% |
| CD8 RO DR_CD3 | 7.1% |
| Tconv memCCR5_mem | 7.1% |
| NK Ki67_NK | 7.1% |
| CD8 RA_CD3 | 7.1% |
| CD8 RO CCR5_CD3 | 7.1% |
| CD27negIgDneg_Bcells | 7.1% |
| CD8 RO CXCR3_CD3 | 3.6% |
| Treg naive_CD4 | 3.6% |
| Tconv memTIGIT_mem | 3.6% |
| CD8 RO CD56_total | 3.6% |
| NKCD56hi_total | 3.6% |
| Tconv memCCR6_mem | 3.6% |
| CD14+16+mono_total | 3.6% |
| Tconv memDR_mem | 3.6% |
| Tconv memCXCR3_mem | 3.6% |

**Total features selected by ElasticNet_Strict_t50**: 21

#### ElasticNet_Strict_t60

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Bcells CD27posIgDneg_total | 26.3% |
| CD8 RO DR_CD8 | 21.1% |
| DR_CD8RO | 15.8% |
| CD14+16+mono_CD3neg | 10.5% |
| CD8 RO CCR5_CD3 | 10.5% |
| NK Ki67_NK | 5.3% |
| Tconv memCCR5_mem | 5.3% |
| Tconv memDR_total | 5.3% |
| CD8 RO CXCR3_CD3 | 5.3% |
| Treg naive_CD4 | 5.3% |
| NKCD16_NK | 5.3% |
| CD27negIgDneg_Bcells | 5.3% |
| CD8 RO DR_CD3 | 5.3% |
| Tconv memDR_mem | 5.3% |
| Tconv memCXCR3_mem | 5.3% |

**Total features selected by ElasticNet_Strict_t60**: 15

#### ElasticNet_Strict_t70

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD8 RO DR_CD8 | 27.3% |
| Bcells CD27posIgDneg_total | 18.2% |
| NK Ki67_NK | 9.1% |
| Tconv memCCR5_mem | 9.1% |
| CD14+16+mono_CD3neg | 9.1% |
| DR_CD8RO | 9.1% |
| Treg naive_CD4 | 9.1% |
| NKCD16_NK | 9.1% |
| CD27negIgDneg_Bcells | 9.1% |
| Tconv memDR_mem | 9.1% |

**Total features selected by ElasticNet_Strict_t70**: 10

#### ElasticNet_Strict_t80

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Tconv memCCR5_mem | 20.0% |
| CD14+16+mono_CD3neg | 20.0% |
| Treg naive_CD4 | 20.0% |
| NKCD16_NK | 20.0% |
| Tconv memDR_mem | 20.0% |

**Total features selected by ElasticNet_Strict_t80**: 5

#### FDR (p < 0.01)_t40

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Tconv memDR_mem | 66.7% |
| Tconv memDR_CD3 | 66.7% |
| Tconv memDR_Tconv | 66.7% |
| CD8 RO DR_CD3 | 16.7% |
| CCR5_CD8RO | 16.7% |
| Bcells_total | 16.7% |
| Bcells CD27posIgDneg_total | 16.7% |
| Tconv memCCR5_mem | 16.7% |
| myeloid_CD3neg | 16.7% |
| Bcells naive_total | 16.7% |
| Bcells naive_CD3neg | 16.7% |
| Tconv memDR_total | 16.7% |

**Total features selected by FDR (p < 0.01)_t40**: 12

#### FDR (p < 0.01)_t50

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Tconv memDR_mem | 66.7% |
| Bcells_total | 33.3% |
| Bcells CD27posIgDneg_total | 33.3% |
| Tconv memDR_total | 33.3% |
| Tconv memDR_CD3 | 33.3% |
| Tconv memDR_Tconv | 33.3% |

**Total features selected by FDR (p < 0.01)_t50**: 6

#### FDR (p < 0.01)_t60

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Tconv memDR_total | 100.0% |
| Tconv memDR_CD3 | 100.0% |
| Tconv memDR_Tconv | 100.0% |

**Total features selected by FDR (p < 0.01)_t60**: 3

#### FDR (p < 0.01)_t70

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Tconv memDR_total | 100.0% |
| Tconv memDR_CD3 | 100.0% |
| Tconv memDR_Tconv | 100.0% |

**Total features selected by FDR (p < 0.01)_t70**: 3

#### FDR (p < 0.01)_t80

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Tconv memDR_total | 100.0% |
| Tconv memDR_CD3 | 100.0% |
| Tconv memDR_Tconv | 100.0% |

**Total features selected by FDR (p < 0.01)_t80**: 3

#### FDR (p < 0.05)_t40

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Bcells CD27posIgDneg_total | 75.8% |
| Tconv memDR_CD3 | 60.6% |
| Tconv memDR_Tconv | 54.5% |
| myeloid_CD3neg | 51.5% |
| Bcells_CD3neg | 48.5% |
| nonTnonB_CD3neg | 48.5% |
| Bcells naive_CD3neg | 45.5% |
| Tconv memDR_mem | 45.5% |
| Bcells_total | 42.4% |
| CD8 RA naive_total | 39.4% |
| CD8 RO CCR5_total | 33.3% |
| CD14+16+mono_total | 33.3% |
| CD14+16+mono_CD3neg | 33.3% |
| Bcells naive_total | 30.3% |
| CD8 RA_total | 30.3% |
| CD8 RA naive_CD3 | 30.3% |
| Tconv memDR_total | 30.3% |
| Bcells memory_CD3neg | 27.3% |
| nonTnonB_total | 24.2% |
| myeloid_total | 24.2% |
| CD14mono_CD3neg | 24.2% |
| CD14mono_total | 24.2% |
| CD8 RO DR_CD3 | 21.2% |
| NKCD16_nonTnonB | 21.2% |
| Tconv memCCR5_mem | 21.2% |
| NK_nonTnonB | 21.2% |
| CD27negIgDneg_Bcells | 21.2% |
| CD8pos_total | 21.2% |
| CD8 RO DR_CD8 | 21.2% |
| NK Ki67_nonTnonB | 18.2% |
| Bcells memory_total | 18.2% |
| CD3neg_total | 15.2% |
| CD3pos_total | 15.2% |
| CD8 RO intB7_total | 15.2% |
| CD8 RA CCR7 naive_CD8 | 12.1% |
| DR_CD8RO | 12.1% |
| CD8 RO CCR5_CD3 | 12.1% |
| Tconv memintB7_total | 12.1% |
| Tconv memintB7_mem | 12.1% |
| CD8 RO CXCR3_total | 9.1% |
| Tconv memCCR5_total | 9.1% |
| Tconv naive_total | 9.1% |
| intB7_CD8RO | 9.1% |
| CD14+16+mono_myeloid | 9.1% |
| CCR5_CD8RO | 9.1% |
| CD8 RO CCR6_total | 9.1% |
| Tconv memCCR6_mem | 9.1% |
| Tconv memCD27_Tconv | 9.1% |
| Ki67_Bcells | 9.1% |
| Tconv memCXCR3_mem | 9.1% |
| CD8 RO CD27_total | 6.1% |
| CD8 RA_CD3 | 6.1% |
| Tconv memCXCR3_Tconv | 6.1% |
| Tconv memCCR5_Tconv | 6.1% |
| Tconv naive_Tconv | 6.1% |
| Tconv mem_Tconv | 6.1% |
| CD8 RO CXCR3_CD3 | 6.1% |
| naive_Bcells | 6.1% |
| CD4 Tconv_total | 6.1% |
| Tconv mem_CD3 | 6.1% |
| Tconv memCD27_CD3 | 6.1% |
| CD8 RO intB7_CD8 | 6.1% |
| CD8 RO CCR5_CD8 | 6.1% |
| Ki67_CD8RO | 3.0% |
| CXCR3_CD8RO | 3.0% |
| Tconv memCXCR3_total | 3.0% |
| Tconv memCCR6_CD3 | 3.0% |
| Tconv memCCR5_CD3 | 3.0% |
| Tconv memCXCR3_CD3 | 3.0% |
| Treg memory_CD4 | 3.0% |
| CD8 RO intB7_CD3 | 3.0% |
| Tconv memintB7_CD3 | 3.0% |
| CD8 RO_total | 3.0% |
| CD8 RO TIGIT_total | 3.0% |
| CD8 RO CCR6_CD3 | 3.0% |
| Tconv memTIGIT_Tconv | 3.0% |
| CD16mono_myeloid | 3.0% |
| NK Ki67_NK | 3.0% |
| Tconv memCCR6_total | 3.0% |
| NK Ki67_CD3neg | 3.0% |
| CD8 RO CD56_CD8 | 3.0% |
| CD56_CD8RO | 3.0% |
| Treg naive_total | 3.0% |
| NKCD16_CD3neg | 3.0% |
| Tconv naive_CD3 | 3.0% |
| NKCD56hi_nonTnonB | 3.0% |

**Total features selected by FDR (p < 0.05)_t40**: 86

#### FDR (p < 0.05)_t50

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Bcells CD27posIgDneg_total | 76.7% |
| myeloid_CD3neg | 36.7% |
| Tconv memDR_Tconv | 36.7% |
| Tconv memDR_CD3 | 36.7% |
| Bcells naive_CD3neg | 36.7% |
| Tconv memDR_mem | 33.3% |
| Bcells_total | 33.3% |
| nonTnonB_CD3neg | 33.3% |
| Bcells_CD3neg | 30.0% |
| Bcells naive_total | 26.7% |
| CD14+16+mono_total | 26.7% |
| CD8 RO CCR5_total | 23.3% |
| Tconv memDR_total | 23.3% |
| CD8 RA naive_total | 20.0% |
| CD27negIgDneg_Bcells | 20.0% |
| NKCD16_nonTnonB | 16.7% |
| CD8 RA_total | 16.7% |
| nonTnonB_total | 16.7% |
| CD8 RA naive_CD3 | 16.7% |
| CD14+16+mono_CD3neg | 13.3% |
| CD8 RO DR_CD8 | 10.0% |
| CD14mono_total | 10.0% |
| myeloid_total | 10.0% |
| NK_nonTnonB | 10.0% |
| CD14mono_CD3neg | 10.0% |
| CD8pos_total | 10.0% |
| CD8 RO CCR5_CD3 | 10.0% |
| NK Ki67_nonTnonB | 10.0% |
| CD8 RO DR_CD3 | 10.0% |
| CCR5_CD8RO | 6.7% |
| Tconv memCCR5_mem | 6.7% |
| CD8 RO CXCR3_total | 6.7% |
| DR_CD8RO | 6.7% |
| Bcells memory_total | 6.7% |
| Tconv memintB7_mem | 6.7% |
| Ki67_Bcells | 6.7% |
| CD14+16+mono_myeloid | 6.7% |
| Tconv memCCR6_mem | 6.7% |
| CD3pos_total | 6.7% |
| CD3neg_total | 6.7% |
| CXCR3_CD8RO | 3.3% |
| Tconv memCCR5_total | 3.3% |
| CD8 RO intB7_total | 3.3% |
| Tconv memCXCR3_CD3 | 3.3% |
| Tconv memCXCR3_mem | 3.3% |
| intB7_CD8RO | 3.3% |
| CD16mono_myeloid | 3.3% |
| NK Ki67_CD3neg | 3.3% |
| NK Ki67_NK | 3.3% |
| CD4 Tconv_total | 3.3% |
| Tconv naive_total | 3.3% |
| Tconv mem_Tconv | 3.3% |
| Tconv naive_Tconv | 3.3% |

**Total features selected by FDR (p < 0.05)_t50**: 53

#### FDR (p < 0.05)_t60

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Bcells CD27posIgDneg_total | 45.8% |
| Bcells naive_CD3neg | 37.5% |
| Tconv memDR_CD3 | 37.5% |
| Tconv memDR_Tconv | 37.5% |
| Tconv memDR_mem | 29.2% |
| myeloid_CD3neg | 29.2% |
| Bcells_CD3neg | 25.0% |
| Bcells_total | 25.0% |
| nonTnonB_CD3neg | 25.0% |
| Bcells naive_total | 20.8% |
| CD14+16+mono_total | 16.7% |
| CD8 RA naive_CD3 | 16.7% |
| CD14+16+mono_CD3neg | 12.5% |
| CD8 RA naive_total | 12.5% |
| CD8 RO DR_CD8 | 12.5% |
| NKCD16_nonTnonB | 8.3% |
| Ki67_Bcells | 8.3% |
| myeloid_total | 8.3% |
| CD8 RO CCR5_total | 8.3% |
| CD8 RA_total | 8.3% |
| NK Ki67_nonTnonB | 8.3% |
| CD14+16+mono_myeloid | 8.3% |
| DR_CD8RO | 8.3% |
| Tconv memDR_total | 4.2% |
| CXCR3_CD8RO | 4.2% |
| Tconv memintB7_mem | 4.2% |
| CCR5_CD8RO | 4.2% |
| CD8 RO DR_CD3 | 4.2% |
| Tconv memCCR5_mem | 4.2% |
| CD8 RO CCR5_CD3 | 4.2% |
| CD8pos_total | 4.2% |
| CD3neg_total | 4.2% |
| CD3pos_total | 4.2% |
| nonTnonB_total | 4.2% |
| CD16mono_myeloid | 4.2% |
| CD14mono_CD3neg | 4.2% |
| NK_nonTnonB | 4.2% |
| Tconv mem_Tconv | 4.2% |
| Tconv naive_Tconv | 4.2% |

**Total features selected by FDR (p < 0.05)_t60**: 39

#### FDR (p < 0.05)_t70

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Tconv memDR_CD3 | 40.0% |
| Tconv memDR_Tconv | 40.0% |
| Bcells CD27posIgDneg_total | 33.3% |
| Tconv memDR_mem | 26.7% |
| Bcells_total | 26.7% |
| Bcells naive_CD3neg | 20.0% |
| Bcells naive_total | 13.3% |
| CD14+16+mono_total | 13.3% |
| Bcells_CD3neg | 13.3% |
| nonTnonB_CD3neg | 13.3% |
| myeloid_CD3neg | 13.3% |
| CD8 RO DR_CD3 | 6.7% |
| CD14+16+mono_myeloid | 6.7% |
| CD14+16+mono_CD3neg | 6.7% |
| CD8 RO DR_CD8 | 6.7% |
| Tconv memCCR5_mem | 6.7% |
| DR_CD8RO | 6.7% |
| CCR5_CD8RO | 6.7% |
| Tconv memintB7_mem | 6.7% |
| Tconv memDR_total | 6.7% |
| CD8 RA_total | 6.7% |
| CD8 RA naive_total | 6.7% |
| nonTnonB_total | 6.7% |
| myeloid_total | 6.7% |
| Ki67_Bcells | 6.7% |
| CD8 RA naive_CD3 | 6.7% |
| NKCD16_nonTnonB | 6.7% |

**Total features selected by FDR (p < 0.05)_t70**: 27

#### FDR (p < 0.05)_t80

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Tconv memDR_Tconv | 44.4% |
| Bcells_total | 33.3% |
| Bcells CD27posIgDneg_total | 33.3% |
| Tconv memDR_CD3 | 33.3% |
| Bcells naive_CD3neg | 22.2% |
| Tconv memDR_mem | 22.2% |
| CD8 RO DR_CD3 | 11.1% |
| DR_CD8RO | 11.1% |
| CD8 RO DR_CD8 | 11.1% |
| Tconv memCCR5_mem | 11.1% |
| nonTnonB_CD3neg | 11.1% |
| Bcells naive_total | 11.1% |
| Bcells_CD3neg | 11.1% |
| Tconv memDR_total | 11.1% |
| CD8 RA naive_total | 11.1% |
| nonTnonB_total | 11.1% |
| Ki67_Bcells | 11.1% |

**Total features selected by FDR (p < 0.05)_t80**: 17

#### FDR (p < 0.1)_t40

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Bcells CD27posIgDneg_total | 83.3% |
| myeloid_CD3neg | 77.8% |
| Tconv memDR_CD3 | 77.8% |
| Tconv memDR_Tconv | 75.0% |
| nonTnonB_CD3neg | 69.4% |
| CD8 RA naive_total | 69.4% |
| Bcells_CD3neg | 69.4% |
| CD14+16+mono_total | 66.7% |
| CD8 RA_total | 66.7% |
| Bcells naive_CD3neg | 63.9% |
| Bcells_total | 63.9% |
| Tconv memDR_mem | 61.1% |
| CD14+16+mono_CD3neg | 61.1% |
| Bcells memory_CD3neg | 58.3% |
| NKCD16_nonTnonB | 58.3% |
| CD8 RA naive_CD3 | 55.6% |
| CD8 RO CCR5_total | 52.8% |
| Bcells naive_total | 52.8% |
| Bcells memory_total | 52.8% |
| NK_nonTnonB | 52.8% |
| CD14mono_CD3neg | 52.8% |
| Tconv memCCR5_mem | 50.0% |
| nonTnonB_total | 50.0% |
| CD8pos_total | 50.0% |
| CD8 RO CCR5_CD3 | 47.2% |
| CD27negIgDneg_Bcells | 47.2% |
| NK Ki67_nonTnonB | 44.4% |
| CD8 RO DR_CD8 | 41.7% |
| myeloid_total | 41.7% |
| CD8 RO DR_CD3 | 38.9% |
| CD14mono_total | 36.1% |
| CD14+16+mono_myeloid | 33.3% |
| DR_CD8RO | 33.3% |
| Tconv memDR_total | 33.3% |
| CD8 RA CCR7 naive_CD8 | 30.6% |
| CD8 RO intB7_total | 30.6% |
| CD3pos_total | 27.8% |
| Tconv mem_Tconv | 27.8% |
| CD3neg_total | 27.8% |
| Tconv naive_Tconv | 25.0% |
| Tconv naive_total | 25.0% |
| CD8 RO CCR6_total | 25.0% |
| CD8 RO CXCR3_total | 25.0% |
| Treg memory_CD3 | 25.0% |
| Tconv memintB7_mem | 22.2% |
| CCR5_CD8RO | 22.2% |
| CD4 Tconv_total | 22.2% |
| Tconv memintB7_total | 19.4% |
| Treg naive_total | 19.4% |
| NK Ki67_CD3neg | 19.4% |
| CD8 RO CD27_total | 19.4% |
| CD8 RA_CD3 | 19.4% |
| Tconv memCD27_CD3 | 19.4% |
| NKCD16_CD3neg | 19.4% |
| NK_CD3neg | 16.7% |
| naive_Bcells | 16.7% |
| Tconv memCCR5_total | 16.7% |
| Tconv mem_CD3 | 16.7% |
| Tconv memCXCR3_mem | 16.7% |
| CD8 RO TIGIT_total | 16.7% |
| Tconv memCD27_Tconv | 16.7% |
| Ki67_Bcells | 13.9% |
| CD8 RO CXCR3_CD3 | 13.9% |
| CD8 RO_total | 13.9% |
| CD4 Treg _CD3 | 13.9% |
| intB7_CD8RO | 13.9% |
| Tconv memCCR6_mem | 13.9% |
| Tconv naive_CD3 | 13.9% |
| Tconv memCXCR3_total | 13.9% |
| Ki67_CD8RO | 13.9% |
| Treg naive_CD4 | 11.1% |
| CD8 RO intB7_CD8 | 11.1% |
| CD8 RO intB7_CD3 | 11.1% |
| Bcells Ki67_CD3neg | 11.1% |
| CD8 RO CD56_CD8 | 11.1% |
| Tconv memCCR6_total | 11.1% |
| CD4neg_total | 11.1% |
| Tconv memCXCR3_Tconv | 11.1% |
| Tconv memKi67_Tconv | 11.1% |
| Tconv memTIGIT_CD3 | 11.1% |
| CD56_CD8RO | 8.3% |
| NK Ki67_NK | 8.3% |
| CD16mono_myeloid | 8.3% |
| NKCD16_NK | 8.3% |
| Treg memory_CD4 | 8.3% |
| CD8 RO Ki67_CD8 | 8.3% |
| Tconv memCCR5_Tconv | 8.3% |
| CD8 RO CCR5_CD8 | 8.3% |
| Tconv memKi67_CD3 | 8.3% |
| CXCR3_CD8RO | 8.3% |
| Treg naive_CD3 | 5.6% |
| NKCD16_total | 5.6% |
| CD8 RO CD27_CD3 | 5.6% |
| Tconv memCXCR3_CD3 | 5.6% |
| CD4 Treg_CD4 | 5.6% |
| CD3hi_CD4neg | 5.6% |
| CD8 RO PD1_total | 5.6% |
| Tconv memTIGIT_Tconv | 5.6% |
| Tconv memCCR4_total | 5.6% |
| CD8  RO Ki67_CD3 | 5.6% |
| CD8 RO CCR4_total | 5.6% |
| CD27IgD_Bcells | 5.6% |
| CD8 RO CXCR3_CD8 | 5.6% |
| NK_total | 2.8% |
| Tconv memCCR4_Tconv | 2.8% |
| Tconv memCCR5_CD3 | 2.8% |
| CD8 RA_CD8 | 2.8% |
| Tconv memCD56_CD3 | 2.8% |
| Tconv memCD56_Tconv | 2.8% |
| CCR4_CD8RO | 2.8% |
| Tconv memintB7_CD3 | 2.8% |
| Tconv memCCR6_CD3 | 2.8% |
| CD8pos_CD3 | 2.8% |
| CD8 RO CCR6_CD3 | 2.8% |
| NKCD56hi_NK | 2.8% |
| NK Ki67_total | 2.8% |
| Bcells Ki67_total | 2.8% |
| CD3hi_CD3 | 2.8% |
| CD4 Treg_total | 2.8% |
| CD8 RO CD56_total | 2.8% |
| NKCD56hi_nonTnonB | 2.8% |
| NKCD56hi_CD3neg | 2.8% |

**Total features selected by FDR (p < 0.1)_t40**: 122

#### FDR (p < 0.1)_t50

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Bcells CD27posIgDneg_total | 80.0% |
| Tconv memDR_CD3 | 71.4% |
| myeloid_CD3neg | 65.7% |
| Tconv memDR_Tconv | 62.9% |
| nonTnonB_CD3neg | 54.3% |
| Bcells_CD3neg | 54.3% |
| Bcells_total | 54.3% |
| CD8 RA naive_total | 51.4% |
| Tconv memDR_mem | 48.6% |
| CD14+16+mono_total | 45.7% |
| CD8 RA_total | 42.9% |
| CD8 RO CCR5_total | 42.9% |
| Bcells naive_total | 40.0% |
| CD14+16+mono_CD3neg | 40.0% |
| NKCD16_nonTnonB | 40.0% |
| Bcells naive_CD3neg | 37.1% |
| NK_nonTnonB | 37.1% |
| CD8 RA naive_CD3 | 37.1% |
| Tconv memDR_total | 34.3% |
| Tconv memCCR5_mem | 34.3% |
| CD14mono_CD3neg | 34.3% |
| CD8 RO DR_CD8 | 31.4% |
| CD8pos_total | 28.6% |
| CD27negIgDneg_Bcells | 28.6% |
| Bcells memory_total | 28.6% |
| DR_CD8RO | 25.7% |
| CD8 RO DR_CD3 | 25.7% |
| Bcells memory_CD3neg | 25.7% |
| myeloid_total | 25.7% |
| CD14mono_total | 22.9% |
| CD8 RO CCR5_CD3 | 20.0% |
| CD14+16+mono_myeloid | 20.0% |
| NK Ki67_nonTnonB | 20.0% |
| CD8 RO intB7_total | 20.0% |
| nonTnonB_total | 20.0% |
| CCR5_CD8RO | 20.0% |
| Tconv naive_total | 17.1% |
| CD8 RO CXCR3_total | 17.1% |
| Treg memory_CD3 | 17.1% |
| Tconv memCCR5_total | 14.3% |
| intB7_CD8RO | 14.3% |
| CD8 RA_CD3 | 14.3% |
| NKCD16_CD3neg | 14.3% |
| CD3pos_total | 14.3% |
| CD3neg_total | 14.3% |
| CD4 Tconv_total | 11.4% |
| Tconv naive_Tconv | 11.4% |
| naive_Bcells | 11.4% |
| Treg naive_total | 11.4% |
| Ki67_Bcells | 11.4% |
| Tconv memintB7_mem | 11.4% |
| Tconv mem_Tconv | 11.4% |
| Tconv memCCR6_mem | 11.4% |
| NK Ki67_CD3neg | 11.4% |
| Tconv memCXCR3_total | 8.6% |
| Tconv memCXCR3_mem | 8.6% |
| CD8 RA CCR7 naive_CD8 | 8.6% |
| Tconv memCD27_Tconv | 8.6% |
| CD8 RO intB7_CD3 | 8.6% |
| NK_CD3neg | 8.6% |
| CD8 RO CCR6_total | 8.6% |
| CD8 RO CD27_total | 8.6% |
| CD8 RO CXCR3_CD3 | 8.6% |
| Treg memory_CD4 | 8.6% |
| Tconv naive_CD3 | 5.7% |
| CD8 RO_total | 5.7% |
| Ki67_CD8RO | 5.7% |
| Tconv memintB7_total | 5.7% |
| Tconv memCXCR3_Tconv | 5.7% |
| CD8 RO CCR5_CD8 | 5.7% |
| CD8 RO Ki67_CD8 | 5.7% |
| Treg naive_CD4 | 5.7% |
| CD27IgD_Bcells | 5.7% |
| Tconv mem_CD3 | 5.7% |
| CD8 RO CD56_CD8 | 5.7% |
| Tconv memCD27_CD3 | 5.7% |
| CD8 RO CXCR3_CD8 | 5.7% |
| Tconv memCCR6_total | 2.9% |
| CD4 Treg_CD4 | 2.9% |
| Tconv memCCR5_Tconv | 2.9% |
| Tconv memintB7_CD3 | 2.9% |
| Tconv memCXCR3_CD3 | 2.9% |
| Tconv memCCR5_CD3 | 2.9% |
| Tconv memTIGIT_CD3 | 2.9% |
| CXCR3_CD8RO | 2.9% |
| Bcells Ki67_CD3neg | 2.9% |
| Tconv memCD56_Tconv | 2.9% |
| CD8pos_CD3 | 2.9% |
| CD4 Treg _CD3 | 2.9% |
| CD4neg_total | 2.9% |
| CD8 RO CD27_CD3 | 2.9% |
| Tconv memCCR4_total | 2.9% |
| Treg naive_CD3 | 2.9% |
| CD16mono_myeloid | 2.9% |
| CD8 RO CCR6_CD3 | 2.9% |
| NK Ki67_NK | 2.9% |
| NKCD16_NK | 2.9% |
| CD8 RO CCR4_total | 2.9% |
| CD8 RO TIGIT_total | 2.9% |
| CD8 RO intB7_CD8 | 2.9% |
| CD56_CD8RO | 2.9% |
| CD4 Treg_total | 2.9% |
| NKCD56hi_nonTnonB | 2.9% |

**Total features selected by FDR (p < 0.1)_t50**: 103

#### FDR (p < 0.1)_t60

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Bcells CD27posIgDneg_total | 80.6% |
| Tconv memDR_CD3 | 58.1% |
| myeloid_CD3neg | 54.8% |
| Tconv memDR_Tconv | 48.4% |
| Bcells_total | 45.2% |
| nonTnonB_CD3neg | 41.9% |
| Bcells_CD3neg | 38.7% |
| Bcells naive_CD3neg | 38.7% |
| Tconv memDR_mem | 38.7% |
| CD14+16+mono_total | 35.5% |
| CD14+16+mono_CD3neg | 32.3% |
| CD8 RO CCR5_total | 32.3% |
| CD8 RA naive_total | 29.0% |
| Tconv memCCR5_mem | 29.0% |
| NKCD16_nonTnonB | 25.8% |
| CD8 RA_total | 25.8% |
| CD8 RO DR_CD3 | 25.8% |
| Bcells naive_total | 25.8% |
| Bcells memory_total | 22.6% |
| CD8 RO DR_CD8 | 22.6% |
| CD8 RA naive_CD3 | 22.6% |
| CD14mono_CD3neg | 22.6% |
| NK_nonTnonB | 19.4% |
| Tconv memDR_total | 19.4% |
| CD27negIgDneg_Bcells | 19.4% |
| DR_CD8RO | 16.1% |
| CD8pos_total | 16.1% |
| NK Ki67_nonTnonB | 16.1% |
| Bcells memory_CD3neg | 16.1% |
| CD8 RO CCR5_CD3 | 12.9% |
| CD14mono_total | 12.9% |
| myeloid_total | 12.9% |
| nonTnonB_total | 12.9% |
| CD8 RO CXCR3_total | 12.9% |
| Tconv memCXCR3_mem | 9.7% |
| Tconv memCCR5_total | 9.7% |
| Tconv naive_Tconv | 9.7% |
| CD14+16+mono_myeloid | 9.7% |
| NKCD16_CD3neg | 9.7% |
| CD8 RA CCR7 naive_CD8 | 9.7% |
| CD3neg_total | 9.7% |
| CD8 RA_CD3 | 9.7% |
| CD8 RO intB7_total | 9.7% |
| Tconv memintB7_mem | 9.7% |
| CCR5_CD8RO | 9.7% |
| Tconv mem_Tconv | 9.7% |
| CD3pos_total | 9.7% |
| Ki67_Bcells | 9.7% |
| naive_Bcells | 6.5% |
| Treg naive_total | 6.5% |
| CD8 RO CXCR3_CD3 | 6.5% |
| CD8 RO CD27_total | 6.5% |
| Tconv naive_total | 6.5% |
| NK Ki67_CD3neg | 6.5% |
| Tconv memCCR6_mem | 6.5% |
| CD4 Treg_CD4 | 3.2% |
| Tconv memCXCR3_total | 3.2% |
| CD8 RO Ki67_CD8 | 3.2% |
| Treg memory_CD4 | 3.2% |
| CXCR3_CD8RO | 3.2% |
| Tconv memCCR5_CD3 | 3.2% |
| CD8 RO CCR5_CD8 | 3.2% |
| intB7_CD8RO | 3.2% |
| Bcells Ki67_CD3neg | 3.2% |
| Tconv memCCR5_Tconv | 3.2% |
| CD8 RO CCR6_CD3 | 3.2% |
| Tconv memintB7_total | 3.2% |
| CD4 Tconv_total | 3.2% |
| NK Ki67_NK | 3.2% |
| Treg naive_CD4 | 3.2% |
| CD16mono_myeloid | 3.2% |
| NKCD16_NK | 3.2% |
| CD8 RO intB7_CD8 | 3.2% |
| CD27IgD_Bcells | 3.2% |
| Ki67_CD8RO | 3.2% |
| NK_CD3neg | 3.2% |
| Tconv naive_CD3 | 3.2% |
| CD8 RO intB7_CD3 | 3.2% |

**Total features selected by FDR (p < 0.1)_t60**: 78

#### FDR (p < 0.1)_t70

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Bcells CD27posIgDneg_total | 64.3% |
| Tconv memDR_CD3 | 50.0% |
| Tconv memDR_Tconv | 46.4% |
| Bcells_total | 35.7% |
| Bcells naive_CD3neg | 32.1% |
| myeloid_CD3neg | 32.1% |
| Tconv memDR_mem | 32.1% |
| nonTnonB_CD3neg | 25.0% |
| Bcells_CD3neg | 25.0% |
| CD14+16+mono_total | 25.0% |
| Bcells naive_total | 21.4% |
| CD8 RO CCR5_total | 21.4% |
| CD8 RO DR_CD8 | 21.4% |
| CD14+16+mono_CD3neg | 21.4% |
| CD8 RA naive_total | 21.4% |
| Tconv memCCR5_mem | 17.9% |
| CD8 RO DR_CD3 | 17.9% |
| NKCD16_nonTnonB | 17.9% |
| CD8 RA naive_CD3 | 17.9% |
| CD8 RA_total | 17.9% |
| Tconv memDR_total | 14.3% |
| myeloid_total | 10.7% |
| CD27negIgDneg_Bcells | 10.7% |
| CD8 RO CCR5_CD3 | 10.7% |
| CD14mono_total | 10.7% |
| NK_nonTnonB | 10.7% |
| CD14+16+mono_myeloid | 7.1% |
| DR_CD8RO | 7.1% |
| Tconv memCCR5_total | 7.1% |
| NK Ki67_nonTnonB | 7.1% |
| CCR5_CD8RO | 7.1% |
| CD14mono_CD3neg | 7.1% |
| Bcells memory_total | 7.1% |
| CD8pos_total | 7.1% |
| NK Ki67_CD3neg | 7.1% |
| nonTnonB_total | 7.1% |
| CD8 RA_CD3 | 7.1% |
| Ki67_Bcells | 7.1% |
| CD8 RA CCR7 naive_CD8 | 3.6% |
| CD4 Treg_CD4 | 3.6% |
| Treg memory_CD4 | 3.6% |
| Tconv naive_Tconv | 3.6% |
| Tconv mem_Tconv | 3.6% |
| Tconv memintB7_mem | 3.6% |
| CD8 RO CXCR3_total | 3.6% |
| CD3pos_total | 3.6% |
| Tconv memintB7_total | 3.6% |
| CD8 RO CXCR3_CD3 | 3.6% |
| Treg naive_CD4 | 3.6% |
| CD8 RO intB7_total | 3.6% |
| Treg naive_total | 3.6% |
| Bcells memory_CD3neg | 3.6% |
| CD3neg_total | 3.6% |
| NK Ki67_NK | 3.6% |
| Tconv memCCR6_mem | 3.6% |
| NKCD16_NK | 3.6% |
| NKCD16_CD3neg | 3.6% |

**Total features selected by FDR (p < 0.1)_t70**: 57

#### FDR (p < 0.1)_t80

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Bcells CD27posIgDneg_total | 50.0% |
| Tconv memDR_CD3 | 36.4% |
| Tconv memDR_Tconv | 31.8% |
| Bcells_total | 27.3% |
| Bcells naive_CD3neg | 27.3% |
| nonTnonB_CD3neg | 22.7% |
| Bcells_CD3neg | 22.7% |
| Bcells naive_total | 18.2% |
| Tconv memDR_mem | 18.2% |
| Tconv memCCR5_mem | 18.2% |
| myeloid_CD3neg | 18.2% |
| CD8 RA naive_CD3 | 18.2% |
| CD8 RO DR_CD8 | 13.6% |
| CD8 RA naive_total | 13.6% |
| CD8 RO CCR5_total | 13.6% |
| CD8 RA_total | 13.6% |
| CD27negIgDneg_Bcells | 9.1% |
| CD8 RO DR_CD3 | 9.1% |
| NK Ki67_nonTnonB | 9.1% |
| CD14mono_total | 9.1% |
| CD8 RO CCR5_CD3 | 9.1% |
| nonTnonB_total | 9.1% |
| CD14+16+mono_total | 9.1% |
| Tconv memDR_total | 9.1% |
| myeloid_total | 9.1% |
| CD14mono_CD3neg | 4.5% |
| CD4 Treg_CD4 | 4.5% |
| Bcells memory_total | 4.5% |
| CD14+16+mono_CD3neg | 4.5% |
| DR_CD8RO | 4.5% |
| CD8 RO CXCR3_total | 4.5% |
| CD8pos_total | 4.5% |
| CD3neg_total | 4.5% |
| CD3pos_total | 4.5% |
| NK Ki67_CD3neg | 4.5% |
| Bcells memory_CD3neg | 4.5% |
| NK Ki67_NK | 4.5% |
| Ki67_Bcells | 4.5% |
| CCR5_CD8RO | 4.5% |
| NKCD16_nonTnonB | 4.5% |

**Total features selected by FDR (p < 0.1)_t80**: 40

#### LASSO_Lenient_t40

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Bcells CD27posIgDneg_total | 62.5% |
| CD8 RO DR_CD8 | 55.0% |
| CD14+16+mono_CD3neg | 35.0% |
| NKCD16_NK | 30.0% |
| DR_CD8RO | 27.5% |
| Tconv memCCR5_mem | 25.0% |
| Tconv memDR_total | 25.0% |
| CD8 RO DR_CD3 | 20.0% |
| CD27negIgDneg_Bcells | 20.0% |
| NK Ki67_NK | 17.5% |
| NK Ki67_nonTnonB | 15.0% |
| Treg naive_CD4 | 15.0% |
| Tconv memCXCR3_mem | 15.0% |
| NKCD56hi_total | 12.5% |
| CD8 RO CCR5_CD3 | 12.5% |
| Tconv memDR_mem | 12.5% |
| CD8 RA_CD3 | 10.0% |
| Tconv memTIGIT_mem | 7.5% |
| Tconv memCCR6_mem | 7.5% |
| CD14+16+mono_total | 7.5% |
| Ki67_Bcells | 7.5% |
| Treg memory_CD3 | 7.5% |
| CD8 RO CD56_CD8 | 7.5% |
| NKCD56hi_NK | 7.5% |
| Tconv memKi67_total | 5.0% |
| Tconv memDR_Tconv | 5.0% |
| Tconv memDR_CD3 | 5.0% |
| CD8 RO CD56_CD3 | 5.0% |
| CD3hi_total | 5.0% |
| CCR6_CD8RO | 5.0% |
| CD8 RO CD56_total | 5.0% |
| Treg memory_total | 5.0% |
| CD8 RO CCR5_total | 5.0% |
| naive_Bcells | 5.0% |
| myeloid_CD3neg | 5.0% |
| Bcells memory_total | 5.0% |
| CD8 RA naive_total | 5.0% |
| NKCD16_nonTnonB | 5.0% |
| CD56_CD8RO | 5.0% |
| NKCD16_total | 2.5% |
| Tconv memCD56_mem | 2.5% |
| CD16mono_CD3neg | 2.5% |
| Bcells naive_total | 2.5% |
| CD27IgD_Bcells | 2.5% |
| Tconv memCCR4_CD3 | 2.5% |
| CD3hi_CD4neg | 2.5% |
| CD8 RO intB7_total | 2.5% |
| Bcells_total | 2.5% |
| Tconv memCCR4_Tconv | 2.5% |
| CD8 RO CCR6_CD3 | 2.5% |
| CD8 RO intB7_CD3 | 2.5% |
| CD8 RO CXCR3_CD3 | 2.5% |
| Bcells Ki67_total | 2.5% |
| Tconv memCCR4_mem | 2.5% |
| CD8 RO Ki67_total | 2.5% |
| CD8 RA naive_CD3 | 2.5% |
| Tconv memintB7_mem | 2.5% |

**Total features selected by LASSO_Lenient_t40**: 57

#### LASSO_Lenient_t50

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Bcells CD27posIgDneg_total | 45.7% |
| CD14+16+mono_CD3neg | 31.4% |
| CD8 RO DR_CD8 | 31.4% |
| Tconv memCCR5_mem | 25.7% |
| NKCD16_NK | 22.9% |
| Tconv memDR_total | 17.1% |
| NK Ki67_nonTnonB | 14.3% |
| NK Ki67_NK | 14.3% |
| CD8 RO DR_CD3 | 11.4% |
| Tconv memCXCR3_mem | 11.4% |
| DR_CD8RO | 11.4% |
| NKCD56hi_total | 11.4% |
| CD8 RO CCR5_CD3 | 11.4% |
| Tconv memDR_mem | 8.6% |
| CD8 RO CD56_CD8 | 5.7% |
| CD8 RA_CD3 | 5.7% |
| Tconv memTIGIT_mem | 5.7% |
| Treg naive_CD4 | 5.7% |
| NKCD16_nonTnonB | 5.7% |
| CD27negIgDneg_Bcells | 5.7% |
| CD3hi_CD4neg | 2.9% |
| Treg memory_total | 2.9% |
| CD8 RO CXCR3_CD3 | 2.9% |
| Tconv memCCR4_mem | 2.9% |
| CD8 RO CCR6_CD3 | 2.9% |
| CD8 RO CD56_total | 2.9% |
| CD8 RO CCR5_total | 2.9% |
| CD8 RA naive_CD3 | 2.9% |
| Tconv memCCR6_mem | 2.9% |

**Total features selected by LASSO_Lenient_t50**: 29

#### LASSO_Lenient_t60

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Bcells CD27posIgDneg_total | 30.0% |
| CD8 RO DR_CD8 | 23.3% |
| CD14+16+mono_CD3neg | 16.7% |
| NKCD16_NK | 13.3% |
| Tconv memCCR5_mem | 13.3% |
| CD8 RO DR_CD3 | 10.0% |
| Tconv memDR_total | 10.0% |
| NK Ki67_nonTnonB | 10.0% |
| CD8 RO CCR5_CD3 | 10.0% |
| DR_CD8RO | 6.7% |
| NK Ki67_NK | 6.7% |
| CD8 RO CD56_CD8 | 6.7% |
| CD27negIgDneg_Bcells | 6.7% |
| Tconv memCXCR3_mem | 6.7% |
| CD8 RO CXCR3_CD3 | 3.3% |
| CD8 RA_CD3 | 3.3% |
| Tconv memTIGIT_mem | 3.3% |
| Treg naive_CD4 | 3.3% |
| CD8 RO CD56_total | 3.3% |
| NKCD56hi_total | 3.3% |
| CD8 RA naive_CD3 | 3.3% |
| Tconv memDR_mem | 3.3% |

**Total features selected by LASSO_Lenient_t60**: 22

#### LASSO_Lenient_t70

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Bcells CD27posIgDneg_total | 31.6% |
| CD14+16+mono_CD3neg | 26.3% |
| CD8 RO DR_CD8 | 15.8% |
| CD8 RO CCR5_CD3 | 10.5% |
| CD8 RO DR_CD3 | 10.5% |
| NKCD16_NK | 10.5% |
| Tconv memCCR5_mem | 5.3% |
| CD8 RO CD56_CD8 | 5.3% |
| NK Ki67_NK | 5.3% |
| DR_CD8RO | 5.3% |
| CD8 RO CXCR3_CD3 | 5.3% |
| CD8 RA_CD3 | 5.3% |
| Treg naive_CD4 | 5.3% |
| Tconv memTIGIT_mem | 5.3% |
| CD27negIgDneg_Bcells | 5.3% |
| CD8 RA naive_CD3 | 5.3% |
| Tconv memDR_mem | 5.3% |
| NK Ki67_nonTnonB | 5.3% |

**Total features selected by LASSO_Lenient_t70**: 18

#### LASSO_Lenient_t80

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Bcells CD27posIgDneg_total | 30.0% |
| CD14+16+mono_CD3neg | 30.0% |
| Tconv memCCR5_mem | 10.0% |
| CD8 RO CD56_CD8 | 10.0% |
| NK Ki67_NK | 10.0% |
| Treg naive_CD4 | 10.0% |
| Tconv memTIGIT_mem | 10.0% |
| NKCD16_NK | 10.0% |
| CD8 RO DR_CD8 | 10.0% |
| Tconv memDR_mem | 10.0% |

**Total features selected by LASSO_Lenient_t80**: 10

#### LASSO_RFE_t40

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Bcells CD27posIgDneg_total | 31.6% |
| CD14+16+mono_CD3neg | 21.1% |
| CD8 RO DR_CD8 | 18.4% |
| Tconv memCCR5_mem | 15.8% |
| Tconv memDR_total | 13.2% |
| CD8 RO DR_CD3 | 13.2% |
| Tconv memDR_mem | 10.5% |
| CD8 RO CCR5_CD3 | 10.5% |
| DR_CD8RO | 10.5% |
| NKCD16_NK | 7.9% |
| CD27negIgDneg_Bcells | 7.9% |
| NK Ki67_NK | 5.3% |
| NK Ki67_nonTnonB | 5.3% |
| naive_Bcells | 2.6% |
| NKCD16_total | 2.6% |
| CD8 RO CD56_CD8 | 2.6% |
| Tconv memCXCR3_mem | 2.6% |
| CD27IgD_Bcells | 2.6% |
| Bcells_total | 2.6% |
| CD8 RO CXCR3_CD3 | 2.6% |
| Treg naive_CD4 | 2.6% |
| Ki67_Bcells | 2.6% |
| NKCD56hi_NK | 2.6% |
| CD8 RO CCR5_total | 2.6% |
| NKCD56hi_total | 2.6% |
| CD8 RA naive_CD3 | 2.6% |

**Total features selected by LASSO_RFE_t40**: 26

#### LASSO_RFE_t50

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Bcells CD27posIgDneg_total | 37.5% |
| CD8 RO DR_CD8 | 18.8% |
| Tconv memCCR5_mem | 18.8% |
| CD8 RO CCR5_CD3 | 12.5% |
| CD14+16+mono_CD3neg | 12.5% |
| NKCD16_NK | 12.5% |
| DR_CD8RO | 6.2% |
| CD8 RO CD56_CD8 | 6.2% |
| NK Ki67_NK | 6.2% |
| CD8 RO DR_CD3 | 6.2% |
| Tconv memDR_total | 6.2% |

**Total features selected by LASSO_RFE_t50**: 11

#### LASSO_RFE_t60

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Bcells CD27posIgDneg_total | 37.5% |
| CD14+16+mono_CD3neg | 12.5% |
| Tconv memCCR5_mem | 12.5% |
| NKCD16_NK | 12.5% |
| CD8 RO DR_CD3 | 12.5% |
| CD8 RO CCR5_CD3 | 12.5% |
| CD8 RO DR_CD8 | 12.5% |

**Total features selected by LASSO_RFE_t60**: 7

#### LASSO_RFE_t70

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Bcells CD27posIgDneg_total | 50.0% |
| Tconv memCCR5_mem | 25.0% |
| CD14+16+mono_CD3neg | 25.0% |

**Total features selected by LASSO_RFE_t70**: 3

#### LASSO_RFE_t80

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Tconv memCCR5_mem | 100.0% |

**Total features selected by LASSO_RFE_t80**: 1

#### LASSO_Strict_t40

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Bcells CD27posIgDneg_total | 35.5% |
| CD8 RO DR_CD8 | 29.0% |
| Tconv memDR_total | 12.9% |
| CD14+16+mono_CD3neg | 12.9% |
| NKCD16_NK | 12.9% |
| CD8 RO DR_CD3 | 12.9% |
| DR_CD8RO | 9.7% |
| Tconv memCCR5_mem | 9.7% |
| CD8 RO CD56_CD8 | 6.5% |
| NK Ki67_NK | 6.5% |
| CD8 RA_CD3 | 6.5% |
| CD27negIgDneg_Bcells | 6.5% |
| CD8 RO CCR5_CD3 | 6.5% |
| naive_Bcells | 3.2% |
| CD14+16+mono_total | 3.2% |
| Treg naive_CD4 | 3.2% |
| CD8 RO CXCR3_CD3 | 3.2% |
| Tconv memTIGIT_mem | 3.2% |
| CD8 RO CD56_total | 3.2% |
| NKCD56hi_total | 3.2% |
| Tconv memDR_mem | 3.2% |

**Total features selected by LASSO_Strict_t40**: 21

#### LASSO_Strict_t50

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Bcells CD27posIgDneg_total | 27.3% |
| CD8 RO DR_CD8 | 22.7% |
| NKCD16_NK | 13.6% |
| DR_CD8RO | 9.1% |
| Tconv memDR_total | 9.1% |
| CD27negIgDneg_Bcells | 9.1% |
| CD14+16+mono_CD3neg | 9.1% |
| CD8 RO CCR5_CD3 | 9.1% |
| NK Ki67_NK | 4.5% |
| CD8 RA_CD3 | 4.5% |
| Tconv memCCR5_mem | 4.5% |
| CD8 RO CD56_CD8 | 4.5% |
| CD8 RO CXCR3_CD3 | 4.5% |
| CD8 RO CD56_total | 4.5% |
| Treg naive_CD4 | 4.5% |
| CD8 RO DR_CD3 | 4.5% |
| Tconv memDR_mem | 4.5% |

**Total features selected by LASSO_Strict_t50**: 17

#### LASSO_Strict_t60

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Bcells CD27posIgDneg_total | 33.3% |
| CD8 RO DR_CD8 | 16.7% |
| Tconv memCCR5_mem | 8.3% |
| NK Ki67_NK | 8.3% |
| Tconv memDR_total | 8.3% |
| Treg naive_CD4 | 8.3% |
| NKCD16_NK | 8.3% |
| CD14+16+mono_CD3neg | 8.3% |
| CD8 RO DR_CD3 | 8.3% |
| CD8 RO CCR5_CD3 | 8.3% |
| Tconv memDR_mem | 8.3% |

**Total features selected by LASSO_Strict_t60**: 11

#### LASSO_Strict_t70

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Tconv memCCR5_mem | 16.7% |
| NK Ki67_NK | 16.7% |
| Treg naive_CD4 | 16.7% |
| NKCD16_NK | 16.7% |
| CD8 RO DR_CD8 | 16.7% |
| Tconv memDR_mem | 16.7% |

**Total features selected by LASSO_Strict_t70**: 6

#### LASSO_Strict_t80

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Tconv memCCR5_mem | 50.0% |
| Treg naive_CD4 | 50.0% |

**Total features selected by LASSO_Strict_t80**: 2

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

**Total features selected by LogisticRegression_Permutation_Top10%_t80**: 16

#### Mutual Information (Top 10%)_t40

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Bcells CD27posIgDneg_total | 80.0% |
| myeloid_total | 72.5% |
| CD8 RO CCR5_total | 57.5% |
| Bcells memory_CD3neg | 55.0% |
| Tconv memDR_CD3 | 45.0% |
| CD3hi_CD3 | 42.5% |
| Tconv memDR_Tconv | 40.0% |
| CD14mono_total | 40.0% |
| CD8 RO CCR5_CD3 | 35.0% |
| CD27negIgDneg_Bcells | 32.5% |
| Tconv memDR_mem | 32.5% |
| CD8 RO DR_CD3 | 30.0% |
| Tconv memCXCR3_mem | 27.5% |
| CD14+16+mono_CD3neg | 25.0% |
| CD8 RO DR_CD8 | 25.0% |
| Bcells_total | 22.5% |
| Tconv memCCR5_mem | 22.5% |
| Tconv memDR_total | 22.5% |
| CD16mono_myeloid | 22.5% |
| CD8 RA_CD8 | 20.0% |
| nonTnonB_total | 17.5% |
| myeloid_CD3neg | 17.5% |
| Tconv memCCR4_mem | 17.5% |
| CD27IgD_Bcells | 15.0% |
| Tconv naive_CD3 | 15.0% |
| CCR5_CD8RO | 12.5% |
| Tconv memCD27_CD3 | 12.5% |
| Bcells memory_total | 12.5% |
| Treg naive_CD4 | 12.5% |
| Tconv mem_Tconv | 12.5% |
| CD8 RA naive_CD3 | 12.5% |
| CD8 RA naive_total | 10.0% |
| CD14+16+mono_total | 10.0% |
| CD8 RA_total | 10.0% |
| CD8 RO_CD8 | 10.0% |
| CD14mono_CD3neg | 10.0% |
| Bcells naive_CD3neg | 10.0% |
| CD8 RA_CD3 | 10.0% |
| CD8 RO CXCR3_CD3 | 10.0% |
| Tconv naive_Tconv | 7.5% |
| CD8pos_total | 7.5% |
| NKCD16_nonTnonB | 7.5% |
| CD8 RO CD27_CD3 | 7.5% |
| Bcells naive_total | 7.5% |
| nonTnonB_CD3neg | 7.5% |
| CD8 RO CCR4_total | 7.5% |
| CD8 RO PD1_total | 5.0% |
| NK_nonTnonB | 5.0% |
| Tconv memCD27_Tconv | 5.0% |
| Tconv memPD1_total | 5.0% |
| Tconv memCCR5_CD3 | 5.0% |
| Bcells_CD3neg | 5.0% |
| Tconv memTIGIT_CD3 | 5.0% |
| Tconv memKi67_total | 5.0% |
| CD8 RO CXCR3_total | 5.0% |
| DR_CD8RO | 2.5% |
| Tconv memCCR4_total | 2.5% |
| CD8 RO TIGIT_CD3 | 2.5% |
| CD8 RO_total | 2.5% |
| CD3pos_total | 2.5% |
| CD3neg_total | 2.5% |
| Tconv memPD1_Tconv | 2.5% |
| PD1_CD8RO | 2.5% |
| CD8 RO CD27_total | 2.5% |
| Tconv memTIGIT_mem | 2.5% |
| memory_Bcells | 2.5% |
| Tconv memCCR5_total | 2.5% |
| CD16mono_CD3neg | 2.5% |
| Tconv memintB7_total | 2.5% |
| Tconv memCCR5_Tconv | 2.5% |
| Tconv memCD56_Tconv | 2.5% |
| NK Ki67_NK | 2.5% |
| Treg naive_CD3 | 2.5% |
| Treg naive_total | 2.5% |
| NK Ki67_CD3neg | 2.5% |
| Tconv memCCR6_Tconv | 2.5% |
| Tconv memCCR4_CD3 | 2.5% |
| CD3hi_total | 2.5% |
| NK Ki67_nonTnonB | 2.5% |
| CD4neg_total | 2.5% |
| Tconv memCCR6_mem | 2.5% |
| CD14+16+mono_myeloid | 2.5% |
| Ki67_Bcells | 2.5% |
| Tconv naive_total | 2.5% |
| CD8 RO CXCR3_CD8 | 2.5% |
| CD8 RO PD1_CD3 | 2.5% |
| CD8 RO intB7_total | 2.5% |

**Total features selected by Mutual Information (Top 10%)_t40**: 87

#### Mutual Information (Top 10%)_t50

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Bcells CD27posIgDneg_total | 72.5% |
| myeloid_total | 55.0% |
| CD8 RO CCR5_total | 52.5% |
| Bcells memory_CD3neg | 42.5% |
| CD3hi_CD3 | 32.5% |
| Tconv memDR_mem | 30.0% |
| Tconv memDR_Tconv | 27.5% |
| Tconv memDR_CD3 | 27.5% |
| CD14mono_total | 27.5% |
| CD8 RO CCR5_CD3 | 22.5% |
| Tconv memCXCR3_mem | 22.5% |
| CD27negIgDneg_Bcells | 22.5% |
| CD8 RO DR_CD8 | 17.5% |
| CD8 RO DR_CD3 | 15.0% |
| CD14+16+mono_CD3neg | 12.5% |
| Tconv memDR_total | 12.5% |
| Bcells_total | 12.5% |
| Tconv memCCR5_mem | 12.5% |
| CD8 RA_CD8 | 12.5% |
| Tconv mem_Tconv | 7.5% |
| Tconv memCCR4_mem | 7.5% |
| CD8 RO CXCR3_CD3 | 7.5% |
| Treg naive_CD4 | 7.5% |
| nonTnonB_total | 7.5% |
| Tconv naive_CD3 | 7.5% |
| myeloid_CD3neg | 7.5% |
| CD16mono_myeloid | 5.0% |
| Tconv naive_Tconv | 5.0% |
| Tconv memCD27_Tconv | 5.0% |
| CD8 RA_total | 5.0% |
| CD8 RO_CD8 | 5.0% |
| Bcells naive_total | 5.0% |
| CD8 RA_CD3 | 5.0% |
| Tconv memCD27_CD3 | 5.0% |
| NK_nonTnonB | 5.0% |
| CD14mono_CD3neg | 5.0% |
| CD27IgD_Bcells | 5.0% |
| Tconv memCCR5_CD3 | 5.0% |
| CD8 RO CD27_CD3 | 5.0% |
| Tconv memCCR4_total | 2.5% |
| DR_CD8RO | 2.5% |
| CD8 RO CXCR3_total | 2.5% |
| CD8 RO CCR4_total | 2.5% |
| CD8 RO PD1_total | 2.5% |
| Tconv memTIGIT_CD3 | 2.5% |
| Tconv memPD1_Tconv | 2.5% |
| Bcells naive_CD3neg | 2.5% |
| Tconv memCCR5_total | 2.5% |
| memory_Bcells | 2.5% |
| NK Ki67_CD3neg | 2.5% |
| NK Ki67_NK | 2.5% |
| Tconv memPD1_total | 2.5% |
| Tconv memCD56_Tconv | 2.5% |
| CCR5_CD8RO | 2.5% |
| Bcells memory_total | 2.5% |
| Bcells_CD3neg | 2.5% |
| NK Ki67_nonTnonB | 2.5% |
| nonTnonB_CD3neg | 2.5% |
| CD4neg_total | 2.5% |
| Ki67_Bcells | 2.5% |
| Tconv memKi67_total | 2.5% |
| CD8 RO PD1_CD3 | 2.5% |
| CD8pos_total | 2.5% |
| CD8 RA naive_CD3 | 2.5% |
| CD8 RA naive_total | 2.5% |

**Total features selected by Mutual Information (Top 10%)_t50**: 65

#### Mutual Information (Top 10%)_t60

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Bcells CD27posIgDneg_total | 50.0% |
| myeloid_total | 30.0% |
| CD8 RO CCR5_total | 25.0% |
| Bcells memory_CD3neg | 22.5% |
| Tconv memDR_Tconv | 20.0% |
| Tconv memDR_CD3 | 20.0% |
| CD8 RO CCR5_CD3 | 20.0% |
| CD14mono_total | 17.5% |
| Tconv memDR_mem | 17.5% |
| CD8 RO DR_CD8 | 12.5% |
| CD8 RO DR_CD3 | 10.0% |
| CD3hi_CD3 | 10.0% |
| CD27negIgDneg_Bcells | 10.0% |
| Tconv memCXCR3_mem | 10.0% |
| CD8 RO CXCR3_CD3 | 7.5% |
| CD8 RA_CD8 | 7.5% |
| Tconv memCCR4_mem | 5.0% |
| Bcells_total | 5.0% |
| Tconv memCCR5_mem | 5.0% |
| CD16mono_myeloid | 5.0% |
| CD14+16+mono_CD3neg | 5.0% |
| Tconv memDR_total | 5.0% |
| Bcells naive_total | 2.5% |
| DR_CD8RO | 2.5% |
| Treg naive_CD4 | 2.5% |
| CD8 RO_CD8 | 2.5% |
| CD8 RO CD27_CD3 | 2.5% |
| CD14mono_CD3neg | 2.5% |
| CCR5_CD8RO | 2.5% |
| Tconv memCD56_Tconv | 2.5% |
| NK Ki67_NK | 2.5% |
| NK Ki67_CD3neg | 2.5% |
| NK Ki67_nonTnonB | 2.5% |
| Bcells_CD3neg | 2.5% |
| CD8 RA_CD3 | 2.5% |
| CD4neg_total | 2.5% |
| CD8 RA_total | 2.5% |
| myeloid_CD3neg | 2.5% |
| CD8pos_total | 2.5% |
| CD8 RA naive_CD3 | 2.5% |
| CD27IgD_Bcells | 2.5% |

**Total features selected by Mutual Information (Top 10%)_t60**: 41

#### Mutual Information (Top 10%)_t70

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Bcells CD27posIgDneg_total | 46.7% |
| myeloid_total | 26.7% |
| CD8 RO CCR5_total | 20.0% |
| Tconv memDR_CD3 | 16.7% |
| Tconv memDR_mem | 13.3% |
| Tconv memDR_Tconv | 13.3% |
| CD8 RA_CD8 | 6.7% |
| Bcells memory_CD3neg | 6.7% |
| CD8 RO DR_CD3 | 6.7% |
| CD8 RO CXCR3_CD3 | 6.7% |
| Tconv memCCR5_mem | 6.7% |
| CD3hi_CD3 | 6.7% |
| CD8 RO CCR5_CD3 | 6.7% |
| CD8 RO DR_CD8 | 6.7% |
| CD14mono_total | 6.7% |
| Tconv memDR_total | 6.7% |
| DR_CD8RO | 3.3% |
| Tconv memCCR4_mem | 3.3% |
| CD8 RO_CD8 | 3.3% |
| CCR5_CD8RO | 3.3% |
| Bcells_total | 3.3% |
| CD8 RO CD27_CD3 | 3.3% |
| CD14mono_CD3neg | 3.3% |
| CD8 RA_CD3 | 3.3% |
| CD14+16+mono_CD3neg | 3.3% |
| myeloid_CD3neg | 3.3% |
| Tconv memCXCR3_mem | 3.3% |

**Total features selected by Mutual Information (Top 10%)_t70**: 27

#### Mutual Information (Top 10%)_t80

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Bcells CD27posIgDneg_total | 28.6% |
| myeloid_total | 23.8% |
| CD8 RO CCR5_total | 19.0% |
| Tconv memDR_CD3 | 19.0% |
| Tconv memDR_Tconv | 19.0% |
| Tconv memCCR5_mem | 9.5% |
| Bcells memory_CD3neg | 9.5% |
| DR_CD8RO | 4.8% |
| CD8 RO CD27_CD3 | 4.8% |
| CD8 RO DR_CD8 | 4.8% |
| CD8 RO DR_CD3 | 4.8% |
| CCR5_CD8RO | 4.8% |
| Tconv memDR_total | 4.8% |
| Tconv memDR_mem | 4.8% |
| CD8 RO CCR5_CD3 | 4.8% |
| Tconv memCXCR3_mem | 4.8% |

**Total features selected by Mutual Information (Top 10%)_t80**: 16

#### NaiveBayes_Permutation_AboveMean_t40

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Bcells CD27posIgDneg_total | 87.5% |
| Ki67_Bcells | 75.0% |
| Tconv memCXCR3_total | 47.5% |
| Tconv memCD56_total | 47.5% |
| Bcells memory_CD3neg | 40.0% |
| CD8 RO CD56_total | 37.5% |
| CD3hi_total | 35.0% |
| CD8 RO intB7_total | 35.0% |
| CD8 RO CCR5_total | 32.5% |
| CD8 RA_total | 27.5% |
| CD8 RO CD56_CD3 | 27.5% |
| Tconv memDR_CD3 | 25.0% |
| Tconv memDR_Tconv | 22.5% |
| NK Ki67_nonTnonB | 22.5% |
| Bcells memory_total | 22.5% |
| Bcells naive_CD3neg | 20.0% |
| CD8 RA_CD3 | 20.0% |
| CD8 RO CCR5_CD3 | 20.0% |
| CD8 RA naive_total | 20.0% |
| NK Ki67_CD3neg | 20.0% |
| CD8 RO CXCR3_total | 17.5% |
| CD8 RO DR_CD8 | 17.5% |
| Bcells Ki67_total | 17.5% |
| CD8 RA naive_CD3 | 15.0% |
| CD8 RO intB7_CD3 | 15.0% |
| Tconv memCD56_mem | 15.0% |
| Tconv memCD56_Tconv | 15.0% |
| nonTnonB_CD3neg | 15.0% |
| Tconv memDR_mem | 15.0% |
| Tconv memCXCR3_CD3 | 12.5% |
| Tconv memCD56_CD3 | 12.5% |
| CD8 RO Ki67_total | 12.5% |
| Tconv memCXCR3_Tconv | 12.5% |
| CD8 RO CXCR3_CD3 | 12.5% |
| Treg memory_CD4 | 12.5% |
| Bcells_CD3neg | 12.5% |
| CD3hi_CD3 | 12.5% |
| Tconv memDR_total | 12.5% |
| NK Ki67_total | 12.5% |
| DR_CD8RO | 10.0% |
| CD8 RO DR_CD3 | 10.0% |
| Bcells Ki67_CD3neg | 10.0% |
| NKCD56hi_NK | 10.0% |
| CD8 RO CXCR3_CD8 | 10.0% |
| NK Ki67_NK | 10.0% |
| Tconv memCXCR3_mem | 10.0% |
| Tconv memCCR5_total | 10.0% |
| CD27IgD_Bcells | 7.5% |
| Tconv memCD27_Tconv | 7.5% |
| CD16mono_myeloid | 7.5% |
| NKCD16_NK | 7.5% |
| CD8pos_total | 7.5% |
| Tconv memCCR6_CD3 | 7.5% |
| CD8 RO CD56_CD8 | 7.5% |
| Bcells_total | 7.5% |
| Treg naive_total | 7.5% |
| CD14+16+mono_myeloid | 7.5% |
| Bcells naive_total | 7.5% |
| Treg naive_CD3 | 7.5% |
| CD8 ncytotox RO CCR4_CD3 | 7.5% |
| CD4neg_total | 7.5% |
| CXCR3_CD8RO | 7.5% |
| Treg naive_CD4 | 7.5% |
| CD27negIgDneg_Bcells | 7.5% |
| memory_Bcells | 7.5% |
| CD4 Treg_CD4 | 5.0% |
| NKCD56hi_total | 5.0% |
| CD8 RO TIGIT_total | 5.0% |
| CD8  RO Ki67_CD3 | 5.0% |
| CD14+16+mono_CD3neg | 5.0% |
| Tconv memTIGIT_mem | 5.0% |
| CD8 RO PD1_total | 5.0% |
| Tconv memCD27_mem | 5.0% |
| CD14+16+mono_total | 5.0% |
| CD8 RO PD1_CD3 | 5.0% |
| CD8 RO_total | 5.0% |
| NKCD16_total | 5.0% |
| CD8 RO DR_total | 5.0% |
| CD4neg_CD3 | 5.0% |
| Tconv memCCR6_Tconv | 5.0% |
| CD8 RO CD27_total | 5.0% |
| Tconv memCCR4_Tconv | 5.0% |
| NK_total | 5.0% |
| CD8 RO CCR6_total | 2.5% |
| CD4 Treg_total | 2.5% |
| CD8 RO CD27_CD3 | 2.5% |
| Bcells CD27negIgDneg_total | 2.5% |
| CD16+mono_total | 2.5% |
| CD4 Tconv_CD3 | 2.5% |
| Tconv memCCR5_CD3 | 2.5% |
| CD8 RO CCR4_total | 2.5% |
| CD8 RO PD1_CD8 | 2.5% |
| Tconv memCCR6_mem | 2.5% |
| CD8 RA_CD8 | 2.5% |
| CD8 RO CCR6_CD8 | 2.5% |
| CD8 RO_CD8 | 2.5% |
| Tconv mem_CD3 | 2.5% |
| Tconv memCCR4_CD3 | 2.5% |
| Tconv memCCR5_Tconv | 2.5% |
| Treg memory_CD3 | 2.5% |
| CD4 Treg _CD3 | 2.5% |
| Tconv memTIGIT_CD3 | 2.5% |
| Tconv memPD1_Tconv | 2.5% |
| Tconv memKi67_total | 2.5% |
| CCR6_CD8RO | 2.5% |
| Tconv memTIGIT_Tconv | 2.5% |
| Tconv memCD27_CD3 | 2.5% |
| CD56_CD8RO | 2.5% |
| CD27_CD8RO | 2.5% |
| NK_CD3neg | 2.5% |
| NKCD16_CD3neg | 2.5% |
| Tconv naive_CD3 | 2.5% |
| Tconv memintB7_Tconv | 2.5% |
| CD8 RO TIGIT_CD3 | 2.5% |
| Tconv memCCR5_mem | 2.5% |
| CD8 RO TIGIT_CD8 | 2.5% |
| CD8 RA CCR7 naive_CD8 | 2.5% |
| CD8 RO CCR5_CD8 | 2.5% |
| CCR5_CD8RO | 2.5% |
| CD8pos_CD3 | 2.5% |
| Tconv memPD1_mem | 2.5% |
| CD14mono_myeloid | 2.5% |
| NK_nonTnonB | 2.5% |
| Tconv memKi67_mem | 2.5% |
| CD3hi_CD4neg | 2.5% |
| Tconv memKi67_CD3 | 2.5% |
| Tconv memPD1_CD3 | 2.5% |
| CD8 RO CCR6_CD3 | 2.5% |
| NKCD16_nonTnonB | 2.5% |
| Tconv naive_total | 2.5% |
| CD4 Tconv_total | 2.5% |
| Tconv memCCR6_total | 2.5% |
| Tconv memintB7_CD3 | 2.5% |
| intB7_CD8RO | 2.5% |
| CD8 RO intB7_CD8 | 2.5% |
| myeloid_CD3neg | 2.5% |
| CD14mono_CD3neg | 2.5% |
| CD16mono_CD3neg | 2.5% |
| NKCD56hi_nonTnonB | 2.5% |

**Total features selected by NaiveBayes_Permutation_AboveMean_t40**: 139

#### NaiveBayes_Permutation_AboveMean_t50

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Bcells CD27posIgDneg_total | 85.0% |
| Ki67_Bcells | 60.0% |
| Tconv memCD56_total | 35.0% |
| Tconv memCXCR3_total | 25.0% |
| CD3hi_total | 22.5% |
| CD8 RA_total | 22.5% |
| CD8 RO CD56_total | 17.5% |
| Bcells memory_CD3neg | 15.0% |
| CD8 RO CCR5_total | 15.0% |
| CD8 RO intB7_total | 15.0% |
| CD8 RO CXCR3_total | 12.5% |
| Bcells naive_CD3neg | 12.5% |
| CD8 RO CCR5_CD3 | 12.5% |
| CD8 RA_CD3 | 10.0% |
| Tconv memCD56_mem | 10.0% |
| CD8 RO CD56_CD3 | 10.0% |
| Bcells Ki67_total | 10.0% |
| Tconv memDR_CD3 | 10.0% |
| CD8 RA naive_total | 7.5% |
| Bcells Ki67_CD3neg | 7.5% |
| Tconv memCD56_Tconv | 7.5% |
| CD8 RO Ki67_total | 7.5% |
| nonTnonB_CD3neg | 7.5% |
| Bcells_CD3neg | 7.5% |
| Tconv memDR_mem | 7.5% |
| Bcells memory_total | 7.5% |
| CD27IgD_Bcells | 5.0% |
| Tconv memDR_Tconv | 5.0% |
| Tconv memCD56_CD3 | 5.0% |
| DR_CD8RO | 5.0% |
| CD8 RO DR_CD8 | 5.0% |
| Bcells_total | 5.0% |
| CD14+16+mono_CD3neg | 5.0% |
| Tconv memCXCR3_CD3 | 5.0% |
| CD8 RA naive_CD3 | 5.0% |
| CD8 RO DR_CD3 | 5.0% |
| Tconv memCXCR3_mem | 5.0% |
| CD8 RO CXCR3_CD3 | 5.0% |
| CD27negIgDneg_Bcells | 5.0% |
| CD8 RO intB7_CD3 | 5.0% |
| CD14+16+mono_myeloid | 2.5% |
| Treg memory_CD4 | 2.5% |
| CD14+16+mono_total | 2.5% |
| CD8 RO CD27_CD3 | 2.5% |
| Bcells naive_total | 2.5% |
| CD8 RO CXCR3_CD8 | 2.5% |
| CXCR3_CD8RO | 2.5% |
| CD4 Treg_CD4 | 2.5% |
| CD8 RO CCR6_total | 2.5% |
| Tconv memDR_total | 2.5% |
| CD8pos_total | 2.5% |
| CD4neg_total | 2.5% |
| CD8 RO DR_total | 2.5% |
| CD8 RO PD1_total | 2.5% |
| CD16+mono_total | 2.5% |
| Tconv memCCR5_CD3 | 2.5% |
| CD8 RO PD1_CD8 | 2.5% |
| Tconv memCCR6_mem | 2.5% |
| CD8 RA_CD8 | 2.5% |
| CD8 RO_CD8 | 2.5% |
| Tconv memCCR5_Tconv | 2.5% |
| CD3hi_CD3 | 2.5% |
| NK_total | 2.5% |
| NKCD16_CD3neg | 2.5% |
| NK_CD3neg | 2.5% |
| NKCD16_total | 2.5% |
| Tconv memCCR6_CD3 | 2.5% |
| Tconv memCCR5_mem | 2.5% |
| CD8 RO CCR5_CD8 | 2.5% |
| CCR5_CD8RO | 2.5% |
| Tconv memTIGIT_mem | 2.5% |
| NK_nonTnonB | 2.5% |
| NK Ki67_nonTnonB | 2.5% |
| NKCD16_nonTnonB | 2.5% |
| Tconv memCCR6_total | 2.5% |
| Tconv memCXCR3_Tconv | 2.5% |
| myeloid_CD3neg | 2.5% |

**Total features selected by NaiveBayes_Permutation_AboveMean_t50**: 77

#### NaiveBayes_Permutation_AboveMean_t60

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Bcells CD27posIgDneg_total | 68.4% |
| Ki67_Bcells | 36.8% |
| Tconv memCD56_total | 21.1% |
| CD8 RO CD56_total | 18.4% |
| CD3hi_total | 10.5% |
| CD8 RA_total | 10.5% |
| CD8 RO CCR5_total | 7.9% |
| CD8 RO CXCR3_total | 7.9% |
| Tconv memCD56_Tconv | 5.3% |
| Tconv memCXCR3_total | 5.3% |
| Bcells memory_total | 5.3% |
| CD8 RO CCR5_CD3 | 5.3% |
| Bcells memory_CD3neg | 5.3% |
| CD8 RA naive_total | 5.3% |
| CD8 RO intB7_total | 5.3% |
| CD8 RO CD56_CD3 | 5.3% |
| Bcells naive_CD3neg | 5.3% |
| CD8 RO DR_CD3 | 5.3% |
| CD27IgD_Bcells | 2.6% |
| Tconv memCD56_mem | 2.6% |
| Tconv memCD56_CD3 | 2.6% |
| Bcells Ki67_total | 2.6% |
| Tconv memDR_CD3 | 2.6% |
| CD8 RO intB7_CD3 | 2.6% |
| Tconv memDR_Tconv | 2.6% |
| Tconv memCXCR3_CD3 | 2.6% |
| DR_CD8RO | 2.6% |
| CD8 RO DR_CD8 | 2.6% |
| Tconv memCXCR3_mem | 2.6% |
| CD8 RO Ki67_total | 2.6% |
| CD8pos_total | 2.6% |
| CD8 RO CXCR3_CD3 | 2.6% |
| CD8 RA_CD3 | 2.6% |
| CD27negIgDneg_Bcells | 2.6% |
| Bcells_CD3neg | 2.6% |
| nonTnonB_CD3neg | 2.6% |
| Tconv memCCR5_mem | 2.6% |
| CCR5_CD8RO | 2.6% |
| NK_nonTnonB | 2.6% |
| NKCD16_nonTnonB | 2.6% |
| Tconv memCCR6_total | 2.6% |
| myeloid_CD3neg | 2.6% |

**Total features selected by NaiveBayes_Permutation_AboveMean_t60**: 42

#### NaiveBayes_Permutation_AboveMean_t70

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Bcells CD27posIgDneg_total | 62.1% |
| Ki67_Bcells | 31.0% |
| Tconv memCD56_total | 13.8% |
| Bcells memory_CD3neg | 6.9% |
| Tconv memCD56_mem | 3.4% |
| Tconv memCD56_CD3 | 3.4% |
| CD8 RO intB7_CD3 | 3.4% |
| CD8 RO intB7_total | 3.4% |
| Tconv memDR_CD3 | 3.4% |
| Tconv memCD56_Tconv | 3.4% |
| Bcells naive_CD3neg | 3.4% |
| CD8 RA_total | 3.4% |
| CD8 RO CD56_total | 3.4% |
| CD3hi_total | 3.4% |
| CD8 RO CD56_CD3 | 3.4% |
| Bcells_CD3neg | 3.4% |
| nonTnonB_CD3neg | 3.4% |
| myeloid_CD3neg | 3.4% |

**Total features selected by NaiveBayes_Permutation_AboveMean_t70**: 18

#### NaiveBayes_Permutation_AboveMean_t80

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Bcells CD27posIgDneg_total | 45.5% |
| Ki67_Bcells | 36.4% |
| Tconv memCD56_total | 18.2% |
| Tconv memCD56_CD3 | 9.1% |
| Tconv memCD56_mem | 9.1% |
| Tconv memCD56_Tconv | 9.1% |
| Bcells memory_CD3neg | 9.1% |

**Total features selected by NaiveBayes_Permutation_AboveMean_t80**: 7

#### NaiveBayes_Permutation_Top10%_t40

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Tconv memCXCR3_total | 97.5% |
| Tconv memCCR6_total | 97.5% |
| Tconv memCD56_total | 97.5% |
| Tconv memKi67_total | 92.5% |
| Tconv memintB7_total | 90.0% |
| Tconv naive_total | 90.0% |
| Tconv memCD27_total | 87.5% |
| Tconv memDR_total | 85.0% |
| Tconv memPD1_total | 85.0% |
| Bcells CD27posIgDneg_total | 80.0% |
| Tconv memCCR5_total | 72.5% |
| Ki67_Bcells | 65.0% |
| CD4 Treg_total | 60.0% |
| CD4 Tconv mem_total | 52.5% |
| Tconv memTIGIT_total | 47.5% |
| Tconv memCCR4_total | 47.5% |
| CD3pos_total | 32.5% |
| CD3hi_total | 22.5% |
| CD8 RO CD56_total | 20.0% |
| CD8 RA_total | 20.0% |
| CD8 RO CCR5_total | 17.5% |
| CD4 Tconv_total | 15.0% |
| CD8 RO intB7_total | 15.0% |
| Bcells naive_CD3neg | 12.5% |
| Tconv memDR_CD3 | 10.0% |
| Tconv memDR_Tconv | 10.0% |
| Bcells Ki67_total | 7.5% |
| CD8 RA naive_total | 7.5% |
| CD8 RO CXCR3_total | 7.5% |
| CD8 RO CD56_CD3 | 7.5% |
| CD8 RA_CD3 | 7.5% |
| CD8 RO CCR5_CD3 | 7.5% |
| Tconv memCXCR3_CD3 | 5.0% |
| Tconv memCD56_CD3 | 5.0% |
| Tconv memCD56_mem | 5.0% |
| CD8 RO intB7_CD3 | 5.0% |
| nonTnonB_CD3neg | 5.0% |
| Tconv memCD56_Tconv | 5.0% |
| CD8 RO Ki67_total | 5.0% |
| Bcells memory_total | 5.0% |
| CD8 RO DR_CD8 | 5.0% |
| CD27IgD_Bcells | 2.5% |
| CD8 RO CD27_CD3 | 2.5% |
| Tconv memCD27_mem | 2.5% |
| NK Ki67_CD3neg | 2.5% |
| NK Ki67_nonTnonB | 2.5% |
| CD8 RA naive_CD3 | 2.5% |
| Tconv memCXCR3_mem | 2.5% |
| CD3hi_CD3 | 2.5% |
| Bcells Ki67_CD3neg | 2.5% |
| CD8 RO DR_CD3 | 2.5% |
| DR_CD8RO | 2.5% |
| CD8  RO Ki67_CD3 | 2.5% |
| Bcells_CD3neg | 2.5% |
| Bcells memory_CD3neg | 2.5% |
| myeloid_CD3neg | 2.5% |
| memory_Bcells | 2.5% |
| CD4neg_CD3 | 2.5% |

**Total features selected by NaiveBayes_Permutation_Top10%_t40**: 58

#### NaiveBayes_Permutation_Top10%_t50

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Tconv memCD56_total | 90.0% |
| Tconv memKi67_total | 85.0% |
| Tconv memCXCR3_total | 85.0% |
| Tconv memCD27_total | 75.0% |
| Tconv memCCR6_total | 72.5% |
| Bcells CD27posIgDneg_total | 72.5% |
| Tconv memPD1_total | 70.0% |
| Tconv naive_total | 65.0% |
| Tconv memDR_total | 62.5% |
| Tconv memintB7_total | 55.0% |
| Tconv memCCR5_total | 55.0% |
| Ki67_Bcells | 47.5% |
| CD4 Tconv mem_total | 35.0% |
| CD4 Treg_total | 35.0% |
| Tconv memCCR4_total | 25.0% |
| Tconv memTIGIT_total | 25.0% |
| CD3pos_total | 15.0% |
| CD8 RO CD56_total | 12.5% |
| CD8 RA_total | 12.5% |
| CD3hi_total | 10.0% |
| Bcells naive_CD3neg | 7.5% |
| CD8 RO intB7_total | 7.5% |
| CD8 RO CXCR3_total | 7.5% |
| CD8 RA_CD3 | 5.0% |
| CD8 RO CCR5_total | 5.0% |
| Tconv memDR_Tconv | 5.0% |
| Tconv memDR_CD3 | 5.0% |
| Tconv memCD56_CD3 | 2.5% |
| CD4 Tconv_total | 2.5% |
| CD27IgD_Bcells | 2.5% |
| Tconv memCD56_mem | 2.5% |
| CD8 RO intB7_CD3 | 2.5% |
| CD8 RO CD27_CD3 | 2.5% |
| Tconv memCD56_Tconv | 2.5% |
| Bcells Ki67_total | 2.5% |
| CD8 RA naive_CD3 | 2.5% |
| Bcells Ki67_CD3neg | 2.5% |
| CD8 RA naive_total | 2.5% |
| CD8 RO CCR5_CD3 | 2.5% |

**Total features selected by NaiveBayes_Permutation_Top10%_t50**: 39

#### NaiveBayes_Permutation_Top10%_t60

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Tconv memCD56_total | 80.0% |
| Tconv memCXCR3_total | 72.5% |
| Tconv memCCR6_total | 55.0% |
| Bcells CD27posIgDneg_total | 55.0% |
| Tconv naive_total | 50.0% |
| Tconv memKi67_total | 47.5% |
| Tconv memCD27_total | 42.5% |
| Tconv memPD1_total | 40.0% |
| Tconv memCCR5_total | 40.0% |
| Tconv memintB7_total | 40.0% |
| Tconv memDR_total | 40.0% |
| Ki67_Bcells | 32.5% |
| Tconv memTIGIT_total | 20.0% |
| CD4 Treg_total | 17.5% |
| CD4 Tconv mem_total | 12.5% |
| Tconv memCCR4_total | 10.0% |
| CD8 RO CD56_total | 5.0% |
| CD8 RO CXCR3_total | 5.0% |
| Bcells naive_CD3neg | 5.0% |
| Tconv memCD56_Tconv | 2.5% |
| Tconv memCD56_mem | 2.5% |
| Tconv memCD56_CD3 | 2.5% |
| CD8 RO intB7_total | 2.5% |
| CD8 RO intB7_CD3 | 2.5% |
| CD27IgD_Bcells | 2.5% |
| CD8 RA naive_total | 2.5% |
| CD3pos_total | 2.5% |
| Tconv memDR_CD3 | 2.5% |
| CD3hi_total | 2.5% |
| CD8 RO CCR5_CD3 | 2.5% |

**Total features selected by NaiveBayes_Permutation_Top10%_t60**: 30

#### NaiveBayes_Permutation_Top10%_t70

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Tconv memCD56_total | 73.0% |
| Tconv memCXCR3_total | 45.9% |
| Tconv memKi67_total | 37.8% |
| Tconv memCCR6_total | 35.1% |
| Tconv naive_total | 32.4% |
| Bcells CD27posIgDneg_total | 29.7% |
| Tconv memDR_total | 29.7% |
| Tconv memintB7_total | 27.0% |
| Tconv memPD1_total | 24.3% |
| Tconv memCD27_total | 21.6% |
| Ki67_Bcells | 16.2% |
| Tconv memCCR5_total | 10.8% |
| CD4 Treg_total | 10.8% |
| Tconv memTIGIT_total | 8.1% |
| CD4 Tconv mem_total | 5.4% |
| Tconv memCD56_Tconv | 2.7% |
| Tconv memCD56_mem | 2.7% |
| CD3pos_total | 2.7% |
| Tconv memCCR4_total | 2.7% |

**Total features selected by NaiveBayes_Permutation_Top10%_t70**: 19

#### NaiveBayes_Permutation_Top10%_t80

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Tconv memCD56_total | 70.8% |
| Tconv memCXCR3_total | 25.0% |
| Tconv memKi67_total | 25.0% |
| Tconv memCCR6_total | 25.0% |
| Tconv memintB7_total | 20.8% |
| Ki67_Bcells | 12.5% |
| Bcells CD27posIgDneg_total | 12.5% |
| Tconv memCD27_total | 12.5% |
| Tconv memDR_total | 12.5% |
| Tconv naive_total | 12.5% |
| Tconv memPD1_total | 8.3% |
| Tconv memCCR5_total | 8.3% |
| CD4 Treg_total | 4.2% |
| CD3pos_total | 4.2% |

**Total features selected by NaiveBayes_Permutation_Top10%_t80**: 14

#### RFE (RandomForest)_t40

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| naive_Bcells | 95.0% |
| CD27negIgDneg_Bcells | 95.0% |
| CD16mono_myeloid | 92.5% |
| CCR5_CD8RO | 90.0% |
| Tconv memDR_mem | 90.0% |
| myeloid_CD3neg | 90.0% |
| NK Ki67_nonTnonB | 90.0% |
| Ki67_Bcells | 90.0% |
| memory_Bcells | 90.0% |
| CD14+16+mono_myeloid | 90.0% |
| CD14+16+mono_CD3neg | 87.5% |
| CD8 RO DR_CD8 | 87.5% |
| DR_CD8RO | 87.5% |
| NK Ki67_NK | 87.5% |
| nonTnonB_CD3neg | 87.5% |
| CD27IgD_Bcells | 87.5% |
| Bcells naive_CD3neg | 87.5% |
| Tconv memDR_Tconv | 87.5% |
| CD14mono_CD3neg | 85.0% |
| Tconv memDR_CD3 | 85.0% |
| NKCD16_NK | 85.0% |
| NKCD56hi_NK | 85.0% |
| Bcells memory_CD3neg | 85.0% |
| Bcells_CD3neg | 85.0% |
| NK Ki67_CD3neg | 82.5% |
| CD14mono_myeloid | 80.0% |
| NKCD16_nonTnonB | 80.0% |
| NK_nonTnonB | 77.5% |
| Bcells Ki67_CD3neg | 75.0% |
| CD56_CD8RO | 75.0% |
| PD1_CD8RO | 75.0% |
| CD16mono_CD3neg | 75.0% |
| Tconv memCCR5_mem | 75.0% |
| NKCD56hi_CD3neg | 75.0% |
| NKCD16_CD3neg | 72.5% |
| NKCD56hi_nonTnonB | 72.5% |
| CD8 RO CD56_CD8 | 72.5% |
| NK_CD3neg | 72.5% |
| intB7_CD8RO | 72.5% |
| CD8 RO DR_CD3 | 72.5% |
| CD8 RO CCR5_CD3 | 72.5% |
| Bcells CD27posIgDneg_total | 70.0% |
| CD8 RO PD1_CD8 | 70.0% |
| CXCR3_CD8RO | 70.0% |
| TIGIT_CD8RO | 67.5% |
| CD8 RA CCR7 naive_CD8 | 67.5% |
| Tconv naive_Tconv | 65.0% |
| Ki67_CD8RO | 65.0% |
| CCR4_CD8RO | 62.5% |
| Tconv memCCR6_mem | 62.5% |
| CD3hi_CD4neg | 60.0% |
| Tconv memTIGIT_mem | 60.0% |
| CD8 RO_CD8 | 60.0% |
| CD8 RO CCR5_CD8 | 60.0% |
| CD8 RO intB7_CD8 | 60.0% |
| CD27_CD8RO | 60.0% |
| CD8 RO TIGIT_CD8 | 60.0% |
| CD8 RO Ki67_CD8 | 60.0% |
| CD8 ncytotox RO CCR4_CD8ntox | 57.5% |
| CD8 RO CCR6_CD8 | 57.5% |
| Tconv memCXCR3_mem | 57.5% |
| CCR6_CD8RO | 55.0% |
| CD8 RO CXCR3_CD8 | 55.0% |
| Tconv mem_Tconv | 55.0% |
| Tconv memCD27_Tconv | 52.5% |
| CD8 RA naive_CD3 | 52.5% |
| CD8 RO CD27_CD8 | 52.5% |
| CD8 RA_CD8 | 50.0% |
| Treg naive_CD4 | 50.0% |
| CD8 RO CCR5_total | 47.5% |
| Tconv memCD27_mem | 47.5% |
| Tconv memintB7_mem | 47.5% |
| Tconv memCXCR3_Tconv | 45.0% |
| Tconv memPD1_Tconv | 45.0% |
| Tconv memKi67_mem | 42.5% |
| Tconv memCCR5_Tconv | 42.5% |
| Tconv memCD56_mem | 42.5% |
| Tconv memintB7_Tconv | 42.5% |
| CD8 RO CXCR3_CD3 | 40.0% |
| Tconv memCD56_Tconv | 40.0% |
| Tconv memCCR4_mem | 40.0% |
| CD3hi_CD3 | 37.5% |
| Tconv memCCR6_Tconv | 37.5% |
| CD8 RA_CD3 | 37.5% |
| Tconv memPD1_mem | 37.5% |
| Tconv memCCR4_Tconv | 35.0% |
| Treg memory_CD4 | 35.0% |
| Tconv memKi67_Tconv | 35.0% |
| CD8pos_CD3 | 35.0% |
| Tconv memTIGIT_Tconv | 35.0% |
| CD8 RO CD27_CD3 | 35.0% |
| CD4 Treg_CD4 | 35.0% |
| CD8 RO intB7_CD3 | 32.5% |
| CD8 RO TIGIT_CD3 | 32.5% |
| CD14+16+mono_total | 32.5% |
| CD8 RO CD56_CD3 | 32.5% |
| Tconv naive_CD3 | 30.0% |
| Bcells naive_total | 30.0% |
| Bcells_total | 30.0% |
| NK Ki67_total | 25.0% |
| CD8 RO CCR6_CD3 | 25.0% |
| Tconv memDR_total | 25.0% |
| CD8 RO_CD3 | 25.0% |
| Tconv memCD27_CD3 | 25.0% |
| Treg memory_CD3 | 22.5% |
| CD8  RO Ki67_CD3 | 22.5% |
| CD14mono_total | 22.5% |
| CD8 RO PD1_CD3 | 22.5% |
| CD4neg_CD3 | 20.0% |
| myeloid_total | 20.0% |
| CD8 ncytotox RO CCR4_CD3 | 20.0% |
| nonTnonB_total | 20.0% |
| CD8pos_total | 20.0% |
| Tconv mem_CD3 | 20.0% |
| CD4 Treg _CD3 | 17.5% |
| Bcells memory_total | 15.0% |
| CD8 RA naive_total | 15.0% |
| NK_total | 12.5% |
| Treg naive_CD3 | 12.5% |
| Tconv memCCR5_CD3 | 12.5% |
| Tconv memKi67_CD3 | 12.5% |
| CD8 RA_total | 12.5% |
| Tconv memCXCR3_CD3 | 12.5% |
| NKCD16_total | 10.0% |
| CD4 Tconv_CD3 | 10.0% |
| Tconv memTIGIT_CD3 | 10.0% |
| Bcells CD27negIgDneg_total | 10.0% |
| Tconv memintB7_CD3 | 10.0% |
| Tconv memPD1_CD3 | 10.0% |
| CD8 RO CXCR3_total | 10.0% |
| CD8 RO_total | 7.5% |
| Tconv naive_total | 7.5% |
| Tconv memCD56_CD3 | 7.5% |
| CD3neg_total | 7.5% |
| Tconv memCCR6_CD3 | 7.5% |
| Bcells Ki67_total | 7.5% |
| Tconv memCCR4_CD3 | 7.5% |
| CD4neg_total | 5.0% |
| CD8 RO CD27_total | 5.0% |
| CD8 RO intB7_total | 5.0% |
| CD8 RO TIGIT_total | 5.0% |
| CD3hi_total | 5.0% |
| CD8 RO DR_total | 2.5% |
| CD8 RO CD56_total | 2.5% |
| CD3pos_total | 2.5% |
| CD8 RO CCR6_total | 2.5% |
| Treg naive_total | 2.5% |
| NKCD56hi_total | 2.5% |
| Treg memory_total | 2.5% |
| CD8 RO PD1_total | 2.5% |
| CD16+mono_total | 2.5% |

**Total features selected by RFE (RandomForest)_t40**: 151

#### RFE (RandomForest)_t50

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD14+16+mono_CD3neg | 80.0% |
| CD27negIgDneg_Bcells | 80.0% |
| Bcells naive_CD3neg | 77.5% |
| CCR5_CD8RO | 77.5% |
| Tconv memDR_Tconv | 77.5% |
| nonTnonB_CD3neg | 75.0% |
| DR_CD8RO | 75.0% |
| naive_Bcells | 75.0% |
| CD14+16+mono_myeloid | 72.5% |
| NK Ki67_NK | 70.0% |
| myeloid_CD3neg | 70.0% |
| Tconv memDR_mem | 70.0% |
| NK_nonTnonB | 70.0% |
| Tconv memDR_CD3 | 70.0% |
| NKCD16_NK | 70.0% |
| memory_Bcells | 67.5% |
| CD8 RO DR_CD8 | 67.5% |
| Bcells memory_CD3neg | 67.5% |
| CD27IgD_Bcells | 67.5% |
| NK Ki67_CD3neg | 67.5% |
| Bcells_CD3neg | 67.5% |
| NKCD56hi_NK | 65.0% |
| NK Ki67_nonTnonB | 62.5% |
| NKCD16_nonTnonB | 62.5% |
| Tconv memCCR5_mem | 62.5% |
| CD16mono_myeloid | 60.0% |
| CD14mono_myeloid | 60.0% |
| Ki67_Bcells | 55.0% |
| CD14mono_CD3neg | 55.0% |
| NKCD16_CD3neg | 55.0% |
| CD8 RO CCR5_CD3 | 52.5% |
| NKCD56hi_CD3neg | 52.5% |
| NKCD56hi_nonTnonB | 50.0% |
| CD56_CD8RO | 50.0% |
| CD8 RA CCR7 naive_CD8 | 47.5% |
| Bcells Ki67_CD3neg | 47.5% |
| CD8 RO DR_CD3 | 47.5% |
| TIGIT_CD8RO | 45.0% |
| CD16mono_CD3neg | 45.0% |
| PD1_CD8RO | 42.5% |
| Bcells CD27posIgDneg_total | 42.5% |
| Ki67_CD8RO | 42.5% |
| CD8 RO CD56_CD8 | 42.5% |
| intB7_CD8RO | 42.5% |
| NK_CD3neg | 42.5% |
| CD8 RO Ki67_CD8 | 42.5% |
| Tconv memCCR6_mem | 42.5% |
| CD8 RO TIGIT_CD8 | 40.0% |
| Tconv naive_Tconv | 40.0% |
| CCR4_CD8RO | 40.0% |
| CXCR3_CD8RO | 37.5% |
| CD3hi_CD4neg | 37.5% |
| Tconv memCXCR3_mem | 35.0% |
| CD8 RO PD1_CD8 | 35.0% |
| Tconv memCD27_Tconv | 35.0% |
| CD8 RO intB7_CD8 | 35.0% |
| CCR6_CD8RO | 35.0% |
| CD27_CD8RO | 35.0% |
| CD8 RO CCR5_total | 30.0% |
| CD8 RA_CD8 | 30.0% |
| CD8 RO CCR6_CD8 | 30.0% |
| CD8 RO CCR5_CD8 | 30.0% |
| Tconv mem_Tconv | 27.5% |
| Tconv memintB7_mem | 27.5% |
| Tconv memTIGIT_mem | 25.0% |
| CD8 RA naive_CD3 | 25.0% |
| CD8 ncytotox RO CCR4_CD8ntox | 25.0% |
| CD8 RO CXCR3_CD8 | 25.0% |
| Tconv memCD56_Tconv | 25.0% |
| CD8 RO CD27_CD8 | 25.0% |
| Treg naive_CD4 | 22.5% |
| Tconv memCCR4_mem | 22.5% |
| CD8 RO_CD8 | 22.5% |
| CD8 RO intB7_CD3 | 20.0% |
| Tconv memPD1_Tconv | 20.0% |
| Tconv memCCR5_Tconv | 17.5% |
| Treg memory_CD4 | 17.5% |
| CD8 RO TIGIT_CD3 | 17.5% |
| CD14+16+mono_total | 17.5% |
| Tconv memCD56_mem | 17.5% |
| Tconv memCCR6_Tconv | 17.5% |
| Tconv memCXCR3_Tconv | 17.5% |
| CD8pos_CD3 | 17.5% |
| Tconv memTIGIT_Tconv | 17.5% |
| CD8 RO CD56_CD3 | 17.5% |
| CD3hi_CD3 | 15.0% |
| Tconv memKi67_Tconv | 15.0% |
| CD8 RO CXCR3_CD3 | 15.0% |
| Tconv memCD27_mem | 15.0% |
| CD8 RO CD27_CD3 | 15.0% |
| Tconv memDR_total | 15.0% |
| Tconv memCD27_CD3 | 15.0% |
| Tconv memintB7_Tconv | 15.0% |
| Treg memory_CD3 | 15.0% |
| Bcells_total | 12.5% |
| CD8 RA_CD3 | 12.5% |
| Tconv memKi67_mem | 12.5% |
| Tconv memPD1_mem | 12.5% |
| Tconv memCCR4_Tconv | 10.0% |
| Tconv naive_CD3 | 10.0% |
| Bcells naive_total | 10.0% |
| CD8 RO CCR6_CD3 | 10.0% |
| CD4 Treg_CD4 | 10.0% |
| myeloid_total | 10.0% |
| NK Ki67_total | 7.5% |
| CD4neg_CD3 | 7.5% |
| nonTnonB_total | 7.5% |
| CD8 RO PD1_CD3 | 7.5% |
| Tconv mem_CD3 | 7.5% |
| CD8pos_total | 5.0% |
| CD4 Tconv_CD3 | 5.0% |
| Tconv memCCR6_CD3 | 5.0% |
| CD4 Treg _CD3 | 5.0% |
| Treg naive_CD3 | 5.0% |
| CD8  RO Ki67_CD3 | 5.0% |
| Tconv memTIGIT_CD3 | 5.0% |
| CD14mono_total | 5.0% |
| Bcells memory_total | 5.0% |
| CD8 RA_total | 5.0% |
| CD8 RO_total | 2.5% |
| CD8 ncytotox RO CCR4_CD3 | 2.5% |
| CD8 RO_CD3 | 2.5% |
| CD3hi_total | 2.5% |
| CD8 RO CXCR3_total | 2.5% |
| NKCD16_total | 2.5% |
| Tconv memCXCR3_CD3 | 2.5% |
| Tconv memCCR5_CD3 | 2.5% |
| Tconv memKi67_CD3 | 2.5% |
| CD3pos_total | 2.5% |
| CD8 RO CD27_total | 2.5% |
| CD3neg_total | 2.5% |
| Tconv memCCR4_CD3 | 2.5% |
| Tconv memintB7_CD3 | 2.5% |

**Total features selected by RFE (RandomForest)_t50**: 133

#### RFE (RandomForest)_t60

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Tconv memDR_Tconv | 60.0% |
| nonTnonB_CD3neg | 57.5% |
| Bcells naive_CD3neg | 57.5% |
| Tconv memDR_CD3 | 57.5% |
| Tconv memDR_mem | 55.0% |
| myeloid_CD3neg | 52.5% |
| CD14+16+mono_CD3neg | 52.5% |
| CD14+16+mono_myeloid | 52.5% |
| CD27negIgDneg_Bcells | 52.5% |
| CD16mono_myeloid | 50.0% |
| Bcells_CD3neg | 50.0% |
| CCR5_CD8RO | 50.0% |
| NK Ki67_nonTnonB | 50.0% |
| NKCD56hi_NK | 47.5% |
| naive_Bcells | 45.0% |
| NKCD16_NK | 45.0% |
| DR_CD8RO | 45.0% |
| CD14mono_CD3neg | 42.5% |
| NK Ki67_CD3neg | 42.5% |
| CD8 RO DR_CD8 | 42.5% |
| CD27IgD_Bcells | 40.0% |
| NK_nonTnonB | 37.5% |
| NK Ki67_NK | 37.5% |
| Tconv memCCR5_mem | 37.5% |
| Ki67_Bcells | 35.0% |
| NKCD16_nonTnonB | 35.0% |
| NKCD56hi_nonTnonB | 30.0% |
| Bcells memory_CD3neg | 30.0% |
| memory_Bcells | 27.5% |
| CD8 RO DR_CD3 | 27.5% |
| CD8 RO CCR5_CD3 | 27.5% |
| NK_CD3neg | 25.0% |
| CCR4_CD8RO | 25.0% |
| CD14mono_myeloid | 25.0% |
| CD8 RO CD56_CD8 | 22.5% |
| CD56_CD8RO | 22.5% |
| CXCR3_CD8RO | 22.5% |
| NKCD16_CD3neg | 22.5% |
| Bcells Ki67_CD3neg | 22.5% |
| Ki67_CD8RO | 22.5% |
| CD16mono_CD3neg | 20.0% |
| CD8 RA CCR7 naive_CD8 | 20.0% |
| NKCD56hi_CD3neg | 20.0% |
| CD8 RO Ki67_CD8 | 17.5% |
| CD8 RA naive_CD3 | 17.5% |
| Bcells CD27posIgDneg_total | 17.5% |
| TIGIT_CD8RO | 17.5% |
| Tconv naive_Tconv | 17.5% |
| CCR6_CD8RO | 17.5% |
| intB7_CD8RO | 15.0% |
| PD1_CD8RO | 15.0% |
| CD8 RO CCR5_CD8 | 15.0% |
| Tconv memCD27_Tconv | 15.0% |
| CD8 RO TIGIT_CD8 | 15.0% |
| CD8 RO PD1_CD8 | 15.0% |
| CD3hi_CD4neg | 12.5% |
| CD8 ncytotox RO CCR4_CD8ntox | 12.5% |
| Tconv memTIGIT_mem | 12.5% |
| CD27_CD8RO | 12.5% |
| CD8 RO CCR5_total | 12.5% |
| CD8 RO CXCR3_CD8 | 12.5% |
| Tconv memCCR6_mem | 12.5% |
| Treg naive_CD4 | 12.5% |
| CD8 RO_CD8 | 10.0% |
| Tconv memCXCR3_mem | 10.0% |
| CD8 RA_CD8 | 10.0% |
| Tconv memPD1_Tconv | 7.5% |
| Tconv memPD1_mem | 7.5% |
| Tconv memCD27_mem | 7.5% |
| CD8 RO intB7_CD8 | 7.5% |
| CD8 RO CCR6_CD8 | 7.5% |
| Tconv memintB7_mem | 7.5% |
| Tconv memCXCR3_Tconv | 7.5% |
| Tconv memCCR4_mem | 7.5% |
| Tconv memCCR5_Tconv | 7.5% |
| Bcells_total | 5.0% |
| Tconv memintB7_Tconv | 5.0% |
| Tconv memCCR6_Tconv | 5.0% |
| Tconv mem_CD3 | 5.0% |
| Tconv memKi67_mem | 5.0% |
| CD8 RA_CD3 | 5.0% |
| Tconv memDR_total | 5.0% |
| Treg memory_CD4 | 5.0% |
| CD14+16+mono_total | 5.0% |
| CD8 RO CD27_CD8 | 5.0% |
| CD3hi_CD3 | 5.0% |
| Tconv memCCR6_CD3 | 5.0% |
| Tconv memCD56_mem | 5.0% |
| Tconv memCD56_Tconv | 5.0% |
| Tconv mem_Tconv | 5.0% |
| CD8 RO CD27_CD3 | 5.0% |
| CD8 RO CXCR3_CD3 | 5.0% |
| CD4 Tconv_CD3 | 2.5% |
| Tconv memCD27_CD3 | 2.5% |
| Tconv memCCR4_Tconv | 2.5% |
| Tconv memKi67_Tconv | 2.5% |
| CD8pos_CD3 | 2.5% |
| CD8 RO TIGIT_CD3 | 2.5% |
| CD8  RO Ki67_CD3 | 2.5% |
| CD4 Treg_CD4 | 2.5% |
| CD8 RO CCR6_CD3 | 2.5% |
| CD3hi_total | 2.5% |
| NKCD16_total | 2.5% |
| Tconv memCXCR3_CD3 | 2.5% |
| NK Ki67_total | 2.5% |
| CD14mono_total | 2.5% |
| CD4 Treg _CD3 | 2.5% |
| CD8 RO CD56_CD3 | 2.5% |
| CD8 RO intB7_CD3 | 2.5% |
| myeloid_total | 2.5% |
| Tconv naive_CD3 | 2.5% |
| nonTnonB_total | 2.5% |
| Tconv memintB7_CD3 | 2.5% |

**Total features selected by RFE (RandomForest)_t60**: 113

#### RFE (RandomForest)_t70

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| myeloid_CD3neg | 47.5% |
| CD14+16+mono_CD3neg | 42.5% |
| NK Ki67_nonTnonB | 35.0% |
| nonTnonB_CD3neg | 32.5% |
| Tconv memDR_Tconv | 32.5% |
| Bcells_CD3neg | 32.5% |
| Tconv memDR_CD3 | 30.0% |
| Bcells naive_CD3neg | 30.0% |
| Tconv memDR_mem | 27.5% |
| CCR5_CD8RO | 27.5% |
| CD8 RO DR_CD8 | 27.5% |
| CD27negIgDneg_Bcells | 27.5% |
| naive_Bcells | 25.0% |
| CD14+16+mono_myeloid | 25.0% |
| Tconv memCCR5_mem | 25.0% |
| NKCD16_NK | 22.5% |
| NK Ki67_NK | 20.0% |
| CD27IgD_Bcells | 20.0% |
| NK Ki67_CD3neg | 20.0% |
| CD8 RO DR_CD3 | 17.5% |
| CD16mono_myeloid | 17.5% |
| NK_nonTnonB | 17.5% |
| DR_CD8RO | 17.5% |
| memory_Bcells | 15.0% |
| Ki67_Bcells | 15.0% |
| NKCD16_CD3neg | 15.0% |
| NKCD16_nonTnonB | 15.0% |
| NKCD56hi_NK | 15.0% |
| CD14mono_CD3neg | 12.5% |
| Bcells Ki67_CD3neg | 12.5% |
| NKCD56hi_nonTnonB | 12.5% |
| CD8 RO CCR5_CD3 | 12.5% |
| Bcells memory_CD3neg | 12.5% |
| Bcells CD27posIgDneg_total | 12.5% |
| CCR4_CD8RO | 10.0% |
| NK_CD3neg | 10.0% |
| CD8 RO Ki67_CD8 | 10.0% |
| CD8 RO CD56_CD8 | 10.0% |
| CD8 RA naive_CD3 | 7.5% |
| Tconv memCXCR3_mem | 7.5% |
| Ki67_CD8RO | 7.5% |
| intB7_CD8RO | 7.5% |
| Tconv naive_Tconv | 7.5% |
| CD8 RO PD1_CD8 | 7.5% |
| CD27_CD8RO | 7.5% |
| Tconv memCD27_Tconv | 7.5% |
| NKCD56hi_CD3neg | 7.5% |
| CD8 RA CCR7 naive_CD8 | 7.5% |
| CD14mono_myeloid | 5.0% |
| Tconv memDR_total | 5.0% |
| PD1_CD8RO | 5.0% |
| CCR6_CD8RO | 5.0% |
| CD8 RO TIGIT_CD8 | 5.0% |
| CXCR3_CD8RO | 5.0% |
| CD14+16+mono_total | 5.0% |
| Treg naive_CD4 | 5.0% |
| CD16mono_CD3neg | 5.0% |
| CD8 RO CD27_CD3 | 5.0% |
| CD8 RO CCR5_CD8 | 5.0% |
| Tconv memCCR4_mem | 5.0% |
| Tconv memKi67_mem | 2.5% |
| Tconv memCCR4_Tconv | 2.5% |
| Tconv memCD56_mem | 2.5% |
| Tconv memintB7_mem | 2.5% |
| Tconv memTIGIT_mem | 2.5% |
| CD8 RO CD27_CD8 | 2.5% |
| CD8 RO_CD8 | 2.5% |
| CD8 ncytotox RO CCR4_CD8ntox | 2.5% |
| CD8 RO CCR6_CD8 | 2.5% |
| CD8 RA_CD8 | 2.5% |
| CD56_CD8RO | 2.5% |
| CD8 RA_CD3 | 2.5% |
| Tconv memCD27_mem | 2.5% |
| CD8 RO intB7_CD8 | 2.5% |
| CD8 RO CXCR3_CD8 | 2.5% |
| CD8 RO CCR5_total | 2.5% |
| TIGIT_CD8RO | 2.5% |
| Tconv memCCR5_Tconv | 2.5% |
| CD8 RO intB7_CD3 | 2.5% |
| myeloid_total | 2.5% |
| Tconv memCXCR3_Tconv | 2.5% |

**Total features selected by RFE (RandomForest)_t70**: 81

#### RFE (RandomForest)_t80

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| myeloid_CD3neg | 32.0% |
| Tconv memDR_Tconv | 24.0% |
| CD14+16+mono_CD3neg | 24.0% |
| Tconv memDR_mem | 24.0% |
| Bcells naive_CD3neg | 16.0% |
| NKCD16_NK | 16.0% |
| NKCD56hi_NK | 16.0% |
| CD27negIgDneg_Bcells | 16.0% |
| NK Ki67_nonTnonB | 16.0% |
| Tconv memCCR5_mem | 12.0% |
| CCR5_CD8RO | 12.0% |
| CD8 RO DR_CD8 | 12.0% |
| DR_CD8RO | 12.0% |
| naive_Bcells | 12.0% |
| Tconv memDR_CD3 | 12.0% |
| Bcells_CD3neg | 12.0% |
| NKCD16_nonTnonB | 8.0% |
| Bcells memory_CD3neg | 8.0% |
| Ki67_Bcells | 8.0% |
| NKCD16_CD3neg | 8.0% |
| NK_nonTnonB | 8.0% |
| nonTnonB_CD3neg | 8.0% |
| memory_Bcells | 8.0% |
| Tconv memDR_total | 8.0% |
| CD8 RO DR_CD3 | 8.0% |
| Tconv memCCR4_mem | 8.0% |
| CD16mono_myeloid | 4.0% |
| CD14+16+mono_myeloid | 4.0% |
| CD16mono_CD3neg | 4.0% |
| CCR4_CD8RO | 4.0% |
| CD14mono_myeloid | 4.0% |
| NK Ki67_CD3neg | 4.0% |
| CD27_CD8RO | 4.0% |
| Tconv memCD27_Tconv | 4.0% |
| intB7_CD8RO | 4.0% |
| Bcells Ki67_CD3neg | 4.0% |
| CD8 RO CCR5_CD3 | 4.0% |
| CD8 RO CCR5_total | 4.0% |
| Tconv memCXCR3_mem | 4.0% |
| Bcells CD27posIgDneg_total | 4.0% |
| CXCR3_CD8RO | 4.0% |
| CD27IgD_Bcells | 4.0% |

**Total features selected by RFE (RandomForest)_t80**: 42

#### RF_Importance_t40

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Bcells CD27posIgDneg_total | 97.5% |
| Tconv memDR_CD3 | 97.5% |
| Tconv memDR_Tconv | 92.5% |
| Tconv memDR_mem | 90.0% |
| CD8 RO CCR5_total | 85.0% |
| Tconv memCCR5_mem | 80.0% |
| CD14+16+mono_CD3neg | 77.5% |
| CD8 RO CCR5_CD3 | 77.5% |
| Tconv memDR_total | 75.0% |
| myeloid_CD3neg | 72.5% |
| CCR5_CD8RO | 72.5% |
| NK Ki67_total | 67.5% |
| CD8 RO DR_CD3 | 67.5% |
| myeloid_total | 67.5% |
| nonTnonB_CD3neg | 65.0% |
| NK Ki67_nonTnonB | 65.0% |
| NKCD16_nonTnonB | 65.0% |
| Bcells naive_CD3neg | 62.5% |
| CD14+16+mono_total | 62.5% |
| CD8 RO DR_CD8 | 62.5% |
| Tconv memCD27_Tconv | 62.5% |
| NK Ki67_CD3neg | 62.5% |
| Bcells_total | 60.0% |
| Bcells naive_total | 60.0% |
| CD27negIgDneg_Bcells | 60.0% |
| DR_CD8RO | 57.5% |
| CD8 RA CCR7 naive_CD8 | 57.5% |
| CD8 RA naive_CD3 | 57.5% |
| CD8pos_total | 57.5% |
| Tconv naive_CD3 | 52.5% |
| Tconv mem_Tconv | 52.5% |
| Tconv memCXCR3_mem | 52.5% |
| Tconv memCCR5_Tconv | 52.5% |
| NKCD16_NK | 52.5% |
| NK_nonTnonB | 50.0% |
| CD8 RA naive_total | 50.0% |
| nonTnonB_total | 50.0% |
| Bcells_CD3neg | 47.5% |
| Tconv memintB7_mem | 47.5% |
| CD14mono_total | 45.0% |
| CD27IgD_Bcells | 45.0% |
| CD16mono_myeloid | 45.0% |
| CD8 RA_CD3 | 45.0% |
| CD8 RA_total | 42.5% |
| NKCD16_CD3neg | 42.5% |
| CD8 RO CXCR3_CD3 | 42.5% |
| CD14mono_CD3neg | 42.5% |
| CD4neg_total | 42.5% |
| Tconv naive_Tconv | 42.5% |
| CD14+16+mono_myeloid | 42.5% |
| Treg memory_CD3 | 40.0% |
| CD56_CD8RO | 40.0% |
| Bcells memory_total | 40.0% |
| Tconv memCD27_CD3 | 40.0% |
| Treg naive_CD4 | 40.0% |
| Tconv memCCR5_total | 37.5% |
| CD4 Treg _CD3 | 37.5% |
| CD8 RO CCR6_total | 35.0% |
| naive_Bcells | 35.0% |
| CD8pos_CD3 | 35.0% |
| CD8 RO CD27_CD3 | 35.0% |
| Treg memory_CD4 | 35.0% |
| NK_total | 32.5% |
| NK_CD3neg | 32.5% |
| Bcells memory_CD3neg | 32.5% |
| CD8 RO_total | 32.5% |
| Ki67_Bcells | 32.5% |
| CD8 RO intB7_total | 32.5% |
| Treg naive_total | 30.0% |
| Tconv naive_total | 30.0% |
| CCR4_CD8RO | 30.0% |
| CD3hi_total | 30.0% |
| Tconv memCCR4_CD3 | 30.0% |
| CD8 RO CD56_CD8 | 30.0% |
| NK Ki67_NK | 30.0% |
| Tconv memCXCR3_CD3 | 27.5% |
| Tconv memCCR6_mem | 27.5% |
| NKCD56hi_total | 27.5% |
| CD4 Treg_CD4 | 27.5% |
| NKCD56hi_NK | 27.5% |
| CD8 RO CD27_total | 27.5% |
| Tconv memPD1_total | 27.5% |
| NKCD16_total | 25.0% |
| CD3neg_total | 25.0% |
| CD8 RO CCR5_CD8 | 25.0% |
| CD8 RO intB7_CD3 | 25.0% |
| CD8 RO CXCR3_total | 25.0% |
| Tconv memCCR4_mem | 25.0% |
| Tconv memCCR6_Tconv | 25.0% |
| CD8 RA_CD8 | 25.0% |
| Ki67_CD8RO | 25.0% |
| CD8 RO TIGIT_total | 22.5% |
| memory_Bcells | 22.5% |
| CD3hi_CD3 | 22.5% |
| Tconv memCXCR3_total | 22.5% |
| CD8 RO DR_total | 20.0% |
| CD8 RO CCR4_total | 20.0% |
| CD8 RO CD56_total | 20.0% |
| CD8 RO CCR6_CD3 | 20.0% |
| CD3hi_CD4neg | 20.0% |
| Treg naive_CD3 | 20.0% |
| CD8 RO TIGIT_CD3 | 20.0% |
| intB7_CD8RO | 20.0% |
| CD8 RO PD1_CD8 | 20.0% |
| CD8 RO CXCR3_CD8 | 17.5% |
| Tconv mem_CD3 | 17.5% |
| Tconv memCD27_mem | 17.5% |
| Tconv memCCR4_Tconv | 17.5% |
| CD4 Treg_total | 17.5% |
| Tconv memPD1_Tconv | 17.5% |
| Tconv memCXCR3_Tconv | 17.5% |
| CD8 RO PD1_total | 17.5% |
| Bcells CD27negIgDneg_total | 17.5% |
| CD8  RO Ki67_CD3 | 15.0% |
| CD8 RO_CD8 | 15.0% |
| CD8 RO_CD3 | 15.0% |
| Tconv memTIGIT_mem | 15.0% |
| CD8 RO Ki67_CD8 | 15.0% |
| Tconv memKi67_mem | 15.0% |
| CD3pos_total | 15.0% |
| NKCD56hi_nonTnonB | 12.5% |
| Tconv memintB7_CD3 | 12.5% |
| CD8 RO Ki67_total | 12.5% |
| CD4 Tconv_CD3 | 12.5% |
| CXCR3_CD8RO | 12.5% |
| Tconv memCCR6_total | 12.5% |
| Tconv memCCR6_CD3 | 12.5% |
| Tconv memCCR5_CD3 | 12.5% |
| CD8 ncytotox RO CCR4_CD8ntox | 12.5% |
| CD27_CD8RO | 12.5% |
| CD8 RO CCR6_CD8 | 12.5% |
| Tconv memCCR4_total | 10.0% |
| Tconv memKi67_total | 10.0% |
| NKCD56hi_CD3neg | 10.0% |
| Tconv memTIGIT_total | 10.0% |
| Tconv memTIGIT_Tconv | 10.0% |
| CD8 RO CD27_CD8 | 10.0% |
| CD8 RO PD1_CD3 | 10.0% |
| Tconv memCD56_Tconv | 10.0% |
| Tconv memKi67_Tconv | 10.0% |
| CD8 RO intB7_CD8 | 10.0% |
| Tconv memTIGIT_CD3 | 10.0% |
| Tconv memCD56_mem | 7.5% |
| Tconv memintB7_total | 7.5% |
| Tconv memPD1_CD3 | 7.5% |
| CD4 Tconv_total | 7.5% |
| TIGIT_CD8RO | 7.5% |
| CCR6_CD8RO | 7.5% |
| CD16+mono_total | 7.5% |
| Tconv memCD27_total | 7.5% |
| Tconv memintB7_Tconv | 7.5% |
| Bcells Ki67_total | 7.5% |
| CD16mono_CD3neg | 7.5% |
| Bcells Ki67_CD3neg | 7.5% |
| Tconv memPD1_mem | 5.0% |
| CD8 ncytotox RO CCR4_CD3 | 5.0% |
| Tconv memCD56_total | 5.0% |
| CD8 RO TIGIT_CD8 | 5.0% |
| CD14mono_myeloid | 5.0% |
| CD8 RO CD56_CD3 | 5.0% |
| CD4 Tconv mem_total | 5.0% |
| PD1_CD8RO | 2.5% |
| Tconv memKi67_CD3 | 2.5% |
| Tconv memCD56_CD3 | 2.5% |
| CD4neg_CD3 | 2.5% |

**Total features selected by RF_Importance_t40**: 165

#### RF_Importance_t50

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Tconv memDR_CD3 | 95.0% |
| Bcells CD27posIgDneg_total | 92.5% |
| Tconv memDR_Tconv | 90.0% |
| Tconv memDR_mem | 75.0% |
| CD8 RO CCR5_total | 75.0% |
| Tconv memCCR5_mem | 67.5% |
| Tconv memDR_total | 65.0% |
| CD8 RO CCR5_CD3 | 65.0% |
| CCR5_CD8RO | 62.5% |
| CD14+16+mono_CD3neg | 62.5% |
| CD8 RO DR_CD8 | 57.5% |
| myeloid_CD3neg | 57.5% |
| CD8 RO DR_CD3 | 52.5% |
| CD27negIgDneg_Bcells | 52.5% |
| nonTnonB_CD3neg | 50.0% |
| NK Ki67_nonTnonB | 47.5% |
| NK Ki67_total | 47.5% |
| Bcells naive_CD3neg | 45.0% |
| CD8pos_total | 42.5% |
| myeloid_total | 42.5% |
| CD14+16+mono_total | 42.5% |
| Bcells_total | 42.5% |
| NK Ki67_CD3neg | 40.0% |
| Tconv memCD27_Tconv | 40.0% |
| CD8 RA CCR7 naive_CD8 | 40.0% |
| CD8 RA naive_CD3 | 37.5% |
| nonTnonB_total | 37.5% |
| NKCD16_NK | 37.5% |
| Tconv mem_Tconv | 37.5% |
| Bcells naive_total | 37.5% |
| Bcells_CD3neg | 37.5% |
| NKCD16_nonTnonB | 35.0% |
| CD8 RA naive_total | 32.5% |
| DR_CD8RO | 32.5% |
| CD16mono_myeloid | 32.5% |
| Tconv memCXCR3_mem | 30.0% |
| CD14mono_CD3neg | 30.0% |
| CD8 RO_total | 27.5% |
| CD14mono_total | 27.5% |
| CD14+16+mono_myeloid | 27.5% |
| Tconv memCCR5_Tconv | 27.5% |
| CD27IgD_Bcells | 27.5% |
| NKCD16_CD3neg | 25.0% |
| Treg memory_CD4 | 25.0% |
| Tconv memCD27_CD3 | 25.0% |
| NK_nonTnonB | 25.0% |
| CD8 RO CXCR3_CD3 | 25.0% |
| CD8 RA_total | 25.0% |
| CD4 Treg _CD3 | 25.0% |
| CD8pos_CD3 | 25.0% |
| Tconv memintB7_mem | 22.5% |
| Tconv naive_CD3 | 22.5% |
| CD8 RO CD27_CD3 | 20.0% |
| Bcells memory_CD3neg | 20.0% |
| Bcells memory_total | 20.0% |
| Tconv naive_Tconv | 20.0% |
| CD4neg_total | 20.0% |
| naive_Bcells | 20.0% |
| CD8 RO CXCR3_total | 17.5% |
| NK Ki67_NK | 17.5% |
| NKCD16_total | 17.5% |
| CD56_CD8RO | 17.5% |
| CD8 RO CCR6_total | 17.5% |
| Treg memory_CD3 | 15.0% |
| Treg naive_CD4 | 15.0% |
| NKCD56hi_NK | 15.0% |
| Treg naive_total | 15.0% |
| Tconv memCXCR3_CD3 | 15.0% |
| NK_total | 15.0% |
| CD3neg_total | 15.0% |
| CD8 RO CD56_CD8 | 15.0% |
| NKCD56hi_total | 15.0% |
| CD8 RA_CD3 | 15.0% |
| CD8 RO CXCR3_CD8 | 15.0% |
| CD4 Treg_CD4 | 15.0% |
| CD3hi_CD3 | 15.0% |
| Ki67_Bcells | 12.5% |
| CD8 RO intB7_total | 12.5% |
| Tconv naive_total | 12.5% |
| CD8 RO intB7_CD3 | 12.5% |
| CD8 RO TIGIT_CD3 | 12.5% |
| CD8 RO TIGIT_total | 12.5% |
| Tconv memCCR4_CD3 | 12.5% |
| CD8 RO CCR5_CD8 | 12.5% |
| Tconv memCCR6_mem | 12.5% |
| CD8 RO CCR6_CD3 | 10.0% |
| Tconv memPD1_total | 10.0% |
| NK_CD3neg | 10.0% |
| CD8 RA_CD8 | 10.0% |
| CCR4_CD8RO | 10.0% |
| CD8 RO_CD8 | 10.0% |
| Treg naive_CD3 | 10.0% |
| Tconv memCCR4_mem | 10.0% |
| CD3pos_total | 10.0% |
| CD8 RO DR_total | 10.0% |
| Tconv memTIGIT_CD3 | 10.0% |
| Bcells CD27negIgDneg_total | 10.0% |
| Tconv memTIGIT_mem | 7.5% |
| Ki67_CD8RO | 7.5% |
| CD8 RO CD27_total | 7.5% |
| CD8 RO intB7_CD8 | 7.5% |
| Tconv memCCR6_Tconv | 7.5% |
| CD8 RO Ki67_CD8 | 7.5% |
| CD8 RO CD27_CD8 | 7.5% |
| CD3hi_total | 7.5% |
| Tconv memCD56_mem | 7.5% |
| Tconv memCXCR3_Tconv | 7.5% |
| Tconv memCCR4_Tconv | 7.5% |
| Tconv memCCR5_total | 7.5% |
| CD8 RO CCR4_total | 7.5% |
| NKCD56hi_CD3neg | 5.0% |
| NKCD56hi_nonTnonB | 5.0% |
| Tconv memintB7_CD3 | 5.0% |
| CD8 RO CD56_total | 5.0% |
| Tconv memCD27_mem | 5.0% |
| Tconv memKi67_mem | 5.0% |
| Tconv memPD1_Tconv | 5.0% |
| Tconv memCXCR3_total | 5.0% |
| Tconv memCD27_total | 5.0% |
| CD27_CD8RO | 5.0% |
| CXCR3_CD8RO | 5.0% |
| Tconv memTIGIT_Tconv | 5.0% |
| CCR6_CD8RO | 5.0% |
| CD4 Tconv_CD3 | 5.0% |
| Tconv memCCR6_CD3 | 5.0% |
| CD8 RO CCR6_CD8 | 5.0% |
| memory_Bcells | 5.0% |
| Tconv mem_CD3 | 5.0% |
| CD4 Treg_total | 5.0% |
| Tconv memintB7_Tconv | 5.0% |
| CD8 RO Ki67_total | 5.0% |
| Tconv memCCR6_total | 5.0% |
| Tconv memCCR5_CD3 | 5.0% |
| CD3hi_CD4neg | 2.5% |
| CD8 RO PD1_CD8 | 2.5% |
| Tconv memCCR4_total | 2.5% |
| Tconv memCD56_Tconv | 2.5% |
| CD4 Tconv_total | 2.5% |
| CD8 RO PD1_total | 2.5% |
| CD14mono_myeloid | 2.5% |
| Tconv memKi67_Tconv | 2.5% |
| CD16+mono_total | 2.5% |
| Bcells Ki67_CD3neg | 2.5% |
| TIGIT_CD8RO | 2.5% |
| CD8  RO Ki67_CD3 | 2.5% |
| Tconv memintB7_total | 2.5% |
| Tconv memPD1_CD3 | 2.5% |
| CD8 RO_CD3 | 2.5% |
| CD8 ncytotox RO CCR4_CD3 | 2.5% |
| CD8 ncytotox RO CCR4_CD8ntox | 2.5% |
| intB7_CD8RO | 2.5% |
| Tconv memTIGIT_total | 2.5% |
| CD8 RO PD1_CD3 | 2.5% |
| Tconv memPD1_mem | 2.5% |

**Total features selected by RF_Importance_t50**: 154

#### RF_Importance_t60

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Bcells CD27posIgDneg_total | 77.5% |
| Tconv memDR_CD3 | 77.5% |
| Tconv memDR_Tconv | 72.5% |
| Tconv memDR_mem | 60.0% |
| CD8 RO CCR5_total | 55.0% |
| CD8 RO CCR5_CD3 | 52.5% |
| CCR5_CD8RO | 50.0% |
| CD14+16+mono_CD3neg | 50.0% |
| myeloid_CD3neg | 47.5% |
| Tconv memDR_total | 47.5% |
| CD8 RO DR_CD8 | 45.0% |
| CD8 RO DR_CD3 | 40.0% |
| Tconv memCCR5_mem | 37.5% |
| NK Ki67_nonTnonB | 35.0% |
| CD8pos_total | 35.0% |
| Bcells_total | 32.5% |
| Bcells naive_CD3neg | 32.5% |
| CD27negIgDneg_Bcells | 32.5% |
| nonTnonB_CD3neg | 30.0% |
| myeloid_total | 30.0% |
| NK Ki67_total | 27.5% |
| Bcells naive_total | 25.0% |
| CD8 RA naive_CD3 | 25.0% |
| CD8 RA naive_total | 25.0% |
| NKCD16_NK | 25.0% |
| NK Ki67_CD3neg | 25.0% |
| CD8 RA CCR7 naive_CD8 | 22.5% |
| DR_CD8RO | 22.5% |
| CD8 RO_total | 20.0% |
| Tconv mem_Tconv | 20.0% |
| CD8 RA_total | 20.0% |
| nonTnonB_total | 20.0% |
| CD14+16+mono_total | 20.0% |
| CD16mono_myeloid | 20.0% |
| Bcells_CD3neg | 20.0% |
| CD27IgD_Bcells | 17.5% |
| Tconv memCD27_Tconv | 17.5% |
| Tconv memCCR5_Tconv | 17.5% |
| naive_Bcells | 17.5% |
| Tconv naive_CD3 | 17.5% |
| CD8pos_CD3 | 17.5% |
| CD14mono_total | 17.5% |
| CD14+16+mono_myeloid | 15.0% |
| NKCD16_CD3neg | 15.0% |
| NKCD16_total | 15.0% |
| CD8 RO CXCR3_CD3 | 15.0% |
| Tconv memCD27_CD3 | 12.5% |
| Treg memory_CD4 | 12.5% |
| Tconv memCXCR3_mem | 12.5% |
| NK Ki67_NK | 12.5% |
| CD4neg_total | 12.5% |
| Bcells memory_total | 12.5% |
| CD8 RO intB7_CD3 | 10.0% |
| CD14mono_CD3neg | 10.0% |
| CD8 RO TIGIT_CD3 | 10.0% |
| NKCD16_nonTnonB | 10.0% |
| Treg naive_CD4 | 10.0% |
| NK_nonTnonB | 10.0% |
| Tconv memCCR6_mem | 10.0% |
| CD8 RO CXCR3_total | 7.5% |
| CD3neg_total | 7.5% |
| CD8 RO TIGIT_total | 7.5% |
| Tconv naive_Tconv | 7.5% |
| Tconv memintB7_mem | 7.5% |
| CD4 Treg_CD4 | 7.5% |
| CD4 Treg _CD3 | 7.5% |
| CD3hi_CD3 | 7.5% |
| NK_total | 7.5% |
| Bcells memory_CD3neg | 7.5% |
| NKCD56hi_total | 5.0% |
| Tconv naive_total | 5.0% |
| NKCD56hi_CD3neg | 5.0% |
| Treg memory_CD3 | 5.0% |
| CD8 RO Ki67_CD8 | 5.0% |
| CD4 Tconv_CD3 | 5.0% |
| CD3hi_total | 5.0% |
| CD8 RO CD56_CD8 | 5.0% |
| CD8 RO CCR5_CD8 | 5.0% |
| CD8 RO CCR6_total | 5.0% |
| CD8 RO CD27_CD3 | 5.0% |
| NKCD56hi_NK | 5.0% |
| Ki67_Bcells | 5.0% |
| Tconv memCCR4_mem | 5.0% |
| CD8 RO Ki67_total | 5.0% |
| CD8 RO CCR6_CD3 | 5.0% |
| Tconv memTIGIT_CD3 | 5.0% |
| CD8 RO_CD8 | 5.0% |
| Tconv memPD1_total | 5.0% |
| Tconv memCXCR3_CD3 | 5.0% |
| CD8 RO CXCR3_CD8 | 5.0% |
| CD3pos_total | 5.0% |
| CD56_CD8RO | 5.0% |
| CD8 RA_CD8 | 5.0% |
| CD8 RO CCR6_CD8 | 2.5% |
| CD3hi_CD4neg | 2.5% |
| CD8 RO CCR4_total | 2.5% |
| Tconv mem_CD3 | 2.5% |
| CCR6_CD8RO | 2.5% |
| NK_CD3neg | 2.5% |
| CD8 RO DR_total | 2.5% |
| Tconv memCXCR3_total | 2.5% |
| CD8 RO CD27_CD8 | 2.5% |
| CD8 RO CD27_total | 2.5% |
| Tconv memCD56_mem | 2.5% |
| CCR4_CD8RO | 2.5% |
| CD4 Treg_total | 2.5% |
| Bcells CD27negIgDneg_total | 2.5% |
| Tconv memCCR6_total | 2.5% |
| Tconv memCCR5_total | 2.5% |
| Tconv memCCR6_Tconv | 2.5% |
| Tconv memTIGIT_mem | 2.5% |
| Tconv memCCR4_CD3 | 2.5% |
| CXCR3_CD8RO | 2.5% |
| intB7_CD8RO | 2.5% |
| CD8 RO intB7_total | 2.5% |
| Treg naive_total | 2.5% |
| CD8 RO PD1_CD3 | 2.5% |
| Tconv memCXCR3_Tconv | 2.5% |
| Ki67_CD8RO | 2.5% |

**Total features selected by RF_Importance_t60**: 119

#### RF_Importance_t70

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Tconv memDR_CD3 | 62.5% |
| Bcells CD27posIgDneg_total | 57.5% |
| Tconv memDR_Tconv | 52.5% |
| Tconv memDR_mem | 37.5% |
| CD8 RO CCR5_total | 37.5% |
| CD8 RO CCR5_CD3 | 37.5% |
| CD8 RO DR_CD3 | 35.0% |
| Tconv memDR_total | 32.5% |
| CD8 RO DR_CD8 | 27.5% |
| Bcells naive_CD3neg | 27.5% |
| CD14+16+mono_CD3neg | 27.5% |
| Tconv memCCR5_mem | 25.0% |
| CCR5_CD8RO | 25.0% |
| CD27negIgDneg_Bcells | 22.5% |
| CD8pos_total | 20.0% |
| nonTnonB_CD3neg | 20.0% |
| DR_CD8RO | 17.5% |
| myeloid_total | 17.5% |
| myeloid_CD3neg | 17.5% |
| Bcells naive_total | 17.5% |
| Bcells_total | 17.5% |
| NK Ki67_nonTnonB | 15.0% |
| nonTnonB_total | 15.0% |
| CD16mono_myeloid | 12.5% |
| CD8 RA naive_CD3 | 12.5% |
| CD8 RA CCR7 naive_CD8 | 12.5% |
| NK Ki67_CD3neg | 10.0% |
| CD14+16+mono_total | 10.0% |
| CD8 RA_total | 10.0% |
| CD27IgD_Bcells | 10.0% |
| Tconv memCXCR3_mem | 10.0% |
| Tconv mem_Tconv | 10.0% |
| NKCD16_CD3neg | 10.0% |
| CD14+16+mono_myeloid | 10.0% |
| NKCD16_NK | 7.5% |
| Bcells_CD3neg | 7.5% |
| NK Ki67_NK | 7.5% |
| CD8 RO TIGIT_CD3 | 7.5% |
| NK Ki67_total | 7.5% |
| CD8 RA naive_total | 7.5% |
| CD4 Treg_CD4 | 7.5% |
| NKCD16_nonTnonB | 5.0% |
| CD4 Tconv_CD3 | 5.0% |
| Tconv naive_total | 5.0% |
| CD8 RO intB7_CD3 | 5.0% |
| CD8 RO CCR5_CD8 | 5.0% |
| CD8 RO_total | 5.0% |
| CD8 RO CD27_CD3 | 5.0% |
| Treg memory_CD4 | 5.0% |
| Ki67_Bcells | 5.0% |
| CD8 RO CXCR3_CD3 | 5.0% |
| CD8pos_CD3 | 5.0% |
| Tconv memCD27_Tconv | 5.0% |
| CD4neg_total | 5.0% |
| CD14mono_CD3neg | 5.0% |
| CD14mono_total | 5.0% |
| CD3pos_total | 5.0% |
| NKCD16_total | 5.0% |
| CD8 RO DR_total | 2.5% |
| CD8 RO CCR6_total | 2.5% |
| CD8 RO TIGIT_total | 2.5% |
| CD8 RO CXCR3_total | 2.5% |
| CD8 RO CCR4_total | 2.5% |
| Tconv memintB7_mem | 2.5% |
| Tconv memCCR4_mem | 2.5% |
| Tconv memCCR6_total | 2.5% |
| CD8 RO Ki67_total | 2.5% |
| Tconv memCCR5_total | 2.5% |
| Treg naive_CD4 | 2.5% |
| CD8 RO CD27_total | 2.5% |
| Tconv memCCR5_Tconv | 2.5% |
| NKCD56hi_NK | 2.5% |
| CD8 RO CCR6_CD3 | 2.5% |
| Tconv memCD27_CD3 | 2.5% |
| Bcells memory_total | 2.5% |
| Tconv memPD1_total | 2.5% |
| Tconv memCCR6_mem | 2.5% |
| CXCR3_CD8RO | 2.5% |
| intB7_CD8RO | 2.5% |
| naive_Bcells | 2.5% |
| NK_total | 2.5% |
| Treg memory_CD3 | 2.5% |
| Bcells memory_CD3neg | 2.5% |
| NK_nonTnonB | 2.5% |
| Tconv naive_Tconv | 2.5% |
| CD3neg_total | 2.5% |

**Total features selected by RF_Importance_t70**: 86

#### RF_Importance_t80

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Tconv memDR_CD3 | 52.5% |
| Tconv memDR_Tconv | 37.5% |
| Bcells CD27posIgDneg_total | 32.5% |
| Tconv memDR_total | 25.0% |
| CD8 RO CCR5_CD3 | 22.5% |
| CD8 RO DR_CD3 | 20.0% |
| Tconv memDR_mem | 20.0% |
| CD8 RO CCR5_total | 20.0% |
| Tconv memCCR5_mem | 20.0% |
| CCR5_CD8RO | 15.0% |
| nonTnonB_CD3neg | 12.5% |
| CD8 RO DR_CD8 | 12.5% |
| nonTnonB_total | 10.0% |
| Bcells naive_total | 10.0% |
| CD14+16+mono_CD3neg | 10.0% |
| Bcells_total | 10.0% |
| myeloid_total | 7.5% |
| DR_CD8RO | 7.5% |
| CD8pos_total | 7.5% |
| CD14+16+mono_myeloid | 7.5% |
| CD8 RA naive_CD3 | 7.5% |
| CD14+16+mono_total | 5.0% |
| Tconv mem_Tconv | 5.0% |
| CD27IgD_Bcells | 5.0% |
| CD16mono_myeloid | 5.0% |
| Bcells naive_CD3neg | 5.0% |
| NK Ki67_nonTnonB | 5.0% |
| CD8 RA_total | 5.0% |
| CD27negIgDneg_Bcells | 5.0% |
| NK Ki67_CD3neg | 2.5% |
| CD8 RA CCR7 naive_CD8 | 2.5% |
| Tconv memCXCR3_mem | 2.5% |
| CD8 RO intB7_CD3 | 2.5% |
| NKCD16_nonTnonB | 2.5% |
| CD8 RO DR_total | 2.5% |
| CD8 RO_total | 2.5% |
| CD8 RO TIGIT_CD3 | 2.5% |
| CD8 RO CD27_CD3 | 2.5% |
| CD8 RO CD27_total | 2.5% |
| CD4 Treg_CD4 | 2.5% |
| Treg memory_CD4 | 2.5% |
| CD8 RO CXCR3_CD3 | 2.5% |
| CD8 RO CXCR3_total | 2.5% |
| CD8 RO CCR6_CD3 | 2.5% |
| NKCD56hi_NK | 2.5% |
| CD8 RA naive_total | 2.5% |
| NKCD16_CD3neg | 2.5% |
| NKCD16_NK | 2.5% |
| Tconv memCCR5_Tconv | 2.5% |
| Tconv memCCR6_mem | 2.5% |
| intB7_CD8RO | 2.5% |
| Ki67_Bcells | 2.5% |
| CD14mono_total | 2.5% |
| CD14mono_CD3neg | 2.5% |
| Treg memory_CD3 | 2.5% |
| Bcells memory_CD3neg | 2.5% |
| NK_nonTnonB | 2.5% |
| NK Ki67_NK | 2.5% |
| Tconv naive_total | 2.5% |

**Total features selected by RF_Importance_t80**: 59

#### RandomForest_Permutation_Top10%_t40

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

**Total features selected by RandomForest_Permutation_Top10%_t40**: 16

#### RandomForest_Permutation_Top10%_t50

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD3pos_total | 100.0% |
| CD4 Tconv_total | 100.0% |
| CD4 Tconv mem_total | 100.0% |
| Tconv memCCR4_total | 100.0% |
| Tconv memCCR5_total | 100.0% |
| Tconv memCD27_total | 100.0% |
| Tconv memCD56_total | 100.0% |
| Tconv memCXCR3_total | 100.0% |
| Tconv memPD1_total | 100.0% |
| Tconv memDR_total | 100.0% |
| Tconv memintB7_total | 100.0% |
| Tconv memKi67_total | 100.0% |
| Tconv naive_total | 100.0% |
| Tconv memTIGIT_total | 100.0% |
| CD4 Treg_total | 100.0% |
| Tconv memCCR6_total | 95.0% |

**Total features selected by RandomForest_Permutation_Top10%_t50**: 16

#### RandomForest_Permutation_Top10%_t60

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD3pos_total | 100.0% |
| CD4 Tconv mem_total | 100.0% |
| Tconv memCD27_total | 100.0% |
| Tconv memCCR5_total | 100.0% |
| Tconv memCD56_total | 100.0% |
| Tconv memintB7_total | 100.0% |
| Tconv memDR_total | 100.0% |
| Tconv memCXCR3_total | 100.0% |
| Tconv memPD1_total | 100.0% |
| Tconv naive_total | 100.0% |
| CD4 Treg_total | 100.0% |
| Tconv memKi67_total | 100.0% |
| CD4 Tconv_total | 97.5% |
| Tconv memCCR4_total | 97.5% |
| Tconv memTIGIT_total | 97.5% |
| Tconv memCCR6_total | 82.5% |

**Total features selected by RandomForest_Permutation_Top10%_t60**: 16

#### RandomForest_Permutation_Top10%_t70

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD3pos_total | 100.0% |
| Tconv memCD56_total | 100.0% |
| Tconv memCD27_total | 100.0% |
| Tconv memPD1_total | 100.0% |
| Tconv memKi67_total | 100.0% |
| Tconv memintB7_total | 100.0% |
| Tconv memDR_total | 100.0% |
| Tconv memCXCR3_total | 100.0% |
| CD4 Treg_total | 100.0% |
| Tconv naive_total | 100.0% |
| CD4 Tconv mem_total | 97.5% |
| Tconv memTIGIT_total | 97.5% |
| Tconv memCCR4_total | 90.0% |
| CD4 Tconv_total | 87.5% |
| Tconv memCCR5_total | 87.5% |
| Tconv memCCR6_total | 70.0% |

**Total features selected by RandomForest_Permutation_Top10%_t70**: 16

#### RandomForest_Permutation_Top10%_t80

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Tconv memCD27_total | 100.0% |
| Tconv memCD56_total | 100.0% |
| Tconv memDR_total | 100.0% |
| Tconv naive_total | 100.0% |
| Tconv memKi67_total | 100.0% |
| Tconv memintB7_total | 100.0% |
| Tconv memCXCR3_total | 100.0% |
| Tconv memPD1_total | 97.5% |
| CD4 Treg_total | 95.0% |
| CD3pos_total | 92.5% |
| CD4 Tconv mem_total | 87.5% |
| Tconv memTIGIT_total | 82.5% |
| CD4 Tconv_total | 72.5% |
| Tconv memCCR4_total | 72.5% |
| Tconv memCCR5_total | 57.5% |
| Tconv memCCR6_total | 47.5% |

**Total features selected by RandomForest_Permutation_Top10%_t80**: 16

#### Ridge_Strict_t40

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD8 RO DR_CD8 | 100.0% |
| Bcells CD27posIgDneg_total | 100.0% |
| DR_CD8RO | 100.0% |
| NKCD16_NK | 97.5% |
| NK Ki67_NK | 95.0% |
| NKCD56hi_NK | 95.0% |
| CD14+16+mono_CD3neg | 92.5% |
| Tconv memDR_total | 92.5% |
| CD14+16+mono_myeloid | 92.5% |
| Tconv memCCR4_mem | 92.5% |
| NKCD56hi_total | 92.5% |
| CD8 RO DR_total | 92.5% |
| NK Ki67_nonTnonB | 90.0% |
| NKCD56hi_CD3neg | 90.0% |
| Treg naive_CD4 | 90.0% |
| Tconv memKi67_mem | 87.5% |
| Bcells naive_total | 85.0% |
| CD8 RO DR_CD3 | 85.0% |
| Bcells_total | 85.0% |
| Treg naive_CD3 | 85.0% |
| NK Ki67_CD3neg | 85.0% |
| Bcells memory_CD3neg | 85.0% |
| Tconv memCXCR3_mem | 85.0% |
| Tconv memCXCR3_Tconv | 82.5% |
| Tconv memDR_mem | 82.5% |
| Tconv memCCR5_mem | 80.0% |
| CD27negIgDneg_Bcells | 80.0% |
| Tconv memCCR6_mem | 80.0% |
| Tconv memCD27_CD3 | 80.0% |
| CD14+16+mono_total | 80.0% |
| memory_Bcells | 80.0% |
| Tconv memDR_CD3 | 77.5% |
| Bcells naive_CD3neg | 77.5% |
| Bcells Ki67_total | 77.5% |
| Treg memory_total | 75.0% |
| Tconv memTIGIT_mem | 75.0% |
| CCR6_CD8RO | 75.0% |
| CCR5_CD8RO | 75.0% |
| Tconv memCXCR3_CD3 | 75.0% |
| CD4 Treg_total | 75.0% |
| CD8 RO Ki67_CD8 | 75.0% |
| Tconv memKi67_total | 72.5% |
| Bcells_CD3neg | 72.5% |
| Tconv memDR_Tconv | 72.5% |
| nonTnonB_CD3neg | 72.5% |
| NK Ki67_total | 72.5% |
| CD8 RO TIGIT_CD8 | 72.5% |
| CXCR3_CD8RO | 72.5% |
| CD56_CD8RO | 72.5% |
| naive_Bcells | 72.5% |
| CD8 RO CXCR3_CD8 | 72.5% |
| CCR4_CD8RO | 70.0% |
| CD8 RO CD56_total | 70.0% |
| CD27IgD_Bcells | 70.0% |
| CD8 RO CCR6_CD8 | 70.0% |
| CD8 RO CD56_CD8 | 70.0% |
| CD3hi_CD4neg | 67.5% |
| CD3hi_total | 67.5% |
| NKCD16_nonTnonB | 67.5% |
| CD8 RO CD56_CD3 | 67.5% |
| NKCD16_total | 65.0% |
| Tconv memCD27_mem | 65.0% |
| NKCD16_CD3neg | 65.0% |
| CD8 RO intB7_CD3 | 65.0% |
| Treg memory_CD3 | 65.0% |
| Tconv memCD27_Tconv | 65.0% |
| Bcells memory_total | 65.0% |
| Bcells Ki67_CD3neg | 62.5% |
| intB7_CD8RO | 62.5% |
| myeloid_CD3neg | 62.5% |
| CD4 Treg _CD3 | 62.5% |
| CD8 RA naive_CD3 | 62.5% |
| Tconv memCXCR3_total | 62.5% |
| CD14mono_myeloid | 62.5% |
| Tconv memCCR4_CD3 | 62.5% |
| Tconv memKi67_CD3 | 62.5% |
| Tconv mem_CD3 | 62.5% |
| CD16mono_myeloid | 62.5% |
| Ki67_Bcells | 60.0% |
| Tconv memintB7_mem | 60.0% |
| NK_total | 60.0% |
| Tconv memintB7_Tconv | 60.0% |
| CD8 ncytotox RO CCR4_CD8ntox | 60.0% |
| CD8 RO CCR5_CD8 | 60.0% |
| CD8 RO intB7_CD8 | 60.0% |
| NK_nonTnonB | 57.5% |
| NK_CD3neg | 57.5% |
| CD4neg_total | 57.5% |
| Tconv memCCR6_CD3 | 57.5% |
| NKCD56hi_nonTnonB | 57.5% |
| CD16mono_CD3neg | 55.0% |
| CD16+mono_total | 55.0% |
| Tconv memCCR4_total | 55.0% |
| CD8 RO CXCR3_CD3 | 52.5% |
| CD8 RA_CD3 | 52.5% |
| Tconv naive_Tconv | 50.0% |
| Tconv mem_Tconv | 50.0% |
| Tconv memKi67_Tconv | 50.0% |
| PD1_CD8RO | 50.0% |
| CD8 RO PD1_CD8 | 50.0% |
| Tconv memCCR6_Tconv | 50.0% |
| CD8 RO intB7_total | 50.0% |
| Tconv memCCR4_Tconv | 47.5% |
| Treg naive_total | 47.5% |
| CD8 RA naive_total | 47.5% |
| Bcells CD27negIgDneg_total | 47.5% |
| CD3hi_CD3 | 47.5% |
| CD8 RO CCR5_CD3 | 47.5% |
| CD8 RO_CD8 | 45.0% |
| Tconv memCCR5_total | 45.0% |
| CD27_CD8RO | 45.0% |
| CD4 Treg_CD4 | 42.5% |
| Tconv memintB7_CD3 | 42.5% |
| Ki67_CD8RO | 42.5% |
| CD8 RO CXCR3_total | 42.5% |
| Tconv memCD56_mem | 42.5% |
| Tconv memCCR5_Tconv | 42.5% |
| CD8 RO CCR5_total | 42.5% |
| Treg memory_CD4 | 42.5% |
| Tconv memCD27_total | 42.5% |
| Tconv memCD56_total | 40.0% |
| CD8 RA CCR7 naive_CD8 | 40.0% |
| TIGIT_CD8RO | 40.0% |
| Tconv memTIGIT_total | 37.5% |
| Tconv memCCR5_CD3 | 37.5% |
| Tconv memCD56_CD3 | 37.5% |
| CD8 RA_CD8 | 37.5% |
| CD4 Tconv_CD3 | 37.5% |
| CD8 ncytotox RO CCR4_CD3 | 35.0% |
| CD8 RO Ki67_total | 35.0% |
| CD8 RA_total | 35.0% |
| Tconv memCD56_Tconv | 32.5% |
| CD8 RO CD27_CD8 | 32.5% |
| CD8 RO TIGIT_CD3 | 30.0% |
| CD8 RO CCR6_CD3 | 30.0% |
| Tconv memCCR6_total | 30.0% |
| Tconv memTIGIT_CD3 | 30.0% |
| CD4neg_CD3 | 27.5% |
| Tconv memPD1_mem | 27.5% |
| CD8 RO CCR4_total | 25.0% |
| Tconv memPD1_CD3 | 25.0% |
| Tconv memTIGIT_Tconv | 25.0% |
| CD8 RO CD27_CD3 | 22.5% |
| CD8pos_CD3 | 22.5% |
| CD8 RO CCR6_total | 22.5% |
| CD8  RO Ki67_CD3 | 20.0% |
| Tconv naive_CD3 | 20.0% |
| Tconv memPD1_Tconv | 20.0% |
| CD14mono_CD3neg | 17.5% |
| CD4 Tconv mem_total | 15.0% |
| CD8 RO PD1_CD3 | 12.5% |
| CD8 RO_CD3 | 12.5% |
| Tconv memPD1_total | 10.0% |
| Tconv naive_total | 7.5% |
| CD8 RO TIGIT_total | 7.5% |
| CD8pos_total | 7.5% |
| CD4 Tconv_total | 5.0% |
| CD8 RO CD27_total | 5.0% |
| Tconv memintB7_total | 2.5% |
| CD8 RO_total | 2.5% |
| CD8 RO PD1_total | 2.5% |
| nonTnonB_total | 2.5% |

**Total features selected by Ridge_Strict_t40**: 162

#### Ridge_Strict_t50

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| DR_CD8RO | 97.5% |
| Bcells CD27posIgDneg_total | 97.5% |
| CD8 RO DR_CD8 | 97.5% |
| NKCD16_NK | 95.0% |
| Tconv memDR_total | 92.5% |
| NKCD56hi_NK | 92.5% |
| NKCD56hi_total | 90.0% |
| Tconv memKi67_mem | 85.0% |
| NK Ki67_NK | 85.0% |
| CD8 RO DR_total | 82.5% |
| Treg naive_CD3 | 82.5% |
| CD14+16+mono_CD3neg | 82.5% |
| CD14+16+mono_myeloid | 80.0% |
| Bcells naive_total | 80.0% |
| NK Ki67_nonTnonB | 80.0% |
| Tconv memCCR4_mem | 80.0% |
| CD27negIgDneg_Bcells | 77.5% |
| CD8 RO DR_CD3 | 77.5% |
| Tconv memCXCR3_Tconv | 75.0% |
| NKCD56hi_CD3neg | 75.0% |
| Bcells_total | 75.0% |
| Treg naive_CD4 | 75.0% |
| CD14+16+mono_total | 70.0% |
| Tconv memDR_mem | 70.0% |
| Bcells memory_CD3neg | 70.0% |
| Tconv memDR_CD3 | 67.5% |
| NK Ki67_CD3neg | 67.5% |
| Tconv memCD27_CD3 | 65.0% |
| CCR6_CD8RO | 65.0% |
| Tconv memCCR5_mem | 65.0% |
| Treg memory_total | 65.0% |
| Tconv memCXCR3_mem | 65.0% |
| nonTnonB_CD3neg | 62.5% |
| CCR5_CD8RO | 62.5% |
| CD8 RO CD56_CD8 | 62.5% |
| Tconv memCD27_Tconv | 62.5% |
| Tconv memTIGIT_mem | 62.5% |
| CD56_CD8RO | 60.0% |
| Bcells Ki67_total | 60.0% |
| Bcells memory_total | 60.0% |
| memory_Bcells | 60.0% |
| CD3hi_CD4neg | 60.0% |
| CD4 Treg_total | 60.0% |
| Tconv memKi67_total | 57.5% |
| Tconv memKi67_CD3 | 57.5% |
| Bcells_CD3neg | 57.5% |
| CD8 RO CCR6_CD8 | 57.5% |
| CD8 RO CD56_CD3 | 57.5% |
| Tconv memCCR6_mem | 55.0% |
| Tconv memDR_Tconv | 55.0% |
| CCR4_CD8RO | 55.0% |
| Bcells naive_CD3neg | 55.0% |
| NKCD16_nonTnonB | 55.0% |
| CD8 RO Ki67_CD8 | 55.0% |
| CD8 RO CD56_total | 52.5% |
| Tconv memCXCR3_CD3 | 52.5% |
| Tconv mem_CD3 | 52.5% |
| CD8 RO CXCR3_CD8 | 52.5% |
| CD8 RA naive_CD3 | 52.5% |
| CD8 RO TIGIT_CD8 | 50.0% |
| CXCR3_CD8RO | 50.0% |
| CD3hi_total | 50.0% |
| NK Ki67_total | 50.0% |
| NK_nonTnonB | 47.5% |
| myeloid_CD3neg | 47.5% |
| CD16mono_myeloid | 47.5% |
| CD8 RO intB7_CD8 | 47.5% |
| NKCD16_total | 47.5% |
| CD14mono_myeloid | 47.5% |
| CD27IgD_Bcells | 45.0% |
| Tconv memCCR4_total | 45.0% |
| Treg memory_CD3 | 45.0% |
| NKCD56hi_nonTnonB | 45.0% |
| CD4 Treg _CD3 | 45.0% |
| CD8 RO CXCR3_CD3 | 45.0% |
| naive_Bcells | 45.0% |
| Tconv memCCR6_CD3 | 42.5% |
| Tconv memCD27_mem | 42.5% |
| Tconv memCCR4_CD3 | 42.5% |
| CD8 RO intB7_total | 42.5% |
| CD8 RO intB7_CD3 | 42.5% |
| NKCD16_CD3neg | 42.5% |
| Tconv mem_Tconv | 40.0% |
| Tconv naive_Tconv | 40.0% |
| CD8 ncytotox RO CCR4_CD8ntox | 40.0% |
| CD8 RO PD1_CD8 | 40.0% |
| Tconv memKi67_Tconv | 37.5% |
| Ki67_Bcells | 37.5% |
| CD16+mono_total | 37.5% |
| NK_CD3neg | 37.5% |
| CD8 RA_CD3 | 37.5% |
| NK_total | 37.5% |
| CD8 RA naive_total | 37.5% |
| Tconv memintB7_Tconv | 35.0% |
| CD16mono_CD3neg | 35.0% |
| intB7_CD8RO | 35.0% |
| CD8 RO CCR5_CD8 | 35.0% |
| Tconv memintB7_mem | 35.0% |
| Bcells Ki67_CD3neg | 32.5% |
| CD8 RO CCR5_total | 32.5% |
| CD4neg_total | 32.5% |
| Tconv memCXCR3_total | 32.5% |
| CD8 RO CCR5_CD3 | 32.5% |
| Tconv memCCR5_CD3 | 30.0% |
| Tconv memCCR5_Tconv | 30.0% |
| Tconv memCCR5_total | 27.5% |
| Ki67_CD8RO | 27.5% |
| PD1_CD8RO | 27.5% |
| Tconv memCCR6_Tconv | 27.5% |
| Tconv memCD56_total | 27.5% |
| CD8 RA CCR7 naive_CD8 | 27.5% |
| Treg naive_total | 27.5% |
| CD8 RA_CD8 | 25.0% |
| CD8 ncytotox RO CCR4_CD3 | 25.0% |
| CD27_CD8RO | 25.0% |
| CD4 Tconv_CD3 | 25.0% |
| Tconv memCCR4_Tconv | 25.0% |
| Tconv memCD56_mem | 25.0% |
| CD8 RO CXCR3_total | 25.0% |
| TIGIT_CD8RO | 25.0% |
| Tconv memCD27_total | 22.5% |
| CD8 RO_CD8 | 22.5% |
| Tconv memCD56_Tconv | 22.5% |
| CD8 RA_total | 22.5% |
| CD8 RO Ki67_total | 22.5% |
| Tconv memCD56_CD3 | 22.5% |
| CD4 Treg_CD4 | 22.5% |
| CD3hi_CD3 | 22.5% |
| Treg memory_CD4 | 20.0% |
| Tconv memTIGIT_total | 20.0% |
| Tconv memintB7_CD3 | 20.0% |
| Bcells CD27negIgDneg_total | 20.0% |
| CD8pos_CD3 | 17.5% |
| CD8 RO CCR6_CD3 | 17.5% |
| Tconv memTIGIT_CD3 | 17.5% |
| CD8 RO TIGIT_CD3 | 15.0% |
| Tconv memPD1_CD3 | 15.0% |
| Tconv memPD1_Tconv | 15.0% |
| CD8 RO CCR4_total | 12.5% |
| CD8 RO_CD3 | 12.5% |
| CD8 RO CD27_CD3 | 12.5% |
| CD8 RO CCR6_total | 12.5% |
| CD14mono_CD3neg | 12.5% |
| CD8 RO CD27_CD8 | 12.5% |
| CD4neg_CD3 | 10.0% |
| Tconv memTIGIT_Tconv | 10.0% |
| Tconv naive_CD3 | 10.0% |
| CD4 Tconv mem_total | 10.0% |
| Tconv memPD1_mem | 10.0% |
| Tconv memCCR6_total | 7.5% |
| CD8  RO Ki67_CD3 | 7.5% |
| Tconv memPD1_total | 5.0% |
| CD8 RO PD1_CD3 | 5.0% |
| Tconv naive_total | 5.0% |
| Tconv memintB7_total | 2.5% |
| CD8 RO PD1_total | 2.5% |
| CD8 RO CD27_total | 2.5% |
| CD8 RO TIGIT_total | 2.5% |
| CD8pos_total | 2.5% |

**Total features selected by Ridge_Strict_t50**: 159

#### Ridge_Strict_t60

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Bcells CD27posIgDneg_total | 95.0% |
| CD8 RO DR_CD8 | 95.0% |
| DR_CD8RO | 92.5% |
| NKCD16_NK | 85.0% |
| NK Ki67_NK | 82.5% |
| Tconv memDR_total | 82.5% |
| NKCD56hi_total | 82.5% |
| NKCD56hi_NK | 82.5% |
| CD14+16+mono_CD3neg | 77.5% |
| Tconv memKi67_mem | 77.5% |
| CD8 RO DR_total | 72.5% |
| Bcells naive_total | 70.0% |
| CD14+16+mono_myeloid | 67.5% |
| CD8 RO DR_CD3 | 65.0% |
| NK Ki67_nonTnonB | 65.0% |
| Tconv memCXCR3_Tconv | 62.5% |
| Tconv memDR_CD3 | 62.5% |
| CD14+16+mono_total | 62.5% |
| Tconv memCXCR3_mem | 60.0% |
| CD27negIgDneg_Bcells | 60.0% |
| Bcells_total | 60.0% |
| Tconv memDR_mem | 57.5% |
| NKCD56hi_CD3neg | 55.0% |
| Bcells memory_CD3neg | 55.0% |
| Treg memory_total | 52.5% |
| Tconv memKi67_total | 52.5% |
| Tconv memTIGIT_mem | 52.5% |
| nonTnonB_CD3neg | 52.5% |
| Tconv memCCR5_mem | 52.5% |
| NK Ki67_CD3neg | 52.5% |
| Bcells_CD3neg | 50.0% |
| Treg naive_CD4 | 50.0% |
| CD8 RO CD56_CD3 | 50.0% |
| Tconv memCD27_CD3 | 50.0% |
| CCR5_CD8RO | 47.5% |
| Treg naive_CD3 | 47.5% |
| CD8 RO Ki67_CD8 | 47.5% |
| CD8 RO CD56_total | 47.5% |
| Tconv memKi67_CD3 | 47.5% |
| Tconv memCD27_Tconv | 47.5% |
| CD8 RO CCR6_CD8 | 45.0% |
| CD56_CD8RO | 45.0% |
| Bcells naive_CD3neg | 42.5% |
| NK Ki67_total | 42.5% |
| CD8 RA naive_CD3 | 42.5% |
| CD4 Treg_total | 40.0% |
| CCR6_CD8RO | 40.0% |
| memory_Bcells | 40.0% |
| Tconv memCXCR3_CD3 | 40.0% |
| Bcells memory_total | 40.0% |
| Tconv memCCR6_mem | 40.0% |
| Tconv memCCR4_mem | 40.0% |
| CD8 RO CD56_CD8 | 37.5% |
| CD3hi_CD4neg | 37.5% |
| Bcells Ki67_total | 37.5% |
| CD8 RO PD1_CD8 | 37.5% |
| myeloid_CD3neg | 37.5% |
| CXCR3_CD8RO | 35.0% |
| CD27IgD_Bcells | 35.0% |
| Tconv memDR_Tconv | 35.0% |
| NKCD16_nonTnonB | 35.0% |
| Tconv mem_CD3 | 35.0% |
| NKCD16_CD3neg | 35.0% |
| Tconv memCCR4_total | 35.0% |
| CD14mono_myeloid | 32.5% |
| Tconv memCD27_mem | 32.5% |
| NKCD16_total | 32.5% |
| CD8 RO CXCR3_CD8 | 32.5% |
| naive_Bcells | 32.5% |
| CD3hi_total | 32.5% |
| Ki67_Bcells | 30.0% |
| CD8 RO TIGIT_CD8 | 30.0% |
| CD8 RO CCR5_total | 30.0% |
| Tconv memCCR4_CD3 | 30.0% |
| CD8 RO intB7_CD3 | 30.0% |
| NK_CD3neg | 30.0% |
| CD8 RO CXCR3_CD3 | 30.0% |
| Tconv naive_Tconv | 27.5% |
| CCR4_CD8RO | 27.5% |
| CD8 RO intB7_total | 27.5% |
| CD16mono_myeloid | 27.5% |
| CD4 Treg _CD3 | 27.5% |
| Tconv memCCR6_CD3 | 27.5% |
| CD8 RO CCR5_CD3 | 27.5% |
| CD8 RA_CD3 | 25.0% |
| NK_nonTnonB | 25.0% |
| Tconv memCCR5_Tconv | 25.0% |
| NK_total | 25.0% |
| Tconv memKi67_Tconv | 25.0% |
| PD1_CD8RO | 25.0% |
| CD8 RA naive_total | 25.0% |
| CD8 RO intB7_CD8 | 22.5% |
| CD8 RO CCR5_CD8 | 22.5% |
| Tconv mem_Tconv | 22.5% |
| CD16mono_CD3neg | 22.5% |
| CD16+mono_total | 22.5% |
| Tconv memintB7_mem | 22.5% |
| CD27_CD8RO | 20.0% |
| Tconv memCCR5_CD3 | 20.0% |
| CD8 ncytotox RO CCR4_CD8ntox | 20.0% |
| NKCD56hi_nonTnonB | 20.0% |
| intB7_CD8RO | 20.0% |
| CD4neg_total | 20.0% |
| CD8 RO CXCR3_total | 20.0% |
| Treg memory_CD3 | 20.0% |
| Tconv memintB7_Tconv | 17.5% |
| Tconv memCCR5_total | 17.5% |
| Tconv memCD56_mem | 17.5% |
| CD8 ncytotox RO CCR4_CD3 | 15.0% |
| CD8 RA CCR7 naive_CD8 | 15.0% |
| Tconv memCD27_total | 15.0% |
| Tconv memCD56_total | 15.0% |
| Bcells CD27negIgDneg_total | 15.0% |
| CD4 Tconv_CD3 | 15.0% |
| TIGIT_CD8RO | 15.0% |
| Ki67_CD8RO | 15.0% |
| CD8 RA_CD8 | 12.5% |
| Tconv memTIGIT_total | 12.5% |
| CD8 RO Ki67_total | 12.5% |
| CD3hi_CD3 | 12.5% |
| CD4 Treg_CD4 | 12.5% |
| Tconv memCD56_CD3 | 12.5% |
| CD8 RO CCR6_CD3 | 12.5% |
| Tconv memPD1_Tconv | 12.5% |
| Bcells Ki67_CD3neg | 12.5% |
| CD8pos_CD3 | 12.5% |
| Tconv memCCR6_Tconv | 12.5% |
| CD8 RO CCR4_total | 10.0% |
| Tconv memCD56_Tconv | 10.0% |
| CD8 RA_total | 10.0% |
| Tconv memCCR4_Tconv | 10.0% |
| CD8 RO CD27_CD3 | 10.0% |
| Tconv memPD1_mem | 10.0% |
| Tconv memintB7_CD3 | 10.0% |
| Treg naive_total | 10.0% |
| Tconv memCXCR3_total | 7.5% |
| CD14mono_CD3neg | 7.5% |
| CD4 Tconv mem_total | 7.5% |
| CD8 RO_CD3 | 7.5% |
| CD8 RO TIGIT_CD3 | 7.5% |
| CD8 RO CCR6_total | 7.5% |
| Tconv memPD1_CD3 | 7.5% |
| Treg memory_CD4 | 7.5% |
| CD8 RO_CD8 | 5.0% |
| CD8 RO PD1_CD3 | 5.0% |
| Tconv memCCR6_total | 5.0% |
| Tconv memTIGIT_Tconv | 5.0% |
| Tconv naive_CD3 | 5.0% |
| Tconv naive_total | 2.5% |
| CD8 RO CD27_CD8 | 2.5% |
| CD8 RO CD27_total | 2.5% |
| CD8 RO PD1_total | 2.5% |
| Tconv memTIGIT_CD3 | 2.5% |
| CD8pos_total | 2.5% |

**Total features selected by Ridge_Strict_t60**: 154

#### Ridge_Strict_t70

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Bcells CD27posIgDneg_total | 92.5% |
| CD8 RO DR_CD8 | 87.5% |
| DR_CD8RO | 82.5% |
| NKCD16_NK | 77.5% |
| NKCD56hi_total | 77.5% |
| Tconv memDR_total | 77.5% |
| Tconv memKi67_mem | 72.5% |
| NKCD56hi_NK | 72.5% |
| CD8 RO DR_total | 62.5% |
| CD14+16+mono_CD3neg | 62.5% |
| NK Ki67_NK | 60.0% |
| CD8 RO DR_CD3 | 60.0% |
| Bcells_total | 57.5% |
| Tconv memDR_CD3 | 55.0% |
| CD14+16+mono_myeloid | 55.0% |
| NK Ki67_nonTnonB | 52.5% |
| CD27negIgDneg_Bcells | 47.5% |
| Tconv memCXCR3_mem | 47.5% |
| CD14+16+mono_total | 47.5% |
| NK Ki67_CD3neg | 47.5% |
| NKCD56hi_CD3neg | 45.0% |
| Tconv memDR_mem | 45.0% |
| Bcells memory_CD3neg | 45.0% |
| Tconv memCXCR3_Tconv | 45.0% |
| Bcells naive_total | 45.0% |
| Bcells_CD3neg | 42.5% |
| Tconv memKi67_total | 40.0% |
| Tconv memCCR5_mem | 40.0% |
| nonTnonB_CD3neg | 40.0% |
| Bcells naive_CD3neg | 37.5% |
| CD8 RA naive_CD3 | 35.0% |
| CCR5_CD8RO | 32.5% |
| CD8 RO CD56_total | 32.5% |
| Treg memory_total | 32.5% |
| Tconv memCD27_CD3 | 32.5% |
| CD8 RO CD56_CD3 | 32.5% |
| NK Ki67_total | 32.5% |
| Tconv memDR_Tconv | 30.0% |
| CD8 RO PD1_CD8 | 30.0% |
| Treg naive_CD4 | 30.0% |
| Tconv memTIGIT_mem | 30.0% |
| CD27IgD_Bcells | 30.0% |
| Tconv mem_CD3 | 27.5% |
| Tconv memCXCR3_CD3 | 27.5% |
| Bcells memory_total | 27.5% |
| myeloid_CD3neg | 27.5% |
| Treg naive_CD3 | 27.5% |
| Tconv memKi67_CD3 | 27.5% |
| CD3hi_total | 27.5% |
| CD8 RO Ki67_CD8 | 27.5% |
| NKCD16_nonTnonB | 25.0% |
| NK_nonTnonB | 25.0% |
| CCR6_CD8RO | 25.0% |
| CD4 Treg_total | 25.0% |
| CD8 RO CCR6_CD8 | 25.0% |
| CD8 RO CCR5_CD3 | 25.0% |
| CD8 RO CCR5_total | 25.0% |
| Tconv memCCR4_mem | 22.5% |
| CXCR3_CD8RO | 22.5% |
| Bcells Ki67_total | 22.5% |
| Tconv memCCR5_Tconv | 22.5% |
| Tconv memCD27_mem | 22.5% |
| NKCD16_total | 22.5% |
| CD16mono_myeloid | 22.5% |
| CD8 RO CD56_CD8 | 22.5% |
| Tconv memCCR6_mem | 22.5% |
| CD8 RO CXCR3_CD3 | 22.5% |
| CD14mono_myeloid | 20.0% |
| CD56_CD8RO | 20.0% |
| CD8 RA_CD3 | 20.0% |
| CCR4_CD8RO | 20.0% |
| naive_Bcells | 20.0% |
| Ki67_Bcells | 17.5% |
| Tconv memKi67_Tconv | 17.5% |
| Tconv memCD27_Tconv | 17.5% |
| NK_total | 17.5% |
| CD8 RA naive_total | 17.5% |
| CD8 RO intB7_CD3 | 17.5% |
| CD8 ncytotox RO CCR4_CD8ntox | 17.5% |
| NKCD16_CD3neg | 17.5% |
| CD3hi_CD4neg | 17.5% |
| NKCD56hi_nonTnonB | 15.0% |
| PD1_CD8RO | 15.0% |
| CD8 RO CXCR3_CD8 | 15.0% |
| Tconv naive_Tconv | 12.5% |
| Tconv memCCR4_total | 12.5% |
| CD8 RO intB7_total | 12.5% |
| NK_CD3neg | 12.5% |
| Tconv memCD27_total | 12.5% |
| CD8 RO CCR5_CD8 | 12.5% |
| Tconv memCCR5_total | 12.5% |
| Tconv memCCR4_CD3 | 12.5% |
| Tconv memintB7_mem | 12.5% |
| Bcells CD27negIgDneg_total | 12.5% |
| CD4 Treg _CD3 | 12.5% |
| CD16mono_CD3neg | 10.0% |
| Treg memory_CD3 | 10.0% |
| intB7_CD8RO | 10.0% |
| Tconv memCD56_mem | 10.0% |
| Tconv memCD56_CD3 | 10.0% |
| CD4neg_total | 10.0% |
| Tconv memCCR5_CD3 | 10.0% |
| Tconv mem_Tconv | 10.0% |
| Bcells Ki67_CD3neg | 10.0% |
| CD8 RO TIGIT_CD8 | 10.0% |
| memory_Bcells | 10.0% |
| Tconv memCCR6_Tconv | 10.0% |
| CD8 RA CCR7 naive_CD8 | 10.0% |
| Tconv memintB7_Tconv | 10.0% |
| CD8 RO CXCR3_total | 7.5% |
| CD14mono_CD3neg | 7.5% |
| CD4 Tconv_CD3 | 7.5% |
| Tconv memintB7_CD3 | 7.5% |
| Tconv memCD56_Tconv | 7.5% |
| CD8 RO intB7_CD8 | 7.5% |
| Ki67_CD8RO | 7.5% |
| CD8 RO Ki67_total | 7.5% |
| CD8 ncytotox RO CCR4_CD3 | 7.5% |
| CD8pos_CD3 | 7.5% |
| CD27_CD8RO | 7.5% |
| CD8 RO CCR6_CD3 | 7.5% |
| Tconv memCCR6_CD3 | 7.5% |
| CD8 RO CCR4_total | 5.0% |
| CD4 Tconv mem_total | 5.0% |
| Treg naive_total | 5.0% |
| Tconv memPD1_CD3 | 5.0% |
| CD8 RO CD27_CD3 | 5.0% |
| CD8 RA_total | 5.0% |
| Tconv memPD1_mem | 5.0% |
| Tconv memCCR4_Tconv | 5.0% |
| Tconv memCD56_total | 5.0% |
| Tconv naive_CD3 | 5.0% |
| CD3hi_CD3 | 5.0% |
| CD16+mono_total | 2.5% |
| Tconv memCCR6_total | 2.5% |
| Treg memory_CD4 | 2.5% |
| CD8 RO CD27_CD8 | 2.5% |
| CD8 RO PD1_CD3 | 2.5% |
| TIGIT_CD8RO | 2.5% |
| CD8 RO_CD8 | 2.5% |
| CD8 RA_CD8 | 2.5% |
| CD8 RO_CD3 | 2.5% |
| CD8 RO TIGIT_CD3 | 2.5% |
| CD8 RO PD1_total | 2.5% |
| Tconv memTIGIT_CD3 | 2.5% |
| Tconv memTIGIT_Tconv | 2.5% |
| Tconv memCXCR3_total | 2.5% |
| Tconv memPD1_Tconv | 2.5% |
| CD4 Treg_CD4 | 2.5% |

**Total features selected by Ridge_Strict_t70**: 149

#### Ridge_Strict_t80

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Bcells CD27posIgDneg_total | 80.0% |
| CD8 RO DR_CD8 | 80.0% |
| DR_CD8RO | 75.0% |
| Tconv memDR_total | 70.0% |
| NKCD16_NK | 62.5% |
| NKCD56hi_total | 60.0% |
| CD8 RO DR_total | 55.0% |
| NKCD56hi_NK | 52.5% |
| Tconv memKi67_mem | 52.5% |
| CD14+16+mono_CD3neg | 50.0% |
| CD8 RO DR_CD3 | 47.5% |
| NK Ki67_nonTnonB | 42.5% |
| Tconv memDR_mem | 37.5% |
| CD14+16+mono_myeloid | 37.5% |
| Bcells_CD3neg | 37.5% |
| CD27negIgDneg_Bcells | 37.5% |
| nonTnonB_CD3neg | 37.5% |
| NK Ki67_NK | 35.0% |
| CD14+16+mono_total | 35.0% |
| Bcells_total | 35.0% |
| Bcells naive_total | 35.0% |
| NKCD56hi_CD3neg | 32.5% |
| Tconv memCCR5_mem | 32.5% |
| Tconv memDR_CD3 | 32.5% |
| NK Ki67_CD3neg | 32.5% |
| Tconv memCXCR3_Tconv | 30.0% |
| Bcells memory_CD3neg | 27.5% |
| Tconv memCXCR3_mem | 27.5% |
| Bcells naive_CD3neg | 27.5% |
| NK Ki67_total | 25.0% |
| CD8 RO CCR6_CD8 | 25.0% |
| CD8 RO CCR5_CD3 | 22.5% |
| CD8 RO CCR5_total | 22.5% |
| CD27IgD_Bcells | 22.5% |
| CD8 RO CD56_total | 20.0% |
| Tconv memKi67_CD3 | 20.0% |
| Tconv memKi67_total | 20.0% |
| Tconv memDR_Tconv | 20.0% |
| NKCD16_nonTnonB | 20.0% |
| Bcells memory_total | 20.0% |
| CCR5_CD8RO | 20.0% |
| Tconv memCD27_CD3 | 17.5% |
| CD8 RO CD56_CD3 | 17.5% |
| Treg memory_total | 17.5% |
| CD8 RA naive_CD3 | 17.5% |
| CD3hi_total | 17.5% |
| Tconv memCD27_mem | 15.0% |
| Tconv memTIGIT_mem | 15.0% |
| NK_nonTnonB | 15.0% |
| Tconv memCXCR3_CD3 | 15.0% |
| Tconv memCCR5_Tconv | 15.0% |
| CD8 RO CD56_CD8 | 15.0% |
| myeloid_CD3neg | 15.0% |
| CD8 RA_CD3 | 15.0% |
| NK_total | 15.0% |
| CD8 RO intB7_CD3 | 15.0% |
| CD16mono_myeloid | 15.0% |
| CD8 RO PD1_CD8 | 15.0% |
| CD8 RO Ki67_CD8 | 15.0% |
| CCR6_CD8RO | 15.0% |
| NKCD16_total | 15.0% |
| naive_Bcells | 12.5% |
| CD8 RA naive_total | 12.5% |
| CD3hi_CD4neg | 12.5% |
| Tconv mem_CD3 | 12.5% |
| Tconv memKi67_Tconv | 10.0% |
| NKCD16_CD3neg | 10.0% |
| Treg naive_CD3 | 10.0% |
| CD8 RO intB7_total | 10.0% |
| CD8 ncytotox RO CCR4_CD8ntox | 10.0% |
| NKCD56hi_nonTnonB | 10.0% |
| Treg naive_CD4 | 10.0% |
| CCR4_CD8RO | 10.0% |
| CXCR3_CD8RO | 10.0% |
| Tconv memCCR6_mem | 10.0% |
| memory_Bcells | 10.0% |
| CD4 Treg_total | 10.0% |
| NK_CD3neg | 10.0% |
| CD56_CD8RO | 10.0% |
| CD14mono_myeloid | 10.0% |
| Bcells Ki67_total | 10.0% |
| Tconv memCCR4_mem | 7.5% |
| Tconv memCD56_mem | 7.5% |
| intB7_CD8RO | 7.5% |
| Bcells CD27negIgDneg_total | 7.5% |
| Tconv memCCR4_total | 7.5% |
| CD8pos_CD3 | 7.5% |
| Tconv mem_Tconv | 7.5% |
| Tconv memintB7_mem | 7.5% |
| CD8 RO CXCR3_CD3 | 7.5% |
| Tconv memCCR5_total | 7.5% |
| PD1_CD8RO | 7.5% |
| Tconv memCD27_total | 7.5% |
| CD8 RO TIGIT_CD8 | 7.5% |
| Tconv memCCR6_CD3 | 7.5% |
| Tconv memPD1_CD3 | 5.0% |
| CD8 RO CD27_CD3 | 5.0% |
| Tconv memCD56_Tconv | 5.0% |
| CD8 RO intB7_CD8 | 5.0% |
| CD14mono_CD3neg | 5.0% |
| CD8 RA CCR7 naive_CD8 | 5.0% |
| Tconv memCCR6_Tconv | 5.0% |
| Tconv naive_Tconv | 5.0% |
| CD4 Treg _CD3 | 5.0% |
| Bcells Ki67_CD3neg | 5.0% |
| CD8 RA_total | 5.0% |
| Treg naive_total | 5.0% |
| CD8 RO CXCR3_CD8 | 5.0% |
| Ki67_Bcells | 5.0% |
| CD4 Tconv_CD3 | 5.0% |
| CD3hi_CD3 | 5.0% |
| Treg memory_CD3 | 5.0% |
| CD16mono_CD3neg | 2.5% |
| CD16+mono_total | 2.5% |
| Tconv memintB7_CD3 | 2.5% |
| Tconv memCCR6_total | 2.5% |
| Tconv memCD27_Tconv | 2.5% |
| CD8 ncytotox RO CCR4_CD3 | 2.5% |
| CD8 RO CCR5_CD8 | 2.5% |
| CD8 RA_CD8 | 2.5% |
| Tconv memCD56_CD3 | 2.5% |
| CD8 RO PD1_CD3 | 2.5% |
| Treg memory_CD4 | 2.5% |
| Tconv naive_CD3 | 2.5% |
| Tconv memCCR5_CD3 | 2.5% |
| CD8 RO TIGIT_CD3 | 2.5% |
| CD4neg_total | 2.5% |
| CD8 RO CXCR3_total | 2.5% |
| CD8 RO PD1_total | 2.5% |
| CD8 RO CCR6_CD3 | 2.5% |
| Tconv memTIGIT_CD3 | 2.5% |
| CD8 RO Ki67_total | 2.5% |
| Tconv memintB7_Tconv | 2.5% |

**Total features selected by Ridge_Strict_t80**: 133

#### SVM_RBF_Permutation_Top10%_t40

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

**Total features selected by SVM_RBF_Permutation_Top10%_t40**: 16

#### SVM_RBF_Permutation_Top10%_t50

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

**Total features selected by SVM_RBF_Permutation_Top10%_t50**: 16

#### SVM_RBF_Permutation_Top10%_t60

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

**Total features selected by SVM_RBF_Permutation_Top10%_t60**: 16

#### SVM_RBF_Permutation_Top10%_t70

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

**Total features selected by SVM_RBF_Permutation_Top10%_t70**: 16

#### SVM_RBF_Permutation_Top10%_t80

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

**Total features selected by SVM_RBF_Permutation_Top10%_t80**: 16

#### XGB_Importance_t40

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Tconv memDR_CD3 | 56.4% |
| CD8 RO CCR5_total | 43.6% |
| Tconv memDR_total | 30.8% |
| CD8 RO CCR5_CD3 | 28.2% |
| CD8 RO DR_CD3 | 23.1% |
| Bcells CD27posIgDneg_total | 17.9% |
| CD27negIgDneg_Bcells | 15.4% |
| CD16mono_myeloid | 10.3% |
| Tconv memCCR5_mem | 10.3% |
| Treg naive_CD4 | 7.7% |
| NKCD16_NK | 7.7% |
| CD14+16+mono_CD3neg | 7.7% |
| CD3pos_total | 5.1% |
| Ki67_Bcells | 5.1% |
| NKCD56hi_total | 5.1% |
| CD8 RA_total | 5.1% |
| CD8 RO intB7_CD3 | 5.1% |
| CD8pos_total | 5.1% |
| NK Ki67_total | 5.1% |
| Tconv memDR_Tconv | 5.1% |
| CD4 Tconv mem_total | 5.1% |
| myeloid_CD3neg | 5.1% |
| CD8 RO CXCR3_CD3 | 5.1% |
| CD8 RA CCR7 naive_CD8 | 2.6% |
| CD8 RA naive_CD3 | 2.6% |
| NK_total | 2.6% |
| CD8 RO TIGIT_CD3 | 2.6% |
| Tconv memCCR6_mem | 2.6% |
| CD8 RO CCR4_total | 2.6% |
| CD14mono_myeloid | 2.6% |
| CD8 RO CD27_CD3 | 2.6% |
| Bcells naive_total | 2.6% |
| Tconv memDR_mem | 2.6% |
| Bcells memory_total | 2.6% |
| CD8 RO CD56_CD8 | 2.6% |
| CD14+16+mono_total | 2.6% |
| Tconv memCD27_CD3 | 2.6% |
| Tconv memKi67_total | 2.6% |
| Tconv memCCR5_total | 2.6% |

**Total features selected by XGB_Importance_t40**: 39

#### XGB_Importance_t50

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Tconv memDR_CD3 | 33.3% |
| CD8 RO CCR5_total | 27.3% |
| CD27negIgDneg_Bcells | 18.2% |
| Tconv memDR_total | 15.2% |
| Bcells CD27posIgDneg_total | 15.2% |
| CD8 RO CCR5_CD3 | 12.1% |
| CD8 RO DR_CD3 | 9.1% |
| Tconv memCCR5_mem | 6.1% |
| CD3pos_total | 6.1% |
| CD8 RA CCR7 naive_CD8 | 3.0% |
| CD8 RO CCR4_total | 3.0% |
| CD8 RO CD27_CD3 | 3.0% |
| CD4 Tconv mem_total | 3.0% |
| CD14mono_myeloid | 3.0% |
| CD8 RO intB7_CD3 | 3.0% |
| Bcells naive_total | 3.0% |
| CD8 RA_total | 3.0% |
| Tconv memDR_Tconv | 3.0% |
| CD14+16+mono_total | 3.0% |
| CD8 RO CXCR3_CD3 | 3.0% |
| myeloid_CD3neg | 3.0% |
| NKCD16_NK | 3.0% |

**Total features selected by XGB_Importance_t50**: 22

#### XGB_Importance_t60

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Tconv memDR_CD3 | 30.0% |
| CD8 RO CCR5_total | 25.0% |
| Tconv memDR_total | 15.0% |
| CD27negIgDneg_Bcells | 10.0% |
| Bcells CD27posIgDneg_total | 10.0% |
| CD8 RA CCR7 naive_CD8 | 5.0% |
| Tconv memCCR5_mem | 5.0% |
| CD8 RO CD27_CD3 | 5.0% |
| CD8 RO CCR4_total | 5.0% |
| CD8 RO DR_CD3 | 5.0% |
| CD8 RO CCR5_CD3 | 5.0% |

**Total features selected by XGB_Importance_t60**: 11

#### XGB_Importance_t70

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Tconv memDR_CD3 | 27.3% |
| Tconv memDR_total | 18.2% |
| Bcells CD27posIgDneg_total | 18.2% |
| CD8 RO CCR4_total | 9.1% |
| CD8 RO DR_CD3 | 9.1% |
| CD8 RO CCR5_CD3 | 9.1% |
| CD8 RO CCR5_total | 9.1% |

**Total features selected by XGB_Importance_t70**: 7

#### XGB_Importance_t80

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Tconv memDR_CD3 | 40.0% |
| Bcells CD27posIgDneg_total | 40.0% |
| CD8 RO CCR5_total | 20.0% |

**Total features selected by XGB_Importance_t80**: 3

#### XGBoost_Permutation_AboveMean_t40

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Tconv memDR_CD3 | 31.2% |
| Bcells CD27posIgDneg_total | 25.0% |
| CD8 RO CCR5_total | 6.2% |
| CD8 RO DR_CD3 | 6.2% |
| Bcells naive_total | 6.2% |
| CD27negIgDneg_Bcells | 6.2% |
| Treg naive_CD4 | 6.2% |
| Tconv memDR_total | 6.2% |
| myeloid_CD3neg | 6.2% |
| CD8 RO CCR5_CD3 | 6.2% |

**Total features selected by XGBoost_Permutation_AboveMean_t40**: 10

#### XGBoost_Permutation_AboveMean_t50

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Bcells CD27posIgDneg_total | 50.0% |
| Tconv memDR_CD3 | 33.3% |
| CD8 RO DR_CD3 | 16.7% |

**Total features selected by XGBoost_Permutation_AboveMean_t50**: 3

#### XGBoost_Permutation_AboveMean_t60

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Tconv memDR_CD3 | 66.7% |
| Bcells CD27posIgDneg_total | 33.3% |

**Total features selected by XGBoost_Permutation_AboveMean_t60**: 2

#### XGBoost_Permutation_AboveMean_t70

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Tconv memDR_CD3 | 50.0% |
| Bcells CD27posIgDneg_total | 50.0% |

**Total features selected by XGBoost_Permutation_AboveMean_t70**: 2

#### XGBoost_Permutation_AboveMean_t80

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Bcells CD27posIgDneg_total | 100.0% |

**Total features selected by XGBoost_Permutation_AboveMean_t80**: 1

#### XGBoost_Permutation_Top10%_t40

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD3pos_total | 100.0% |
| CD4 Tconv_total | 100.0% |
| CD4 Tconv mem_total | 100.0% |
| Tconv memCCR4_total | 100.0% |
| Tconv memCCR5_total | 100.0% |
| Tconv memCD27_total | 100.0% |
| Tconv memCD56_total | 100.0% |
| Tconv memCXCR3_total | 100.0% |
| Tconv memDR_total | 100.0% |
| Tconv memTIGIT_total | 100.0% |
| Tconv memintB7_total | 100.0% |
| Tconv memKi67_total | 100.0% |
| Tconv memPD1_total | 100.0% |
| CD4 Treg_total | 100.0% |
| Tconv naive_total | 100.0% |
| Tconv memCCR6_total | 57.5% |
| Tconv memDR_CD3 | 12.5% |
| Bcells CD27posIgDneg_total | 10.0% |
| CD8 RO CCR5_total | 2.5% |
| CD8 RO DR_CD3 | 2.5% |
| Bcells naive_total | 2.5% |
| CD27negIgDneg_Bcells | 2.5% |
| Treg naive_CD4 | 2.5% |
| myeloid_CD3neg | 2.5% |
| CD8 RO CCR5_CD3 | 2.5% |

**Total features selected by XGBoost_Permutation_Top10%_t40**: 25

#### XGBoost_Permutation_Top10%_t50

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD3pos_total | 100.0% |
| CD4 Tconv_total | 100.0% |
| CD4 Tconv mem_total | 100.0% |
| Tconv memCCR4_total | 100.0% |
| Tconv memCD27_total | 100.0% |
| Tconv memCXCR3_total | 100.0% |
| Tconv memCD56_total | 100.0% |
| Tconv memDR_total | 100.0% |
| Tconv memintB7_total | 100.0% |
| Tconv memPD1_total | 100.0% |
| Tconv memKi67_total | 100.0% |
| CD4 Treg_total | 100.0% |
| Tconv naive_total | 100.0% |
| Tconv memTIGIT_total | 100.0% |
| Tconv memCCR5_total | 97.5% |
| Tconv memCCR6_total | 40.0% |
| Bcells CD27posIgDneg_total | 7.5% |
| Tconv memDR_CD3 | 5.0% |
| CD8 RO DR_CD3 | 2.5% |

**Total features selected by XGBoost_Permutation_Top10%_t50**: 19

#### XGBoost_Permutation_Top10%_t60

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD3pos_total | 100.0% |
| CD4 Tconv mem_total | 100.0% |
| CD4 Treg_total | 100.0% |
| Tconv memCCR4_total | 100.0% |
| Tconv memCD27_total | 100.0% |
| Tconv memCD56_total | 100.0% |
| Tconv memDR_total | 100.0% |
| Tconv memCXCR3_total | 100.0% |
| Tconv memintB7_total | 100.0% |
| Tconv memKi67_total | 100.0% |
| Tconv memTIGIT_total | 100.0% |
| Tconv memPD1_total | 100.0% |
| Tconv naive_total | 100.0% |
| CD4 Tconv_total | 97.5% |
| Tconv memCCR5_total | 97.5% |
| Tconv memCCR6_total | 17.5% |
| Tconv memDR_CD3 | 5.0% |
| Bcells CD27posIgDneg_total | 2.5% |

**Total features selected by XGBoost_Permutation_Top10%_t60**: 18

#### XGBoost_Permutation_Top10%_t70

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD3pos_total | 100.0% |
| CD4 Tconv mem_total | 100.0% |
| Tconv naive_total | 100.0% |
| Tconv memCD27_total | 100.0% |
| Tconv memCXCR3_total | 100.0% |
| Tconv memCD56_total | 100.0% |
| Tconv memDR_total | 100.0% |
| Tconv memintB7_total | 100.0% |
| Tconv memPD1_total | 100.0% |
| Tconv memKi67_total | 100.0% |
| CD4 Treg_total | 97.5% |
| Tconv memCCR4_total | 97.5% |
| Tconv memTIGIT_total | 95.0% |
| CD4 Tconv_total | 92.5% |
| Tconv memCCR5_total | 87.5% |
| Tconv memDR_CD3 | 2.5% |
| Bcells CD27posIgDneg_total | 2.5% |
| Tconv memCCR6_total | 2.5% |

**Total features selected by XGBoost_Permutation_Top10%_t70**: 18

#### XGBoost_Permutation_Top10%_t80

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD3pos_total | 100.0% |
| CD4 Tconv mem_total | 100.0% |
| Tconv memCD56_total | 100.0% |
| Tconv memCD27_total | 100.0% |
| Tconv memCXCR3_total | 100.0% |
| Tconv memKi67_total | 100.0% |
| Tconv memintB7_total | 100.0% |
| Tconv memDR_total | 100.0% |
| Tconv naive_total | 100.0% |
| Tconv memPD1_total | 100.0% |
| Tconv memCCR4_total | 97.5% |
| CD4 Treg_total | 90.0% |
| Tconv memTIGIT_total | 72.5% |
| CD4 Tconv_total | 65.0% |
| Tconv memCCR5_total | 37.5% |
| Bcells CD27posIgDneg_total | 2.5% |

**Total features selected by XGBoost_Permutation_Top10%_t80**: 16

#### mRMR (Top 10%)_t40

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Bcells CD27posIgDneg_total | 72.5% |
| Tconv memDR_CD3 | 62.5% |
| CD8 RO DR_CD8 | 62.5% |
| Tconv memDR_mem | 55.0% |
| Tconv memDR_Tconv | 52.5% |
| Tconv memDR_total | 50.0% |
| CD14+16+mono_CD3neg | 50.0% |
| myeloid_CD3neg | 50.0% |
| CD14+16+mono_total | 45.0% |
| DR_CD8RO | 40.0% |
| Tconv memCCR5_mem | 37.5% |
| Bcells_total | 35.0% |
| CD8 RA naive_CD3 | 35.0% |
| CD8 RO DR_CD3 | 30.0% |
| nonTnonB_CD3neg | 30.0% |
| Bcells_CD3neg | 30.0% |
| NKCD16_NK | 30.0% |
| CD8 RO CCR5_total | 30.0% |
| NKCD16_nonTnonB | 30.0% |
| CD8 RO CCR5_CD3 | 27.5% |
| Bcells naive_CD3neg | 27.5% |
| CD27negIgDneg_Bcells | 25.0% |
| Bcells naive_total | 22.5% |
| CD8 RA naive_total | 20.0% |
| CD8 RA CCR7 naive_CD8 | 17.5% |
| NK Ki67_nonTnonB | 17.5% |
| CCR5_CD8RO | 17.5% |
| NKCD56hi_NK | 15.0% |
| NK_nonTnonB | 15.0% |
| Tconv memCD27_CD3 | 15.0% |
| CD14+16+mono_myeloid | 15.0% |
| Treg naive_CD4 | 15.0% |
| NK Ki67_NK | 15.0% |
| Treg memory_CD3 | 12.5% |
| CD8 RA_total | 12.5% |
| CD8 RA_CD3 | 12.5% |
| Tconv naive_Tconv | 10.0% |
| CD8pos_total | 10.0% |
| Tconv memCD27_Tconv | 10.0% |
| CD8 RO Ki67_total | 10.0% |
| naive_Bcells | 7.5% |
| CD56_CD8RO | 7.5% |
| Bcells memory_CD3neg | 7.5% |
| Bcells memory_total | 7.5% |
| CD8 RO CXCR3_CD3 | 7.5% |
| Tconv mem_Tconv | 7.5% |
| Tconv memCCR6_mem | 7.5% |
| Tconv memTIGIT_mem | 7.5% |
| CD8 RO CD56_CD8 | 7.5% |
| NK_total | 5.0% |
| NKCD56hi_total | 5.0% |
| myeloid_total | 5.0% |
| Tconv mem_CD3 | 5.0% |
| CD16mono_myeloid | 5.0% |
| CD14mono_CD3neg | 5.0% |
| CD27IgD_Bcells | 5.0% |
| NKCD16_CD3neg | 5.0% |
| Tconv naive_CD3 | 5.0% |
| CD4neg_total | 5.0% |
| NK Ki67_total | 5.0% |
| Tconv memCCR5_Tconv | 5.0% |
| Ki67_Bcells | 2.5% |
| Tconv memKi67_total | 2.5% |
| CD8 RO CCR6_CD8 | 2.5% |
| CD8 RA_CD8 | 2.5% |
| intB7_CD8RO | 2.5% |
| NKCD16_total | 2.5% |
| CD8 RO CD27_CD3 | 2.5% |
| CD3hi_CD4neg | 2.5% |
| CD14mono_myeloid | 2.5% |
| Tconv memCXCR3_mem | 2.5% |
| CD8pos_CD3 | 2.5% |
| Tconv memCCR5_CD3 | 2.5% |
| Tconv memCCR4_mem | 2.5% |
| CD8 RO Ki67_CD8 | 2.5% |
| nonTnonB_total | 2.5% |
| Treg naive_CD3 | 2.5% |
| CD8 RO CCR6_CD3 | 2.5% |
| CXCR3_CD8RO | 2.5% |
| CD3neg_total | 2.5% |
| CD4 Treg _CD3 | 2.5% |
| CD8 RO CCR5_CD8 | 2.5% |
| NK Ki67_CD3neg | 2.5% |

**Total features selected by mRMR (Top 10%)_t40**: 83

#### mRMR (Top 10%)_t50

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Bcells CD27posIgDneg_total | 67.5% |
| CD8 RO DR_CD8 | 50.0% |
| Tconv memDR_CD3 | 45.0% |
| Tconv memDR_total | 42.5% |
| Tconv memDR_mem | 40.0% |
| myeloid_CD3neg | 37.5% |
| DR_CD8RO | 30.0% |
| CD14+16+mono_CD3neg | 30.0% |
| Bcells_total | 27.5% |
| Tconv memCCR5_mem | 27.5% |
| Tconv memDR_Tconv | 25.0% |
| nonTnonB_CD3neg | 22.5% |
| CD8 RO DR_CD3 | 22.5% |
| CD14+16+mono_total | 22.5% |
| NKCD16_nonTnonB | 20.0% |
| CD8 RO CCR5_CD3 | 20.0% |
| CD27negIgDneg_Bcells | 20.0% |
| CD8 RA naive_CD3 | 20.0% |
| Bcells_CD3neg | 20.0% |
| CD8 RA naive_total | 17.5% |
| NKCD16_NK | 17.5% |
| CD8 RO CCR5_total | 15.0% |
| Bcells naive_total | 12.5% |
| NK_nonTnonB | 10.0% |
| NKCD56hi_NK | 10.0% |
| CCR5_CD8RO | 10.0% |
| Bcells naive_CD3neg | 10.0% |
| CD14+16+mono_myeloid | 7.5% |
| NK Ki67_nonTnonB | 7.5% |
| CD8 RA CCR7 naive_CD8 | 7.5% |
| CD8 RA_CD3 | 5.0% |
| Tconv memCCR6_mem | 5.0% |
| CD27IgD_Bcells | 5.0% |
| NK Ki67_NK | 5.0% |
| Tconv memCD27_CD3 | 5.0% |
| Tconv mem_Tconv | 5.0% |
| NKCD16_total | 2.5% |
| Tconv memKi67_total | 2.5% |
| CD8 RO Ki67_total | 2.5% |
| Tconv naive_Tconv | 2.5% |
| CD56_CD8RO | 2.5% |
| CD8 RO CD27_CD3 | 2.5% |
| Tconv memCCR5_Tconv | 2.5% |
| CD3hi_CD4neg | 2.5% |
| Tconv memCCR5_CD3 | 2.5% |
| naive_Bcells | 2.5% |
| CD8 RO CXCR3_CD3 | 2.5% |
| CD8pos_CD3 | 2.5% |
| Treg naive_CD4 | 2.5% |
| Treg naive_CD3 | 2.5% |
| CD8 RA_total | 2.5% |
| nonTnonB_total | 2.5% |
| NKCD16_CD3neg | 2.5% |
| CD4neg_total | 2.5% |
| CD8pos_total | 2.5% |
| myeloid_total | 2.5% |
| Treg memory_CD3 | 2.5% |
| Bcells memory_CD3neg | 2.5% |
| CD16mono_myeloid | 2.5% |
| NK Ki67_total | 2.5% |

**Total features selected by mRMR (Top 10%)_t50**: 60

#### mRMR (Top 10%)_t60

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Bcells CD27posIgDneg_total | 47.5% |
| Tconv memDR_CD3 | 40.0% |
| Tconv memDR_mem | 37.5% |
| CD8 RO DR_CD8 | 37.5% |
| Tconv memDR_total | 27.5% |
| myeloid_CD3neg | 27.5% |
| CD14+16+mono_CD3neg | 25.0% |
| Tconv memCCR5_mem | 22.5% |
| Tconv memDR_Tconv | 20.0% |
| nonTnonB_CD3neg | 17.5% |
| DR_CD8RO | 17.5% |
| CD8 RO CCR5_CD3 | 17.5% |
| CD14+16+mono_total | 15.0% |
| Bcells_total | 15.0% |
| CD8 RO CCR5_total | 12.5% |
| CD8 RO DR_CD3 | 12.5% |
| NKCD16_NK | 12.5% |
| NKCD16_nonTnonB | 12.5% |
| Bcells naive_total | 10.0% |
| CD8 RA naive_CD3 | 10.0% |
| Bcells_CD3neg | 10.0% |
| NKCD56hi_NK | 7.5% |
| CD14+16+mono_myeloid | 7.5% |
| CD27negIgDneg_Bcells | 7.5% |
| CD8 RA naive_total | 5.0% |
| Bcells naive_CD3neg | 2.5% |
| CD27IgD_Bcells | 2.5% |
| NK Ki67_NK | 2.5% |
| Tconv memCCR5_CD3 | 2.5% |
| Tconv mem_Tconv | 2.5% |
| CD3hi_CD4neg | 2.5% |
| CD56_CD8RO | 2.5% |
| CD8 RO CXCR3_CD3 | 2.5% |
| NK Ki67_nonTnonB | 2.5% |
| Treg naive_CD4 | 2.5% |
| CD8 RA_CD3 | 2.5% |
| CD8 RA_total | 2.5% |
| NK_nonTnonB | 2.5% |
| Treg memory_CD3 | 2.5% |
| CCR5_CD8RO | 2.5% |

**Total features selected by mRMR (Top 10%)_t60**: 40

#### mRMR (Top 10%)_t70

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Tconv memDR_CD3 | 35.3% |
| CD8 RO DR_CD8 | 32.4% |
| Bcells CD27posIgDneg_total | 29.4% |
| Tconv memDR_mem | 23.5% |
| Tconv memDR_total | 17.6% |
| CD14+16+mono_CD3neg | 17.6% |
| myeloid_CD3neg | 17.6% |
| Tconv memDR_Tconv | 14.7% |
| DR_CD8RO | 14.7% |
| Tconv memCCR5_mem | 14.7% |
| CD14+16+mono_total | 14.7% |
| CD8 RO DR_CD3 | 11.8% |
| CD8 RO CCR5_CD3 | 11.8% |
| CD8 RO CCR5_total | 8.8% |
| Bcells_total | 8.8% |
| nonTnonB_CD3neg | 8.8% |
| CD8 RA naive_total | 5.9% |
| Bcells_CD3neg | 5.9% |
| CD14+16+mono_myeloid | 5.9% |
| CD27negIgDneg_Bcells | 5.9% |
| CD8 RA naive_CD3 | 5.9% |
| NKCD16_nonTnonB | 5.9% |
| NKCD16_NK | 5.9% |
| Bcells naive_total | 2.9% |
| Bcells naive_CD3neg | 2.9% |
| NK Ki67_NK | 2.9% |
| NK Ki67_nonTnonB | 2.9% |
| NKCD56hi_NK | 2.9% |
| CCR5_CD8RO | 2.9% |

**Total features selected by mRMR (Top 10%)_t70**: 29

#### mRMR (Top 10%)_t80

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Bcells CD27posIgDneg_total | 30.0% |
| Tconv memDR_CD3 | 26.7% |
| CD8 RO DR_CD8 | 20.0% |
| Tconv memDR_Tconv | 16.7% |
| myeloid_CD3neg | 13.3% |
| Tconv memCCR5_mem | 13.3% |
| Tconv memDR_total | 13.3% |
| Bcells_total | 10.0% |
| DR_CD8RO | 10.0% |
| CD8 RO DR_CD3 | 10.0% |
| CD8 RO CCR5_CD3 | 10.0% |
| CD14+16+mono_CD3neg | 10.0% |
| Tconv memDR_mem | 6.7% |
| CD8 RO CCR5_total | 6.7% |
| CD8 RA naive_total | 6.7% |
| Bcells naive_total | 3.3% |
| CD14+16+mono_total | 3.3% |
| NK Ki67_NK | 3.3% |
| NK Ki67_nonTnonB | 3.3% |
| CD8 RA naive_CD3 | 3.3% |
| NKCD16_nonTnonB | 3.3% |
| NKCD16_NK | 3.3% |
| nonTnonB_CD3neg | 3.3% |
| Bcells_CD3neg | 3.3% |
| CD14+16+mono_myeloid | 3.3% |
| CD27negIgDneg_Bcells | 3.3% |

**Total features selected by mRMR (Top 10%)_t80**: 26

## Overall Stable Features by Threshold

### Threshold 40%

`Tconv memDR_total`, `Bcells CD27posIgDneg_total`

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
| Bcells CD27posIgDneg_total | 48.8% |
| CD8 RO DR_CD8 | 46.5% |
| CD14+16+mono_CD3neg | 42.0% |
| NKCD16_NK | 34.0% |
| DR_CD8RO | 33.0% |
| Tconv memDR_total | 32.5% |
| Tconv memCCR5_mem | 27.0% |
| Tconv memCXCR3_mem | 25.8% |
| NKCD56hi_total | 23.8% |
| CD8 RO DR_CD3 | 23.2% |
| NK Ki67_nonTnonB | 23.0% |
| CD27negIgDneg_Bcells | 21.0% |
| NK Ki67_NK | 20.8% |
| Tconv memDR_CD3 | 20.0% |
| NKCD56hi_NK | 20.0% |
| CD14+16+mono_total | 20.0% |
| NKCD16_nonTnonB | 19.5% |
| Tconv memDR_mem | 19.0% |
| Treg naive_CD4 | 18.8% |
| CD8 RO CD56_CD8 | 18.2% |
| Bcells naive_total | 17.0% |
| CD8 RO CD56_total | 16.8% |
| CD8 RA naive_CD3 | 16.5% |
| CD8 RA_CD3 | 16.2% |
| CD8 RO CD56_CD3 | 16.0% |
| Tconv memKi67_mem | 15.5% |
| Tconv memTIGIT_mem | 15.2% |
| Bcells_total | 15.2% |
| CD56_CD8RO | 14.5% |
| Treg memory_CD3 | 13.5% |
| CD3hi_CD4neg | 13.2% |
| CD14+16+mono_myeloid | 13.2% |
| nonTnonB_CD3neg | 13.0% |
| CD8 RO CCR5_CD3 | 13.0% |
| Treg memory_total | 13.0% |
| Ki67_Bcells | 13.0% |
| Tconv memCCR6_mem | 12.8% |
| Bcells Ki67_total | 12.5% |
| myeloid_CD3neg | 12.2% |
| CD8 RO CCR6_CD8 | 12.0% |
| Tconv mem_CD3 | 12.0% |
| NK_nonTnonB | 12.0% |
| CD8 RO intB7_CD3 | 11.8% |
| Tconv memKi67_total | 11.0% |
| naive_Bcells | 11.0% |
| Tconv memCCR4_mem | 11.0% |
| Tconv memCCR4_CD3 | 11.0% |
| CD3hi_total | 10.8% |
| NKCD16_total | 10.5% |
| Tconv memCXCR3_total | 10.2% |
| CD8 RO CXCR3_CD3 | 9.8% |
| CCR5_CD8RO | 9.5% |
| Bcells_CD3neg | 9.2% |
| Bcells memory_CD3neg | 9.2% |
| Tconv memCD27_CD3 | 9.2% |
| Bcells memory_total | 9.0% |
| CD16mono_myeloid | 9.0% |
| CD4neg_total | 9.0% |
| Tconv memCD27_Tconv | 8.8% |
| CCR6_CD8RO | 8.5% |
| NK Ki67_CD3neg | 8.5% |
| CD8 RO CCR5_total | 8.5% |
| Tconv memDR_Tconv | 8.2% |
| Tconv memCCR4_Tconv | 8.2% |
| CXCR3_CD8RO | 8.2% |
| CD8 RA naive_total | 8.0% |
| NK_total | 8.0% |
| CD8 RO DR_total | 8.0% |
| CD4 Treg _CD3 | 7.8% |
| Tconv mem_Tconv | 7.8% |
| memory_Bcells | 7.5% |
| CD27IgD_Bcells | 7.5% |
| Bcells naive_CD3neg | 7.5% |
| NKCD16_CD3neg | 7.2% |
| Tconv naive_Tconv | 7.2% |
| CD8 RO intB7_total | 7.2% |
| Tconv memCXCR3_Tconv | 7.2% |
| Tconv memCD56_mem | 6.8% |
| CD8 RO TIGIT_CD8 | 6.5% |
| Tconv memCCR4_total | 6.5% |
| CCR4_CD8RO | 6.2% |
| CD8 RO intB7_CD8 | 6.2% |
| intB7_CD8RO | 6.0% |
| CD8 RO Ki67_total | 5.8% |
| Tconv memCD27_mem | 5.8% |
| CD8 RO CCR6_CD3 | 5.8% |
| CD8 RO Ki67_CD8 | 5.5% |
| Tconv memintB7_mem | 5.5% |
| Tconv memintB7_Tconv | 5.5% |
| CD8pos_CD3 | 5.2% |
| CD16+mono_total | 5.2% |
| NK Ki67_total | 5.2% |
| CD8 RO CXCR3_CD8 | 5.0% |
| Treg naive_CD3 | 5.0% |
| CD8 RA CCR7 naive_CD8 | 5.0% |
| Bcells Ki67_CD3neg | 4.8% |
| Tconv memCCR6_Tconv | 4.8% |
| Ki67_CD8RO | 4.5% |
| Tconv memTIGIT_total | 4.5% |
| Tconv memCCR5_total | 4.2% |
| CD8 RA_CD8 | 4.0% |
| Tconv memCCR5_Tconv | 4.0% |
| CD8 RA_total | 3.8% |
| CD27_CD8RO | 3.8% |
| CD16mono_CD3neg | 3.5% |
| CD8 ncytotox RO CCR4_CD3 | 3.5% |
| NK_CD3neg | 3.5% |
| Tconv memCCR6_CD3 | 3.5% |
| Tconv naive_CD3 | 3.5% |
| CD8 RO PD1_CD8 | 3.5% |
| Tconv memintB7_CD3 | 3.2% |
| CD8 RO CCR5_CD8 | 3.2% |
| Bcells CD27negIgDneg_total | 3.2% |
| CD8 RO CXCR3_total | 3.0% |
| Tconv memCCR6_total | 3.0% |
| Tconv memPD1_total | 3.0% |
| Tconv memCD56_total | 3.0% |
| Treg memory_CD4 | 2.8% |
| CD4 Tconv_CD3 | 2.8% |
| CD14mono_myeloid | 2.8% |
| Tconv memPD1_mem | 2.8% |
| CD8 RO_CD8 | 2.8% |
| Tconv memCD56_CD3 | 2.8% |
| CD4 Treg_CD4 | 2.8% |
| Tconv memCXCR3_CD3 | 2.5% |
| Tconv memCD56_Tconv | 2.5% |
| CD4 Treg_total | 2.5% |
| CD4neg_CD3 | 2.5% |
| CD8 ncytotox RO CCR4_CD8ntox | 2.2% |
| CD8 RO_CD3 | 2.2% |
| CD8 RO TIGIT_CD3 | 2.2% |
| TIGIT_CD8RO | 2.2% |
| CD14mono_CD3neg | 2.0% |
| PD1_CD8RO | 2.0% |
| NKCD56hi_CD3neg | 2.0% |
| CD8 RO CCR4_total | 2.0% |
| CD8 RO CD27_CD8 | 2.0% |
| CD8 RO PD1_CD3 | 2.0% |
| CD8  RO Ki67_CD3 | 2.0% |
| Tconv memCCR5_CD3 | 1.8% |
| Tconv naive_total | 1.5% |
| Tconv memKi67_CD3 | 1.5% |
| Tconv memCD27_total | 1.5% |
| Treg naive_total | 1.5% |
| CD3hi_CD3 | 1.2% |
| CD8 RO CD27_CD3 | 1.2% |
| CD8 RO PD1_total | 1.2% |
| CD4 Tconv mem_total | 1.2% |
| Tconv memTIGIT_CD3 | 1.0% |
| CD4 Tconv_total | 1.0% |
| CD8 RO CCR6_total | 1.0% |
| CD8 RO TIGIT_total | 1.0% |
| Tconv memPD1_CD3 | 0.8% |
| Tconv memKi67_Tconv | 0.8% |
| Tconv memTIGIT_Tconv | 0.8% |
| Tconv memintB7_total | 0.8% |
| NKCD56hi_nonTnonB | 0.5% |
| Tconv memPD1_Tconv | 0.5% |
| CD8pos_total | 0.5% |
| CD8 RO CD27_total | 0.5% |
| CD3pos_total | 0.2% |
| CD3neg_total | 0.2% |
| nonTnonB_total | 0.2% |
| CD8 RO_total | 0.2% |

### ElasticNet_RFE

**Base Method**: Raw feature selection frequencies across all bootstrap samples

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Bcells CD27posIgDneg_total | 27.0% |
| CD14+16+mono_CD3neg | 24.0% |
| CD8 RO DR_CD8 | 23.0% |
| Tconv memDR_total | 17.5% |
| NKCD16_NK | 14.5% |
| DR_CD8RO | 14.2% |
| Tconv memCCR5_mem | 13.5% |
| Tconv memDR_mem | 13.2% |
| CD8 RO DR_CD3 | 13.0% |
| CD27negIgDneg_Bcells | 11.8% |
| Tconv memDR_CD3 | 11.2% |
| NK Ki67_nonTnonB | 10.2% |
| NK Ki67_NK | 9.8% |
| CD14+16+mono_total | 9.5% |
| NKCD56hi_NK | 9.2% |
| Bcells naive_total | 8.8% |
| Treg naive_CD4 | 8.5% |
| NKCD16_nonTnonB | 8.2% |
| myeloid_CD3neg | 8.0% |
| CD8 RO CCR5_CD3 | 7.8% |
| Bcells_total | 7.8% |
| CD14+16+mono_myeloid | 7.0% |
| CD8 RA naive_CD3 | 7.0% |
| NKCD56hi_total | 7.0% |
| CD56_CD8RO | 6.5% |
| Tconv memCXCR3_mem | 6.5% |
| CD16mono_myeloid | 6.5% |
| nonTnonB_CD3neg | 5.8% |
| CD8 RA_CD3 | 5.8% |
| CCR5_CD8RO | 5.8% |
| Tconv memTIGIT_mem | 5.8% |
| Ki67_Bcells | 5.5% |
| CD8 RO CCR5_total | 5.2% |
| CD8 RO CD56_CD8 | 5.2% |
| Tconv memCCR6_mem | 5.0% |
| CD3hi_CD4neg | 5.0% |
| Tconv memDR_Tconv | 4.8% |
| naive_Bcells | 4.5% |
| CD8 RO CXCR3_CD3 | 4.5% |
| CD8 RO CD56_total | 4.5% |
| Bcells_CD3neg | 4.5% |
| CD8 RA naive_total | 4.2% |
| Bcells memory_CD3neg | 4.2% |
| CD8 RO intB7_CD3 | 4.2% |
| Tconv memCD27_CD3 | 4.0% |
| NK_total | 4.0% |
| Tconv mem_CD3 | 4.0% |
| Tconv mem_Tconv | 4.0% |
| Tconv memCD27_Tconv | 4.0% |
| Bcells naive_CD3neg | 3.8% |
| Tconv memCCR4_CD3 | 3.8% |
| NKCD16_total | 3.8% |
| Tconv naive_Tconv | 3.5% |
| NK Ki67_CD3neg | 3.5% |
| Treg memory_CD3 | 3.5% |
| CD27IgD_Bcells | 3.2% |
| Tconv memKi67_mem | 3.2% |
| CD3hi_total | 3.2% |
| CD4neg_total | 3.2% |
| NK_nonTnonB | 3.2% |
| CD8 RO CD56_CD3 | 3.2% |
| Bcells Ki67_total | 3.0% |
| CD8 RA_total | 2.8% |
| Tconv memKi67_total | 2.8% |
| CD8 RO Ki67_total | 2.8% |
| Tconv memCXCR3_total | 2.8% |
| NKCD16_CD3neg | 2.8% |
| Ki67_CD8RO | 2.5% |
| Bcells memory_total | 2.5% |
| CD4 Treg _CD3 | 2.5% |
| CD8 RO CCR6_CD8 | 2.5% |
| CD8pos_CD3 | 2.2% |
| NK Ki67_total | 2.2% |
| CD8 RO intB7_total | 2.2% |
| CXCR3_CD8RO | 2.2% |
| CCR4_CD8RO | 2.2% |
| memory_Bcells | 2.0% |
| CD8 RO CCR6_CD3 | 2.0% |
| Treg naive_CD3 | 2.0% |
| Tconv memCCR4_Tconv | 1.8% |
| Treg memory_total | 1.8% |
| Tconv memCCR4_mem | 1.8% |
| CD8 RO DR_total | 1.8% |
| Tconv memCD56_mem | 1.8% |
| intB7_CD8RO | 1.8% |
| Tconv memCCR4_total | 1.8% |
| Tconv memCCR5_total | 1.5% |
| CCR6_CD8RO | 1.5% |
| CD8 RA CCR7 naive_CD8 | 1.5% |
| CD8 RO Ki67_CD8 | 1.5% |
| Tconv memintB7_mem | 1.5% |
| Tconv memintB7_CD3 | 1.2% |
| CD8 RO intB7_CD8 | 1.2% |
| Tconv memCCR5_Tconv | 1.2% |
| Bcells CD27negIgDneg_total | 1.2% |
| Tconv memCCR6_total | 1.2% |
| Tconv memCCR6_CD3 | 1.2% |
| Tconv memTIGIT_total | 1.2% |
| CD8 RA_CD8 | 1.2% |
| CD8 RO CXCR3_total | 1.2% |
| CD4 Treg_CD4 | 1.2% |
| NK_CD3neg | 1.2% |
| Tconv memPD1_total | 1.2% |
| Tconv memCCR6_Tconv | 1.2% |
| Tconv naive_CD3 | 1.0% |
| Tconv memCD27_mem | 1.0% |
| CD8 RO CXCR3_CD8 | 1.0% |
| Tconv memCXCR3_Tconv | 1.0% |
| CD4 Tconv_CD3 | 1.0% |
| CD8 RO TIGIT_CD8 | 1.0% |
| CD27_CD8RO | 1.0% |
| CD8 ncytotox RO CCR4_CD3 | 0.8% |
| Tconv memintB7_Tconv | 0.8% |
| CD4 Treg_total | 0.8% |
| CD8 RO_CD3 | 0.8% |
| CD4 Tconv mem_total | 0.8% |
| CD8 RO TIGIT_CD3 | 0.8% |
| CD14mono_myeloid | 0.8% |
| CD14mono_CD3neg | 0.8% |
| Treg naive_total | 0.8% |
| NKCD56hi_CD3neg | 0.8% |
| CD4neg_CD3 | 0.8% |
| Bcells Ki67_CD3neg | 0.8% |
| CD8 RO CCR5_CD8 | 0.8% |
| NKCD56hi_nonTnonB | 0.5% |
| Treg memory_CD4 | 0.5% |
| CD8 RO CCR4_total | 0.5% |
| CD16+mono_total | 0.5% |
| Tconv naive_total | 0.5% |
| CD8  RO Ki67_CD3 | 0.5% |
| CD8 RO_CD8 | 0.5% |
| CD8 RO TIGIT_total | 0.5% |
| CD8 RO PD1_CD8 | 0.5% |
| CD8 RO CD27_total | 0.5% |
| CD16mono_CD3neg | 0.5% |
| TIGIT_CD8RO | 0.5% |
| Tconv memPD1_mem | 0.5% |
| Tconv memCD56_total | 0.5% |
| CD4 Tconv_total | 0.2% |
| CD8pos_total | 0.2% |
| PD1_CD8RO | 0.2% |
| CD8 RO PD1_CD3 | 0.2% |
| Tconv memCCR5_CD3 | 0.2% |
| Tconv memCD27_total | 0.2% |
| CD8 RO CCR6_total | 0.2% |
| CD8 RO CD27_CD3 | 0.2% |
| Tconv memintB7_total | 0.2% |
| Tconv memTIGIT_Tconv | 0.2% |
| CD8 RO PD1_total | 0.2% |
| nonTnonB_total | 0.2% |
| Tconv memCXCR3_CD3 | 0.2% |
| CD8 RO CD27_CD8 | 0.2% |
| Tconv memPD1_CD3 | 0.2% |

### ElasticNet_Strict

**Base Method**: Raw feature selection frequencies across all bootstrap samples

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Bcells CD27posIgDneg_total | 29.0% |
| CD8 RO DR_CD8 | 28.7% |
| DR_CD8RO | 21.2% |
| CD14+16+mono_CD3neg | 20.2% |
| NKCD16_NK | 16.8% |
| Tconv memDR_total | 15.5% |
| Tconv memCCR5_mem | 15.0% |
| CD8 RO DR_CD3 | 14.2% |
| NKCD56hi_total | 12.0% |
| CD27negIgDneg_Bcells | 11.2% |
| NK Ki67_NK | 11.0% |
| Tconv memDR_mem | 10.8% |
| Tconv memCXCR3_mem | 9.8% |
| NK Ki67_nonTnonB | 9.8% |
| CD14+16+mono_total | 9.2% |
| CD8 RO CD56_CD8 | 9.0% |
| Tconv memDR_CD3 | 8.5% |
| Treg naive_CD4 | 8.2% |
| Tconv memTIGIT_mem | 8.0% |
| NKCD56hi_NK | 7.5% |
| Tconv memKi67_mem | 7.2% |
| NKCD16_nonTnonB | 7.0% |
| CD8 RO CCR5_CD3 | 6.8% |
| CD8 RA_CD3 | 6.5% |
| naive_Bcells | 6.0% |
| Tconv memCCR6_mem | 5.8% |
| CD3hi_CD4neg | 5.8% |
| Treg memory_total | 5.8% |
| CD56_CD8RO | 5.5% |
| CCR5_CD8RO | 5.5% |
| CD8 RO CD56_CD3 | 5.5% |
| CD8 RO CD56_total | 5.5% |
| Tconv mem_CD3 | 5.5% |
| Bcells naive_total | 5.2% |
| Treg memory_CD3 | 5.0% |
| CD8 RA naive_CD3 | 4.8% |
| Bcells Ki67_total | 4.5% |
| Tconv memCCR4_mem | 4.2% |
| Tconv memCCR4_CD3 | 4.2% |
| CD8 RO DR_total | 4.0% |
| CD8 RO CXCR3_CD3 | 4.0% |
| myeloid_CD3neg | 4.0% |
| Tconv memCD27_CD3 | 3.8% |
| CD16mono_myeloid | 3.8% |
| CD4neg_total | 3.8% |
| CD3hi_total | 3.8% |
| CXCR3_CD8RO | 3.8% |
| Tconv memCD27_Tconv | 3.8% |
| Ki67_Bcells | 3.5% |
| CD8 RO intB7_CD3 | 3.5% |
| Tconv memDR_Tconv | 3.5% |
| Bcells memory_CD3neg | 3.2% |
| Bcells memory_total | 3.2% |
| Bcells_total | 3.2% |
| Tconv memKi67_total | 3.0% |
| NKCD16_total | 3.0% |
| CD8pos_CD3 | 3.0% |
| Tconv memCCR4_Tconv | 2.8% |
| CD8 RO CCR6_CD8 | 2.8% |
| CD27IgD_Bcells | 2.8% |
| CD4 Treg _CD3 | 2.8% |
| CD14+16+mono_myeloid | 2.8% |
| CCR6_CD8RO | 2.8% |
| CD8 RO Ki67_total | 2.8% |
| CD8 RA naive_total | 2.8% |
| NK_total | 2.5% |
| Tconv memCCR4_total | 2.5% |
| Tconv mem_Tconv | 2.5% |
| CD8 RO CCR5_total | 2.5% |
| nonTnonB_CD3neg | 2.5% |
| CCR4_CD8RO | 2.2% |
| NK Ki67_CD3neg | 2.2% |
| Tconv memCXCR3_total | 2.2% |
| Tconv naive_Tconv | 2.0% |
| memory_Bcells | 2.0% |
| Tconv memCD56_mem | 2.0% |
| NK Ki67_total | 1.8% |
| CD8 RO CXCR3_CD8 | 1.8% |
| Tconv memCXCR3_Tconv | 1.8% |
| CD8 RO Ki67_CD8 | 1.8% |
| CD8 RO TIGIT_CD8 | 1.8% |
| CD8 RA CCR7 naive_CD8 | 1.8% |
| intB7_CD8RO | 1.8% |
| NKCD16_CD3neg | 1.5% |
| CD8 RO CCR4_total | 1.5% |
| Tconv memintB7_Tconv | 1.5% |
| CD8 RO intB7_total | 1.5% |
| NK_nonTnonB | 1.5% |
| CD8 RO CCR6_CD3 | 1.5% |
| CD4 Tconv_CD3 | 1.2% |
| CD16mono_CD3neg | 1.2% |
| CD8 ncytotox RO CCR4_CD3 | 1.0% |
| Tconv memCCR5_Tconv | 1.0% |
| Treg memory_CD4 | 1.0% |
| Tconv memCD27_mem | 1.0% |
| CD8 RO PD1_CD8 | 1.0% |
| Tconv memCCR6_Tconv | 1.0% |
| CD8 RO CXCR3_total | 1.0% |
| CD8 RO CCR5_CD8 | 1.0% |
| Tconv memCCR6_CD3 | 0.8% |
| Tconv memCCR6_total | 0.8% |
| Treg naive_CD3 | 0.8% |
| Bcells_CD3neg | 0.8% |
| Tconv naive_CD3 | 0.8% |
| CD8 RA_total | 0.8% |
| Tconv memintB7_CD3 | 0.8% |
| CD16+mono_total | 0.8% |
| CD8 RA_CD8 | 0.8% |
| CD27_CD8RO | 0.8% |
| Tconv memPD1_total | 0.8% |
| Tconv memintB7_mem | 0.8% |
| TIGIT_CD8RO | 0.5% |
| Tconv memCD56_Tconv | 0.5% |
| Tconv naive_total | 0.5% |
| Tconv memTIGIT_total | 0.5% |
| Tconv memCXCR3_CD3 | 0.5% |
| CD8 RO PD1_total | 0.5% |
| Tconv memPD1_mem | 0.5% |
| Bcells Ki67_CD3neg | 0.5% |
| Bcells naive_CD3neg | 0.5% |
| Bcells CD27negIgDneg_total | 0.5% |
| CD4 Treg_total | 0.5% |
| Ki67_CD8RO | 0.5% |
| Tconv memTIGIT_CD3 | 0.5% |
| Tconv memCCR5_total | 0.5% |
| Tconv memCD56_total | 0.5% |
| Tconv memCD27_total | 0.2% |
| Treg naive_total | 0.2% |
| CD8  RO Ki67_CD3 | 0.2% |
| NK_CD3neg | 0.2% |
| CD14mono_myeloid | 0.2% |
| CD4 Tconv mem_total | 0.2% |
| CD8 RO PD1_CD3 | 0.2% |
| CD8pos_total | 0.2% |
| Tconv memKi67_CD3 | 0.2% |
| Tconv memCD56_CD3 | 0.2% |
| CD14mono_CD3neg | 0.2% |
| PD1_CD8RO | 0.2% |
| CD4 Treg_CD4 | 0.2% |
| CD8 RO TIGIT_CD3 | 0.2% |
| CD8 RO_CD8 | 0.2% |
| CD3hi_CD3 | 0.2% |
| CD8 RO intB7_CD8 | 0.2% |
| CD8 RO CCR6_total | 0.2% |
| CD8 RO CD27_CD8 | 0.2% |
| CD8 RO_CD3 | 0.2% |

### FDR (p < 0.01)

**Base Method**: Raw feature selection frequencies across all bootstrap samples

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Tconv memDR_CD3 | 14.9% |
| Tconv memDR_Tconv | 13.4% |
| Tconv memDR_mem | 12.0% |
| Bcells CD27posIgDneg_total | 11.4% |
| myeloid_CD3neg | 10.6% |
| nonTnonB_CD3neg | 9.1% |
| Bcells_CD3neg | 8.6% |
| Tconv memDR_total | 8.3% |
| CD8 RO CCR5_total | 8.3% |
| Bcells_total | 8.3% |
| CD14+16+mono_CD3neg | 7.4% |
| Bcells naive_CD3neg | 6.6% |
| CD14+16+mono_total | 6.6% |
| Bcells naive_total | 6.0% |
| NKCD16_nonTnonB | 5.4% |
| Tconv memCCR5_mem | 5.1% |
| NK_nonTnonB | 5.1% |
| CD8 RA naive_total | 5.1% |
| CD8 RA_total | 5.1% |
| CD8 RO DR_CD3 | 4.9% |
| CD8 RO DR_CD8 | 4.6% |
| CD14mono_CD3neg | 4.3% |
| nonTnonB_total | 4.3% |
| CD8pos_total | 4.3% |
| CD14+16+mono_myeloid | 4.0% |
| myeloid_total | 4.0% |
| Tconv memCD27_CD3 | 4.0% |
| CD8 RO CCR5_CD3 | 4.0% |
| CD8 RO CXCR3_total | 3.7% |
| CD14mono_total | 3.7% |
| NK Ki67_nonTnonB | 3.7% |
| CD8 RA naive_CD3 | 3.4% |
| Tconv memCD27_Tconv | 3.4% |
| CCR5_CD8RO | 3.4% |
| CD8 RO intB7_total | 2.9% |
| CD8 RO TIGIT_total | 2.9% |
| Bcells memory_CD3neg | 2.9% |
| CD27negIgDneg_Bcells | 2.9% |
| DR_CD8RO | 2.9% |
| CD3neg_total | 2.9% |
| CD3pos_total | 2.9% |
| Tconv memCCR5_total | 2.9% |
| CD8 RA CCR7 naive_CD8 | 2.6% |
| CD8 RO CD27_total | 2.6% |
| Tconv naive_Tconv | 2.6% |
| Tconv mem_Tconv | 2.6% |
| Tconv memCCR6_mem | 2.6% |
| NKCD16_CD3neg | 2.3% |
| Bcells memory_total | 2.3% |
| CD8 RO CCR6_total | 2.3% |
| Ki67_Bcells | 2.0% |
| NK_CD3neg | 2.0% |
| CD8 RA_CD3 | 1.7% |
| CD8 RO PD1_total | 1.7% |
| Tconv memintB7_total | 1.7% |
| CD8 RO_total | 1.7% |
| naive_Bcells | 1.7% |
| Tconv memTIGIT_CD3 | 1.7% |
| CD8 RO Ki67_CD8 | 1.7% |
| Tconv memintB7_mem | 1.7% |
| CD8 RO intB7_CD3 | 1.7% |
| CD56_CD8RO | 1.7% |
| Tconv memCCR6_total | 1.4% |
| Tconv memCXCR3_mem | 1.4% |
| Tconv memCCR4_total | 1.4% |
| Ki67_CD8RO | 1.4% |
| Tconv mem_CD3 | 1.4% |
| Tconv naive_total | 1.4% |
| Treg memory_CD3 | 1.4% |
| CD8 RO CCR4_total | 1.1% |
| Tconv memCCR5_Tconv | 1.1% |
| CD8 RO CD56_total | 1.1% |
| CD8 RO TIGIT_CD3 | 1.1% |
| Tconv memCXCR3_total | 1.1% |
| CD8 RO CCR5_CD8 | 1.1% |
| Tconv memPD1_CD3 | 1.1% |
| Tconv memTIGIT_Tconv | 1.1% |
| Tconv memPD1_Tconv | 1.1% |
| CD8  RO Ki67_CD3 | 1.1% |
| CD8 RO CXCR3_CD3 | 1.1% |
| CD4 Treg_CD4 | 1.1% |
| Treg naive_total | 1.1% |
| CD4 Tconv_total | 1.1% |
| Tconv naive_CD3 | 1.1% |
| Tconv memCCR5_CD3 | 1.1% |
| NK Ki67_CD3neg | 1.1% |
| CD4 Treg _CD3 | 1.1% |
| Treg memory_CD4 | 1.1% |
| CD4neg_total | 1.1% |
| intB7_CD8RO | 1.1% |
| CD8 RO intB7_CD8 | 0.9% |
| NK_total | 0.9% |
| NKCD16_total | 0.9% |
| CD8 RO CD56_CD8 | 0.9% |
| CD8 RO CXCR3_CD8 | 0.9% |
| Tconv memKi67_Tconv | 0.9% |
| Tconv memKi67_mem | 0.9% |
| Tconv memCXCR3_CD3 | 0.9% |
| Tconv memKi67_CD3 | 0.9% |
| CXCR3_CD8RO | 0.9% |
| Tconv memCXCR3_Tconv | 0.9% |
| CD8 RO CD27_CD3 | 0.9% |
| CD3hi_CD4neg | 0.9% |
| CD8 RA_CD8 | 0.6% |
| NKCD16_NK | 0.6% |
| CD8 RO CD56_CD3 | 0.6% |
| CD8 RO DR_total | 0.6% |
| CD8 RO PD1_CD3 | 0.6% |
| CD16mono_myeloid | 0.6% |
| NK Ki67_total | 0.6% |
| CD4 Tconv mem_total | 0.6% |
| CD3hi_CD3 | 0.6% |
| CD4 Treg_total | 0.6% |
| PD1_CD8RO | 0.3% |
| CD8 RO PD1_CD8 | 0.3% |
| CD8 RO TIGIT_CD8 | 0.3% |
| Tconv memCD27_total | 0.3% |
| Tconv memCCR6_CD3 | 0.3% |
| Tconv memCD56_Tconv | 0.3% |
| Tconv memCD56_CD3 | 0.3% |
| Tconv memintB7_CD3 | 0.3% |
| NKCD56hi_NK | 0.3% |
| CD8 ncytotox RO CCR4_CD3 | 0.3% |
| Tconv memTIGIT_total | 0.3% |
| Tconv memCD56_total | 0.3% |
| Treg naive_CD4 | 0.3% |
| CD8pos_CD3 | 0.3% |
| NKCD56hi_CD3neg | 0.3% |
| NKCD56hi_total | 0.3% |
| Tconv memCCR6_Tconv | 0.3% |
| Tconv memTIGIT_mem | 0.3% |
| NK Ki67_NK | 0.3% |
| NKCD56hi_nonTnonB | 0.3% |
| memory_Bcells | 0.3% |
| Tconv memPD1_total | 0.3% |
| Bcells Ki67_total | 0.3% |
| Bcells Ki67_CD3neg | 0.3% |
| CD8 RO_CD8 | 0.3% |
| CD8 RO CD27_CD8 | 0.3% |
| CD27IgD_Bcells | 0.3% |
| CD16+mono_total | 0.3% |

### FDR (p < 0.05)

**Base Method**: Raw feature selection frequencies across all bootstrap samples

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Bcells CD27posIgDneg_total | 42.8% |
| Tconv memDR_CD3 | 35.9% |
| Tconv memDR_Tconv | 35.1% |
| myeloid_CD3neg | 32.6% |
| Bcells_total | 30.5% |
| nonTnonB_CD3neg | 30.0% |
| Bcells_CD3neg | 29.7% |
| Bcells naive_CD3neg | 29.7% |
| Tconv memDR_mem | 29.2% |
| CD8 RA naive_total | 26.2% |
| CD14+16+mono_total | 25.4% |
| Bcells naive_total | 24.4% |
| CD8 RO CCR5_total | 24.1% |
| CD8 RA naive_CD3 | 23.3% |
| CD14+16+mono_CD3neg | 23.3% |
| CD8 RA_total | 22.8% |
| nonTnonB_total | 21.0% |
| NKCD16_nonTnonB | 21.0% |
| myeloid_total | 20.8% |
| CD8 RO DR_CD3 | 19.7% |
| Bcells memory_CD3neg | 19.7% |
| Tconv memDR_total | 19.5% |
| CD14mono_total | 19.2% |
| Bcells memory_total | 19.2% |
| NK_nonTnonB | 19.2% |
| CD27negIgDneg_Bcells | 19.0% |
| CD8 RO DR_CD8 | 19.0% |
| CD8pos_total | 19.0% |
| CD14mono_CD3neg | 19.0% |
| NK Ki67_nonTnonB | 17.9% |
| Tconv memCCR5_mem | 17.4% |
| CD8 RO CCR5_CD3 | 16.7% |
| CD3pos_total | 16.2% |
| CD3neg_total | 16.2% |
| CD14+16+mono_myeloid | 16.2% |
| DR_CD8RO | 14.4% |
| CD8 RO intB7_total | 14.1% |
| CD8 RO CCR6_total | 13.6% |
| CD8 RA CCR7 naive_CD8 | 12.8% |
| CCR5_CD8RO | 12.6% |
| CD8 RO CXCR3_total | 12.3% |
| Tconv mem_Tconv | 12.3% |
| Tconv naive_Tconv | 11.8% |
| Tconv naive_total | 11.5% |
| Treg naive_total | 11.5% |
| Tconv memintB7_mem | 11.3% |
| NKCD16_CD3neg | 11.0% |
| NK Ki67_CD3neg | 10.8% |
| CD8 RA_CD3 | 10.8% |
| Tconv memCCR5_total | 10.8% |
| Tconv memCD27_CD3 | 10.5% |
| CD8 RO TIGIT_total | 10.5% |
| NK_CD3neg | 10.5% |
| Tconv memintB7_total | 10.5% |
| Tconv memCCR6_mem | 10.3% |
| Tconv mem_CD3 | 10.3% |
| CD8 RO CD27_total | 9.7% |
| Tconv memCD27_Tconv | 9.7% |
| CD4 Tconv_total | 9.7% |
| Ki67_Bcells | 9.5% |
| CD4neg_total | 8.7% |
| CD8 RO CXCR3_CD3 | 8.7% |
| Tconv memCXCR3_total | 8.5% |
| Tconv memCXCR3_mem | 8.5% |
| CD8 RO_total | 8.5% |
| Treg memory_CD3 | 8.5% |
| Tconv naive_CD3 | 8.5% |
| CD8 RO CD56_CD8 | 8.2% |
| CD8 RO intB7_CD3 | 8.2% |
| CD16mono_myeloid | 8.2% |
| NK Ki67_total | 8.2% |
| Tconv memCCR6_total | 7.4% |
| intB7_CD8RO | 7.2% |
| NK Ki67_NK | 7.2% |
| Ki67_CD8RO | 6.7% |
| naive_Bcells | 6.7% |
| CD56_CD8RO | 6.7% |
| Treg memory_CD4 | 6.4% |
| CD4 Treg _CD3 | 6.4% |
| CD8 RO PD1_total | 6.4% |
| CD8 RO Ki67_CD8 | 6.4% |
| Tconv memCXCR3_Tconv | 6.2% |
| CD8 RO CCR5_CD8 | 6.2% |
| Tconv memTIGIT_Tconv | 6.2% |
| Tconv memKi67_CD3 | 6.2% |
| Treg naive_CD4 | 6.2% |
| CD27IgD_Bcells | 6.2% |
| CD8 RO CCR4_total | 5.6% |
| Tconv memCCR5_Tconv | 5.6% |
| Tconv memTIGIT_CD3 | 5.4% |
| CD8 RO intB7_CD8 | 5.4% |
| CD4 Treg_CD4 | 5.4% |
| NKCD16_total | 5.4% |
| CD8 RO CD56_total | 5.1% |
| CXCR3_CD8RO | 5.1% |
| Tconv memCXCR3_CD3 | 5.1% |
| Bcells Ki67_CD3neg | 4.9% |
| Treg naive_CD3 | 4.9% |
| Tconv memKi67_Tconv | 4.9% |
| CD8  RO Ki67_CD3 | 4.9% |
| Tconv memPD1_total | 4.9% |
| CD4 Treg_total | 4.9% |
| Tconv memPD1_Tconv | 4.9% |
| NK_total | 4.6% |
| NKCD16_NK | 4.6% |
| CD8 RO CD27_CD3 | 4.6% |
| CD3hi_CD4neg | 4.4% |
| CD8 RO TIGIT_CD3 | 4.4% |
| Tconv memPD1_CD3 | 4.4% |
| Tconv memCCR4_total | 4.4% |
| CD8pos_CD3 | 4.4% |
| CD4 Tconv mem_total | 4.1% |
| Tconv memCCR5_CD3 | 4.1% |
| Tconv memintB7_CD3 | 4.1% |
| CD8 RO PD1_CD3 | 3.6% |
| Tconv memCCR6_CD3 | 3.6% |
| Treg memory_total | 3.6% |
| CD8 RA_CD8 | 3.3% |
| NKCD56hi_nonTnonB | 3.3% |
| Tconv memCCR4_Tconv | 3.3% |
| Tconv memCCR4_CD3 | 3.1% |
| CD8 RO CCR6_CD3 | 3.1% |
| CD8 RO PD1_CD8 | 3.1% |
| CD8 RO DR_total | 2.8% |
| CD8 RO_CD8 | 2.8% |
| Tconv memCD56_Tconv | 2.8% |
| Tconv memintB7_Tconv | 2.8% |
| CD8 RO CXCR3_CD8 | 2.8% |
| Tconv memTIGIT_total | 2.6% |
| CD4neg_CD3 | 2.6% |
| NKCD56hi_NK | 2.6% |
| CD3hi_CD3 | 2.6% |
| CD8 ncytotox RO CCR4_CD8ntox | 2.6% |
| Tconv memKi67_mem | 2.6% |
| Tconv memCD27_total | 2.3% |
| Tconv memCCR6_Tconv | 2.3% |
| Bcells CD27negIgDneg_total | 2.3% |
| Tconv memPD1_mem | 2.3% |
| CD8 RO CD56_CD3 | 2.3% |
| CD8 RO Ki67_total | 2.1% |
| Tconv memCCR4_mem | 2.1% |
| Tconv memCD56_CD3 | 2.1% |
| CD8 RO CD27_CD8 | 2.1% |
| CCR4_CD8RO | 2.1% |
| memory_Bcells | 2.1% |
| Bcells Ki67_total | 2.1% |
| NKCD56hi_CD3neg | 1.8% |
| TIGIT_CD8RO | 1.8% |
| CD16+mono_total | 1.8% |
| NKCD56hi_total | 1.5% |
| CD8 RO TIGIT_CD8 | 1.5% |
| CD4 Tconv_CD3 | 1.5% |
| PD1_CD8RO | 1.3% |
| Tconv memCD56_mem | 1.3% |
| CCR6_CD8RO | 1.3% |
| CD8 RO CCR6_CD8 | 1.3% |
| Tconv memCD27_mem | 1.3% |
| CD8 RO_CD3 | 1.0% |
| CD27_CD8RO | 0.8% |
| CD3hi_total | 0.8% |
| Tconv memCD56_total | 0.5% |
| Tconv memTIGIT_mem | 0.5% |
| CD8 ncytotox RO CCR4_CD3 | 0.5% |
| CD14mono_myeloid | 0.3% |
| CD16mono_CD3neg | 0.3% |
| Tconv memKi67_total | 0.3% |

### FDR (p < 0.1)

**Base Method**: Raw feature selection frequencies across all bootstrap samples

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Bcells CD27posIgDneg_total | 57.0% |
| Tconv memDR_CD3 | 52.2% |
| Tconv memDR_Tconv | 48.0% |
| myeloid_CD3neg | 47.5% |
| Bcells_total | 43.2% |
| nonTnonB_CD3neg | 42.0% |
| Bcells_CD3neg | 41.5% |
| Tconv memDR_mem | 41.2% |
| CD14+16+mono_total | 41.2% |
| Bcells naive_CD3neg | 40.5% |
| CD8 RO CCR5_total | 38.5% |
| CD14+16+mono_CD3neg | 38.5% |
| CD8 RA naive_total | 38.2% |
| CD8 RA_total | 38.0% |
| CD8 RA naive_CD3 | 36.2% |
| NKCD16_nonTnonB | 35.5% |
| Bcells naive_total | 34.2% |
| Tconv memCCR5_mem | 34.2% |
| NK_nonTnonB | 33.5% |
| CD14mono_CD3neg | 33.0% |
| Bcells memory_CD3neg | 32.8% |
| Bcells memory_total | 32.5% |
| CD8 RO CCR5_CD3 | 31.2% |
| CD27negIgDneg_Bcells | 31.0% |
| CD8pos_total | 30.5% |
| nonTnonB_total | 30.0% |
| NK Ki67_nonTnonB | 29.8% |
| CD8 RO DR_CD8 | 29.5% |
| CD8 RO DR_CD3 | 29.2% |
| myeloid_total | 28.0% |
| Tconv memDR_total | 27.8% |
| CD14+16+mono_myeloid | 27.3% |
| CD14mono_total | 27.0% |
| DR_CD8RO | 23.8% |
| CCR5_CD8RO | 23.2% |
| CD3pos_total | 22.8% |
| CD3neg_total | 22.8% |
| CD8 RO intB7_total | 22.5% |
| CD8 RO CXCR3_total | 22.0% |
| CD8 RA CCR7 naive_CD8 | 22.0% |
| NK Ki67_CD3neg | 21.2% |
| Tconv mem_Tconv | 21.0% |
| CD8 RO CCR6_total | 20.8% |
| CD8 RA_CD3 | 20.5% |
| NKCD16_CD3neg | 20.2% |
| Tconv naive_Tconv | 20.0% |
| Tconv naive_total | 19.8% |
| Tconv memCCR5_total | 19.8% |
| Tconv memintB7_mem | 19.8% |
| CD8 RO CD27_total | 19.0% |
| NK_CD3neg | 18.8% |
| CD8 RO_total | 18.2% |
| Treg naive_total | 18.2% |
| Tconv memintB7_total | 18.0% |
| Tconv memCCR6_mem | 17.8% |
| Tconv memCD27_CD3 | 17.5% |
| Tconv memCD27_Tconv | 17.5% |
| Ki67_Bcells | 17.5% |
| Treg memory_CD3 | 16.8% |
| CD8 RO CXCR3_CD3 | 16.5% |
| CD4 Tconv_total | 16.2% |
| Tconv mem_CD3 | 16.2% |
| CD8 RO TIGIT_total | 16.0% |
| Tconv memCXCR3_mem | 15.8% |
| CD8 RO Ki67_CD8 | 15.5% |
| CD8 RO intB7_CD3 | 15.5% |
| CD4neg_total | 15.2% |
| Treg naive_CD4 | 15.2% |
| Treg memory_CD4 | 15.0% |
| NK Ki67_total | 14.8% |
| Tconv naive_CD3 | 14.8% |
| Tconv memCXCR3_total | 14.2% |
| CD8 RO CD56_CD8 | 14.2% |
| intB7_CD8RO | 14.0% |
| CD16mono_myeloid | 13.8% |
| CD8 RO PD1_total | 13.8% |
| Tconv memCCR6_total | 13.5% |
| NKCD16_NK | 13.0% |
| CD4 Treg _CD3 | 12.8% |
| Ki67_CD8RO | 12.8% |
| CD8 RO CCR5_CD8 | 12.5% |
| NK Ki67_NK | 12.5% |
| CD8 RO CCR4_total | 12.2% |
| CD27IgD_Bcells | 12.2% |
| Bcells Ki67_CD3neg | 12.2% |
| naive_Bcells | 12.0% |
| Treg naive_CD3 | 11.8% |
| Tconv memCXCR3_Tconv | 11.5% |
| Tconv memKi67_Tconv | 11.5% |
| Tconv memCCR5_Tconv | 11.5% |
| CD4 Treg_CD4 | 11.5% |
| CD56_CD8RO | 11.2% |
| CD3hi_CD4neg | 11.0% |
| Tconv memKi67_CD3 | 10.8% |
| CD8 RO CD27_CD3 | 9.5% |
| CD8 RA_CD8 | 9.5% |
| CD8 RO intB7_CD8 | 9.5% |
| CD8 RO CD56_total | 9.2% |
| CXCR3_CD8RO | 9.2% |
| Tconv memCCR4_total | 9.0% |
| CD8pos_CD3 | 9.0% |
| NKCD16_total | 8.8% |
| Tconv memTIGIT_CD3 | 8.8% |
| Tconv memPD1_CD3 | 8.5% |
| Tconv memTIGIT_Tconv | 8.5% |
| CD8 RO TIGIT_CD3 | 8.2% |
| NKCD56hi_nonTnonB | 8.2% |
| NKCD56hi_NK | 8.2% |
| CD8 RO PD1_CD8 | 8.0% |
| Tconv memPD1_Tconv | 8.0% |
| Tconv memCCR4_Tconv | 7.8% |
| Tconv memCXCR3_CD3 | 7.5% |
| CD3hi_CD3 | 7.5% |
| NK_total | 7.5% |
| Tconv memintB7_CD3 | 7.5% |
| CD4 Treg_total | 7.2% |
| Tconv memPD1_total | 7.0% |
| Treg memory_total | 7.0% |
| Tconv memCCR5_CD3 | 7.0% |
| CD4 Tconv mem_total | 6.8% |
| CD8  RO Ki67_CD3 | 6.8% |
| CD8 RO CXCR3_CD8 | 6.8% |
| Tconv memCCR4_CD3 | 6.5% |
| NKCD56hi_CD3neg | 6.2% |
| CD8 ncytotox RO CCR4_CD8ntox | 6.2% |
| CD8 RO PD1_CD3 | 6.2% |
| CD8 RO CCR6_CD3 | 6.2% |
| Bcells Ki67_total | 6.0% |
| CD8 RO_CD8 | 6.0% |
| CD8 RO DR_total | 6.0% |
| Tconv memintB7_Tconv | 5.5% |
| Tconv memCD56_CD3 | 5.5% |
| Tconv memTIGIT_total | 5.2% |
| CD8 RO_CD3 | 5.2% |
| CD8 RO TIGIT_CD8 | 5.2% |
| Tconv memCCR6_CD3 | 5.2% |
| Tconv memCD56_Tconv | 5.0% |
| NKCD56hi_total | 5.0% |
| Tconv memPD1_mem | 5.0% |
| CCR4_CD8RO | 5.0% |
| CD8 RO CD27_CD8 | 5.0% |
| Tconv memCCR4_mem | 5.0% |
| CD8 RO CD56_CD3 | 4.8% |
| Tconv memCCR6_Tconv | 4.8% |
| Tconv memKi67_mem | 4.8% |
| memory_Bcells | 4.5% |
| Tconv memCD56_mem | 4.5% |
| Tconv memTIGIT_mem | 4.2% |
| Tconv memCD27_total | 4.2% |
| CD4neg_CD3 | 4.0% |
| Tconv memCD27_mem | 4.0% |
| Bcells CD27negIgDneg_total | 3.8% |
| CD8 ncytotox RO CCR4_CD3 | 3.8% |
| CD16+mono_total | 3.8% |
| TIGIT_CD8RO | 3.5% |
| CD8 RO Ki67_total | 3.2% |
| PD1_CD8RO | 3.2% |
| CD4 Tconv_CD3 | 3.2% |
| CD27_CD8RO | 3.2% |
| CD3hi_total | 3.0% |
| CD8 RO CCR6_CD8 | 2.8% |
| Tconv memKi67_total | 2.5% |
| Tconv memCD56_total | 2.2% |
| CD16mono_CD3neg | 2.2% |
| CCR6_CD8RO | 2.2% |
| CD14mono_myeloid | 1.2% |

### LASSO_Lenient

**Base Method**: Raw feature selection frequencies across all bootstrap samples

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Bcells CD27posIgDneg_total | 42.5% |
| CD8 RO DR_CD8 | 35.5% |
| CD14+16+mono_CD3neg | 31.2% |
| NKCD16_NK | 26.5% |
| Tconv memDR_total | 25.0% |
| Tconv memCCR5_mem | 23.0% |
| DR_CD8RO | 22.2% |
| NK Ki67_nonTnonB | 20.2% |
| NKCD56hi_total | 19.2% |
| CD8 RO DR_CD3 | 18.2% |
| Tconv memCXCR3_mem | 18.0% |
| NK Ki67_NK | 17.5% |
| CD27negIgDneg_Bcells | 17.2% |
| Treg naive_CD4 | 16.0% |
| CD8 RO CD56_CD8 | 14.2% |
| Tconv memTIGIT_mem | 13.8% |
| Tconv memDR_mem | 13.5% |
| NKCD16_nonTnonB | 13.2% |
| Bcells naive_total | 12.8% |
| CD8 RO CD56_total | 11.8% |
| CD8 RO CCR5_CD3 | 11.5% |
| Tconv memCCR6_mem | 11.5% |
| CD14+16+mono_total | 11.5% |
| Ki67_Bcells | 11.0% |
| CD8 RA_CD3 | 10.8% |
| NKCD56hi_NK | 10.8% |
| CD8 RA naive_CD3 | 10.5% |
| Bcells Ki67_total | 10.5% |
| Treg memory_total | 10.5% |
| Tconv memKi67_mem | 10.5% |
| CD3hi_CD4neg | 10.2% |
| naive_Bcells | 10.2% |
| Tconv memDR_CD3 | 10.0% |
| Treg memory_CD3 | 9.8% |
| CD8 RO CD56_CD3 | 9.8% |
| CD3hi_total | 9.5% |
| Bcells_total | 9.5% |
| Tconv memCCR4_mem | 9.2% |
| CD8 RO intB7_CD3 | 9.0% |
| myeloid_CD3neg | 9.0% |
| CD56_CD8RO | 9.0% |
| Tconv memCCR4_CD3 | 8.8% |
| Tconv mem_CD3 | 8.8% |
| CD8 RO CCR6_CD8 | 8.8% |
| CD4neg_total | 7.8% |
| CD16mono_myeloid | 7.2% |
| CCR5_CD8RO | 7.2% |
| NKCD16_total | 7.2% |
| Tconv memKi67_total | 7.2% |
| Tconv memCD27_CD3 | 7.0% |
| CCR6_CD8RO | 7.0% |
| CD14+16+mono_myeloid | 6.8% |
| CD27IgD_Bcells | 6.8% |
| Bcells memory_total | 6.8% |
| CD8 RO intB7_total | 6.2% |
| CD8 RO CXCR3_CD3 | 6.0% |
| Bcells memory_CD3neg | 5.8% |
| CD8 RO CCR5_total | 5.8% |
| Tconv memCD27_Tconv | 5.8% |
| Tconv memCXCR3_total | 5.8% |
| CXCR3_CD8RO | 5.8% |
| CCR4_CD8RO | 5.8% |
| Tconv memDR_Tconv | 5.5% |
| Tconv memCD56_mem | 5.5% |
| NK_total | 5.5% |
| CD8 RA naive_total | 5.2% |
| Tconv memCCR4_Tconv | 5.0% |
| CD8 RO Ki67_total | 4.8% |
| Tconv memCD27_mem | 4.8% |
| CD8pos_CD3 | 4.5% |
| Tconv memCCR4_total | 4.5% |
| CD8 RO DR_total | 4.5% |
| nonTnonB_CD3neg | 4.5% |
| Tconv memintB7_Tconv | 4.2% |
| intB7_CD8RO | 4.2% |
| Tconv memCXCR3_Tconv | 4.2% |
| CD8 RO CXCR3_CD8 | 4.2% |
| CD16+mono_total | 4.2% |
| Tconv mem_Tconv | 4.0% |
| Tconv memintB7_mem | 4.0% |
| CD8 RO Ki67_CD8 | 4.0% |
| CD8 RA CCR7 naive_CD8 | 4.0% |
| CD8 RO CCR6_CD3 | 4.0% |
| memory_Bcells | 3.8% |
| Tconv memTIGIT_total | 3.8% |
| CD8 RO intB7_CD8 | 3.8% |
| Bcells naive_CD3neg | 3.8% |
| CD4 Treg _CD3 | 3.8% |
| Bcells CD27negIgDneg_total | 3.5% |
| NK_nonTnonB | 3.5% |
| CD8 RO TIGIT_CD8 | 3.2% |
| CD4neg_CD3 | 3.0% |
| Treg naive_CD3 | 3.0% |
| Tconv memCCR6_CD3 | 3.0% |
| NK Ki67_total | 3.0% |
| Bcells Ki67_CD3neg | 2.8% |
| Treg memory_CD4 | 2.8% |
| Tconv memCCR6_Tconv | 2.8% |
| NK Ki67_CD3neg | 2.8% |
| CD8 RA_CD8 | 2.8% |
| NKCD16_CD3neg | 2.8% |
| CD27_CD8RO | 2.8% |
| Ki67_CD8RO | 2.8% |
| CD14mono_myeloid | 2.5% |
| CD8 RO CXCR3_total | 2.5% |
| Tconv memCCR6_total | 2.5% |
| Tconv naive_CD3 | 2.5% |
| Tconv memCD56_CD3 | 2.5% |
| Tconv memCD56_total | 2.5% |
| CD8 ncytotox RO CCR4_CD3 | 2.2% |
| Tconv memPD1_mem | 2.2% |
| CD16mono_CD3neg | 2.2% |
| Tconv memintB7_CD3 | 2.2% |
| CD4 Treg_CD4 | 2.2% |
| CD8 RO PD1_CD8 | 2.2% |
| Tconv memKi67_CD3 | 2.2% |
| Tconv memCCR5_total | 2.2% |
| CD8 RO TIGIT_CD3 | 2.2% |
| CD4 Tconv_CD3 | 2.2% |
| Tconv naive_Tconv | 2.0% |
| CD4 Treg_total | 2.0% |
| CD8 RO CCR4_total | 1.8% |
| Treg naive_total | 1.8% |
| CD8 RO CCR5_CD8 | 1.8% |
| CD8 RA_total | 1.8% |
| Tconv memCCR5_CD3 | 1.8% |
| CD8 ncytotox RO CCR4_CD8ntox | 1.8% |
| TIGIT_CD8RO | 1.8% |
| Tconv memPD1_total | 1.5% |
| Tconv memCCR5_Tconv | 1.5% |
| NK_CD3neg | 1.5% |
| CD8  RO Ki67_CD3 | 1.5% |
| PD1_CD8RO | 1.5% |
| CD8 RO CD27_CD8 | 1.5% |
| CD8 RO_CD8 | 1.2% |
| NKCD56hi_CD3neg | 1.2% |
| CD8 RO PD1_CD3 | 1.2% |
| Tconv memCD27_total | 1.2% |
| Tconv memCXCR3_CD3 | 1.2% |
| CD8 RO CCR6_total | 1.2% |
| Tconv memKi67_Tconv | 1.0% |
| CD8 RO PD1_total | 1.0% |
| Tconv naive_total | 1.0% |
| CD8 RO_CD3 | 1.0% |
| Tconv memTIGIT_Tconv | 1.0% |
| CD4 Tconv mem_total | 1.0% |
| CD3hi_CD3 | 1.0% |
| CD8pos_total | 0.8% |
| Tconv memintB7_total | 0.8% |
| NKCD56hi_nonTnonB | 0.8% |
| Tconv memPD1_CD3 | 0.8% |
| Bcells_CD3neg | 0.8% |
| CD14mono_CD3neg | 0.8% |
| Tconv memTIGIT_CD3 | 0.5% |
| CD8 RO_total | 0.5% |
| Tconv memCD56_Tconv | 0.5% |
| CD8 RO CD27_total | 0.2% |
| CD8 RO CD27_CD3 | 0.2% |
| CD3neg_total | 0.2% |
| nonTnonB_total | 0.2% |
| CD8 RO TIGIT_total | 0.2% |
| CD4 Tconv_total | 0.2% |

### LASSO_RFE

**Base Method**: Raw feature selection frequencies across all bootstrap samples

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Bcells CD27posIgDneg_total | 26.5% |
| CD8 RO DR_CD8 | 19.0% |
| CD14+16+mono_CD3neg | 18.8% |
| Tconv memCCR5_mem | 15.5% |
| Tconv memDR_total | 14.8% |
| NKCD16_NK | 13.2% |
| CD8 RO DR_CD3 | 11.8% |
| DR_CD8RO | 11.8% |
| CD27negIgDneg_Bcells | 9.5% |
| Tconv memDR_mem | 9.2% |
| NK Ki67_nonTnonB | 8.8% |
| NK Ki67_NK | 8.0% |
| CD8 RO CCR5_CD3 | 7.8% |
| Tconv memCXCR3_mem | 7.0% |
| Treg naive_CD4 | 6.8% |
| Bcells naive_total | 6.8% |
| CD8 RA naive_CD3 | 6.2% |
| CCR5_CD8RO | 6.0% |
| Tconv memDR_CD3 | 6.0% |
| Ki67_Bcells | 6.0% |
| NKCD56hi_NK | 5.8% |
| CD8 RO CD56_CD8 | 5.5% |
| Tconv memCCR6_mem | 5.5% |
| myeloid_CD3neg | 5.2% |
| Bcells_total | 5.2% |
| NKCD16_nonTnonB | 5.2% |
| NKCD56hi_total | 4.8% |
| CD16mono_myeloid | 4.8% |
| Tconv memTIGIT_mem | 4.8% |
| CD56_CD8RO | 4.5% |
| CD8 RA_CD3 | 4.5% |
| naive_Bcells | 4.2% |
| CD14+16+mono_myeloid | 4.0% |
| Tconv memDR_Tconv | 4.0% |
| CD4neg_total | 4.0% |
| CD14+16+mono_total | 3.8% |
| Tconv mem_CD3 | 3.8% |
| Tconv memCD27_CD3 | 3.5% |
| CD8 RO CCR5_total | 3.5% |
| Bcells memory_total | 3.5% |
| CD3hi_CD4neg | 3.5% |
| CD3hi_total | 3.2% |
| nonTnonB_CD3neg | 3.2% |
| Bcells memory_CD3neg | 3.0% |
| Tconv memKi67_mem | 2.8% |
| CD8 RA naive_total | 2.8% |
| NKCD16_total | 2.8% |
| CD8 RO intB7_total | 2.8% |
| CD8 RO CD56_total | 2.5% |
| Tconv memCD27_Tconv | 2.5% |
| CD8 RO CXCR3_CD3 | 2.5% |
| Treg memory_CD3 | 2.5% |
| Treg memory_total | 2.5% |
| CD8 RO CCR6_CD8 | 2.5% |
| CCR6_CD8RO | 2.5% |
| Tconv mem_Tconv | 2.2% |
| NK_total | 2.2% |
| CD8 RO CD56_CD3 | 2.2% |
| CD8pos_CD3 | 2.2% |
| CD27IgD_Bcells | 2.2% |
| CD8 RO intB7_CD3 | 2.2% |
| Tconv memCCR4_CD3 | 2.2% |
| Bcells naive_CD3neg | 2.0% |
| CD8 RO Ki67_total | 2.0% |
| NKCD16_CD3neg | 2.0% |
| Tconv memCCR4_mem | 2.0% |
| Ki67_CD8RO | 1.8% |
| CD4 Treg _CD3 | 1.5% |
| CCR4_CD8RO | 1.5% |
| Tconv memKi67_total | 1.5% |
| CXCR3_CD8RO | 1.5% |
| Bcells Ki67_total | 1.5% |
| Tconv memintB7_Tconv | 1.2% |
| intB7_CD8RO | 1.2% |
| CD4 Treg_total | 1.2% |
| CD8 RO Ki67_CD8 | 1.2% |
| NK_nonTnonB | 1.2% |
| CD8 RA_total | 1.2% |
| Tconv memintB7_mem | 1.2% |
| Tconv memCCR6_CD3 | 1.2% |
| CD8 RA CCR7 naive_CD8 | 1.2% |
| Tconv memCCR4_total | 1.2% |
| CD8 RO CCR4_total | 1.0% |
| Tconv memCD56_mem | 1.0% |
| CD8 RO CXCR3_CD8 | 1.0% |
| NK Ki67_total | 1.0% |
| CD8 RO CCR6_CD3 | 1.0% |
| NK Ki67_CD3neg | 1.0% |
| CD8 RA_CD8 | 1.0% |
| CD8 RO DR_total | 1.0% |
| Treg naive_CD3 | 0.8% |
| Tconv naive_CD3 | 0.8% |
| CD16+mono_total | 0.8% |
| Tconv naive_Tconv | 0.8% |
| CD8 RO intB7_CD8 | 0.8% |
| Treg memory_CD4 | 0.8% |
| Tconv memCD27_mem | 0.8% |
| CD8 RO TIGIT_CD3 | 0.8% |
| CD8 RO CXCR3_total | 0.8% |
| Tconv memCCR6_total | 0.8% |
| Tconv memTIGIT_total | 0.8% |
| Tconv memCCR4_Tconv | 0.8% |
| PD1_CD8RO | 0.8% |
| CD27_CD8RO | 0.8% |
| Bcells CD27negIgDneg_total | 0.8% |
| Tconv memCCR6_Tconv | 0.8% |
| Tconv memCCR5_total | 0.8% |
| CD8pos_total | 0.5% |
| Tconv memCCR5_Tconv | 0.5% |
| TIGIT_CD8RO | 0.5% |
| CD8 RO CCR5_CD8 | 0.5% |
| Tconv memPD1_mem | 0.5% |
| CD8 RO TIGIT_CD8 | 0.5% |
| memory_Bcells | 0.5% |
| CD4 Treg_CD4 | 0.5% |
| Treg naive_total | 0.5% |
| CD8  RO Ki67_CD3 | 0.5% |
| Tconv memCXCR3_total | 0.5% |
| Tconv memCD56_total | 0.5% |
| CD8 RO PD1_CD3 | 0.5% |
| CD8 RO CD27_CD8 | 0.5% |
| CD14mono_myeloid | 0.5% |
| CD8 ncytotox RO CCR4_CD3 | 0.5% |
| Tconv memCXCR3_Tconv | 0.5% |
| Tconv memintB7_CD3 | 0.5% |
| Tconv memCXCR3_CD3 | 0.2% |
| CD4 Tconv_CD3 | 0.2% |
| CD16mono_CD3neg | 0.2% |
| CD8 RO PD1_CD8 | 0.2% |
| CD8 RO CCR6_total | 0.2% |
| NKCD56hi_CD3neg | 0.2% |
| Tconv memCD56_CD3 | 0.2% |
| CD8 RO CD27_total | 0.2% |
| Bcells_CD3neg | 0.2% |
| CD3hi_CD3 | 0.2% |
| NK_CD3neg | 0.2% |
| Bcells Ki67_CD3neg | 0.2% |
| CD14mono_CD3neg | 0.2% |
| Tconv memPD1_total | 0.2% |
| nonTnonB_total | 0.2% |
| CD8 RO PD1_total | 0.2% |
| CD8 RO TIGIT_total | 0.2% |
| CD4neg_CD3 | 0.2% |
| CD8 RO_CD3 | 0.2% |
| NKCD56hi_nonTnonB | 0.2% |

### LASSO_Strict

**Base Method**: Raw feature selection frequencies across all bootstrap samples

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Bcells CD27posIgDneg_total | 23.0% |
| CD8 RO DR_CD8 | 21.2% |
| CD14+16+mono_CD3neg | 14.2% |
| NKCD16_NK | 13.2% |
| DR_CD8RO | 12.8% |
| Tconv memDR_total | 12.2% |
| Tconv memCCR5_mem | 12.2% |
| CD8 RO DR_CD3 | 11.2% |
| Tconv memDR_mem | 9.0% |
| NK Ki67_NK | 8.8% |
| CD27negIgDneg_Bcells | 8.8% |
| NKCD56hi_total | 8.5% |
| CD14+16+mono_total | 6.8% |
| CD8 RO CD56_CD8 | 6.8% |
| Treg naive_CD4 | 6.2% |
| CD8 RO CCR5_CD3 | 6.2% |
| NK Ki67_nonTnonB | 6.0% |
| Tconv memTIGIT_mem | 5.8% |
| CD8 RA_CD3 | 5.8% |
| NKCD16_nonTnonB | 5.5% |
| Tconv memDR_CD3 | 5.5% |
| Tconv memCXCR3_mem | 5.2% |
| CD8 RA naive_CD3 | 4.5% |
| Tconv memCCR6_mem | 4.5% |
| CD56_CD8RO | 4.5% |
| Tconv memKi67_mem | 4.2% |
| CD3hi_CD4neg | 4.2% |
| naive_Bcells | 4.0% |
| CCR5_CD8RO | 4.0% |
| NKCD56hi_NK | 4.0% |
| Tconv mem_CD3 | 3.5% |
| CD8 RO CD56_total | 3.5% |
| Bcells_total | 3.5% |
| Tconv memCD27_CD3 | 3.5% |
| Tconv memCD27_Tconv | 3.2% |
| CD8 RO CD56_CD3 | 3.2% |
| myeloid_CD3neg | 3.2% |
| Bcells naive_total | 3.2% |
| Tconv memCCR4_mem | 3.2% |
| CD8 RO CXCR3_CD3 | 3.0% |
| Treg memory_total | 3.0% |
| CCR6_CD8RO | 3.0% |
| CD3hi_total | 3.0% |
| Tconv mem_Tconv | 3.0% |
| Tconv memCCR4_CD3 | 3.0% |
| CXCR3_CD8RO | 2.8% |
| Treg memory_CD3 | 2.8% |
| CD16mono_myeloid | 2.5% |
| Bcells memory_total | 2.2% |
| CD4neg_total | 2.2% |
| Tconv memKi67_total | 2.2% |
| NK_total | 2.0% |
| Ki67_Bcells | 2.0% |
| Bcells Ki67_total | 2.0% |
| NK Ki67_total | 2.0% |
| NKCD16_total | 2.0% |
| Bcells memory_CD3neg | 2.0% |
| CD8 RA naive_total | 2.0% |
| CD27IgD_Bcells | 2.0% |
| CD8pos_CD3 | 2.0% |
| CD8 RO DR_total | 2.0% |
| Tconv memDR_Tconv | 1.8% |
| Tconv memCCR4_total | 1.8% |
| Tconv memCCR4_Tconv | 1.8% |
| CD8 RO Ki67_CD8 | 1.8% |
| CD8 RO CCR5_total | 1.8% |
| CD8 RO intB7_total | 1.5% |
| Tconv memCXCR3_Tconv | 1.5% |
| Tconv memCD56_mem | 1.5% |
| Treg naive_CD3 | 1.5% |
| CD8 RO CCR6_CD8 | 1.5% |
| nonTnonB_CD3neg | 1.5% |
| CD14+16+mono_myeloid | 1.5% |
| CD4 Treg _CD3 | 1.2% |
| CD8 RO Ki67_total | 1.2% |
| CD8 RO TIGIT_CD8 | 1.2% |
| Tconv memintB7_CD3 | 1.2% |
| CCR4_CD8RO | 1.2% |
| Tconv memCXCR3_total | 1.0% |
| CD14mono_myeloid | 1.0% |
| Tconv memCCR6_total | 1.0% |
| CD8 RO CCR6_CD3 | 1.0% |
| Tconv memCD27_mem | 1.0% |
| CD8 RO intB7_CD3 | 1.0% |
| NK_nonTnonB | 1.0% |
| CD16mono_CD3neg | 1.0% |
| CD8 RA_CD8 | 1.0% |
| CD8 RO CCR4_total | 1.0% |
| Tconv memintB7_Tconv | 1.0% |
| CD8 RO CXCR3_CD8 | 0.8% |
| Treg memory_CD4 | 0.8% |
| Tconv naive_CD3 | 0.8% |
| CD8 RA_total | 0.8% |
| NKCD16_CD3neg | 0.8% |
| CD8 ncytotox RO CCR4_CD3 | 0.8% |
| Tconv memPD1_mem | 0.8% |
| CD8 RO CXCR3_total | 0.8% |
| Tconv memCCR6_CD3 | 0.8% |
| Tconv memCCR6_Tconv | 0.8% |
| Tconv naive_Tconv | 0.8% |
| CD4 Tconv_CD3 | 0.8% |
| CD8 RA CCR7 naive_CD8 | 0.8% |
| CD8 RO PD1_CD8 | 0.8% |
| intB7_CD8RO | 0.8% |
| TIGIT_CD8RO | 0.5% |
| memory_Bcells | 0.5% |
| Tconv memCCR5_Tconv | 0.5% |
| Tconv memTIGIT_total | 0.5% |
| Treg naive_total | 0.5% |
| NK Ki67_CD3neg | 0.5% |
| CD8 RO CCR5_CD8 | 0.5% |
| Tconv memCD56_CD3 | 0.5% |
| Tconv memCD56_total | 0.5% |
| CD4 Treg_total | 0.5% |
| Tconv memCCR5_total | 0.5% |
| CD4 Tconv mem_total | 0.5% |
| Ki67_CD8RO | 0.5% |
| Tconv memintB7_mem | 0.5% |
| Tconv memCD27_total | 0.2% |
| CD8 RO intB7_CD8 | 0.2% |
| Tconv memTIGIT_CD3 | 0.2% |
| CD8 RO PD1_CD3 | 0.2% |
| CD8pos_total | 0.2% |
| CD8 RO TIGIT_CD3 | 0.2% |
| CD14mono_CD3neg | 0.2% |
| Tconv memPD1_total | 0.2% |
| Bcells naive_CD3neg | 0.2% |
| CD8 RO CD27_total | 0.2% |
| Bcells_CD3neg | 0.2% |
| Tconv naive_total | 0.2% |
| CD8 RO_CD8 | 0.2% |
| NK_CD3neg | 0.2% |
| CD27_CD8RO | 0.2% |
| CD8 RO CCR6_total | 0.2% |
| CD8 RO PD1_total | 0.2% |
| CD4 Treg_CD4 | 0.2% |
| Tconv memPD1_CD3 | 0.2% |
| CD8 RO CD27_CD8 | 0.2% |
| CD8 RO_total | 0.2% |
| NKCD56hi_CD3neg | 0.2% |
| CD16+mono_total | 0.2% |

### LogisticRegression_Permutation_AboveMean

**Base Method**: Raw feature selection frequencies across all bootstrap samples

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| nonTnonB_total | 10.0% |
| Tconv mem_Tconv | 10.0% |
| Tconv naive_Tconv | 10.0% |
| Tconv naive_CD3 | 10.0% |
| Treg memory_CD3 | 10.0% |
| CD14mono_total | 10.0% |
| NKCD56hi_nonTnonB | 10.0% |
| CD8 RA_CD8 | 10.0% |
| CD8 RO_CD8 | 10.0% |
| CD8 RO PD1_CD8 | 10.0% |
| CD8 RO TIGIT_CD8 | 10.0% |
| CD27_CD8RO | 10.0% |
| NK Ki67_nonTnonB | 10.0% |
| CD14mono_CD3neg | 10.0% |
| CXCR3_CD8RO | 10.0% |
| NKCD16_nonTnonB | 10.0% |

### LogisticRegression_Permutation_Top10%

**Base Method**: Raw feature selection frequencies across all bootstrap samples

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD3pos_total | 99.8% |
| CD4 Tconv_total | 99.8% |
| CD4 Tconv mem_total | 99.8% |
| Tconv memCCR4_total | 99.8% |
| Tconv memCCR5_total | 99.8% |
| Tconv memCCR6_total | 99.8% |
| Tconv memCD27_total | 99.8% |
| Tconv memCD56_total | 99.8% |
| Tconv memCXCR3_total | 99.8% |
| Tconv memDR_total | 99.8% |
| Tconv memintB7_total | 99.8% |
| Tconv memKi67_total | 99.8% |
| Tconv memPD1_total | 99.8% |
| Tconv memTIGIT_total | 99.8% |
| Tconv naive_total | 99.8% |
| CD4 Treg_total | 99.8% |
| nonTnonB_total | 0.2% |
| Tconv mem_Tconv | 0.2% |
| Tconv naive_Tconv | 0.2% |
| Tconv naive_CD3 | 0.2% |
| Treg memory_CD3 | 0.2% |
| CD14mono_total | 0.2% |
| NKCD56hi_nonTnonB | 0.2% |
| CD8 RA_CD8 | 0.2% |
| CD8 RO_CD8 | 0.2% |
| CD8 RO PD1_CD8 | 0.2% |
| CD8 RO TIGIT_CD8 | 0.2% |
| CD27_CD8RO | 0.2% |
| NK Ki67_nonTnonB | 0.2% |
| CD14mono_CD3neg | 0.2% |
| CXCR3_CD8RO | 0.2% |
| NKCD16_nonTnonB | 0.2% |

### Mutual Information (Top 10%)

**Base Method**: Raw feature selection frequencies across all bootstrap samples

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Bcells CD27posIgDneg_total | 55.8% |
| myeloid_total | 46.8% |
| CD8 RO CCR5_total | 44.0% |
| Bcells memory_CD3neg | 38.2% |
| Tconv memDR_CD3 | 36.2% |
| CD3hi_CD3 | 33.8% |
| Tconv memDR_Tconv | 33.2% |
| CD14mono_total | 32.0% |
| CD8 RO CCR5_CD3 | 30.2% |
| CD27negIgDneg_Bcells | 27.8% |
| Tconv memDR_mem | 27.0% |
| CD8 RO DR_CD3 | 26.8% |
| Tconv memCCR5_mem | 25.2% |
| CD8 RO DR_CD8 | 24.8% |
| Tconv memCXCR3_mem | 24.2% |
| Tconv memDR_total | 22.2% |
| CD14+16+mono_CD3neg | 22.0% |
| CD8 RA_CD8 | 21.0% |
| Tconv memCCR4_mem | 20.5% |
| Bcells_total | 19.8% |
| Tconv naive_CD3 | 19.8% |
| myeloid_CD3neg | 19.5% |
| CD8 RO CD27_CD3 | 19.0% |
| Bcells memory_total | 18.0% |
| CD16mono_myeloid | 18.0% |
| nonTnonB_total | 17.8% |
| CCR5_CD8RO | 17.2% |
| CD14mono_CD3neg | 17.0% |
| Tconv memCD27_CD3 | 16.8% |
| NK_nonTnonB | 16.5% |
| CD8 RO CXCR3_CD3 | 16.5% |
| CD8pos_total | 15.5% |
| CD27IgD_Bcells | 15.0% |
| Tconv mem_Tconv | 15.0% |
| CD8 RO PD1_total | 14.5% |
| Tconv naive_Tconv | 14.2% |
| CD8 RA_total | 13.8% |
| CD8 RO_CD8 | 13.8% |
| Bcells_CD3neg | 13.2% |
| CD8 RO CCR4_total | 13.0% |
| Bcells naive_CD3neg | 13.0% |
| NKCD16_nonTnonB | 12.8% |
| nonTnonB_CD3neg | 12.8% |
| CD8 RA_CD3 | 12.5% |
| CD14+16+mono_total | 12.5% |
| Treg naive_CD4 | 12.5% |
| CD8 RA naive_CD3 | 12.2% |
| Tconv memKi67_total | 12.2% |
| NK Ki67_nonTnonB | 12.0% |
| CD8 RO CXCR3_CD8 | 11.8% |
| DR_CD8RO | 11.8% |
| Tconv memCCR5_CD3 | 11.5% |
| Tconv memPD1_total | 11.5% |
| CD8 RA naive_total | 11.2% |
| Tconv memCD27_Tconv | 11.2% |
| CD3hi_total | 11.0% |
| Tconv memCCR4_CD3 | 10.2% |
| CD8 RO CXCR3_total | 10.0% |
| CD8 RO_total | 9.8% |
| Bcells naive_total | 9.8% |
| Tconv memCCR4_total | 9.5% |
| CD3neg_total | 9.0% |
| CD14+16+mono_myeloid | 9.0% |
| CD3pos_total | 9.0% |
| CD8 RO CD27_total | 8.8% |
| Tconv memCXCR3_CD3 | 8.8% |
| Treg naive_total | 8.5% |
| memory_Bcells | 8.5% |
| NK Ki67_CD3neg | 8.5% |
| Tconv memCCR6_CD3 | 8.2% |
| CD16mono_CD3neg | 8.2% |
| NKCD16_NK | 8.2% |
| NKCD56hi_nonTnonB | 8.2% |
| CD4neg_total | 8.2% |
| CD8 RO CCR6_total | 8.2% |
| Tconv memintB7_mem | 8.0% |
| NK Ki67_total | 8.0% |
| Tconv memCCR5_Tconv | 7.8% |
| Tconv memintB7_total | 7.8% |
| CD8 RO TIGIT_total | 7.5% |
| naive_Bcells | 7.5% |
| CD8 RO_CD3 | 7.5% |
| CD8 RO TIGIT_CD3 | 7.5% |
| NKCD56hi_NK | 7.5% |
| Tconv naive_total | 7.2% |
| CD8 RA CCR7 naive_CD8 | 7.0% |
| Tconv memTIGIT_mem | 7.0% |
| Ki67_Bcells | 7.0% |
| Tconv memTIGIT_CD3 | 7.0% |
| Tconv memCCR6_total | 7.0% |
| CD8 ncytotox RO CCR4_CD8ntox | 6.5% |
| CD14mono_myeloid | 6.5% |
| PD1_CD8RO | 6.2% |
| Tconv memCCR6_Tconv | 6.2% |
| Bcells Ki67_total | 6.2% |
| CD8 RO intB7_total | 6.0% |
| CD8 RO CCR6_CD3 | 6.0% |
| CD8 RO CD56_CD8 | 6.0% |
| NKCD16_total | 5.8% |
| CD4 Treg_total | 5.8% |
| CD8pos_CD3 | 5.8% |
| CD8 ncytotox RO CCR4_CD3 | 5.5% |
| Tconv memKi67_mem | 5.5% |
| Tconv memintB7_CD3 | 5.2% |
| Tconv memCXCR3_Tconv | 5.2% |
| Tconv memintB7_Tconv | 5.2% |
| CD8 RO intB7_CD3 | 5.2% |
| Treg memory_CD4 | 5.2% |
| Tconv memPD1_Tconv | 5.0% |
| Tconv memCD56_Tconv | 5.0% |
| NK Ki67_NK | 5.0% |
| Tconv memCCR5_total | 5.0% |
| CD8 RO CCR5_CD8 | 4.8% |
| Tconv memCCR6_mem | 4.8% |
| NK_CD3neg | 4.8% |
| Tconv memTIGIT_Tconv | 4.8% |
| CD56_CD8RO | 4.5% |
| intB7_CD8RO | 4.5% |
| Treg memory_CD3 | 4.5% |
| Treg naive_CD3 | 4.5% |
| CD27_CD8RO | 4.2% |
| CD8 RO Ki67_CD8 | 4.2% |
| NKCD56hi_CD3neg | 4.2% |
| CD8 RO PD1_CD3 | 4.2% |
| Bcells Ki67_CD3neg | 4.0% |
| CD8 RO CCR6_CD8 | 3.8% |
| CD8 RO CD56_total | 3.8% |
| CD8 RO PD1_CD8 | 3.8% |
| CCR6_CD8RO | 3.8% |
| NKCD56hi_total | 3.5% |
| Tconv memCXCR3_total | 3.5% |
| CD8 RO CD27_CD8 | 3.5% |
| NKCD16_CD3neg | 3.5% |
| NK_total | 3.2% |
| Ki67_CD8RO | 3.2% |
| CD4 Treg _CD3 | 3.2% |
| CD4 Tconv mem_total | 3.2% |
| Tconv memPD1_CD3 | 3.2% |
| CD8 RO intB7_CD8 | 3.0% |
| Tconv memKi67_CD3 | 3.0% |
| Tconv mem_CD3 | 3.0% |
| CD4 Treg_CD4 | 3.0% |
| CD8 RO CD56_CD3 | 3.0% |
| CD3hi_CD4neg | 3.0% |
| CCR4_CD8RO | 3.0% |
| TIGIT_CD8RO | 3.0% |
| Tconv memPD1_mem | 2.8% |
| Tconv memCD27_total | 2.8% |
| CD8 RO Ki67_total | 2.8% |
| CXCR3_CD8RO | 2.8% |
| Bcells CD27negIgDneg_total | 2.8% |
| CD8  RO Ki67_CD3 | 2.8% |
| Tconv memTIGIT_total | 2.5% |
| Tconv memCCR4_Tconv | 2.5% |
| Tconv memCD56_CD3 | 2.2% |
| Tconv memCD27_mem | 2.2% |
| CD4 Tconv_total | 2.0% |
| CD8 RO DR_total | 2.0% |
| Tconv memCD56_total | 2.0% |
| CD8 RO TIGIT_CD8 | 2.0% |
| Tconv memKi67_Tconv | 1.8% |
| CD4neg_CD3 | 1.8% |
| Tconv memCD56_mem | 1.8% |
| CD4 Tconv_CD3 | 1.5% |
| Treg memory_total | 1.2% |

### NaiveBayes_Permutation_AboveMean

**Base Method**: Raw feature selection frequencies across all bootstrap samples

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Bcells CD27posIgDneg_total | 59.8% |
| Ki67_Bcells | 47.5% |
| Tconv memCD56_total | 34.8% |
| Tconv memCXCR3_total | 30.8% |
| CD8 RO CD56_total | 30.5% |
| CD8 RA_total | 29.8% |
| CD3hi_total | 29.2% |
| Bcells memory_CD3neg | 29.0% |
| CD8 RO intB7_total | 29.0% |
| CD8 RO CCR5_total | 28.0% |
| Tconv memDR_CD3 | 25.0% |
| CD8 RA_CD3 | 25.0% |
| Tconv memDR_Tconv | 25.0% |
| CD8 RO CD56_CD3 | 24.8% |
| Bcells naive_CD3neg | 24.5% |
| CD8 RO CCR5_CD3 | 23.2% |
| CD8 RA naive_total | 22.8% |
| Bcells memory_total | 22.8% |
| Tconv memDR_mem | 22.5% |
| Tconv memCD56_mem | 22.2% |
| CD8 RO DR_CD8 | 22.0% |
| Bcells Ki67_total | 21.8% |
| Tconv memCD56_Tconv | 21.8% |
| CD8 RO Ki67_total | 21.8% |
| CD8 RO CXCR3_total | 21.5% |
| CD8 RA naive_CD3 | 21.5% |
| NK Ki67_CD3neg | 20.8% |
| Tconv memCD56_CD3 | 20.5% |
| Bcells_CD3neg | 20.5% |
| NK Ki67_nonTnonB | 20.5% |
| nonTnonB_CD3neg | 20.0% |
| CD8 RO intB7_CD3 | 19.5% |
| NK Ki67_total | 19.2% |
| DR_CD8RO | 19.2% |
| CD8 RO DR_CD3 | 19.2% |
| Tconv memCXCR3_mem | 18.8% |
| Bcells Ki67_CD3neg | 18.8% |
| Tconv memCXCR3_CD3 | 18.5% |
| CD3hi_CD3 | 18.0% |
| Tconv memCXCR3_Tconv | 18.0% |
| CD27IgD_Bcells | 17.5% |
| Tconv memDR_total | 17.0% |
| CD8 ncytotox RO CCR4_CD3 | 16.8% |
| Bcells_total | 16.8% |
| Bcells naive_total | 16.8% |
| CD8 RO CXCR3_CD8 | 16.0% |
| CD8 RO CXCR3_CD3 | 16.0% |
| Tconv memCD27_mem | 15.8% |
| CD16mono_myeloid | 15.5% |
| Treg memory_CD4 | 15.2% |
| CD4neg_total | 15.2% |
| NKCD16_NK | 15.0% |
| CD4neg_CD3 | 14.8% |
| Tconv memCCR6_CD3 | 14.8% |
| Treg naive_CD3 | 14.8% |
| Treg naive_CD4 | 14.8% |
| Tconv memCCR5_total | 14.5% |
| Bcells CD27negIgDneg_total | 14.5% |
| NKCD56hi_NK | 14.5% |
| NKCD16_total | 14.5% |
| CD8 RO DR_total | 14.5% |
| CXCR3_CD8RO | 14.5% |
| Treg naive_total | 14.2% |
| CD14+16+mono_CD3neg | 14.2% |
| NK Ki67_NK | 14.2% |
| CD8 RO CCR4_total | 14.0% |
| NK_total | 14.0% |
| CD27negIgDneg_Bcells | 14.0% |
| CD8 RO_CD8 | 14.0% |
| Tconv memPD1_total | 13.8% |
| Tconv memCD27_Tconv | 13.8% |
| CD14+16+mono_myeloid | 13.8% |
| CD8pos_total | 13.5% |
| CD27_CD8RO | 13.5% |
| CD8 RA CCR7 naive_CD8 | 13.2% |
| myeloid_CD3neg | 13.2% |
| CD8 RO CD56_CD8 | 13.2% |
| Treg memory_total | 13.0% |
| Tconv memCCR6_Tconv | 13.0% |
| CD8 RA_CD8 | 13.0% |
| memory_Bcells | 13.0% |
| CD8 RO PD1_CD3 | 13.0% |
| CD8 RO TIGIT_CD3 | 12.8% |
| CD8 RO PD1_CD8 | 12.8% |
| Tconv naive_CD3 | 12.8% |
| NK_nonTnonB | 12.8% |
| CD4 Treg_CD4 | 12.5% |
| NKCD56hi_total | 12.5% |
| CD8 RO intB7_CD8 | 12.5% |
| NKCD16_nonTnonB | 12.5% |
| Tconv memTIGIT_mem | 12.5% |
| CD8  RO Ki67_CD3 | 12.5% |
| NKCD56hi_CD3neg | 12.5% |
| Tconv memCCR6_total | 12.2% |
| CD8 RO PD1_total | 12.2% |
| CD4 Tconv mem_total | 12.2% |
| NKCD16_CD3neg | 12.0% |
| NK_CD3neg | 12.0% |
| Tconv memPD1_mem | 12.0% |
| CD8 RO TIGIT_CD8 | 11.8% |
| Tconv naive_total | 11.8% |
| Tconv memCCR4_Tconv | 11.8% |
| CD16mono_CD3neg | 11.8% |
| CD3hi_CD4neg | 11.8% |
| Tconv memCCR5_Tconv | 11.8% |
| CD16+mono_total | 11.8% |
| CD14+16+mono_total | 11.5% |
| Tconv memCCR5_mem | 11.5% |
| Tconv memCCR5_CD3 | 11.5% |
| NKCD56hi_nonTnonB | 11.5% |
| CD14mono_myeloid | 11.5% |
| CD8 ncytotox RO CCR4_CD8ntox | 11.2% |
| CD8 RO_total | 11.2% |
| Tconv memKi67_total | 11.2% |
| CD8 RO CD27_CD3 | 11.2% |
| Treg memory_CD3 | 11.2% |
| CD4 Treg _CD3 | 11.0% |
| Tconv memCD27_CD3 | 11.0% |
| CD56_CD8RO | 11.0% |
| CCR4_CD8RO | 11.0% |
| CD8 RO CCR6_total | 11.0% |
| Tconv memCCR4_CD3 | 11.0% |
| CD8 RO CCR6_CD8 | 11.0% |
| CCR6_CD8RO | 10.8% |
| Tconv memTIGIT_total | 10.8% |
| intB7_CD8RO | 10.8% |
| CD8 RO CD27_CD8 | 10.8% |
| Tconv memCCR4_mem | 10.8% |
| Tconv memKi67_mem | 10.8% |
| Tconv naive_Tconv | 10.8% |
| CCR5_CD8RO | 10.8% |
| Tconv memCCR4_total | 10.5% |
| Tconv memPD1_Tconv | 10.5% |
| Tconv memPD1_CD3 | 10.5% |
| CD4 Tconv_CD3 | 10.5% |
| CD8 RO TIGIT_total | 10.5% |
| PD1_CD8RO | 10.5% |
| CD8 RO CCR5_CD8 | 10.5% |
| Tconv mem_Tconv | 10.5% |
| CD14mono_CD3neg | 10.2% |
| CD8 RO CD27_total | 10.2% |
| CD4 Treg_total | 10.0% |
| CD8 RO_CD3 | 10.0% |
| Tconv memCD27_total | 10.0% |
| Tconv memKi67_Tconv | 10.0% |
| Tconv memTIGIT_Tconv | 10.0% |
| TIGIT_CD8RO | 9.8% |
| Tconv memKi67_CD3 | 9.8% |
| CD8 RO Ki67_CD8 | 9.5% |
| CD8pos_CD3 | 9.5% |
| Tconv memintB7_Tconv | 9.5% |
| CD8 RO CCR6_CD3 | 9.2% |
| Tconv memTIGIT_CD3 | 9.2% |
| naive_Bcells | 9.2% |
| Tconv memintB7_CD3 | 9.0% |
| Tconv memintB7_total | 8.8% |
| CD4 Tconv_total | 8.5% |
| Tconv mem_CD3 | 8.5% |
| CD3pos_total | 8.0% |
| Ki67_CD8RO | 8.0% |
| CD3neg_total | 8.0% |
| Tconv memCCR6_mem | 8.0% |
| myeloid_total | 7.8% |
| nonTnonB_total | 7.8% |
| CD14mono_total | 7.8% |
| Tconv memintB7_mem | 7.2% |

### NaiveBayes_Permutation_Top10%

**Base Method**: Raw feature selection frequencies across all bootstrap samples

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Tconv memCD56_total | 69.8% |
| Tconv memCXCR3_total | 62.5% |
| Tconv memCCR6_total | 57.8% |
| Tconv memKi67_total | 57.8% |
| Tconv naive_total | 54.2% |
| Bcells CD27posIgDneg_total | 53.8% |
| Tconv memCD27_total | 53.2% |
| Tconv memDR_total | 52.5% |
| Tconv memPD1_total | 52.2% |
| Tconv memintB7_total | 52.2% |
| Tconv memCCR5_total | 47.5% |
| Ki67_Bcells | 41.5% |
| CD4 Treg_total | 41.0% |
| Tconv memTIGIT_total | 36.2% |
| Tconv memCCR4_total | 36.0% |
| CD4 Tconv mem_total | 35.8% |
| CD3pos_total | 29.5% |
| CD8 RO CD56_total | 22.8% |
| CD3hi_total | 21.2% |
| CD8 RO CCR5_total | 20.8% |
| CD8 RO intB7_total | 20.5% |
| CD8 RA_total | 20.2% |
| CD4 Tconv_total | 16.5% |
| CD8 RA_CD3 | 15.8% |
| Tconv memDR_Tconv | 15.5% |
| Bcells memory_CD3neg | 15.2% |
| Tconv memDR_CD3 | 14.8% |
| Bcells naive_CD3neg | 14.8% |
| Bcells Ki67_total | 14.2% |
| CD8 RO CD56_CD3 | 14.2% |
| CD8 RA naive_total | 13.8% |
| CD8 RO CCR5_CD3 | 13.8% |
| CD8 RO Ki67_total | 13.8% |
| CD8 RO CXCR3_total | 12.8% |
| Bcells_CD3neg | 12.0% |
| nonTnonB_CD3neg | 11.2% |
| CD8 RO DR_CD8 | 11.2% |
| Bcells Ki67_CD3neg | 11.2% |
| Tconv memCD56_Tconv | 11.0% |
| Tconv memCD56_CD3 | 10.8% |
| NK Ki67_CD3neg | 10.8% |
| Tconv memCD56_mem | 10.5% |
| Tconv memDR_mem | 10.2% |
| CD8 RA naive_CD3 | 10.2% |
| NK Ki67_nonTnonB | 10.0% |
| Bcells memory_total | 10.0% |
| CD8 RO intB7_CD3 | 9.5% |
| Bcells naive_total | 8.8% |
| Tconv memCXCR3_Tconv | 8.5% |
| CD3hi_CD3 | 8.5% |
| Tconv memCXCR3_mem | 8.5% |
| Tconv memCXCR3_CD3 | 8.5% |
| CD8 ncytotox RO CCR4_CD3 | 8.2% |
| CD8 RO DR_CD3 | 8.2% |
| DR_CD8RO | 8.0% |
| NK Ki67_total | 8.0% |
| Bcells_total | 7.8% |
| CD27IgD_Bcells | 7.0% |
| NK_total | 6.5% |
| CD8 RO CXCR3_CD3 | 6.2% |
| CD4neg_CD3 | 6.2% |
| Tconv memCD27_mem | 6.0% |
| CD14+16+mono_CD3neg | 5.8% |
| CD8 RO DR_total | 5.8% |
| CD8 RO CCR4_total | 5.5% |
| CD4neg_total | 5.5% |
| Treg memory_CD4 | 5.5% |
| Treg naive_total | 5.2% |
| CD16mono_myeloid | 5.2% |
| CD27negIgDneg_Bcells | 5.0% |
| CD8  RO Ki67_CD3 | 5.0% |
| CD14+16+mono_myeloid | 4.8% |
| CD14+16+mono_total | 4.2% |
| CD27_CD8RO | 4.0% |
| Treg naive_CD4 | 4.0% |
| CD8 RO CXCR3_CD8 | 4.0% |
| CD8pos_total | 4.0% |
| CXCR3_CD8RO | 4.0% |
| myeloid_CD3neg | 3.8% |
| Bcells CD27negIgDneg_total | 3.8% |
| CD8 RO CD56_CD8 | 3.8% |
| Treg memory_total | 3.5% |
| CD8 RO CD27_CD3 | 3.5% |
| NKCD16_NK | 3.5% |
| NKCD16_total | 3.5% |
| Tconv memCCR6_CD3 | 3.5% |
| CD8 RO_total | 3.2% |
| NK Ki67_NK | 3.2% |
| CD8 RO PD1_total | 3.2% |
| Treg naive_CD3 | 3.2% |
| CD8 RO TIGIT_CD3 | 3.0% |
| NKCD56hi_NK | 3.0% |
| Tconv memCCR5_mem | 2.8% |
| NKCD16_nonTnonB | 2.8% |
| Tconv memCCR5_Tconv | 2.8% |
| Tconv memCCR4_Tconv | 2.8% |
| CD8 RO TIGIT_total | 2.8% |
| Tconv memCD27_Tconv | 2.8% |
| CD4 Treg_CD4 | 2.5% |
| CD8 RO PD1_CD3 | 2.5% |
| CD8 RO Ki67_CD8 | 2.2% |
| CD8 RO CCR6_total | 2.2% |
| CD8 RO_CD8 | 2.2% |
| CD8 RO intB7_CD8 | 2.2% |
| CD8 RO CD27_total | 2.2% |
| NKCD56hi_total | 2.2% |
| Tconv memCCR5_CD3 | 2.2% |
| CCR5_CD8RO | 2.2% |
| CD8 RA CCR7 naive_CD8 | 2.2% |
| memory_Bcells | 2.2% |
| Tconv memKi67_Tconv | 2.0% |
| intB7_CD8RO | 2.0% |
| NKCD16_CD3neg | 2.0% |
| Tconv memKi67_mem | 2.0% |
| NK_CD3neg | 2.0% |
| CD8 RO PD1_CD8 | 2.0% |
| CD16mono_CD3neg | 2.0% |
| NK_nonTnonB | 2.0% |
| Tconv memCCR4_CD3 | 2.0% |
| Tconv memPD1_mem | 1.8% |
| CD8 RA_CD8 | 1.8% |
| CD16+mono_total | 1.8% |
| Tconv memTIGIT_mem | 1.8% |
| CD8 RO CCR5_CD8 | 1.5% |
| CCR4_CD8RO | 1.5% |
| Treg memory_CD3 | 1.5% |
| CD3hi_CD4neg | 1.5% |
| Tconv memCCR4_mem | 1.5% |
| CD8 RO TIGIT_CD8 | 1.2% |
| CD14mono_CD3neg | 1.2% |
| Ki67_CD8RO | 1.2% |
| CD4 Treg _CD3 | 1.2% |
| CD14mono_myeloid | 1.2% |
| CCR6_CD8RO | 1.2% |
| CD8 ncytotox RO CCR4_CD8ntox | 1.2% |
| CD56_CD8RO | 1.2% |
| Tconv memCD27_CD3 | 1.2% |
| NKCD56hi_nonTnonB | 1.0% |
| Tconv memKi67_CD3 | 1.0% |
| NKCD56hi_CD3neg | 1.0% |
| Tconv memPD1_Tconv | 1.0% |
| Tconv memCCR6_Tconv | 1.0% |
| CD8 RO_CD3 | 1.0% |
| Tconv naive_CD3 | 1.0% |
| CD3neg_total | 1.0% |
| CD4 Tconv_CD3 | 1.0% |
| nonTnonB_total | 0.8% |
| Tconv mem_Tconv | 0.8% |
| CD8 RO CD27_CD8 | 0.8% |
| Tconv memPD1_CD3 | 0.8% |
| Tconv memTIGIT_Tconv | 0.8% |
| CD8 RO CCR6_CD3 | 0.8% |
| CD8pos_CD3 | 0.8% |
| myeloid_total | 0.8% |
| Tconv mem_CD3 | 0.5% |
| Tconv memTIGIT_CD3 | 0.5% |
| naive_Bcells | 0.5% |
| PD1_CD8RO | 0.5% |
| Tconv naive_Tconv | 0.5% |
| CD8 RO CCR6_CD8 | 0.2% |
| CD14mono_total | 0.2% |
| Tconv memintB7_CD3 | 0.2% |
| Tconv memintB7_mem | 0.2% |
| Tconv memintB7_Tconv | 0.2% |
| Tconv memCCR6_mem | 0.2% |
| TIGIT_CD8RO | 0.2% |

### RFE (RandomForest)

**Base Method**: Raw feature selection frequencies across all bootstrap samples

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| myeloid_CD3neg | 58.2% |
| Tconv memDR_Tconv | 57.5% |
| CD14+16+mono_CD3neg | 57.2% |
| CD27negIgDneg_Bcells | 57.0% |
| Bcells naive_CD3neg | 56.2% |
| Tconv memDR_mem | 56.0% |
| NK Ki67_nonTnonB | 56.0% |
| CCR5_CD8RO | 55.8% |
| naive_Bcells | 54.5% |
| nonTnonB_CD3neg | 54.5% |
| Tconv memDR_CD3 | 54.5% |
| Bcells_CD3neg | 53.8% |
| CD14+16+mono_myeloid | 53.2% |
| NKCD16_NK | 52.8% |
| DR_CD8RO | 52.8% |
| CD8 RO DR_CD8 | 52.8% |
| CD16mono_myeloid | 52.2% |
| NKCD56hi_NK | 51.7% |
| NK Ki67_CD3neg | 51.2% |
| CD27IgD_Bcells | 51.2% |
| NK Ki67_NK | 51.0% |
| NK_nonTnonB | 50.0% |
| Ki67_Bcells | 49.8% |
| memory_Bcells | 49.8% |
| Tconv memCCR5_mem | 49.8% |
| Bcells memory_CD3neg | 49.5% |
| NKCD16_nonTnonB | 48.8% |
| CD14mono_CD3neg | 48.0% |
| CD14mono_myeloid | 46.5% |
| NKCD16_CD3neg | 46.0% |
| CD8 RO DR_CD3 | 45.2% |
| CD8 RO CCR5_CD3 | 45.2% |
| NKCD56hi_nonTnonB | 45.2% |
| Bcells Ki67_CD3neg | 45.0% |
| NKCD56hi_CD3neg | 44.2% |
| NK_CD3neg | 43.8% |
| CD16mono_CD3neg | 43.5% |
| CD56_CD8RO | 43.2% |
| intB7_CD8RO | 43.0% |
| CD8 RA CCR7 naive_CD8 | 42.8% |
| Bcells CD27posIgDneg_total | 42.8% |
| CD8 RO CD56_CD8 | 42.8% |
| PD1_CD8RO | 42.2% |
| Ki67_CD8RO | 42.2% |
| CCR4_CD8RO | 42.2% |
| CXCR3_CD8RO | 42.0% |
| TIGIT_CD8RO | 41.5% |
| CD8 RO Ki67_CD8 | 41.5% |
| Tconv naive_Tconv | 40.2% |
| CD8 RO CCR5_CD8 | 40.0% |
| CD27_CD8RO | 40.0% |
| CD8 RO PD1_CD8 | 39.8% |
| Tconv memCXCR3_mem | 39.0% |
| CCR6_CD8RO | 39.0% |
| CD8 RO TIGIT_CD8 | 38.8% |
| Tconv memCCR6_mem | 38.5% |
| CD3hi_CD4neg | 38.5% |
| CD8 RO intB7_CD8 | 37.8% |
| CD8 ncytotox RO CCR4_CD8ntox | 37.5% |
| Tconv memCD27_Tconv | 37.5% |
| CD8 RO CCR5_total | 37.2% |
| CD8 RO CXCR3_CD8 | 37.0% |
| CD8 RA naive_CD3 | 36.8% |
| CD8 RO CCR6_CD8 | 36.5% |
| Tconv mem_Tconv | 36.2% |
| Tconv memTIGIT_mem | 36.2% |
| CD8 RO_CD8 | 36.0% |
| Tconv memintB7_mem | 36.0% |
| CD8 RA_CD8 | 35.8% |
| CD8 RO CD27_CD8 | 35.2% |
| Tconv memCCR4_mem | 35.0% |
| Tconv memCD27_mem | 34.2% |
| Treg naive_CD4 | 34.2% |
| Tconv memCCR5_Tconv | 33.8% |
| Tconv memCD56_mem | 33.5% |
| Tconv memPD1_Tconv | 33.5% |
| Tconv memKi67_mem | 32.8% |
| Tconv memCXCR3_Tconv | 32.5% |
| Tconv memintB7_Tconv | 32.2% |
| CD8 RO CD27_CD3 | 32.2% |
| Tconv memPD1_mem | 32.0% |
| CD8 RO intB7_CD3 | 31.8% |
| CD8 RO TIGIT_CD3 | 31.5% |
| Tconv memCCR4_Tconv | 31.0% |
| CD8 RO CXCR3_CD3 | 30.8% |
| CD8 RA_CD3 | 30.8% |
| CD8pos_CD3 | 30.5% |
| Tconv memTIGIT_Tconv | 30.5% |
| Treg memory_CD4 | 30.2% |
| Tconv memCD56_Tconv | 30.2% |
| Tconv memCCR6_Tconv | 30.0% |
| Tconv memKi67_Tconv | 30.0% |
| CD14+16+mono_total | 29.8% |
| CD3hi_CD3 | 29.0% |
| Tconv naive_CD3 | 28.7% |
| CD4 Treg_CD4 | 28.2% |
| Bcells_total | 27.0% |
| CD8 RO CCR6_CD3 | 27.0% |
| Tconv memDR_total | 27.0% |
| CD8 RO CD56_CD3 | 26.5% |
| Bcells naive_total | 26.5% |
| CD8 RO_CD3 | 26.5% |
| Treg memory_CD3 | 26.2% |
| CD8  RO Ki67_CD3 | 25.8% |
| CD8 ncytotox RO CCR4_CD3 | 24.8% |
| CD8 RO PD1_CD3 | 24.8% |
| Tconv memCD27_CD3 | 24.2% |
| CD4 Treg _CD3 | 23.8% |
| NK Ki67_total | 23.5% |
| myeloid_total | 23.0% |
| CD4neg_CD3 | 23.0% |
| CD8pos_total | 22.5% |
| nonTnonB_total | 22.5% |
| Tconv mem_CD3 | 21.8% |
| Treg naive_CD3 | 21.8% |
| Tconv memCCR4_CD3 | 21.0% |
| Tconv memCXCR3_CD3 | 21.0% |
| CD14mono_total | 20.8% |
| Tconv memTIGIT_CD3 | 20.2% |
| Tconv memPD1_CD3 | 20.0% |
| CD4 Tconv_CD3 | 20.0% |
| Tconv memintB7_CD3 | 20.0% |
| Tconv memCCR6_CD3 | 20.0% |
| Bcells memory_total | 19.8% |
| Tconv memCCR5_CD3 | 19.5% |
| Tconv memKi67_CD3 | 19.2% |
| Tconv memCD56_CD3 | 18.0% |
| NK_total | 17.8% |
| NKCD16_total | 17.8% |
| Bcells Ki67_total | 17.5% |
| CD8 RA_total | 17.2% |
| CD8 RA naive_total | 17.2% |
| Bcells CD27negIgDneg_total | 17.0% |
| NKCD56hi_total | 17.0% |
| CD8 RO CXCR3_total | 15.5% |
| Tconv naive_total | 15.2% |
| CD3neg_total | 14.8% |
| CD8 RO DR_total | 14.8% |
| CD8 RO TIGIT_total | 14.8% |
| CD8 RO CCR4_total | 14.2% |
| CD8 RO Ki67_total | 14.0% |
| CD8 RO intB7_total | 14.0% |
| CD8 RO CCR6_total | 13.8% |
| CD16+mono_total | 13.8% |
| CD8 RO_total | 13.5% |
| CD8 RO CD56_total | 13.5% |
| CD8 RO CD27_total | 13.2% |
| CD8 RO PD1_total | 13.2% |
| CD4neg_total | 13.2% |
| CD3hi_total | 13.0% |
| Treg naive_total | 10.8% |
| Treg memory_total | 10.5% |
| CD3pos_total | 10.5% |
| Tconv memPD1_total | 10.2% |
| Tconv memCXCR3_total | 9.8% |
| Tconv memCCR5_total | 9.8% |
| CD4 Treg_total | 9.2% |
| Tconv memKi67_total | 9.0% |
| Tconv memTIGIT_total | 8.5% |
| Tconv memCCR4_total | 8.2% |
| Tconv memintB7_total | 6.8% |
| Tconv memCD27_total | 5.8% |
| Tconv memCD56_total | 5.8% |
| CD4 Tconv_total | 5.5% |
| Tconv memCCR6_total | 5.2% |
| CD4 Tconv mem_total | 4.8% |

### RF_Importance

**Base Method**: Raw feature selection frequencies across all bootstrap samples

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Tconv memDR_CD3 | 73.2% |
| Tconv memDR_Tconv | 66.8% |
| Bcells CD27posIgDneg_total | 66.5% |
| Tconv memDR_mem | 58.0% |
| CD8 RO CCR5_total | 57.2% |
| Tconv memDR_total | 54.0% |
| CD8 RO CCR5_CD3 | 53.8% |
| Tconv memCCR5_mem | 52.0% |
| CCR5_CD8RO | 51.7% |
| CD14+16+mono_CD3neg | 51.5% |
| CD8 RO DR_CD3 | 50.7% |
| CD8 RO DR_CD8 | 48.0% |
| myeloid_CD3neg | 47.2% |
| nonTnonB_CD3neg | 45.8% |
| Bcells naive_CD3neg | 44.2% |
| myeloid_total | 43.5% |
| CD27negIgDneg_Bcells | 43.5% |
| Bcells_total | 43.2% |
| CD8pos_total | 43.0% |
| Bcells naive_total | 42.5% |
| NK Ki67_nonTnonB | 42.2% |
| NK Ki67_total | 41.5% |
| DR_CD8RO | 41.2% |
| CD8 RA naive_CD3 | 41.0% |
| CD8 RA CCR7 naive_CD8 | 40.2% |
| NK Ki67_CD3neg | 40.0% |
| CD14+16+mono_total | 40.0% |
| Tconv mem_Tconv | 39.5% |
| nonTnonB_total | 38.8% |
| NKCD16_nonTnonB | 38.5% |
| Tconv memCD27_Tconv | 38.5% |
| Tconv memCXCR3_mem | 38.5% |
| CD8 RA naive_total | 38.2% |
| Bcells_CD3neg | 37.0% |
| CD16mono_myeloid | 36.2% |
| CD14+16+mono_myeloid | 36.0% |
| NKCD16_NK | 35.8% |
| CD8 RA_total | 35.2% |
| CD4neg_total | 34.2% |
| CD14mono_total | 34.2% |
| NK_nonTnonB | 34.2% |
| Tconv memCCR5_Tconv | 33.5% |
| NKCD16_CD3neg | 33.2% |
| CD14mono_CD3neg | 33.2% |
| Tconv naive_CD3 | 33.0% |
| CD27IgD_Bcells | 32.8% |
| CD8 RO CXCR3_CD3 | 32.8% |
| Tconv naive_Tconv | 32.8% |
| CD8 RA_CD3 | 32.5% |
| Tconv memintB7_mem | 32.2% |
| Treg memory_CD4 | 32.2% |
| Tconv memCD27_CD3 | 31.8% |
| Bcells memory_CD3neg | 31.5% |
| CD8 RO CD27_CD3 | 31.0% |
| Treg naive_CD4 | 31.0% |
| Bcells memory_total | 30.8% |
| CD8 RO_total | 30.5% |
| CD8pos_CD3 | 30.2% |
| Ki67_Bcells | 30.2% |
| CD4 Treg _CD3 | 30.0% |
| naive_Bcells | 29.5% |
| NKCD56hi_total | 29.5% |
| CD8 RO CCR6_total | 29.2% |
| NK Ki67_NK | 28.7% |
| CD3hi_total | 28.5% |
| NKCD16_total | 28.5% |
| NKCD56hi_NK | 28.2% |
| Treg memory_CD3 | 28.0% |
| NK_total | 27.8% |
| CD8 RO intB7_CD3 | 27.3% |
| Tconv memCCR5_total | 27.0% |
| Tconv naive_total | 27.0% |
| CD56_CD8RO | 26.8% |
| CD3hi_CD3 | 26.5% |
| Tconv memCCR6_mem | 26.5% |
| NK_CD3neg | 26.5% |
| CD8 RO intB7_total | 26.2% |
| CD8 RO CD56_CD8 | 26.2% |
| Tconv memPD1_total | 26.0% |
| CD4 Treg_CD4 | 25.8% |
| CD8 RO CD27_total | 25.8% |
| CD8 RA_CD8 | 25.8% |
| CCR4_CD8RO | 25.2% |
| CD8 RO CCR5_CD8 | 25.0% |
| CD8 RO CXCR3_total | 25.0% |
| CD8 RO TIGIT_CD3 | 24.8% |
| CD3neg_total | 24.0% |
| Tconv memCCR4_CD3 | 23.8% |
| Ki67_CD8RO | 23.8% |
| Tconv memCCR4_mem | 23.8% |
| Treg naive_total | 23.5% |
| Tconv memCXCR3_CD3 | 23.2% |
| CD8 RO TIGIT_total | 23.0% |
| CD8 RO CCR4_total | 22.8% |
| Tconv memCXCR3_total | 22.8% |
| CD8 RO CCR6_CD3 | 22.5% |
| CD8 RO Ki67_CD8 | 22.5% |
| Tconv memCCR6_Tconv | 22.2% |
| Tconv mem_CD3 | 21.8% |
| CD8 RO DR_total | 21.8% |
| Tconv memCXCR3_Tconv | 21.8% |
| CD4 Treg_total | 21.5% |
| CD3pos_total | 21.5% |
| Treg naive_CD3 | 21.5% |
| CD8 RO PD1_CD8 | 21.5% |
| CD8 RO Ki67_total | 21.2% |
| memory_Bcells | 21.2% |
| CD8 RO CXCR3_CD8 | 21.2% |
| CD8 RO CD56_total | 21.2% |
| Tconv memCD27_mem | 21.0% |
| intB7_CD8RO | 20.8% |
| CD8 ncytotox RO CCR4_CD8ntox | 20.8% |
| Tconv memintB7_Tconv | 20.8% |
| CD3hi_CD4neg | 20.2% |
| CD8 RO CCR6_CD8 | 20.2% |
| CXCR3_CD8RO | 20.0% |
| CD4 Tconv_CD3 | 19.5% |
| Tconv memKi67_total | 19.5% |
| Tconv memTIGIT_mem | 19.2% |
| Tconv memCCR6_CD3 | 19.2% |
| CD8 RO_CD3 | 19.2% |
| CD8  RO Ki67_CD3 | 19.2% |
| CD8 RO_CD8 | 19.2% |
| NKCD56hi_CD3neg | 19.0% |
| CD8 RO PD1_total | 19.0% |
| Bcells CD27negIgDneg_total | 18.8% |
| Tconv memCCR5_CD3 | 18.5% |
| Tconv memCCR4_Tconv | 18.5% |
| Tconv memCD56_Tconv | 18.2% |
| Tconv memKi67_mem | 18.0% |
| CD27_CD8RO | 18.0% |
| Tconv memCD27_total | 17.8% |
| Tconv memTIGIT_CD3 | 17.8% |
| Tconv memCCR4_total | 17.5% |
| Tconv memCCR6_total | 17.5% |
| Tconv memintB7_CD3 | 17.5% |
| CD16mono_CD3neg | 17.5% |
| CD8 RO CD56_CD3 | 17.2% |
| Bcells Ki67_total | 17.2% |
| CD8 RO CD27_CD8 | 17.0% |
| Tconv memintB7_total | 17.0% |
| Tconv memTIGIT_total | 17.0% |
| Bcells Ki67_CD3neg | 17.0% |
| CD8 RO intB7_CD8 | 17.0% |
| CD14mono_myeloid | 16.8% |
| NKCD56hi_nonTnonB | 16.8% |
| Tconv memPD1_Tconv | 16.8% |
| CD8 RO PD1_CD3 | 16.2% |
| Tconv memPD1_CD3 | 16.0% |
| Tconv memTIGIT_Tconv | 16.0% |
| PD1_CD8RO | 16.0% |
| Tconv memKi67_Tconv | 15.8% |
| Tconv memCD56_mem | 15.8% |
| CD8 RO TIGIT_CD8 | 15.8% |
| CCR6_CD8RO | 15.5% |
| Tconv memPD1_mem | 15.5% |
| CD4 Tconv mem_total | 15.2% |
| TIGIT_CD8RO | 14.5% |
| Tconv memCD56_total | 13.8% |
| CD4 Tconv_total | 13.5% |
| Tconv memCD56_CD3 | 13.5% |
| CD16+mono_total | 13.0% |
| CD8 ncytotox RO CCR4_CD3 | 13.0% |
| Tconv memKi67_CD3 | 12.5% |
| CD4neg_CD3 | 11.8% |
| Treg memory_total | 9.2% |

### RandomForest_Permutation_AboveMean

**Base Method**: Raw feature selection frequencies across all bootstrap samples

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Bcells naive_total | 3.7% |
| Ki67_Bcells | 3.7% |
| CD8 RO CCR5_CD3 | 3.7% |
| Tconv memCD27_Tconv | 3.7% |
| CD4 Treg_CD4 | 3.7% |
| Bcells CD27posIgDneg_total | 3.3% |
| Tconv mem_Tconv | 3.3% |
| Tconv memDR_Tconv | 3.3% |
| Bcells_CD3neg | 3.0% |
| Treg naive_CD3 | 3.0% |
| myeloid_CD3neg | 3.0% |
| Tconv naive_CD3 | 3.0% |
| CD8 RO CCR5_total | 2.7% |
| NKCD16_NK | 2.7% |
| Tconv memDR_CD3 | 2.7% |
| CD8 RO DR_CD8 | 2.7% |
| Tconv memCCR6_mem | 2.7% |
| CD16mono_CD3neg | 2.7% |
| CD14+16+mono_CD3neg | 2.7% |
| nonTnonB_CD3neg | 2.7% |
| Bcells_total | 2.7% |
| CD14mono_total | 2.3% |
| Tconv memDR_total | 2.3% |
| CD27IgD_Bcells | 2.3% |
| CD8 RA_total | 2.3% |
| Tconv memPD1_total | 2.3% |
| CD8pos_total | 2.3% |
| Tconv memCD56_CD3 | 2.3% |
| CD8 RO DR_CD3 | 2.3% |
| CD8 RO Ki67_total | 2.3% |
| CD8 RO CCR4_total | 2.3% |
| CD8 RO intB7_total | 2.3% |
| CD8 RA naive_total | 2.3% |
| Bcells naive_CD3neg | 2.3% |
| Treg memory_CD4 | 2.3% |
| CD14+16+mono_myeloid | 2.3% |
| CD8 RO TIGIT_CD8 | 2.3% |
| CD3neg_total | 2.3% |
| NKCD16_nonTnonB | 2.0% |
| CD8 RO Ki67_CD8 | 2.0% |
| Tconv memCCR5_mem | 2.0% |
| CD8 RO_CD8 | 2.0% |
| CD8 RO_total | 2.0% |
| Tconv memCD56_Tconv | 2.0% |
| CD8 RA CCR7 naive_CD8 | 2.0% |
| Tconv memCCR4_Tconv | 2.0% |
| Tconv memTIGIT_Tconv | 2.0% |
| CD8 RA_CD3 | 2.0% |
| CD8 RO_CD3 | 2.0% |
| CCR5_CD8RO | 2.0% |
| CD27negIgDneg_Bcells | 2.0% |
| NK Ki67_total | 2.0% |
| CD27_CD8RO | 2.0% |
| CD4 Tconv_CD3 | 2.0% |
| CD8 RO PD1_CD3 | 2.0% |
| CD8 RO CCR6_CD3 | 2.0% |
| CD4 Tconv mem_total | 2.0% |
| naive_Bcells | 2.0% |
| Tconv memCXCR3_mem | 2.0% |
| CD14+16+mono_total | 2.0% |
| NK_nonTnonB | 2.0% |
| CD8  RO Ki67_CD3 | 1.7% |
| CD8pos_CD3 | 1.7% |
| NK_total | 1.7% |
| Tconv memCCR5_total | 1.7% |
| CD16mono_myeloid | 1.7% |
| Tconv memTIGIT_CD3 | 1.7% |
| NK Ki67_CD3neg | 1.7% |
| CCR4_CD8RO | 1.7% |
| CD8 RO CXCR3_total | 1.7% |
| intB7_CD8RO | 1.7% |
| Tconv memintB7_CD3 | 1.7% |
| CD4neg_total | 1.7% |
| NK Ki67_NK | 1.7% |
| Tconv memCCR5_CD3 | 1.7% |
| CD14mono_myeloid | 1.7% |
| CD8 RO CD27_CD8 | 1.7% |
| Tconv memPD1_CD3 | 1.7% |
| Tconv memTIGIT_total | 1.7% |
| CD8 RO CXCR3_CD3 | 1.7% |
| CD8 RO PD1_total | 1.7% |
| CD4 Treg_total | 1.7% |
| CD8 RO CCR5_CD8 | 1.7% |
| CD8 RO CD56_CD8 | 1.7% |
| CD8 RA naive_CD3 | 1.7% |
| PD1_CD8RO | 1.7% |
| CD8 RO intB7_CD3 | 1.7% |
| CD8 RO TIGIT_total | 1.7% |
| Tconv memPD1_mem | 1.3% |
| NKCD16_CD3neg | 1.3% |
| Tconv memDR_mem | 1.3% |
| CD4neg_CD3 | 1.3% |
| Tconv memTIGIT_mem | 1.3% |
| Tconv memCXCR3_total | 1.3% |
| Tconv memCCR6_CD3 | 1.3% |
| CD8 RO DR_total | 1.3% |
| Treg memory_CD3 | 1.3% |
| CD16+mono_total | 1.3% |
| CD4 Treg _CD3 | 1.3% |
| Bcells memory_total | 1.3% |
| Ki67_CD8RO | 1.3% |
| CD3hi_total | 1.3% |
| CD8 RO TIGIT_CD3 | 1.3% |
| CD3pos_total | 1.3% |
| memory_Bcells | 1.3% |
| NK_CD3neg | 1.3% |
| Tconv naive_Tconv | 1.3% |
| Tconv memCXCR3_CD3 | 1.3% |
| Tconv memintB7_mem | 1.3% |
| CXCR3_CD8RO | 1.3% |
| CD56_CD8RO | 1.3% |
| Tconv memCD27_mem | 1.3% |
| DR_CD8RO | 1.3% |
| CD14mono_CD3neg | 1.3% |
| Treg naive_CD4 | 1.3% |
| Tconv memCXCR3_Tconv | 1.3% |
| CD8 ncytotox RO CCR4_CD8ntox | 1.3% |
| CD8 RO CD56_CD3 | 1.3% |
| Tconv memCCR5_Tconv | 1.0% |
| Tconv memKi67_total | 1.0% |
| CD8 RA_CD8 | 1.0% |
| Tconv memKi67_mem | 1.0% |
| Tconv memCCR6_Tconv | 1.0% |
| NKCD56hi_NK | 1.0% |
| TIGIT_CD8RO | 1.0% |
| Tconv mem_CD3 | 1.0% |
| myeloid_total | 1.0% |
| Tconv memCD27_CD3 | 1.0% |
| Tconv memCCR4_CD3 | 1.0% |
| NKCD56hi_CD3neg | 1.0% |
| CD8 RO CD27_total | 1.0% |
| CD8 RO PD1_CD8 | 1.0% |
| CD8 ncytotox RO CCR4_CD3 | 1.0% |
| CD3hi_CD3 | 1.0% |
| CD4 Tconv_total | 1.0% |
| Treg naive_total | 1.0% |
| Tconv memCCR6_total | 1.0% |
| NKCD16_total | 1.0% |
| Treg memory_total | 1.0% |
| CCR6_CD8RO | 1.0% |
| Tconv naive_total | 1.0% |
| Tconv memCCR4_mem | 1.0% |
| CD8 RO CCR6_total | 1.0% |
| NK Ki67_nonTnonB | 1.0% |
| NKCD56hi_nonTnonB | 0.7% |
| Tconv memCCR4_total | 0.7% |
| Tconv memCD27_total | 0.7% |
| Bcells CD27negIgDneg_total | 0.7% |
| Tconv memKi67_CD3 | 0.7% |
| CD3hi_CD4neg | 0.7% |
| Tconv memintB7_Tconv | 0.7% |
| nonTnonB_total | 0.7% |
| Tconv memCD56_mem | 0.7% |
| Bcells memory_CD3neg | 0.7% |
| Tconv memKi67_Tconv | 0.7% |
| CD8 RO intB7_CD8 | 0.3% |
| CD8 RO CXCR3_CD8 | 0.3% |
| Bcells Ki67_total | 0.3% |
| CD8 RO CCR6_CD8 | 0.3% |
| Bcells Ki67_CD3neg | 0.3% |
| CD8 RO CD56_total | 0.3% |
| Tconv memintB7_total | 0.3% |
| Tconv memPD1_Tconv | 0.3% |
| Tconv memCD56_total | 0.3% |
| CD8 RO CD27_CD3 | 0.3% |

### RandomForest_Permutation_Top10%

**Base Method**: Raw feature selection frequencies across all bootstrap samples

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Tconv memKi67_total | 97.0% |
| Tconv memintB7_total | 96.5% |
| Tconv memCD27_total | 96.2% |
| Tconv naive_total | 95.8% |
| Tconv memCXCR3_total | 95.5% |
| Tconv memDR_total | 95.5% |
| Tconv memCD56_total | 95.0% |
| Tconv memPD1_total | 94.5% |
| CD4 Treg_total | 93.0% |
| CD3pos_total | 91.8% |
| CD4 Tconv mem_total | 90.5% |
| Tconv memTIGIT_total | 87.8% |
| Tconv memCCR4_total | 85.2% |
| CD4 Tconv_total | 83.2% |
| Tconv memCCR5_total | 81.5% |
| Tconv memCCR6_total | 75.2% |
| Ki67_Bcells | 2.5% |
| Tconv memCD27_Tconv | 2.5% |
| Tconv memDR_Tconv | 2.5% |
| Bcells naive_total | 2.2% |
| CD4 Treg_CD4 | 2.2% |
| CD8 RO CCR5_CD3 | 2.2% |
| myeloid_CD3neg | 2.0% |
| CD8 RO CCR5_total | 2.0% |
| Bcells CD27posIgDneg_total | 2.0% |
| Tconv mem_Tconv | 2.0% |
| CD8 RO CCR4_total | 1.8% |
| Tconv naive_CD3 | 1.8% |
| Bcells_CD3neg | 1.8% |
| CD8 RA naive_total | 1.8% |
| CD8 RO intB7_total | 1.8% |
| nonTnonB_CD3neg | 1.8% |
| CD8 RA_total | 1.8% |
| Bcells_total | 1.8% |
| CD8 RO DR_CD3 | 1.8% |
| CD8 RO Ki67_total | 1.8% |
| Tconv memDR_CD3 | 1.8% |
| CD8 RO DR_CD8 | 1.8% |
| NKCD16_NK | 1.5% |
| CD8pos_total | 1.5% |
| CD8 RA CCR7 naive_CD8 | 1.5% |
| Tconv memCCR6_mem | 1.5% |
| naive_Bcells | 1.5% |
| Tconv memCD56_CD3 | 1.5% |
| CD27IgD_Bcells | 1.5% |
| CD14mono_total | 1.5% |
| CD14+16+mono_myeloid | 1.5% |
| CD8 RO TIGIT_CD8 | 1.5% |
| Treg naive_CD3 | 1.5% |
| CD16mono_CD3neg | 1.5% |
| Tconv memCXCR3_mem | 1.5% |
| Bcells naive_CD3neg | 1.5% |
| CD3neg_total | 1.5% |
| Treg memory_CD4 | 1.5% |
| CD4neg_total | 1.2% |
| CD8 RO CD27_CD8 | 1.2% |
| CD27negIgDneg_Bcells | 1.2% |
| CD8 RO TIGIT_total | 1.2% |
| CD8 RA_CD3 | 1.2% |
| CD14mono_myeloid | 1.2% |
| CD8 RO_total | 1.2% |
| Tconv memCCR5_mem | 1.2% |
| CD14+16+mono_CD3neg | 1.2% |
| Tconv memTIGIT_CD3 | 1.2% |
| CD27_CD8RO | 1.2% |
| Tconv memTIGIT_Tconv | 1.2% |
| CD8 RO_CD8 | 1.2% |
| NK_total | 1.0% |
| CD8 RO Ki67_CD8 | 1.0% |
| NK Ki67_total | 1.0% |
| CCR4_CD8RO | 1.0% |
| CD4 Tconv_CD3 | 1.0% |
| CD8 RA naive_CD3 | 1.0% |
| CD8 RO CCR5_CD8 | 1.0% |
| CD14+16+mono_total | 1.0% |
| PD1_CD8RO | 1.0% |
| NK Ki67_NK | 1.0% |
| CD8 RO CD56_CD8 | 1.0% |
| Tconv memCCR6_CD3 | 1.0% |
| Tconv memCCR5_CD3 | 1.0% |
| intB7_CD8RO | 1.0% |
| Tconv memCCR4_Tconv | 1.0% |
| CD8 RO_CD3 | 1.0% |
| CXCR3_CD8RO | 1.0% |
| CD8  RO Ki67_CD3 | 1.0% |
| Tconv memDR_mem | 1.0% |
| Treg memory_CD3 | 1.0% |
| NK Ki67_CD3neg | 1.0% |
| CD8 RO PD1_CD3 | 1.0% |
| CD8 RO CXCR3_CD3 | 1.0% |
| CD4 Treg _CD3 | 1.0% |
| CD8 RO intB7_CD3 | 1.0% |
| DR_CD8RO | 1.0% |
| CD8 RO PD1_total | 1.0% |
| NKCD16_CD3neg | 0.8% |
| Tconv memintB7_CD3 | 0.8% |
| Tconv memintB7_mem | 0.8% |
| NK_nonTnonB | 0.8% |
| Tconv memCXCR3_CD3 | 0.8% |
| CD8 ncytotox RO CCR4_CD8ntox | 0.8% |
| CD3hi_total | 0.8% |
| Tconv memCCR5_Tconv | 0.8% |
| CD16mono_myeloid | 0.8% |
| Tconv memPD1_mem | 0.8% |
| CD8 RO CCR6_CD3 | 0.8% |
| CD8 RA_CD8 | 0.8% |
| Tconv memTIGIT_mem | 0.8% |
| CD8 RO TIGIT_CD3 | 0.8% |
| CD3hi_CD3 | 0.8% |
| CD56_CD8RO | 0.8% |
| CD8 RO DR_total | 0.8% |
| memory_Bcells | 0.8% |
| Tconv memCCR4_mem | 0.8% |
| Tconv memPD1_CD3 | 0.8% |
| Tconv memCD27_mem | 0.8% |
| Tconv memCXCR3_Tconv | 0.8% |
| NKCD16_total | 0.8% |
| CCR5_CD8RO | 0.8% |
| Tconv memCD56_Tconv | 0.8% |
| Treg naive_CD4 | 0.8% |
| CCR6_CD8RO | 0.8% |
| CD8 RO CXCR3_total | 0.8% |
| CD4neg_CD3 | 0.5% |
| CD8pos_CD3 | 0.5% |
| Treg naive_total | 0.5% |
| CD16+mono_total | 0.5% |
| NKCD56hi_CD3neg | 0.5% |
| CD8 RO CD56_CD3 | 0.5% |
| CD8 RO CD27_total | 0.5% |
| Bcells memory_CD3neg | 0.5% |
| nonTnonB_total | 0.5% |
| CD8 RO CCR6_total | 0.5% |
| CD14mono_CD3neg | 0.5% |
| CD3hi_CD4neg | 0.5% |
| Treg memory_total | 0.5% |
| Bcells memory_total | 0.5% |
| NKCD16_nonTnonB | 0.5% |
| Tconv memCCR4_CD3 | 0.5% |
| Tconv naive_Tconv | 0.5% |
| CD8 ncytotox RO CCR4_CD3 | 0.5% |
| Tconv mem_CD3 | 0.5% |
| NK_CD3neg | 0.5% |
| Tconv memCCR6_Tconv | 0.5% |
| myeloid_total | 0.5% |
| NK Ki67_nonTnonB | 0.5% |
| Tconv memKi67_Tconv | 0.2% |
| CD8 RO CCR6_CD8 | 0.2% |
| Bcells Ki67_total | 0.2% |
| Tconv memCD27_CD3 | 0.2% |
| Tconv memPD1_Tconv | 0.2% |
| Ki67_CD8RO | 0.2% |
| CD8 RO PD1_CD8 | 0.2% |
| CD8 RO CD27_CD3 | 0.2% |
| Bcells CD27negIgDneg_total | 0.2% |
| NKCD56hi_NK | 0.2% |
| Tconv memCD56_mem | 0.2% |

### Ridge_Strict

**Base Method**: Raw feature selection frequencies across all bootstrap samples

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| CD8 RO DR_CD8 | 87.2% |
| Bcells CD27posIgDneg_total | 86.8% |
| DR_CD8RO | 84.5% |
| NKCD16_NK | 79.2% |
| Tconv memDR_total | 78.8% |
| NKCD56hi_total | 75.8% |
| NKCD56hi_NK | 74.8% |
| CD14+16+mono_CD3neg | 72.2% |
| CD8 RO DR_total | 71.0% |
| Tconv memKi67_mem | 70.0% |
| NK Ki67_NK | 68.0% |
| CD8 RO DR_CD3 | 67.8% |
| NK Ki67_nonTnonB | 66.0% |
| CD14+16+mono_myeloid | 65.2% |
| Bcells naive_total | 63.7% |
| Bcells_total | 63.0% |
| Tconv memDR_mem | 62.5% |
| CD14+16+mono_total | 61.8% |
| NKCD56hi_CD3neg | 61.8% |
| Tconv memDR_CD3 | 61.5% |
| CD27negIgDneg_Bcells | 61.3% |
| Bcells memory_CD3neg | 60.0% |
| NK Ki67_CD3neg | 59.8% |
| Tconv memCXCR3_Tconv | 59.5% |
| Tconv memCXCR3_mem | 59.5% |
| Tconv memCCR5_mem | 59.5% |
| nonTnonB_CD3neg | 58.5% |
| Bcells_CD3neg | 56.8% |
| Treg naive_CD4 | 55.2% |
| Treg naive_CD3 | 55.0% |
| Tconv memCCR4_mem | 54.5% |
| Tconv memCD27_CD3 | 54.0% |
| CCR5_CD8RO | 53.5% |
| Tconv memKi67_total | 52.8% |
| CCR6_CD8RO | 52.5% |
| Bcells naive_CD3neg | 52.2% |
| NK Ki67_total | 52.0% |
| Tconv memTIGIT_mem | 51.7% |
| Tconv memDR_Tconv | 51.5% |
| CD8 RO CCR6_CD8 | 51.5% |
| Treg memory_total | 51.0% |
| CD8 RO CD56_CD8 | 50.5% |
| CD8 RO Ki67_CD8 | 50.5% |
| Bcells memory_total | 50.0% |
| Tconv memCCR6_mem | 49.8% |
| CD8 RO CD56_total | 49.8% |
| Tconv memCXCR3_CD3 | 49.5% |
| CD27IgD_Bcells | 49.5% |
| CD56_CD8RO | 49.5% |
| CD8 RO CD56_CD3 | 49.2% |
| memory_Bcells | 49.2% |
| CD3hi_CD4neg | 49.0% |
| CD3hi_total | 48.8% |
| NKCD16_nonTnonB | 48.5% |
| CD8 RA naive_CD3 | 48.5% |
| Bcells Ki67_total | 48.0% |
| CD4 Treg_total | 48.0% |
| CXCR3_CD8RO | 47.5% |
| CCR4_CD8RO | 47.2% |
| Tconv memCD27_Tconv | 47.0% |
| NKCD16_total | 46.0% |
| Tconv memKi67_CD3 | 46.0% |
| CD8 RO CXCR3_CD8 | 45.8% |
| myeloid_CD3neg | 45.5% |
| naive_Bcells | 45.5% |
| CD8 RO TIGIT_CD8 | 45.2% |
| NK_nonTnonB | 45.2% |
| Tconv mem_CD3 | 45.0% |
| CD8 RO intB7_CD3 | 44.8% |
| NKCD16_CD3neg | 44.8% |
| Tconv memCD27_mem | 44.5% |
| CD16mono_myeloid | 44.0% |
| CD8 RO PD1_CD8 | 43.8% |
| CD8 RO CCR5_CD3 | 43.2% |
| CD14mono_myeloid | 43.2% |
| Tconv memCCR4_total | 42.8% |
| NK_total | 42.5% |
| CD8 ncytotox RO CCR4_CD8ntox | 42.5% |
| Ki67_Bcells | 42.2% |
| NKCD56hi_nonTnonB | 42.2% |
| Tconv memCCR4_CD3 | 42.2% |
| CD8 RA_CD3 | 41.8% |
| CD8 RO CCR5_total | 41.5% |
| NK_CD3neg | 41.5% |
| CD8 RO intB7_CD8 | 41.2% |
| intB7_CD8RO | 41.2% |
| Treg memory_CD3 | 41.0% |
| CD4 Treg _CD3 | 41.0% |
| CD8 RO intB7_total | 40.8% |
| Tconv memCCR6_CD3 | 40.5% |
| CD8 RO CXCR3_CD3 | 40.0% |
| CD16mono_CD3neg | 39.8% |
| Tconv memCCR5_Tconv | 39.2% |
| Tconv memintB7_mem | 39.2% |
| Tconv memintB7_Tconv | 38.8% |
| Tconv naive_Tconv | 38.5% |
| CD16+mono_total | 38.5% |
| CD4neg_total | 38.2% |
| Tconv mem_Tconv | 38.2% |
| Tconv memCXCR3_total | 38.2% |
| CD8 RO CCR5_CD8 | 37.8% |
| Bcells Ki67_CD3neg | 37.8% |
| CD8 RA naive_total | 37.5% |
| Tconv memKi67_Tconv | 36.8% |
| PD1_CD8RO | 36.2% |
| Tconv memCCR5_CD3 | 35.8% |
| Bcells CD27negIgDneg_total | 35.2% |
| CD27_CD8RO | 35.2% |
| Tconv memCCR4_Tconv | 35.2% |
| Tconv memCCR6_Tconv | 34.8% |
| Tconv memCD56_mem | 34.0% |
| Tconv memCCR5_total | 33.8% |
| TIGIT_CD8RO | 33.8% |
| Treg naive_total | 33.5% |
| CD8 RA CCR7 naive_CD8 | 33.5% |
| Ki67_CD8RO | 33.2% |
| Tconv memintB7_CD3 | 33.0% |
| CD3hi_CD3 | 33.0% |
| Tconv memCD27_total | 32.8% |
| CD4 Tconv_CD3 | 32.5% |
| CD8 RA_CD8 | 31.8% |
| CD8 RO_CD8 | 31.5% |
| CD8 ncytotox RO CCR4_CD3 | 31.5% |
| CD8 RO CXCR3_total | 31.5% |
| Tconv memTIGIT_total | 30.8% |
| CD8 RO Ki67_total | 30.5% |
| CD4 Treg_CD4 | 30.5% |
| Tconv memCD56_total | 30.2% |
| Treg memory_CD4 | 30.0% |
| Tconv memCD56_CD3 | 29.2% |
| Tconv memCD56_Tconv | 29.0% |
| CD8 RO CCR6_CD3 | 28.0% |
| CD8 RA_total | 28.0% |
| Tconv memTIGIT_CD3 | 27.5% |
| CD8pos_CD3 | 27.5% |
| CD8 RO CD27_CD8 | 26.8% |
| Tconv memPD1_mem | 25.2% |
| CD8 RO TIGIT_CD3 | 25.0% |
| Tconv memCCR6_total | 24.2% |
| CD14mono_CD3neg | 23.5% |
| Tconv memTIGIT_Tconv | 23.2% |
| CD4 Tconv mem_total | 23.2% |
| CD4neg_CD3 | 22.5% |
| Tconv memPD1_CD3 | 22.2% |
| CD8 RO CCR4_total | 22.2% |
| CD8 RO CD27_CD3 | 21.8% |
| CD8 RO CCR6_total | 21.5% |
| Tconv memPD1_Tconv | 21.5% |
| Tconv naive_CD3 | 21.0% |
| CD8 RO PD1_CD3 | 21.0% |
| CD8  RO Ki67_CD3 | 19.8% |
| CD8 RO_CD3 | 17.5% |
| Tconv naive_total | 15.8% |
| Tconv memPD1_total | 15.0% |
| CD8 RO TIGIT_total | 14.8% |
| Tconv memintB7_total | 13.8% |
| CD8pos_total | 11.8% |
| CD8 RO PD1_total | 11.0% |
| CD4 Tconv_total | 10.8% |
| CD8 RO CD27_total | 8.5% |
| CD8 RO_total | 8.0% |
| nonTnonB_total | 6.8% |
| CD3neg_total | 5.8% |
| CD3pos_total | 5.8% |
| CD14mono_total | 3.0% |
| myeloid_total | 2.5% |

### SVM_RBF_Permutation_Top10%

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

### XGB_Importance

**Base Method**: Raw feature selection frequencies across all bootstrap samples

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Tconv memDR_CD3 | 35.2% |
| CD8 RO CCR5_total | 30.2% |
| Tconv memDR_total | 27.5% |
| CD8 RO DR_CD3 | 21.8% |
| CD8 RO CCR5_CD3 | 21.8% |
| Bcells CD27posIgDneg_total | 20.5% |
| CD27negIgDneg_Bcells | 16.0% |
| CD3pos_total | 13.8% |
| Tconv memCCR5_mem | 12.5% |
| NKCD16_NK | 12.2% |
| CD16mono_myeloid | 12.0% |
| CD8pos_total | 11.5% |
| Tconv memCCR5_total | 11.0% |
| CD14+16+mono_CD3neg | 10.5% |
| myeloid_CD3neg | 10.5% |
| CD4 Tconv mem_total | 10.2% |
| Ki67_Bcells | 10.2% |
| Tconv memCCR4_total | 9.5% |
| CD14+16+mono_total | 9.5% |
| Tconv memKi67_total | 9.2% |
| NK Ki67_total | 9.2% |
| Bcells naive_total | 9.0% |
| CD8 RA naive_CD3 | 8.8% |
| CD8 RO intB7_CD3 | 8.5% |
| NKCD56hi_total | 8.0% |
| Tconv memDR_Tconv | 8.0% |
| Tconv memDR_mem | 7.5% |
| Bcells_total | 7.5% |
| Tconv memCD56_total | 7.2% |
| CD3hi_total | 7.2% |
| CD8 RA CCR7 naive_CD8 | 7.0% |
| CD8 RA_total | 7.0% |
| CD8 RO CXCR3_CD3 | 7.0% |
| Tconv memCCR6_mem | 6.8% |
| CD4 Tconv_total | 6.5% |
| CD4neg_total | 6.5% |
| Treg naive_CD4 | 6.5% |
| Tconv naive_total | 6.5% |
| Tconv memCCR6_total | 6.2% |
| NK Ki67_nonTnonB | 6.0% |
| CD8 RO CD56_CD8 | 5.8% |
| Tconv memTIGIT_total | 5.8% |
| CD8 RO intB7_total | 5.8% |
| CD8 RO Ki67_total | 5.8% |
| CD8 RO CCR4_total | 5.5% |
| Tconv memTIGIT_mem | 5.2% |
| CD3hi_CD3 | 5.0% |
| Tconv memCXCR3_total | 4.8% |
| Tconv mem_CD3 | 4.8% |
| NK Ki67_NK | 4.8% |
| CD8pos_CD3 | 4.8% |
| Tconv memCD27_CD3 | 4.8% |
| CD27IgD_Bcells | 4.5% |
| NK_total | 4.5% |
| CD8 RO DR_total | 4.5% |
| CD8 RA naive_total | 4.0% |
| Tconv memCD27_total | 4.0% |
| CD14mono_myeloid | 4.0% |
| Tconv memPD1_total | 4.0% |
| CD4 Treg _CD3 | 4.0% |
| CD16+mono_total | 4.0% |
| NKCD56hi_NK | 4.0% |
| CD3hi_CD4neg | 3.8% |
| Tconv memintB7_mem | 3.8% |
| CD8 RO CD27_CD3 | 3.8% |
| NKCD56hi_CD3neg | 3.8% |
| CCR5_CD8RO | 3.8% |
| Tconv memintB7_CD3 | 3.5% |
| Tconv memCCR4_CD3 | 3.5% |
| Tconv naive_CD3 | 3.5% |
| Bcells memory_total | 3.5% |
| CD8  RO Ki67_CD3 | 3.5% |
| Tconv memCCR4_Tconv | 3.5% |
| CD8 RA_CD3 | 3.2% |
| CD4 Treg_total | 3.2% |
| myeloid_total | 3.2% |
| CD8 RO_total | 3.0% |
| CCR4_CD8RO | 3.0% |
| Tconv memCCR4_mem | 3.0% |
| nonTnonB_total | 3.0% |
| CD8 RO CD56_total | 3.0% |
| CD4 Tconv_CD3 | 2.8% |
| naive_Bcells | 2.8% |
| Bcells Ki67_total | 2.8% |
| Tconv memCCR6_CD3 | 2.8% |
| Bcells CD27negIgDneg_total | 2.8% |
| CD8 RO CD27_total | 2.8% |
| Treg memory_CD3 | 2.5% |
| Tconv memCCR6_Tconv | 2.5% |
| Treg memory_total | 2.5% |
| CD8 RO CXCR3_total | 2.5% |
| Tconv mem_Tconv | 2.5% |
| Tconv memintB7_total | 2.5% |
| CD8 RO CCR6_CD8 | 2.5% |
| Tconv memCCR5_CD3 | 2.5% |
| memory_Bcells | 2.5% |
| CD8 RO CD27_CD8 | 2.2% |
| CD8 RA_CD8 | 2.2% |
| CD27_CD8RO | 2.0% |
| CD8 RO CXCR3_CD8 | 2.0% |
| Tconv memCXCR3_CD3 | 2.0% |
| CD8 RO Ki67_CD8 | 2.0% |
| CD8 RO TIGIT_CD3 | 2.0% |
| CD8 RO_CD3 | 1.8% |
| CD8 ncytotox RO CCR4_CD3 | 1.8% |
| TIGIT_CD8RO | 1.8% |
| Tconv memCCR5_Tconv | 1.8% |
| CCR6_CD8RO | 1.8% |
| CD8 RO intB7_CD8 | 1.5% |
| NK_nonTnonB | 1.5% |
| NK_CD3neg | 1.5% |
| Treg naive_CD3 | 1.5% |
| NK Ki67_CD3neg | 1.5% |
| CD56_CD8RO | 1.5% |
| NKCD16_CD3neg | 1.5% |
| CD16mono_CD3neg | 1.5% |
| CXCR3_CD8RO | 1.5% |
| Tconv memTIGIT_Tconv | 1.2% |
| CD8 ncytotox RO CCR4_CD8ntox | 1.2% |
| Tconv memPD1_mem | 1.2% |
| NKCD16_total | 1.2% |
| Tconv memCD56_Tconv | 1.2% |
| Tconv memKi67_mem | 1.2% |
| CD4 Treg_CD4 | 1.2% |
| Tconv memCXCR3_mem | 1.2% |
| Tconv memCD27_Tconv | 1.2% |
| Tconv memTIGIT_CD3 | 1.2% |
| CD8 RO CCR6_CD3 | 1.2% |
| Tconv memCD27_mem | 1.0% |
| Treg memory_CD4 | 1.0% |
| DR_CD8RO | 1.0% |
| CD8 RO CCR6_total | 1.0% |
| Tconv memKi67_CD3 | 1.0% |
| Tconv memCD56_CD3 | 1.0% |
| Bcells memory_CD3neg | 1.0% |
| Tconv memintB7_Tconv | 1.0% |
| Tconv memPD1_Tconv | 0.8% |
| Bcells Ki67_CD3neg | 0.8% |
| CD8 RO TIGIT_total | 0.8% |
| CD8 RO TIGIT_CD8 | 0.8% |
| Bcells naive_CD3neg | 0.8% |
| Treg naive_total | 0.5% |
| CD8 RO PD1_CD3 | 0.5% |
| Ki67_CD8RO | 0.5% |
| Tconv memCD56_mem | 0.5% |
| nonTnonB_CD3neg | 0.5% |
| CD14mono_total | 0.5% |
| Tconv memPD1_CD3 | 0.5% |
| intB7_CD8RO | 0.5% |
| CD8 RO PD1_total | 0.5% |
| CD8 RO PD1_CD8 | 0.5% |
| CD8 RO_CD8 | 0.2% |
| CD8 RO CCR5_CD8 | 0.2% |
| CD4neg_CD3 | 0.2% |
| Tconv memCXCR3_Tconv | 0.2% |
| PD1_CD8RO | 0.2% |
| NKCD56hi_nonTnonB | 0.2% |
| CD14+16+mono_myeloid | 0.2% |
| CD8 RO CD56_CD3 | 0.2% |
| NKCD16_nonTnonB | 0.2% |

### XGBoost_Permutation_AboveMean

**Base Method**: Raw feature selection frequencies across all bootstrap samples

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Tconv memDR_CD3 | 16.8% |
| Bcells CD27posIgDneg_total | 12.5% |
| CD8 RO CCR5_total | 12.0% |
| Tconv memDR_total | 7.0% |
| CD8 RO DR_CD3 | 6.0% |
| CD8 RO CCR5_CD3 | 6.0% |
| CD27negIgDneg_Bcells | 5.8% |
| Tconv memCCR5_mem | 3.8% |
| CD16mono_myeloid | 3.2% |
| CD8pos_total | 3.2% |
| CD14+16+mono_total | 3.0% |
| myeloid_CD3neg | 2.8% |
| CD14+16+mono_CD3neg | 2.5% |
| Bcells naive_total | 2.5% |
| Tconv memDR_mem | 2.5% |
| Ki67_Bcells | 2.5% |
| Tconv memDR_Tconv | 2.2% |
| myeloid_total | 1.8% |
| CD8 RA_total | 1.5% |
| NKCD16_NK | 1.5% |
| Bcells_total | 1.5% |
| Treg naive_CD4 | 1.5% |
| CD8 RO CD27_CD3 | 1.5% |
| NK Ki67_total | 1.5% |
| CD8 RA CCR7 naive_CD8 | 1.2% |
| CD8 RO intB7_CD3 | 1.0% |
| CD3hi_CD4neg | 1.0% |
| CD8 RA naive_CD3 | 1.0% |
| CD8 RO CXCR3_total | 1.0% |
| CD27IgD_Bcells | 1.0% |
| CD8 RO CXCR3_CD3 | 1.0% |
| CD8 RO TIGIT_CD3 | 1.0% |
| Tconv memCCR6_mem | 1.0% |
| CD3hi_total | 1.0% |
| NK Ki67_nonTnonB | 0.8% |
| CD8 RO intB7_total | 0.8% |
| CD8 RO CCR4_total | 0.8% |
| CD8 RO Ki67_total | 0.8% |
| NK Ki67_NK | 0.8% |
| Tconv memPD1_total | 0.8% |
| Tconv mem_CD3 | 0.8% |
| CD56_CD8RO | 0.8% |
| CD8 RA_CD3 | 0.5% |
| CD8pos_CD3 | 0.5% |
| Tconv memintB7_mem | 0.5% |
| CD4neg_total | 0.5% |
| CD3pos_total | 0.5% |
| Tconv memCD27_CD3 | 0.5% |
| CD8 RO CD56_CD8 | 0.5% |
| nonTnonB_total | 0.5% |
| CD8 RO_total | 0.5% |
| CD3hi_CD3 | 0.5% |
| CD8 RA naive_total | 0.5% |
| CCR5_CD8RO | 0.5% |
| Tconv memintB7_CD3 | 0.5% |
| CD8  RO Ki67_CD3 | 0.5% |
| Tconv memTIGIT_mem | 0.5% |
| CCR6_CD8RO | 0.5% |
| Tconv memCD56_Tconv | 0.5% |
| Tconv naive_total | 0.5% |
| Treg naive_total | 0.2% |
| Bcells naive_CD3neg | 0.2% |
| CD8 RO_CD8 | 0.2% |
| Treg memory_CD3 | 0.2% |
| naive_Bcells | 0.2% |
| NKCD56hi_total | 0.2% |
| NKCD56hi_NK | 0.2% |
| Bcells memory_CD3neg | 0.2% |
| CD8 RO CXCR3_CD8 | 0.2% |
| CD8 RA_CD8 | 0.2% |
| Tconv memCCR5_CD3 | 0.2% |
| Tconv memCCR5_total | 0.2% |
| Bcells memory_total | 0.2% |
| Tconv memCXCR3_CD3 | 0.2% |
| Tconv memCD27_Tconv | 0.2% |
| Tconv memCCR6_CD3 | 0.2% |
| CD8 RO PD1_CD8 | 0.2% |
| Tconv memCXCR3_mem | 0.2% |
| Treg memory_total | 0.2% |
| CD8 RO DR_total | 0.2% |
| Tconv memCD56_CD3 | 0.2% |
| Tconv naive_CD3 | 0.2% |
| Tconv memTIGIT_total | 0.2% |
| NK_total | 0.2% |
| Tconv memCCR4_CD3 | 0.2% |
| CD8 RO CD27_total | 0.2% |
| CXCR3_CD8RO | 0.2% |
| CD4 Treg_total | 0.2% |
| Tconv memKi67_total | 0.2% |
| NKCD16_nonTnonB | 0.2% |
| CD27_CD8RO | 0.2% |
| Tconv mem_Tconv | 0.2% |
| CD4 Tconv_CD3 | 0.2% |

### XGBoost_Permutation_Top10%

**Base Method**: Raw feature selection frequencies across all bootstrap samples

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Tconv memintB7_total | 100.0% |
| Tconv naive_total | 100.0% |
| Tconv memCD56_total | 99.8% |
| Tconv memCXCR3_total | 99.8% |
| Tconv memKi67_total | 99.8% |
| Tconv memCD27_total | 99.8% |
| CD3pos_total | 99.5% |
| Tconv memPD1_total | 99.0% |
| CD4 Tconv mem_total | 98.8% |
| Tconv memDR_total | 98.2% |
| Tconv memCCR4_total | 95.0% |
| CD4 Treg_total | 91.8% |
| Tconv memTIGIT_total | 83.2% |
| CD4 Tconv_total | 80.0% |
| Tconv memCCR5_total | 74.5% |
| Tconv memCCR6_total | 39.5% |
| Tconv memDR_CD3 | 16.8% |
| Bcells CD27posIgDneg_total | 12.8% |
| CD8 RO CCR5_total | 12.5% |
| CD8 RO DR_CD3 | 6.2% |
| CD27negIgDneg_Bcells | 6.0% |
| CD8 RO CCR5_CD3 | 6.0% |
| Tconv memCCR5_mem | 4.0% |
| CD8pos_total | 4.0% |
| CD16mono_myeloid | 3.2% |
| CD14+16+mono_total | 3.2% |
| myeloid_CD3neg | 3.0% |
| Bcells naive_total | 2.8% |
| CD14+16+mono_CD3neg | 2.5% |
| Tconv memDR_Tconv | 2.5% |
| Tconv memDR_mem | 2.5% |
| Ki67_Bcells | 2.5% |
| myeloid_total | 2.0% |
| CD8 RA_total | 1.8% |
| NKCD16_NK | 1.8% |
| CD8 RO CD27_CD3 | 1.8% |
| Bcells_total | 1.5% |
| CD8 RA CCR7 naive_CD8 | 1.5% |
| NK Ki67_total | 1.5% |
| Treg naive_CD4 | 1.5% |
| CD8 RO intB7_CD3 | 1.2% |
| CD3hi_total | 1.2% |
| CD8 RA naive_CD3 | 1.2% |
| CD3hi_CD4neg | 1.2% |
| NK Ki67_nonTnonB | 1.2% |
| CD8 RO CXCR3_CD3 | 1.2% |
| CD8 RO intB7_total | 1.0% |
| CD8 RO Ki67_total | 1.0% |
| CD8 RO TIGIT_CD3 | 1.0% |
| CD27IgD_Bcells | 1.0% |
| Tconv memCCR6_mem | 1.0% |
| CD8 RO CXCR3_total | 1.0% |
| nonTnonB_total | 0.8% |
| Tconv mem_CD3 | 0.8% |
| CD8 RO CCR4_total | 0.8% |
| Tconv memCD27_CD3 | 0.8% |
| CD8  RO Ki67_CD3 | 0.8% |
| NK Ki67_NK | 0.8% |
| CD8 RO_total | 0.8% |
| CD56_CD8RO | 0.8% |
| CD8 RA_CD3 | 0.5% |
| CD8 RO DR_total | 0.5% |
| CCR5_CD8RO | 0.5% |
| Tconv memCCR4_mem | 0.5% |
| Tconv memintB7_CD3 | 0.5% |
| CD8 RO CD27_total | 0.5% |
| Treg naive_total | 0.5% |
| CD8pos_CD3 | 0.5% |
| CD3hi_CD3 | 0.5% |
| Tconv memintB7_mem | 0.5% |
| CD8 RO CD56_CD8 | 0.5% |
| Tconv memCD56_Tconv | 0.5% |
| NKCD56hi_NK | 0.5% |
| Tconv memTIGIT_mem | 0.5% |
| NKCD56hi_total | 0.5% |
| CD8 RO CCR6_CD8 | 0.5% |
| Treg memory_total | 0.5% |
| CCR6_CD8RO | 0.5% |
| CD4neg_total | 0.5% |
| Tconv memCCR4_CD3 | 0.5% |
| CD8 ncytotox RO CCR4_CD3 | 0.5% |
| CD8 RA naive_total | 0.5% |
| Bcells memory_total | 0.5% |
| Bcells naive_CD3neg | 0.2% |
| Treg memory_CD3 | 0.2% |
| CD8 RO_CD8 | 0.2% |
| Bcells memory_CD3neg | 0.2% |
| Tconv memCCR4_Tconv | 0.2% |
| CD8 RO CXCR3_CD8 | 0.2% |
| CD14mono_myeloid | 0.2% |
| Tconv memPD1_CD3 | 0.2% |
| CD8 RA_CD8 | 0.2% |
| CD8 RO TIGIT_total | 0.2% |
| Tconv memCCR5_CD3 | 0.2% |
| Tconv memCXCR3_CD3 | 0.2% |
| NK Ki67_CD3neg | 0.2% |
| Tconv memCD27_Tconv | 0.2% |
| naive_Bcells | 0.2% |
| Tconv memCCR6_CD3 | 0.2% |
| Tconv memCXCR3_mem | 0.2% |
| CD8 RO PD1_CD8 | 0.2% |
| Tconv memCD56_CD3 | 0.2% |
| Tconv naive_CD3 | 0.2% |
| NK_total | 0.2% |
| CXCR3_CD8RO | 0.2% |
| CD8 RO CD56_total | 0.2% |
| NKCD16_nonTnonB | 0.2% |
| CD27_CD8RO | 0.2% |
| Tconv mem_Tconv | 0.2% |
| CD4 Tconv_CD3 | 0.2% |

### mRMR (Top 10%)

**Base Method**: Raw feature selection frequencies across all bootstrap samples

| Feature | Selection Frequency (%) |
|---------|-------------------------|
| Bcells CD27posIgDneg_total | 51.5% |
| Tconv memDR_CD3 | 46.0% |
| CD8 RO DR_CD8 | 45.2% |
| Tconv memDR_mem | 38.2% |
| Tconv memDR_total | 38.0% |
| CD14+16+mono_CD3neg | 37.8% |
| myeloid_CD3neg | 37.5% |
| Tconv memDR_Tconv | 36.2% |
| CD14+16+mono_total | 34.0% |
| Tconv memCCR5_mem | 32.5% |
| Bcells_total | 30.8% |
| DR_CD8RO | 30.0% |
| nonTnonB_CD3neg | 29.0% |
| CD8 RA naive_CD3 | 28.7% |
| CD8 RO CCR5_total | 28.5% |
| CD8 RO CCR5_CD3 | 28.2% |
| Bcells_CD3neg | 27.3% |
| CD8 RO DR_CD3 | 27.0% |
| NKCD16_NK | 23.8% |
| NKCD16_nonTnonB | 23.5% |
| Bcells naive_total | 23.0% |
| Bcells naive_CD3neg | 21.2% |
| CD27negIgDneg_Bcells | 21.0% |
| CD14+16+mono_myeloid | 20.2% |
| CD8 RA naive_total | 19.0% |
| NK Ki67_nonTnonB | 19.0% |
| CCR5_CD8RO | 18.5% |
| Bcells memory_CD3neg | 17.2% |
| NK_nonTnonB | 17.0% |
| NKCD56hi_NK | 16.8% |
| Tconv memCD27_CD3 | 16.2% |
| CD8 RA_CD3 | 15.8% |
| CD8 RA CCR7 naive_CD8 | 15.0% |
| Tconv memCD27_Tconv | 14.8% |
| CD8 RA_total | 13.8% |
| Treg memory_CD3 | 13.0% |
| NK Ki67_NK | 13.0% |
| Treg naive_CD4 | 12.5% |
| Bcells memory_total | 12.0% |
| CD8 RO CD56_CD8 | 12.0% |
| naive_Bcells | 12.0% |
| Tconv mem_Tconv | 11.5% |
| Tconv memCCR6_mem | 11.0% |
| Tconv naive_Tconv | 11.0% |
| CD8pos_total | 10.8% |
| CD27IgD_Bcells | 10.5% |
| CD56_CD8RO | 10.5% |
| CD16mono_myeloid | 10.2% |
| CD4neg_total | 10.0% |
| Tconv mem_CD3 | 9.8% |
| nonTnonB_total | 9.8% |
| NKCD56hi_total | 9.8% |
| NK Ki67_total | 9.5% |
| CD4 Treg _CD3 | 9.5% |
| Tconv memCCR5_Tconv | 9.5% |
| CD3hi_CD4neg | 9.5% |
| Tconv memCXCR3_mem | 8.8% |
| myeloid_total | 8.8% |
| CD14mono_CD3neg | 8.5% |
| CD8 RO CCR4_total | 8.5% |
| CD8 RO DR_total | 8.2% |
| NKCD16_CD3neg | 8.2% |
| CXCR3_CD8RO | 8.0% |
| CD8 RO Ki67_total | 7.8% |
| Tconv memCCR4_mem | 7.5% |
| Tconv memCCR5_CD3 | 7.5% |
| CD8 RO CXCR3_CD3 | 7.5% |
| Tconv memCCR5_total | 7.2% |
| Tconv memTIGIT_mem | 7.2% |
| NK Ki67_CD3neg | 7.0% |
| CD8 RO TIGIT_total | 7.0% |
| Treg naive_CD3 | 7.0% |
| CD8 RO CCR6_CD8 | 6.5% |
| CD8 RO intB7_CD3 | 6.2% |
| Tconv memintB7_mem | 6.2% |
| Tconv naive_CD3 | 6.0% |
| CD8 RO Ki67_CD8 | 6.0% |
| CD8 RO CCR5_CD8 | 6.0% |
| CD8 RO CD27_CD3 | 6.0% |
| CD8 RO CD56_total | 6.0% |
| NKCD16_total | 5.8% |
| CD8 RA_CD8 | 5.5% |
| memory_Bcells | 5.5% |
| CD8pos_CD3 | 5.5% |
| CD3hi_total | 5.5% |
| Bcells Ki67_CD3neg | 5.5% |
| Tconv memCCR4_total | 5.5% |
| CD8 RO_total | 5.2% |
| Tconv memKi67_total | 5.2% |
| Ki67_Bcells | 5.2% |
| intB7_CD8RO | 5.0% |
| NK_total | 4.8% |
| CD8 RO CD27_total | 4.8% |
| Tconv memintB7_CD3 | 4.8% |
| CD8 RO PD1_CD8 | 4.5% |
| CCR4_CD8RO | 4.5% |
| NK_CD3neg | 4.5% |
| Treg memory_total | 4.5% |
| CD8 RO CCR6_CD3 | 4.2% |
| CD4 Treg_CD4 | 4.2% |
| CD8 RO CD56_CD3 | 4.0% |
| Treg memory_CD4 | 4.0% |
| Tconv memCCR4_Tconv | 4.0% |
| TIGIT_CD8RO | 4.0% |
| CD3hi_CD3 | 4.0% |
| Tconv memCCR4_CD3 | 4.0% |
| CCR6_CD8RO | 3.8% |
| NKCD56hi_CD3neg | 3.8% |
| CD4 Tconv_CD3 | 3.8% |
| Tconv memTIGIT_total | 3.5% |
| CD8 RO_CD8 | 3.5% |
| Tconv memCCR6_Tconv | 3.2% |
| CD8 RO TIGIT_CD3 | 3.2% |
| Ki67_CD8RO | 3.2% |
| CD8 RO CXCR3_CD8 | 3.2% |
| Tconv memCXCR3_Tconv | 3.0% |
| CD8 RO CXCR3_total | 3.0% |
| Tconv memintB7_total | 2.8% |
| Tconv memCD56_mem | 2.8% |
| CD3neg_total | 2.8% |
| Tconv memPD1_CD3 | 2.8% |
| Tconv naive_total | 2.8% |
| Bcells Ki67_total | 2.8% |
| Tconv memCCR6_CD3 | 2.8% |
| CD8 RO CCR6_total | 2.8% |
| Tconv memCCR6_total | 2.5% |
| CD4 Treg_total | 2.5% |
| Tconv memKi67_mem | 2.5% |
| CD14mono_myeloid | 2.5% |
| CD4 Tconv_total | 2.5% |
| Tconv memTIGIT_CD3 | 2.5% |
| CD16mono_CD3neg | 2.5% |
| CD8 RO intB7_total | 2.5% |
| CD8 RO CD27_CD8 | 2.5% |
| Tconv memCD27_mem | 2.5% |
| CD3pos_total | 2.5% |
| CD8  RO Ki67_CD3 | 2.2% |
| CD8 ncytotox RO CCR4_CD8ntox | 2.2% |
| CD8 ncytotox RO CCR4_CD3 | 2.2% |
| CD4neg_CD3 | 2.2% |
| Tconv memintB7_Tconv | 2.2% |
| PD1_CD8RO | 2.2% |
| CD14mono_total | 2.0% |
| CD8 RO intB7_CD8 | 2.0% |
| Tconv memPD1_Tconv | 2.0% |
| Treg naive_total | 1.8% |
| Tconv memCXCR3_CD3 | 1.8% |
| CD8 RO_CD3 | 1.8% |
| Tconv memCD56_total | 1.8% |
| Tconv memKi67_CD3 | 1.8% |
| Tconv memPD1_mem | 1.8% |
| CD27_CD8RO | 1.5% |
| Tconv memCD27_total | 1.5% |
| Tconv memCD56_CD3 | 1.5% |
| Tconv memCD56_Tconv | 1.5% |
| Bcells CD27negIgDneg_total | 1.2% |
| Tconv memPD1_total | 1.2% |
| CD8 RO PD1_total | 1.2% |
| Tconv memCXCR3_total | 1.2% |
| Tconv memTIGIT_Tconv | 1.0% |
| CD16+mono_total | 1.0% |
| CD8 RO TIGIT_CD8 | 0.8% |
| Tconv memKi67_Tconv | 0.8% |
| CD4 Tconv mem_total | 0.5% |
| CD8 RO PD1_CD3 | 0.5% |
| NKCD56hi_nonTnonB | 0.2% |

