# Schema / JSON-LD 結構化資料檢查

> 詳細 SEO 標準參考 `_shared/seo-best-practices.md` §3。

---

## 1. 檢查項目

### 1.1 Schema 類型覆蓋
- BreadcrumbList
- Article
- FAQPage（最重要，AIO 引用核心）
- Product
- Organization（首頁必備）
- ProfilePage（律師/醫師等個人專業頁）
- WebSite / WebPage（基本）
- LocalBusiness（實體店面）

### 1.2 各類 Schema 的覆蓋率
從 `_rag_summary.json` 取得各 Schema 類型的數量與佔總頁數比例。

### 1.3 Schema 完整度
不只是「有沒有」，還要看「欄位是否完整」：
- Product Schema：是否含 price、availability、aggregateRating？
- Article Schema：是否含 datePublished、dateModified、author？
- FAQPage：問答是否完整（不只 1-2 題）？

---

## 2. 從 harvester 資料萃取

### _rag_summary.json 範例
```json
{
  "schema_stats": {
    "BreadcrumbList": 240,
    "Article": 67,
    "FAQPage": 0,
    "Product": 80,
    "Organization": 1
  },
  "schema_coverage": 0.85
}
```

### 從 _rag_chunks.jsonl 抽樣
取 5-10 個頁面的 Schema 原始 JSON，檢查完整度。

---

## 3. 報告中呈現方式

### 各 Schema 類型分佈表

```
| Schema 類型 | 數量 | 覆蓋率 | 完整度 | 評估 |
|------------|------|-------|--------|------|
| BreadcrumbList | 240 | 97% | 完整 | 🔵 良好 |
| Article | 67 | - | 缺 dateModified | 🟡 需補 |
| FAQPage | 0 | 0% | - | 🟠 完全缺位 |
| Product | 80 | 90% | 缺 aggregateRating | 🟡 需補 |
| Organization | 1 | - | 完整 | 🔵 良好 |
| ProfilePage | 0 | 0% | - | 🟠 缺位（如為服務型） |
```

### Schema 範例展開

對每個有問題的 Schema，提供標準範本（從 `_shared/seo-best-practices.md` §3 取得）。

```html
<details>
  <summary>建議補上的 FAQPage Schema 範例</summary>
  <pre><code>
&lt;script type="application/ld+json"&gt;
{
  "@context": "https://schema.org",
  "@type": "FAQPage",
  "mainEntity": [
    {
      "@type": "Question",
      "name": "Q1",
      "acceptedAnswer": {
        "@type": "Answer",
        "text": "A1"
      }
    }
  ]
}
&lt;/script&gt;
  </code></pre>
</details>
```

---

## 4. 平台合作客戶的 Schema 處理

### SHOPLINE / Shopify / 91APP / Cyberbiz
- BreadcrumbList、Product Schema 通常自動產生
- FAQPage 需手動建置（平台不自動）
- Organization Schema 需在首頁手動加

### Wix
- 部分 Schema 限制較多
- 需透過第三方插件補建

詳見 `_shared/platform-partners.md`。

---

## 5. Organization Schema 是核心

### 重要性
2023/11/29 起 Google 擴大 Organization Schema 支援範圍，對品牌知識面板呈現極為關鍵。

### 必備欄位
- `name`：品牌中文名稱
- `url`：官網主版本
- `logo`：完整 URL
- `description`：簡潔品牌介紹
- `address`：完整地址（PostalAddress）
- `contactPoint`：電話、Email

### 必須放在首頁 `<head></head>`

---

## 6. 服務型品牌 ProfilePage 是核心

### 重要性
律師、醫師、會計師等個人專業頁的 ProfilePage Schema 配合 sameAs 連結，強化 E-E-A-T。

### 必備欄位
- `mainEntity.@type`: Person
- `name`、`jobTitle`、`url`、`image`
- `worksFor`：所屬機構
- `alumniOf`：學歷
- `sameAs`：論文、社群、媒體連結

詳見 `_shared/seo-best-practices.md` §3.6。

---

## 7. 報告中與業務版的對照

如業務版說：
> 「您的 Schema 覆蓋率 85%，建議補上 FAQ Schema」

專員版應：
- 確認實際覆蓋率（從原始資料計算）
- 列出全部 Schema 類型分佈
- 提供 FAQ Schema 範本（讓專員直接套用）
- 標記矛盾點（如業務版說的覆蓋率與實際不符）
