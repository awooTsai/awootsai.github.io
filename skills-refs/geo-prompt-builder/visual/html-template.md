# geo-prompt-builder HTML 結構模板

> Prompt 拓展報告的視覺結構。
> 沿襲 ada-geo-site-audit + ada-geo-keyword-research，差異在 Hero 數字與 Prompt 卡片區塊。

---

## 沿用元素

完全沿用 `_shared/visual-system.md` 的：
- Sticky nav
- Intro 區塊
- Glossary 小辭彙
- Footer 兩段式

---

## Hero 三大數字（Prompt 版）

```html
<section id="hero">
  <div class="container">
    <div class="hero-label">PROMPT POOL · KEY NUMBERS</div>
    <div class="hero-numbers">
      <div class="hero-num-card num-purple">
        <span class="big-num">[N]</span>
        <div class="num-label">Prompt 候選池</div>
        <div class="num-sub">最終將篩選為 [M] 條上線追蹤</div>
      </div>
      <div class="hero-num-card num-orange">
        <span class="big-num">[N]</span>
        <div class="num-label">關鍵字主題</div>
        <div class="num-sub">每組關鍵字 4-7 條 Prompt</div>
      </div>
      <div class="hero-num-card num-red">
        <span class="big-num">[N]</span>
        <div class="num-label">需補內容的 Prompt</div>
        <div class="num-sub">代表內容缺口與優化機會</div>
      </div>
    </div>
  </div>
</section>
```

---

## 三意圖比例展示

```html
<section id="intent-balance">
  <div class="container">
    <div class="section-tag">CUSTOMER JOURNEY</div>
    <h2 class="section-title">三意圖比例</h2>
    <p class="section-desc">候選池依 Customer Journey 分為三種意圖，覆蓋使用者從探索到決策的完整路徑。</p>
    
    <div class="intent-bars">
      <div class="intent-bar">
        <div class="intent-label">
          <span class="intent-icon" style="background:#6366f1;">🔍</span>
          <span>探索型</span>
          <span class="intent-pct">[X]%</span>
        </div>
        <div class="intent-track">
          <div class="intent-fill" style="width:[X]%;background:#6366f1;"></div>
        </div>
        <div class="intent-desc">使用者正在了解該主題，AI 引擎透過此類 Prompt 建立基礎認知</div>
      </div>
      
      <div class="intent-bar">
        <div class="intent-label">
          <span class="intent-icon" style="background:#f59e0b;">⚖️</span>
          <span>決策型</span>
          <span class="intent-pct">[X]%</span>
        </div>
        <div class="intent-track">
          <div class="intent-fill" style="width:[X]%;background:#f59e0b;"></div>
        </div>
        <div class="intent-desc">使用者正在比較選擇，AI 推薦時直接連動到您的品牌</div>
      </div>
      
      <div class="intent-bar">
        <div class="intent-label">
          <span class="intent-icon" style="background:#dc2626;">🎯</span>
          <span>品牌型</span>
          <span class="intent-pct">[X]%</span>
        </div>
        <div class="intent-track">
          <div class="intent-fill" style="width:[X]%;background:#dc2626;"></div>
        </div>
        <div class="intent-desc">使用者已知您品牌，AI 回答時是您強化品牌印象的機會</div>
      </div>
    </div>
  </div>
</section>
```

```css
.intent-bars{display:flex;flex-direction:column;gap:24px;}
.intent-bar{background:var(--white);border:1px solid var(--border);border-radius:14px;padding:20px 24px;}
.intent-label{display:flex;align-items:center;gap:12px;margin-bottom:10px;}
.intent-icon{width:36px;height:36px;border-radius:50%;display:flex;align-items:center;justify-content:center;color:#fff;font-size:18px;}
.intent-pct{margin-left:auto;font-family:var(--font-num);font-size:24px;color:var(--dark);}
.intent-track{height:8px;background:var(--gray-light);border-radius:100px;overflow:hidden;margin-bottom:10px;}
.intent-fill{height:100%;border-radius:100px;}
.intent-desc{font-size:15px;color:var(--mid);line-height:1.7;}
```

---

## 主要區塊：Prompt 候選池（依關鍵字分組）

```html
<section id="prompt-pool">
  <div class="container">
    <div class="section-tag">CANDIDATE POOL</div>
    <h2 class="section-title">候選 Prompt 清單</h2>
    <p class="section-desc">點擊任一 Prompt 旁的「複製」按鈕，可複製到剪貼簿。</p>
    
    <!-- 每組關鍵字一個卡片 -->
    <div class="kw-prompt-group">
      <div class="kw-prompt-header">
        <h3>葉黃素</h3>
        <span class="kw-stats">月搜量 8500 · 6 條 Prompt</span>
      </div>
      
      <!-- 探索型 -->
      <div class="prompt-cluster">
        <div class="cluster-label" style="background:#6366f1;">🔍 探索型 · 2 條</div>
        <div class="prompt-item">
          <div class="prompt-text">葉黃素是什麼？對眼睛有什麼幫助？</div>
          <div class="prompt-meta">
            <span class="coverage good">✅ 已有承接</span>
            <button class="copy-btn" data-q="葉黃素是什麼？對眼睛有什麼幫助？" onclick="awooCopy(this)">複製</button>
          </div>
        </div>
        <div class="prompt-item">
          <div class="prompt-text">葉黃素有哪些種類？游離型和酯化型差在哪？</div>
          <div class="prompt-meta">
            <span class="coverage partial">⚠️ 部分承接</span>
            <button class="copy-btn" data-q="..." onclick="awooCopy(this)">複製</button>
          </div>
        </div>
      </div>
      
      <!-- 決策型 -->
      <div class="prompt-cluster">
        <div class="cluster-label" style="background:#f59e0b;">⚖️ 決策型 · 3 條</div>
        ...
      </div>
      
      <!-- 品牌型 -->
      <div class="prompt-cluster">
        <div class="cluster-label" style="background:#dc2626;">🎯 品牌型 · 1 條</div>
        ...
      </div>
    </div>
    
    <!-- 下一組關鍵字 -->
    <div class="kw-prompt-group">...</div>
  </div>
</section>
```

```css
.kw-prompt-group{background:var(--white);border:1px solid var(--border);border-radius:16px;padding:24px;margin-bottom:20px;}
.kw-prompt-header{display:flex;align-items:baseline;justify-content:space-between;margin-bottom:18px;padding-bottom:14px;border-bottom:1px solid var(--border);}
.kw-prompt-header h3{font-size:22px;font-weight:900;color:var(--dark);}
.kw-stats{font-size:15px;color:var(--mid);}
.prompt-cluster{margin-bottom:16px;}
.cluster-label{display:inline-block;font-size:15px;font-weight:700;color:#fff;padding:5px 14px;border-radius:100px;margin-bottom:10px;}
.prompt-item{background:var(--gray-light);border-radius:10px;padding:14px 16px;margin-bottom:8px;display:flex;justify-content:space-between;align-items:center;gap:12px;}
.prompt-text{flex:1;font-size:15px;color:var(--gray-700);line-height:1.7;}
.prompt-meta{display:flex;gap:10px;align-items:center;flex-shrink:0;}
.coverage{font-size:15px;font-weight:700;padding:3px 10px;border-radius:100px;}
.coverage.good{background:rgba(39,174,96,0.15);color:#15803d;}
.coverage.partial{background:rgba(243,156,18,0.15);color:#92400e;}
.coverage.none{background:rgba(200,10,20,0.1);color:var(--red);}
.copy-btn{background:var(--white);border:1px solid var(--border);color:var(--gray-700);font-size:15px;padding:5px 12px;border-radius:8px;cursor:pointer;font-family:var(--font-main);}
.copy-btn:hover{background:var(--red);color:#fff;border-color:var(--red);}

@media(max-width:640px){
  .prompt-item{flex-direction:column;align-items:flex-start;}
  .prompt-meta{margin-top:8px;}
}
```

---

## CTA 區塊（Prompt 拓展版）

```html
<section id="cta">
  <div class="container">
    <p class="cta-intro">候選池已產出，下一步請從中挑選最終要上線追蹤的 Prompt。awoo 顧問可協助您依「業務優先」或「內容承接」邏輯篩選。</p>
    
    <div class="awoo-actions">
      <div class="action-item">
        <div class="action-num">1</div>
        <div>
          <div class="action-title">與您共同篩選</div>
          <div class="action-desc">從 [N] 條候選池中選定 [M] 條最終上線追蹤的 Prompt</div>
        </div>
      </div>
      <div class="action-item">
        <div class="action-num">2</div>
        <div>
          <div class="action-title">補強內容缺口</div>
          <div class="action-desc">針對 ⚠️/❌ 標記的 Prompt，由 awoo 內容團隊規劃補強</div>
        </div>
      </div>
      <div class="action-item">
        <div class="action-num">3</div>
        <div>
          <div class="action-title">上線 GEO Suite</div>
          <div class="action-desc">每週追蹤 ChatGPT、Gemini、Perplexity 中您品牌的能見度與引用率</div>
        </div>
      </div>
    </div>
    
    <div class="cta-contact">
      <h3>準備上線 GEO Suite</h3>
      <p>讓 awoo 顧問團隊協助您將候選 Prompt 上線追蹤</p>
      <a href="https://www.awoo.ai/" class="cta-btn">與 AE 預約討論</a>
    </div>
  </div>
</section>
```

---

## 「複製」按鈕的 JavaScript

```javascript
function awooCopy(btn){
  var q=btn.dataset.q||'';
  if(navigator.clipboard&&navigator.clipboard.writeText){
    navigator.clipboard.writeText(q).then(function(){
      _showToast('✓ Prompt 已複製');
    }).catch(function(){_fallback(q);});
  }else{_fallback(q);}
}
function _fallback(text){
  var ta=document.createElement('textarea');
  ta.value=text;ta.style.cssText='position:fixed;opacity:0;top:0;';
  document.body.appendChild(ta);ta.focus();ta.select();
  try{document.execCommand('copy');_showToast('✓ Prompt 已複製');}
  catch(e){_showToast('請手動長按複製');}
  document.body.removeChild(ta);
}
function _showToast(text){
  var t=document.createElement('div');t.className='gem-toast';t.textContent=text;
  document.body.appendChild(t);
  requestAnimationFrame(function(){t.classList.add('show');});
  setTimeout(function(){t.classList.remove('show');setTimeout(function(){t.remove();},300);},2500);
}
```

---

## 驗證清單

- [ ] 字體最小 15px
- [ ] awoo 全小寫
- [ ] Hero 三大數字（候選池總數 / 關鍵字主題 / 需補內容數）
- [ ] 三意圖比例條圖
- [ ] 每組關鍵字至少 4 條 Prompt
- [ ] 每組關鍵字至少 1 條品牌型
- [ ] 每條 Prompt 有承接狀態（✅/⚠️/❌）
- [ ] 每條 Prompt 有「複製」按鈕（含 fallback）
- [ ] 三意圖配色：藍紫 / 琥珀 / 紅
- [ ] CTA 區塊提示「下一步進入 GEO Suite」
- [ ] footer 兩段式格式
