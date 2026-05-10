# 平台合作夥伴鐵律

> awoo 與多個電商平台是合作夥伴關係，所有對外文案必須遵守此規則。
> 違反此規則的報告**不可輸出**。

---

## 1. 合作平台清單（所有 Skill 通用）

awoo 與以下平台是合作夥伴：

- **SHOPLINE**
- **Shopify**
- **91APP**
- **Cyberbiz**
- **Wix**

未來新增的合作平台請阿達直接編輯此檔案加入清單。

---

## 2. 對這些平台的措辭禁忌

### 禁忌 1：不可暗示平台是問題來源
- ❌ 「您網站使用 SHOPLINE 平台，所以無法做 X 優化」
- ❌ 「Shopify 預設限制了 SEO 表現」
- ❌ 「91APP 平台本身的 SEO 結構較弱」

### 禁忌 2：不可寫「awoo 與 XX 共創」
- ❌ 「awoo 與 SHOPLINE 共同打造的 GEO 解決方案」
- ❌ 「awoo × Shopify 聯名服務」
- ❌ 「嘉惠所有 91APP 商家」

### 禁忌 3：不可暗示「找 awoo = 補足平台不足」
- ❌ 「找 awoo 顧問可彌補 Cyberbiz 在 GEO 上的弱項」
- ❌ 「Wix 客戶必須透過 awoo 才能突破限制」

---

## 3. 正確措辭

### awoo 角色定位
僅可寫「對該客戶提供工具/服務」：

- ✅ 「awoo 可為您提供針對網站體質的 GEO 優化建議」
- ✅ 「awoo 顧問團隊將協助您規劃 GEO 內容方向」
- ✅ 「awoo 將為您提供 GEO Suite 工具的追蹤服務」

### 平台中立化
- ✅ 「您目前網站的 H1 設定疑似有可優化空間」（直接描述客戶網站狀況，不提平台）
- ✅ 「建議檢視 Title 多樣性，提升 AI 對各頁差異化特色的辨識」（描述優化方向，不提平台）

---

## 4. 各平台技術判斷的注意事項

### SHOPLINE
- liquid template 渲染（`Rendered '*.liquid'`、`{{ ... | translate }}` 等特徵）= SHOPLINE 確認
- URL slug 格式單獨判斷不夠，必須結合 HTML 結構特徵
- 自動產生 sitemap，不應寫「缺少 sitemap」
- 產品頁、分類頁、文章頁有固定模板限制——這些是「平台共通特性」，不是「客戶網站問題」

### Shopify
- `/products/`、`/collections/`、`/blogs/`、`/pages/` 標準路徑
- 一般具備自動 canonical、自動 robots.txt
- 若發現 cross-canonical，先確認是否為 Shopify 自動產生的合理規則

### 91APP
- 商品 URL 含特定參數，分類頁結構穩定
- 部分功能與 SHOPLINE 類似

### Cyberbiz
- 部分功能與 SHOPLINE 類似
- 商品頁、分類頁有固定模板限制

### Wix
- URL 結構與其他平台差異較大
- 部分技術 SEO 限制較多
- 動態渲染較重，AI 爬蟲讀取需注意

---

## 5. 平台識別的判斷流程

判斷平台時，**不能單憑 URL slug 格式就下結論**。應同時觀察：

1. **URL 路徑模式**
2. **模板渲染方式**（liquid / Vue / React）
3. **HTML 結構特徵**（class 命名習慣）
4. **robots.txt 內容**
5. **Schema 自動生成模式**

確認多個證據才下平台判斷。

---

## 6. 健檢報告中提到平台的標準寫法

如果報告中必須提到平台名稱：

### 中性陳述
> 「您的網站採用 SHOPLINE 平台，這是台灣常見的電商解決方案。基於 SHOPLINE 的固定模板特性，部分頁面結構可在範圍內進行 GEO 優化。」

### 不寫批評，只寫機會
> 「在 SHOPLINE 平台的範圍內，可優化的方向包括 [Title 多樣性 / FAQ Schema / 文章內部連結結構] 等。」

### 不寫平台限制當問題
- ❌ 「SHOPLINE 平台無法調整 X，這是個問題」
- ✅ 「在現有平台範圍內，可優先處理的優化機會包括 [...]」

---

## 7. 違反此規則的後果

如果報告草稿中出現以下內容，**必須修正後才可輸出**：
- 暗示平台是問題來源
- 提到「awoo × 平台共創」
- 寫「補足平台不足」
- 對平台架構作負面評價

阿達會親自檢核此規則。Skill 產出時應自我審查。

---

## 8. 平台合作關係的更新

未來若有新增合作平台，或合作關係變更，請阿達編輯本檔案：
- `https://github.com/awootsai/awootsai.github.io/blob/main/skills-refs/_shared/platform-partners.md`

更新後 1 分鐘內，四個 Skill 自動套用最新規則。
