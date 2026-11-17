# MVTec AD

## Dataset Purpose

MVTec AD 是為 unsupervised anomaly detection 設計的 real-world industrial inspection benchmark。資料集使用 defect-free images 作為訓練資料，並以包含正常與異常樣本的 test set 評估 anomaly detection。[Source: `raw/01_mvtec-ad.pdf`, pp.1-2]

## Data Scale

資料集共包含 **5,354 張 high-resolution color images**，涵蓋 **5 個 texture categories** 與 **10 個 object categories**。論文列出 **73 種 defect types**；dataset table 中共有 **3,629 張 training images、467 張正常 test images、1,258 張 defective test images**，以及 **1,888 個 defect regions**。[Source: `raw/01_mvtec-ad.pdf`, pp.1-2, 4]

## Categories

### Textures

- Carpet
- Grid
- Leather
- Tile
- Wood

### Objects

- Bottle
- Cable
- Capsule
- Hazelnut
- Metal Nut
- Pill
- Screw
- Toothbrush
- Transistor
- Zipper

[Source: `raw/01_mvtec-ad.pdf`, pp.3-4]

## Annotation

所有 anomalous images 都提供 pixel-precise ground truth regions，因此資料集可同時支援 image-level anomaly classification 與 pixel-level anomaly segmentation 的評估。[Source: `raw/01_mvtec-ad.pdf`, pp.1-2, 5-6]

## Task Setting

MVTec AD 的 training set 只包含沒有 defect 的影像；test set 同時包含正常與具有多種 defect 的影像。異常可能是 surface defects，例如 scratches、dents，也可能是 structural defects，例如 object parts 的變形或缺失。[Source: `raw/01_mvtec-ad.pdf`, p.4]

## Evaluation Usage

原論文的 benchmark 同時評估 anomaly classification 與 segmentation。對 segmentation，論文除了使用 threshold-dependent 的 relative per-region overlap，也計算 threshold-independent 的 ROC AUC。[Source: `raw/01_mvtec-ad.pdf`, p.6]

## Notes for Comparison with VisA

VisA 論文指出，MVTec AD 相較 VisA 的物件結構較簡單、通常一個畫面只有單一物件，而且多數物件大致對齊；VisA 則納入更複雜結構、多實例與較大的位置變化。這是 VisA 論文對兩個 benchmark 的比較，應保留其來源脈絡。[Source: `raw/02_visa.pdf`, pp.9-10]

## References

1. Paul Bergmann, Michael Fauser, David Sattlegger, Carsten Steger. *MVTec AD — A Comprehensive Real-World Dataset for Unsupervised Anomaly Detection*. 2019. Source file: `raw/01_mvtec-ad.pdf`.
2. Yang Zou, Jongheon Jeong, Latha Pemula, Dongqing Zhang, Onkar Dabeer. *SPot-the-Difference Self-Supervised Pre-training for Anomaly Detection and Segmentation*. 2022. Source file: `raw/02_visa.pdf`.
