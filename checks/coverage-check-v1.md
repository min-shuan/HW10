# Coverage Check v1

## Test Goal

驗證現有 Wiki 是否足以支撐 Visual Anomaly Detection 12–15 頁入門教學簡報的六個必要 coverage 類別。

## Test Rule

- 只能使用 `wiki/` 已存在內容。
- 不使用模型自身知識補齊缺口。
- 每個 retrieval 結果需保留 Wiki entry 與 original source。
- 若必要主題缺乏足夠 evidence，標記 `FAIL` 並回到 Retrieval。

## Results

| Topic | Result | Main Wiki Evidence | Notes |
|---|---|---|---|
| Task Definition | **PASS** | `wiki/concepts/visual-anomaly-detection.md`<br>`wiki/datasets/mvtec-ad.md`<br>`wiki/datasets/visa.md` | 足以支撐入門定義；與一般 classification 的更完整理論比較若要加入簡報，需額外來源。 |
| Dataset | **PASS** | `wiki/datasets/mvtec-ad.md`<br>`wiki/datasets/visa.md` | 數字與比較都有來源脈絡。 |
| Normality Modeling | **PASS** | `wiki/concepts/normality-modeling.md`<br>`wiki/methods/patchcore.md`<br>`wiki/methods/winclip.md` | 三種 anomaly evidence 機制可以清楚比較，但 WinCLIP 不應被硬套成與 PatchCore/SubspaceAD 相同的 normality-modeling 定義。 |
| Foundation Model | **PASS** | `wiki/concepts/pretrained-visual-features.md`<br>`wiki/methods/patchcore.md`<br>`wiki/methods/subspacead.md` | DINOv2 本身不被描述成 anomaly detector。 |
| Zero / Few-shot | **PASS** | `wiki/concepts/zero-few-shot-anomaly-detection.md`<br>`wiki/methods/winclip.md`<br>`wiki/methods/subspacead.md` | protocol 已分開，不混用。 |
| Evaluation | **PASS** | `wiki/metrics/auroc-aupr.md`<br>`wiki/metrics/pro.md`<br>`wiki/datasets/mvtec-ad.md` | 足以做教學簡報的 metric overview；若要教完整公式，需補專門 metric 來源。 |

## Retrieval Records

### 1. Task Definition

**Query**：什麼是 Visual Anomaly Detection？它和一般影像分類有什麼差異？

**Retrieved answer**：Wiki 將 Visual Anomaly Detection 定義為在影像中辨識與正常資料不同的異常樣本，並在需要時定位異常區域。MVTec AD 與 VisA 都支援 image-level detection；兩者也提供 pixel-level annotations，可支援 localization / segmentation。現有 Wiki 沒有建立「一般影像分類」的正式比較條目，因此測試只保留 Wiki 明確支援的差異：VAD 同時關注 anomaly presence 與 anomaly location，且常出現在 defect-scarce / normal-only training setting。

**Wiki entries**：
- `wiki/concepts/visual-anomaly-detection.md`
- `wiki/datasets/mvtec-ad.md`
- `wiki/datasets/visa.md`

**Original sources**：
- `raw/01_mvtec-ad.pdf`
- `raw/02_visa.pdf`

**Coverage**：PASS

**Note**：足以支撐入門定義；與一般 classification 的更完整理論比較若要加入簡報，需額外來源。

### 2. Dataset

**Query**：MVTec AD 與 VisA 分別提供什麼資料與標註？兩者有什麼差異？

**Retrieved answer**：MVTec AD 含 5,354 張高解析度彩色影像、15 個 categories、73 種 defect types，異常影像提供 pixel-precise ground truth。VisA 含 10,821 張高解析度彩色影像、12 個 objects、3 個 domains，所有影像提供 image-level 與 pixel-level annotations；VisA 論文並指出其包含較複雜 object structure、multiple instances 與較大位置變化。

**Wiki entries**：
- `wiki/datasets/mvtec-ad.md`
- `wiki/datasets/visa.md`

**Original sources**：
- `raw/01_mvtec-ad.pdf`
- `raw/02_visa.pdf`

**Coverage**：PASS

**Note**：數字與比較都有來源脈絡。

### 3. Normality Modeling

**Query**：PatchCore、WinCLIP、SubspaceAD 如何表示正常性或異常證據？

**Retrieved answer**：PatchCore 以 nominal patch features 建立 memory bank，透過 test patch 與最近鄰 normal feature 的距離形成 anomaly evidence。WinCLIP 的 zero-shot 路線以 normal / anomalous text prototypes 與 multi-scale visual features建立 language-guided anomaly scores；WinCLIP+ 再加入 normal reference memories。SubspaceAD 以少量 normal DINOv2 patch features 經 PCA 建立 normal subspace，再以 reconstruction residual 作為 anomaly score。

**Wiki entries**：
- `wiki/concepts/normality-modeling.md`
- `wiki/methods/patchcore.md`
- `wiki/methods/winclip.md`
- `wiki/methods/subspacead.md`

**Original sources**：
- `raw/03_patchcore.pdf`
- `raw/05_winclip.pdf`
- `raw/06_subspacead.pdf`

**Coverage**：PASS

**Note**：三種 anomaly evidence 機制可以清楚比較，但 WinCLIP 不應被硬套成與 PatchCore/SubspaceAD 相同的 normality-modeling 定義。

### 4. Foundation Model

**Query**：DINOv2 在這個 Wiki 中扮演什麼角色？哪些 anomaly detection 方法使用 pretrained visual features？

**Retrieved answer**：DINOv2 在 Wiki 中被標記為 Supporting Source，用來提供 self-supervised general-purpose visual features 與 patch-level representation 的背景。PatchCore 使用 ImageNet-pretrained network 的 intermediate features；SubspaceAD 則直接使用 frozen DINOv2-G patch tokens 建立 PCA normal subspace。

**Wiki entries**：
- `wiki/concepts/pretrained-visual-features.md`
- `wiki/methods/patchcore.md`
- `wiki/methods/subspacead.md`
- `wiki/papers/dinov2-tmlr2024.md`

**Original sources**：
- `raw/03_patchcore.pdf`
- `raw/04_dinov2.pdf`
- `raw/06_subspacead.pdf`

**Coverage**：PASS

**Note**：DINOv2 本身不被描述成 anomaly detector。

### 5. Zero / Few-shot

**Query**：WinCLIP 與 SubspaceAD 的 zero-shot / few-shot 設定有什麼不同？

**Retrieved answer**：WinCLIP 的 zero-shot 不使用 task-specific normal images，依靠 CLIP 與 compositional prompts；WinCLIP+ 則加入 K=1–4 個 normal reference images。SubspaceAD 的 few-shot 使用 k∈{1,2,4} normal images 擬合 PCA subspace；其 batched 0-shot 會利用整批 test tokens 建立統計模型，因此 Wiki 明確不將它與 prompt-based zero-shot 視為同一 setting。

**Wiki entries**：
- `wiki/concepts/zero-few-shot-anomaly-detection.md`
- `wiki/methods/winclip.md`
- `wiki/methods/subspacead.md`

**Original sources**：
- `raw/05_winclip.pdf`
- `raw/06_subspacead.pdf`

**Coverage**：PASS

**Note**：protocol 已分開，不混用。

### 6. Evaluation

**Query**：Visual Anomaly Detection 常用哪些 image-level 與 pixel-level metric？

**Retrieved answer**：現有 Wiki 可支援 AU-ROC、AU-PR 與 PRO。MVTec AD 與後續方法同時使用 image-level 與 pixel-level AUROC；VisA 同時報告 AU-PR 與 AU-ROC，並指出 class imbalance 下 AU-ROC 可能過度樂觀；PatchCore 使用 PRO 評估 anomaly regions 的 overlap / recovery。現有 Wiki 刻意不補來源未展開的完整公式。

**Wiki entries**：
- `wiki/metrics/auroc-aupr.md`
- `wiki/metrics/pro.md`
- `wiki/datasets/mvtec-ad.md`
- `wiki/datasets/visa.md`

**Original sources**：
- `raw/01_mvtec-ad.pdf`
- `raw/02_visa.pdf`
- `raw/03_patchcore.pdf`

**Coverage**：PASS

**Note**：足以做教學簡報的 metric overview；若要教完整公式，需補專門 metric 來源。

## Overall Result

**Coverage = PASS**

六個必要類別目前都有可追溯 Wiki evidence，因此本輪不需要新增來源，可以進入 Evidence Card 與 Teaching Point Extraction。

### Known Boundaries

- 現有 Wiki 對「Visual Anomaly Detection 與一般 image classification 的一般理論比較」沒有獨立來源，因此只允許使用 Wiki 已明確支持的 task setting 差異。
- Evaluation 足以介紹 AU-ROC、AU-PR、PRO 的用途與來源脈絡，但現有 Wiki 不支援完整公式教學。
- DINOv2 只能作為 Supporting Source，不得描述成 anomaly detector。