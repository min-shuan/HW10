# Batch 1 Lint Report

## Batch

- `raw/01_mvtec-ad.pdf`
- `raw/02_visa.pdf`
- Date: 2026-11-17

## 1. Topic Relevance Check

### MVTec AD

- Result: **Relevant**
- Reason: 論文直接建立並評估 unsupervised visual anomaly detection benchmark，涵蓋 image-level classification 與 pixel-level segmentation。

### VisA / SPD

- Result: **Relevant**
- Reason: 論文直接研究 anomaly detection / segmentation，提出 VisA dataset 與 SPD representation learning method。

**Result: PASS**

---

## 2. Programmatic Check

### File / Structure

- `wiki/index.md` exists: PASS
- `wiki/log.md` exists: PASS
- `wiki/concepts/`: PASS
- `wiki/datasets/`: PASS
- `wiki/methods/`: PASS
- `wiki/metrics/`: PASS
- `wiki/papers/`: PASS

### Internal Links

所有 Markdown 內部連結皆能解析到現有檔案。

**Result: PASS**

### Citation Target Check

所有 Wiki 段落中的 `raw/01_mvtec-ad.pdf` 與 `raw/02_visa.pdf` source markers 均對應到現有原始檔案。

**Result: PASS**

### Required Paper Note Sections

兩個 paper notes 均包含：

- Research Problem
- Main Contribution
- Method
- Datasets
- Evaluation
- Key Results
- Strengths
- Limitations
- Related Wiki Entries
- References

**Result: PASS**

### Reference Structure

除 `index.md` 與 `log.md` 外，本批建立的所有 Wiki content pages 均包含：

- 段落級 `[Source: ...]` 標記
- 頁尾 `References`

**Result: PASS**

---

## 3. Numeric Check

### MVTec AD

已回查原始論文：

- 5,354 high-resolution color images: PASS
- 5 texture categories + 10 object categories: PASS
- 73 defect types: PASS
- 3,629 training images: PASS
- 467 normal test images: PASS
- 1,258 defective test images: PASS
- 1,888 defect regions: PASS

### VisA

已回查原始論文：

- 10,821 images: PASS
- 9,621 normal samples: PASS
- 1,200 anomalous samples: PASS
- 12 objects: PASS
- 3 domains: PASS
- image-level + pixel-level annotations: PASS
- 4,000 × 6,000 RGB acquisition: PASS
- 1-class 90% normal train protocol: PASS
- 5/10-shot low-shot setting: PASS

**Result: PASS**

---

## 4. Cross-paper Check

### MVTec AD vs VisA Comparison

VisA 對 MVTec AD 的比較包含：

- VisA object structures 更複雜
- VisA 可包含 multiple instances
- VisA 涵蓋較大的 object location variation
- VisA 10,821 images，MVTec AD 5,354 images

這些比較只保留在標有 VisA source 的段落中，未改寫成 MVTec AD 作者自己的結論。

**Result: PASS**

### Evaluation Metrics

MVTec AD source：整理其 ROC AUC 與 relative per-region overlap 的 benchmark 使用方式。

VisA source：整理 AU-PR + AU-ROC，以及作者對 class imbalance 下 AU-ROC 可能偏樂觀的主張。

兩篇來源的 evaluation protocol 未被合併成單一標準。

**Result: PASS**

---

## 5. Technical Fidelity Review

### Visual Anomaly Detection concept

內容只使用兩篇來源對 industrial anomaly detection / segmentation 的任務描述與資料特性，未加入來源外的一般化定義。

**Result: PASS**

### SPD

- local perturbation 作為 SPD negative: PASS
- weak global augmentation 作為 SPD positive 的組成: PASS
- shared encoder / projection head: PASS
- SmoothBlend local perturbation: PASS
- SPD 是 representation pre-training regularization，而非獨立 normality modeling algorithm: PASS
- 未自行補 anomaly score: PASS

### Limitations

兩篇 paper notes 都沒有自行虛構 limitations。原文沒有主要本文獨立 limitations section，因此明確標示「不自行推論」。

**Result: PASS**

---

## 6. Problems Found and Handling

1. **Potential issue:** VisA paper 對 MVTec AD 提出 benchmark comparison，容易被錯寫成 MVTec AD 自己承認的 limitation。
   - **Handling:** 所有此類內容均保留 VisA citation context。

2. **Potential issue:** AU-ROC 與 AU-PR 容易被整理成一般性教科書定義。
   - **Handling:** 只保留兩篇來源實際描述的 evaluation usage 與 VisA 作者對 imbalance 的論述，不自行補公式或一般化定義。

3. **Potential issue:** SPD paper 同時含 dataset 與 method，容易把 SPD 當成完整 downstream anomaly detector。
   - **Handling:** `methods/spd.md` 明確區分 SPD 的 representation-learning role，並標記原文未定義通用 anomaly score。

---

## 7. Final Lint Result

**PASS**

Batch 1 可進入 Git commit。下一批來源在此 batch commit 完成前不應開始 ingest。
