# VisA

## Dataset Purpose

Visual Anomaly (VisA) Dataset 是為 industrial anomaly classification 與 segmentation 建立的 benchmark。論文希望補足既有 benchmark 在物件複雜度、資料規模與 training setup 上的限制，並同時評估 1-class 與 2-class scenarios。[Source: `raw/02_visa.pdf`, pp.1-3]

## Data Scale

VisA 共包含 **10,821 張 high-resolution color images**，其中 **9,621 張 normal samples**、**1,200 張 anomalous samples**，涵蓋 **12 個 objects、3 個 domains**。所有影像皆提供 image-level 與 pixel-level annotations。[Source: `raw/02_visa.pdf`, pp.1, 8-9]

## Object Groups

論文將 12 個 subsets 分成幾種不同結構情境：

- **Complex structure**：PCB1、PCB2、PCB3、PCB4
- **Multiple instances**：Capsules、Candle、Macaroni1、Macaroni2
- **Single instance**：Cashew、Chewing gum、Fryum、Pipe fryum

VisA 中的 anomaly 包含 scratches、dents、color spots、cracks，以及 misplacement 或 missing parts 等 structural defects。[Source: `raw/02_visa.pdf`, p.8]

## Image Resolution and Annotation

論文指出影像使用 **4,000 × 6,000 high-resolution RGB sensor** 取得，並提供 image-level 與 pixel-level annotations。[Source: `raw/02_visa.pdf`, p.9]

## Evaluation Protocols

VisA 為每個 object 建立三類 evaluation protocols：

1. **1-class**：90% normal images 作為 training set，10% normal images 與全部 anomalous samples 作為 test set。
2. **2-class high-shot**：normal 與 anomalous images 各以 60% / 40% 分配到 train / test。
3. **2-class low-shot**：先以 20% / 80% 分配 normal 與 anomalous images 到 train / test，再從 training set 的兩個 classes 各抽取 k-shot，k = 5 或 10；結果取 5 次 random runs 的平均。[Source: `raw/02_visa.pdf`, pp.9-10]

## Evaluation Metrics

VisA 論文同時報告 **AU-PR** 與 **AU-ROC**。作者指出 anomaly detection 經常具有明顯 class imbalance，尤其 pixel-level segmentation 中 normal pixels 可能遠多於 anomalous pixels；在這類情況下，AU-ROC 可能呈現偏樂觀的表現，因此作者主張 AU-PR 能提供更有資訊量的補充評估。[Source: `raw/02_visa.pdf`, p.10]

## Comparison with MVTec AD

VisA 論文將 VisA 與 MVTec AD 比較時，強調 VisA 包含更複雜的 object structures、同一影像中的 multiple instances，以及更大的 object location variation。論文也指出 MVTec AD 有 5,354 張影像，而 VisA 有 10,821 張影像。[Source: `raw/02_visa.pdf`, pp.9-10]

## References

1. Yang Zou, Jongheon Jeong, Latha Pemula, Dongqing Zhang, Onkar Dabeer. *SPot-the-Difference Self-Supervised Pre-training for Anomaly Detection and Segmentation*. 2022. Source file: `raw/02_visa.pdf`.
