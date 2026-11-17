# Evidence Card 03 — Normality Modeling

## Teaching Topic
如何利用正常資料建立 anomaly evidence？

## Claim
PatchCore 與 SubspaceAD 都利用 normal data 建立表示，再以 test sample 與 normal representation 的偏離作為 anomaly evidence，但 representation 與 scoring mechanism 不同。

## Explanation
PatchCore 保存 representative normal patch features 作為 memory bank，使用 nearest-neighbour distance scoring；SubspaceAD 將 normal DINOv2 patch features 壓縮成 PCA subspace，再用 reconstruction residual scoring。WinCLIP 則使用 language-guided normal/anomalous prototypes，few-normal-shot 版本再加入 normal reference memories。

## Wiki Entry
- `wiki/concepts/normality-modeling.md`
- `wiki/methods/patchcore.md`
- `wiki/methods/winclip.md`
- `wiki/methods/subspacead.md`

## Original Source
- `raw/03_patchcore.pdf`
- `raw/05_winclip.pdf`
- `raw/06_subspacead.pdf`

## Important Numbers
無必要數字。

## Allowed Usage
可用於方法比較與 normality / anomaly evidence 的概念教學。

## Do Not Claim
不要把 WinCLIP 強制歸類為與 PatchCore、SubspaceAD 完全相同的 normality-modeling 機制。
