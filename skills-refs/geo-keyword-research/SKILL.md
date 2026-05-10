---
name: ada-geo-keyword-research
description: awoo 阿物科技 GEO 關鍵字主題研究報告生成器（GitHub-backed v8）。當使用者提到「關鍵字拓展」「拓字」「選字」「關鍵字研究」「GEO 關鍵字」「幫我拓展關鍵字」「關鍵字主題」「keyword research」「幫我找關鍵字」「這個品牌可以做什麼字」「幫我生成關鍵字報告」，或上傳了 _claude_briefing.md / pages.zip / _rag_chunks.jsonl 並要求分析可操作的關鍵字時觸發。本 Skill 採 GitHub-backed 分層架構，所有 references 從 https://awootsai.github.io/skills-refs/ 讀取。核心原則：(1) 關鍵字必須從客戶網站既有內容 DNA 出發；(2) 字數最少、廣義、最高搜尋量優先；(3) 每字通過搜尋量或 Google Autocomplete 驗證；(4) 三波策略（順風 / 補強 / 攻堅）；(5) 比對 awoo_keywords.db（跟著 Skill zip 走，39K+ 關鍵字 600+ 客戶歷史資料庫）。
---

# ada-geo-keyword-research — GEO 關鍵字主題研究

## 觸發條件

當使用者明確說以下任一觸發詞時啟動：
- 「關鍵字拓展」「拓字」「選字」「關鍵字研究」
- 「GEO 關鍵字」「幫我拓展關鍵字」「關鍵字主題」
- 「keyword research」「幫我找關鍵字」「這個品牌可以做什麼字」
- 「幫我生成關鍵字報告」

或上傳網站體質分析三件組並要求關鍵字分析時。

---

## 任務啟動流程

### Step 1：讀取共用內核（必讀）

依序 web_fetch：
1. `https://awootsai.github.io/skills-refs/_shared/awoo-tone.md`
2. `https://awootsai.github.io/skills-refs/_shared/customer-tone.md`
3. `https://awootsai.github.io/skills-refs/_shared/platform-partners.md`
4. `https://awootsai.github.io/skills-refs/_shared/visual-system.md`
5. `https://awootsai.github.io/skills-refs/_shared/glossary.md`

### Step 2：讀取 Skill 自己的核心規則

6. `https://awootsai.github.io/skills-refs/geo-keyword-research/_index.md`
7. `https://awootsai.github.io/skills-refs/geo-keyword-research/core/master-rules.md`
8. `https://awootsai.github.io/skills-refs/geo-keyword-research/core/selection-rules.md` — 選字鐵則（字數最短、搜尋量最高）
9. `https://awootsai.github.io/skills-refs/geo-keyword-research/core/db-integration.md` — awoo_keywords.db 比對邏輯

### Step 3：讀取三波策略

10. `https://awootsai.github.io/skills-refs/geo-keyword-research/strategies/wave-1-tailwind.md` — 順風波段（已有排名基礎）
11. `https://awootsai.github.io/skills-refs/geo-keyword-research/strategies/wave-2-reinforce.md` — 補強波段（有內容缺機會）
12. `https://awootsai.github.io/skills-refs/geo-keyword-research/strategies/wave-3-attack.md` — 攻堅波段（要新建內容）

### Step 4：讀取產業診斷（取對應段落）

13. `https://awootsai.github.io/skills-refs/_shared/industry-patterns.md`

### Step 5：產出 HTML 前讀視覺範本

14. `https://awootsai.github.io/skills-refs/geo-keyword-research/visual/html-template.md`
15. `https://awootsai.github.io/skills-refs/_shared/footer-signature.html`

### Step 6：比對 awoo_keywords.db（本地，跟著 Skill zip 走）

歷史關鍵字資料庫應放在 Skill 的 references/ 目錄下：
```
references/awoo_keywords.db  (SQLite, 39K+ keywords, 600+ clients)
```

比對邏輯：
1. 從客戶網站內容萃取候選關鍵字
2. 查詢 awoo_keywords.db，看歷史上 awoo 對相關客戶推薦過哪些字
3. 結合歷史推薦字 + 即時 web_search 補充當前趨勢字

### Step 7：產出與輸出

輸出到 `/mnt/user-data/outputs/{品牌英文 slug}_keywords_{YYYY-MM-DD}.html`，用 `present_files` 呈現。

---

## 硬性規則

### 選字鐵則（最重要）
1. **字數越短越好**：業主最在意「有搜尋量」的字
2. **topic 主關鍵字必須是字數最短、搜尋量最高的廣義字**
3. **延伸字也優先選短尾通用字**，後面才放長尾字
4. **禁止產出過長或明顯沒有搜尋量的冷門組合**
5. 每個關鍵字必須通過搜尋量驗證或 Google Autocomplete 驗證

### 三波策略命名（不可改）
- 第一波：**順風波段**（客戶已有相關內容、調整後有機會排名）
- 第二波：**補強波段**（客戶內容方向正確但缺重要面向）
- 第三波：**攻堅波段**（要新建內容才能切入的主題）

### 視覺對齊
- 與 `ada-geo-site-audit` 同一套 visual-system
- footer 統一使用 `_shared/footer-signature.html`
- 字體最小 15px

### 平台鐵律
- 比對歷史資料時，若客戶為 SHOPLINE / Shopify / 91APP / Cyberbiz / Wix 平台，依 `_shared/platform-partners.md` 規則處理

---

## 報告產出後的 awoo Suite 整合提示

報告結尾應提示：「下一步可進入 `ada-geo-prompt-builder`，將選定的關鍵字延伸成 Prompt 候選池，上 GEO Suite 追蹤」。

形成完整工作流：
```
本 Skill 拓字 → 客戶選字 → ada-geo-prompt-builder 拓 Prompt → GEO Suite 追蹤
```

---

## 對話風格

同 `ada-geo-site-audit`，沿襲蔡阿達工作守則。

---

## v8 GitHub-backed 架構

新增規則時：
- 跨 Skill 共用 → `_shared/`
- 本 Skill 選字邏輯 → `geo-keyword-research/core/`
- 三波策略調整 → `geo-keyword-research/strategies/`
- 視覺調整 → `geo-keyword-research/visual/`
