# AAA v1.0 Workflow Generator v1.1.0 使用手冊

> **Skill 名稱**：`aaa-v1-workflow-generator`  
> **AAA SOP 版本**：AAA v1.0（6 Gates／18 Steps）  
> **套件版本**：v1.1.0  
> **日期**：2026-08-29

---

## 1. 這個 Skill 是什麼？

`aaa-v1-workflow-generator` 是用來執行 **AAA（AI Assisted Academic Writing）v1.0** 的研究工作流程控制器。它不是一般的論文代寫 Prompt，而是以「來源驗證、證據狀態、逐句可追溯、人工把關」為核心的研究寫作 SOP。

它將研究流程固定為 **6 個品質閘門（Gates）與 18 個步驟（Steps）**，並要求所有可進入正式稿件的實質性主張，必須經過來源驗證。

核心原則：

> **No substantive claim enters the controlled manuscript unless it has passed source verification, and no new claim introduced by AI may bypass the evidence loop.**

中文意義：任何實質性研究主張在進入受控稿件前，都必須通過來源驗證；AI 新增的任何主張都不得繞過證據回圈。

---

## 2. v1.1.0 主要新增內容

v1.1.0 **沒有改動 AAA v1.0 的 6 Gates／18 Steps**，而是補強 Step 8 與 Step 14 的執行規格。

### 2.1 Step 8：固定使用 Appendix 1 Prompt 1

新增 Canonical Prompt 1，用來從已上傳的全文來源抽取 Candidate Atomic Sentences（Candidate AS）。

重要規則：

- 只可使用已提供／已上傳來源。
- 不得加入來源中不存在的資訊。
- 輸出格式固定為：`sentence | Author | Year | Page | #tags`。
- Prompt 1 產生的 AS 一律先標記為 **TO VERIFY**。
- 即使使用 source-grounded 工具，也不能直接標為 VERIFIED。

### 2.2 Step 14A：固定使用 Appendix 1 Prompt 2

Step 14A 以 VERIFIED AS 為封閉證據集合進行 synthesis。

核心 Prompt：

> Organize the following VERIFIED atomic sentences into a coherent paragraph. Preserve every citation exactly. Do NOT introduce any new claim or reference.

重要規則：

- 只能使用 VERIFIED／TRACEABLE AS。
- 必須原樣保留 citation。
- 不得新增 claim。
- 不得新增 reference。

### 2.3 Step 14B：Write and polish 邊界

AI 可以改善：grammar、syntax、transitions、coherence、redundancy、academic tone、rhetorical flow。

但不得：

- 改變證據原意。
- 改變統計數據、分母、方向、限定條件或比較組。
- 新增 factual／empirical claim。
- 新增 citation 或 reference。

如果潤飾需要新的證據，必須標記 `[NEEDS NEW EVIDENCE]`，並啟動 Step 17，回到 Steps 4–12。

---

## 3. 安裝方式

### 3.1 全域安裝

下載 `aaa-v1-workflow-generator-v1.1.0.zip`，解壓到全域 Skill 目錄：

```bash
unzip aaa-v1-workflow-generator-v1.1.0.zip -d /home/oai/skills/
```

安裝後應為：

```text
/home/oai/skills/aaa-v1-workflow-generator/
├── SKILL.md
├── VERSION
├── CHANGELOG.md
├── INSTALL.md
├── manifest.txt
├── references/
└── templates/
```

### 3.2 檢查版本

```bash
cat /home/oai/skills/aaa-v1-workflow-generator/VERSION
```

應輸出 `1.1.0`。

---

## 4. 最簡單的使用方式

直接告訴 ChatGPT：

```text
用 AAA v1.0 幫我處理這個研究題目：［研究題目／研究觀察］
```

也可以指定模式：

```text
@aaa-v1 plan
@aaa-v1 run step 3
@aaa-v1 extract-as
@aaa-v1 audit
@aaa-v1 resume
@aaa-v1 disclose
```

如果平台不支援 `@aaa-v1` 形式，也可直接說：

```text
用 aaa-v1-workflow-generator 幫我規劃這個研究。
```

---

## 5. 六種操作模式

| Mode | 用途 | 適用情境 |
|---|---|---|
| `explain` | 說明 AAA v1.0 | 教學、課堂、說明流程 |
| `plan` | 規劃 18-step research workflow | 剛開始研究題目 |
| `run` | 執行目前／指定 Step | 已進入研究流程 |
| `audit` | 稽核是否符合 AAA | 已有文獻回顧或稿件 |
| `resume` | 判斷目前進度並續作 | 做到一半、有既有檔案 |
| `export` | 匯出流程／表格／教材規格 | 教學、講義、流程圖 |

---

## 6. AAA v1.0 的 6 Gates／18 Steps

### A. Question Gate — Steps 1–3

1. 寫出原始研究觀察與研究動機。
2. 人工確認並界定研究問題；必要時形成 PICO／PECO／PICOT／SPIDER 等結構。
3. AI 協助產生搜尋概念、關鍵詞與同義詞。

**通過條件**：研究者明確確認研究問題。

### B. Source Gate — Steps 4–6

4. 正式資料庫搜尋＋citation mapping。
5. 人工篩選並取得全文。
6. 建立可追溯 reference library。

**通過條件**：文獻來源、搜尋紀錄與全文可追溯。

### C. Epistemic Gate — Step 7

7. AI 協助閱讀，但所有輸出標示為 **UNVERIFIED**。

**通過條件**：AI reading notes 與正式 evidence 清楚分開。

### D. Verification Gate — Steps 8–12

8. 使用 Canonical Prompt 1 產生 Candidate AS。
9. 加入 provenance metadata。
10. 人工逐句核對原始 PDF／全文。
11. 驗證失敗 → DISCARD，不修補。
12. 驗證後再進行 SPS 評分；內容若有實質變更，必須重新驗證。

**通過條件**：只有人類實際 cross-reference verification 後的單位才能成為 VERIFIED。

### E. Claim Gate — Steps 13–15

13. 建立 Verified AS Library。
14. Evidence-constrained drafting：14A Canonical Prompt 2 synthesis；14B constrained Write and polish。
15. 逐段／逐 claim trace-back。

**通過條件**：每個 substantive claim 可回查到 Verified AS 與來源定位資訊。

### F. Integrity Gate — Steps 16–18

16. AI 模擬 peer review。
17. 任何新 claim／新 evidence need → 回 Steps 4–12。
18. 人工終審＋citation audit＋AI disclosure。

**通過條件**：新主張均已完成 evidence loop，並完成最終 citation audit 與 AI 使用揭露。

---

## 7. 證據狀態（Evidence States）

AAA v1.0 固定使用：

```text
UNVERIFIED → TO VERIFY → VERIFIED → TRACEABLE
```

| 狀態 | 定義 | 可否作為正式 evidence |
|---|---|---|
| `UNVERIFIED` | AI 摘要、閱讀筆記、探索結果 | 否 |
| `TO VERIFY` | 已形成 Candidate AS，等待人工核對 | 否 |
| `VERIFIED` | 人工確認來源支持該 claim | 是 |
| `TRACEABLE` | claim → AS → source/page 已可回查 | 是 |
| `DISCARD` | 驗證失敗或不可用 | 否 |
| `NEEDS NEW SEARCH` | 現有證據庫不足 | 否，必須回搜尋流程 |

最重要規則：AI 不得自行把 `UNVERIFIED` 或 `TO VERIFY` 升級為 `VERIFIED`。

---

## 8. Step 8：Candidate Atomic Sentence 的標準操作

### 8.1 前提

必須有已篩選文獻、全文 PDF／全文內容，以及已確認研究主題或 PICO-aligned core topic。

### 8.2 Canonical Prompt 1

Skill 會使用 `references/candidate_as_prompt.md` 或 `templates/prompt1_candidate_as.txt`。

核心結構：

```text
[TASK]
Precise atomic-sentence extraction from the uploaded source(s) ONLY.

[CORE TOPIC]
{{PICO_ALIGNED_CORE_TOPIC}}

[EXTRACTION INTENT]
A1 = core findings
A2 = mechanism/theory
A3 = methods
A4 = limitations

[WORD LIMIT]
A1: 15–18 words
A2: 20–30 words
A3: 25–35 words
A4: ≤25 words

[QUALITY]
Semantically complete; independently readable; concise; SPS target ≥8.

[GROUNDING]
Use ONLY the uploaded sources.
Do NOT add any fact not present in the sources.
If a claim is not in the sources, omit it.

[OUTPUT]
sentence | Author | Year | Page | #tags
```

### 8.3 輸出後狀態

所有 Candidate AS 的初始狀態固定為：

```text
Evidence state = TO VERIFY
```

不能直接進入正式稿件。

---

## 9. Steps 9–12：如何完成真正的驗證

### Step 9 — Provenance

至少保留：`sentence | author | year | page_or_locator | tags | evidence_state`。

建議再加 DOI / PMID / source_id、supporting excerpt、verifier、verification date、SPS、notes。

### Step 10 — Human verification

研究者必須打開原始全文，逐一確認：reference 確實存在；原文確實支持 claim；統計數值、方向、樣本、條件、比較組均正確。

### Step 11 — Discard-not-edit

若驗證失敗，狀態為 `DISCARD`。不要把錯誤句子修一修繼續使用。若內容實質改變，應視為新的 Candidate AS，再重新驗證。

### Step 12 — SPS

只有在 validity 成立後，才使用 Semantic Purity Score 評估句子的品質與可重用性。

> **Validity precedes quality.**

---

## 10. Step 14A：Verified-AS synthesis

輸入只能是 `VERIFIED` 或 `TRACEABLE`。

Skill 固定使用 `references/verified_as_synthesis_prompt.md`，核心文字：

```text
Organize the following VERIFIED atomic sentences into a coherent paragraph.
Preserve every citation exactly.
Do NOT introduce any new claim or reference.
```

這一步不是自由寫作，而是把封閉的 Verified AS evidence set 組織成連貫文字。可以重排順序與建立不增加實質命題的連接；不得加入新研究結果、機轉、統計數字、citation 或 reference。

---

## 11. Step 14B：Write and polish

Prompt 2 完成後，才可進行語言與修辭潤飾。Skill 使用 `references/write_and_polish_wrapper.md` 或 `templates/write_and_polish_wrapper.txt`。

可改善 grammar、syntax、clarity、coherence、transitions、concision、academic tone、rhetorical flow。

不可改變研究結果意義、把 association 改成 causation、改變 effect direction、改動統計數字、移除重要限定條件、增加新的 empirical claim 或 reference。

若需要新的 evidence：`[NEEDS NEW EVIDENCE]` → Step 17 → Steps 4–12。

---

## 12. Step 15：Claim-level trace-back

正式草稿中的 substantive claim 必須可回查：

```text
Manuscript claim
      ↓
Verified AS
      ↓
Original source
      ↓
Page / locator
```

建議使用 `templates/claim_evidence_matrix.csv` 與 `templates/trace_back.md`。

---

## 13. Step 16–17：Peer review 不等於證據

AI 可以模擬 reviewer，例如指出文獻不足、缺少比較研究、理論機轉尚未交代、研究 gap 不夠明確。但 reviewer suggestion 只能視為 `UNVERIFIED / NEEDS NEW SEARCH`，不能直接加入正文。

凡是 reviewer 要求增加新 evidence-bearing claim：

```text
Step 17 → Step 4 Search → Steps 5–12 → Step 13 Verified AS Library → Step 14 synthesis
```

---

## 14. Step 18：AI disclosure

Skill 提供 `templates/ai_disclosure.md`，可整理 AI 工具名稱、版本／developer（若可確認）、使用目的、使用階段、prompts／prompting method、content verification、human oversight、data privacy，以及 AI 是否影響 conclusions。最後內容仍須由人類作者確認。

---

## 15. 常用指令範例

### 15.1 從研究觀察開始

```text
用 AAA v1.0 幫我處理這個研究題目：
精神障礙者接受支持性就業服務後，哪些因素與工作維持有關？
```

### 15.2 只做到搜尋策略

```text
用 AAA v1.0 執行 Steps 1–3，幫我把研究問題轉成 PICO，並產生 PubMed 搜尋概念與同義詞。
```

### 15.3 已有全文，開始 Atomic Sentence

```text
用 AAA v1.0 執行 Step 8。
以這些全文為唯一來源，使用 canonical Prompt 1 產生 Candidate AS。
所有輸出保持 TO VERIFY。
```

### 15.4 人工核對後建立 Verified AS Library

```text
以下 Candidate AS 我已逐句核對原始 PDF。
請依我的確認結果更新 evidence state，建立 Verified AS Library。
```

### 15.5 從 Verified AS 寫文獻回顧

```text
用 AAA v1.0 Step 14A。
只使用這批 VERIFIED AS，依 canonical Prompt 2 組成文獻回顧段落。
Preserve every citation exactly. Do NOT introduce any new claim or reference.
```

### 15.6 再做學術潤飾

```text
執行 AAA v1.0 Step 14B。
只能改善語言、結構與學術語氣，不得增加 claim 或 reference。
```

### 15.7 稽核既有草稿

```text
用 AAA v1.0 audit 這份文獻回顧。
請列出：
1. 未有 Verified AS 支持的 claim；
2. citation 與 claim 不匹配處；
3. 需要進入 Step 17 的新 evidence needs。
```

### 15.8 做到一半繼續

```text
用 AAA v1.0 resume。
我已有 Search Log、24 篇全文、80 個 Candidate AS。
請判定目前在哪一個 Gate／Step，列出還缺什麼。
```

---

## 16. 套件目錄與用途

```text
aaa-v1-workflow-generator/
├── VERSION
├── SKILL.md
├── CHANGELOG.md
├── INSTALL.md
├── manifest.txt
│
├── references/
│   ├── aaa_v1_canonical_18steps.md
│   ├── evidence_states.md
│   ├── gate_rules.md
│   ├── atomic_sentence_sps.md
│   ├── candidate_as_prompt.md
│   ├── verified_as_synthesis_prompt.md
│   ├── write_and_polish_wrapper.md
│   └── gamer_reporting.md
│
└── templates/
    ├── project_state.yaml
    ├── search_log.md
    ├── candidate_as.csv
    ├── verified_as.csv
    ├── claim_evidence_matrix.csv
    ├── trace_back.md
    ├── ai_disclosure.md
    ├── prompt1_candidate_as.txt
    ├── prompt2_verified_as_synthesis.txt
    └── write_and_polish_wrapper.txt
```

---

## 17. 建議專案工作區

```text
00_Research_Question/
01_Search_Log/
02_Full_Text_Library/
03_UNVERIFIED_Reading_Notes/
04_Candidate_AS/
05_Verified_AS_Library/
06_Draft_Traceback/
07_Review_Audit/
08_AI_Disclosure/
```

這種結構方便 `resume`、audit 與研究稽核。

---

## 18. AAA v1.0 的五條關鍵安全規則

1. **Never invent references.** 不得虛構 reference、DOI、頁碼、統計資料或研究特徵。
2. **Human verification controls VERIFIED status.** AI 不能自行宣布某一 AS 已 VERIFIED。
3. **Validity precedes quality.** 先 Step 10 驗證，再 Step 12 SPS。
4. **Verification failure = DISCARD, not repair.** 來源不支持就丟棄，不以改寫掩蓋 citation mismatch。
5. **New claim → Step 17 → Steps 4–12.** 任何 AI／reviewer／作者新增的 evidence-bearing claim，都必須重新進證據流程。

---

## 19. 常見錯誤

- 把 NotebookLM／AI 摘要直接當 evidence：錯。AI reading output 是 `UNVERIFIED`；Candidate AS 只是 `TO VERIFY`。
- SPS 8–9 分就等於 VERIFIED：錯。SPS 評估句子品質，不是 citation validity。
- Prompt 2 後讓 AI 自由補文獻：錯。Prompt 2 使用 closed evidence set，不得新增 reference。
- Write and polish 時補一句合理的機轉：若是新 factual claim，不允許；應標記 `[NEEDS NEW EVIDENCE]`。
- Reviewer 建議等於可以直接寫入正文：錯。Reviewer suggestion 不是 evidence；必須進 Step 17 evidence loop。

---

## 20. 版本管理

本 Skill 應區分：

- **AAA SOP version**：AAA v1.0（固定 6 Gates／18 Steps）。
- **Skill package version**：目前 v1.1.0。

v1.1.0 為 execution-specification revision，沒有改動 AAA v1.0 SOP 的步驟編號。未來若修改 18-step 本體，應另建立 AAA v2.x 或其他明確版本，而不是覆寫 v1.0 baseline。

---

## 21. 快速記憶版

```text
Question
  ↓
Search
  ↓
Full text
  ↓
UNVERIFIED reading
  ↓
Prompt 1 → Candidate AS / TO VERIFY
  ↓
Human verification
  ↓
VERIFIED AS
  ↓
Prompt 2 → evidence-constrained synthesis
  ↓
Write & polish (no new claim/reference)
  ↓
Trace-back
  ↓
Peer review
  ↓
New claim? → Step 17 → Search again
  ↓
Final citation audit + AI disclosure
```

---

## 22. 發行檔

- `aaa-v1-workflow-generator-v1.1.0.zip`
- `AAA_v1.0_Workflow_Generator_v1.1.0_使用手冊.md`

建議 Git commit message：

```text
feat: add AAA v1.0 workflow generator v1.1.0 and user manual
```