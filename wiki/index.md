# Visual Anomaly Detection LLM Wiki

本 Wiki 以 Visual Anomaly Detection 為主題，內容由 `raw/` 中通過 Topic Relevance Check 的來源分批 ingest 而來。所有重要技術敘述與數字都應能追溯到原始來源。

## Concepts

- [Visual Anomaly Detection 基本概念](concepts/visual-anomaly-detection.md)
- [Normality Modeling](concepts/normality-modeling.md)
- [Pretrained Visual Features 與 DINOv2](concepts/pretrained-visual-features.md)
- [Zero-shot 與 Few-normal-shot Anomaly Detection](concepts/zero-few-shot-anomaly-detection.md)

## Datasets

- [MVTec AD](datasets/mvtec-ad.md)
- [VisA](datasets/visa.md)

## Methods

- [SPot-the-Difference (SPD)](methods/spd.md)
- [PatchCore](methods/patchcore.md)
- [WinCLIP / WinCLIP+](methods/winclip.md)
- [SubspaceAD](methods/subspacead.md)

## Metrics

- [AU-ROC 與 AU-PR](metrics/auroc-aupr.md)
- [PRO (Per-Region Overlap)](metrics/pro.md)

## Papers

- [MVTec AD — A Comprehensive Real-World Dataset for Unsupervised Anomaly Detection](papers/mvtec-ad-cvpr2019.md)
- [SPot-the-Difference Self-Supervised Pre-training for Anomaly Detection and Segmentation](papers/spot-the-difference-visa.md)
- [Towards Total Recall in Industrial Anomaly Detection](papers/patchcore-cvpr2022.md)
- [DINOv2 — Learning Robust Visual Features without Supervision](papers/dinov2-tmlr2024.md)
- [WinCLIP — Zero-/Few-Shot Anomaly Classification and Segmentation](papers/winclip-cvpr2023.md)
- [SubspaceAD — Training-Free Few-Shot Anomaly Detection via Subspace Modeling](papers/subspacead-cvpr2026.md)

## Ingest Log

- [log.md](log.md)
