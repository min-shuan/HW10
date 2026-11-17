# Evidence Card 06 — Evaluation

## Teaching Topic
Visual Anomaly Detection 如何評估？

## Claim
現有 Wiki 支援以 AU-ROC、AU-PR 與 PRO 說明 image-level / pixel-level evaluation；VisA 特別指出高度 class imbalance 下 AU-ROC 可能呈現偏樂觀結果，因此 AU-PR 可作為補充。

## Explanation
MVTec AD 與後續方法使用 ROC AUC / AUROC 評估 detection 或 segmentation；VisA 同時報告 AU-PR 與 AU-ROC；PatchCore 使用 PRO 評估 connected anomaly regions 的 overlap / recovery。

## Wiki Entry
- `wiki/metrics/auroc-aupr.md`
- `wiki/metrics/pro.md`
- `wiki/datasets/mvtec-ad.md`
- `wiki/datasets/visa.md`

## Original Source
- `raw/01_mvtec-ad.pdf`
- `raw/02_visa.pdf`
- `raw/03_patchcore.pdf`

## Important Numbers
無必要數字。

## Allowed Usage
可做 evaluation overview，說明為何不能只看單一 metric。

## Do Not Claim
現有 Wiki 不支援 AUROC、AUPR、PRO 的完整公式推導；需要公式教學時應補專門來源。
