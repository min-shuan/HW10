# Normality Modeling

## Overview

在本 Wiki 中，Normality Modeling 用來描述「只利用正常樣本建立正常資料表示，再用測試樣本與正常表示的偏離程度判斷 anomaly」的做法。PatchCore 是目前已 ingest 來源中的一個具體例子：它只使用 nominal images 建立 patch-level feature memory bank，測試時再以 test patch 與 memory bank 中最近鄰 feature 的距離估計異常程度。[Source: `raw/03_patchcore.pdf`, pp.1, 3-5]

## Patch-level Normal Representation

PatchCore 不直接以整張影像的單一 high-level feature 表示正常資料，而是從 ImageNet-pretrained backbone 的 intermediate / mid-level feature maps 取得 patch-level representations。作者指出，太深層的 features 會更偏向 ImageNet classification，而過度局部的 features 又可能缺乏足夠 context，因此方法使用 local neighbourhood aggregation 增加 patch representation 的 receptive field，同時保留較高 spatial resolution。[Source: `raw/03_patchcore.pdf`, pp.3-4]

## Memory Bank

所有 nominal training images 的 locally aware patch features 會被集合成 memory bank `M`。由於完整 memory bank 可能非常大，PatchCore 再使用 greedy coreset subsampling 保留 feature-space coverage，同時降低 storage 與 nearest-neighbour inference cost。[Source: `raw/03_patchcore.pdf`, pp.4-5]

## Using Deviation as Anomaly Evidence

測試時，PatchCore 對 test image 的 patch feature 尋找 memory bank 中最近鄰 feature。距離越大，代表該 patch 與正常 patch representation 越不相似。Image-level anomaly score 由最異常的 patch 為核心計算，pixel-level anomaly localization 則利用各 patch 的 anomaly score 重新對齊到影像空間。[Source: `raw/03_patchcore.pdf`, p.5]


## PCA Subspace as Normality Model

SubspaceAD 提供另一種 normality representation：不保存所有 normal patch features，而是使用 frozen DINOv2-G 抽取 normal patch features，並以 PCA 建立低維 normal subspace。測試 patch 投影到該 subspace 後，其 reconstruction residual 被視為 anomaly evidence。[Source: `raw/06_subspacead.pdf`, pp.3-4]

這與 PatchCore 的 memory-bank nearest-neighbour 路線不同。PatchCore 保存 representative normal patches，SubspaceAD 則將 normal variation 壓縮為 PCA mean 與 basis。兩者都以「與 normal representation 的偏離」判斷 anomaly，但 representation 與 scoring mechanism 不同。[Source: `raw/03_patchcore.pdf`, pp.4-5] [Source: `raw/06_subspacead.pdf`, pp.3-4]

## Boundary of This Entry

本頁目前以 PatchCore 與 SubspaceAD 兩種機制呈現 Normality Modeling：前者以 patch-feature memory bank 表示正常資料，後者以 PCA subspace 表示 normal variation。本頁不將這兩種做法擴張成所有 anomaly detection 方法的一般定義。

## References

1. Karsten Roth, Latha Pemula, Joaquin Zepeda, Bernhard Schölkopf, Thomas Brox, Peter Gehler. *Towards Total Recall in Industrial Anomaly Detection*. CVPR 2022. Source file: `raw/03_patchcore.pdf`.
2. Camile Lendering, Erkut Akdag, Egor Bondarev. *SubspaceAD: Training-Free Few-Shot Anomaly Detection via Subspace Modeling*. CVPR 2026. Source file: `raw/06_subspacead.pdf`.
