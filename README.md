# Tamweel — 90-Day Financing Default Risk Decision System

**Sarah Alanazi** · **SDA-DSC-211 — Advanced Machine Learning Methods** · **SDAIA Academy**

An end-to-end machine learning project for predicting 90-day financing default risk using information available at application time. The project covers leakage-aware validation, cost-sensitive decision policy, explainability, calibration, model selection, and capacity-constrained scoring.

## Project at a Glance

| Metric | Result |
|---|---:|
| Applications | 10,000 |
| Features | 22 |
| Default rate | ~8% |
| Final model | **Logistic Regression** |
| Mean OOF Average Precision | **0.39166** |
| Decision threshold | **0.16892** |
| Review capacity | **12%** |
| OOF flagged fraction | **11.37%** |

## Honest Validation

Post-application leakage features were excluded, validation respected time order, and customer grouping prevented the same customer from appearing across training and validation.

![Validation comparison](evidence/day2/day2_validation_comparison.png)

## Cost-Sensitive Decision Policy

The operating threshold was selected from out-of-fold predictions under the operational capacity constraint rather than using the default 0.5 threshold.

![Cost curve](evidence/day3/artifacts/cost_curve.png)

## Final Model Selection

Individual models and ensemble approaches were compared using time-aware out-of-fold evidence. **Logistic Regression** was retained because it achieved the highest mean OOF Average Precision and no ensemble passed the improvement gate.

![Ensemble comparison](artifacts/day5_ensemble_comparison.png)

## Challenge Batch

The final challenge batch contained **2,500 applications**. **330** exceeded the threshold, and the 12% capacity rule retained the highest-risk **300** applications.

![Challenge capacity](artifacts/day5_challenge_capacity.png)

## Regional Diagnostics

Regional behavior was reviewed as a monitoring diagnostic rather than a fairness certification.

![Regional diagnostics](artifacts/day5_policy_regions.png)

## Project Structure

- `notebooks/` — executed machine learning notebooks
- `artifacts/` — final metrics, figures, model outputs, and policy artifacts
- `evidence/` — evidence from the project development phases
- `reports/` — model and decision documentation
- `presentation/` — final presentation
- `submission/` — challenge predictions
- `scripts/` — reproducibility and inference utilities

## Workflow

**Baseline modeling → Honest validation → Cost-sensitive policy → Explainability & calibration → Final model selection → Challenge scoring**

## Final Status

**READY FOR HUMAN REVIEW** · Technical replay and evidence verification completed.

## Intended Use

Developed for educational purposes as part of **SDA-DSC-211 — Advanced Machine Learning Methods at SDAIA Academy**. This project is not intended to make autonomous real-world lending decisions.

---

## Training Program Reference

This project was completed as part of **SDA-DSC-211 — Advanced Machine Learning Methods** at **SDAIA Academy**.

Training program reference: [SDAIA Academy on GitHub](https://github.com/SDAIAAcademy)
