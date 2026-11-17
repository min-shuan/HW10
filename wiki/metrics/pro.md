# PRO (Per-Region Overlap)

## Usage in PatchCore

PatchCore 在 MVTec AD anomaly segmentation 評估中，同時使用 pixel-wise AUROC 與 **PRO**。作者指出 PRO 用來考慮 connected anomaly components 的 overlap / recovery，並可較好地處理 MVTec AD 中 anomaly region size 不同的情況。[Source: `raw/03_patchcore.pdf`, p.5]

## Reported PatchCore Result

PatchCore 論文在 MVTec AD 上報告 PatchCore-10% 的 PRO 為 **93.5%**，PatchCore-25% 為 **93.4%**，PatchCore-1% 為 **93.1%**。[Source: `raw/03_patchcore.pdf`, p.7]

## Interpretation Boundary

本頁只整理 PatchCore 論文對 PRO 的用途與其報告結果。完整 PRO 定義與原始 metric protocol 應回到 PatchCore 引用的 MVTec / PRO 相關來源；本批次不自行補入來源未展開的公式。

## References

1. Karsten Roth et al. *Towards Total Recall in Industrial Anomaly Detection*. CVPR 2022. Source file: `raw/03_patchcore.pdf`.
