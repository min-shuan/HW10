# PatchCore

## Overview

PatchCore 是用於 cold-start industrial anomaly detection 的方法，訓練時只需要 nominal / non-defective images。方法核心是建立一個具代表性的正常 patch-feature memory bank，測試時透過 nearest-neighbour feature matching 進行 image-level anomaly detection 與 pixel-level anomaly localization。[Source: `raw/03_patchcore.pdf`, pp.1, 3-5]

## Core Idea

PatchCore 的流程可以分成三個主要部分：

1. 從 pretrained backbone 抽取 locally aware patch features。
2. 將 nominal patch features 建成 memory bank，並用 greedy coreset subsampling 降低冗餘。
3. 測試時比較 test patch feature 與 normal memory bank 的最近鄰距離，產生 anomaly score 與 localization map。

[Source: `raw/03_patchcore.pdf`, pp.3-5]

## Input

Training input 為 nominal images；test input 可以是 nominal 或 anomalous image。PatchCore 將此設定描述為 cold-start / one-class industrial anomaly detection。[Source: `raw/03_patchcore.pdf`, pp.1, 3]

## Feature Representation

PatchCore 使用 ImageNet-pretrained network，並選擇 intermediate / mid-level feature hierarchies。作者的動機是保留局部 anomaly information、降低過深 feature 對 ImageNet classification 的偏向，同時維持 spatial resolution。方法再透過 local neighbourhood aggregation 建立 locally aware patch features。[Source: `raw/03_patchcore.pdf`, pp.3-4]

## Normality Modeling

所有 nominal images 的 patch-level representations 被加入 memory bank `M`。這個 memory bank 代表訓練資料中可觀察到的 normal patch context。[Source: `raw/03_patchcore.pdf`, p.4]

為降低 memory bank 大小與 inference cost，PatchCore 使用 greedy coreset subsampling。作者的目標是以較小的 subset 近似完整 memory bank 在 feature space 中的 coverage；論文也比較 coreset 與 random subsampling，指出 coreset 較能保留 feature-space coverage。[Source: `raw/03_patchcore.pdf`, pp.4, 7]

## Anomaly Scoring

對 test image 的每個 patch feature，PatchCore 尋找 memory bank 中最近鄰 normal feature。Image-level score 以距離最大的 test patch 為核心，再利用其鄰近 memory-bank features 進行 re-weighting。[Source: `raw/03_patchcore.pdf`, p.5]

## Detection / Localization Pipeline

論文 Figure 2 的流程為：nominal samples 經 pretrained encoder 轉成 neighbourhood-aware patch features，建立並 coreset-reduce memory bank；testing 時，test patch features 與 memory bank 做 nearest-neighbour search，產生 image-level anomaly score，並由每個 patch score 建立 anomaly segmentation。[Source: `raw/03_patchcore.pdf`, pp.4-5]

## Experimental Setting

主要實驗使用 MVTec AD。論文也在 Magnetic Tile Defects (MTD) 與 Mini Shanghai Tech Campus (mSTC) 上測試方法的延伸能力。MVTec AD 的主要 evaluation 包含 image-level AUROC、pixel-wise AUROC 與 PRO。[Source: `raw/03_patchcore.pdf`, p.5]

## Key Results

在論文的 MVTec AD main setting 中，PatchCore-25% 的 image-level AUROC 為 **99.1%**，pixel-wise AUROC 為 **98.1%**；PatchCore-10% 的 PRO 為 **93.5%**。作者進一步使用較高 resolution / larger backbones / ensemble 的 PatchCore-1% setup，報告最高 **99.6% image-level AUROC**。[Source: `raw/03_patchcore.pdf`, pp.6-7]

## Strengths Reported by the Paper

作者強調 PatchCore 能同時提供高 image-level detection 與 pixel-level localization performance，且 coreset subsampling 可大幅縮小 memory bank、降低 inference time，同時維持 performance。論文也報告 low-shot setting 中，使用一部分 nominal training data 仍可維持競爭力。[Source: `raw/03_patchcore.pdf`, pp.1, 6-8]

## Limitations

原論文主要本文沒有建立獨立 limitations section。本次 ingest 不自行新增作者未明確提出的限制。可確認的設計取捨包含 memory bank size / inference cost，因此作者使用 coreset subsampling 處理此問題；這裡只記錄方法設計所處理的問題，不擴寫為未被作者陳述的 limitation。[Source: `raw/03_patchcore.pdf`, pp.4-7]

## Related Methods

- SPADE
- PaDiM
- PatchSVDD

以上方法出現在 PatchCore 的 related work 或 benchmark 中。本批次只建立 PatchCore 完整 method page，不對其他方法補入來源外細節。[Source: `raw/03_patchcore.pdf`, pp.2-3, 6-7]

## Related Wiki Entries

- [Normality Modeling](../concepts/normality-modeling.md)
- [Pretrained Visual Features 與 DINOv2](../concepts/pretrained-visual-features.md)
- [MVTec AD](../datasets/mvtec-ad.md)
- [PRO](../metrics/pro.md)

## References

1. Karsten Roth, Latha Pemula, Joaquin Zepeda, Bernhard Schölkopf, Thomas Brox, Peter Gehler. *Towards Total Recall in Industrial Anomaly Detection*. CVPR 2022. Source file: `raw/03_patchcore.pdf`.
