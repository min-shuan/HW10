# SubspaceAD

## Overview

SubspaceAD 是一個 **training-free few-shot Visual Anomaly Detection** 方法。它使用 frozen DINOv2-G 抽取少量 normal images 的 patch-level features，再以 Principal Component Analysis (PCA) 建立 normal variation 的低維 subspace；test patch 對該 subspace 的 reconstruction residual 作為 anomaly score。[Source: `raw/06_subspacead.pdf`, pp.1, 3-4]

## Core Idea

作者提出的核心假設是：foundation model feature space 中，normal patch features 可近似落在低維 linear subspace，而 anomalous regions 會在 subspace 外留下較大的 reconstruction residual。因此方法不需要 memory bank、prompt tuning 或額外 training。[Source: `raw/06_subspacead.pdf`, pp.1, 3-4]

## Input

- 每個 category 的 k 個 normal images，k ∈ {1, 2, 4}
- Test image
- Frozen DINOv2-G feature extractor

方法不需要 anomaly samples 作為 few-shot fitting data。[Source: `raw/06_subspacead.pdf`, pp.1, 3-5]

## Feature Representation

SubspaceAD 使用 frozen DINOv2-G 的 patch tokens。論文不是只使用最後一層，而是從多個 intermediate layers 取得 tokens，並以 mean pooling 聚合，使 representation 同時保留 semantic 與 spatial detail。主要設定使用 DINOv2-G layers 22–28。[Source: `raw/06_subspacead.pdf`, p.3]

為了從極少量 normal images 建立較穩定的 covariance estimate，作者對每張 normal image 產生 Na = 30 個 rotation-based augmented views，再收集所有 patch features。[Source: `raw/06_subspacead.pdf`, p.4]

## Normality Modeling

所有 normal patch features 以 PCA 建模。PCA 由 empirical mean μ 與 covariance Σ 求得 principal components，並選擇能達到 explained variance threshold τ 的 top-r components。主要實驗採用 **τ = 0.99**。[Source: `raw/06_subspacead.pdf`, p.4]

## Anomaly Scoring

Test patch feature `x_p` 先投影至 normal PCA subspace：

`x_proj = μ + CC^T(x_p - μ)`

再以 squared reconstruction residual：

`S(x_p) = ||x_p - x_proj||²`

作為 patch-level anomaly score。較大的 residual 代表 patch feature 無法由 normal subspace 良好重建。[Source: `raw/06_subspacead.pdf`, p.4]

## Detection / Localization Pipeline

1. 從 k 個 normal images 與其 augmented views 抽取 DINOv2 patch features。
2. 聚合多個 intermediate layers。
3. 以 PCA 擬合 normal feature subspace。
4. Test image 抽取相同 feature representation。
5. 將 test patches 投影至 normal subspace。
6. 以 reconstruction residual 產生 anomaly map。
7. 以 top-tail patch scores 聚合成 image-level anomaly score。[Source: `raw/06_subspacead.pdf`, pp.3-5]

## Experimental Setting

主要 benchmark 為 MVTec AD 與 VisA，評估 1-, 2-, 4-shot。Image-level metrics 包含 AUROC 與 AUPR；pixel-level localization 使用 pixel-wise AUROC 與 PRO。主要設定使用 frozen DINOv2-G、672 px input resolution、PCA threshold τ = 0.99，並跨 5 個 random seeds 報告 mean ± standard deviation。[Source: `raw/06_subspacead.pdf`, pp.5-6]

## Key Results

Table 1 報告：

### 1-shot
- **MVTec AD**：97.1 ± 0.9 I-AUROC、98.6 ± 0.4 I-AUPR、97.5 ± 0.1 P-AUROC、93.7 ± 0.2 PRO
- **VisA**：93.4 ± 0.7 I-AUROC、93.1 ± 0.8 I-AUPR、98.2 ± 0.1 P-AUROC、93.5 ± 0.2 PRO

### 4-shot
- **MVTec AD**：97.9 ± 0.4 I-AUROC、99.0 ± 0.2 I-AUPR、97.8 ± 0.1 P-AUROC、94.3 ± 0.0 PRO
- **VisA**：94.7 ± 0.2 I-AUROC、94.3 ± 0.5 I-AUPR、98.4 ± 0.0 P-AUROC、93.8 ± 0.2 PRO

這些結果屬於論文 Table 1 的 few-shot protocol，不能與 batched 0-shot 或其他 experimental setup 混用。[Source: `raw/06_subspacead.pdf`, p.6]

## Batched 0-shot

SubspaceAD 另外評估 batched 0-shot：對整批 test tokens 擬合單一 PCA subspace。作者明確指出這種設定與 prompt-based zero-shot 或一般 few-shot paradigm 不同。Table 2 報告 MVTec AD 96.6% 與 VisA 94.1% image-level AUROC。[Source: `raw/06_subspacead.pdf`, pp.6-7]

## Strengths

依作者結論，SubspaceAD 以 frozen foundation features 與 PCA statistical model，在不使用 memory bank、auxiliary dataset、prompt tuning 或 training 的情況下進行 few-shot anomaly detection / localization，並在 MVTec AD 與 VisA 的 one-/few-shot setting 取得強勁結果。[Source: `raw/06_subspacead.pdf`, pp.1, 7-8]

## Limitations

論文沒有獨立 general limitations section。本次 ingest 不自行增加來源未明示的 limitation。Ablation 顯示 performance 會受到 backbone scale、layer aggregation、input resolution 與 PCA explained-variance threshold 等 design choices 影響。[Source: `raw/06_subspacead.pdf`, pp.7-8]

## Related Methods

- [Normality Modeling](../concepts/normality-modeling.md)
- [Pretrained Visual Features 與 DINOv2](../concepts/pretrained-visual-features.md)
- [Zero-shot 與 Few-normal-shot Anomaly Detection](../concepts/zero-few-shot-anomaly-detection.md)
- [PatchCore](patchcore.md)
- [WinCLIP / WinCLIP+](winclip.md)

## References

1. Camile Lendering, Erkut Akdag, Egor Bondarev. *SubspaceAD: Training-Free Few-Shot Anomaly Detection via Subspace Modeling*. CVPR 2026. Source file: `raw/06_subspacead.pdf`.
