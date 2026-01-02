---
title: "Welcome"
date: 2026-01-02T15:00:00+09:00
draft: false
---

# 最初の記事


# 🚀 Hugo Wiki Markdown記法

**Hugo v0.111.3 + Goldmark**対応。**table shortcode不要**・**標準記法のみ**で完璧動作。

```markdown
---
title: "🚀 Hugo Wiki Markdown完全ガイド"
date: 2026-01-02
draft: false
---

# Hugo Wiki Markdown記法（Goldmark拡張）

**Hugo v0.111.3対応・table shortcode不要**。**コピペ即使用可**。

## 📋 基本記法
| 記法 | 表記 | 例 | 結果 | Wiki用途 |
|---|---|---|---|---|
| **見出し** | `# H1`〜`###### H6` | `## 見出し2` | ## 見出し2 | 章立て |
| **太字** | `**bold**` | `**重要**` | **重要** | 強調 |
| **斜体** | `*italic*` | `*補足*` | *補足* | 解説 |
| **打ち消し** | `~~del~~` | `~~削除~~` | ~~削除~~ | 差分 |
| **インラインコード** | `` `code` `` | `` `hugo server` `` | `hugo server` | コマンド |
| **キーボード** | `<kbd>Ctrl+C</kbd>` | `<kbd>Ctrl+C</kbd>` | <kbd>Ctrl+C</kbd> | 操作 |

## ✨ Hugo拡張記法
| 記法 | 表記 | 例 | 結果 | 用途 |
|---|---|---|---|---|
| **タスクリスト** | `- [ ] / - [x]` | `- [ ] TODO`<br>`- [x] 完了` | - [ ] TODO<br>- [x] 完了 | チェックリスト |
| **脚注** | `[^1]`<br>`[^1]:注釈` | `Hugo[^1]` | Hugo[^1] | 詳細説明 |
| **定義リスト** | `用語`<br>`: 説明` | `Hugo`<br>`: SSG` | <dl><dt>Hugo</dt><dd>SSG</dd></dl> | 用語集 |
| **詳細開閉** | `<details>` | `<details><summary>詳細</summary>内容</details>` | <details><summary>詳細</summary>内容</details> | FAQ |

## 📊 **Markdownテーブル**（shortcode不要）
'```markdown'
| 設定 | 値 | 説明 |
|---|---|---|
| `baseURL` | `/` | ローカル開発 |
| `draft` | `false` | 公開必須 |
| `ports` | `1313:1313` | localhost |
'```'

## 💻 ブロック要素

'```markdown'
### コードブロック
'```powershell'
docker compose up -d
docker compose exec hugo hugo new posts/記事.md
git push  # 5分公開
'```'

### 引用
> Hugoは最速の静的サイトジェネレータ

## 🎯 **記事Frontmatter必須**
'```markdown'
***
title: "記事タイトル"
date: 2026-01-02
draft: false  # 公開！
***

# 記事タイトル

本文...
'```'

## ⚙️ **運用コマンド表**
| 手順 | コマンド | 結果 |
|---|---|---|
| 1 | `docker compose up -d` | コンテナ起動 |
| 2 | `hugo new posts/記事.md` | 新規記事 |
| 3 | **Ctrl+S** → **F5** | 即反映（2秒） |
| 4 | **Ctrl+C** → **Enter** | 確実再起動（3秒） |
| 5 | `git push` | 5分自動公開 |

## 🚨 **必須注意点**
| 注意 | 対処 |
|---|---|
| `draft: true` | `draft: false`に変更 |
| `localhost`繋がらない | `127.0.0.1:1313`使用 |
| 即反映なし | F5 / 3秒再起動 |
| table壊れ | **パイプ記法のみ**使用 |
| 画像| `![alt](image.jpg)`（static/配置）|


**参考**: [Hugo公式](https://gohugo.io/content-management/markdown/)

**これでSeta Wiki完全Markdown運用**！**コピペ→Ctrl+S→F5**で即プレビュー🚀、**127.0.0.1:1313**で確認！
```

**結果**:
## 📋 基本記法
| 記法 | 表記 | 例 | 結果 | Wiki用途 |
|---|---|---|---|---|
| **見出し** | `# H1`〜`###### H6` | `## 見出し2` | ## 見出し2 | 章立て |
| **太字** | `**bold**` | `**重要**` | **重要** | 強調 |
| **斜体** | `*italic*` | `*補足*` | *補足* | 解説 |
| **打ち消し** | `~~del~~` | `~~削除~~` | ~~削除~~ | 差分 |
| **インラインコード** | `` `code` `` | `` `hugo server` `` | `hugo server` | コマンド |
| **キーボード** | `<kbd>Ctrl+C</kbd>` | `<kbd>Ctrl+C</kbd>` | <kbd>Ctrl+C</kbd> | 操作 |

## ✨ Hugo拡張記法
| 記法 | 表記 | 例 | 結果 | 用途 |
|---|---|---|---|---|
| **タスクリスト** | `- [ ] / - [x]` | `- [ ] TODO`<br>`- [x] 完了` | - [ ] TODO<br>- [x] 完了 | チェックリスト |
| **脚注** | `[^1]`<br>`[^1]:注釈` | `Hugo[^1]` | Hugo[^1] | 詳細説明 |
| **定義リスト** | `用語`<br>`: 説明` | `Hugo`<br>`: SSG` | <dl><dt>Hugo</dt><dd>SSG</dd></dl> | 用語集 |
| **詳細開閉** | `<details>` | `<details><summary>詳細</summary>内容</details>` | <details><summary>詳細</summary>内容</details> | FAQ |

## 📊 **Markdownテーブル**（shortcode不要）
| 設定 | 値 | 説明 |
|---|---|---|
| `baseURL` | `/` | ローカル開発 |
| `draft` | `false` | 公開必須！ |
| `ports` | `1313:1313` | localhost必須 |

## 💻 ブロック要素
```markdown
### コードブロック
```powershell
docker compose up -d
docker compose exec hugo hugo new posts/記事.md
git push  # 5分公開
```

### 引用
> Hugoは最速の静的サイトジェネレータ


## 🎯 **記事Frontmatter必須**
```markdown
***
title: "記事タイトル"
date: 2026-01-02
draft: false  # 公開！
***

# 記事タイトル

本文...
```

## ⚙️ **運用コマンド表**
| 手順 | コマンド | 結果 |
|---|---|---|
| 1 | `docker compose up -d` | コンテナ起動 |
| 2 | `hugo new posts/記事.md` | 新規記事 |
| 3 | **Ctrl+S** → **F5** | 即反映（2秒） |
| 4 | **Ctrl+C** → **Enter** | 確実再起動（3秒） |
| 5 | `git push` | 5分自動公開 |

## 🚨 **必須注意点**
| 注意 | 対処 |
|---|---|
| `draft: true` | `draft: false`に変更 |
| `localhost`繋がらない | `127.0.0.1:1313`使用 |
| 即反映なし | F5 / 3秒再起動 |
| table壊れ | **パイプ記法のみ**使用 |
| 画像| `![alt](image.jpg)`（static/配置）|


**参考**: [Hugo公式](https://gohugo.io/content-management/markdown/)

**これでhugo Wiki完全Markdown運用**！**コピペ→Ctrl+S→F5**で即プレビュー🚀、**127.0.0.1:1313**で確認！
