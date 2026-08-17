# 🚀 2026 GEM to Skill Kit (v2.0 升級全套件)

> 本儲存庫為 **Google Gemini 自訂 GEM 升級為標準 Agent Skill (`SKILL.md`)** 的全套開源資源庫，遵循 [gem-to-skill-kit](https://github.com/mathruffian-dot/gem-to-skill-kit) 規範重構完成。

---

## 📂 目錄架構

```tree
.
├── AGENTS.md                    # 跨 Agent 通用入口與安全規範
├── GEMINI.md                    # Gemini CLI / AntiGravity 入口
├── README.md                    # 專案說明與總覽目錄
├── 00_2026GEM_升級總覽_v2.0.md    # 14組 GEM 與 Skill 對照總表
├── gems/                        # 升級版 GEM (v2.0) 系統提示詞
│   ├── 01_TANA_M3_研究輪廓教練_v2.0.md
│   ├── 02_論文拾光_織網館_v2.0.md
│   ├── 03_TANA_M1_研究陪跑教練_v2.0.md
│   ├── 04_TANA_M2_經驗轉譯教練_v2.0.md
│   ├── 05_論文拾光_夢蝶館_v2.0.md
│   ├── 06_論文拾光_破曉館_架構版_v2.0.md
│   ├── 07_Prompt_精進版_v2.0.md
│   ├── 08_論文拾光_破曉館_完整版_v2.0.md
│   ├── 09_EID_IC_感染控制教育顧問_v2.0.md
│   ├── 10_潤飾論文助手_v2.0.md
│   ├── 11_資深白秘書_v2.0.md
│   ├── 12_IRB_撰寫範本_v2.0.md
│   ├── 13_Puti_AI填空心智圖產生器_v2.0.md
│   └── 14_筆記神之研習筆記王_v2.0.md
└── skills/                      # 14 個標準 Agent Skills (SKILL.md)
    ├── tana-m3-research-outline/
    ├── thesis-literature-web/
    ├── tana-m1-research-companion/
    ├── tana-m2-experience-translator/
    ├── thesis-topic-ideation/
    ├── thesis-ch1-architect/
    ├── prompt-optimizer-pro/
    ├── thesis-dawn-ch1-full/
    ├── eid-infection-control-advisor/
    ├── academic-paper-polisher/
    ├── senior-executive-secretary/
    ├── nckuh-irb-protocol-generator/
    ├── cloze-mindmap-generator/
    └── study-notes-master/
```

---

## 📋 14 組升級 GEM 與 SKILL 對照清單

| 編號 | GEM 原名 (v2.0) | 對應 Skill 名稱 | 適用情境與主要功能 |
| :---: | :--- | :--- | :--- |
| **01** | `01_TANA M3 研究輪廓教練` | `tana-m3-research-outline` | 護理研究切入點展開、四特質檢核與方法學審查 |
| **02** | `02_論文拾光: 織網館` | `thesis-literature-web` | 論文第二章文獻查證之知識地圖與論證鷹架 |
| **03** | `03_TANA M1 研究陪跑教練` | `tana-m1-research-companion` | 好壞問法對照、AI 協作界線與提問訓練 |
| **04** | `04_TANA M2 經驗轉譯教練` | `tana-m2-experience-translator` | 四步將臨床口語觀察轉譯為 150-250 字背景初稿 |
| **05** | `05_論文拾光: 夢蝶館` | `thesis-topic-ideation` | 六大發想入口與五把解剖刀提煉高競爭力題目 |
| **06** | `06_論文拾光: 破曉館-1` | `thesis-ch1-architect` | 論文第一章五段式結構（背景/重要性/Gap/目的/假說） |
| **07** | `07_Prompt 精進版` | `prompt-optimizer-pro` | 提示詞優化、5種場景變體生成與紅隊測試樣例 |
| **08** | `08_論文拾光: 破曉館` | `thesis-dawn-ch1-full` | 破題第一章完整引導系統與邏輯完整性稽核報告 |
| **09** | `09_EID_IC GEM` | `eid-infection-control-advisor` | TOCC 風險評估、PPE 配置與感控處置表格化指引 |
| **10** | `10_潤飾論文助手` | `academic-paper-polisher` | 成大論文規範與 APA 7th 格式檢查與修潤建議 |
| **11** | `11_資深白秘書` | `senior-executive-secretary` | 開課通知、演講婉拒、會議公文等高規格商務草稿 |
| **12** | `12_IRB 撰寫範本` | `nckuh-irb-protocol-generator` | 成大醫院 04007 IRB 主文件、案別判定與附件打包 |
| **13** | `13_Puti-AI填空心智圖產生器` | `cloze-mindmap-generator` | 文本結構化分析、填空挖空與插畫風心智圖生圖 Prompt |
| **14** | `14_筆記神之研習筆記王` | `study-notes-master` | 研習與講義重點萃取、Emoji 排版與延伸網路資源 |

---

## 🛠️ GitHub 快速發布步驟 (1 分鐘)

1. 在 GitHub 建立一個新的 Public Repository（例如 `2026-gem-to-skill-kit`）。
2. 將本資料夾內的所有檔案（或下載自 Google Drive 的 `2026GEM_Upgraded_v2.0.zip` 解壓縮後）上傳至該 Repository。
3. 執行 Git 指令（或使用 GitHub 網頁直接上傳）：
   ```bash
   git init
   git add .
   git commit -m "feat: release 14 upgraded GEMs (v2.0) and Agent Skills"
   git branch -M main
   git remote add origin https://github.com/<YOUR_GITHUB_USERNAME>/2026-gem-to-skill-kit.git
   git push -u origin main
   ```
