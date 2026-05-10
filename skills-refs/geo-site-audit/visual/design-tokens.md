# geo-site-audit 視覺微調

> 業務提案版健檢 Skill 自有的視覺微調規則。
> 共用視覺系統見 `_shared/visual-system.md`，本檔案僅補充本 Skill 特有元件。

---

## 1. Hero 三大數字的選色策略

| 數字類型 | 顏色 | 使用情境 |
|---------|------|---------|
| 紅色（主強調） | `--red: #C80A14` / `#ff6b7a`（深色背景版） | 最關鍵的「問題」數字（如缺 H1 頁數、Description 多樣性） |
| 橙色（次強調） | `#fbbf24` | 第二嚴重的問題數字 |
| 紫色（亮點） | `#c4b5fd` | 客戶網站的亮點（如 Schema 覆蓋率、頁數規模） |

選擇邏輯：3 個數字必須是「2 個問題 + 1 個亮點」，不要全部是負面。

---

## 2. problem-card 的視覺差異化

```css
.problem-card.high  { border-left: 4px solid var(--red); }     /* 第一痛點 */
.problem-card.med   { border-left: 4px solid var(--orange); }  /* 第二痛點 */
.problem-card.med2  { border-left: 4px solid var(--yellow); }  /* 第三痛點 */
```

不要使用 4 種以上的 border-left 顏色，超過 3 個痛點的話往後合併或精簡。

---

## 3. AI 引用測試區（深色 Section）的特殊配色

```css
#ai-citation {
  background: #111114;
  color: rgba(255,255,255,0.85);
}
.ai-link.gpt-link { background: #19c37d; color: #fff; }   /* ChatGPT 綠 */
.ai-link.gem-link { background: #4285f4; color: #fff; }   /* Gemini 藍 */
.ai-link.copy-link { background: rgba(255,255,255,0.12); color: rgba(255,255,255,0.8); }
```

按鈕配色不可改，這是 awoo 業務提案版健檢的識別色。

---

## 4. 文字排版鐵律

- 段落 line-height: 1.85（中文閱讀舒適區間）
- 區段間距 padding: 60px 0
- max-width: 860px（內容最大寬度）

字級檢查（grep 應為 0 結果）：
```
grep -E 'font-size:\s*1[01234]px' [檔案]
```

---

## 5. 動畫節制原則

業務提案版健檢的動畫必須節制：
- ✅ Sticky nav 進場
- ✅ Toast 提示
- ✅ 痛點區塊 fade-in（如有）
- ❌ 不用大量 hover 動畫
- ❌ 不用滾動視差
- ❌ 不用會干擾閱讀的視覺特效

報告是給客戶看的「商務文件」，不是炫技作品。
