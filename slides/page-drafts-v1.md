# Per-page Drafts v1

## Deck Title
**From Normal to Abnormal: An Introduction to Visual Anomaly Detection**

> Drafting rule: each page only uses claims already supported by the approved outline, Evidence Cards, and referenced Wiki entries. No new factual claims are introduced here.

---

## Slide 1 — What Are We Trying to Detect?

### On-slide draft
**Visual Anomaly Detection (VAD)** asks whether an image contains something that deviates from normal data, and when needed, where the abnormal region is located.

**Two common outputs**
- **Image-level detection**: Is this image normal or anomalous?
- **Pixel-level localization**: Which region is anomalous?

**Today’s path**
Task → Data → Normality Modeling → Low-shot Methods → Evaluation

### Speaker note
Industrial inspection is a useful entry point because many anomaly-detection benchmarks are built around normal products and defective products. We will first understand what information the model receives, then look at how different methods construct anomaly evidence.

### Grounding
- Evidence: `evidence/01-task-definition.md`
- Wiki: `wiki/concepts/visual-anomaly-detection.md`
- Sources: `raw/01_mvtec-ad.pdf`, `raw/02_visa.pdf`

---

## Slide 2 — The Basic Task Setting

### On-slide draft
A common industrial setting is **normal-only / defect-scarce training**.

**Training**
- Normal samples are available.
- Defective examples may be unavailable or very limited.

**Testing**
- Both normal and anomalous images can appear.
- The system may need to produce an image-level decision and a pixel-level anomaly map.

**Key question**
How can we recognize something abnormal when the model mainly learns from normal data?

### Speaker note
MVTec AD formalizes this setting with defect-free training data and normal plus defective test data. This setting naturally motivates methods that first model normality and later detect deviations from it.

### Grounding
- Evidence: `evidence/01-task-definition.md`
- Wiki: `wiki/datasets/mvtec-ad.md`, `wiki/datasets/visa.md`
- Sources: `raw/01_mvtec-ad.pdf`, `raw/02_visa.pdf`

---

## Slide 3 — Two Benchmarks: MVTec AD and VisA

### On-slide draft
| Benchmark | Scale | Structure highlighted in source | Annotation / task |
|---|---:|---|---|
| **MVTec AD** | 5,354 images, 15 categories, 73 defect types | Industrial objects and textures | Pixel-precise anomaly ground truth |
| **VisA** | 10,821 images, 12 objects, 3 domains | Complex structures, multiple instances, location variation | Image-level and pixel-level annotations |

**Why use both?**
They expose methods to different industrial image structures and provide benchmark settings for detection and localization.

### Speaker note
The useful comparison here is about dataset composition and scene structure. The sources do not support a simple claim that one dataset is universally harder, so the slide avoids ranking them by difficulty.

### Grounding
- Evidence: `evidence/02-datasets.md`
- Wiki: `wiki/datasets/mvtec-ad.md`, `wiki/datasets/visa.md`
- Sources: `raw/01_mvtec-ad.pdf`, `raw/02_visa.pdf`

---

## Slide 4 — A Core Idea: Model Normality First

### On-slide draft
When anomaly examples are scarce, one useful strategy is to build a representation of **normal data** first.

**Conceptual flow**
Normal images → normal representation → compare test features → deviation becomes anomaly evidence

A larger deviation can indicate stronger anomaly evidence.

**Important:** different methods define “normal representation” and “deviation” differently.

### Speaker note
This slide is a bridge from the data setting to the algorithms. PatchCore uses a memory bank of representative normal patch features. SubspaceAD uses a PCA normal subspace. WinCLIP introduces language-guided normal and anomalous prototypes, so its mechanism should be treated separately rather than forced into exactly the same normality-modeling template.

### Grounding
- Evidence: `evidence/03-normality-modeling.md`
- Wiki: `wiki/concepts/normality-modeling.md`
- Sources: `raw/03_patchcore.pdf`, `raw/05_winclip.pdf`, `raw/06_subspacead.pdf`

---

## Slide 5 — PatchCore: Normality as a Memory Bank

### On-slide draft
**PatchCore pipeline**
1. Extract intermediate patch features with a pretrained backbone.
2. Store representative normal patch features in a **memory bank**.
3. Reduce the memory with **coreset subsampling**.
4. Compare a test patch with its nearest normal neighbour.
5. Use distance as anomaly evidence and form an anomaly map.

**Normality representation:** memory bank  
**Anomaly evidence:** nearest-neighbour distance

### Speaker note
PatchCore makes normality concrete by keeping representative normal patch features. A test patch that is far from this stored normal feature set receives stronger anomaly evidence. This is also a good example of separating the feature extractor from the anomaly-scoring mechanism.

### Grounding
- Evidence: `evidence/03-normality-modeling.md`, `evidence/04-foundation-features.md`
- Wiki: `wiki/methods/patchcore.md`
- Source: `raw/03_patchcore.pdf`

---

## Slide 6 — Why Pretrained Visual Features Matter

### On-slide draft
Many VAD methods first convert images into **pretrained visual features** and then perform anomaly modeling in feature space.

**Examples in this Wiki**
- PatchCore: ImageNet-pretrained intermediate features
- DINOv2: general-purpose self-supervised image / patch features
- SubspaceAD: frozen DINOv2-G patch tokens

**Role separation**
Feature extractor → visual representation  
Anomaly method → normality / anomaly evidence

### Speaker note
This distinction is important. A strong visual representation can be reused by a downstream anomaly method, while the anomaly detector still needs its own mechanism for scoring abnormality. DINOv2 is therefore introduced here as a feature source, not as an anomaly detector.

### Grounding
- Evidence: `evidence/04-foundation-features.md`
- Wiki: `wiki/concepts/pretrained-visual-features.md`
- Sources: `raw/03_patchcore.pdf`, `raw/04_dinov2.pdf`, `raw/06_subspacead.pdf`

---

## Slide 7 — DINOv2 as a Feature Source

### On-slide draft
**DINOv2** provides general-purpose self-supervised visual representations with image-level and patch-level information.

In this Wiki, its anomaly-detection connection comes from downstream use:

DINOv2 patch tokens → frozen feature source → SubspaceAD normal subspace

**Optional scale fact**
LVD-142M contains **142,109,386 images**.

### Speaker note
The original DINOv2 work focuses on transferable visual features. SubspaceAD later uses frozen DINOv2-G patch tokens as input to its anomaly-detection pipeline. Keeping those two source roles separate prevents us from attributing an anomaly-detection claim to the DINOv2 paper itself.

### Grounding
- Evidence: `evidence/04-foundation-features.md`
- Wiki: `wiki/concepts/pretrained-visual-features.md`, `wiki/papers/dinov2-tmlr2024.md`, `wiki/methods/subspacead.md`
- Sources: `raw/04_dinov2.pdf`, `raw/06_subspacead.pdf`

---

## Slide 8 — Low-shot Settings Are Not All the Same

### On-slide draft
| Setting | Available information |
|---|---|
| **WinCLIP zero-shot** | No task-specific normal images |
| **WinCLIP+** | K = 1–4 normal references |
| **SubspaceAD few-shot** | k ∈ {1,2,4} normal images |
| **SubspaceAD batched 0-shot** | Batch test tokens are used to fit a statistical model |

**Takeaway:** “zero-shot” and “few-shot” results must be interpreted together with the exact protocol.

### Speaker note
The labels can sound similar while the available information differs. In particular, SubspaceAD batched 0-shot is not the same protocol as WinCLIP’s prompt-based zero-shot setting, so their results should not be treated as directly interchangeable.

### Grounding
- Evidence: `evidence/05-zero-few-shot.md`
- Wiki: `wiki/concepts/zero-few-shot-anomaly-detection.md`
- Sources: `raw/05_winclip.pdf`, `raw/06_subspacead.pdf`

---

## Slide 9 — WinCLIP: Language-Guided Anomaly Evidence

### On-slide draft
**WinCLIP** combines visual features with **normal / anomalous text prototypes**.

**Core components**
- Compositional Prompt Ensemble
- normal / anomalous text prototypes
- image, patch, and multi-scale window features
- language-guided anomaly scores

**WinCLIP+** adds a small number of normal references for few-normal-shot detection.

### Speaker note
This route differs from PatchCore’s nearest-neighbour memory-bank distance. WinCLIP uses language guidance to construct normal and anomalous prototypes, while WinCLIP+ additionally uses a small set of normal references.

### Grounding
- Evidence: `evidence/03-normality-modeling.md`, `evidence/05-zero-few-shot.md`
- Wiki: `wiki/methods/winclip.md`
- Source: `raw/05_winclip.pdf`

---

## Slide 10 — SubspaceAD: Normality as a PCA Subspace

### On-slide draft
**SubspaceAD pipeline**
1. Collect a few normal images.
2. Extract frozen DINOv2-G patch tokens.
3. Fit a **PCA normal subspace**.
4. Project test patch features onto that subspace.
5. Use the **reconstruction residual** as anomaly evidence.
6. Aggregate patch evidence for image-level scoring.

**Normality representation:** PCA subspace  
**Anomaly evidence:** reconstruction residual

### Speaker note
SubspaceAD compresses normal patch features into a low-dimensional subspace. If a test patch cannot be well reconstructed by this normal subspace, its residual becomes anomaly evidence. The few-shot protocol and the separate batched 0-shot protocol should remain clearly distinguished.

### Grounding
- Evidence: `evidence/03-normality-modeling.md`, `evidence/04-foundation-features.md`, `evidence/05-zero-few-shot.md`
- Wiki: `wiki/methods/subspacead.md`
- Source: `raw/06_subspacead.pdf`

---

## Slide 11 — Three Ways to Build Anomaly Evidence

### On-slide draft
| Method | Main representation | Extra information | Anomaly evidence |
|---|---|---|---|
| **PatchCore** | Normal patch memory bank | Normal images | Nearest-neighbour distance |
| **WinCLIP** | Language prototypes + visual features | Text prompts; optional normal references | Language / reference-guided score |
| **SubspaceAD** | PCA normal subspace | Few normal images | Reconstruction residual |

**Common question:** How different is this test feature from what the method considers normal or expected?

### Speaker note
The methods share a high-level goal of producing anomaly evidence, but their representation and scoring mechanisms are different. This table compares those mechanisms and protocols only; it does not rank performance across incompatible experimental settings.

### Grounding
- Evidence: `evidence/03-normality-modeling.md`, `evidence/04-foundation-features.md`, `evidence/05-zero-few-shot.md`
- Wiki: `wiki/methods/patchcore.md`, `wiki/methods/winclip.md`, `wiki/methods/subspacead.md`
- Sources: `raw/03_patchcore.pdf`, `raw/05_winclip.pdf`, `raw/06_subspacead.pdf`

---

## Slide 12 — How Do We Evaluate Anomaly Detection?

### On-slide draft
VAD evaluation should separate **image-level detection** from **pixel-level localization**.

**Metrics covered by this Wiki**
- **AU-ROC**: used for detection / segmentation evaluation in the cited benchmark and method papers
- **AU-PR**: useful as a complementary view when class imbalance is high
- **PRO**: evaluates overlap / recovery of connected anomaly regions

**Key caution**
VisA notes that AU-ROC can appear optimistic under strong class imbalance, so AU-PR provides complementary information.

### Speaker note
A single metric does not fully describe system behavior. The Wiki supports an overview of AU-ROC, AU-PR, and PRO and their usage context, but it does not contain enough evidence for a full mathematical derivation, so formulas are intentionally omitted.

### Grounding
- Evidence: `evidence/06-evaluation.md`
- Wiki: `wiki/metrics/auroc-aupr.md`, `wiki/metrics/pro.md`
- Sources: `raw/01_mvtec-ad.pdf`, `raw/02_visa.pdf`, `raw/03_patchcore.pdf`

---

## Slide 13 — Takeaways: From Normal Data to Anomaly Evidence

### On-slide draft
When reading or designing a VAD method, ask four questions:

1. **Data setting**: normal-only, zero-shot, or few-shot?
2. **Feature source**: what pretrained / foundation representation is used?
3. **Anomaly evidence**: memory-bank distance, language guidance, or subspace residual?
4. **Evaluation**: how are image-level detection and pixel-level localization measured?

**Examples**
- PatchCore → memory bank + nearest-neighbour distance
- WinCLIP → language-guided prototypes / optional normal references
- SubspaceAD → PCA normal subspace + reconstruction residual

### Speaker note
These four questions provide a reusable reading framework. They connect the data protocol, representation, scoring mechanism, and evaluation without introducing any new method claim beyond the content already covered in the deck.

### Grounding
- Evidence: `evidence/01-task-definition.md`, `evidence/03-normality-modeling.md`, `evidence/04-foundation-features.md`, `evidence/05-zero-few-shot.md`, `evidence/06-evaluation.md`
- Sources: `raw/01_mvtec-ad.pdf`, `raw/03_patchcore.pdf`, `raw/04_dinov2.pdf`, `raw/05_winclip.pdf`, `raw/06_subspacead.pdf`

---

## Draft Status
**READY FOR GROUNDING CHECK**
