# Tamweel Lite | مشروعك النهائي

## الملخص التنفيذي
Logistic Regression was selected as the final model because it achieved the highest mean OOF Average Precision of 0.39166 and no ensemble provided sufficient improvement. The decision policy was selected using OOF evidence with a 12% capacity constraint. On the unlabeled challenge batch, 330 requests exceeded the threshold and the capacity rule retained 300 of 2,500 requests. Continued monitoring is required.

## Executive summary
Logistic Regression was selected as the final model because it achieved the highest mean OOF Average Precision of 0.39166 and no ensemble provided sufficient improvement. The decision policy was selected using OOF evidence with a 12% capacity constraint. On the unlabeled challenge batch, 330 requests exceeded the threshold and the capacity rule retained 300 of 2,500 requests. Continued monitoring of performance, calibration, capacity and regional diagnostics is required.

Decision: KEEP SINGLE / Logistic. Full-batch flags: 300/2500.

اقرأ reports/MODEL_CARD.md والسياسة في artifacts/final_policy.json. الحزمة للتدريب؛ ليست نتيجة تقييم نهائية أو إثبات تسليم. ادمج أدلة أيامك السابقة واحفظ الدفتر المنفذ والعرض.
