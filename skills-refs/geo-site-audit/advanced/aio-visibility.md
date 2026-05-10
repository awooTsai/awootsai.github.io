# AIO 能見度進階分析

> 當客戶提供 Ahrefs AIO CSV 時觸發。
> 用法：將 AIO 觸發關鍵字資料整合進業務提案版健檢報告。

---

## 1. Ahrefs AIO CSV 標準欄位

Ahrefs 匯出的 AIO 能見度檔案常見欄位：
- `Keyword`：搜尋關鍵字
- `URL`：客戶網站 URL（被 AI 引用的頁面）
- `AI Overview`：是否觸發 AIO（True / False）
- `Search Volume`：月搜尋量
- `Position`：自然排名

---

## 2. 兩種 AIO 關鍵字分類

| 類型 | 條件 | 對應 awoo 策略 |
|------|------|--------------|
| **已觸發 AIO** | `AI Overview = True` 且客戶 URL 出現 | 深化內容、確保 dateModified 最新 |
| **有搜量但未觸發 AIO** | 自然有排名（Position ≤ 50）但 `AI Overview = False`/未引用 | 分析 AIO 引用競品的內容缺口，補齊 |

---

## 3. 報告中呈現方式

### 3.1 AIO Visibility 區塊（在 specific-issues 之後新增）

```html
<section id="aio-visibility" style="background:#1a1a24;color:#fff;">
  <div class="container">
    <div class="section-tag" style="background:rgba(255,255,255,0.08);color:rgba(255,255,255,0.7);">AIO VISIBILITY</div>
    <h2 class="section-title" style="color:#fff;">AI 引用現況</h2>
    
    <!-- 兩個並列的 group -->
    <div class="aio-groups">
      <div class="aio-group">
        <div class="aio-label">已觸發 AIO 的關鍵字</div>
        <div class="aio-count">[X] 字</div>
        <div class="aio-pills">
          <span class="aio-pill triggered">關鍵字 1</span>
          <span class="aio-pill triggered">關鍵字 2</span>
          ...
        </div>
      </div>
      
      <div class="aio-group">
        <div class="aio-label">有搜量但未觸發 AIO</div>
        <div class="aio-count">[Y] 字</div>
        <div class="aio-pills">
          <span class="aio-pill missed">關鍵字 A</span>
          <span class="aio-pill missed">關鍵字 B</span>
          ...
        </div>
      </div>
    </div>
    
    <div class="aio-insight">
      💡 觀察重點：[基於資料的觀察說明]
    </div>
  </div>
</section>
```

### 3.2 pill 隱藏月搜尋量

⚠️ 鐵律：AIO pills 不顯示月搜尋量數字（避免客戶覺得「我自己看 Ahrefs 就好」）。

只顯示關鍵字本身。

---

## 4. AIO 觀察的標準措辭

### 4.1 已觸發 AIO 多、品牌引用率高
> 「您的網站在 [N] 個關鍵字上已被 AI Overview 引用，這代表 AI 已認可您網站內容的權威性。下一步建議：深化既有內容的時效性與深度。」

### 4.2 已觸發 AIO 多但品牌引用率低
> 「[N] 個關鍵字已觸發 AIO，但 AI 引用的疑似為競品內容。建議分析 AIO 競品引用的具體段落，從內容深度與結構化資料切入。」

### 4.3 知識型 vs 品牌推薦型的落差
> 「您的知識型 AIO 表現良好（[N] 字觸發），但品牌推薦型問句（如『XX 推薦』）幾乎空白。消費者看完知識後問 AI 推薦品牌時，AI 尚未建立對應的語意識別框架——這是知識→品牌橋接的機會。」

---

## 5. AIO 範例頁面引用規則

當引用 AIO 中被 AI 引用的客戶頁面時：
- 必先 web_fetch 該 URL，確認 200 OK
- 確認頁面內容與 AIO 引用情境一致
- 在 verified-pages 區塊呈現

---

## 6. 「awoo 顧問推估」標註

AI 引用測試區若無實際 API 呼叫驗證（僅 awoo 推估），必須標註：

```html
<div class="citation-verdict">
  <strong style="color:#fbbf24;">awoo 顧問推估</strong>
  <p>以下為依據品牌可見度與競品比較的推估評估，非即時實測</p>
</div>
```

避免客戶誤以為是即時 API 結果。

---

## 7. 與 ada-geo-keyword-research 的銜接

業務版健檢的 AIO 區塊發現的「未觸發 AIO 的關鍵字」，可以直接帶入 `ada-geo-keyword-research` Skill 進行下一輪拓展，形成完整流程：

```
業務版健檢（找出 AIO 缺口）
  ↓
關鍵字拓展（系統化分析該補哪些字）
  ↓
Prompt 拓展（上 GEO Suite 追蹤）
```

報告結尾應提示這個下一步路徑。
