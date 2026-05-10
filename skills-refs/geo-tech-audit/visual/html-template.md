# geo-tech-audit HTML 結構模板

> 專員體質健檢報告的視覺結構。
> 沿用 `_shared/visual-system.md`，但針對「專員快速檢視」做調整：
> - 表格化呈現多
> - 資訊密度高
> - 標記🔵 事實 vs 🟡 推論
> - 全部 URL 展開（不只 3 個範例）

---

## 與業務版的視覺差異總覽

| 元素 | 業務版 | 專員版（本 Skill） |
|------|-------|----------------|
| Hero 三大數字 | 大字 + 漂亮配色 | 簡潔表格 |
| Strength banner | 必有 | 不需要 |
| Problem-card | 三大痛點獨立卡 | 全項目表格 |
| AIO 視覺區塊 | 有（深色） | 無 |
| Growth map | 三波同行 | 改為「執行清單」 |
| CTA 區塊 | 有 | 無（這是內部執行檔） |

---

## 完整 CSS（基於 _shared/visual-system.md 簡化）

```css
*,*::before,*::after{box-sizing:border-box;margin:0;padding:0;}
:root{
  --red:#C80A14;--gray-light:#F3F5F7;--border:#E2E6E8;
  --gray-600:#70787D;--gray-700:#4D4D4D;--dark:#111114;--mid:#8E969B;
  --white:#ffffff;--orange:#E67E22;--green:#27AE60;--yellow:#F39C12;
  --fact-blue:#3b82f6;--inference-yellow:#f59e0b;
  --max-w:980px;
  --font-main:'Noto Sans TC',sans-serif;
}
body{font-family:var(--font-main);font-size:15px;line-height:1.7;color:var(--gray-700);background:var(--gray-light);}
.container{max-width:var(--max-w);margin:0 auto;padding:0 24px;}
section{padding:40px 0;}

/* Header */
#header{background:var(--white);border-bottom:1px solid var(--border);padding:24px 0;}
.header-inner{display:flex;align-items:center;gap:16px;}
.header-logo{height:32px;}
.header-meta{margin-left:auto;font-size:15px;color:var(--mid);}
.report-type-badge{background:var(--dark);color:#fff;font-size:15px;font-weight:700;padding:4px 12px;border-radius:6px;margin-left:8px;}

/* Section title */
.section-title{font-size:20px;font-weight:900;color:var(--dark);margin-bottom:8px;border-bottom:2px solid var(--border);padding-bottom:8px;}
.section-desc{font-size:15px;color:var(--mid);margin-bottom:20px;}

/* Quick stats table */
.quick-stats{display:grid;grid-template-columns:repeat(auto-fit,minmax(160px,1fr));gap:12px;margin-bottom:32px;}
.qs-item{background:var(--white);border:1px solid var(--border);border-radius:10px;padding:14px;text-align:center;}
.qs-value{font-size:24px;font-weight:900;color:var(--dark);line-height:1.1;margin-bottom:4px;}
.qs-label{font-size:15px;color:var(--mid);}
.qs-item.alert .qs-value{color:var(--red);}
.qs-item.warn .qs-value{color:var(--orange);}
.qs-item.ok .qs-value{color:var(--green);}

/* Check table */
.check-table{width:100%;background:var(--white);border-collapse:collapse;border-radius:12px;overflow:hidden;border:1px solid var(--border);font-size:15px;margin-bottom:24px;}
.check-table th{background:var(--gray-light);padding:12px 14px;text-align:left;font-weight:700;color:var(--dark);font-size:15px;border-bottom:1px solid var(--border);}
.check-table td{padding:12px 14px;border-bottom:1px solid var(--border);vertical-align:top;}
.check-table tr:last-child td{border-bottom:none;}

/* Status badges */
.status-badge{display:inline-flex;align-items:center;gap:4px;font-size:15px;font-weight:700;padding:3px 10px;border-radius:100px;white-space:nowrap;}
.status-badge.fact{background:rgba(59,130,246,0.12);color:var(--fact-blue);}
.status-badge.inference{background:rgba(245,158,11,0.12);color:var(--inference-yellow);}
.status-badge.ok{background:rgba(39,174,96,0.12);color:#15803d;}
.status-badge.warn{background:rgba(245,158,11,0.12);color:#92400e;}
.status-badge.alert{background:rgba(200,10,20,0.12);color:var(--red);}

/* Details/expand */
details{background:var(--white);border:1px solid var(--border);border-radius:10px;padding:14px 16px;margin-bottom:12px;}
details summary{cursor:pointer;font-weight:700;color:var(--dark);font-size:15px;outline:none;}
details summary:hover{color:var(--red);}
details[open] summary{margin-bottom:10px;}
details ol,details ul{padding-left:20px;font-size:15px;}
details li{padding:4px 0;color:var(--gray-700);font-family:'SF Mono','Consolas',monospace;font-size:15px;word-break:break-all;}
details li a{color:var(--fact-blue);text-decoration:none;}
details li a:hover{text-decoration:underline;}

/* Code block */
pre{background:#1e1e2e;color:#d4d4d8;padding:14px 16px;border-radius:10px;overflow-x:auto;font-size:15px;font-family:'SF Mono','Consolas',monospace;line-height:1.6;}
code{font-family:'SF Mono','Consolas',monospace;}

/* Verification result */
.verification-grid{display:grid;grid-template-columns:1fr 1fr;gap:14px;}
.v-card{background:var(--white);border:1px solid var(--border);border-radius:10px;padding:14px;}
.v-card.matched{border-left:4px solid var(--green);}
.v-card.mismatch{border-left:4px solid var(--red);}
.v-card.partial{border-left:4px solid var(--orange);}
.v-title{font-weight:700;margin-bottom:6px;font-size:15px;}
.v-desc{font-size:15px;color:var(--gray-700);}

/* Execution checklist */
.exec-checklist{background:var(--white);border-radius:12px;padding:20px 24px;border:1px solid var(--border);}
.exec-item{display:flex;align-items:flex-start;gap:12px;padding:10px 0;border-bottom:1px solid var(--border);}
.exec-item:last-child{border-bottom:none;}
.exec-checkbox{width:18px;height:18px;border:2px solid var(--mid);border-radius:4px;flex-shrink:0;margin-top:2px;}
.exec-content{flex:1;}
.exec-title{font-weight:700;color:var(--dark);font-size:15px;margin-bottom:3px;}
.exec-desc{font-size:15px;color:var(--gray-600);}
.exec-priority{font-size:15px;font-weight:700;padding:2px 8px;border-radius:6px;margin-left:8px;}
.exec-priority.high{background:rgba(200,10,20,0.12);color:var(--red);}
.exec-priority.med{background:rgba(245,158,11,0.12);color:#92400e;}
.exec-priority.low{background:rgba(39,174,96,0.12);color:#15803d;}

/* Footer */
.report-footer{background:var(--dark);text-align:center;padding:32px 24px;font-size:15px;color:rgba(255,255,255,0.5);}
.footer-p1{color:rgba(255,255,255,0.4);font-size:15px;padding:0 1rem 6px;}
.footer-p2{color:rgba(180,83,9,0.65);font-style:italic;font-size:15px;padding:0 1rem 18px;}
.report-footer img{height:28px;opacity:0.5;display:block;margin:0 auto 14px;filter:brightness(0) invert(1);}

@media(max-width:640px){
  .verification-grid{grid-template-columns:1fr;}
  .quick-stats{grid-template-columns:repeat(2,1fr);}
  .check-table{font-size:15px;}
}
```

---

## 完整 HTML 結構

```html
<!DOCTYPE html>
<html lang="zh-TW">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width,initial-scale=1">
  <title>{客戶名} — 專員體質健檢 {YYYY-MM-DD}</title>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link href="https://fonts.googleapis.com/css2?family=Noto+Sans+TC:wght@400;700;900&display=swap" rel="stylesheet">
  <style>/* 上方完整 CSS */</style>
</head>
<body>

<!-- Header -->
<section id="header">
  <div class="container">
    <div class="header-inner">
      <img class="header-logo" src="https://awootsai.github.io/awoo_logo_hdr.png" alt="awoo">
      <div>
        <strong>{客戶名}</strong>
        <span class="report-type-badge">技術盤點</span>
      </div>
      <div class="header-meta">
        掃描日期 {YYYY-MM-DD} · 僅供 awoo 內部使用
      </div>
    </div>
  </div>
</section>

<!-- 快速統計 -->
<section id="quick-stats">
  <div class="container">
    <h2 class="section-title">🔵 爬蟲事實總覽</h2>
    <p class="section-desc">以下數字來自 harvester 直接掃描，為客觀事實。</p>
    <div class="quick-stats">
      <div class="qs-item"><div class="qs-value">247</div><div class="qs-label">總頁數</div></div>
      <div class="qs-item alert"><div class="qs-value">23</div><div class="qs-label">缺 H1</div></div>
      <div class="qs-item warn"><div class="qs-value">85%</div><div class="qs-label">Schema 覆蓋</div></div>
      <div class="qs-item ok"><div class="qs-value">240</div><div class="qs-label">BreadcrumbList</div></div>
    </div>
  </div>
</section>

<!-- 五大檢查項目 -->
<section id="url-consistency">
  <div class="container">
    <h2 class="section-title">URL 一致性檢查</h2>
    <table class="check-table">
      <!-- 參考 tech-checks/url-consistency.md -->
    </table>
    <details>
      <summary>原始資料：cross-canonical pair 清單</summary>
      <ol>
        <li>...全部 URL...</li>
      </ol>
    </details>
  </div>
</section>

<section id="h-tags-check">
  <div class="container">
    <h2 class="section-title">H 標籤結構檢查</h2>
    <!-- 參考 tech-checks/h-tags.md -->
  </div>
</section>

<section id="schema-check">
  <div class="container">
    <h2 class="section-title">Schema / JSON-LD 檢查</h2>
    <!-- 參考 tech-checks/schema-jsonld.md -->
  </div>
</section>

<section id="canonical-check">
  <div class="container">
    <h2 class="section-title">Canonical / noindex 檢查</h2>
    <!-- 參考 tech-checks/canonical-noindex.md -->
  </div>
</section>

<section id="freshness-check">
  <div class="container">
    <h2 class="section-title">文章新鮮度檢查</h2>
    <!-- 參考 tech-checks/content-freshness.md -->
  </div>
</section>

<!-- 業務版對照（如有） -->
<section id="verification-section">
  <div class="container">
    <h2 class="section-title">業務版報告對照</h2>
    <p class="section-desc">本區針對業務版健檢報告進行驗證，標記矛盾點供阿達決策。</p>
    <div class="verification-grid">
      <div class="v-card mismatch">
        <div class="v-title">⚠️ 矛盾點 1</div>
        <div class="v-desc">業務版說 Schema 覆蓋率 60%，實際為 75%</div>
      </div>
      <div class="v-card matched">
        <div class="v-title">✅ 一致</div>
        <div class="v-desc">業務版觀察：缺 H1 23 頁。已驗證一致</div>
      </div>
    </div>
  </div>
</section>

<!-- 執行清單 -->
<section id="execution-checklist">
  <div class="container">
    <h2 class="section-title">專員執行清單</h2>
    <p class="section-desc">以下為依優先順序排列的具體執行項目。</p>
    <div class="exec-checklist">
      <div class="exec-item">
        <div class="exec-checkbox"></div>
        <div class="exec-content">
          <div>
            <span class="exec-title">補上首頁 Organization Schema</span>
            <span class="exec-priority high">高</span>
          </div>
          <div class="exec-desc">建議放在 head 區塊，含 name / logo / address / contactPoint</div>
        </div>
      </div>
    </div>
  </div>
</section>

<!-- Footer（專員版微調文案） -->
<footer class="report-footer">
  <img src="https://awootsai.github.io/awoo_logo_ftr.png" alt="awoo">
  <div class="footer-p1">本技術盤點透過 awoo 阿物科技 近 20 年資料庫與 AI 運算生成（掃描日期 {SCAN_DATE}）</div>
  <div class="footer-p2">⚠️ 此報告僅供 awoo 內部專員執行使用，不對客戶呈現</div>
</footer>

</body>
</html>
```

---

## 驗證清單

- [ ] 字體最小 15px
- [ ] awoo 全小寫
- [ ] 標記🔵 事實 vs 🟡 推論
- [ ] 五大檢查項目（URL、H、Schema、Canonical、新鮮度）全展開
- [ ] 業務版對照區塊（如有業務版可比對）
- [ ] 執行清單區塊（依優先順序）
- [ ] 全部原始資料用 details 展開（不要只列 3 個範例）
- [ ] footer 標註「僅供 awoo 內部專員執行使用」
- [ ] 不需 CTA、Hero 大字、Strength banner（這些是業務版才有）
