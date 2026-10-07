# قرار التجميع

KEEP SINGLE — Logistic

I kept Logistic Regression as the final model because it achieved the highest mean OOF Average Precision of 0.39166. None of the ensemble methods passed the improvement gate, and the closest, Weighted, achieved 0.38942 with a negative lift of -0.00224.

The model comparison used 2,155 OOF requests across three forward periods. This provides time-aware validation evidence, but it does not guarantee the same performance on future data or changing populations.

الدليل: artifacts/ensemble_comparison.csv وday5_ensemble_gate.json. SD وصفي، وليس اختبار دلالة.
