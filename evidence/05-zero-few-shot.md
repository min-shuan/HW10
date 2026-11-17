# Evidence Card 05 — Zero / Few-shot

## Teaching Topic
Zero-shot 與 Few-shot anomaly detection

## Claim
WinCLIP、WinCLIP+ 與 SubspaceAD 使用的 low-shot protocols 不同，不能把所有 zero/few-shot 結果直接視為同一設定。

## Explanation
WinCLIP zero-shot 不使用 task-specific normal images；WinCLIP+ 加入 K=1–4 normal references。SubspaceAD few-shot 使用 k∈{1,2,4} normal images 建 PCA subspace；其 batched 0-shot 使用整批 test tokens 擬合統計模型，與 prompt-based zero-shot 不同。

## Wiki Entry
- `wiki/concepts/zero-few-shot-anomaly-detection.md`
- `wiki/methods/winclip.md`
- `wiki/methods/subspacead.md`

## Original Source
- `raw/05_winclip.pdf`
- `raw/06_subspacead.pdf`

## Important Numbers
- WinCLIP+: K = 1–4 normal references
- SubspaceAD few-shot: k ∈ {1,2,4}

## Allowed Usage
可用來解釋 low-shot settings 與方法比較。

## Do Not Claim
不要把 SubspaceAD batched 0-shot 與 WinCLIP prompt-based zero-shot 混為相同 protocol。
