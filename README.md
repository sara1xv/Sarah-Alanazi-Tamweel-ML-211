# Tamweel — 90-Day Financing Default Risk Decision System
## نظام Tamweel للتنبؤ بمخاطر التعثر خلال 90 يومًا

**Student | المتدربة:** Sarah Alanazi  
**Course | الدورة:** SDA-DSC-211 — Advanced Machine Learning Methods | أساليب تعلم الآلة المتقدمة  
**Programme | البرنامج:** SDAIA Academy

> Educational learner project. This repository is not an official SDAIA repository and is not intended for autonomous real-world lending decisions.

## Project idea and problem | فكرة المشروع والمشكلة

Tamweel is an end-to-end machine learning decision system that estimates whether a financing applicant may default within 90 days using only information available at application time. It connects predictive modelling with honest validation, a simulated cost-sensitive review policy, explainability, calibration, operational capacity and reproducible inference.

## Architecture and learner journey | معمارية المشروع

**Synthetic data → Leakage control → Time/group validation → OOF model comparison → Cost/capacity policy → Explainability & calibration → Final model → Challenge scoring**

1. [Day 1 — Baseline & Boosting](notebooks/01_baseline_boosting.ipynb)
2. [Day 2 — Honest Validation & Optuna](notebooks/02_validation_tuning.ipynb)
3. [Day 3 — Cost-Sensitive Decision](notebooks/03_cost_sensitive_decision.ipynb)
4. [Day 4 — Explainability & Calibration](notebooks/04_explain_calibrate.ipynb)
5. [Day 5 — Final Model & Delivery](notebooks/05_final_model.ipynb)

## Data | البيانات

The synthetic course dataset contains **10,000 applications**, **22 application-time predictors**, and an observed default rate of about **8%**. The target is `default_within_90d`. Challenge labels remain unavailable and are not used for training, tuning, calibration or threshold selection.

[Data contract](data/data_contract.json) · [Training data](data/tamweel_train.csv) · [Challenge data](data/tamweel_challenge.csv)

## Honest validation | التحقق الصادق

Post-application leakage fields were removed. Model comparison uses forward time-aware validation with customer separation, and threshold selection uses honest out-of-fold predictions. Preprocessing is learned from training rows only.

![Honest validation comparison](evidence/day2/day2_validation_comparison.png)

## Final model | النموذج النهائي

**Logistic Regression** was retained because it achieved the highest mean OOF Average Precision (**0.39166**) and no ensemble passed the documented improvement gate.

![Final model comparison](artifacts/day5_ensemble_comparison.png)

| Final evidence | Result |
|---|---:|
| Mean OOF Average Precision | **0.39166** |
| OOF rows | **2,155** |
| Raw OOF threshold | **0.16892** |
| OOF flagged fraction | **11.37%** |
| Recall | **46.93%** |
| Precision | **34.29%** |
| Simulated decision loss | **1,111 units** |
| Capacity constraint | **12%** |

## Decision policy | سياسة القرار

The teaching policy uses simulated loss **10 × FN + 1 × FP** with review capacity not exceeding 12%. The threshold was selected from OOF development evidence, not the challenge batch.

![Cost-sensitive threshold evidence](evidence/day3/artifacts/cost_curve.png)

On the **2,500-row unlabeled challenge batch**, 330 requests exceeded the transported threshold and the frozen capacity rule retained **300**. No challenge performance metric is claimed because labels are unavailable.

![Challenge capacity](artifacts/day5_challenge_capacity.png)

## Explainability and calibration | التفسير والمعايرة

Day 4 used permutation importance and SHAP. `bureau_score` and `dti` were the strongest global SHAP drivers in that fitted model. SHAP values are model contributions in raw log-odds, not causal explanations.

On 1,733 Day 4 evaluation requests, sigmoid calibration improved Brier score from **0.1130 to 0.0671** and ECE from **0.1469 to 0.0225**. This evidence applies to the Day 4 model/evaluation period. Regional results are diagnostic only and are not a fairness certification.

![Regional diagnostics](artifacts/day5_policy_regions.png)

## Required reports | التقارير المطلوبة

- [Decision Card](evidence/day3/reports/DECISION_CARD.md)
- [Ensemble Decision](reports/ENSEMBLE_DECISION.md)
- [Model Card](reports/MODEL_CARD.md)
- Interpretability Report — generated from the executed Day 4 evidence and included in the final submission version.

## Environment and reproducibility | البيئة وإعادة الإنتاج

The assessed path is designed for free Google Colab CPU. Recorded environment: **Python 3.13.16**, seed **211**, `n_jobs=2`. Exact versions are in [environment.json](artifacts/environment.json), [requirements-colab.txt](requirements-colab.txt) and [constraints.txt](constraints.txt).

To reproduce:
1. Open Days 1–5 in order in Google Colab.
2. Use the pinned environment and included synthetic course data.
3. Run each notebook from a clean runtime with **Run all**.
4. Review generated artifacts and reports; do not edit metrics manually.
5. Use [scripts/inference.py](scripts/inference.py) for the final inference interface.
6. Compare outputs with [submission.csv](submission/submission.csv) and its [manifest](submission/submission_manifest.json).

## Outputs | المخرجات

[Final metrics](artifacts/final_metrics.json) · [Final policy](artifacts/final_policy.json) · [Final model](artifacts/final_model/model.json) · [Submission](submission/submission.csv) · [Presentation PDF](presentation/final_presentation.pdf) · [Technical check](artifacts/day5_project_check.json)

The recorded project check status is **READY_FOR_HUMAN_REVIEW**. This is technical evidence, not a grade or submission receipt.

## Limitations and responsible use | القيود والاستخدام المسؤول

The project uses synthetic educational data and simplified cost/capacity assumptions. OOF evidence does not guarantee future performance. Calibration, capacity, score distributions, drift and regional diagnostics require monitoring. The system must not be used as an autonomous real-world lending decision system.

## References and disclosure | المراجع والإفصاح

- [SDAIA Academy on GitHub](https://github.com/SDAIAAcademy)
- **SDA-DSC-211 — Advanced Machine Learning Methods | أساليب تعلم الآلة المتقدمة**
- Course-provided notebooks, synthetic data and instructional scaffolding were used as the learning foundation. Learner responses, executed outputs and project decisions are documented in this repository.
- External or AI assistance that materially affects the project should be disclosed rather than presented as independently authored evidence.

This learner repository does not represent an official SDAIA publication.
