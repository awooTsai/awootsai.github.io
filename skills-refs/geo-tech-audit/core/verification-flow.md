# 業務版幻覺驗證流程

> 業務版健檢報告若有 AI 幻覺，由本 Skill 標記出來。

---

## 1. 常見的業務版幻覺類型

### 類型 1：URL 抄錯
業務版列了 example.com/page-X 作為缺 H1 範例，但該 URL 實際 404。

**驗證方式**：
- 對業務版每個 verified-pages URL 執行 web_fetch
- 任何 ≠ 200 的 URL 標記為「業務版 URL 失效」

### 類型 2：cross-canonical 誤報
業務版說「您網站有 cross-canonical 問題」，但實際只是尾斜線差異（誤報）。

**驗證方式**：
- 對業務版提到的 cross-canonical 案例，curl 取得原始 HTML
- 比對兩個 URL 的 canonical 是否真的指向不同網域
- 只是尾斜線差異 → 標記「誤報」

### 類型 3：平台特性誤判為問題
業務版說「您網站的 sitemap 設置不當」，但客戶是 SHOPLINE，sitemap 是平台自動產生的。

**驗證方式**：
- 確認客戶平台類型
- 對照 `_shared/platform-partners.md`
- 平台自動產生的內容不應寫成「問題」

### 類型 4：數字推估錯誤
業務版說「您的 Schema 覆蓋率 60%」，但專員版核對發現實際是 75%。

**驗證方式**：
- 重新從 _rag_summary.json 取得原始數字
- 標記任何不一致

### 類型 5：產業判斷錯誤
業務版說「您的網站是電商」，但實際是服務型（如線上預約系統）。

**驗證方式**：
- 重新分析客戶內容主題
- 標記產業判斷的可能錯誤

---

## 2. 驗證工作流

### Step 1：載入業務版報告
如使用者提供業務版 HTML 報告，read_file 載入。

### Step 2：萃取業務版的「觀察陳述」
- 三大痛點
- 各個 verified-pages
- AIO 區塊
- 提到的數字、URL、Schema 類型

### Step 3：對每個觀察執行驗證

| 觀察類型 | 驗證方式 |
|---------|---------|
| URL 引用 | web_fetch 確認 200 |
| 數字（覆蓋率、頁數） | 重新從 _rag_summary.json 計算 |
| Schema 類型 | 從 _rag_chunks.jsonl 抽樣確認 |
| cross-canonical | curl 取得原始 HTML |
| 平台識別 | 多重證據比對 |
| 業態判斷 | 內容主題重新分析 |

### Step 4：產出驗證結果

```html
<section id="verification-results">
  <h2>業務版報告對照驗證</h2>
  
  <table>
    <thead>
      <tr>
        <th>業務版觀察</th>
        <th>驗證結果</th>
        <th>原始資料</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td>「您的 Schema 覆蓋率 60%」</td>
        <td>⚠️ 驗證後實際為 75%</td>
        <td>_rag_summary.json line 42</td>
      </tr>
      <tr>
        <td>「網站有 cross-canonical 問題」</td>
        <td>❌ 誤報（僅尾斜線差異）</td>
        <td>curl example.com/page vs /page/</td>
      </tr>
      ...
    </tbody>
  </table>
</section>
```

---

## 3. 驗證結果的處理原則

### 對阿達回報
- 列出所有發現的矛盾點
- 提供原始資料佐證
- 建議業務版報告應修正的內容

### 不直接改業務版
- 阿達 / AE 才能決定是否要修改業務版報告
- 本 Skill 只負責標記矛盾，不擅自改動

### 累積回饋給 harvester 改進
- 若發現某類型錯誤反覆出現，記錄下來
- 每月整理一次給開發團隊
- 改進 harvester 的判斷邏輯

---

## 4. 與業務版的協作流程

```
1. AE 跑業務版健檢（ada-geo-site-audit）
   ↓
2. 業務版 HTML 產出
   ↓
3. 客戶買單後，內部專員拿業務版 + 原始資料
   ↓
4. 專員跑 ada-geo-tech-audit（本 Skill）
   ↓
5. 專員版報告：對照業務版 + 展開所有原始資料
   ↓
6. 矛盾點回報給阿達 / AE
   ↓
7. 開始實際 SEO 執行
```

每個客戶都會經過這個雙層驗證，確保業務版品質與內部執行一致。

---

## 5. 不要過度挑剔

雖然本 Skill 是驗證業務版，但要記住：
- 業務版的口吻就是「不卑不亢、客觀觀察」
- 業務版不需要列全所有 URL（那是專員版的事）
- 業務版的「謹慎口吻」（如「疑似」「建議確認」）不是錯誤，是設計

只有真正的「事實錯誤」才算矛盾點：
- ❌ 不算錯：「業務版用『疑似』，但實際是確定」（這是業務版的口吻設計）
- ✅ 算錯：「業務版列了 example.com/page-1 但該 URL 404」（事實錯誤）
