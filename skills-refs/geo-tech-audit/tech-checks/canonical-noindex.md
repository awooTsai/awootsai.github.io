# Canonical / noindex 檢查

> 詳細 SEO 標準參考 `_shared/seo-best-practices.md` §4。

---

## 1. 檢查項目

### 1.1 Canonical 設定
- 每頁是否有 canonical 標籤？
- self-canonical（指向自己）的比例？
- cross-canonical（指向其他 URL）的數量？
- 真實的 cross-canonical（指向不同網域）？

### 1.2 Noindex 設定
- 哪些頁面被設為 noindex？
- noindex 頁面是否包含應該被收錄的內容？
- noindex 與 nofollow 的搭配？

### 1.3 robots.txt
- 是否阻擋了重要頁面？
- 是否含 Sitemap 語法？

---

## 2. cross-canonical 誤報識別

**鐵律**：cross-canonical 若差異只是尾斜線（/path vs /path/）= **誤報**。

### 驗證流程
1. 從 harvester 取得 cross-canonical URL pair
2. 對每個 pair 執行 curl
3. 比對兩個 URL 的原始 HTML 中的 canonical 標籤
4. 確認 canonical 是否真的指向不同網域

### 範例
```bash
# URL A
curl -s "https://example.com/page" | grep -i canonical
# 輸出：<link rel="canonical" href="https://example.com/page" />

# URL B
curl -s "https://example.com/page/" | grep -i canonical  
# 輸出：<link rel="canonical" href="https://example.com/page" />
```

兩者 canonical 都指向 `https://example.com/page`，這是**正確的 self-canonical**，不是 cross-canonical。

---

## 3. 真實的 cross-canonical 案例

```bash
# 頁面 A
curl -s "https://example.com/page-a" | grep canonical
# 輸出：<link rel="canonical" href="https://other-domain.com/different-page" />
```

頁面 A 把權重轉到外部網域 → 真實 cross-canonical → 需深入分析意圖。

可能的合理情境：
- 集團網站共享內容（指定主站為 canonical）
- 商品頁指向品牌官方頁

可能的問題情境：
- 配置錯誤
- 駭客置入

---

## 4. Noindex 涉及內容頁的問題

### 業務版可能提示
> 「您的網站疑似有 N 個頁面被設定為不可被搜尋引擎收錄」

### 專員版必做
- 列出全部 noindex 的 URL
- 標註每個 URL 的內容類型
- 判斷是否合理 noindex

### 合理 noindex 的情境
- 結帳頁、購物車（通常）
- 會員頁、登入頁
- 站內搜尋結果頁
- 廢棄測試商品

### 不合理 noindex 的情境
- FAQ 頁面（Simmpo 案例）
- 商品頁（特別是有 SEO 流量的）
- 知識文章

---

## 5. robots.txt 標準檢查

### 應檢查項目
```
# 是否有 Sitemap 宣告
Sitemap: https://example.com/sitemap.xml

# 是否阻擋了重要目錄
Disallow: /products/  ← 這會阻擋商品頁，通常是錯的

# 是否阻擋了 AI 爬蟲
User-agent: GPTBot
Disallow: /  ← 這會阻擋 ChatGPT 爬取
```

### 平台合作客戶
- SHOPLINE 自動產生 robots.txt，通常合理
- 不要把平台預設寫成「客戶問題」

---

## 6. 報告格式建議

```html
<section class="check-section">
  <h3>Canonical / noindex 檢查</h3>
  
  <table class="check-table">
    <thead>
      <tr>
        <th>檢查項目</th>
        <th>狀態</th>
        <th>細節</th>
        <th>原始資料</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td>self-canonical 比例</td>
        <td>🔵 95%</td>
        <td>235 / 247 頁</td>
        <td>_rag_summary.json</td>
      </tr>
      <tr>
        <td>cross-canonical（真實）</td>
        <td>🔵 0 個</td>
        <td>原 harvester 標記為誤報</td>
        <td>curl 驗證</td>
      </tr>
      <tr>
        <td>noindex 頁面</td>
        <td>🟡 23 個</td>
        <td>含 8 個疑似內容頁，需檢視</td>
        <td>展開列表 ↓</td>
      </tr>
    </tbody>
  </table>
  
  <details>
    <summary>noindex 頁面清單（23 個）</summary>
    <ol>
      <li>example.com/cart（合理）</li>
      <li>example.com/account（合理）</li>
      <li>example.com/old-products/55-series（廢棄商品，合理）</li>
      <li>example.com/faq（⚠️ 不合理！需確認）</li>
      ...
    </ol>
  </details>
</section>
```
