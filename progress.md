# CSC172 Data Mining and Analysis Project Progress Report
**Student:** Jemar John J Lumingkit, 2022-1991  
**Date:** 12/13/25  
**Repository:** [https://github.com/KINGSTING/CSC172-AssociationMining-Lumingkit](https://github.com/KINGSTING/CSC172-AssociationMining-Lumingkit)  
**Commits Since Proposal:** [9 commits] | **Last Commit:** [12/13/25]

## 📊 Project Status: COMPLETED
| Milestone | Status | Notes |
|-----------|--------|-------|
| Data Preprocessing | ✅ Completed | Continuous features discretized (Zero/Low/High) & One-Hot Encoded |
| Mining Engine | ✅ Completed | Apriori Algorithm implementation via `mlxtend` |
| Rule Optimization | ✅ Completed | Sensitivity analysis performed (Support: 0.01 vs 0.05 vs 0.10) |
| Visualization | ✅ Completed | Generated Co-occurrence Heatmaps & Scatter Plots |
| Final Evaluation | ✅ Completed | Extracted 1,531 high-quality attack signatures |

## 1. Dataset Progress
- **Source:** NSL-KDD Dataset (KDDTrain+_20Percent.txt)
- **Volume:** ~25,000 Network Connection Records.
- **Preprocessing applied:**
    - **Discretization:** Mapped continuous numerical columns (e.g., `duration`, `src_bytes`) into categorical bins (`Zero`, `Low`, `High`).
    - **Transaction Encoding:** Converted categorical features into a sparse boolean matrix suitable for Association Rule Mining.

**Sample data preview:**
> Note: Dataset successfully transformed from raw connection logs into transactional format for the Apriori algorithm.

## 2. Mining & Experiments Progress

**Metric Evaluation (Sensitivity Analysis)**
![Support vs. Confidence](https://github.com/KINGSTING/CSC172-AssociationMining-Lumingkit/blob/main/results/plots/04_rules_scatter.png)

**Current Metrics (Selected "Balanced" Model):**
| Metric | Value | Interpretation |
|--------|-------|-----|
| Min Support | 0.05 (5%) | Filters out noise while retaining significant attack patterns. |
| Min Confidence | 0.60 (60%) | Ensures generated rules have high predictive reliability. |
| Total Rules | 4,515 | Total associations found before filtering. |
| **Attack Signatures**| **1,531** | **Actionable rules mapping traffic patterns to specific attacks.** |

## 3. Challenges Encountered & Solutions
| Issue | Status | Resolution |
|-------|--------|------------|
| **Continuous Data Incompatibility** | ✅ Fixed | Apriori requires categorical data. Implemented a custom **Binning Logic** to categorize `src_bytes` and `duration` into discrete labels (Zero/Low/High). |
| **Rule Explosion** | ✅ Fixed | Initial runs with 1% support generated 16,000+ rules (too many to analyze). Tuned `min_support` to **0.05** to balance quantity vs. quality. |
| **"Black Box" Interpretability** | ✅ Fixed | Switched from opaque metrics to **Association Rules**, generating human-readable "IF-THEN" logic (e.g., *IF Flag=S0 THEN Attack=Neptune*). |
| **Noise Filtering** | ✅ Fixed | Applied post-mining filters to isolate rules where the *Consequent* specifically contained "Attack", discarding normal traffic correlations. |

## 4. Final Deliverables
- [x] **Full Pipeline:** Ingestion $\rightarrow$ Discretization $\rightarrow$ Apriori Mining completed.
- [x] **Rule Extraction:** 1,531 rules generated and saved to CSV.
- [x] **Visualization:** Heatmaps and Lift scatter plots generated.
- [x] **Documentation:** README.md updated with Abstract, Methodology, and References.
- [x] **Demo:** Detection GIF and video walkthrough finalized.