# geo-tech-audit references 路由索引

> 專員體質健檢 — 條件式載入路由表
> 此 Skill **不對客戶呈現**，僅內部 SEO 專員使用

---

## 必讀（任務一律先讀）

### 來自 _shared/
1. `_shared/awoo-tone.md`
2. `_shared/seo-best-practices.md` — SEO 最佳實務（核心參考）
3. `_shared/visual-system.md`
4. `_shared/glossary.md`

### 來自本 Skill
5. `geo-tech-audit/core/master-rules.md`
6. `geo-tech-audit/core/verification-flow.md`

---

## 技術檢查項目（依任務需求讀取）

| 檢查項目 | 應讀取 |
|---------|-------|
| URL 一致性問題 | `geo-tech-audit/tech-checks/url-consistency.md` |
| H 標籤結構 | `geo-tech-audit/tech-checks/h-tags.md` |
| Schema / JSON-LD | `geo-tech-audit/tech-checks/schema-jsonld.md` |
| Canonical / noindex | `geo-tech-audit/tech-checks/canonical-noindex.md` |
| 文章新鮮度 | `geo-tech-audit/tech-checks/content-freshness.md` |

通常會用到全部 5 項。

---

## 進階情境

| 情境 | 應讀取 |
|------|-------|
| 卡關時翻歷史案例 | `geo-tech-audit/advanced/case-lessons.md` |

---

## 依客戶業態讀取

`_shared/industry-patterns.md` 對應段落

---

## 產出 HTML 時讀取

1. `geo-tech-audit/visual/html-template.md`（待補；可暫用標準模板）
2. `_shared/footer-signature.html`（內部版有微調文案）

---

## 產出檢查清單

- [ ] 區分 🔵 爬蟲事實 vs 🟡 AI 推論
- [ ] 列出所有 missing_samples、issue_samples 完整 URL
- [ ] 比對業務版健檢報告（如有），標記矛盾點
- [ ] 表格化呈現，方便逐項檢查
- [ ] 字體最小 15px
- [ ] footer 標註「僅供 awoo 內部專員執行使用」
- [ ] 內部術語可使用（harvester、RAG 等）
