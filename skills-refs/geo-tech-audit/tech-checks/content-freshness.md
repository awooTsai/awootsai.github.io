# 文章新鮮度檢查

> 詳細 SEO 標準參考 `_shared/seo-best-practices.md` §7。
> 對 AI 引擎的引用偏好詳見 `_shared/awoo-knowledge.md` §1。

---

## 1. 檢查項目

### 1.1 dateModified 同步
- Article Schema 是否含 dateModified？
- dateModified 是否與實際內容更新同步？

### 1.2 標題年份過時
- Title / H1 含「2024」「2025」等過期年份？
- 應更新到當前年份

### 1.3 內容時效性
- 文章中提到的政策、法規、價格是否過時？
- 文章中引用的數據是否仍適用？

### 1.4 內部連結失效
- 文章中連到失效頁面的內部連結？
- 連到競業已下線資源的外部連結？

---

## 2. 從 harvester 資料萃取

### Article Schema 統計
```json
{
  "article_stats": {
    "total_articles": 67,
    "with_datepublished": 65,
    "with_datemodified": 23,
    "datemodified_synced": 18,
    "datemodified_outdated": 5
  }
}
```

### 標題年份檢查
從 _rag_chunks.jsonl 的 title / h1 欄位用 regex 找：
```python
import re
year_pattern = re.compile(r'\b(202[0-4])\b')

outdated_titles = []
for chunk in chunks:
    if chunk['type'] == 'title':
        match = year_pattern.search(chunk['content'])
        if match:
            outdated_titles.append({
                'url': chunk['url'],
                'title': chunk['content'],
                'year': match.group()
            })
```

---

## 3. 報告中呈現方式

### 統計表格
```
| 指標 | 數量 | 評估 |
|------|------|------|
| Article 總數 | 67 |  |
| 有 dateModified | 23 (34%) | 🟡 偏低 |
| dateModified 同步 | 18 / 23 | 🟡 部分過時 |
| 標題含過時年份 | 12 篇 | 🟡 需更新 |
```

### 過時文章清單（展開）
```html
<details>
  <summary>標題含過時年份的 12 篇文章</summary>
  <table>
    <thead>
      <tr><th>URL</th><th>當前標題</th><th>建議新標題</th></tr>
    </thead>
    <tbody>
      <tr>
        <td><a href="...">/blog/article-1</a></td>
        <td>2024 年葉黃素推薦</td>
        <td>2026 年葉黃素推薦</td>
      </tr>
      ...
    </tbody>
  </table>
</details>
```

---

## 4. 文章更新的 Checklist（給專員）

每篇過時文章更新時：

- [ ] 修改 Title 中的年份
- [ ] H1 同步更新年份
- [ ] 更新前台顯示的日期文字
- [ ] 更新結構化資料的 `dateModified`
- [ ] H 標籤內容小幅調整
- [ ] 補充最新資訊（新產品、新研究資料）
- [ ] 確認內部連結是否仍有效
- [ ] GSC 提交 URL 要求重新索引

---

## 5. AI 偏好新鮮內容的數據

引用 `_shared/awoo-knowledge.md` §1.2：

- 90% 的 AI bot 造訪近三年內更新的內容
- AI 引用內容新鮮度高出一般 SERP 25.7%
- ChatGPT 生產設定含 `use_freshness_scoring_profile: true`

這些數據可在報告中作為「為何要持續更新」的論述依據。

---

## 6. 文章更新禁忌

### 不要單純改日期不改內容
- Google 與 LLM 判斷新鮮度時會評估是否有實質更新
- 假更新會被識別出來

### 不要頻繁假更新
- 每月修改少量段落 + 更新日期 = 合理
- 每週改 dateModified 但不改內容 = 操弄行為，可能反效果

---

## 7. 報告中與業務版的對照

業務版可能說：
> 「您的文章疑似有時效性問題」

專員版應：
- 列出全部過時文章
- 提供具體更新建議（標題、段落、Schema）
- 給優先順序（高流量文章優先更新）
