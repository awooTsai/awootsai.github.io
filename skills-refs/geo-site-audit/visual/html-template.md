# geo-site-audit HTML 結構模板

> 業務提案版健檢報告的完整 HTML 結構與 CSS。
> 視覺對齊：https://awoo-vital.vercel.app/jerscy

---

## 完整 CSS（直接複製到 `<style>` 區塊）

```css
*,*::before,*::after{box-sizing:border-box;margin:0;padding:0;}
:root{
  --red:#C80A14;--gray-light:#F3F5F7;--border:#E2E6E8;
  --gray-600:#70787D;--gray-700:#4D4D4D;--dark:#111114;--mid:#8E969B;
  --white:#ffffff;--orange:#E67E22;--green:#27AE60;--yellow:#F39C12;
  --max-w:860px;
  --font-main:'Noto Sans TC',sans-serif;--font-num:'Bebas Neue',cursive;
}
body{font-family:var(--font-main);font-size:16px;line-height:1.8;color:var(--gray-700);background:#F0F1F4;}
.container{max-width:var(--max-w);margin:0 auto;padding:0 28px;}
section{padding:60px 0;}

/* Sticky Nav */
#sticky-nav{position:fixed;top:0;left:0;right:0;z-index:1000;height:52px;background:rgba(255,255,255,0);backdrop-filter:blur(0px);border-bottom:1px solid rgba(200,10,20,0);display:flex;align-items:center;justify-content:center;transition:background .35s,backdrop-filter .35s,border-color .35s;}
#sticky-nav.active{background:rgba(255,255,255,0.88);backdrop-filter:blur(16px);border-bottom:1px solid rgba(200,10,20,0.15);}
#sticky-nav img{height:28px;opacity:0;transform:translateY(-6px);transition:opacity .35s,transform .35s;}
#sticky-nav.active img{opacity:1;transform:translateY(0);}

/* Intro */
#intro{background:var(--white);padding:0;border-top:4px solid var(--red);}
.intro-inner{max-width:var(--max-w);margin:0 auto;padding:64px 28px 52px;display:flex;flex-direction:column;align-items:center;text-align:center;}
.intro-logo{height:100px;display:block;margin-bottom:36px;}
.intro-rule{width:1px;height:40px;background:linear-gradient(to bottom,var(--border),transparent);margin-bottom:28px;}
.intro-eyebrow{font-size:15px;font-weight:700;letter-spacing:3px;text-transform:uppercase;color:var(--red);margin-bottom:12px;}
.intro-client{font-size:clamp(24px,5.5vw,42px);font-weight:900;line-height:1.2;color:var(--dark);margin-bottom:8px;letter-spacing:-0.5px;}
.intro-subtitle{font-size:clamp(15px,3vw,18px);color:var(--mid);margin-bottom:32px;}
.intro-pills{display:flex;flex-wrap:wrap;justify-content:center;gap:8px;}
.intro-pill{display:inline-flex;align-items:center;gap:5px;font-size:15px;color:var(--gray-600);background:var(--gray-light);border:1px solid var(--border);padding:5px 14px;border-radius:100px;}
.intro-pill.stage{background:rgba(230,126,34,0.1);border-color:rgba(230,126,34,0.35);color:#92400e;font-weight:700;}
.intro-pill.good{background:rgba(39,174,96,0.1);border-color:rgba(39,174,96,0.35);color:#15803d;font-weight:700;}

/* Hero */
#hero{background:var(--dark);padding:60px 0 56px;position:relative;overflow:hidden;}
#hero::after{content:'';position:absolute;bottom:-80px;left:-80px;width:320px;height:320px;background:radial-gradient(circle,rgba(200,10,20,0.18) 0%,transparent 70%);pointer-events:none;}
.hero-label{font-size:15px;font-weight:700;letter-spacing:3px;text-transform:uppercase;color:rgba(255,255,255,0.3);margin-bottom:28px;}
.hero-numbers{display:grid;grid-template-columns:repeat(3,1fr);gap:16px;}
.hero-num-card{background:rgba(255,255,255,0.04);border:1px solid rgba(255,255,255,0.08);border-radius:20px;padding:32px 24px 28px;text-align:center;position:relative;overflow:hidden;}
.hero-num-card::after{content:'';position:absolute;bottom:0;left:20%;right:20%;height:2px;border-radius:2px;}
.hero-num-card.num-red::after{background:var(--red);box-shadow:0 0 12px rgba(200,10,20,0.6);}
.hero-num-card.num-orange::after{background:#f5a623;box-shadow:0 0 12px rgba(245,166,35,0.5);}
.hero-num-card.num-purple::after{background:#a78bfa;box-shadow:0 0 12px rgba(167,139,250,0.5);}
.big-num{font-family:var(--font-num);font-size:clamp(50px,9vw,74px);line-height:1;letter-spacing:1px;display:block;margin-bottom:12px;}
.num-red .big-num{color:#ff6b7a;}.num-orange .big-num{color:#fbbf24;}.num-purple .big-num{color:#c4b5fd;}
.num-label{font-size:15px;color:rgba(255,255,255,0.7);line-height:1.5;}
.num-sub{font-size:15px;color:rgba(255,255,255,0.45);margin-top:8px;line-height:1.4;}

/* Section common */
.section-tag{display:inline-block;font-size:15px;font-weight:700;letter-spacing:2px;text-transform:uppercase;color:var(--red);background:rgba(200,10,20,0.07);padding:4px 12px;border-radius:100px;margin-bottom:12px;}
.section-title{font-size:clamp(22px,4vw,30px);font-weight:900;color:var(--dark);margin-bottom:8px;line-height:1.3;}
.section-desc{font-size:15px;color:var(--mid);margin-bottom:32px;line-height:1.9;max-width:640px;}

/* Glossary */
#glossary{background:var(--white);}
.glossary-grid{display:grid;grid-template-columns:repeat(2,1fr);gap:0;background:#F8F9FA;border:1px solid var(--border);border-radius:14px;overflow:hidden;}
.g-item{padding:14px 18px;border-bottom:1px solid var(--border);}
.g-item:nth-child(odd){border-right:1px solid var(--border);}
.g-item:nth-last-child(-n+2){border-bottom:none;}
.g-item dt{font-size:15px;font-weight:700;color:var(--dark);margin-bottom:3px;}
.g-item dd{font-size:15px;color:var(--gray-600);}

/* Strength banner */
.strength-banner{background:linear-gradient(135deg,#064e3b,#065f46);border-radius:16px;padding:24px 28px;margin-bottom:36px;display:flex;align-items:flex-start;gap:18px;}
.strength-icon{font-size:28px;flex-shrink:0;margin-top:2px;}
.strength-title{font-size:17px;font-weight:900;color:#4ade80;margin-bottom:8px;}
.strength-body{font-size:15px;color:rgba(255,255,255,0.8);line-height:1.85;}
.strength-chips{display:flex;flex-wrap:wrap;gap:8px;margin-top:12px;}
.s-chip{background:rgba(74,222,128,0.15);border:1px solid rgba(74,222,128,0.3);color:#4ade80;font-size:15px;padding:4px 12px;border-radius:100px;font-weight:700;}

/* Objective finding (痛點區) */
#objective-finding{background:#F8F9FA;}
.icon-grid{display:grid;grid-template-columns:repeat(4,1fr);gap:12px;margin-bottom:32px;}
.ig-item{background:var(--white);border:1px solid var(--border);border-radius:12px;padding:18px 14px;text-align:center;}
.ig-num{font-family:var(--font-num);font-size:28px;color:var(--red);line-height:1;margin-bottom:6px;}
.ig-label{font-size:15px;color:var(--mid);}
.problem-grid{display:flex;flex-direction:column;gap:20px;}
.problem-card{background:var(--white);border-radius:16px;padding:28px 28px 22px;border:1px solid var(--border);}
.problem-card.high{border-left:4px solid var(--red);}
.problem-card.med{border-left:4px solid var(--orange);}
.problem-card.med2{border-left:4px solid var(--yellow);}
.problem-header{display:flex;align-items:flex-start;justify-content:space-between;margin-bottom:14px;gap:12px;}
.problem-title{font-size:17px;font-weight:900;color:var(--dark);}
.impact-badge{font-size:15px;font-weight:700;padding:4px 12px;border-radius:100px;white-space:nowrap;flex-shrink:0;}
.impact-badge.high{background:rgba(200,10,20,0.1);color:var(--red);}
.impact-badge.med{background:rgba(230,126,34,0.1);color:#92400e;}
.problem-loss{font-size:15px;color:var(--gray-700);line-height:1.85;margin-bottom:14px;overflow-wrap:break-word;}
.verified-pages{background:var(--gray-light);border-radius:10px;padding:14px 16px;}
.vt{font-weight:700;color:var(--dark);margin-bottom:8px;font-size:15px;}
.verified-pages a{display:block;color:#1a6fc4;font-size:15px;text-decoration:none;margin-top:4px;overflow-wrap:break-word;}
.verified-pages a:hover{text-decoration:underline;}

/* Specific issues */
#specific-issues{background:var(--white);}
.scorecard{display:grid;grid-template-columns:repeat(3,1fr);gap:14px;margin-bottom:36px;}
.sc-card{border-radius:14px;padding:20px 18px;text-align:center;}
.sc-card.red{background:rgba(200,10,20,0.07);border:1px solid rgba(200,10,20,0.2);}
.sc-card.yellow{background:rgba(243,156,18,0.07);border:1px solid rgba(243,156,18,0.25);}
.sc-card.green{background:rgba(39,174,96,0.07);border:1px solid rgba(39,174,96,0.2);}
.sc-dot{width:10px;height:10px;border-radius:50%;display:inline-block;margin-bottom:10px;}
.sc-dot.red{background:var(--red);}.sc-dot.yellow{background:var(--yellow);}.sc-dot.green{background:var(--green);}
.sc-val{font-family:var(--font-num);font-size:32px;line-height:1;margin-bottom:6px;}
.sc-card.red .sc-val{color:var(--red);}.sc-card.yellow .sc-val{color:var(--yellow);}.sc-card.green .sc-val{color:var(--green);}
.sc-label{font-size:15px;color:var(--gray-600);}
.pain-bars{display:flex;flex-direction:column;gap:22px;}
.pain-bar-label{font-size:15px;font-weight:700;color:var(--dark);margin-bottom:8px;}
.pain-bar-track{position:relative;height:28px;background:var(--gray-light);border-radius:100px;overflow:hidden;}
.pain-bar-current{position:absolute;left:0;top:0;height:100%;background:linear-gradient(90deg,var(--red),#e01020);border-radius:100px;display:flex;align-items:center;justify-content:flex-end;padding-right:8px;font-family:var(--font-num);font-size:15px;color:#fff;min-width:36px;}

/* Content DNA */
#content-dna{background:#F8F9FA;}
.dna-donut-wrap{display:flex;gap:36px;align-items:center;margin-bottom:24px;}
.donut-container{position:relative;flex-shrink:0;}
.donut-chart{width:180px;height:180px;border-radius:50%;}
.donut-hole{position:absolute;top:50%;left:50%;transform:translate(-50%,-50%);width:88px;height:88px;background:var(--white);border-radius:50%;display:flex;flex-direction:column;align-items:center;justify-content:center;}
.donut-hole-num{font-family:var(--font-num);font-size:28px;color:var(--dark);line-height:1;}
.donut-hole-label{font-size:15px;color:var(--mid);}
.dna-legend{flex:1;}
.legend-item{display:flex;align-items:center;gap:10px;padding:8px 0;border-bottom:1px solid var(--border);}
.legend-item:last-child{border-bottom:none;}
.legend-dot{width:12px;height:12px;border-radius:3px;flex-shrink:0;}
.legend-name{font-size:15px;color:var(--dark);flex:1;}
.legend-pct{font-family:var(--font-num);font-size:17px;color:var(--dark);}
.dna-insight{background:rgba(99,102,241,0.06);border-left:3px solid #6366f1;padding:14px 18px;font-size:15px;color:#4338ca;border-radius:0 10px 10px 0;line-height:1.8;}

/* AI Citation */
.ai-link{display:inline-flex;align-items:center;font-size:15px;padding:5px 12px;border-radius:8px;text-decoration:none;cursor:pointer;border:none;font-family:var(--font-main);font-weight:600;}
.gpt-link{background:#19c37d;color:#fff;}
.gem-link{background:#4285f4;color:#fff;}
.copy-link{background:rgba(255,255,255,0.12);color:rgba(255,255,255,0.8);}
.citation-verdict{font-size:15px;color:rgba(255,255,255,0.6);line-height:1.9;background:rgba(255,255,255,0.03);border-radius:12px;padding:18px 22px;}
.geo-explainer{background:rgba(255,255,255,0.06);border:1px solid rgba(255,255,255,0.1);border-radius:12px;padding:18px 22px;font-size:15px;color:rgba(255,255,255,0.75);line-height:1.85;margin-bottom:24px;}

/* Growth Map */
#growth-map{background:var(--white);}
.kw-direction{background:var(--gray-light);border:1px solid var(--border);border-radius:16px;padding:24px 24px 20px;margin-bottom:20px;}
.kw-dir-header{display:flex;align-items:center;gap:14px;margin-bottom:16px;}
.kw-icon{width:44px;height:44px;border-radius:12px;display:flex;align-items:center;justify-content:center;font-size:20px;flex-shrink:0;}
.kw-dir-title{font-size:17px;font-weight:900;line-height:1.35;color:var(--dark);}
.kw-dir-sub{font-size:15px;color:var(--mid);margin-top:3px;}
.kw-tracks{display:grid;grid-template-columns:1fr 1fr;gap:14px;}
.kw-track{background:var(--white);border-radius:10px;padding:16px 18px;}
.kw-track-label{font-size:15px;font-weight:700;margin-bottom:10px;}
.kw-track-label.precise{color:var(--green);}.kw-track-label.broad{color:var(--mid);}
.kw-pills{display:flex;flex-wrap:wrap;gap:6px;}
.kw-pill{font-size:15px;padding:4px 11px;border-radius:100px;font-weight:500;}
.kw-pill.precise{background:#dcfce7;color:#15803d;}.kw-pill.broad{background:var(--border);color:var(--mid);}
.kw-strategy-note{background:rgba(99,102,241,0.06);border-left:3px solid #6366f1;padding:12px 16px;font-size:15px;color:#4338ca;border-radius:0 8px 8px 0;margin-top:14px;line-height:1.7;}

/* CTA */
#cta{background:#F8F9FA;}
.cta-intro{font-size:15px;color:var(--mid);margin-bottom:32px;max-width:580px;line-height:1.9;}
.awoo-actions{display:flex;flex-direction:column;gap:12px;margin-bottom:36px;}
.action-item{display:flex;gap:18px;align-items:flex-start;background:var(--white);border:1px solid var(--border);border-radius:14px;padding:20px 22px;}
.action-num{width:38px;height:38px;flex-shrink:0;background:var(--red);color:var(--white);font-family:var(--font-num);font-size:24px;display:flex;align-items:center;justify-content:center;border-radius:10px;}
.action-title{font-size:16px;font-weight:700;margin-bottom:4px;color:var(--dark);}
.action-desc{font-size:15px;color:var(--mid);line-height:1.75;}
.cta-contact{background:linear-gradient(135deg,#9b0a10 0%,var(--red) 45%,#e01020 100%);color:var(--white);border-radius:20px;padding:40px 36px 36px;text-align:center;}
.cta-contact h3{font-size:22px;font-weight:900;margin-bottom:8px;}
.cta-contact p{font-size:15px;color:rgba(255,255,255,0.72);margin-bottom:22px;}
.cta-btn{display:inline-block;background:var(--white);color:var(--red);font-weight:900;font-size:16px;padding:14px 40px;border-radius:50px;text-decoration:none;}

/* Footer */
.report-footer{background:var(--dark);text-align:center;padding:40px 28px;font-size:15px;line-height:1.8;}
.footer-p1{color:rgba(255,255,255,0.4);font-size:15px;padding:0 1rem 6px;}
.footer-p2{color:rgba(180,83,9,0.65);font-style:italic;font-size:15px;padding:0 1rem 18px;}
.report-footer img{height:32px;opacity:0.5;display:block;margin:0 auto 18px;filter:brightness(0) invert(1);}
.footer-link{color:rgba(255,255,255,0.5);font-size:15px;text-decoration:none;}
.footer-link:hover{color:var(--white);text-decoration:underline;}

/* Toast */
.gem-toast{position:fixed;bottom:72px;left:50%;transform:translateX(-50%) translateY(8px);background:#1a73e8;color:#fff;padding:10px 20px;border-radius:10px;font-size:15px;z-index:9999;opacity:0;transition:opacity .25s,transform .25s;pointer-events:none;}
.gem-toast.show{opacity:1;transform:translateX(-50%) translateY(0);}

@media(max-width:640px){
  .hero-numbers{grid-template-columns:1fr;}
  .kw-tracks{grid-template-columns:1fr;}
  .dna-donut-wrap{flex-direction:column;}
  .scorecard{grid-template-columns:1fr;}
  .icon-grid{grid-template-columns:repeat(2,1fr);}
}
```

---

## 完整 HTML 結構（含 Sticky nav + 7 大 sections + footer + scripts）

詳見 ada-geo-site-audit 過去產出案例（如 Cloud Inc、台全牧場、Simmpo 等），完整骨架包含：

```
<!DOCTYPE html>
<html lang="zh-TW">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width,initial-scale=1">
  <title>{客戶名} — GEO 健檢報告 {YYYY-MM-DD}</title>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link href="https://fonts.googleapis.com/css2?family=Bebas+Neue&family=Noto+Sans+TC:wght@400;500;700;900&display=swap" rel="stylesheet">
  <style>
    /* 上方完整 CSS */
  </style>
</head>
<body>

<nav id="sticky-nav">
  <img src="https://awootsai.github.io/awoo_logo_hdr.png" alt="awoo">
</nav>

<!-- 1. INTRO -->
<section id="intro">...</section>

<!-- 2. HERO（三大數字） -->
<section id="hero">...</section>

<!-- 3. GLOSSARY（小辭彙） -->
<section id="glossary">...</section>

<!-- 4. OBJECTIVE FINDING（強項 + 三大痛點） -->
<section id="objective-finding">
  <div class="strength-banner">...</div>
  <div class="problem-grid">
    <div class="problem-card high">...</div>  <!-- 痛點 1 -->
    <div class="problem-card med">...</div>   <!-- 痛點 2 -->
    <div class="problem-card med2">...</div>  <!-- 痛點 3 -->
  </div>
  <!-- Alt 提示框（灰色） -->
</section>

<!-- 5. SPECIFIC ISSUES（體質快覽） -->
<section id="specific-issues">
  <div class="scorecard">...</div>  <!-- 三色燈 -->
  <div class="pain-bars">...</div>
</section>

<!-- 6. CONTENT DNA（內容主題分佈） -->
<section id="content-dna">...</section>

<!-- 7. AI VISIBILITY（AIO 能見度，深色背景） -->
<section id="ai-visibility" style="background:#1a1a24;color:#fff;...">...</section>

<!-- 8. AI CITATION（AI 引用測試，深色） -->
<section id="ai-citation" style="background:#111114;...">...</section>

<!-- 9. GROWTH MAP（三段同行的方向） -->
<section id="growth-map">...</section>

<!-- 10. CTA -->
<section id="cta">...</section>

<!-- Footer（從 _shared/footer-signature.html） -->
<footer class="report-footer">...</footer>

<script>
  /* 複製按鈕 + Toast + Sticky nav 動畫 */
</script>
</body>
</html>
```

---

## JavaScript 標準範本

```javascript
function awooGeminiClick(btn){
  var q=btn.dataset.q||'';
  _awooCopy(q,function(){
    window.open('https://gemini.google.com/app','_blank','noopener');
    awooShowToast('✓ 已複製，請在 Gemini 貼上');
  });
}
function awooCopyClick(btn){
  _awooCopy(btn.dataset.q||'',function(){
    awooShowToast('✓ 問句已複製到剪貼簿');
  });
}
function _awooCopy(text,cb){
  if(navigator.clipboard&&navigator.clipboard.writeText){
    navigator.clipboard.writeText(text).then(cb).catch(function(){_fallbackCopy(text,cb);});
  }else{_fallbackCopy(text,cb);}
}
function _fallbackCopy(text,cb){
  var ta=document.createElement('textarea');
  ta.value=text;ta.style.cssText='position:fixed;opacity:0;top:0;left:0;';
  document.body.appendChild(ta);ta.focus();ta.select();
  try{document.execCommand('copy');cb();}catch(e){awooShowToast('請手動長按問句複製');}
  document.body.removeChild(ta);
}
function awooShowToast(text){
  var t=document.createElement('div');t.className='gem-toast';t.textContent=text;
  document.body.appendChild(t);
  requestAnimationFrame(function(){t.classList.add('show');});
  setTimeout(function(){t.classList.remove('show');setTimeout(function(){t.remove();},300);},3000);
}
(function(){
  var nav=document.getElementById('sticky-nav');
  var logo=document.querySelector('.intro-logo');
  if(!nav||!logo)return;
  var obs=new IntersectionObserver(function(entries){
    entries.forEach(function(e){
      if(e.isIntersecting){nav.classList.remove('active');}
      else{nav.classList.add('active');}
    });
  },{threshold:0,rootMargin:'-52px 0px 0px 0px'});
  obs.observe(logo);
})();
```

---

## 驗證清單

產出 HTML 前確認：

- [ ] 字體最小 15px（grep `font-size:\s*1[01234]px` 應為 0 結果）
- [ ] awoo 全小寫（不應有 AWOO、Awoo）
- [ ] Logo URL 正確（awootsai.github.io/awoo_logo_hdr.png 與 awoo_logo_ftr.png）
- [ ] sticky-nav + IntersectionObserver 已加入
- [ ] big-num class 字級 50-74px
- [ ] problem-card 至少 3 張
- [ ] verified-pages 至少 3 個 URL（已 web_fetch 驗證）
- [ ] 水面上下對比框（AI 能見度區塊）
- [ ] donut-chart + dna-insight
- [ ] kw-direction 至少 3 個（成長方向）
- [ ] cta-contact 區塊完整
- [ ] PROMPT 01 / 複製問句按鈕（含 _fallbackCopy + execCommand 雙保險）
- [ ] AI 問句長度 ≥ 15 字
- [ ] scorecard + pain-bars 有出現
- [ ] strength-banner 有出現
- [ ] Alt 提示框（rgba(243,156,18) 灰色）
- [ ] footer 兩段式格式正確
