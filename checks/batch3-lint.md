# Batch 3 Lint Report

## Batch

- `raw/05_winclip.pdf`
- `raw/06_subspacead.pdf`
- Date: 2026-11-17

## 1. Topic Relevance Check

### WinCLIP

- Result: **Relevant**
- Reason: 論文直接研究 zero-shot 與 few-normal-shot Visual Anomaly Classification / Segmentation，且在 MVTec AD 與 VisA 評估。

### SubspaceAD

- Result: **Relevant**
- Reason: 論文直接研究 training-free few-shot Visual Anomaly Detection / Localization，以 DINOv2 patch features 與 PCA normal subspace 進行 anomaly scoring。

**Result: PASS**

---

## 2. Programmatic Check

### File / Structure

本批新增：

- `wiki/concepts/zero-few-shot-anomaly-detection.md`
- `wiki/methods/winclip.md`
- `wiki/methods/subspacead.md`
- `wiki/papers/winclip-cvpr2023.md`
- `wiki/papers/subspacead-cvpr2026.md`

本批更新：

- `wiki/concepts/normality-modeling.md`
- `wiki/concepts/pretrained-visual-features.md`
- `wiki/index.md`
- `wiki/log.md`

**Result: PASS**

### Internal Links

所有新建與更新的 Markdown internal links 均能解析到現有檔案。

**Result: PASS**

### Citation Target Check

本批 source markers 使用：

- `raw/05_winclip.pdf`
- `raw/06_subspacead.pdf`
- 既有 comparison context 中的 `raw/03_patchcore.pdf`

以上檔案皆存在於專案 `raw/`。

**Result: PASS**

### Required Paper Note Sections

WinCLIP 與 SubspaceAD paper notes 均包含：

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

本批所有新建 Wiki content pages 均包含段落級 Source marker 與頁尾 References。

**Result: PASS**

---

## 3. Numeric Check

### WinCLIP

已回查 `raw/05_winclip.pdf` Abstract：

- MVTec AD zero-shot classification AUROC = **91.8%**: PASS
- MVTec AD zero-shot segmentation AUROC = **85.1%**: PASS
- VisA zero-shot classification AUROC = **78.1%**: PASS
- VisA zero-shot segmentation AUROC = **79.6%**: PASS
- MVTec AD 1-normal-shot WinCLIP+ classification / segmentation AUROC = **93.1% / 95.2%**: PASS
- VisA 1-normal-shot WinCLIP+ classification / segmentation AUROC = **83.8% / 96.4%**: PASS

### SubspaceAD

已回查 `raw/06_subspacead.pdf` Table 1：

#### 1-shot
- MVTec AD I-AUROC = **97.1 ± 0.9**: PASS
- MVTec AD I-AUPR = **98.6 ± 0.4**: PASS
- MVTec AD P-AUROC = **97.5 ± 0.1**: PASS
- MVTec AD PRO = **93.7 ± 0.2**: PASS
- VisA I-AUROC = **93.4 ± 0.7**: PASS
- VisA I-AUPR = **93.1 ± 0.8**: PASS
- VisA P-AUROC = **98.2 ± 0.1**: PASS
- VisA PRO = **93.5 ± 0.2**: PASS

#### 4-shot
- MVTec AD I-AUROC = **97.9 ± 0.4**: PASS
- MVTec AD I-AUPR = **99.0 ± 0.2**: PASS
- MVTec AD P-AUROC = **97.8 ± 0.1**: PASS
- MVTec AD PRO = **94.3 ± 0.0**: PASS
- VisA I-AUROC = **94.7 ± 0.2**: PASS
- VisA I-AUPR = **94.3 ± 0.5**: PASS
- VisA P-AUROC = **98.4 ± 0.0**: PASS
- VisA PRO = **93.8 ± 0.2**: PASS

#### Batched 0-shot
- MVTec AD image-level AUROC = **96.6%**: PASS
- VisA image-level AUROC = **94.1%**: PASS

### SubspaceAD Method Parameters

- Few-shot k ∈ {1, 2, 4}: PASS
- PCA explained-variance threshold τ = **0.99** in main setting: PASS
- Normal augmentation count Na = **30**: PASS
- Main feature extractor = frozen **DINOv2-G**: PASS

**Result: PASS**

---

## 4. Cross-paper Check

### Zero-shot vs Few-normal-shot

WinCLIP zero-shot does not use task-specific normal reference images. WinCLIP+ few-normal-shot adds K normal reference images and reference association.

Wiki keeps the two protocols separate and does not reuse 1-shot numbers as zero-shot results.

**Result: PASS**

### Few-shot vs Batched 0-shot in SubspaceAD

SubspaceAD paper explicitly distinguishes batched 0-shot from prompt-based zero-shot and few-shot settings.

Wiki stores few-shot Table 1 results separately from batched 0-shot Table 2 results.

**Result: PASS**

### DINOv2 Source Role

Batch 2 marked DINOv2 as **Supporting Source** because the DINOv2 paper itself does not propose anomaly detection.

Batch 3 adds a direct downstream link only because SubspaceAD explicitly uses frozen DINOv2-G patch features. The Wiki does not retroactively claim that the DINOv2 authors proposed this anomaly detection pipeline.

**Result: PASS**

### Normality / Anomaly Evidence Mechanisms

- PatchCore: patch-feature memory bank + nearest neighbour
- WinCLIP: language-guided state prototypes; WinCLIP+ adds normal reference memories
- SubspaceAD: PCA normal subspace + reconstruction residual

These mechanisms remain distinct in the Wiki.

**Result: PASS**

---

## 5. Technical Fidelity Review

### WinCLIP

Verified against Sections 4.1–4.3:

1. Compositional Prompt Ensemble builds normal / anomalous text prototypes.
2. Sliding-window CLIP features provide dense, language-aligned local evidence.
3. WinCLIP performs zero-shot AC / AS.
4. WinCLIP+ incorporates normal-reference association for few-normal-shot AC / AS.

Wiki does not describe naive CLIP patch features as equivalent to WinCLIP window features.

**Result: PASS**

### SubspaceAD

Verified against Sections 3.2–3.4 and Figure 2:

1. Frozen DINOv2-G extracts patch features.
2. Multiple intermediate layers are aggregated.
3. Normal features fit a PCA subspace.
4. Test features are projected to the subspace.
5. Squared reconstruction residual provides patch anomaly score.
6. Patch scores are aggregated for image-level prediction.

Wiki pipeline matches the source.

**Result: PASS**

### Limitations

Neither paper is assigned invented general limitations.

- WinCLIP: Wiki only records problems explicitly motivating its design, such as naive CLIP's limitations for anomaly tasks and dense alignment.
- SubspaceAD: Wiki only records design sensitivity supported by the paper's ablation study.

**Result: PASS**

---

## 6. Problems Found and Handling

1. **Potential issue:** WinCLIP and WinCLIP+ names are easy to collapse into one method and one protocol.
   - **Handling:** The Wiki separates zero-shot WinCLIP from few-normal-shot WinCLIP+ and keeps their inputs and reported numbers separate.

2. **Potential issue:** “few-shot” can refer to different supervision conditions across papers.
   - **Handling:** `zero-few-shot-anomaly-detection.md` records each paper's available information and protocol instead of treating all low-shot settings as equivalent.

3. **Potential issue:** SubspaceAD also reports batched 0-shot, which could be mistaken for WinCLIP-style zero-shot.
   - **Handling:** Batched 0-shot is explicitly marked as a different evaluation paradigm and its results are stored separately.

4. **Potential issue:** DINOv2 was previously a Supporting Source, while SubspaceAD directly uses DINOv2-G.
   - **Handling:** The downstream anomaly-detection claim is cited to SubspaceAD, not DINOv2.

5. **Potential issue:** PatchCore, WinCLIP+, and SubspaceAD all use normal-image information in different ways.
   - **Handling:** The Wiki preserves three mechanisms separately: memory bank, reference association, and PCA subspace.

---

## 7. Final Lint Result

**PASS with notes**

Batch 3 completes the six-source initial ingest set and may proceed to Retrieval / Coverage Check.
