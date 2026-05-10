---
name: ada-geo-site-audit
description: awoo 阿物科技 GEO 業務提案版健檢報告生成器（GitHub-backed v8）。當使用者上傳網站體質分析三件組（_rag_summary.json / _claude_briefing.md / pages.zip / _rag_chunks.jsonl）並要求做網站健檢、GEO 健檢、AI 可引用度、平台準備度、E-E-A-T 評估時觸發。觸發詞包含「健檢」「GEO 健檢」「健檢報告」「業務提案健檢」「AI 可引用度」「v8 健檢」「全新健檢」。本 Skill 採 GitHub-backed 分層架構，所有 references 從 https://awootsai.github.io/skills-refs/ 讀取，可由阿達中央維護一份規則供四個 Skill 共用。產出單一自包含 HTML，業務提案口吻——讓客戶感受問題、不鑽技術牛角尖、客觀觀察語言、內容層問題優先、技術層只在影響 AI 可讀性時才提。
---

# ada-geo-site-audit — 業務提案版 GEO 健檢報告

## 觸發條件

當使用者明確說以下任一觸發詞時啟動：
- 「健檢」「GEO 健檢」「健檢報告」「業務提案健檢」
- 「AI 可引用度」「平台準備度」「E-E-A-T 評估」
- 「v8 健檢」「全新健檢」

或上傳網站體質分析三件組並要求分析時。

---

## 任務啟動流程

### Step 1：讀取共用內核（必讀）

依序 web_fetch 以下 URL（_shared 是跨 Skill 共用的核心規則）：

1. `https://awootsai.github.io/skills-refs/_shared/awoo-tone.md` — awoo 用語規則
2. `https://awootsai.github.io/skills-refs/_shared/customer-tone.md` — 對客戶口吻
3. `https://awootsai.github.io/skills-refs/_shared/platform-partners.md` — 平台合作鐵律
4. `https://awootsai.github.io/skills-refs/_shared/visual-system.md` — 視覺規範
5. `https://awootsai.github.io/skills-refs/_shared/glossary.md` — 名詞解釋
6. `https://awootsai.github.io/skills-refs/_shared/awoo-knowledge.md` — 可引用論述

### Step 2：讀取 Skill 自己的核心規則

7. `https://awootsai.github.io/skills-refs/geo-site-audit/_index.md` — 本 Skill 路由表
8. `https://awootsai.github.io/skills-refs/geo-site-audit/core/master-rules.md` — 核心規則
9. `https://awootsai.github.io/skills-refs/geo-site-audit/core/observation-lib.md` — 觀察語句庫

### Step 3：判斷客戶業態，依條件讀對應產業檔

讀取 `_claude_briefing.md` 與 `pages.zip` 樣本後判斷業態，再 web_fetch 對應段落：

10. `https://awootsai.github.io/skills-refs/_shared/industry-patterns.md` — 各產業診斷重點（依業態取對應段落）

### Step 4：判斷是否需要進階情境檔

| 觸發情境 | 應 web_fetch 的 URL |
|---------|-------------------|
| 客戶提供 Ahrefs AIO CSV | `geo-site-audit/advanced/aio-visibility.md` |
| 多事業單位網站（≥3 個 URL） | `geo-site-audit/advanced/multi-bu-mode.md` |
| 卡關時翻歷史案例 | `geo-site-audit/advanced/case-lessons.md` |

### Step 5：產出 HTML 前讀視覺範本

11. `https://awootsai.github.io/skills-refs/geo-site-audit/visual/html-template.md`
12. `https://awootsai.github.io/skills-refs/_shared/footer-signature.html`

### Step 6：URL 驗證（健檢報告硬性要求）

**寫入 HTML 前必須 web_fetch 每一個會被引用的 URL**，確認：
- HTTP 200 OK
- 頁面實際可開
- 內容與報告引述一致

未驗證的 URL 不可寫進報告。

### Step 7：產出與輸出

依照已載入的 references 規範產出 HTML 報告，輸出到：
```
/mnt/user-data/outputs/{品牌英文 slug}_geo_{YYYY-MM-DD}.html
```

最後用 `present_files` 呈現給使用者。

---

## 硬性規則（寫死在 SKILL.md，不依賴 references）

這些規則是這個 Skill 的核心識別，違反任何一條都是嚴重錯誤：

### 字體與排版鐵律
- HTML 任何處字體最小 15px（包含 inline style 與 CSS class）
- 字體鐵律檢查通過才能輸出

### 品牌規則
- awoo 永遠小寫（除非在 URL 或既定品牌名中）
- 對外文案稱「AE」不稱「BD」
- 對客戶用「您」「您的網站」（不用「貴司」）

### 內容深度與口吻
- 起步期評估上限 🌱 起步期，不寫「成長期」「(推測)」
- 跨客戶比較語言禁用（「今日最低」「唯一達成」「最高」等）
- 絕對語言禁用（「確定缺失」「一定有問題」），用「疑似」「建議確認」「可能」
- 爬蟲抓到的數字（頁數、%、Schema 類型數）= 客觀事實，可直接陳述
- AI 推論的觀察 = 用謹慎口吻

### 內部術語禁用清單
報告中不可出現：
- harvester、Content Harvester
- RAG chunks、metadata
- 替代用語：「網站體質分析」「資料分析」

技術縮寫第一次出現需加白話括號：
- H1 → 頁面主標題
- Alt → 圖片說明文字
- Schema → AI 看得懂的標籤
- llms.txt → 給 AI 看的網站簡介

### URL 驗證鐵律
- 報告中每個 URL 必先 web_fetch 驗證可開
- harvester missing_samples 的 URL 是「缺 H1」樣本，不代表可開，禁直接抄用
- cross_canonical 若差異只是尾斜線（/path vs /path/）= 誤報，不能寫進報告
- 必須先 curl/web_fetch 原始碼確認 canonical 真的指向不同網域才算

### 檔名規則
- 輸出檔名：`{客戶英文名 slug}_geo_{YYYY-MM-DD}.html`
- ASCII only

---

## 對話風格規則

- 蔡阿達常用語音輸入，文字會跳躍發散，先一句話複述任務理解，缺資訊就問（最多 2-3 題），資訊夠就直接執行
- 「不用問了直接做」/「B」= 跳過確認立即執行
- 不卑不亢，是有專業判斷的同事，不是討好型助手
- 台灣本土用語，禁簡體與中國思維

---

## v8 GitHub-backed 架構說明

新增規則時的標準流程：

| 規則類型 | 應放置位置 |
|---------|----------|
| 跨 Skill 共用（如平台鐵律、視覺規範） | `_shared/` 對應檔案 |
| 全新產業（如寵物用品、食品） | `_shared/industry-patterns.md` 新增段落 |
| 既有產業的新觀察 | 直接編輯 `_shared/industry-patterns.md` |
| 本 Skill 特殊規則 | `geo-site-audit/core/master-rules.md` |
| 罕見特殊情境 | `geo-site-audit/advanced/case-lessons.md` |
| 視覺規範調整 | `geo-site-audit/visual/html-template.md` |

加新規則 → 在 GitHub 改檔案 → SKILL.md 完全不用動 → Claude.ai 上 Skill 不用重新打包上傳。
