# Ingest Log

## Batch 1 — MVTec AD + VisA

- **Date:** 2026-11-17
- **Sources:**
  - `raw/01_mvtec-ad.pdf`
  - `raw/02_visa.pdf`
- **Relevance Result:**
  - MVTec AD: Relevant
  - VisA / SPD: Relevant
- **Source Role:** Direct Visual Anomaly Detection sources
- **Wiki pages created:**
  - `wiki/concepts/visual-anomaly-detection.md`
  - `wiki/datasets/mvtec-ad.md`
  - `wiki/datasets/visa.md`
  - `wiki/methods/spd.md`
  - `wiki/metrics/auroc-aupr.md`
  - `wiki/papers/mvtec-ad-cvpr2019.md`
  - `wiki/papers/spot-the-difference-visa.md`
  - `wiki/index.md`
- **Wiki pages updated:** `wiki/log.md`
- **Lint result:** PASS with notes. See `checks/batch1-lint.md`.
- **Problems found:**
  1. 兩篇來源對 evaluation 的重點不同，因此 metric page 保留來源脈絡，不將兩篇的 evaluation protocol 合併成單一標準。
  2. VisA 對 MVTec AD 的限制與比較只標示為 VisA paper 的觀點，不回寫成 MVTec AD paper 自身結論。
  3. 兩篇主要本文都沒有獨立 limitations section，因此 paper notes 不自行推論額外 limitation。
- **Git commit:** `first ingest`

## Batch 2 — PatchCore + DINOv2

- **Date:** 2026-11-17
- **Sources:**
  - `raw/03_patchcore.pdf`
  - `raw/04_dinov2.pdf`
- **Relevance Result:**
  - PatchCore: Relevant
  - DINOv2: Supporting Source
- **Source Role:**
  - PatchCore: Direct Visual Anomaly Detection method source
  - DINOv2: Feature Representation / Foundation Model supporting source
- **Wiki pages created:**
  - `wiki/concepts/normality-modeling.md`
  - `wiki/concepts/pretrained-visual-features.md`
  - `wiki/methods/patchcore.md`
  - `wiki/metrics/pro.md`
  - `wiki/papers/patchcore-cvpr2022.md`
  - `wiki/papers/dinov2-tmlr2024.md`
- **Wiki pages updated:**
  - `wiki/index.md`
  - `wiki/log.md`
- **Lint result:** PASS with notes. See `checks/batch2-lint.md`.
- **Problems found:**
  1. DINOv2 並非 anomaly detection 論文，因此只作為 Supporting Source，不從 DINOv2 論文自行推導 anomaly score 或 anomaly detection performance。
  2. PatchCore 的 99.6% image-level AUROC 來自更高 resolution / larger backbone / ensemble setup，與 main table 的 PatchCore-25% / 10% / 1% 設定分開記錄。
  3. PatchCore 與 DINOv2 都使用 pretrained visual features，但兩篇來源的 pretraining 與 downstream role 不同，因此沒有合併成單一方法。
- **Git commit:** `batch 2 ingest`

## Batch 3 — WinCLIP + SubspaceAD

- **Date:** 2026-11-17
- **Sources:**
  - `raw/05_winclip.pdf`
  - `raw/06_subspacead.pdf`
- **Relevance Result:**
  - WinCLIP: Relevant
  - SubspaceAD: Relevant
- **Source Role:**
  - WinCLIP: Direct zero-/few-normal-shot Visual Anomaly Detection source
  - SubspaceAD: Direct training-free few-shot Visual Anomaly Detection source
- **Wiki pages created:**
  - `wiki/concepts/zero-few-shot-anomaly-detection.md`
  - `wiki/methods/winclip.md`
  - `wiki/methods/subspacead.md`
  - `wiki/papers/winclip-cvpr2023.md`
  - `wiki/papers/subspacead-cvpr2026.md`
- **Wiki pages updated:**
  - `wiki/concepts/normality-modeling.md`
  - `wiki/concepts/pretrained-visual-features.md`
  - `wiki/index.md`
  - `wiki/log.md`
- **Lint result:** PASS with notes. See `checks/batch3-lint.md`.
- **Problems found:**
  1. WinCLIP zero-shot 與 WinCLIP+ few-normal-shot 使用不同可用資訊，不能把數字或 protocol 混在一起。
  2. SubspaceAD few-shot 與 batched 0-shot 是不同 setting，已分開記錄。
  3. DINOv2 在 Batch 2 被標為 Supporting Source；Batch 3 只透過 SubspaceAD 建立「DINOv2 features 被直接用於 anomaly detection」的 downstream 證據，不回寫成 DINOv2 原論文主張。
  4. PatchCore memory bank、WinCLIP language/reference scoring、SubspaceAD PCA subspace 皆屬不同 normality / anomaly evidence 機制，未合併為單一方法。
- **Git commit:** `batch 3 ingest`


## Retrieval / Coverage Test v1

- Scope: six required teaching coverage categories
- Result: PASS (6/6)
- Created: `checks/coverage-check-v1.md`
- Created: six Evidence Cards under `evidence/`
- Programmatic check: PASS
- Known boundaries: classification comparison and metric formulas require extra sources if taught in depth.

## Teaching Outline v1
- Stage: Teaching Point Extraction / Teaching Structure Check
- Input: 6 Evidence Cards + current Wiki
- Output: `slides/outline-v1.md`
- Check: `checks/teaching-structure-check-v1.md`
- Result: PASS
- Notes: 13-page beginner-oriented teaching sequence; known evidence boundaries preserved.

## 2026-11-17 — Per-page Drafting + Grounding Check v1
- Input: `slides/outline-v1.md`, six approved Evidence Cards, existing Wiki entries
- Created: `slides/page-drafts-v1.md`
- Created: `checks/grounding-check-v1.md`
- Slides drafted: 13
- Grounding result: PASS
- Unsupported factual claims in final draft: 0
- Revisions during drafting: dataset difficulty wording, DINOv2 role, low-shot protocol separation, metric formula boundary
- Next step: HTML generation → rendering/programmatic checks → independent AI review

---

## HTML Slide Generation and Final Review v1

- Input: grounded 13-page drafts (`slides/page-drafts-v1.md`)
- Output: `slides/index.html`
- Slide count: 13
- Rendering check: PASS
- Programmatic check: PASS
- Independent AI review: PASS
- Blocking issues found: 0
- Review artifacts:
  - `checks/html-render-programmatic-check-v1.md`
  - `checks/independent-ai-review-v1.md`
  - `slides/render-check.pdf`
  - `slides/render-check-montage.png`
- Status: ready for final delivery / publishing
