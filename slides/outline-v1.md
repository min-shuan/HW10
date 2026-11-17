# Teaching Slide Outline v1

## Deck Title
**From Normal to Abnormal: An Introduction to Visual Anomaly Detection**

## Target Audience
- Visual Anomaly Detection 初學者
- 具備基本 Machine Learning 概念，但沒有 Anomaly Detection 經驗的學生

## Teaching Goal
在 13 頁內建立一條完整入門路徑：先理解 Visual Anomaly Detection 的任務與資料設定，再認識 normality / anomaly evidence 的主要建模方式，接著理解 pretrained features 與 low-shot methods，最後用 evaluation 與 method comparison 收束。

---

## Slide 1 — What Are We Trying to Detect?
### Teaching Purpose
建立整份簡報的問題意識與學習目標。

### Core Message
Visual Anomaly Detection 關注影像中是否存在與正常資料不同的異常，並在需要時定位異常區域。

### Suggested Content
- Industrial inspection 作為主要情境
- 兩種輸出：image-level detection、pixel-level localization
- 今日路線：Task → Data → Normality Modeling → Low-shot Methods → Evaluation

### Evidence
- `evidence/01-task-definition.md`

### Guardrail
不延伸成 Visual Anomaly Detection 與一般 image classification 的完整理論比較。

---

## Slide 2 — The Basic Task Setting
### Teaching Purpose
讓初學者先理解模型「手上有什麼資料」。

### Core Message
工業 anomaly detection 常見 normal-only / defect-scarce setting，訓練資料可能只有正常樣本，測試時才同時看到 normal 與 defective images。

### Suggested Content
- Normal training samples
- Normal / anomalous test samples
- Classification 與 localization 兩種任務輸出
- 用簡單流程圖表示 train / test information flow

### Evidence
- `evidence/01-task-definition.md`

### Guardrail
只描述 Wiki 已支持的 task setting，不自行建立一般化的 anomaly detection taxonomy。

---

## Slide 3 — Two Benchmarks: MVTec AD and VisA
### Teaching Purpose
用真實 benchmark 讓任務具體化。

### Core Message
MVTec AD 與 VisA 都支援 industrial anomaly detection / segmentation，但資料規模與場景結構不同。

### Suggested Content
- MVTec AD: 5,354 images, 15 categories, 73 defect types
- VisA: 10,821 images, 12 objects, 3 domains
- VisA: complex structures, multiple instances, location variation
- 兩欄 comparison table

### Evidence
- `evidence/02-datasets.md`

### Guardrail
不直接宣稱哪個 dataset「比較難」。

---

## Slide 4 — A Core Idea: Model Normality First
### Teaching Purpose
從 dataset setting 導出方法設計動機。

### Core Message
當 anomaly samples 稀少時，可以先建立正常資料的 representation，再用 test sample 與正常 representation 的偏離形成 anomaly evidence。

### Suggested Content
- Normal data → representation of normality
- Test feature → compare with normal representation
- Large deviation → stronger anomaly evidence
- 先介紹概念，不進入方法細節

### Evidence
- `evidence/03-normality-modeling.md`

### Guardrail
不把此機制描述成所有 anomaly detection 方法的唯一原理。

---

## Slide 5 — PatchCore: Normality as a Memory Bank
### Teaching Purpose
提供第一個具體 normality modeling 方法。

### Core Message
PatchCore 保存 representative normal patch features，測試時以 nearest-neighbour distance 衡量 test patch 與正常資料的差異。

### Suggested Content
- Pretrained backbone → patch features
- Normal patch memory bank
- Coreset subsampling
- Nearest-neighbour distance
- Image-level score + anomaly map

### Evidence
- `evidence/03-normality-modeling.md`
- `evidence/04-foundation-features.md`
- `wiki/methods/patchcore.md`

### Guardrail
若使用 99.6% AUROC，必須註明是 higher-resolution / larger-backbone / ensemble 的額外設定，不與 main setting 混用。

---

## Slide 6 — Why Pretrained Visual Features Matter
### Teaching Purpose
回答「為什麼方法不從 raw pixels 直接比較」。

### Core Message
現有方法會重用 pretrained visual representations，將影像轉成具有語意與局部資訊的 feature，再進行 anomaly modeling。

### Suggested Content
- PatchCore: ImageNet-pretrained intermediate features
- DINOv2: general-purpose self-supervised image / patch features
- Frozen feature extractor 的概念
- feature source 與 anomaly detector 的角色分離

### Evidence
- `evidence/04-foundation-features.md`

### Guardrail
DINOv2 只能描述為 Supporting Source / feature source，不描述成 anomaly detector。

---

## Slide 7 — DINOv2 as a Feature Source
### Teaching Purpose
進一步建立 foundation / self-supervised feature 的具體概念，為 SubspaceAD 鋪路。

### Core Message
DINOv2 提供 general-purpose patch-level features；在本 Wiki 中，它的 anomaly-detection 關聯來自後續方法對這些 frozen features 的使用。

### Suggested Content
- Self-supervised representation
- Patch-level information
- Frozen features transferable to downstream tasks
- SubspaceAD 使用 frozen DINOv2-G patch tokens
- 可選補充：LVD-142M = 142,109,386 images

### Evidence
- `evidence/04-foundation-features.md`
- `wiki/concepts/pretrained-visual-features.md`

### Guardrail
若提到 SubspaceAD 的 anomaly use case，來源必須標為 SubspaceAD，而非 DINOv2 原論文。

---

## Slide 8 — Low-shot Settings Are Not All the Same
### Teaching Purpose
在介紹 WinCLIP / SubspaceAD 前先定義 protocol，避免方法比較混亂。

### Core Message
Zero-shot、few-normal-shot、few-shot 與 batched 0-shot 使用的可用資訊不同，不能把結果直接視為同一 protocol。

### Suggested Content
- WinCLIP zero-shot: no task-specific normal images
- WinCLIP+: K = 1–4 normal references
- SubspaceAD few-shot: k ∈ {1,2,4} normal images
- SubspaceAD batched 0-shot: uses batch test tokens to fit statistical model
- protocol comparison table

### Evidence
- `evidence/05-zero-few-shot.md`

### Guardrail
不把 SubspaceAD batched 0-shot 與 prompt-based zero-shot 視為相同 setting。

---

## Slide 9 — WinCLIP: Language-Guided Anomaly Evidence
### Teaching Purpose
介紹第二種與 normal-memory / subspace 不同的 anomaly evidence。

### Core Message
WinCLIP 透過 normal / anomalous text prototypes 與 multi-scale visual features形成 language-guided anomaly scores；WinCLIP+ 再加入少量 normal references。

### Suggested Content
- Compositional Prompt Ensemble
- normal / anomalous text prototypes
- image / patch / multi-scale window features
- zero-shot WinCLIP
- few-normal-shot WinCLIP+

### Evidence
- `evidence/03-normality-modeling.md`
- `evidence/05-zero-few-shot.md`
- `wiki/methods/winclip.md`

### Guardrail
不要把 WinCLIP 強制歸類成與 PatchCore / SubspaceAD 完全相同的 normality-modeling mechanism。

---

## Slide 10 — SubspaceAD: Normality as a PCA Subspace
### Teaching Purpose
介紹第三種 representation / scoring mechanism，並連回 DINOv2。

### Core Message
SubspaceAD 使用少量 normal DINOv2 patch features 建立 PCA normal subspace，再用 reconstruction residual 作為 anomaly score。

### Suggested Content
- k normal images
- frozen DINOv2-G patch tokens
- PCA subspace
- test patch projection
- reconstruction residual
- image-level aggregation

### Evidence
- `evidence/03-normality-modeling.md`
- `evidence/04-foundation-features.md`
- `evidence/05-zero-few-shot.md`
- `wiki/methods/subspacead.md`

### Guardrail
few-shot 與 batched 0-shot 結果分開；若列數字，要標明 protocol。

---

## Slide 11 — Three Ways to Build Anomaly Evidence
### Teaching Purpose
整合三個方法，讓學生看到共通問題與不同解法。

### Core Message
PatchCore、WinCLIP、SubspaceAD 都在回答「如何判斷 test feature 是否異常」，但依賴的 evidence source 與 scoring mechanism 不同。

### Suggested Comparison
| Method | Main Representation | Extra Information | Anomaly Evidence |
|---|---|---|---|
| PatchCore | normal patch memory bank | normal images | nearest-neighbour distance |
| WinCLIP | language prototypes + visual features | text prompts; optional normal refs | language / reference-guided score |
| SubspaceAD | PCA normal subspace | few normal images | reconstruction residual |

### Evidence
- `evidence/03-normality-modeling.md`
- `evidence/04-foundation-features.md`
- `evidence/05-zero-few-shot.md`

### Guardrail
比較 representation 與 protocol，不用不同 setup 的 performance number 直接下排名結論。

---

## Slide 12 — How Do We Evaluate Anomaly Detection?
### Teaching Purpose
建立閱讀 anomaly detection paper 時需要的 evaluation literacy。

### Core Message
Image-level 與 pixel-level performance 需要分開評估；AU-ROC、AU-PR、PRO 提供不同觀察角度，單一 metric 不足以完整描述結果。

### Suggested Content
- Image-level: anomaly classification / detection
- Pixel-level: localization / segmentation
- AU-ROC
- AU-PR
- PRO
- VisA 對 class imbalance 下 AU-ROC 可能偏樂觀的提醒

### Evidence
- `evidence/06-evaluation.md`

### Guardrail
不加入 AUROC、AUPR、PRO 的完整公式推導。

---

## Slide 13 — Takeaways: From Normal Data to Anomaly Evidence
### Teaching Purpose
收束整堂課，讓學生帶走一個可重用的思考框架。

### Core Message
理解 Visual Anomaly Detection 時，可以依序問四個問題：有哪些 training information？使用什麼 feature？如何表示 normal / anomalous evidence？如何評估 detection 與 localization？

### Suggested Content
1. **Data setting**: normal-only, zero-shot, few-shot?
2. **Feature source**: pretrained / foundation representation?
3. **Anomaly evidence**: memory bank, language guidance, subspace residual?
4. **Evaluation**: image-level + pixel-level metrics?

最後將三個代表方法放回此框架：PatchCore、WinCLIP、SubspaceAD。

### Evidence
- `evidence/01-task-definition.md`
- `evidence/03-normality-modeling.md`
- `evidence/04-foundation-features.md`
- `evidence/05-zero-few-shot.md`
- `evidence/06-evaluation.md`

### Guardrail
Takeaways 只重新組織前面已支持的內容，不加入新 claim。

---

## Source Mapping Summary

| Slide | Primary Evidence |
|---|---|
| 1 | Task Definition |
| 2 | Task Definition |
| 3 | Datasets |
| 4 | Normality Modeling |
| 5 | Normality Modeling + Foundation Features |
| 6 | Foundation Features |
| 7 | Foundation Features |
| 8 | Zero / Few-shot |
| 9 | Normality Modeling + Zero / Few-shot |
| 10 | Normality Modeling + Foundation Features + Zero / Few-shot |
| 11 | Normality Modeling + Foundation Features + Zero / Few-shot |
| 12 | Evaluation |
| 13 | Cross-evidence synthesis |

## Outline Status
**READY FOR PAGE DRAFTING**, subject to Teaching Structure Check v1.
