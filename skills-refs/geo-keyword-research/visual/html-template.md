# geo-keyword-research HTML 結構模板

> 關鍵字拓展報告的視覺結構。
> 沿襲 ada-geo-site-audit 的 visual-system，差異在 Hero 數字與三波策略區塊。

---

## 沿用元素

完全沿用 `_shared/visual-system.md` 與 `geo-site-audit/visual/html-template.md` 的：
- Sticky nav
- Intro 區塊
- Glossary 小辭彙
- Footer 兩段式

---

## Hero 三大數字（關鍵字版）

```html
<section id="hero">
  <div class="container">
    <div class="hero-label">KEYWORD RESEARCH · KEY NUMBERS</div>
    <div class="hero-numbers">
      <div class="hero-num-card num-purple">
        <span class="big-num">[N]</span>
        <div class="num-label">拓展候選關鍵字</div>
        <div class="num-sub">經三層驗證確認搜量</div>
      </div>
      <div class="hero-num-card num-orange">
        <span class="big-num">[N]</span>
        <div class="num-label">主題分類</div>
        <div class="num-sub">對應您網站既有內容 DNA</div>
      </div>
      <div class="hero-num-card num-red">
        <span class="big-num">[N]K</span>
        <div class="num-label">月總搜尋量</div>
        <div class="num-sub">三波策略預估流量空間</div>
      </div>
    </div>
  </div>
</section>
```

---

## 三波策略區塊（核心呈現）

```html
<section id="three-waves">
  <div class="container">
    <div class="section-tag">THREE WAVES STRATEGY</div>
    <h2 class="section-title">三波策略 · 從順風到攻堅</h2>
    <p class="section-desc">依您網站既有內容深度，將拓展字分配至三個操作階段。</p>
    
    <!-- 第一波 順風 -->
    <div class="kw-direction" style="border-left:4px solid var(--green);">
      <div class="kw-dir-header">
        <div class="kw-icon" style="background:rgba(39,174,96,0.15);">🌱</div>
        <div>
          <div class="kw-dir-title">第一波 · 順風波段</div>
          <div class="kw-dir-sub">已有內容基礎，調整即可有機會排名</div>
        </div>
      </div>
      
      <div class="kw-tracks">
        <div class="kw-track">
          <div class="kw-track-label precise">主關鍵字</div>
          <div class="kw-pills">
            <span class="kw-pill precise">關鍵字 (搜量)</span>
          </div>
        </div>
        <div class="kw-track">
          <div class="kw-track-label broad">延伸字</div>
          <div class="kw-pills">
            <span class="kw-pill broad">關鍵字 (搜量)</span>
          </div>
        </div>
      </div>
      
      <div class="kw-strategy-note">
        💡 動作：[具體 Title/H1/Schema 建議]
      </div>
    </div>
    
    <!-- 第二波 補強 -->
    <div class="kw-direction" style="border-left:4px solid var(--orange);">
      ...（同樣結構，配色橙）
    </div>
    
    <!-- 第三波 攻堅 -->
    <div class="kw-direction" style="border-left:4px solid #a78bfa;">
      ...（同樣結構，配色紫）
    </div>
  </div>
</section>
```

---

## 個別關鍵字明細表（每主題一張表）

```html
<section id="keyword-details">
  <div class="container">
    <h2 class="section-title">[主題名稱] · 拓字明細</h2>
    
    <div class="kw-table-wrap">
      <table class="kw-table">
        <thead>
          <tr>
            <th>關鍵字</th>
            <th>月搜量</th>
            <th>波段</th>
            <th>對應現有頁</th>
            <th>技術優化建議</th>
          </tr>
        </thead>
        <tbody>
          <tr>
            <td>葉黃素推薦</td>
            <td>8500</td>
            <td><span class="badge green">順風</span></td>
            <td><a href="...">/products/lutein</a></td>
            <td>Title 補「推薦」、加 Product Schema</td>
          </tr>
          ...
        </tbody>
      </table>
    </div>
  </div>
</section>
```

```css
.kw-table-wrap{overflow-x:auto;margin-bottom:32px;}
.kw-table{width:100%;border-collapse:collapse;font-size:15px;background:var(--white);border-radius:14px;overflow:hidden;box-shadow:0 1px 3px rgba(0,0,0,0.05);}
.kw-table th{background:var(--gray-light);padding:14px 16px;text-align:left;font-weight:700;color:var(--dark);}
.kw-table td{padding:14px 16px;border-bottom:1px solid var(--border);}
.kw-table tr:last-child td{border-bottom:none;}
.kw-table a{color:#1a6fc4;text-decoration:none;}
.kw-table a:hover{text-decoration:underline;}
.badge{display:inline-block;font-size:15px;padding:3px 10px;border-radius:100px;font-weight:700;}
.badge.green{background:rgba(39,174,96,0.15);color:#15803d;}
.badge.orange{background:rgba(230,126,34,0.15);color:#92400e;}
.badge.purple{background:rgba(167,139,250,0.15);color:#6d28d9;}
```

---

## CTA 區塊（拓字版）

```html
<section id="cta">
  <div class="container">
    <p class="cta-intro">關鍵字拓展只是開始——下一步可進入 Prompt 拓展，將選定關鍵字延伸成可上 GEO Suite 追蹤的 Prompt 候選池。</p>
    
    <div class="awoo-actions">
      <div class="action-item">
        <div class="action-num">1</div>
        <div>
          <div class="action-title">與您共同選定操作字</div>
          <div class="action-desc">從本報告候選池中，選定 [建議數量] 個字作為下階段操作目標</div>
        </div>
      </div>
      <div class="action-item">
        <div class="action-num">2</div>
        <div>
          <div class="action-title">進入 Prompt 拓展</div>
          <div class="action-desc">將選定字延伸成探索/決策/品牌型 Prompt，準備上 GEO Suite 追蹤</div>
        </div>
      </div>
      <div class="action-item">
        <div class="action-num">3</div>
        <div>
          <div class="action-title">執行優化動作</div>
          <div class="action-desc">依本報告各字的「技術優化建議」欄位，由 awoo 專員協助執行</div>
        </div>
      </div>
    </div>
    
    <div class="cta-contact">
      <h3>準備進入下一階段</h3>
      <p>讓 awoo 顧問團隊協助您將候選字轉為實際操作</p>
      <a href="https://www.awoo.ai/" class="cta-btn">與 AE 預約討論</a>
    </div>
  </div>
</section>
```

---

## 驗證清單

- [ ] 字體最小 15px
- [ ] awoo 全小寫
- [ ] Hero 三大數字（拓字總數 / 主題分類 / 月總搜量）
- [ ] 三波策略各有獨立 kw-direction 區塊
- [ ] 三波配色：綠 / 橙 / 紫
- [ ] 各主題明細表 kw-table
- [ ] 每個關鍵字有搜量、波段、對應頁、技術優化建議
- [ ] 對應頁 URL 已 web_fetch 驗證
- [ ] 技術優化建議欄位禁忌：不寫「建立文章」「擴充內容深度」
- [ ] CTA 區塊提示「下一步進入 Prompt 拓展」
- [ ] footer 兩段式格式
