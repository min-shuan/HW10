# Paper Note: MVTec AD — A Comprehensive Real-World Dataset for Unsupervised Anomaly Detection

## Source Role

**Relevant**

本論文直接研究 Visual Anomaly Detection benchmark，符合 Topic Relevance Check。[Source: `raw/01_mvtec-ad.pdf`, pp.1-2]

## Research Problem

作者指出當時缺少適合 real-world unsupervised anomaly detection 的 comprehensive dataset，尤其缺少能同時評估 image-level anomaly classification 與 pixel-level anomalous region segmentation 的資料。[Source: `raw/01_mvtec-ad.pdf`, pp.1-3]

## Main Contribution

論文提出 MVTec AD dataset，涵蓋 5 個 texture categories 與 10 個 object categories，總共 5,354 張 high-resolution color images，包含 defect-free training images、normal / anomalous test images，以及 anomalous regions 的 pixel-precise ground truth。作者並對多種當時的 unsupervised anomaly detection baselines 進行 benchmark。[Source: `raw/01_mvtec-ad.pdf`, pp.1-2]

## Method

本論文的核心貢獻是 dataset 與 benchmark，而非提出單一新的 anomaly detection model。Benchmark 評估包含 GAN-based、autoencoder-based、pre-trained CNN feature-based 與 traditional computer vision baselines。[Source: `raw/01_mvtec-ad.pdf`, pp.2-4]

## Datasets

MVTec AD：15 categories，包含 5 textures 與 10 objects；training set 只包含 defect-free images，test set 同時包含 normal 與 defective images。[Source: `raw/01_mvtec-ad.pdf`, pp.2-4]

## Evaluation

Classification 以正常與異常影像的正確分類表現進行評估；Segmentation 使用 relative per-region overlap，並另外計算 ROC AUC 作為 threshold-independent measure。[Source: `raw/01_mvtec-ad.pdf`, p.6]

## Key Results

作者的初始 benchmark 顯示，不同方法在不同 objects / defect categories 的表現差異明顯，且整體仍有 considerable room for improvement。[Source: `raw/01_mvtec-ad.pdf`, pp.2, 8-9]

## Strengths

依論文自身定位，MVTec AD 的主要優勢是提供多種 textures / objects、real-world industrial inspection context，以及 anomalous regions 的 pixel-precise ground truth，使 image-level 與 pixel-level evaluation 能在同一 benchmark 中進行。[Source: `raw/01_mvtec-ad.pdf`, pp.1-2, 9]

## Limitations

原論文沒有建立獨立 limitations section。本次 ingest 不自行增加來源未提出的限制。VisA 論文後續對 MVTec AD 的比較會保留在各自來源脈絡中，不回寫成 MVTec AD 作者自身的 limitation。[Source context: `raw/02_visa.pdf`, pp.9-10]

## Related Wiki Entries

- [Visual Anomaly Detection 基本概念](../concepts/visual-anomaly-detection.md)
- [MVTec AD](../datasets/mvtec-ad.md)
- [AU-ROC 與 AU-PR](../metrics/auroc-aupr.md)

## References

1. Paul Bergmann, Michael Fauser, David Sattlegger, Carsten Steger. *MVTec AD — A Comprehensive Real-World Dataset for Unsupervised Anomaly Detection*. 2019. Source file: `raw/01_mvtec-ad.pdf`.
