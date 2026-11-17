# WinCLIP / WinCLIP+

## Overview

WinCLIP 研究 zero-shot 與 few-normal-shot Visual Anomaly Classification (AC) / Anomaly Segmentation (AS)。方法以預訓練 CLIP 為基礎，透過 compositional prompt ensemble 與 multi-scale window features 建立 language-guided anomaly scores；WinCLIP+ 再加入少量 normal reference images。[Source: `raw/05_winclip.pdf`, pp.1-2, 4-6]

## Core Idea

WinCLIP 的核心假設是：normal / anomalous 屬於與物件情境相關的 state，language 可以幫助描述這些狀態；同時，pixel-level anomaly segmentation 需要比 CLIP global embedding 更局部的 visual evidence。因此方法同時改進 text prompt 與 dense / multi-scale feature extraction。[Source: `raw/05_winclip.pdf`, pp.2, 4]

## Input

### Zero-shot WinCLIP
- Test image
- Object label（若可用）
- Normal / anomalous state words 與 prompt templates

不使用 task-specific normal training images。[Source: `raw/05_winclip.pdf`, pp.3-4]

### Few-normal-shot WinCLIP+
在上述資訊外，再加入 K 個 normal reference images；論文聚焦 K = 1–4。[Source: `raw/05_winclip.pdf`, pp.1-3, 5-6]

## Feature Representation

WinCLIP 使用 CLIP image encoder，從 image-level、patch-level 與不同 window scales 建立 visual features。作者指出直接使用 ViT penultimate patch features 進行 zero-shot dense prediction時，與 language space 的 alignment 不足，因此提出 sliding-window feature extraction，利用每個 window 的 CLIP-aligned embedding保留局部資訊。[Source: `raw/05_winclip.pdf`, pp.4-5]

## Normality / Anomaly Representation

Zero-shot WinCLIP 以 **Compositional Prompt Ensemble (CPE)** 建立 normal 與 anomalous 兩個 text prototypes。CPE 組合 state words 與 anomaly-task-specific prompt templates，再平均 text embeddings 表示兩種 state。[Source: `raw/05_winclip.pdf`, p.4]

WinCLIP+ 額外利用 normal reference images，從 patch、small-window、mid-window features 建立 reference memories，讓 anomaly 可同時由 language-defined state 與 normal visual references 描述。[Source: `raw/05_winclip.pdf`, pp.5-6]

## Anomaly Scoring

Zero-shot scoring 以 visual features 與 normal / anomalous text embeddings 的相似度形成 anomaly probability。Segmentation 會聚合多尺度 window scores；WinCLIP+ 再加入 reference association 產生的 visual anomaly maps，與 language-guided score 融合。[Source: `raw/05_winclip.pdf`, pp.4-6]

## Detection / Localization Pipeline

1. 組合 normal / anomalous state words 與 prompt templates。
2. 用 CLIP text encoder 建立兩個 state prototypes。
3. 用 CLIP image encoder 抽取 image / patch / multi-scale window features。
4. 計算 language-guided anomaly score。
5. Zero-shot：直接用 multi-scale scores 做 classification / segmentation。
6. Few-normal-shot：以 normal reference memories 建立 reference-based anomaly maps，再與 language-guided score 融合。[Source: `raw/05_winclip.pdf`, pp.4-6]

## Experimental Setting

論文在 MVTec AD 與 VisA 評估 zero-shot 與 few-normal-shot anomaly classification / segmentation。Few-normal-shot 使用 K = 1–4 normal images；主要模型使用 LAION-400M based CLIP ViT-B/16+。[Source: `raw/05_winclip.pdf`, pp.3, 6]

## Key Results

Abstract 報告：
- **MVTec AD zero-shot**：91.8% classification AUROC、85.1% segmentation AUROC
- **VisA zero-shot**：78.1% classification AUROC、79.6% segmentation AUROC
- **MVTec AD 1-normal-shot WinCLIP+**：93.1% classification AUROC、95.2% segmentation AUROC
- **VisA 1-normal-shot WinCLIP+**：83.8% classification AUROC、96.4% segmentation AUROC

這些數字屬於 WinCLIP / WinCLIP+ 的特定 zero-shot / 1-normal-shot protocol，不應與其他 shot settings 混用。[Source: `raw/05_winclip.pdf`, p.1]

## Strengths

依作者實驗，WinCLIP 讓預訓練 CLIP 在不做 task-specific tuning 的情況下處理 zero-shot anomaly classification / segmentation；WinCLIP+ 進一步利用少量 normal reference images，在 low-shot setting 中提升表現。[Source: `raw/05_winclip.pdf`, pp.1-2, 6-8]

## Limitations

論文主要正文沒有獨立 limitations section。本次 ingest 不自行新增來源未明示的 limitation。作者明確指出 naive CLIP adaptation 在 anomaly tasks 上表現不足，並將 dense visual features 與 anomaly-specific prompt design 視為需要處理的問題。[Source: `raw/05_winclip.pdf`, pp.1-4]

## Related Methods

- [PatchCore](patchcore.md)
- [SubspaceAD](subspacead.md)
- [Zero-shot 與 Few-normal-shot Anomaly Detection](../concepts/zero-few-shot-anomaly-detection.md)
- [MVTec AD](../datasets/mvtec-ad.md)
- [VisA](../datasets/visa.md)

## References

1. Jongheon Jeong, Yang Zou, Taewan Kim, Dongqing Zhang, Avinash Ravichandran, Onkar Dabeer. *WinCLIP: Zero-/Few-Shot Anomaly Classification and Segmentation*. CVPR 2023. Source file: `raw/05_winclip.pdf`.
