# Grounding Check v1

## Goal
Verify that every important factual claim in `slides/page-drafts-v1.md` is supported by approved Evidence Cards / Wiki entries and that no unsupported factual content was introduced during per-page drafting.

## Result Summary
- Slides checked: **13 / 13**
- Slides with complete evidence mapping: **13 / 13**
- Unsupported factual claims found: **0**
- Claims revised during drafting to stay within evidence boundaries: **4**
- Final status: **PASS**

---

## Slide-by-slide Check

| Slide | Key claims checked | Evidence | Result | Notes |
|---|---|---|---|---|
| 1 | VAD task; image-level detection; pixel-level localization | Evidence 01 | PASS | No classification-theory comparison added. |
| 2 | normal-only / defect-scarce setting; normal + anomalous test data | Evidence 01 | PASS | Kept task description at benchmark-supported level. |
| 3 | MVTec AD / VisA sizes and structural descriptions | Evidence 02 | PASS | No claim that one benchmark is universally harder. |
| 4 | normal representation → deviation → anomaly evidence | Evidence 03 | PASS | Explicitly states methods differ; avoids universalizing mechanism. |
| 5 | PatchCore memory bank, coreset, nearest-neighbour scoring | Evidence 03, 04 | PASS | No performance number used, avoiding setup ambiguity. |
| 6 | pretrained features as feature source; role separation | Evidence 04 | PASS | DINOv2 is not described as an anomaly detector. |
| 7 | DINOv2 general-purpose features; SubspaceAD downstream use; LVD-142M count | Evidence 04 | PASS | Anomaly-use claim attributed to SubspaceAD context. |
| 8 | WinCLIP, WinCLIP+, SubspaceAD few-shot / batched 0-shot protocols | Evidence 05 | PASS | Protocols remain explicitly separated. |
| 9 | WinCLIP text prototypes, multi-scale features, WinCLIP+ references | Evidence 03, 05 | PASS | Avoids forcing WinCLIP into PatchCore-like normality modeling. |
| 10 | SubspaceAD DINOv2 tokens, PCA, reconstruction residual | Evidence 03, 04, 05 | PASS | Few-shot and batched 0-shot are not merged. |
| 11 | method comparison by representation / evidence mechanism | Evidence 03, 04, 05 | PASS | No cross-protocol performance ranking. |
| 12 | image/pixel evaluation; AU-ROC, AU-PR, PRO; imbalance caution | Evidence 06 | PASS | No formulas added. |
| 13 | four-question synthesis and method recap | Evidence 01, 03, 04, 05, 06 | PASS | Synthesis only; no new factual claim. |

---

## Revisions Made During Drafting

### 1. Slide 3: Dataset comparison wording
Potential risky wording: “VisA is harder than MVTec AD.”

**Action:** Removed ranking language. The draft only states source-supported differences in dataset scale and scene structure.

### 2. Slide 6–7: DINOv2 role
Potential risky wording: “DINOv2 is a foundation anomaly detector.”

**Action:** Reframed DINOv2 strictly as a general-purpose pretrained / self-supervised feature source. Its anomaly-detection connection is attributed to downstream use in SubspaceAD.

### 3. Slide 8: Zero-shot protocol
Potential risky wording: treating WinCLIP zero-shot and SubspaceAD batched 0-shot as the same experimental setting.

**Action:** Added a protocol table and an explicit caution that the available information differs.

### 4. Slide 12: Metric explanation
Potential risky wording: adding mathematical definitions or formulas for AU-ROC, AU-PR, or PRO from model knowledge.

**Action:** Kept the slide at the usage / interpretation level supported by the current Wiki and sources.

---

## Known Boundaries Preserved

1. The current Wiki does not support a full theoretical comparison between VAD and conventional image classification.
2. The current Wiki does not support a universal difficulty ranking between MVTec AD and VisA.
3. DINOv2 is a supporting feature source, not a VAD method in its original paper.
4. WinCLIP zero-shot, WinCLIP+ few-normal-shot, SubspaceAD few-shot, and SubspaceAD batched 0-shot are distinct protocols.
5. The current Wiki does not support full mathematical derivations of AUROC, AUPR, or PRO.

---

## Decision
**GROUNDING CHECK = PASS**

The 13-page draft can proceed to HTML generation. The HTML renderer must preserve approved wording and must not add new factual claims.
