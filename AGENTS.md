# AGENTS.md

## 1. Project Overview

### Project Name
**Visual Anomaly Detection LLM Wiki**

### Project Purpose
本專案建立一個以 **Visual Anomaly Detection** 為主題的可持續擴充知識庫。

主要流程為：

`Source → Relevance Check → Ingest → Wiki → Lint → Retrieval → Evidence → Teaching Content → HTML Slides`

Wiki 將作為後續教學型 HTML 簡報、論文比較、方法流程整理與問答查詢的主要知識來源。

AI 在新增、修改或產生內容前，必須先閱讀本文件。

---

## 2. Target Audience

主要讀者為：

1. 完全沒有接觸過 Anomaly Detection 的初學者
2. 已具備 Machine Learning 基礎，但尚未接觸 Anomaly Detection 的學生

內容應遵循：

`直覺理解 → 基本術語 → 方法 → Dataset → Evaluation → Paper Comparison`

避免在尚未解釋基礎概念前直接使用大量專有術語。

---

## 3. Project Structure

```text
visual-anomaly-detection-wiki/
│
├── AGENTS.md
│
├── raw/
│   └── 原始論文與教材
│
├── wiki/
│   ├── index.md
│   ├── log.md
│   ├── concepts/
│   ├── datasets/
│   ├── methods/
│   ├── metrics/
│   └── papers/
│
├── evidence/
│   └── teaching evidence cards
│
├── slides/
│   └── HTML 簡報相關檔案
│
└── checks/
    └── lint 與檢查紀錄
```

### Directory Responsibilities

#### `raw/`
存放原始來源，例如：

- 論文 PDF
- Dataset paper
- 官方技術文件
- 使用者指定的可信來源

`raw/` 內容不能直接視為 Wiki 知識，必須先通過 Topic Relevance Check 與 ingest。

#### `wiki/`
存放整理完成且通過基本檢查的知識。

#### `evidence/`
存放從 Wiki 查詢後建立的 Evidence Cards，用於後續簡報與 Grounding Check。

#### `slides/`
存放 HTML 教學簡報與相關素材。

#### `checks/`
存放 lint、coverage、grounding 或其他檢查紀錄。

---

## 4. Initial Sources

第一版 Wiki 預計使用至少以下六篇資料：

1. MVTec AD
2. VisA
3. PatchCore
4. DINOv2
5. WinCLIP
6. SubspaceAD

不同資料分別支援：

- Task Definition
- Dataset
- Normality Modeling
- Foundation Model
- Zero / Few-shot Learning
- Evaluation
- Recent Methods

---

## 5. Language Rules

主要內容使用：

**繁體中文**

技術名詞保留英文，例如：

- Anomaly Detection
- Normality Modeling
- Feature Representation
- AUROC
- PatchCore
- DINOv2

第一次出現重要術語時，可以使用：

```text
異常檢測（Anomaly Detection）
```

後續可直接使用英文術語或常用中文名稱。

避免使用中國大陸常用技術翻譯。

---

# 6. Topic Relevance Check

新的來源進入 `raw/` 後，**不得直接 ingest**。

必須先判斷來源與 Visual Anomaly Detection Wiki 的關聯性。

判斷結果分為：

### Relevant
核心研究問題直接屬於 Visual Anomaly Detection。

可以正常進入 ingest。

### Supporting Source
來源本身不以 Visual Anomaly Detection 為主要研究問題，但能明確支援 Wiki 中的核心主題，例如：

- Dataset
- Feature Representation
- Foundation Model
- Normality Modeling
- Zero / Few-shot Learning
- Evaluation

這類來源可以 ingest，但必須標記：

```text
Source Role: Supporting Source
```

### Irrelevant
若來源：

- 不直接研究 Visual Anomaly Detection
- 無法支援任何既有核心主題
- 無法為任何 Wiki entry 提供可引用的新知識

則停止處理，不進入 Wiki。

---

## 7. Topic Relevance Checklist

每篇來源至少檢查：

1. 是否直接研究 Visual Anomaly Detection？
2. 若非直接相關，是否能支援至少一個 Wiki 核心主題？
3. 是否能提供新的、可追溯的知識？

只有：

```text
Relevant
或
Supporting Source
```

才能進入 ingest。

不得因為「可能以後有用」而保留無明確用途的來源。

---

# 8. Ingest Strategy

採用：

**每批 1～2 篇來源**

基本流程：

```text
Add Source
↓
Topic Relevance Check
↓
Ingest
↓
Update Wiki
↓
Lint / Review
↓
Git Commit
↓
Next Batch
```

在當前 batch 通過基本檢查前，不應繼續 ingest 下一批。

---

# 9. Ingest Rules

Ingest 時必須：

1. 以 `raw/` 中實際來源為依據。
2. 不使用模型自身知識補充來源缺少的內容。
3. 不自行修改原論文的研究結果。
4. 不自行補出不存在的 limitation、dataset result 或 conclusion。
5. 可以重新整理與濃縮內容。
6. 可以將不同段落重新組織成適合 Wiki 閱讀的結構。
7. 重新整理後不得改變原意。
8. 重要數字、metric 與 experimental setting 必須可回查原始來源。

---

# 10. Wiki Content Scope

Wiki 主要整理五類內容。

## A. Concepts

例如：

- Visual Anomaly Detection
- Normality Modeling
- Image-level Detection
- Pixel-level Localization
- Zero-shot
- Few-shot

---

## B. Datasets

至少整理：

- Dataset purpose
- Data scale
- Categories
- Annotation
- Task setting
- Evaluation usage

---

## C. Methods

每個方法頁面盡量包含：

```text
Overview
Core Idea
Input
Feature Representation
Normality Modeling
Anomaly Scoring
Detection / Localization Pipeline
Experimental Setting
Strengths
Limitations
Related Methods
References
```

---

## D. Evaluation Metrics

整理：

- Metric name
- What it measures
- Image-level / Pixel-level usage
- Interpretation
- Source

不得自行推導來源沒有提供的 metric 定義。

---

## E. Paper Notes

每篇重要論文至少整理：

```text
Research Problem
Main Contribution
Method
Datasets
Evaluation
Key Results
Strengths
Limitations
Related Wiki Entries
References
```

---

# 11. Citation Rules

Wiki 採用：

**段落級 Citation + 頁尾 References**

重要技術內容、數字、研究結論與比較都必須能追溯來源。

建議格式：

```text
[Source: PatchCore, CVPR 2022]
```

每個 Wiki 頁面最後必須包含完整 References。

不得：

- 虛構 paper
- 虛構 DOI
- 虛構作者
- 將 Paper A 的 result 標成 Paper B
- 將 Supporting Source 當成 anomaly detection 原始方法論文

---

# 12. Handling Conflicting Sources

若不同論文的結果或結論不一致：

1. 保留雙方說法。
2. 分別標示來源。
3. 不自行判定其中一方為唯一正確答案。
4. 整理可能造成差異的因素。

可檢查：

- Dataset
- Backbone
- Training Setting
- Number of Shots
- Evaluation Metric
- Experimental Protocol

若來源不足以解釋差異，應明確標示：

```text
目前來源不足以判斷造成差異的原因。
```

---

# 13. Wiki Index Rules

`wiki/index.md` 應作為 Wiki 導覽入口。

至少整理：

```text
Concepts
Datasets
Methods
Metrics
Papers
```

新增 Wiki entry 後，要同步確認 `index.md` 是否需要新增連結。

---

# 14. Ingest Log

每次 ingest 都應更新：

```text
wiki/log.md
```

記錄：

- Date
- Source
- Relevance Result
- Source Role
- Wiki pages created
- Wiki pages updated
- Lint result
- Problems found
- Git commit

目的在於追蹤哪一批資料造成 Wiki 的改變。

---

# 15. Wiki Lint

每個 batch ingest 後必須執行 lint。

檢查以下內容：

### Source Check
- 重要段落是否有來源
- Citation 是否存在
- Citation 是否對應正確來源

### Numeric Check
- Dataset size
- Performance number
- Percentage
- Metric
- Experimental setting

重要數字必須能回查原始來源。

### Cross-paper Check
確認：

- 不同論文的結果沒有被混合
- Dataset 與 method 對應正確
- Result 與來源對應正確

### Technical Fidelity
確認：

- 技術內容沒有講反
- 簡化後沒有改變原始概念
- Method pipeline 與來源一致

### Structure Check
確認：

- Wiki entry 有正確位置
- 必要 section 完整
- index 已更新
- Reference 完整

---

# 16. Programmatic Check vs AI Review

檢查分成兩類。

## Programmatic Check

適合檢查：

- File 是否存在
- Link 是否有效
- Citation target 是否存在
- 必要欄位是否缺失
- HTML 是否正常
- Slide count
- Overflow

## Independent AI Review

適合檢查：

- 技術內容是否忠於來源
- 結論是否講反
- 不同 paper 是否被錯誤合併
- Teaching content 是否涵蓋必要主題
- 簡化是否造成概念錯誤

AI Reviewer 應盡可能使用新的 context，只提供：

- 成品
- 對應 Wiki
- Evidence / Sources
- Review criteria

Reviewer 不應直接修改成品，只回傳檢查結果。

---

# 17. Retrieval Rules

當使用 Wiki 產生後續內容時：

1. 先明確定義需要回答的主題。
2. 只從 Wiki 取得資訊。
3. 若資訊不足，重新調整 query。
4. 不得直接使用模型自身知識補充。
5. Retrieval result 必須保留來源。

---

# 18. Coverage Check

製作 Visual Anomaly Detection 教學簡報時，至少檢查以下 coverage：

```text
Task Definition
Dataset
Normality Modeling
Foundation Model
Zero / Few-shot
Evaluation
```

若任一必要主題缺少足夠 Wiki evidence：

```text
Coverage = FAIL
```

流程應返回 Wiki Retrieval。

若重新 retrieval 後仍不足：

**停止該部分生成並交由使用者決定是否加入新的來源。**

---

# 19. Evidence Cards

通過 Retrieval 與 Coverage Check 後，建立 Evidence Cards。

每張 Evidence Card 建議包含：

```text
Teaching Topic
Claim
Explanation
Wiki Entry
Original Source
Important Numbers
Allowed Usage
```

後續 Slide Outline 與 HTML Content 只能使用 Evidence Cards 支援的內容。

不得在排版或改寫階段加入 Evidence Card 之外的新事實。

---

# 20. HTML Teaching Slides

最終 HTML 簡報目標：

**12～15 頁**

目標讀者：

- Anomaly Detection 初學者
- 有 Machine Learning 基礎的學生

基本教學方向：

```text
Introduction
↓
Task Definition
↓
Why Anomaly Detection is Difficult
↓
Datasets
↓
Normality Modeling
↓
Representative Methods
↓
Foundation Models
↓
Zero / Few-shot
↓
Evaluation
↓
Method Comparison
↓
Example Workflow
↓
Takeaways
```

實際頁數可依內容調整，但應維持清楚的教學順序。

---

# 21. Slide Grounding Rules

每一頁簡報的重要 claim 必須：

```text
Slide
→ Evidence Card
→ Wiki Entry
→ Original Source
```

若任一 claim 無法建立完整來源鏈：

```text
Grounding = FAIL
```

回到 Teaching Point / Evidence 階段處理。

不得在 HTML Generation 階段自行補充新內容。

---

# 22. Loop Rules

每個 loop 必須明確定義：

- Goal
- Constraints
- Completion Criteria
- Stop Condition
- Trigger

---

## Retrieval Loop

### Goal
取得足夠支援教學內容的 Wiki 資料。

### Trigger
Coverage Check 發現必要主題缺失。

### Constraint
只能查詢 Wiki。

### Completion
所有必要 coverage 都有有效 evidence。

### Stop
重新查詢後仍不足時停止，等待使用者決定是否新增來源。

---

## Teaching Structure Loop

### Goal
建立適合初學者理解的教學順序。

### Trigger
Teaching Structure Check 判定前後概念依賴不合理。

### Constraint
只能重新組織已存在的 Teaching Points。

### Completion
概念順序清楚，沒有尚未解釋就提前使用的核心術語。

### Stop
最多修改 3 輪。

---

## Grounding Loop

### Goal
確保 Slide content 可追溯到 Wiki 與原始來源。

### Trigger
Grounding Check 出現 unsupported claim。

### Constraint
不得自行補寫來源外知識。

### Completion
所有重要 claim 都有 Evidence Card。

### Stop
最多修改 3 輪；仍失敗則停止並輸出問題報告。

---

# 23. Error Handling Principle

錯誤應盡量在**最接近來源的節點**被發現。

例如：

```text
無關論文
→ Topic Relevance Check

資料不足
→ Coverage Check

來源錯誤
→ Evidence / Grounding Check

教學順序問題
→ Teaching Structure Check

HTML Overflow
→ Rendering Check
```

避免所有問題都等到 Final Review 才處理。

---

# 24. Git Rules

每次重要階段完成後建立 commit。

例如：

```text
first ingest
add patchcore wiki
add evidence cards
first slide draft
fix grounding issues
final html slides
```

每次 commit 應只包含一個明確階段的修改，方便回查。

---

# 25. Definition of Done

一批新的來源完成 ingest 前確認：

- [ ] 已通過 Topic Relevance Check
- [ ] 已標示 Relevant / Supporting Source
- [ ] 已完成 Wiki update
- [ ] Citation 可回查
- [ ] 重要數字可回查
- [ ] 沒有混合不同 paper result
- [ ] Technical Fidelity 通過
- [ ] `wiki/index.md` 已更新
- [ ] `wiki/log.md` 已更新
- [ ] 已完成 lint
- [ ] 已建立 Git commit

HTML 簡報完成前確認：

- [ ] 內容只來自 Wiki
- [ ] Coverage Check 通過
- [ ] Evidence Cards 完整
- [ ] Grounding Check 通過
- [ ] 教學順序合理
- [ ] 12～15 頁
- [ ] Programmatic Check 通過
- [ ] Independent AI Review 通過
- [ ] HTML 可以正常瀏覽
- [ ] 沒有明顯 overflow
- [ ] 已保留來源對應關係

---

# 26. Core Principle

> **先建立可信、可追溯的知識，再利用這些知識產生成品。**

若資料不足：

**停止、補資料、重新檢查。**

不得為了完成 Wiki 或簡報而自行填補沒有來源支援的知識。