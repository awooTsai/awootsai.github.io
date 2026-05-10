# H 標籤結構檢查

> 詳細 SEO 標準參考 `_shared/seo-best-practices.md` §1, §2。

---

## 1. 檢查項目

### 1.1 H1 完整率
- 每頁是否有且僅有一個 H1？
- 缺 H1 的頁面數量？
- 多重 H1（>1 個）的頁面數量？

### 1.2 H1 內容品質
- H1 是否含目標關鍵字？
- H1 是否與 Title 過度重複？
- H1 是否為 og-fallback（從 og:title 補位）？

### 1.3 H2-H6 層級
- 是否跳級使用（如 H1 後直接 H4）？
- 各層級的數量分佈？

### 1.4 隱藏 H 標籤
- `uk-hidden`、`sr-only`、`display:none` 等 class 包覆的 H 標籤？
- 隱藏 H1 與顯示 H1 共存的雙 H1 問題？

---

## 2. 從 harvester 資料萃取

### 從 _rag_summary.json
```json
{
  "h1_stats": {
    "total_pages": 247,
    "with_h1": 215,
    "without_h1": 23,
    "multiple_h1": 9,
    "og_fallback_h1": 32
  },
  "missing_samples": ["url1", "url2", ...]
}
```

### 從 _rag_chunks.jsonl
每個頁面的 chunks 含 `h1`、`h2`、`h3` 等欄位，可分析層級分佈。

---

## 3. 報告中呈現方式

### 統計表格
```
| 指標 | 數量 | 比例 | 評估 |
|------|------|------|------|
| 含 H1 頁面 | 215 | 87% | 🔵 |
| 缺 H1 頁面 | 23 | 9% | 🟡 需處理 |
| 多重 H1 | 9 | 4% | 🟡 需處理 |
| og-fallback H1 | 32 | 13% | 🟡 需檢視 |
```

### 全部 URL 展開
```html
<details>
  <summary>缺 H1 的 23 個頁面</summary>
  <ol>
    <li>https://example.com/page-1</li>
    <li>https://example.com/page-2</li>
    ...（全部列出）
  </ol>
</details>

<details>
  <summary>多重 H1 的 9 個頁面</summary>
  ...
</details>

<details>
  <summary>og-fallback H1 的 32 個頁面</summary>
  ...
</details>
```

---

## 4. HOT 大聯盟案例補充：雙 H1

### 情境
頁面同時有：
- 系統共用 H1：「車輛搜尋」（`uk-hidden`）
- 客製 H1：「HONDA本田」（顯示）

### 判斷
雙 H1 即使一個隱藏，仍會被搜尋引擎視為兩個 H1。

### 修正建議
- 系統共用 H1 改為 `<span>` 或 `<p>`
- 保留唯一的頁面專屬 H1
- 確認 H1 內無 `<a>` 連結

```html
<!-- 錯誤 -->
<h1><a class="link_org" href="/...">HONDA本田</a></h1>

<!-- 正確 -->
<h1 class="uk-hidden">HONDA本田認證二手車</h1>
```

---

## 5. 服務型品牌的 H 標籤潤飾

詳見 `_shared/seo-best-practices.md` §2.3，含京宇法律案例的潤飾範例。

關鍵：H 標籤應「自然包含關鍵字」並具備吸引點擊的口吻。

---

## 6. 圖片 H 標籤的處理

如業務版健檢提到「H1 為圖片」，專員應：
1. 用瀏覽器 DevTools 確認該頁的 H1 元素
2. 若為 `<img>` 包裝，記錄該頁面 URL
3. 建議改為 `<text>` + CSS 排版

範例修正：
```html
<!-- 錯誤 -->
<h1><img src="title.png" alt="頁面標題"></h1>

<!-- 正確 -->
<h1 class="hero-title">頁面標題</h1>
<style>
  .hero-title { /* 視覺效果 CSS */ }
</style>
```

---

## 7. 報告中與業務版的對照

如業務版說：
> 「您的網站疑似 23 頁缺 H1」

專員版應對照：
- 從 _rag_summary.json 確認實際數字
- 列出全部 23 個 URL（不只 3 個範例）
- 抽樣 5 個用 web_fetch 確認 H1 確實缺失（避免誤報）
- 標記矛盾點（如有）
