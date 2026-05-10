# geo-site-audit references 路由索引

> 業務提案版健檢 — 條件式載入路由表
> 讀完此索引後，依任務情境條件式 web_fetch 對應檔案。

---

## 必讀（任務一律先讀，依此順序）

### 來自 _shared/（共用內核）
1. `_shared/awoo-tone.md` — 用語規則
2. `_shared/customer-tone.md` — 對客戶口吻
3. `_shared/platform-partners.md` — 平台合作鐵律
4. `_shared/visual-system.md` — 視覺規範
5. `_shared/glossary.md` — 名詞解釋
6. `_shared/awoo-knowledge.md` — 可引用論述

### 來自本 Skill
7. `geo-site-audit/core/master-rules.md` — 核心規則
8. `geo-site-audit/core/observation-lib.md` — 觀察語句庫

---

## 依客戶業態擇一讀取

從 `_claude_briefing.md` 與 `pages.zip` 樣本判斷業態：

| 客戶業態 | 對應段落 |
|---------|---------|
| 電商 / 服飾 / 包袋 / 美妝 / 食品 | `_shared/industry-patterns.md` §1 |
| 金融 / 保險 / 投資 / 銀行 / 外匯 | `_shared/industry-patterns.md` §2 |
| 律師 / 醫師 / 會計師 / 顧問 / 教育機構 | `_shared/industry-patterns.md` §3 |
| 中古車 / 媒合平台 | `_shared/industry-patterns.md` §4 |
| 日文網站 | `_shared/industry-patterns.md` §5 |

---

## 進階情境（特定觸發才讀）

| 觸發情境 | 應讀取的檔案 |
|---------|-----------|
| 客戶提供 Ahrefs AIO CSV | `geo-site-audit/advanced/aio-visibility.md` |
| 多事業單位網站（≥3 個 URL） | `geo-site-audit/advanced/multi-bu-mode.md` |
| 卡關時翻歷史案例 | `geo-site-audit/advanced/case-lessons.md` |

---

## 產出 HTML 報告時讀取

1. `geo-site-audit/visual/html-template.md` — HTML 結構模板
2. `geo-site-audit/visual/design-tokens.md` — 視覺微調
3. `_shared/footer-signature.html` — 統一 footer

---

## 報告產出檢查清單

產出前必確認：
- [ ] 字體最小 15px（含 inline style）
- [ ] awoo 全小寫
- [ ] 對客戶用「您」
- [ ] 起步期評估上限 🌱
- [ ] 三大痛點以「內容層」優先
- [ ] 每個 URL 已 web_fetch 驗證
- [ ] cross-canonical 排除尾斜線誤報
- [ ] 內部術語（harvester/RAG）未出現
- [ ] 技術縮寫第一次出現有白話括號
- [ ] 平台合作鐵律未違反（SHOPLINE 等）
- [ ] footer 兩段式格式正確
