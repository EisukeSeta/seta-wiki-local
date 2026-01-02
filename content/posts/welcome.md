---
title: "Welcome"
date: 2025-12-29T15:00:00+09:00
draft: false
---

# 最初の記事
Wiki動作確認！

# 🚀 Hugo Wiki Markdown記法

**Hugo v0.111.3 + Goldmark**対応。**table shortcode不要**・**標準記法のみ**で完璧動作。

## 基本記法

| 記法 | 例 | 結果 | Wiki用途 |
|---|---|---|---|
| **見出し** | `## 見出し2` | ## 見出し2 | 章立て |
| **太字** | `**重要**` | **重要** | 強調 |
| **斜体** | `*補足*` | *補足* | 解説 |
| **コード** | `` `hugo server` `` | `hugo server` | コマンド |
| **リンク** | `[Google](https://google.com)` | [Google](https://google.com) | 外部参照 |

## Hugo拡張記法

| 記法 | 例 | 結果 | 用途 |
|---|---|---|---|
| **タスクリスト** | `- [x] 完了`<br>`- [ ] TODO` | - [x] 完了<br>- [ ] TODO | チェックリスト |
| **脚注** | `Hugo[^1]`<br>`[^1]: 注釈` | Hugo | 詳細説明 |
| **詳細開閉** | `<details><summary>詳細</summary>内容</details>` | <details><summary>詳細</summary>内容</details> | FAQ |

## **Wiki必須：Markdownテーブル**（shortcode不要）

```markdown
| 設定 | 値 | 説明 |
|---|---|---|
| `baseURL` | `/` | ローカル |
| `draft` | `false` | 公開必須 |
| `ports` | `1313:1313` | localhost |
```

**結果**:
| 設定 | 値 | 説明 |
|---|---|---|
| `baseURL` | `/` | ローカル |
| `draft` | `false` | 公開必須 |
| `ports` | `1313:1313` | localhost |

## ブロック要素

```markdown
### コードブロック（PowerShell）
```powershell
docker compose up -d
docker compose exec hugo hugo new posts/記事.md
```

### 引用
> Hugoは最速の静的ジェネレータ
```

## **記事Frontmatter必須**
```markdown
---
title: "記事タイトル"
date: 2026-01-02
draft: false  # 公開！
---

# 記事タイトル
（本文）
```

## **hugo Wiki運用Tips**
```
1. **Ctrl+S** → **F5**（2秒反映）
2. **Ctrl+C → Enter**（3秒確実再起動）
3. `http://127.0.0.1:1313/`（localhost安定）
4. `git push` → 5分自動公開
```

## ⚠️ **注意**
- `draft: false`忘れ → 非表示
- tableは**パイプ記法のみ**（shortcode不要）
- 画像: `![alt](image.jpg)`（static/配置）

**今すぐコピペで完璧Wiki記事作成**！`http://127.0.0.1:1313/`で即プレビュー🚀