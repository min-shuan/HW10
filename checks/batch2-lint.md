# Batch 2 Lint Report

## Batch

- `raw/03_patchcore.pdf`
- `raw/04_dinov2.pdf`
- Date: 2026-11-17

## 1. Topic Relevance Check

### PatchCore

- Result: **Relevant**
- Reason: 論文直接研究 cold-start industrial Visual Anomaly Detection，並同時處理 image-level anomaly detection 與 pixel-level localization。

### DINOv2

- Result: **Supporting Source**
- Reason: 論文核心是 self-supervised general-purpose visual representation learning，沒有直接提出 anomaly detection 方法；但其 frozen image / patch-level features 可支援本 Wiki 的 Feature Representation / Foundation Model 背景知識。

**Result: PASS**

---

## 2. Programmatic Check

### File / Structure

- `wiki/index.md`: PASS
- `wiki/log.md`: PASS
- `wiki/concepts/normality-modeling.md`: PASS
- `wiki/concepts/pretrained-visual-features.md`: PASS
- `wiki/methods/patchcore.md`: PASS
- `wiki/metrics/pro.md`: PASS
- `wiki/papers/patchcore-cvpr2022.md`: PASS
- `wiki/papers/dinov2-tmlr2024.md`: PASS

### Internal Links

所有 Markdown internal links 均能解析到現有檔案。

**Result: PASS**

### Citation Target Check

本批 Wiki 內使用的 `raw/03_patchcore.pdf` 與 `raw/04_dinov2.pdf` source markers 均對應到專案內現有 PDF。

**Result: PASS**

### Required Paper Note Sections

兩篇 paper notes 均包含：

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

本批建立的 Wiki content pages 均包含段落級 Source marker 與頁尾 References。

**Result: PASS**

---

## 3. Numeric Check

### PatchCore

已回查 `raw/03_patchcore.pdf`：

- PatchCore-25% image-level AUROC = 99.1%: PASS
- PatchCore-25% pixel-wise AUROC = 98.1%: PASS
- PatchCore-10% PRO = 93.5%: PASS
- Higher-resolution / larger-backbone / ensemble PatchCore-1% image-level AUROC = 99.6%: PASS
- PatchCore-1% memory bank 表示 100× reduction: PASS

### DINOv2

已回查 `raw/04_dinov2.pdf`：

- LVD-142M final image count = 142,109,386: PASS
- ViT-g/14 semantic segmentation +ms results:
  - ADE20K = 53.0 mIoU: PASS
  - Cityscapes = 81.0 mIoU: PASS
  - Pascal VOC = 86.2 mIoU: PASS
- Evaluation 使用 frozen features，涵蓋 classification、retrieval、segmentation、depth 等 tasks: PASS

**Result: PASS**

---

## 4. Cross-paper Check

### Pretrained Features

PatchCore 使用 ImageNet-pretrained network 的 intermediate / mid-level patch features，目標是建立 nominal patch-feature memory bank。

DINOv2 研究 general-purpose self-supervised visual features，並未提出 PatchCore 的 normality modeling 或 anomaly scoring。

兩篇來源只在 `pretrained-visual-features.md` 中以「feature representation 背景」建立關聯，未合併為同一個 anomaly detection method。

**Result: PASS**

### DINOv2 Source Role

DINOv2 全部 Wiki 條目均標記為 Supporting Source context。未從 DINOv2 論文自行推導：

- anomaly score
- anomaly detection benchmark result
- DINOv2 在 MVTec AD / VisA 的表現
- DINOv2 必然優於其他 anomaly detection backbone

**Result: PASS**

---

## 5. Technical Fidelity Review

### PatchCore Pipeline

回查論文 Figure 2 與 Section 3：

1. nominal images -> pretrained encoder
2. locally aware patch features
3. patch-feature memory bank
4. greedy coreset subsampling
5. test patch nearest-neighbour search
6. image anomaly score / anomaly segmentation

Wiki pipeline 與來源一致。

**Result: PASS**

### PatchCore Anomaly Scoring

Wiki 僅描述 test patch 與 memory-bank nearest neighbour distance，以及論文的 image-level score re-weighting；沒有自行新增其他 scoring rule。

**Result: PASS**

### DINOv2 Feature Role

Wiki 保留論文的 general-purpose frozen visual feature framing，並記錄 image-level / patch-level evaluation、dense recognition 與 PCA / patch matching evidence。

沒有將 DINOv2 改寫為 anomaly detection model。

**Result: PASS**

### Limitations

兩篇來源均未被自行補上未明示的 anomaly-detection limitation。

- PatchCore：只記錄作者明確處理的 memory-bank size / inference cost 問題。
- DINOv2：保留 fairness / environmental analysis 與 future work 的原始脈絡，不將其改寫成 anomaly detection limitation。

**Result: PASS**

---

## 6. Problems Found and Handling

1. **Potential issue:** PatchCore abstract 報告最高 99.6% image-level AUROC，但 main table 的標準 PatchCore-25% / 10% / 1% 為 99.1 / 99.0 / 99.0。
   - **Handling:** Wiki 明確區分 main table 與 higher-resolution / larger-backbone / ensemble setup，避免將不同 experimental setting 混在一起。

2. **Potential issue:** DINOv2 容易因後續 anomaly detection papers 常使用其 features，而被誤寫為 Visual Anomaly Detection method。
   - **Handling:** Topic Relevance Check 標記為 Supporting Source；Wiki 只使用其 representation-learning evidence。

3. **Potential issue:** PatchCore 與 DINOv2 都涉及 pretrained visual features，容易被寫成同一條方法演進線並產生未經來源支持的因果關係。
   - **Handling:** 只建立「pretrained visual feature」概念連結，不主張 DINOv2 是 PatchCore 的直接組件或後繼方法。

4. **Potential issue:** PRO 的完整 metric 定義在 PatchCore 中只簡要說明並引用其他來源。
   - **Handling:** `metrics/pro.md` 只整理 PatchCore 明確描述的用途與結果，不自行補完整公式。

---

## 7. Final Lint Result

**PASS with notes**

Batch 2 可進入 Git commit。下一批來源應在此批 commit 後再開始 ingest。
