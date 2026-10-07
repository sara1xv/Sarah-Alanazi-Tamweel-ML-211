# Interpretability Report | تقرير التفسير

## Scope | النطاق

This report documents the Day 4 interpretability, calibration and stability evidence produced by Sarah Alanazi's executed Tamweel Lite project. The explanations describe model behaviour and must not be interpreted as causal explanations, fairness certification or legal/compliance conclusions.

يوثق هذا التقرير أدلة اليوم الرابع الخاصة بالتفسير والمعايرة والاستقرار من تنفيذ مشروع Tamweel Lite. تفسر النتائج سلوك النموذج ولا تثبت السببية أو العدالة أو الامتثال.

## Global interpretation | التفسير العام

Permutation and SHAP evidence identified **bureau_score** and **dti** as the strongest global drivers. Their mean absolute SHAP values were **0.9042** and **0.5437**, respectively. Other important features included loan amount, savings balance, existing obligations, prior defaults, months employed, income, recent inquiries and credit utilisation.

SHAP values are contributions in **raw log-odds**, not probability points.

## Local example | مثال محلي

For request **TR-009585**, the strongest positive contributions were:

- bureau_score: **+2.27**
- dti: **+1.20**
- loan_amount_sar: **+0.20**

The raw model score was **0.9031**, while the calibrated probability was **0.4795**. Therefore, the raw score must not be interpreted directly as a 90.31% default probability.

## Calibration evidence | أدلة المعايرة

On **1,733 evaluation requests**, sigmoid calibration changed the diagnostics as follows:

| Metric | Raw | Sigmoid calibrated |
|---|---:|---:|
| Brier score | 0.1130 | **0.0671** |
| ECE | 0.1469 | **0.0225** |
| ROC-AUC | 0.7708 | 0.7708 |
| Average Precision | 0.2587 | 0.2587 |

Calibration improved Brier score in both **2024Q3** and **2024Q4**. The customer-cluster bootstrap 95% interval for Brier change was **-0.0542 to -0.0374**, remaining below zero for the observed evaluation period.

## Stability and capacity | الاستقرار والسعة

The transported calibrated threshold was **0.1733**.

- 2024Q3: 97 risk flags vs capacity 100 — within capacity.
- 2024Q4: 109 risk flags vs capacity 107 — capacity exceeded.
- Including near-threshold review cases increased candidate review to 109 and 122, exceeding capacity in both periods.

This produced **CAPACITY_REVIEW_REQUIRED** evidence. The evaluation period was used for diagnosis, not for retuning the frozen threshold.

## Interpretation limits | حدود التفسير

Feature contributions are model-dependence evidence, not causal reasons for default. Correlated variables can share predictive signal. The Day 4 explanations describe the Day 4 fitted model and should not automatically be attributed to a materially changed final model without renewed interpretation.

The observed calibration improvement supports the evaluated period only and does not guarantee future performance. Regional diagnostics are descriptive and are not a fairness certification.

## Evidence | الأدلة

Primary evidence is contained in the executed Day 4 notebook and `evidence/day4/day4_reflection.json`. The final Model Card separately records that Day 4 interpretation does not automatically transfer to a changed final model.
