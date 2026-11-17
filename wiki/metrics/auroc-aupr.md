# AU-ROC 與 AU-PR

## AU-ROC in MVTec AD

MVTec AD 的 benchmark 在 anomaly segmentation 評估中，除了 threshold-dependent 的 relative per-region overlap，也計算 threshold-independent 的 ROC AUC。論文將 true positive rate 定義為正確判定為 anomalous 的 pixels 百分比，並以 ROC AUC 作為額外的 segmentation performance measure。[Source: `raw/01_mvtec-ad.pdf`, p.6]

## AU-ROC and AU-PR in VisA

VisA 同時報告 **Area Under Precision-Recall curve (AU-PR)** 與 **Area Under Receiver Operating Characteristic curve (AU-ROC)**。作者指出 AU-ROC 是 anomaly detection 常用 metric，但在 highly imbalanced data 中可能讓 performance 看起來過度樂觀。[Source: `raw/02_visa.pdf`, p.10]

在 anomaly segmentation 中，normal pixels 可能比 anomalous pixels 多數十到數百倍。VisA 論文指出，在 negatives 數量非常大的情況下，即使模型產生許多 false positives，false positive rate 仍可能很小，因此 AU-ROC 可能維持偏高；作者因此主張搭配 AU-PR 觀察 anomaly detection / segmentation 表現。[Source: `raw/02_visa.pdf`, p.10]

## Interpretation Boundary

本頁只整理兩篇來源明確討論的用途與比較，不額外提供來源未明示的公式推導或一般化 metric 教科書定義。

## References

1. Paul Bergmann, Michael Fauser, David Sattlegger, Carsten Steger. *MVTec AD — A Comprehensive Real-World Dataset for Unsupervised Anomaly Detection*. 2019. Source file: `raw/01_mvtec-ad.pdf`.
2. Yang Zou, Jongheon Jeong, Latha Pemula, Dongqing Zhang, Onkar Dabeer. *SPot-the-Difference Self-Supervised Pre-training for Anomaly Detection and Segmentation*. 2022. Source file: `raw/02_visa.pdf`.
