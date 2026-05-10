---
name: ada-geo-tech-audit
description: awoo 阿物科技 SEO/GEO 專員專用的網站技術盤點報告生成器（GitHub-backed v8）。當使用者提到以下任何關鍵字時必須觸發：「技術盤點」「技術檢視」「專員報告」「技術審查」「原始資料檢視」「幫技術專員做一份」「給 SEO 專員看的」「harvester 檢視」「盤點這個網站」「raw data 報告」「專員體質健檢」「成案後體質檢視」。也適用於：上傳了 harvester 產出的 pages.zip / _rag_summary.json / _rag_chunks.jsonl 並要求產出「給內部技術專員快速檢視與確認」的場景、要求驗證業務版健檢報告幻覺的場景、要求挖掘原始資料中未被 AI 展開的細節 pattern 的場景。此 Skill 與 ada-geo-site-audit（業務提案版）互補：業務版給客戶看、製造優化焦慮；本 Skill 給專員看、展開所有原始證據、明確標示 AI 主觀推論，方便專員快速驗證並回饋 harvester 改進方向。本 Skill 採 GitHub-backed 分層架構。
---

# ada-geo-tech-audit — 專員體質健檢

## 觸發條件

當使用者明確說以下任一觸發詞時啟動：
- 「技術盤點」「技術檢視」「專員報告」「技術審查」
- 「原始資料檢視」「幫技術專員做一份」「給 SEO 專員看的」
- 「harvester 檢視」「盤點這個網站」「raw data 報告」
- 「專員體質健檢」「成案後體質檢視」

或業務版健檢已出，要求做專員版內部執行檔時。

---

## 任務啟動流程

### Step 1：讀取共用內核（必讀）

依序 web_fetch：
1. `https://awootsai.github.io/skills-refs/_shared/awoo-tone.md`
2. `https://awootsai.github.io/skills-refs/_shared/seo-best-practices.md` — SEO 最佳實務（Title / Description / H1 / Schema）
3. `https://awootsai.github.io/skills-refs/_shared/visual-system.md`
4. `https://awootsai.github.io/skills-refs/_shared/glossary.md`

### Step 2：讀取 Skill 自己的核心規則

5. `https://awootsai.github.io/skills-refs/geo-tech-audit/_index.md`
6. `https://awootsai.github.io/skills-refs/geo-tech-audit/core/master-rules.md`
7. `https://awootsai.github.io/skills-refs/geo-tech-audit/core/verification-flow.md` — 驗證業務版幻覺的方法

### Step 3：讀取技術檢查清單

依任務需求 web_fetch 對應檔案：
- `https://awootsai.github.io/skills-refs/geo-tech-audit/tech-checks/url-consistency.md`
- `https://awootsai.github.io/skills-refs/geo-tech-audit/tech-checks/h-tags.md`
- `https://awootsai.github.io/skills-refs/geo-tech-audit/tech-checks/schema-jsonld.md`
- `https://awootsai.github.io/skills-refs/geo-tech-audit/tech-checks/canonical-noindex.md`
- `https://awootsai.github.io/skills-refs/geo-tech-audit/tech-checks/content-freshness.md`

### Step 4：讀取產業診斷（取對應段落）

8. `https://awootsai.github.io/skills-refs/_shared/industry-patterns.md`

### Step 5：產出 HTML 前讀視覺範本

9. `https://awootsai.github.io/skills-refs/geo-tech-audit/visual/html-template.md`
10. `https://awootsai.github.io/skills-refs/_shared/footer-signature.html`

注意：本 Skill 視覺與業務版健檢有差異——更技術導向、原始資料展開更多、無對外修飾。

### Step 6：產出與輸出

輸出到 `/mnt/user-data/outputs/{品牌英文 slug}_tech_audit_{YYYY-MM-DD}.html`，用 `present_files` 呈現。

---

## 硬性規則

### 與業務版健檢的差異化原則
- **業務版**：讓客戶感受問題、不鑽技術細節、客觀觀察語言
- **專員版（本 Skill）**：展開所有原始證據、明確標示 AI 推論 vs 爬蟲事實、技術術語可直接使用（專員看得懂）

### 必須區分「事實 vs 推論」
報告中每個觀察必須標示：
- 🔵 **爬蟲事實**：harvester 直接取得的客觀資料（頁數、Schema 類型、HTTP 狀態碼等）
- 🟡 **AI 推論**：基於資料做出的判斷（如「此頁疑似為測試頁」「此 Schema 可能未完整實作」）

讓專員一眼分辨哪些是不容質疑的事實、哪些需要進一步驗證。

### 不對客戶呈現
- 此報告**不直接給客戶看**，只給內部專員執行用
- 因此可使用內部術語（harvester、RAG chunks 等）
- 但仍需符合 SEO 業界標準術語

### 提供原始資料展開
- 列出所有 missing_samples、multiple_samples、issue_samples 完整 URL 清單
- 讓專員可以複製貼上去檢查
- 不要像業務版那樣只列 3 個範例

### 視覺風格
- 技術導向、資訊密度高
- 表格化呈現，方便專員逐項檢查
- footer 統一使用 `_shared/footer-signature.html`
- 字體最小 15px

---

## 與 ada-geo-site-audit 的關係

兩個 Skill 應該配對使用：

```
業務版健檢（給客戶）
   ↓ 客戶買單
專員版健檢（給內部）→ 比對業務版有無幻覺、確認執行細節
   ↓
專員開始實際 SEO 執行
```

專員版產出時，應主動比對業務版報告的觀察，標記任何矛盾點供阿達檢視。

---

## 對話風格

同其他 Skill，沿襲蔡阿達工作守則。

---

## v8 GitHub-backed 架構

新增規則時：
- SEO 業界基本知識 → `_shared/seo-best-practices.md`
- 本 Skill 驗證流程 → `geo-tech-audit/core/verification-flow.md`
- 新技術檢查項目 → `geo-tech-audit/tech-checks/` 新增檔案
- 罕見問題模式 → `geo-tech-audit/advanced/case-lessons.md`
