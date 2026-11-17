# Paper Note: SPot-the-Difference Self-Supervised Pre-training for Anomaly Detection and Segmentation

## Source Role

**Relevant**

本論文直接研究 anomaly detection / segmentation，並提出 VisA dataset 與 SPot-the-Difference (SPD) pre-training regularization。[Source: `raw/02_visa.pdf`, p.1]

## Research Problem

論文指出 industrial visual anomaly detection 面臨 anomaly samples 稀少、defects 常很小、製造場域要求高 accuracy，以及產品與檢測 domain 多樣等挑戰；作者同時認為當時常用 benchmark 與 pre-trained representation 仍不足以完整反映這些問題。[Source: `raw/02_visa.pdf`, pp.1-3]

## Main Contribution

論文主要包含兩項貢獻：

1. 提出 VisA dataset，包含 10,821 張 high-resolution color images、12 objects、3 domains，以及 image-level / pixel-level annotations。
2. 提出 SPot-the-Difference (SPD) regularization，讓 pre-trained representation 對局部 anomalous patterns 更敏感。[Source: `raw/02_visa.pdf`, pp.1, 3]

## Method

SPD 將 local perturbation 視為需要辨識的差異：使用 SmoothBlend 產生局部變化，將其作為 SPD negative，同時以 weak global augmentation 產生 SPD positive。訓練時降低 anchor 與 negative 的 similarity，並提高 anchor 與 positive 的 similarity，以促進 local sensitivity。[Source: `raw/02_visa.pdf`, pp.6-8]

## Datasets

主要 downstream evaluation 使用 VisA 與 MVTec AD；VisA 本身包含 9,621 normal 與 1,200 anomalous samples，共 12 objects。[Source: `raw/02_visa.pdf`, pp.1, 8-10]

## Evaluation

論文建立 1-class、2-class high-shot 與 5/10-shot low-shot protocols，並同時報告 AU-PR 與 AU-ROC；作者特別討論 class imbalance 下 AU-ROC 可能呈現偏樂觀結果的問題。[Source: `raw/02_visa.pdf`, pp.9-10]

## Key Results

論文報告 SPD 在 VisA 與 MVTec AD 的多種 pre-training baseline 上，能在多個 anomaly detection / segmentation settings 中帶來改善。Abstract 以 2-class high-shot segmentation 為例，報告 SPD 相較 SimSiam 與 supervised pre-training 的 AU-PR 分別提升 5.9% 與 6.8%。[Source: `raw/02_visa.pdf`, p.1]

## Strengths

依論文自身主張，SPD 能作為 regularization 搭配多種 self-supervised contrastive pre-training，也能延伸到 supervised pre-training；VisA 則補入更複雜物件結構、多實例、位置變化與不同 supervision settings。[Source: `raw/02_visa.pdf`, pp.1, 3, 8-10]

## Limitations

原論文主要本文沒有建立獨立 limitations section。本次 ingest 不自行補入來源未明確提出的限制。

## Related Wiki Entries

- [Visual Anomaly Detection 基本概念](../concepts/visual-anomaly-detection.md)
- [VisA](../datasets/visa.md)
- [SPot-the-Difference (SPD)](../methods/spd.md)
- [AU-ROC 與 AU-PR](../metrics/auroc-aupr.md)

## References

1. Yang Zou, Jongheon Jeong, Latha Pemula, Dongqing Zhang, Onkar Dabeer. *SPot-the-Difference Self-Supervised Pre-training for Anomaly Detection and Segmentation*. 2022. Source file: `raw/02_visa.pdf`.
