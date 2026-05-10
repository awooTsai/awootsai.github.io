# URL 一致性檢查

> 檢查網站 URL 結構的一致性問題。
> 詳細 SEO 標準參考 `_shared/seo-best-practices.md` §4。

---

## 1. 檢查項目

### 1.1 帶 / vs 不帶 /
- `https://example.com/category` vs `https://example.com/category/`
- 兩個 URL 都可訪問且未 301 → 重複內容問題

### 1.2 www vs non-www
- `https://example.com/` vs `https://www.example.com/`
- 兩個都可訪問且未 301 → 信任訊號分散

### 1.3 query parameter 變體
- `?utm_source=...` 等追蹤參數
- 是否有 canonical 指向乾淨 URL？

### 1.4 大小寫
- `/Page` vs `/page`
- 通常伺服器配置決定，但需檢查

### 1.5 trailing index
- `https://example.com/Home/Index` vs `https://example.com/`
- 是否 301？

---

## 2. 驗證方法

### 自動化檢查腳本
```python
import requests

def check_url_consistency(base_url):
    variants = [
        base_url,
        base_url + '/',
        base_url.replace('https://', 'https://www.'),
        base_url.replace('https://www.', 'https://'),
    ]
    
    results = []
    for url in variants:
        try:
            r = requests.head(url, allow_redirects=False, timeout=5)
            results.append({
                'url': url,
                'status': r.status_code,
                'redirects_to': r.headers.get('Location', 'N/A')
            })
        except Exception as e:
            results.append({'url': url, 'error': str(e)})
    
    return results
```

### 報告呈現

| URL 變體 | 狀態碼 | 轉址至 | 評估 |
|---------|-------|-------|------|
| https://example.com | 200 | - | ✅ 主版本 |
| https://example.com/ | 301 | https://example.com | ✅ 正確轉址 |
| https://www.example.com | 301 | https://example.com | ✅ 正確轉址 |
| https://example.com/Home/Index | 200 | - | ⚠️ 應 301 至首頁 |

---

## 3. cross-canonical 誤報識別（重要）

**重要規則**：cross-canonical 若差異只是尾斜線（/path vs /path/）= 誤報，不可寫進報告。

### 驗證流程
1. curl 取得兩個 URL 的原始 HTML
2. 比對 canonical 標籤實際指向
3. 只有當 canonical 真的指向不同網域才算 cross-canonical

### 真實 cross-canonical 案例
```
頁面 A: https://example.com/page-a
  → canonical 指向 https://other-domain.com/page-x

頁面 B: https://example.com/page-b
  → canonical 指向 https://other-domain.com/page-x
```

兩個頁面都把權重移轉到外部網域 → 真實 cross-canonical。

---

## 4. 解決方案優先順序

### 優先順序 1：301 轉址
最強訊號，建議所有 URL 變體都 301 至主版本。

### 優先順序 2：Canonical 標籤
若無法 301（如系統限制），加 canonical 至非主版本頁面。

### 優先順序 3：修正所有內部連結
- 麵包屑
- 導覽列
- Logo 連結
- HTML Sitemap
- XML Sitemap

所有內部連結指向 canonical 版本。

---

## 5. HOT 大聯盟案例補充

### 情境
多個 URL 變體：
- `https://hotcar.com/CarFilter?vBrand=43`
- `https://hotcar.com/CarFilter?vBrandWord=T&vBrand=43`

### 判斷
應以 `vBrandWord=T&vBrand=43` 為主版本（資訊較完整）。

### 動作
- 所有內部連結指向主版本
- 麵包屑、HTML Sitemap 同步修正

---

## 6. 報告格式建議

```html
<section class="check-section">
  <h3>URL 一致性檢查</h3>
  
  <table class="check-table">
    <thead>
      <tr><th>檢查項目</th><th>狀態</th><th>細節</th></tr>
    </thead>
    <tbody>
      <tr>
        <td>主域名一致性</td>
        <td>🔵 正常</td>
        <td>www / non-www 已 301 至主版本</td>
      </tr>
      <tr>
        <td>尾斜線處理</td>
        <td>🟡 需驗證</td>
        <td>抽樣 5 頁，3 頁有 301，2 頁兩版本都 200</td>
      </tr>
      <tr>
        <td>cross-canonical</td>
        <td>🔵 無問題</td>
        <td>原 harvester 標記為誤報（尾斜線差異）</td>
      </tr>
    </tbody>
  </table>
</section>
```
