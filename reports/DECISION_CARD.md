# Tamweel Lite — Decision Card

**Status:** Ready for review; this does not indicate approval or a grade.  
**Evidence source:** LIVE · **Strategy:** weighted · **Rows:** 5,039 OOF

## Decision rule

The positive class, `default_within_90d=1`, represents a synthetic default event within 90 days after application. Each fold validates on later applications, excludes validation customers from training, and requires training outcomes to be mature before the validation period. Identifiers and dates are excluded from model inputs.

| Evidence | Value |
|---|---:|
| Capacity-constrained threshold | 0.6583471436014694 |
| Minimum-loss threshold without capacity constraint | 0.44863935722081005 |
| Recall | 40.89% |
| Precision | 29.85% |
| Pooled OOF AP | 0.3100 |
| Flags | 526 of 5,039 |
| FN / FP | 227 / 369 |
| Teaching loss | 2,639 units |
| Loss at threshold 0.5 | 2,403 units; capacity feasible: False |
| Change from threshold 0.5 | +236 units |
| Loss per 10,000 applications | 5,237.15 units |
| Regional false-positive-rate gap | 0.648 percentage points |

A score greater than or equal to **0.6583471436014694** produces a review flag within this exercise. It must not be used to autonomously approve or reject real financing applications. Full threshold precision should be preserved because rounding may change queue size.

## Cost and capacity policy

The teaching cost is **10 units for a false negative and 1 unit for a false positive**. Review capacity is limited to **12% per period**, rounded down.

Capacity evidence:
- Period 1: 137 / 195
- Period 2: 183 / 200
- Period 3: 206 / 207

The selected threshold satisfies the 12% capacity constraint in every period. The default threshold of 0.5 has lower teaching loss but is not capacity feasible, so the operational constraint changes the preferred threshold.

## Regional diagnostic

The regional FPR gap is approximately 0.65 percentage points. Western has the highest FPR at 8.29%, while Other has the lowest at 7.64%. This is a descriptive diagnostic and must not be interpreted as a fairness certification.

## Limitations

The threshold was selected using OOF development predictions rather than an independent final test. Weighted scores were not yet calibrated at this stage, cost assumptions are simplified, and the 12% capacity rule is a teaching policy. OOF predictions cover 5,039 eligible rows; 4,961 warm-up rows have no OOF prediction. Threshold selection and loss estimation use the OOF development targets, so this remains development evidence rather than final-test evidence. Challenge labels were not used.

Accuracy is misleading for this problem because defaults are rare. Predicting no flags for every application gives 92.38% accuracy while detecting 0% of defaults and producing a loss of 3,840 units.

OOF predictions are used because each prediction is generated for a row that was not used to train that fold's model. Training predictions would be optimistic, while challenge or final-test data must remain separate from development decisions.

Supporting evidence is available in the Day 3 artifacts, including threshold metrics, period capacity, regional audit, cost sensitivity, and the cost curve.
