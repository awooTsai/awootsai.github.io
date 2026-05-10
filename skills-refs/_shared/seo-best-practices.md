# SEO/GEO 最佳實務

> 從 awoo 近 3 年（2022-2026）約 40 份 SEO 建議書精煉而來的執行細節。
> 主要供 `ada-geo-tech-audit`（專員版）使用，其他 Skill 也可以引用。
>
> 涵蓋：Title / Description / H1、Schema、URL 處理、文章新鮮度、E-E-A-T、AIO 策略。

---

## 1. Title / Description / H1 優化

### 1.1 Title 規範

- **長度**：50-60 字元（中文約 25-30 字）
- **結構**：主關鍵字 → 延伸字 → 品牌名
- **電商分類頁格式**：`[主關鍵字]/[延伸字 A]/[延伸字 B] - 品牌名`
- **法律/服務文章格式**：`[問題核心]？[核心解答]，[品牌訴求]！`

### 1.2 Title 與 H1 一致性

- Title 與 H1 建議保持一致（強化關鍵字訊號）
- 但允許 H1 比 Title 更口語、更長
- 注意系統自動附加品牌後綴（如 `- PORTER INTERNATIONAL`），不需在 Title 重複品牌名

**實例（PORTER 包包分類頁）**：
- 原：`WOMEN 長裙 - GU台灣`
- 改：`WOMEN 長裙/牛仔裙/百褶裙/蛋糕裙 - GU台灣`

**實例（京宇法律服務文章）**：
- 原：`ㄟ到別害怕！車禍保障聖經在這裡`
- 改：`車禍刑事責任有哪些？被告過失傷害如何自保？車禍保障聖經`

### 1.3 Description 規範

- **長度**：120-155 字元（中文約 60-75 字）
- **結構**：首句出現主關鍵字 → 延伸字 → 品牌差異化說明 → 行動呼籲
- **多樣性**：每頁 Description 差異度應 > 70%

### 1.4 H1 規範

- **每頁只能有一個 H1**
- H1 應與 Title 語意相關但不完全相同
- H1 可比 Title 更口語、更長
- **不應再使用 meta keywords**：Google 早已不採用，反而洩漏關鍵字策略

### 1.5 雙 H1 / 隱藏 H1 問題（HOT 大聯盟案例）

**常見情境**：系統共用 H1 + 隱藏客製 H1 = 雙 H1

**診斷步驟**：
1. 瀏覽器 DevTools → Elements → 搜尋 `<h1`
2. 看是否有多個 `<h1>` 存在
3. 檢查是否有「隱藏 H1」（`uk-hidden`、`sr-only` 等 class）

**修正建議**：
- 將原本的共用 H1（如「車輛搜尋」）改為 `<span>` 或 `<p>` 標籤
- 保留唯一的頁面專屬 H1
- 確認 `<h1>` 內**不應包含** `<a>` 連結

```html
<!-- 錯誤 -->
<h1><a class="link_org" href="/...">HONDA本田</a></h1>

<!-- 正確 -->
<h1 class="uk-hidden">HONDA本田認證二手車</h1>
```

---

## 2. H 標籤結構優化

### 2.1 層次原則

```
H1（頁面主題，唯一一個）
  H2（主要段落主題）
    H3（子段落）
      H4（細項說明）
```

### 2.2 圖片轉文字化

**診斷方法**：瀏覽器查看「選取文字」能力
- 若標題文字無法被選取 → 疑似圖片
- DevTools 確認：`<img>` 包裝的 H1/H2 → 改為真實文字 + CSS 排版

### 2.3 服務型文章 H 標籤潤飾範例（京宇）

H 標籤應「自然包含關鍵字」並具備吸引點擊的口吻：

| 原 H2 | 潤飾後 H2 |
|-------|---------|
| 「我國現行債務催收手段」 | 「欠錢不還怎麼辦？我國現行債務催收手段」 |
| 「常見的債務關係」 | 「討債前，先了解我國常見的債務關係」 |
| 「執行名義是什麼？」 | 「我該怎麼把錢拿回來？債務催收的執行名義又是什麼？」 |

**潤飾原則**：
- 加入問句吸引點擊
- 自然置入目標關鍵字
- 段落彼此有邏輯關聯

---

## 3. 結構化資料（Schema）

### 3.1 BreadcrumbList JSON-LD

```html
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "BreadcrumbList",
  "itemListElement": [
    { "@type": "ListItem", "position": 1, "name": "首頁", "item": "https://example.com/" },
    { "@type": "ListItem", "position": 2, "name": "分類名稱", "item": "https://example.com/category/" }
  ]
}
</script>
```

### 3.2 Article JSON-LD

```html
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "Article",
  "headline": "文章標題",
  "datePublished": "2025-01-01",
  "dateModified": "2026-05-01",
  "author": { "@type": "Person", "name": "作者名稱" }
}
</script>
```

**重點**：`dateModified` 應在每次更新文章時同步更新，這是 Google 與 LLM 判斷內容新鮮度的主要訊號

### 3.3 FAQPage JSON-LD（對 AIO 引用最重要）

```html
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "FAQPage",
  "mainEntity": [
    {
      "@type": "Question",
      "name": "Q1：問題文字",
      "acceptedAnswer": {
        "@type": "Answer",
        "text": "答案文字，建議完整且包含 HTML 標籤如 <ul><li>"
      }
    }
  ]
}
</script>
```

**執行流程**：
1. 確認文章已有 Q&A 內容
2. 加入 FAQ Schema
3. 用 Google 複合式搜尋結果測試工具驗證：https://search.google.com/test/rich-results

### 3.4 Product JSON-LD

```html
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "Product",
  "name": "商品名稱",
  "description": "商品描述",
  "brand": { "@type": "Brand", "name": "品牌名稱" },
  "offers": {
    "@type": "Offer",
    "price": "1290",
    "priceCurrency": "TWD",
    "availability": "https://schema.org/InStock"
  },
  "aggregateRating": {
    "@type": "AggregateRating",
    "ratingValue": "4.5",
    "reviewCount": "120"
  }
}
</script>
```

### 3.5 Organization JSON-LD（服務型品牌核心）

```html
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "Organization",
  "url": "https://example.com/",
  "logo": "https://example.com/images/logo.svg",
  "name": "品牌中文名稱",
  "description": "品牌介紹（簡潔說明定位、特色、累積實績）",
  "address": {
    "@type": "PostalAddress",
    "streetAddress": "...",
    "addressLocality": "台北市",
    "addressCountry": "TW",
    "postalCode": "..."
  },
  "contactPoint": { "@type": "ContactPoint", "telephone": "+886-..." }
}
</script>
```

**Why this matters**: 2023/11/29 起 Google 官方擴大 Organization Schema 支援範圍，對品牌知識面板呈現極為關鍵。**建議放在首頁 `<head></head>` 區塊**。

### 3.6 ProfilePage JSON-LD（律師、醫師、顧問等個人專業頁）

```html
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "ProfilePage",
  "mainEntity": {
    "@type": "Person",
    "name": "張律師",
    "jobTitle": "律師",
    "url": "https://example.com/team/zhang",
    "image": "https://example.com/images/zhang.jpg",
    "worksFor": { "@type": "Organization", "name": "京宇法律事務所" },
    "alumniOf": { "@type": "EducationalOrganization", "name": "國立台灣大學法律學院" },
    "sameAs": [
      "https://scholar.google.com/...",
      "https://linkedin.com/in/..."
    ]
  }
}
</script>
```

**E-E-A-T 強化重點**：
- `sameAs` 連結至個人的學術論文、專業文章、社群
- `alumniOf` 顯示學經歷
- 配合個人介紹頁面「論文/文章/社群連結」區塊

---

## 4. URL 一致性處理

### 4.1 常見不一致情境

```
情境一：帶 / vs 不帶 /
https://example.com/category   ← 應擇一為主
https://example.com/category/

情境二：www vs non-www
https://example.com/
https://www.example.com/

情境三：參數版本（HOT 大聯盟）
https://hotcar.com/CarFilter?vBrand=43
https://hotcar.com/CarFilter?vBrandWord=T&vBrand=43  ← 應以此為準

情境四：首頁版本
https://www.example.com           ← 主版本
https://www.example.com/Home/Index   ← 應 301 至主版本
```

### 4.2 解決方法（優先順序）

1. **301 轉址**：將舊 URL 永久轉向正確版本
2. **Canonical 標籤**：在非主要版本頁面加入 `<link rel="canonical" href="主要URL">`
3. **修正所有內部連結**：含麵包屑、導覽列、Logo 連結、HTML Sitemap

### 4.3 cross-canonical 誤判規則

**重要**：cross-canonical 若差異只是尾斜線（/path vs /path/）= **誤報**，不能寫進報告。

必須先 curl/web_fetch 原始碼確認 canonical 真的指向不同網域才算。

---

## 5. 轉址式 404（Soft 404）

### 5.1 診斷

1. 頁面顯示「找不到商品/內容」
2. 但 HTTP 狀態碼回傳 200
3. Google Search Console 可能標記為「已檢索但未建立索引」

### 5.2 修正動作

- 商品永久下架 → 確實回傳 404 狀態碼
- 商品暫時下架但仍有 SEO 價值 → noindex，或 canonical 指向相關分類頁
- 商品已轉移 → 301 轉址到替代頁

### 5.3 商品下架完整處理流程

```
商品永久下架：
  → 確實回傳 404 狀態碼
  → 或 301 轉址到同類商品/分類頁

商品暫時下架（預計再上架）：
  → 保留頁面，設定 noindex
  → 有 SEO 價值的商品頁：考慮 301 到同分類頁

有 SEO 流量的商品頁下架：
  → 務必 301 轉址（不要直接 404）
  → 轉向同類商品頁或相關分類頁
```

---

## 6. Robots.txt 與 Sitemap

### 6.1 Robots.txt 標準格式

```
User-agent: *
Allow: /
Disallow: /cart
Disallow: /checkout
Disallow: /account
Disallow: /search?

Sitemap: https://example.com/sitemap.xml
```

**重點**：robots.txt 中**務必加入 Sitemap 語法**，提醒 Google 爬蟲定期抓取。

### 6.2 加速文章收錄

**方法一**：Google Search Console 手動提交
- 新文章上稿後立即 GSC 上方欄位輸入 URL → 點 Enter → 「要求建立索引」

**方法二**：Google Indexing API（更進階）
- 適合大量文章批次提交
- 在 GSC 設定擁有者權限給 awoo 服務帳號（`awoo-index@carbon-ruler-341608.iam.gserviceaccount.com`）

### 6.3 Sitemap 更新時機

- 該段時間有較多新頁面上線：每周更新
- 無新頁面：每 1-2 個月更新
- 大型網站可使用 Sitemap Index 分割

---

## 7. 文章新鮮度（Content Freshness）

### 7.1 Google 判斷日期的三種方式（重要性排序）

1. **結構化資料（datePublished, dateModified）** — 最直接
2. **頁面可見文字的日期** — 若只顯示發布日，後續更新不會自動更新
3. **URL 或其他時間資訊** — 建議網址不帶年份/日期

### 7.2 文章更新後的 Checklist

- [ ] 修改 Title 中的年份（如「2025 推薦」→「2026 推薦」）
- [ ] H1 同步更新年份
- [ ] 更新前台顯示的日期文字
- [ ] 更新結構化資料的 `dateModified`
- [ ] H 標籤內容小幅調整（順序對調、增減子段落）
- [ ] 補充最新資訊（新產品、新研究資料）
- [ ] 確認內部連結是否仍有效

### 7.3 文章更新禁忌

- ❌ 不要單純改日期不改內容
- ❌ 不要頻繁假更新（可能被視為操弄）

---

## 8. 內部連結策略

### 8.1 知識文章 → 商品/服務頁
- 文章末尾「相關商品/服務推薦」區塊
- 文章中段適當插入 CTA
- 文章末尾「延伸閱讀」連結

### 8.2 首頁新增文章區塊（中信i外匯案例）
- 在首頁新增「知識文章」區塊
- 設置 H2 標籤
- 輪播多篇文章縮圖 + 標題連結
- 目的：強化新文章的 PageRank 傳遞

### 8.3 麵包屑指向 canonical 版本（HOT 大聯盟）
```
型號頁麵包屑：首頁 > [廠牌名稱（連結至廠牌頁）] > 型號名稱
```

### 8.4 錨文字（Anchor Text）優化（京宇）
- 不要用「點此」「這裡」等通用文字
- 應使用包含目標關鍵字的描述性文字

### 8.5 相關文章推薦區塊優化（京宇）
- 不應使用全站隨機推薦
- 應根據文章主題推薦真正相關的內容

---

## 9. E-E-A-T 與外部連結

### 9.1 基本外連目標清單

1. **維基百科** — 外部連結區塊新增官網
2. **人力資源網站**（104、518 熊班） — 確認企業頁有官網連結
3. **App 平台**（Google Play、App Store） — 確認 App 頁有官網連結
4. **Google 商家** — 確認 Google Business Profile 完整
5. **edu / gov 網域** — 學術或政府單位連結
6. **品牌官方報導** — 媒體報導確保有超連結

### 9.2 外連品質基本標準

- 來源網域有足夠的 Domain Authority（DA）
- 連結為 dofollow（非 nofollow）
- 錨點文字包含品牌名稱或相關關鍵字
- 連結放置位置在內容主體中（非頁尾/側欄）

### 9.3 進階：連結誘餌（Link Bait）

詳見 `_shared/industry-patterns.md` §3.3 服務型的進階外連策略章節，含 6 種類型完整說明。

---

## 10. AIO / GEO 策略

### 10.1 「延展性關鍵字」判斷框架

**不值得重點佈局（會被 AIO 秒殺）**：
- 有明確唯一答案
- 純列表型查詢
- 答案簡單，使用者不需進站

**值得重點佈局（延展性）**：
- 涉及「選擇」「成本評估」的複雜問題
- 使用者需依自身情況判斷
- 多面向，一個 AIO 答案無法完整解決

### 10.2 AIO 關鍵字的兩種類型追蹤

| 類型 | 說明 | 對應策略 |
|------|------|---------|
| 已觸發 AIO 的關鍵字 | 品牌頁面已出現在 AI Overview | 深化內容、確保 dateModified 最新 |
| 有搜量但未觸發 AIO | 有自然搜尋排名，但不在 AIO | 分析 AIO 引用競品的內容缺口，補齊 |

---

## 11. 文章撰寫禁忌與技巧（awoo 標準）

### 技巧
- 標題含主關鍵字
- 每篇文章聚焦一個特定主題
- 段落分明，H2/H3 清楚劃分
- 善用條列式整理複雜資訊
- 適當加入內部連結
- 文末有明確 CTA

### 禁忌
- ❌ 重複撰寫相同主題的文章（自我競爭）
- ❌ 單純調換段落順序當「更新」
- ❌ 過度使用關鍵字
- ❌ 一篇文章多個不相關關鍵字

---

## 12. 競品分析與 SERP 觀察

### 12.1 SERP 類型分析框架（中信i外匯案例）

面對目標關鍵字，先分析：
- 搜尋結果大多是什麼類型頁面？（文章/服務頁/工具頁）
- AIO 是否已出現？引用的是哪些頁面？
- 使用者的搜尋意圖是什麼？

→ 決定應以哪種頁面類型作為著陸頁

### 12.2 著陸頁判斷（HOT 大聯盟）

- 用 GSC 查看「廠牌+二手車」關鍵字的著陸頁
- 若型號頁排名超過廠牌頁 → 廠牌頁 SEO 信號弱
- 解決：透過麵包屑、頁底區塊、H2 集中信號

### 12.3 文章投廣告策略（京宇）

- 選擇排名 21-50 名的文章
- 投放 Google Ads 帶流量
- 搭配 SEO 優化（H 標籤、內容補充）
- 觀察自然排名是否因流量訊號提升
