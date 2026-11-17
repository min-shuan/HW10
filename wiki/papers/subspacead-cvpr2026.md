# Paper Note: SubspaceAD — Training-Free Few-Shot Anomaly Detection via Subspace Modeling

## Source Role

**Relevant**

本論文直接研究 training-free few-shot Visual Anomaly Detection / Localization，符合 Topic Relevance Check。[Source: `raw/06_subspacead.pdf`, pp.1-3]

## Research Problem

作者關注 practical few-shot industrial anomaly detection：每個 category 只有少量 normal images。論文質疑在 foundation-model features 已具強 representation 能力時，是否仍需要 memory bank、auxiliary data 或 vision-language prompt tuning 等複雜設計。[Source: `raw/06_subspacead.pdf`, pp.1-2]

## Main Contribution

SubspaceAD 使用 frozen DINOv2-G patch features 與 PCA normal subspace，在不進行 training、prompt tuning 或建立 memory bank 的情況下，以 reconstruction residual 進行 anomaly detection / localization。[Source: `raw/06_subspacead.pdf`, pp.1, 3-4]

## Method

1. 從少量 normal images 與 rotation augmentations 抽取 DINOv2-G patch tokens。
2. 聚合多個 intermediate layers。
3. 以 PCA 建立 normal feature subspace。
4. 將 test patch 投影到 normal subspace。
5. 以 reconstruction residual 作為 patch-level anomaly score。
6. 聚合 tail patch scores 得到 image-level score。[Source: `raw/06_subspacead.pdf`, pp.3-5]

## Datasets

主要使用 MVTec AD 與 VisA。[Source: `raw/06_subspacead.pdf`, p.5]

## Evaluation

Few-shot setting 使用 k ∈ {1, 2, 4} normal images；image-level 報告 AUROC / AUPR，pixel-level 報告 AUROC / PRO。主要實驗使用 5 個 random seeds。[Source: `raw/06_subspacead.pdf`, pp.5-6]

## Key Results

1-shot Table 1：
- MVTec AD：97.1 ± 0.9 I-AUROC、98.6 ± 0.4 I-AUPR、97.5 ± 0.1 P-AUROC、93.7 ± 0.2 PRO
- VisA：93.4 ± 0.7 I-AUROC、93.1 ± 0.8 I-AUPR、98.2 ± 0.1 P-AUROC、93.5 ± 0.2 PRO

論文另在 batched 0-shot setting 報告 96.6% MVTec AD 與 94.1% VisA image-level AUROC；此 protocol 與一般 prompt-based zero-shot / few-shot 不同。[Source: `raw/06_subspacead.pdf`, pp.6-7]

## Strengths

依作者結論，方法以簡單 PCA statistical model 搭配 frozen foundation features，在 one-/few-shot setting 中達到強勁 anomaly detection / localization performance，同時避免 memory bank、prompt tuning、auxiliary dataset 與 iterative training。[Source: `raw/06_subspacead.pdf`, pp.1, 7-8]

## Limitations

論文沒有獨立 general limitations section。本次 ingest 不自行補入來源未明示的 limitation。Ablation 顯示 method performance 對 backbone scale、feature aggregation、input resolution 與 PCA variance threshold 等設定有不同程度敏感度。[Source: `raw/06_subspacead.pdf`, pp.7-8]

## Related Wiki Entries

- [SubspaceAD](../methods/subspacead.md)
- [Normality Modeling](../concepts/normality-modeling.md)
- [Pretrained Visual Features 與 DINOv2](../concepts/pretrained-visual-features.md)
- [Zero-shot 與 Few-normal-shot Anomaly Detection](../concepts/zero-few-shot-anomaly-detection.md)

## References

1. Camile Lendering, Erkut Akdag, Egor Bondarev. *SubspaceAD: Training-Free Few-Shot Anomaly Detection via Subspace Modeling*. CVPR 2026. Source file: `raw/06_subspacead.pdf`.
