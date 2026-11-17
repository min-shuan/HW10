# Teaching Structure Check v1

## Goal
檢查 `slides/outline-v1.md` 是否符合初學者教學順序，並確認沒有在概念尚未建立前過早使用方法細節。

## Check Criteria
1. Task definition 是否早於 method introduction。
2. Dataset / training setting 是否早於 normality modeling。
3. Normality modeling 概念是否早於 PatchCore / SubspaceAD 細節。
4. Pretrained feature 概念是否早於 DINOv2 與 SubspaceAD feature use case。
5. Zero / few-shot protocol 是否早於 WinCLIP / SubspaceAD 的 low-shot comparison。
6. Method comparison 是否在三個代表方法皆已介紹後才出現。
7. Evaluation 是否能獨立理解，且沒有加入 Wiki 不支援的公式內容。
8. Final takeaway 是否只重組已教過的內容。
9. 每頁是否至少有一個對應 Evidence Card / Wiki entry。
10. 是否出現 unsupported claim 或超出 Known Boundaries 的內容。

## Results

| Check | Result | Notes |
|---|---|---|
| Task before methods | PASS | Slides 1–2 先建立任務與資料設定。 |
| Dataset before modeling | PASS | Slide 3 先具體化 benchmark，Slide 4 才進 normality modeling。 |
| Concept before PatchCore/SubspaceAD | PASS | Slide 4 先建立 normality modeling，Slides 5 / 10 再進方法。 |
| Feature concept before downstream use | PASS | Slides 6–7 先說 pretrained / DINOv2 features，Slide 10 再接 SubspaceAD。 |
| Protocol before low-shot method comparison | PASS | Slide 8 先定義 zero / few-shot protocols，Slides 9–10 再介紹方法。 |
| Comparison after method introduction | PASS | Slide 11 才整合 PatchCore / WinCLIP / SubspaceAD。 |
| Evaluation grounded | PASS | Slide 12 只使用 AU-ROC、AU-PR、PRO overview，不加入完整公式。 |
| Takeaway reuses prior concepts | PASS | Slide 13 以 data / feature / evidence / evaluation 四問收束。 |
| Evidence mapping complete | PASS | 13/13 slides 均有 evidence mapping。 |
| Unsupported claims | PASS WITH BOUNDARIES | 保留 classification comparison、dataset difficulty、metric formula、DINOv2 role 等限制。 |

## Structural Reasoning

此版刻意避免依論文發表順序排列，也避免「一篇 paper 一頁」成為文獻摘要。教學主軸改為：

`Task → Available Data → Benchmark → Normality Idea → Concrete Method → Feature Source → Low-shot Protocol → More Methods → Comparison → Evaluation → Takeaway`

這樣學生先理解問題與可用資訊，再理解模型如何建立 anomaly evidence，最後才比較不同方法。

## Known Boundaries Kept

- 不建立 Visual Anomaly Detection 與一般 image classification 的完整理論比較。
- 不宣稱 MVTec AD 或 VisA 其中一個客觀上比較難。
- DINOv2 只作為 Supporting Source / feature source。
- WinCLIP、WinCLIP+、SubspaceAD few-shot、SubspaceAD batched 0-shot 不混為同一 protocol。
- AUROC、AUPR、PRO 不做完整公式教學。
- 不使用跨 protocol performance 數字做方法排名。

## Result
**Teaching Structure = PASS**

可以進入下一節點：`Per-page Drafting → Grounding Check`。
