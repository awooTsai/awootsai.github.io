# 專員體質健檢歷史案例教訓

> 給專員看的內部技術案例與判斷方法。
> 與 `geo-site-audit/advanced/case-lessons.md` 是雙生檔案，但本檔案聚焦「專員執行細節」。

---

## 1. 罕見技術問題的判斷

### 1.1 首頁 Title 異常（台全牧場案例）

**業務版觀察**：「首頁 Title 設為『關於我們』」

**專員版驗證**：
1. web_fetch 該客戶首頁，確認 `<title>` 標籤實際內容
2. 檢查 og:title 是否同樣異常
3. 檢查 H1 是否也異常
4. 確認是 CMS 設定錯誤 vs 主題模板問題

**修正建議（給專員）**：
- 直接在後台修改 SEO 設定中的首頁 Title
- 同步檢查整站 Title 模板配置
- 修改後用 GSC 要求重新索引

### 1.2 雙 H1 / 隱藏 H1（HOT 大聯盟案例）

**驗證流程**：
1. 用瀏覽器 DevTools → Elements → 搜尋 `<h1`
2. 統計每頁 H1 數量
3. 檢查 class 中是否有 `uk-hidden`、`sr-only`、`display:none`

**修正動作**：
```html
<!-- 修正前 -->
<h1 class="uk-hidden">車輛搜尋</h1>
<h1><a class="link_org" href="/...">HONDA本田</a></h1>

<!-- 修正後 -->
<span class="uk-hidden">車輛搜尋</span>  <!-- 改為 span -->
<h1 class="visible">HONDA本田認證二手車</h1>  <!-- 移除內部 a -->
```

**注意**：移除 H1 內部 `<a>` 連結時，如果該連結原本是 click-through 必要，需用 JavaScript 處理，避免影響功能。

### 1.3 noindex 涉及 FAQ（Simmpo 案例）

**判斷**：FAQ 是 AIO 引用金礦，noindex 等於放棄機會。

**驗證**：
- 取得該客戶所有 noindex 頁面 URL 清單
- 檢查每個 URL 的內容類型
- 找出疑似 FAQ 的頁面

**修正建議**：
- 移除 FAQ 頁的 noindex
- 補上 FAQPage Schema
- GSC 提交 URL 要求收錄

---

## 2. cross-canonical 誤報的識別技巧

### 標準驗證流程

```bash
# 對 harvester 標記的每個 cross-canonical pair 執行
URL_A="https://example.com/page"
URL_B="https://example.com/page/"

curl -s "$URL_A" -o /tmp/a.html
curl -s "$URL_B" -o /tmp/b.html

# 比對 canonical
grep -oP 'rel="canonical"[^>]+href="[^"]+"' /tmp/a.html
grep -oP 'rel="canonical"[^>]+href="[^"]+"' /tmp/b.html
```

### 三種結果處理

| 結果 | 判斷 |
|------|------|
| 兩個 canonical 都指向同一網域 | 誤報（尾斜線差異） |
| canonical 指向不同子網域（同主域） | 需深入確認意圖 |
| canonical 指向完全不同網域 | 真實 cross-canonical |

---

## 3. SHOPLINE 客戶的特殊執行考量

### 3.1 平台限制下的可執行項目

| 可執行 | 不可執行（平台限制） |
|-------|------------------|
| Title / Description 自訂 | 商品頁模板結構 |
| 商品 Schema 補強欄位 | 系統自動產生的部分 |
| H1 內容調整 | URL 結構 |
| 文章內容更新 | sitemap.xml 格式 |
| 加 FAQ Schema | robots.txt 預設規則 |

### 3.2 平台識別線索

確認 SHOPLINE 的證據：
- HTML 中 `Rendered '*.liquid'` 註解
- `{{ ... | translate }}` 標籤
- 商品 URL 模式 `/products/[slug]`

注意：URL 模式單獨判斷不夠（Shopify 也用相同模式），需多重證據。

### 3.3 Schema 的平台特性

- SHOPLINE 自動產生 Product / BreadcrumbList Schema
- 但不自動產生 FAQPage、Organization、ProfilePage
- 這三類需手動建置（透過後台或客製程式碼）

---

## 4. og-fallback H1 的成因與修正

### 成因
- 主題模板未為頁面設定獨立 H1
- 退回讀取 og:title 作為頁面標題
- 結果：頁面 H1 = og:title = 商品名稱（缺少 SEO 優化空間）

### 修正建議
- 修改主題模板，為商品頁、文章頁加上獨立 H1
- H1 可比 og:title 更口語、更長
- 範例：
  - og:title：`葉黃素膠囊 60 顆裝`（社群分享用）
  - H1：`葉黃素膠囊推薦 — 60 顆裝完整補充眼部營養`（SEO 用）

---

## 5. 動態參數 URL 的處理（HOT 大聯盟）

### 情境
```
https://hotcar.com/CarFilter?vBrand=43
https://hotcar.com/CarFilter?vBrandWord=T&vBrand=43
```

### 判斷
應以 `vBrandWord=T&vBrand=43` 為主版本（資訊較完整）。

### 執行方式
- 修改所有內部連結指向主版本（含麵包屑、HTML Sitemap）
- 主版本 canonical 指向自己
- 非主版本 canonical 指向主版本
- GSC 設定參數處理（如可能）

---

## 6. dateModified 同步的實作方式

### 方式 1（推薦）：CMS 同步
修改 CMS 設定，每次內容更新時自動更新 dateModified。

### 方式 2（fallback）：手動加欄位
- 前台保留 datePublished 為原始發布日
- 新增「最後更新」欄位
- dateModified 結構化資料同步「最後更新」

### 方式 3（最差）：每次手動改
- 每次更新文章時，手動改 dateModified
- 容易遺漏，不建議

---

## 7. 加速文章收錄（京宇實戰）

### GSC 手動提交（基本方式）
1. 新文章上稿後立即 GSC 上方欄位輸入 URL
2. 點 Enter
3. 點選「要求建立索引」

### Google Indexing API（進階方式）
適合大量文章批次提交：
- 在 GSC 設定擁有者權限給 awoo 服務帳號（`awoo-index@carbon-ruler-341608.iam.gserviceaccount.com`）
- awoo 串接 Indexing API 後，可主動通知 Google
- 適用於每月新增文章 ≥10 篇的客戶

---

## 8. 連結誘餌（Link Bait）執行細節

詳見 `_shared/industry-patterns.md` §3.3。

服務型品牌的 6 種類型：
- A. 範本/資源頁面（門檻低，建議優先）
- B. 小工具/計算器（門檻高，效益最強）
- C. 研究洞察、實驗數據（門檻高）
- D. 當事人故事分享（需當事人同意）
- E. 公共熱門話題（需即時性）
- F. 資訊圖表（容易被引用與分享）

---

## 9. 內容差距分析（Content Gap）流程

### 京宇法律專員實戰
1. 用 ahrefs 分析自家文章 vs 競業排名上的關鍵字差異
2. 找出競業有排名、自家未排名的關鍵字
3. 將這些關鍵字補回自家文章的對應 H2/H3 段落
4. 補充內容、設置 H 標籤、更新 dateModified

### 工具
- Ahrefs Content Gap 功能
- Semrush Keyword Gap
- 競品 sitemap.xml 分析

---

## 10. 卡關時的標準處理

### 不確定某個觀察的處理方式

1. **先問**：這個問題對 GEO/AIO 有實質影響嗎？
   - 是 → 繼續
   - 否（如純 SEO 細節，不影響 AI 引用）→ 列入「次要項目」

2. **再問**：能否提供原始資料佐證？
   - 是 → 寫進報告 + 展開原始資料
   - 否 → 不寫進報告

3. **最後問**：與業務版報告是否一致？
   - 一致 → 加深專員執行細節
   - 不一致 → 標記矛盾點，回報阿達

---

## 11. 罕見業態的查找順序

當客戶業態不在標準產業中：

1. 先看是否接近某個既有業態
2. 若完全新業態：
   - 找 3-5 個競業網站當參考
   - 記錄該業態的常見模式
   - 建議寫進 `_shared/industry-patterns.md`
3. 與阿達討論是否要建立新產業段落
