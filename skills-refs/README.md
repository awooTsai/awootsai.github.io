# awoo Skills References

> awoo 阿物科技 — 四大 Skill 共用的 references 中央倉庫
> 維護者：蔡阿達
> 部署位置：`https://awootsai.github.io/skills-refs/`

---

## 這個倉庫是什麼

這是 awoo 四個 Skill 的**共用知識中央倉庫**，所有規則、模板、產業診斷重點、視覺規範都集中在這裡。

四個 Skill 透過 `web_fetch` 從這個倉庫讀取對應的 references，達到：
- 改一份檔案 → 四個 Skill 全部受益
- 不需重新打包 Skill zip 上傳到 Claude.ai
- 任何時間都能在 GitHub 網頁上直接編輯，1 分鐘內生效

---

## 四個 Skill

| # | Skill | 用途 | SKILL.md 位置 |
|---|-------|------|--------------|
| 1 | `ada-geo-site-audit` | 業務提案版健檢（給 AE 對外用） | `geo-site-audit/SKILL.md` |
| 2 | `ada-geo-keyword-research` | 關鍵字拓展（找出客戶該操作的字） | `geo-keyword-research/SKILL.md` |
| 3 | `ada-geo-prompt-builder` | Prompt 候選清單拓展（GEO Suite 追蹤用） | `geo-prompt-builder/SKILL.md` |
| 4 | `ada-geo-tech-audit` | 專員體質健檢（內部 SEO 專員用） | `geo-tech-audit/SKILL.md` |

四個 Skill 的工作流關係：

```
客戶網站
   ↓ harvester.py 產 _rag_chunks.jsonl
   ↓
[Skill 1] 業務提案版健檢   →  AE 拜訪客戶，讓客戶感受問題
   ↓ (成案後)
[Skill 2] 關鍵字拓展        →  與客戶討論該操作哪些字
   ↓ (客戶選定關鍵字)
[Skill 3] Prompt 拓展       →  上 GEO Suite 追蹤
   ↓ (另一條線)
[Skill 4] 專員體質健檢      →  SEO 專員內部執行細節
```

---

## 目錄結構

```
skills-refs/
│
├── _shared/                      ⭐ 跨 Skill 共用內核
│   ├── awoo-tone.md              用語規則（awoo 全小寫、AE 不用 BD、台灣本土用語）
│   ├── platform-partners.md      平台合作鐵律（SHOPLINE / Shopify / 91APP / Cyberbiz / Wix）
│   ├── industry-patterns.md      各產業診斷重點（從 39 份 SEO 建議書精煉）
│   ├── seo-best-practices.md     SEO 最佳實務（Title / Description / H1 / Schema）
│   ├── visual-system.md          統一視覺規範（色系、字體、間距、動畫）
│   ├── footer-signature.html     統一兩段式 footer
│   ├── glossary.md               GEO/SEO 名詞白話解釋
│   ├── awoo-knowledge.md         可引用論述（文章新鮮度、AI 引用偏好等數據）
│   └── customer-tone.md          對客戶的口吻（您、不卑不亢、起步期上限）
│
├── geo-site-audit/               業務提案版健檢
│   ├── SKILL.md                  上傳到 Claude.ai 用的 Skill 檔
│   ├── _index.md                 路由表（依條件決定要 fetch 哪些 references）
│   ├── core/
│   ├── visual/
│   └── advanced/
│
├── geo-keyword-research/         關鍵字拓展
│   ├── SKILL.md
│   ├── _index.md
│   ├── core/
│   ├── strategies/               三波策略（順風 / 補強 / 攻堅）
│   └── visual/
│
├── geo-prompt-builder/           Prompt 拓展
│   ├── SKILL.md
│   ├── _index.md
│   ├── core/
│   ├── customer-journey/         探索 / 決策 / 品牌
│   └── visual/
│
└── geo-tech-audit/               專員體質健檢
    ├── SKILL.md
    ├── _index.md
    ├── core/
    ├── tech-checks/              逐項技術檢查清單
    └── advanced/
```

---

## 如何修改 references

### 情境 1：發現某產業新觀察點
編輯 `_shared/industry-patterns.md` 對應段落 → Commit changes → 1 分鐘後生效，四個 Skill 全部受益。

### 情境 2：要改某個 Skill 的特殊規則
編輯該 Skill 自己的 references 檔案（如 `geo-keyword-research/strategies/wave-2-reinforce.md`） → Commit changes → 1 分鐘後生效，只影響該 Skill。

### 情境 3：footer 簽名檔要更新
編輯 `_shared/footer-signature.html` → Commit changes → 四個 Skill 產出的所有報告下次都自動套新版。

### 修改方式（三選一）

**A. GitHub 網頁直接改（最舒服）**
1. 進入 [github.com/awootsai/awootsai.github.io](https://github.com/awootsai/awootsai.github.io)
2. 找到 `skills-refs/` 下對應檔案
3. 點右上角 pencil icon
4. 編輯，滑到底點 Commit changes

**B. 跟 Claude 說「幫我改 XX 檔」**
Claude 用 `web_fetch` 讀現況、產新版、你貼到 GitHub commit。

**C. Claude Code（進階）**
本地 clone repo，跟 Claude Code 互動修改 + commit + push。

---

## 部署到 GitHub Pages

1. 將整個 `skills-refs/` 資料夾 push 到 `awootsai.github.io` repo 的根目錄
2. GitHub Pages 自動服務於 `https://awootsai.github.io/skills-refs/...`
3. 各檔案的 raw URL 範例：
   - `https://awootsai.github.io/skills-refs/_shared/awoo-tone.md`
   - `https://awootsai.github.io/skills-refs/geo-site-audit/_index.md`

---

## 重要提醒

### 隱私性
這個倉庫的內容會公開可訪問（GitHub Pages 預設公開）。所以：
- ✅ 可以放：方法論、Schema 模板、觀察語句、視覺規範、產業診斷邏輯
- ❌ 不要放：客戶名單、價格策略、合約細節、客戶健檢的 raw data
- ❌ 不要放：39K 關鍵字資料庫（敏感商業資產，跟著 Skill zip 走或本地保存）

### 不要放在這裡的東西
- 客戶實際健檢產出的 HTML 報告（含客戶資料）
- 任何 PPTX / Excel 原始檔
- API key / token / 帳密
- 任何沒有公開的客戶名稱

### Skill zip 內容
四個 Skill 的 zip 檔僅需包含：
- `SKILL.md`（這份是必要的）
- 任何過大不適合放雲端的本地檔案（如 39K keyword DB）

主要邏輯透過 SKILL.md 內的 `web_fetch` URL 引用此 GitHub 倉庫。

---

## 版本控制建議

使用 GitHub 的 commit message 規範方便日後追溯：

```
[shared] 新增寵物用品產業 E-E-A-T 觀察點
[site-audit] 修正 Schema 描述的白話用語
[keyword-research] 三波策略補充競爭性評估邏輯
[prompt-builder] 新增金融業 Prompt 範例
[tech-audit] 補充 Hreflang 多語系驗證流程
```

每次 commit 一個邏輯改動，未來查問題時最快找到原因。

---

> 任何 Skill 改架構、新功能、新規則都應先回到這份 README 思考是否需要更新。
> README 是整個系統的入口指南。
