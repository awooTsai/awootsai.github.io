# awoo Skills References — GitHub 部署教學

> 本教學帶你把 47 份 references 檔案部署到 `awootsai.github.io`，讓四個 Skill 透過 `web_fetch` 讀取。

---

## 第一階段：部署到 GitHub Pages（一次性，約 10 分鐘）

### Step 1：解壓 ZIP 檔

下載 `awoo-skills-refs.zip` 後解壓，會看到：
```
skills-refs/
├── README.md
├── _shared/                  (9 份檔案)
├── geo-site-audit/           (8 份檔案)
├── geo-keyword-research/     (8 份檔案)
├── geo-prompt-builder/       (7 份檔案)
└── geo-tech-audit/           (10 份檔案)
```

### Step 2：上傳到 awootsai.github.io repo

#### 方式 A：GitHub 網頁直接拖拉（最簡單）

1. 開啟 https://github.com/awootsai/awootsai.github.io
2. 點 `Add file` → `Upload files`
3. 將解壓後的整個 `skills-refs` 資料夾**拖拉到頁面**
4. 滑到底，輸入 commit message：
   ```
   Add skills-refs/ for ada-geo-* Skills
   ```
5. 點 `Commit changes`

#### 方式 B：用 git 指令（如已熟悉）

```bash
cd ~/Dropbox/antigravity/awootsai.github.io   # 或你的本地 clone 位置
unzip ~/Downloads/awoo-skills-refs.zip
git add skills-refs/
git commit -m "Add skills-refs/ for ada-geo-* Skills"
git push
```

### Step 3：等 1-2 分鐘，GitHub Pages 自動部署

部署完成後，以下 URL 應該可以開啟：
- https://awootsai.github.io/skills-refs/README.md
- https://awootsai.github.io/skills-refs/_shared/awoo-tone.md
- https://awootsai.github.io/skills-refs/geo-site-audit/SKILL.md
- ...（依此類推）

打開任一個 URL 確認可開啟，就代表部署成功。

---

## 第二階段：上傳 Skill 到 Claude.ai（每個 Skill 各一次）

四個 Skill 各自打包成 zip 上傳。每個 zip 內**只有 SKILL.md 一個檔案**（references 已在 GitHub）。

### Step 1：建立 4 個 Skill zip

```bash
cd ~/Downloads/skills-refs

# Skill 1
mkdir -p ada-geo-site-audit
cp geo-site-audit/SKILL.md ada-geo-site-audit/
zip -r ada-geo-site-audit.zip ada-geo-site-audit/

# Skill 2
mkdir -p ada-geo-keyword-research
cp geo-keyword-research/SKILL.md ada-geo-keyword-research/
# 如有 awoo_keywords.db,放進此資料夾
# cp /path/to/awoo_keywords.db ada-geo-keyword-research/references/
zip -r ada-geo-keyword-research.zip ada-geo-keyword-research/

# Skill 3
mkdir -p ada-geo-prompt-builder
cp geo-prompt-builder/SKILL.md ada-geo-prompt-builder/
zip -r ada-geo-prompt-builder.zip ada-geo-prompt-builder/

# Skill 4
mkdir -p ada-geo-tech-audit
cp geo-tech-audit/SKILL.md ada-geo-tech-audit/
zip -r ada-geo-tech-audit.zip ada-geo-tech-audit/
```

### Step 2：上傳到 Claude.ai

1. 開啟 Claude.ai → Settings → Capabilities → Skills
2. 點「Upload Skill」
3. 選擇 zip 檔（如 `ada-geo-site-audit.zip`）
4. 等待上傳成功
5. 重複步驟 3-4，上傳全部 4 個 zip

> **注意**：v8 新版本與舊版本（如 v7.0）會在 Skill 列表並存。建議：
> - 先測試新版本沒問題
> - 確認沒問題後，再刪除舊版本
> - 避免觸發詞衝突

---

## 第三階段：測試新版 Skill

### 測試 Skill 1：業務提案版健檢

開新對話，輸入：
> 「請對 awoo.ai 做網站健檢」

預期：
- Claude 會 web_fetch GitHub 上的 references
- 可能出現「Reading https://awootsai.github.io/skills-refs/_shared/awoo-tone.md」等訊息
- 最終產出 HTML 報告

### 測試 Skill 2：關鍵字拓展

```
「幫我為 awoo.ai 拓展 GEO 關鍵字」
```

### 測試 Skill 3：Prompt 拓展

```
「幫我把這些關鍵字延伸成 Prompt 候選池：
- GEO
- 生成式引擎優化
- AI 優化
（每組要 6 條，共 18 條候選）」
```

### 測試 Skill 4：專員體質健檢

```
「請對 awoo.ai 做專員版技術盤點」
```

---

## 修改 references 的日常工作流

### 情境 A：發現新觀察點

例：發現新產業「寵物用品」的特別觀察。

1. 開啟 https://github.com/awootsai/awootsai.github.io
2. 找到 `skills-refs/_shared/industry-patterns.md`
3. 點右上角 ✏ pencil icon
4. 在檔案中新增 `## §X 寵物用品類` 段落
5. 滑到底，輸入 commit message：
   ```
   [shared] 新增寵物用品產業診斷重點
   ```
6. 點 `Commit changes`
7. 等 1 分鐘，下個對話 Claude 自動讀到新版

### 情境 B：footer 簽名檔要更新

1. 編輯 `skills-refs/_shared/footer-signature.html`
2. Commit message：
   ```
   [shared] footer 文案更新 v2026-06-XX
   ```
3. 四個 Skill 產出的所有報告下次都自動套新版

### 情境 C：要改某個 Skill 的特殊規則

例：geo-keyword-research 的選字規則調整。

1. 編輯 `skills-refs/geo-keyword-research/core/selection-rules.md`
2. Commit message：
   ```
   [keyword-research] 調整選字字數上限規則
   ```
3. 只影響 `ada-geo-keyword-research` Skill

---

## 修改技巧：跟 Claude 一起改

如果你想跟 Claude 討論該改什麼，操作流程：

1. 開新對話，跟 Claude 說：
   > 「我要更新 industry-patterns.md，先 web_fetch 現況：
   > https://awootsai.github.io/skills-refs/_shared/industry-patterns.md」

2. Claude 讀完後跟你討論該改什麼

3. Claude 產出新版完整內容

4. 你複製到 GitHub web 編輯器，commit

5. 完成。下個對話自動套用。

---

## 常見問題

### Q1：web_fetch 失敗怎麼辦？

可能原因：
- GitHub Pages 還沒部署完成 → 等 1-2 分鐘
- URL 拼錯 → 確認檔案路徑
- 檔名 ASCII 錯誤 → 檢查是否有中文檔名

### Q2：要把舊版 Skill（v7.0）刪除嗎？

建議流程：
1. 上傳新版 v8（觸發詞不同：「全新健檢」vs 舊版的「健檢」）
2. 用 v8 測試 1-2 週
3. 確認沒問題後，再刪除舊版

### Q3：43K 關鍵字 DB 該放哪？

`awoo_keywords.db` 是商業資產，**不該放 GitHub Pages**。

放在本地，跟著 `ada-geo-keyword-research` Skill zip 走：
```
ada-geo-keyword-research/
├── SKILL.md
└── references/
    └── awoo_keywords.db
```

Skill 觸發時，Claude 會在本地讀取此 DB。

### Q4：可以讓同仁用嗎？

理論上可以——但建議先：
1. 自己用 1-2 週確認穩定
2. 寫一份「同仁使用手冊」
3. 找 Aiden（高雄 AE）做種子用戶測試
4. 確認沒問題後再擴展給其他 AE

詳細考量見之前對話討論的「組織化部署」章節。

### Q5：未來要新增第 5 個 Skill 怎麼辦？

加 Skill 的標準流程：
1. 在 `skills-refs/` 下新增 `[新 Skill 名稱]/` 資料夾
2. 建立 SKILL.md、_index.md、core/ 等子檔
3. 引用既有的 `_shared/` 共用內核
4. push 到 GitHub
5. 上傳新 Skill zip 到 Claude.ai

`_shared/` 設計上就是為了多 Skill 共用，所以擴展極為簡單。

---

## 隱私與安全

### GitHub Pages 是公開的

`awootsai.github.io/skills-refs/...` 任何人都可以打開。所以：

✅ 可以放：方法論、Schema 模板、視覺規範、產業診斷邏輯
❌ 不要放：客戶名單、價格策略、合約細節、實際健檢資料

### 模糊路徑保護（額外保險）

如果想增加一層保護，可以重新命名資料夾為較難猜測的名稱：

```
skills-refs/        → 改為 awoo-int-x9k2m7p/
```

對應地，所有 SKILL.md 的 web_fetch URL 也要同步修改。

但這層保護是「security through obscurity」，不要過度依賴。

---

## 最後提醒

1. **測試完整流程一次**：上傳 → 等部署 → 測試 4 個 Skill 都能跑
2. **記下 GitHub Pages URL**：`https://awootsai.github.io/skills-refs/`
3. **建立修改習慣**：每次改 references 用 `[scope] 簡述` 格式 commit
4. **保留版本歷史**：未來查問題時最快找到原因

完成這套部署後，未來任何 references 修改都不需要重新打包 Skill zip 上傳。

🎉 恭喜完成 awoo Skill GitHub 化架構！
