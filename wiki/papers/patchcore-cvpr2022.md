# Paper Note: Towards Total Recall in Industrial Anomaly Detection

## Source Role

**Relevant**

本論文直接研究 cold-start industrial Visual Anomaly Detection，並同時處理 image-level detection 與 anomaly localization。[Source: `raw/03_patchcore.pdf`, p.1]

## Research Problem

作者處理的情境是只有 nominal / non-defective training images 的 industrial anomaly detection。其目標是在未知 defect variations 的情況下，利用 normal samples 建立可同時支援 anomaly detection 與 localization 的方法。[Source: `raw/03_patchcore.pdf`, pp.1-2]

## Main Contribution

論文提出 PatchCore，以 neighbourhood-aware mid-level patch features 建立 nominal memory bank，並使用 greedy coreset subsampling 降低 memory / inference cost。測試時再以 nearest-neighbour matching 產生 image-level anomaly score 與 pixel-level localization。[Source: `raw/03_patchcore.pdf`, pp.1, 3-5]

## Method

方法包含三個主要模組：

1. Locally aware patch features
2. Coreset-reduced patch-feature memory bank
3. Nearest-neighbour based anomaly detection / localization

[Source: `raw/03_patchcore.pdf`, pp.3-5]

## Datasets

主要 benchmark 為 MVTec AD；論文另外在 Magnetic Tile Defects (MTD) 與 Mini Shanghai Tech Campus (mSTC) 測試方法。[Source: `raw/03_patchcore.pdf`, p.5]

## Evaluation

MVTec AD 主要報告 image-level AUROC、pixel-wise AUROC 與 PRO，並另外比較 inference time、coreset subsampling、feature hierarchy、low-shot setting 等。[Source: `raw/03_patchcore.pdf`, pp.5-8]

## Key Results

PatchCore-25% 在 MVTec AD main table 報告 **99.1% image-level AUROC** 與 **98.1% pixel-wise AUROC**；PatchCore-10% 的 PRO 為 **93.5%**。更高 resolution / larger backbone / ensemble 的 PatchCore-1% setup 最高報告 **99.6% image-level AUROC**。[Source: `raw/03_patchcore.pdf`, pp.6-7]

## Strengths

依作者實驗，PatchCore 的 coreset memory bank 可在大幅降低記憶體與 inference burden 的同時保留 anomaly detection / localization performance；論文也顯示其在 limited nominal data setting 中仍有競爭力。[Source: `raw/03_patchcore.pdf`, pp.6-8]

## Limitations

主要本文沒有獨立 limitations section。本次 ingest 不自行推論來源未明示的 limitation。方法中明確處理的 practical issue 包括 memory bank 隨資料量成長造成的 storage / inference cost，因此作者加入 coreset subsampling。[Source: `raw/03_patchcore.pdf`, pp.4-5]

## Related Wiki Entries

- [Normality Modeling](../concepts/normality-modeling.md)
- [Pretrained Visual Features 與 DINOv2](../concepts/pretrained-visual-features.md)
- [PatchCore](../methods/patchcore.md)
- [MVTec AD](../datasets/mvtec-ad.md)
- [PRO](../metrics/pro.md)

## References

1. Karsten Roth, Latha Pemula, Joaquin Zepeda, Bernhard Schölkopf, Thomas Brox, Peter Gehler. *Towards Total Recall in Industrial Anomaly Detection*. CVPR 2022. Source file: `raw/03_patchcore.pdf`.
