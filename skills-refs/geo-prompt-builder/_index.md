# geo-prompt-builder references 路由索引

> Prompt 候選清單拓展 — 條件式載入路由表

---

## 必讀（任務一律先讀）

### 來自 _shared/
1. `_shared/awoo-tone.md`
2. `_shared/customer-tone.md`
3. `_shared/visual-system.md`

### 來自本 Skill
4. `geo-prompt-builder/core/master-rules.md`
5. `geo-prompt-builder/core/extension-logic.md` — 雙倍候選池邏輯

---

## 三種 Customer Journey 意圖（依任務需要讀取）

| 意圖 | 應讀取 |
|------|-------|
| 探索型 Prompt | `geo-prompt-builder/customer-journey/exploration.md` |
| 決策型 Prompt | `geo-prompt-builder/customer-journey/decision.md` |
| 品牌型 Prompt | `geo-prompt-builder/customer-journey/brand.md` |

通常三種都會用到（每組關鍵字至少有 1 條品牌型）。

---

## 產出 HTML 時讀取

1. `geo-prompt-builder/visual/html-template.md`
2. `_shared/footer-signature.html`

---

## 產出檢查清單

- [ ] 每個關鍵字延伸 4-7 條 Prompt
- [ ] 總候選池 = 待選數的 2 倍
- [ ] 每組關鍵字至少有 1 條品牌型 Prompt
- [ ] Prompt 為完整問句（口語化），非搜尋關鍵字格式
- [ ] 三意圖比例：探索 30-40% / 決策 40-50% / 品牌 20-30%
- [ ] 字體最小 15px
- [ ] 視覺對齊 ada-geo-site-audit + ada-geo-keyword-research
- [ ] 提供「一鍵複製」功能
- [ ] footer 兩段式格式
