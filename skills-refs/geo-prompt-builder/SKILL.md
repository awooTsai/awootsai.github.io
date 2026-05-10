---
name: ada-geo-prompt-builder
description: awoo 阿物科技 GEO Prompt 延伸建議工具（GitHub-backed v8）。當客戶已選好關鍵字、需要延伸出可上 GEO Suite 追蹤的 Prompt 候選池時觸發。觸發詞：「幫我延伸 Prompt」「關鍵字轉 Prompt」「Prompt 建議」「GEO Prompt」「關鍵字延伸問句」「追蹤用的 Prompt」「客戶選好字了幫我延伸」「給我候選 Prompt 清單」。每組關鍵字產出 4-7 條 Prompt（總候選池為待選數的 2 倍），按 Customer Journey 分三種意圖（探索 / 決策 / 品牌），每組必須至少有 1 條品牌型 Prompt 確保品牌被提及機會。視覺對齊 ada-geo-site-audit + ada-geo-keyword-research。本 Skill 採 GitHub-backed 分層架構，所有 references 從 https://awootsai.github.io/skills-refs/ 讀取。
---

# ada-geo-prompt-builder — GEO Prompt 候選池拓展

## 觸發條件

當客戶已選定關鍵字，使用者說：
- 「幫我延伸 Prompt」「關鍵字轉 Prompt」「Prompt 建議」
- 「GEO Prompt」「關鍵字延伸問句」「追蹤用的 Prompt」
- 「客戶選好字了幫我延伸」「給我候選 Prompt 清單」

或上傳了關鍵字清單並要求拓展 Prompt 時。

---

## 任務啟動流程

### Step 1：讀取共用內核（必讀）

依序 web_fetch：
1. `https://awootsai.github.io/skills-refs/_shared/awoo-tone.md`
2. `https://awootsai.github.io/skills-refs/_shared/customer-tone.md`
3. `https://awootsai.github.io/skills-refs/_shared/visual-system.md`

### Step 2：讀取 Skill 自己的核心規則

4. `https://awootsai.github.io/skills-refs/geo-prompt-builder/_index.md`
5. `https://awootsai.github.io/skills-refs/geo-prompt-builder/core/master-rules.md`
6. `https://awootsai.github.io/skills-refs/geo-prompt-builder/core/extension-logic.md` — 雙倍候選池邏輯

### Step 3：讀取三種 Customer Journey 意圖

7. `https://awootsai.github.io/skills-refs/geo-prompt-builder/customer-journey/exploration.md` — 探索型
8. `https://awootsai.github.io/skills-refs/geo-prompt-builder/customer-journey/decision.md` — 決策型
9. `https://awootsai.github.io/skills-refs/geo-prompt-builder/customer-journey/brand.md` — 品牌型

### Step 4：產出 HTML 前讀視覺範本

10. `https://awootsai.github.io/skills-refs/geo-prompt-builder/visual/html-template.md`
11. `https://awootsai.github.io/skills-refs/_shared/footer-signature.html`

### Step 5：比對客戶現有內容（如有 _rag_chunks.jsonl）

若使用者提供 `_rag_chunks.jsonl`，先比對：
- 客戶網站是否有對應內容承接此 Prompt
- 沒有對應內容的 Prompt 標記為「需先補內容」

### Step 6：產出與輸出

輸出到 `/mnt/user-data/outputs/{品牌英文 slug}_prompts_{YYYY-MM-DD}.html`，用 `present_files` 呈現。

---

## 硬性規則

### 候選池數量規則
- 每個關鍵字延伸 **4-7 條 Prompt**
- 總候選池 = 待選 Prompt 數的 **2 倍**（例如客戶最終要選 90 條，產 180 條候選）
- 每組關鍵字 **至少有 1 條品牌型 Prompt**，確保品牌被提及機會

### 三意圖分類比例（建議基準，可依產業調整）
- 探索型 (Exploration)：約 30-40%
- 決策型 (Decision)：約 40-50%
- 品牌型 (Brand)：約 20-30%

### Prompt 撰寫風格
- 使用真實使用者會問的口吻（口語化、完整問句）
- 不要寫成搜尋關鍵字的格式（如「葉黃素 推薦」）
- 應寫成完整問句（如「我想找葉黃素，有什麼推薦的品牌？」）

### 視覺對齊
- 與 `ada-geo-site-audit` + `ada-geo-keyword-research` 同一套 visual-system
- footer 統一使用 `_shared/footer-signature.html`
- 字體最小 15px

---

## 報告結構

每組關鍵字呈現方式：
```
[主關鍵字]
  ├─ 探索型 Prompt（X 條）
  ├─ 決策型 Prompt（X 條）
  └─ 品牌型 Prompt（X 條）
       ↓ 標註：是否有客戶現有內容承接
```

提供「一鍵複製」功能，方便上傳 GEO Suite。

---

## 對話風格

同其他 Skill，沿襲蔡阿達工作守則。

---

## v8 GitHub-backed 架構

新增規則時：
- 跨 Skill 共用 → `_shared/`
- Customer Journey 意圖調整 → `geo-prompt-builder/customer-journey/`
- 雙倍候選池邏輯 → `geo-prompt-builder/core/extension-logic.md`
