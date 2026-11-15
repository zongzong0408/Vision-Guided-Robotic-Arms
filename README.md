# 🤖 視覺導引機器手臂：從眼睛到大腦的智慧協調

### Vision-Guided Robotic Manipulators — LLM Wiki & Interactive Teaching Slides

**專為零基礎初學者打造的視覺機器人入門知識庫，結合「來源隔離」與「雙重檢查迴圈（Dual-Loop Gated Graph）」的 Agentic 工作流實作。**

[🚀 立即瀏覽線上簡報](https://zongzong0408.github.io/Vision-Guided-Robotic-Arms/) · [📚 閱讀 LLM Wiki 知識庫](./llm_wiki/index.md) · [📋 檢視完整檢查與重寫紀錄](./output/audit_trace.md)

## 1. 為什麼做這個專案？（專案背景與核心痛點）

傳統工廠裡的工業機器手臂其實就像個「精確的盲人」**——工程師在程式裡把移動座標寫死，手臂就日復一日照表操課；只要輸送帶上的零件歪個一公分，它不是抓空就是直接撞上去。現代機器人學把**「電腦視覺」**跟**「控制工程」接在一起，等於幫手臂裝上眼睛和大腦，讓它能看懂現場狀況隨機應變。

本專案透過 **AI 代理人工作流（Agentic Workflow）**，將 7 篇視覺機械手臂領域的碩士學位論文，從艱澀的數學公式與文獻中抽絲剝繭，降維轉譯為一套連大一新生、文組同學都能無痛看懂的 **LLM Wiki 知識庫**與**單檔互動式教學 HTML 簡報**。

## 2. 知識庫架構與 7 篇核心論文地圖

我們捨棄了傳統「一篇論文寫一段摘要」的流水帳做法，改用機器人運作的「眼、腦、手」靈魂三問重組知識體系：

### 📖 LLM Wiki 模組導覽（`llm_wiki/`）

| 檔案名稱                                                                                                      | 學習單元與核心隱喻          | 解決的靈魂問題                                                | 對應文獻              |
| --------------------------------------------------------------------------------------------------------- | ------------------ | ------------------------------------------------------ | ----------------- |
| [**`index.md`**](./llm_wiki/index.md)                                                                     | **知識庫導讀與全景地圖**     | 建立「眼-腦-手」心智模型、初學者黑話速查表（DOF, PBVS, SLAM）                | 全部 7 篇            |
| [**`01_mechanics_and_kinematics.md`**](./llm_wiki/01_mechanics_and_kinematics.md)                         | **【基礎篇】骨骼、關節與肌肉**  | **手怎麼動？** 正逆運動學幾何解、眼在手 vs. 眼到手對決、梯形與三次多項式減震            | `[文獻 2, 5, 6, 7]` |
| [**`02_vision_and_depth_perception.md`**](./llm_wiki/02_vision_and_depth_perception.md)                   | **【感官篇】從平面到立體視覺**  | **眼看哪裡？** 雙目視差、**500mm 深度量測黃金分界律**、卡爾曼濾波器動態預判          | `[文獻 1, 2, 6, 7]` |
| [**`03_advanced_intelligence_and_evaluation.md`**](./llm_wiki/03_advanced_intelligence_and_evaluation.md) | **【大腦篇】自主探索與精度體檢** | **腦怎麼想？** 主動視覺 A3C 強化學習、GTAM 特徵記憶、**SLAM 0.0353mm 體檢** | `[文獻 1, 3, 4]`    |

### 🎓 原始文獻溯源對照（`raw_sources/`）

- **`[文獻 1]`** 《動態目標抓取與分類之智慧型機器手臂的設計與實作》（暨南大學，2026）— *YOLOv10 + 卡爾曼濾波器預測未來落點*
- **`[文獻 2]`** 《影像視覺結合六軸機器手臂夾取堆疊球形物件之研究》（屏科大，2025）— *揭露 500mm 幾何測距 vs. RGB-D 深度相機黃金分界律*
- **`[文獻 3]`** 《應用同步定位與建圖技術於工業機器手臂之性能評估》（臺灣大學，2025）— *以 2D LiDAR SLAM 達成 0.0353 mm 超高精度，成本降至 1/100*
- **`[文獻 4]`** 《機器手臂夾取任務中基於可夾取性引導深度強化學習之主動視角選取》（臺灣科大，2024/2025）— *雜亂堆疊下主動換視角與 GTAM 潛在特徵記憶*
- **`[文獻 5]`** 《機器手臂視覺抓取系統》（中正大學）— *位置基準視覺伺服（PBVS）與影像／馬達非同步時序解耦*
- **`[文獻 6]`** 《立體視覺伺服機器手臂之智慧追蹤控制的研究》（中原大學）— *雙目立體視差與三次多項式內插避震控制*
- **`[文獻 7]`** 《視覺導引四軸機器手臂之製作與物件抓取控制》（東南科大）— *CAD/CAE 動態扭力模擬與解析幾何逆運動學（< 1ms）*

## 3. 系統架構與雙重檢查迴圈（Dual-Loop Gated Graph）

為了防止 AI 在生成簡報時「偷看原始論文瞎掰」或「直接堆砌初學者看不懂的學術黑話」，本專案採用了結合來源隔離（Source Isolation）**與**檢查左移（Shift-Left Verification）的狀態機工作流：

```
flowchart TD
    subgraph Phase1["Phase 1：知識蒸餾與 Wiki 建置"]
        A["7 篇原始碩士論文 PDF<br/>(raw_sources/)"] --> B["提取核心概念<br/>(自動略過文獻與純數學附錄)"]
        B --> C{"閘門 1：人機架構討論<br/>(先討論、後生成)"}
        C -- "確認 1+3 架構並局部修補" --> D["生成 4 份 LLM Wiki (.md)"]
        D --> E["🔒 啟動嚴格來源隔離<br/>(封鎖 raw_sources 存取)"]
    end

    subgraph Phase2["Phase 2：教學大綱審查迴圈 (Loop 1)"]
        E --> F["僅讀取 llm_wiki/<br/>規劃 8 頁初版大綱 (v1)"]
        F --> G{"閘門 2：教學助教審查<br/>(Pedagogical Shift-Left Gate)"}
        G -- "❌ 抓出黑話過多 / 缺生活比喻" --> H["退回重寫改良版大綱 (v2)<br/>加入比喻與量化實證數據"]
        H --> G
        G -- "✅ 通過初學者門檻與溯源檢查" --> I["定案 v2 教學大綱"]
    end

    subgraph Phase3["Phase 3：HTML 編譯與視覺驗收 (Loop 2)"]
        I --> J["編譯零外部依賴單檔簡報<br/>(output/presentation.html)"]
        J --> K{"閘門 3：瀏覽器實機視覺驗收<br/>(Browser Visual Audit)"}
        K -- "❌ 抓出橫向捲軸 / Raw LaTeX" --> L["修復響應式 CSS 與語意 HTML"]
        L --> K
        K -- "✅ 全視口無破版 (PASSED)" --> M["輸出最終簡報與完整稽核日誌<br/>(audit_trace.md)"]
    end

    classDef gate fill:#f59e0b,stroke:#d97706,stroke-width:2px,color:#fff;
    classDef reject fill:#ef4444,stroke:#b91c1c,stroke-width:2px,color:#fff;
    classDef pass fill:#10b981,stroke:#047857,stroke-width:2px,color:#fff;
    class C,G,K gate;
    class H,L reject;
    class M pass;
```

### ⚙️ 三大核心工程設計亮點

1. **檢查左移（Shift-Left Testing）**：在純文字的大綱階段（Phase 2）就引入「嚴格教學助教」檢查閘門。把「逆運動學非線性解析」、「單應性矩陣」等硬核名詞在這個階段就退回改寫成生活比喻，修改成本只要幾秒鐘，徹底避免寫完數百行 HTML/CSS 後才推倒重來。
2. **嚴格來源隔離（Source Isolation）**：Wiki 建構完成並修補筆誤後，Phase 2 與 Phase 3 強制**只能讀取 `llm_wiki/`**，切斷與原始 PDF 的連線，確保簡報每頁底部的 `[文獻 X]` 溯源標註 100% 真實可靠。
3. **瀏覽器實機驗收閉環（Loop 2）**：在無外部 CDN 依賴（離線可開）的條件下，透過自動化瀏覽器實測 8 頁排版，攔截並修復了窄螢幕 ASCII 圖解橫向溢出、離線無 KaTeX 導致 Raw LaTeX 符號（如 `$Z$`）外露等 4 項前端瑕疵（完整紀錄詳見 [`output/audit_trace.md`](./output/audit_trace.md)）。

## 4. 倉庫結構與雙分支部署架構

本倉庫採用 **Dual-Branch Separation of Concerns（雙分支職責分離）** 設計，將完整的知識庫開發歷史與對外展示的純淨靜態網頁徹底解耦：

```
zongzong0408/Vision-Guided-Robotic-Arms
│
├── 🌿 Branch: main (完整專案原始碼與知識庫)
│   ├── README.md                              # 專案總覽與架構說明文件
│   ├── llm_wiki/                              # 結構化 Markdown 知識庫 (Single Source of Truth)
│   │   ├── index.md
│   │   ├── 01_mechanics_and_kinematics.md
│   │   ├── 02_vision_and_depth_perception.md
│   │   └── 03_advanced_intelligence_and_evaluation.md
│   ├── output/                                # 編譯產物與可觀測稽核紀錄
│   │   ├── presentation.html                  # 100% 零外部依賴 8 頁互動教學簡報
│   │   ├── audit_trace.md                     # 雙重檢查迴圈與瑕疵修復完整足跡
│   │   └── submission_report.md               # 專案總結與工程反思報告
│   └── raw_sources/                           # 7 篇原始研究論文 PDF
│
└── 🌿 Branch: gh-pages (Orphan Branch 靜態網站部署分支)
    └── index.html                             # 由 output/presentation.html 編譯發布，驅動 GitHub Pages
```

## 5. 快速預覽與本地執行（Quick Start）

這份教學簡報採用 **Zero-Dependency Standalone HTML5** 架構，所有 CSS Grid 雙欄卡片佈局與 Vanilla JS 翻頁邏輯皆內嵌於單一檔案中，**不需要安裝 Node.js、Python 或任何套件，甚至完全斷網也能流暢操作**：

1. **線上直接瀏覽（推薦）**： 點擊前往 👉 [**https://zongzong0408.github.io/Vision-Guided-Robotic-Arms/**](https://zongzong0408.github.io/Vision-Guided-Robotic-Arms/)

2. **本機離線開啟**：
   
   ```
   git clone https://github.com/zongzong0408/Vision-Guided-Robotic-Arms.git
   cd Vision-Guided-Robotic-Arms
   # 直接用任何瀏覽器雙擊打開 output/presentation.html 即可！
   ```

3. **簡報操作快捷鍵**：
   
   - `→` / `Space` / `PageDown`：下一頁（或手機/平板向左滑動）
   - `←` / `PageUp`：上一頁（或向右滑動）
   - `Home` / `End`：快速跳至第一頁 / 最後一頁
