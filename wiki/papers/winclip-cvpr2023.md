# Paper Note: WinCLIP — Zero-/Few-Shot Anomaly Classification and Segmentation

## Source Role

**Relevant**

本論文直接研究 zero-shot 與 few-normal-shot Visual Anomaly Classification / Segmentation，符合 Topic Relevance Check。[Source: `raw/05_winclip.pdf`, pp.1-3]

## Research Problem

既有 industrial anomaly detection 多為每個 inspection task 建立 bespoke model，並仰賴 task-specific normal images。作者研究更低資料需求的 zero-shot 與 few-normal-shot setting，同時處理 image-level anomaly classification 與 pixel-level anomaly segmentation。[Source: `raw/05_winclip.pdf`, pp.1-2]

## Main Contribution

1. 提出 anomaly-specific **Compositional Prompt Ensemble (CPE)**。
2. 提出 **WinCLIP**，以 CLIP 的 multi-scale window features 做 zero-shot anomaly classification / segmentation。
3. 提出 **WinCLIP+**，加入少量 normal reference images，以 visual reference association 補充 language-guided scores。
4. 在 MVTec AD 與 VisA 評估 zero-shot / few-normal-shot performance。[Source: `raw/05_winclip.pdf`, pp.1-2]

## Method

WinCLIP 以 normal / anomalous state words 與 prompt templates 建立 text prototypes，並以 sliding-window CLIP feature extraction 取得與 language 對齊且具局部資訊的 visual features。WinCLIP+ 另外從 normal reference images 建立多尺度 reference memories，再融合 language-guided 與 visual-reference anomaly scores。[Source: `raw/05_winclip.pdf`, pp.4-6]

## Datasets

主要 benchmark 為 MVTec AD 與 VisA。[Source: `raw/05_winclip.pdf`, p.6]

## Evaluation

論文分別評估 zero-shot 與 few-normal-shot anomaly classification / segmentation，few-normal-shot 聚焦 K = 1–4 normal reference images。[Source: `raw/05_winclip.pdf`, pp.3, 6-8]

## Key Results

Abstract 報告：
- WinCLIP zero-shot：MVTec AD 91.8% classification AUROC / 85.1% segmentation AUROC；VisA 78.1% / 79.6%。
- WinCLIP+ 1-normal-shot：MVTec AD 93.1% / 95.2%；VisA 83.8% / 96.4%。[Source: `raw/05_winclip.pdf`, p.1]

## Strengths

依作者實驗，WinCLIP 能在不進行 per-task tuning 的情況下執行 zero-shot AC / AS；WinCLIP+ 則利用少量 normal references 進一步改善 low-shot performance。[Source: `raw/05_winclip.pdf`, pp.1-2, 6-8]

## Limitations

主要正文沒有獨立 limitations section。本次 ingest 不自行補入來源未明示的 limitation。論文自身明確指出 naive CLIP 對 anomaly classification / segmentation 並不足夠，並以 prompt design 與 dense multi-scale features 解決這些問題。[Source: `raw/05_winclip.pdf`, pp.1-4]

## Related Wiki Entries

- [WinCLIP / WinCLIP+](../methods/winclip.md)
- [Zero-shot 與 Few-normal-shot Anomaly Detection](../concepts/zero-few-shot-anomaly-detection.md)
- [MVTec AD](../datasets/mvtec-ad.md)
- [VisA](../datasets/visa.md)

## References

1. Jongheon Jeong, Yang Zou, Taewan Kim, Dongqing Zhang, Avinash Ravichandran, Onkar Dabeer. *WinCLIP: Zero-/Few-Shot Anomaly Classification and Segmentation*. CVPR 2023. Source file: `raw/05_winclip.pdf`.
