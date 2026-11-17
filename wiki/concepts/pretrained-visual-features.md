# Pretrained Visual Features 與 DINOv2

## Why Pretrained Features Matter

PatchCore 說明 industrial anomaly detection 可以直接利用 pretrained visual representations：其方法使用 ImageNet-pretrained network 的 intermediate features，將正常影像轉為 patch-level representations，再建立 normal memory bank。[Source: `raw/03_patchcore.pdf`, pp.1, 3-4]

DINOv2 的研究目標更廣泛。作者希望透過大規模 self-supervised pretraining 學到可直接轉移到多種 computer vision tasks 的 general-purpose visual features，並特別強調 image-level 與 patch-level information。[Source: `raw/04_dinov2.pdf`, pp.1-3]

## Self-supervised Feature Learning

DINOv2 不依賴人工分類標籤來建立 visual representation。論文重新設計並擴展 discriminative self-supervised learning recipe，並建立自動化 data filtering / rebalancing pipeline，從大規模 uncurated data 建立 **LVD-142M** curated dataset；論文附錄列出的最終資料量為 **142,109,386 images**。[Source: `raw/04_dinov2.pdf`, pp.2-4, 30]

## Frozen Features

DINOv2 評估時大量使用 frozen backbone features，再以 linear probe 或較輕量的 task head 測試 representation 品質。論文在 classification、retrieval、semantic segmentation 與 monocular depth 等多種 downstream tasks 中評估其 transferable features。[Source: `raw/04_dinov2.pdf`, pp.1, 12-18]

## Patch-level Information

DINOv2 特別檢查 patch-level features。論文在 semantic segmentation 與 depth estimation 等 dense tasks 上使用 frozen patch features，並進一步以 PCA 與 patch matching 展示 features 會形成 foreground / background、object parts 與跨影像對應等 emergent properties。[Source: `raw/04_dinov2.pdf`, pp.15-18]

## Relation to Visual Anomaly Detection

DINOv2 論文本身沒有提出 Visual Anomaly Detection 方法，因此在本 Wiki 中標記為 **Supporting Source**。它提供的知識角色是說明 self-supervised general-purpose visual features 與 patch-level representation 的來源背景；後續 anomaly detection 方法是否以及如何使用 DINOv2，必須由對應 anomaly detection 論文另外提供證據。[Source: `raw/04_dinov2.pdf`, pp.1-3, 15-18]


## DINOv2 as a Feature Source in SubspaceAD

SubspaceAD 提供一個直接的 downstream anomaly detection 例子：它使用 frozen DINOv2-G 的 patch tokens，並聚合多個 intermediate layers，再以 PCA 建立 normal subspace。這個 anomaly detection 用法的證據來自 SubspaceAD，而不是 DINOv2 原論文本身。[Source: `raw/06_subspacead.pdf`, pp.1, 3-4]

## References

1. Maxime Oquab et al. *DINOv2: Learning Robust Visual Features without Supervision*. Transactions on Machine Learning Research, 2024. Source file: `raw/04_dinov2.pdf`.
2. Karsten Roth et al. *Towards Total Recall in Industrial Anomaly Detection*. CVPR 2022. Source file: `raw/03_patchcore.pdf`.
3. Camile Lendering, Erkut Akdag, Egor Bondarev. *SubspaceAD: Training-Free Few-Shot Anomaly Detection via Subspace Modeling*. CVPR 2026. Source file: `raw/06_subspacead.pdf`.
