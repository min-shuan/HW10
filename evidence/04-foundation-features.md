# Evidence Card 04 — Foundation / Pretrained Visual Features

## Teaching Topic
Pretrained visual features 為什麼會出現在 anomaly detection？

## Claim
現有 Wiki 顯示 anomaly detection 方法可以重用 pretrained visual representations；DINOv2 提供 general-purpose self-supervised image / patch features，而 SubspaceAD 是使用 frozen DINOv2-G patch tokens 的直接 anomaly detection 例子。

## Explanation
PatchCore 使用 ImageNet-pretrained intermediate features；DINOv2 的原始論文建立可轉移到多種 computer vision tasks 的 general-purpose features；SubspaceAD 使用 frozen DINOv2-G patch features 建 PCA normal subspace。

## Wiki Entry
- `wiki/concepts/pretrained-visual-features.md`
- `wiki/methods/patchcore.md`
- `wiki/methods/subspacead.md`
- `wiki/papers/dinov2-tmlr2024.md`

## Original Source
- `raw/03_patchcore.pdf`
- `raw/04_dinov2.pdf`
- `raw/06_subspacead.pdf`

## Important Numbers
DINOv2 的 LVD-142M curated dataset: 142,109,386 images。此數字僅在需要介紹 DINOv2 pretraining scale 時使用。

## Allowed Usage
可說明 pretrained / self-supervised visual features 如何成為 anomaly method 的 feature source。

## Do Not Claim
DINOv2 原論文本身不是 Visual Anomaly Detection 方法。
