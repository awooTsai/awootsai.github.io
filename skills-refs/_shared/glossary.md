# GEO/SEO 名詞白話解釋

> 四個 Skill 共用的名詞辭典。
> 報告中使用技術術語時，第一次出現需依此檔案的白話解釋輔助說明。

---

## 對客戶版（業務提案、關鍵字拓展、Prompt 拓展）

這些是客戶會看到的報告中應使用的白話解釋。

### A. 核心名詞

| 術語 | 白話解釋 |
|------|---------|
| **GEO** | 生成式引擎最佳化（Generative Engine Optimization），讓品牌在 ChatGPT、Gemini、Perplexity 等 AI 引擎中被推薦的優化技術 |
| **SEO** | 搜尋引擎最佳化（Search Engine Optimization），讓網站在 Google、Bing 等搜尋引擎中排名靠前的技術 |
| **AIO** | AI Overview，Google 搜尋結果頂部由 AI 直接回答的區塊 |
| **AI 引擎** | ChatGPT、Gemini、Perplexity、Claude、Copilot 等大型語言模型 |
| **可引用度** | AI 在回答相關問題時，引用您網站內容的可能性 |
| **平台準備度** | 網站結構、內容對 AI 引擎的友善程度 |

### B. 技術名詞（第一次出現需括號白話）

| 術語 | 白話括號 |
|------|---------|
| **H1** | 頁面主標題 |
| **H2 / H3** | 段落標題 |
| **Title** | 瀏覽器分頁標題 |
| **Meta Description** | 搜尋結果中的描述文字 |
| **Alt** | 圖片說明文字 |
| **Schema** | AI 看得懂的標籤 |
| **Schema 結構化資料** | 讓 AI 識別頁面內容類型的標記 |
| **JSON-LD** | Schema 的標準格式 |
| **canonical** | 主要網址標記（告訴 AI 哪個 URL 是該頁面的標準版本） |
| **noindex** | 不要被搜尋引擎收錄的標記 |
| **robots.txt** | 給搜尋引擎爬蟲看的網站指引檔 |
| **llms.txt** | 給 AI 看的網站簡介檔 |
| **sitemap.xml** | 網站地圖（告訴搜尋引擎網站有哪些頁面） |
| **dateModified** | 最後更新日期的結構化資料 |
| **og:title / og:image** | 分享到社群時顯示的標題與圖片 |
| **OG 完整率** | 網站頁面具備完整社群分享資訊的比例 |

### C. 評估等級

| 等級 | 對客戶說明 |
|------|---------|
| 🌱 **起步期** | 已建立基本的網站體質，但 AI 引擎時代的優化機會尚未充分掌握 |

注意：業務提案版健檢一律僅評估到 🌱 起步期。

### D. AIO 相關名詞

| 術語 | 白話解釋 |
|------|---------|
| **已觸發 AIO 的關鍵字** | Google 搜尋這些字時，您的頁面已被 AI 引用為答案來源 |
| **品牌推薦型問句** | 使用者問「XX 品牌推薦」「OO 哪家好」這類問句時的搜尋結果 |
| **知識型問句** | 使用者問「XX 是什麼」「OO 怎麼用」這類問句時的搜尋結果 |
| **延展性關鍵字** | 使用者需要進一步探索、判斷的複雜問題（不會被 AI 一句話答完） |

### E. E-E-A-T

| 字母 | 對客戶說明 |
|------|---------|
| **E** (Experience) | 經驗：作者是否有實際操作經驗 |
| **E** (Expertise) | 專業：作者是否具備該領域專業 |
| **A** (Authoritativeness) | 權威：來源是否具備產業影響力 |
| **T** (Trustworthiness) | 可信賴：內容是否經得起查證 |

四項合稱「E-E-A-T」，是 AI 判斷品牌是否具備推薦價值的核心指標。

---

## 內部版（專員體質健檢）

這些是內部專員報告中可直接使用的術語，無需白話括號（專員看得懂）。

### F. 技術 SEO 術語（專員版可直接使用）

- canonical / cross-canonical / self-canonical
- 301 / 302 redirect / Soft 404
- noindex / nofollow / dofollow
- crawl budget / crawl frequency
- index status / indexed pages
- TBT (Total Blocking Time) / LCP / CLS / Core Web Vitals
- structured data / rich result / FAQ Schema / Article Schema
- hreflang / x-default
- sitemap index / sitemap chunking
- HTTP status code / status 200 / status 404
- meta keywords（已不採用）
- Domain Authority / Page Authority / Trust Flow
- Anchor Text / dofollow link / nofollow link
- Indexing API / GSC submit
- Server Side Rendering / Client Side Rendering / Static Generation

### G. 內部開發術語（**不對客戶呈現**）

- harvester / harvester.py / Content Harvester
- RAG chunks / _rag_chunks.jsonl / _rag_summary.json
- pages.zip / _claude_briefing.md
- chunk size / chunking strategy
- embedding / pgvector / Supabase
- llms-full.txt
- Skill / SKILL.md / references
- awoo_keywords.db

這些只能在 `ada-geo-tech-audit` 內部報告中出現，**業務版健檢、關鍵字拓展、Prompt 拓展報告中嚴禁使用**。

---

## 報告中辭彙小卡的使用

### 業務提案版健檢（geo-site-audit）

報告中應有「📖 一句話讀懂的小辭彙」區塊，挑選與該客戶報告最相關的 6-8 個術語放入小卡：

```html
<section id="glossary">
  <h2>📖 一句話讀懂的小辭彙</h2>
  <div class="glossary-grid">
    <div class="g-item">
      <dt>GEO</dt>
      <dd>生成式引擎最佳化，讓 AI 主動推薦品牌</dd>
    </div>
    <!-- ... -->
  </div>
</section>
```

### 關鍵字拓展（geo-keyword-research）

關鍵字報告應提供術語：
- 關鍵字搜尋量
- 競爭性
- AIO 觸發
- 順風波段 / 補強波段 / 攻堅波段

### Prompt 拓展（geo-prompt-builder）

Prompt 報告應提供術語：
- Customer Journey
- 探索型 / 決策型 / 品牌型 Prompt
- GEO Suite

### 專員體質健檢（geo-tech-audit）

不需要術語小卡，內部專員看得懂。
