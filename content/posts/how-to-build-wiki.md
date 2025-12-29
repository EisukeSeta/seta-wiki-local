# Windows Docker + Hugo Wiki + S3 + CloudFront 完全自動デプロイ構築ガイド

## 概要
Windows環境でDocker + Hugo Wikiを構築し、GitHub ActionsでAWS S3静的ウェブサイトに自動デプロイ、CloudFront + ACMでHTTPS公開する完全自動化手順です。

## 前提条件
- Windows 10/11 + Docker Desktop
- Git + GitHubアカウント
- AWSアカウント（S3、CloudFront、ACM、IAM）
- mydns.jp（または任意DDNS）アカウント

## 1. Hugo Wikiローカル環境構築

### 1.1 Hugoインストール
```powershell
# PowerShell（管理者権限）
winget install Hugo.Hugo.Extended
hugo version
```

### 1.2 新規サイト作成
```powershell
mkdir C:\wiki-project
cd C:\wiki-project
hugo new site . --force
```

### 1.3 テーマ設定（config.toml）
```toml
baseURL = "https://wiki.example.com/"
languageCode = "ja-jp"
title = "技術Wiki"
theme = "ananke"  # または任意テーマ

[params]
  description = "技術メモ・AIツール集"
```

### 1.4 初回ビルド確認
```powershell
hugo new posts/first-post.md
# content/編集後
hugo --minify
dir public  # index.html確認
```

## 2. GitHubリポジトリ連携

### 2.1 Git初期化・プッシュ
```powershell
git init
git add .
git commit -m "Initial Hugo Wiki"
git branch -M main
git remote add origin https://github.com/ユーザー名/wiki-project.git
git push -u origin main
```

### 2.2 SSHキー設定（推奨）
```powershell
ssh-keygen -t ed25519 -C "email@example.com"
# ~/.ssh/id_ed25519.pub内容をGitHub SSHキー登録
ssh -T git@github.com
```

## 3. AWS S3静的ウェブサイト設定

### 3.1 S3バケット作成
```
バケット名: wiki.example.com （ドメイン完全一致）
リージョン: us-east-1
静的ウェブサイトホスティング: 有効
インデックス: index.html
パブリックアクセスブロック: 全OFF
```

### 3.2 バケットポリシー
```json
{
  "Version": "2012-10-17",
  "Statement": [{
    "Effect": "Allow",
    "Principal": "*",
    "Action": "s3:GetObject",
    "Resource": "arn:aws:s3:::wiki.example.com/*"
  }]
}
```

### 3.3 IAMデプロイユーザー
```json
{
  "Version": "2012-10-17",
  "Statement": [{
    "Effect": "Allow",
    "Action": ["s3:PutObject*", "s3:GetObject*", "s3:DeleteObject", "s3:ListBucket"],
    "Resource": ["arn:aws:s3:::wiki.example.com", "arn:aws:s3:::wiki.example.com/*"]
  }]
}
```

## 4. GitHub Actions自動デプロイ

### 4.1 Repository Secrets設定
```
AWS_ACCESS_KEY_ID: [IAMキー]
AWS_SECRET_ACCESS_KEY: [シークレットキー]
AWS_S3_BUCKET: wiki.example.com
AWS_REGION: us-east-1
```

### 4.2 .github/workflows/deploy.yaml
```yaml
name: Deploy Hugo to S3
on:
  push:
    branches: [ main ]
jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v4
    - name: Setup Hugo
      uses: peaceiris/actions-hugo@v3
      with:
        hugo-version: '0.153.0'
    - name: Build
      run: hugo --minify
    - name: Configure AWS
      uses: aws-actions/configure-aws-credentials@v4
      with:
        aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
        aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
        aws-region: us-east-1
    - name: Deploy
      run: aws s3 sync public/ s3://${{ secrets.AWS_S3_BUCKET }}/ --delete
```

## 5. HTTPS対応（CloudFront + ACM）

### 5.1 ACMワイルドカード証明書
```
us-east-1 ACM → *.example.com + example.com
DNS検証 → mydns.jp TXTレコード2つ追加
```

### 5.2 CloudFrontディストリビューション
```
オリジン: wiki.example.com.s3-website-us-east-1.amazonaws.com
CNAME: wiki.example.com
SSL証明書: *.example.com (ACM)
価格プラン: Flat-rate Free ($0/month)
```

### 5.3 mydns.jp設定
```
wiki.example.com → d123456789.cloudfront.net
```

## 6. 運用フロー
```
1. content/編集
2. hugo --minify （任意）
3. git add . && git commit -m "Update" && git push
4. 5分後: https://wiki.example.com/即時反映
```

## 7. トラブルシューティング

| 問題 | 解決策 |
|------|--------|
| 404 NoSuchKey | `hugo --minify` → `public/`確認 → Actions再実行 |
| 403 Forbidden | S3バケットポリシー確認、CloudFrontオリジンWebsite Endpoint使用 |
| CNAMEエラー | mydns.jp CNAME → CloudFrontドメイン確認 |
| HTTPS証明書 | ACM us-east-1、DNS検証TXT2つ |

## 8. コスト最適化
```
S3: $0.023/GB（静的ファイル）
CloudFront: Flat-rate Free ($0/month, 1Mリクエスト/100GB無料)
ACM: 無料（自動更新）
合計: 個人利用なら実質無料
```

**これでDocker + Hugo + GitHub Actions + S3 + CloudFront + HTTPSの完全自動デプロイWikiが構築完了！** 🚀

[1](https://wiki.seta.mydns.jp)