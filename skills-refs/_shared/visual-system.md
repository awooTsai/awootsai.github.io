# 統一視覺規範

> 四個 Skill 產出 HTML 報告的共用視覺系統。
> 改一處全部報告風格自動同步。

---

## 1. 色彩系統

### 主色（awoo 識別色）
- `--red: #C80A14`（awoo 品牌紅，主強調色）
- `--dark: #111114`（深色背景、Hero 區）
- `--white: #ffffff`（白底）

### 灰階
- `--gray-light: #F3F5F7`（淺灰背景）
- `--border: #E2E6E8`（邊框）
- `--gray-600: #70787D`（中等文字）
- `--gray-700: #4D4D4D`（一般文字）
- `--mid: #8E969B`（輔助文字）

### 狀態色
- `--green: #27AE60`（強項、達標）
- `--orange: #E67E22`（中等警示）
- `--yellow: #F39C12`（注意）

### 高亮色（用於數據強調）
- 紅色亮度版：`#ff6b7a`（深色背景的紅）
- 紫色：`#a78bfa`（紫色強調）
- 琥珀色：`#fbbf24`（橙黃強調）

---

## 2. 字體系統

### 字型家族
```css
--font-main: 'Noto Sans TC', sans-serif;   /* 中文主字型 */
--font-num: 'Bebas Neue', cursive;          /* 數字強調字型 */
```

字型載入：
```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Bebas+Neue&family=Noto+Sans+TC:wght@400;500;700;900&display=swap" rel="stylesheet">
```

### 字級鐵律

**最小字體 15px** — 不論 inline style 或 CSS class 都不可低於此。

| 用途 | 字級 |
|------|------|
| 一般正文 | 16px (line-height 1.8) |
| 區段內輔助文字 | 15px（最小值） |
| 區段標題 | clamp(22px, 4vw, 30px) |
| 客戶品牌名（Intro） | clamp(24px, 5.5vw, 42px) |
| Hero 數字（big-num） | clamp(50px, 9vw, 74px) |

---

## 3. 空間系統

### 容器寬度
```css
--max-w: 860px;
.container { max-width: var(--max-w); margin: 0 auto; padding: 0 28px; }
```

### Section padding
```css
section { padding: 60px 0; }
```

### 圓角
- 大區塊（card, banner）：`border-radius: 16px` 或 `20px`
- 中等區塊（item）：`border-radius: 12px` 或 `14px`
- 標籤、徽章：`border-radius: 100px`（藥丸狀）

---

## 4. 必備區塊結構

### 4.1 Sticky Nav（固定頂部導覽）

```html
<nav id="sticky-nav">
  <img src="https://awootsai.github.io/awoo_logo_hdr.png" alt="awoo">
</nav>
```

特性：
- 進入 Hero 後才出現（用 IntersectionObserver）
- 半透明白底 + backdrop-filter blur
- 統一在所有報告類型出現

### 4.2 Intro 區塊（報告開場）

```html
<section id="intro">
  <div class="intro-inner">
    <img class="intro-logo" src="https://awootsai.github.io/awoo_logo_hdr.png" alt="awoo 阿物科技">
    <div class="intro-rule"></div>
    <div class="intro-eyebrow">[報告類型] · [日期]</div>
    <h1 class="intro-client">[客戶名稱]</h1>
    <div class="intro-subtitle">[一行簡介]</div>
    <div class="intro-pills">
      <!-- 數據標籤 -->
    </div>
  </div>
</section>
```

### 4.3 Hero 區塊（深色，三大數字）

```html
<section id="hero">
  <div class="container">
    <div class="hero-label">SITE HEALTH · KEY NUMBERS</div>
    <div class="hero-numbers">
      <div class="hero-num-card num-red">
        <span class="big-num">[數字]</span>
        <div class="num-label">[標籤]</div>
        <div class="num-sub">[說明]</div>
      </div>
      <!-- 共三張卡 -->
    </div>
  </div>
</section>
```

### 4.4 Footer 區塊

統一使用 `_shared/footer-signature.html` 內容。

---

## 5. 動畫與互動

### Sticky Nav 進場動畫
```javascript
const obs = new IntersectionObserver(function(entries) {
  entries.forEach(function(e) {
    if (e.isIntersecting) {
      nav.classList.remove('active');
    } else {
      nav.classList.add('active');
    }
  });
}, { threshold: 0, rootMargin: '-52px 0px 0px 0px' });
obs.observe(logo);
```

### Toast 提示（複製成功）
```css
.toast {
  position: fixed;
  bottom: 72px;
  left: 50%;
  transform: translateX(-50%) translateY(8px);
  opacity: 0;
  transition: opacity .25s, transform .25s;
}
.toast.show {
  opacity: 1;
  transform: translateX(-50%) translateY(0);
}
```

### Copy 按鈕（雙保險）
```javascript
function _awooCopy(text, cb) {
  if (navigator.clipboard && navigator.clipboard.writeText) {
    navigator.clipboard.writeText(text).then(cb).catch(function() {
      _fallbackCopy(text, cb);
    });
  } else {
    _fallbackCopy(text, cb);
  }
}
function _fallbackCopy(text, cb) {
  var ta = document.createElement('textarea');
  ta.value = text;
  ta.style.cssText = 'position:fixed;opacity:0;top:0;left:0;';
  document.body.appendChild(ta);
  ta.focus();
  ta.select();
  try {
    document.execCommand('copy');
    cb();
  } catch(e) {
    awooShowToast('請手動長按複製');
  }
  document.body.removeChild(ta);
}
```

---

## 6. 各 Skill 的視覺差異

### geo-site-audit（業務提案版健檢）
- 完整套用本視覺系統
- Hero 三大數字 + Strength banner + 三大痛點 + Growth map + CTA
- 最完整的視覺呈現

### geo-keyword-research（關鍵字拓展）
- 沿襲 visual-system，但 Hero 改為「關鍵字盤點數量」三數字
- 增加「三波策略」分區（順風 / 補強 / 攻堅）
- 每組關鍵字呈現：搜尋量 + 競爭性 + 與客戶內容的對應

### geo-prompt-builder（Prompt 候選池）
- 沿襲 visual-system
- Hero 改為「總候選池數量 / 三意圖比例」
- 主要呈現：每組關鍵字的 Prompt 列表 + 一鍵複製

### geo-tech-audit（專員體質健檢）
- **不對客戶呈現**，視覺更技術導向
- 表格化呈現多
- 區分「🔵 爬蟲事實」vs「🟡 AI 推論」標記
- 字體可略小（但仍不低於 15px）
- 資訊密度比業務版高

---

## 7. 響應式設計

```css
@media (max-width: 640px) {
  .hero-numbers { grid-template-columns: 1fr; }
  .scorecard { grid-template-columns: 1fr; }
  .icon-grid { grid-template-columns: repeat(2, 1fr); }
}
```

所有 Skill 應確保在手機檢視時正常呈現。

---

## 8. 完整 CSS 範本

詳見各 Skill 的 `visual/html-template.md`，內含完整可直接複製的 CSS。

各 Skill 自己的 visual 應：
1. 引用本 `visual-system.md` 的 CSS 變數
2. 加上 Skill 自己特殊的視覺元件（如關鍵字 pill、Prompt card）
3. 保留 `_shared/footer-signature.html` 的 footer
