# awoo_keywords.db 整合邏輯

> 過去 awoo 為 600+ 客戶累積的審字表資料庫。
> 本檔案說明如何在拓字 Skill 中善用這份歷史資產。

---

## 1. 資料庫位置

`awoo_keywords.db` 是 SQLite 格式，跟著 Skill zip 走（不放雲端，是 awoo 內部商業資產）。

預期路徑：
```
ada-geo-keyword-research/
├── SKILL.md
└── references/
    └── awoo_keywords.db    ← SQLite, ~39K keywords, 600+ clients
```

---

## 2. 資料庫結構（建議）

> 確切結構需阿達確認，以下為建議標準格式：

```sql
-- 核心表
CREATE TABLE keywords (
  id INTEGER PRIMARY KEY,
  keyword TEXT NOT NULL,
  search_volume INTEGER,
  industry TEXT,
  client_id INTEGER,
  recommended_date DATE,
  recommended_by TEXT,
  topic TEXT,
  notes TEXT
);

CREATE TABLE clients (
  id INTEGER PRIMARY KEY,
  name TEXT,
  industry TEXT,
  url TEXT,
  first_engagement DATE
);

CREATE INDEX idx_keyword ON keywords(keyword);
CREATE INDEX idx_industry ON keywords(industry);
CREATE INDEX idx_topic ON keywords(topic);
```

---

## 3. 整合工作流程

### Step 1：識別客戶業態
從 `_claude_briefing.md` 與 `pages.zip` 判斷業態（電商、金融、服務型等）。

### Step 2：查詢 DB 歷史資料

```python
import sqlite3

# 載入 DB
conn = sqlite3.connect('references/awoo_keywords.db')
cursor = conn.cursor()

# 查詢 1：同業態的歷史推薦字
cursor.execute("""
    SELECT keyword, search_volume, COUNT(*) as recommend_count
    FROM keywords
    WHERE industry = ?
    GROUP BY keyword
    ORDER BY recommend_count DESC, search_volume DESC
    LIMIT 100
""", ('保健食品',))

# 查詢 2：特定主題的歷史推薦字
cursor.execute("""
    SELECT keyword, search_volume
    FROM keywords
    WHERE topic LIKE ? AND industry = ?
    ORDER BY search_volume DESC
""", ('%葉黃素%', '保健食品'))
```

### Step 3：合併新舊候選池

```
歷史推薦字（有信任基礎，但可能過時）
   +
即時 web_search 補充（捕捉當前趨勢）
   =
完整候選池
```

### Step 4：標註來源

報告中每個關鍵字應標註：
- 🔵 **歷史推薦字**：awoo 過去對相關客戶推薦過
- 🟢 **新趨勢字**：基於 2026 即時搜尋補充
- ⚪ **既有內容字**：客戶網站已有對應內容

---

## 4. DB 查詢的常見模式

### 4.1 同業態的「熱門推薦字」TOP 30

```sql
SELECT keyword, AVG(search_volume) as avg_sv, COUNT(*) as freq
FROM keywords
WHERE industry = '保健食品'
GROUP BY keyword
HAVING freq >= 3
ORDER BY freq DESC, avg_sv DESC
LIMIT 30;
```

意義：被多個客戶推薦過的字，是該業態的「兵家必爭字」。

### 4.2 客戶歷史拓字進化

```sql
-- 同一客戶的歷史拓字字
SELECT keyword, recommended_date, search_volume
FROM keywords
WHERE client_id = ?
ORDER BY recommended_date DESC;
```

意義：看出客戶過去走過的路、避開重複推薦。

### 4.3 主題字的搜量趨勢

```sql
SELECT 
  STRFTIME('%Y-%m', recommended_date) as month,
  AVG(search_volume) as avg_sv
FROM keywords
WHERE keyword LIKE '%葉黃素%'
GROUP BY month
ORDER BY month;
```

意義：看主題字的搜量是上升還是下降。

---

## 5. 隱私與合規

### 不可在報告中暴露
- 其他客戶實名
- 其他客戶的拓字明細
- 報價金額或合約細節

### 可以呈現
- 「awoo 過去輔導同業時，[XX 主題] 是常見的高搜量字」
- 「在 [業態] 領域，[XX 字] 累計被推薦多次，是核心競爭字」

### 客戶看到的標準說法

> 「awoo 累積近 20 年、600+ 客戶的審字資料庫，本次為您拓展的關鍵字結合了：
> - 過去同業客戶被驗證有效的字
> - 2026 年最新搜尋趨勢
> - 您網站既有內容對應的字」

---

## 6. DB 查詢失敗的 fallback

如果 DB 不可用（檔案損壞、缺失等）：

1. 不要直接報錯讓使用者看到
2. 改用純 web_search 補充候選池
3. 報告中說明「本次拓字以即時搜尋資料為主」（不提 DB 失敗）
4. 內部 log 記錄問題，回報阿達

---

## 7. DB 維護建議

### 定期更新（建議每季）
- 新增客戶的拓字結果寫回 DB
- 清理過時的字（超過 3 年無人推薦的字標記為 deprecated）
- 標註失效的關鍵字（如品牌已下市）

### 質量管控
- 不要把 client 內部測試字寫進 DB
- 不要把已被剔除的字寫進 DB
- 維持 keyword + industry + topic 三軸的整潔

---

## 8. 與 ada-geo-prompt-builder 的接力

關鍵字拓出來後，下一步是進入 Prompt 拓展：
- 客戶從拓字報告中**選定 N 個關鍵字**
- 進入 `ada-geo-prompt-builder` Skill
- 系統按客戶選定的字 × 4-7 條 Prompt = 候選池
- 客戶再從候選池選最終 90 條（或其他客戶定數）

DB 整合應為這個接力做好準備：
- 拓字報告中的關鍵字都需有可被選取的 ID
- 客戶選定後，可直接帶入下一個 Skill
