# Lucid-SRD 販売サイト

Sony Spatial Reality Display (ELF-SR2) 向けの医療用3D可視化アプリケーション「Lucid-SRD」の公式販売サイトです。

## プロジェクト概要

- **製品名**: Lucid-SRD
- **目的**: 医療用3D可視化ソリューションの販売・プロモーション
- **技術スタック**: HTML5 + Tailwind CSS (CDN) + Vanilla JavaScript

## ファイル構成

```
.
├── index.html              # メインランディングページ
├── terms.html              # 利用規約
├── tokusho.html            # 特定商取引法に基づく表記
├── privacy.html            # プライバシーポリシー
├── assets/
│   ├── images/            # 画像ファイル
│   │   ├── favicon.png
│   │   ├── logo.png
│   │   ├── hero-bg.jpg
│   │   ├── use-case-1.jpg
│   │   ├── use-case-2.jpg
│   │   ├── use-case-3.jpg
│   │   ├── ogp-image.jpg
│   │   └── twitter-image.jpg
│   ├── videos/            # 動画ファイル（将来用）
│   └── README.md          # アセット管理ガイド
├── CLAUDECODE.md          # 開発仕様書
└── README.md              # このファイル
```

## 主な機能

### ページ構成
1. **ヒーローセクション** - キャッチコピー、CTA
2. **製品特徴** - 3つの主要機能を紹介
3. **ユースケース** - 3つの活用シーン
4. **動作環境** - スペック表
5. **購入オプション** - 2プラン（ダウンロード版/USB版）
6. **FAQ** - 7項目のアコーディオン
7. **お問い合わせ** - Netlify Forms統合フォーム
8. **フッター** - 法務ページへのリンク

### JavaScript機能
- スムーススクロール
- FAQアコーディオン
- ヘッダー背景変化（スクロール時）

### SEO対策
- メタタグ（title, description, keywords）
- OGP（Facebook）対応
- Twitter Card対応
- 構造化データ（JSON-LD）
- セマンティックHTML

### お問い合わせフォーム
- **Netlify Forms**統合済み
- スパム対策内蔵
- 月100件まで無料

## Netlifyへのデプロイ手順

### 前提条件
- Gitリポジトリ（GitHub、GitLab、Bitbucket）
- Netlifyアカウント（無料）

### 手順

#### 1. Gitリポジトリの作成

```bash
cd "/Users/ootsukisatoshi/Desktop/アプリ販売サイト"

# Gitリポジトリを初期化
git init

# .gitignoreファイルを作成
echo ".DS_Store" > .gitignore
echo ".claude/" >> .gitignore

# すべてのファイルをステージング
git add .

# 初回コミット
git commit -m "Initial commit: Lucid-SRD販売サイト"
```

#### 2. GitHubにプッシュ

```bash
# GitHubで新しいリポジトリを作成してから以下を実行
git remote add origin https://github.com/YOUR_USERNAME/lucid-srd-website.git
git branch -M main
git push -u origin main
```

#### 3. Netlifyにデプロイ

1. **Netlifyにログイン**: https://app.netlify.com/
2. **「Add new site」→「Import an existing project」**をクリック
3. **GitHubを選択**してリポジトリを連携
4. **「lucid-srd-website」リポジトリ**を選択
5. **ビルド設定**:
   - Build command: （空欄のまま）
   - Publish directory: （空欄のまま）または `.`
6. **「Deploy site」**をクリック

#### 4. フォームの有効化

デプロイ後、Netlify Formsが自動的に検出されます。

- **フォーム送信の確認**: Netlifyダッシュボード → Site settings → Forms
- **通知設定**: Forms → Notifications → メール通知を設定

#### 5. カスタムドメインの設定（オプション）

1. Netlifyダッシュボード → **Domain settings**
2. **Add custom domain**をクリック
3. ドメインを入力して指示に従う
4. DNSレコードを設定

#### 6. メタタグのURL更新

デプロイ後、`index.html`のOGP/Twitter CardのURLを実際のURLに更新:

```html
<!-- 更新が必要な箇所 -->
<meta property="og:url" content="https://your-site.netlify.app/">
<meta property="og:image" content="https://your-site.netlify.app/assets/images/ogp-image.jpg">
<meta name="twitter:image" content="https://your-site.netlify.app/assets/images/twitter-image.jpg">
```

変更後、再度プッシュ:

```bash
git add index.html
git commit -m "Update OGP and Twitter Card URLs"
git push
```

Netlifyは自動的に再デプロイします。

## フォームのテスト

1. デプロイ後、サイトにアクセス
2. お問い合わせフォームに入力して送信
3. Netlifyダッシュボードの**Forms**タブで送信内容を確認
4. メール通知が設定されている場合、メールが届くことを確認

## ローカルでの確認

ブラウザで`index.html`を直接開くか、簡易サーバーを起動:

```bash
# Python 3の場合
python3 -m http.server 8000

# ブラウザで開く
open http://localhost:8000
```

**注意**: ローカル環境ではNetlify Formsは動作しません。フォーム送信機能のテストはデプロイ後に行ってください。

## 今後の拡張予定

- [ ] 決済システムの統合（Stripe等）
- [ ] ライセンスキー自動発行システム
- [ ] ブログ機能（活用事例の追加）
- [ ] 多言語対応（英語版）
- [ ] チャットボット
- [ ] Google Analytics統合

## メンテナンス

### 画像の更新
`assets/images/`フォルダ内の画像を差し替えて、Gitにプッシュ。

### コンテンツの更新
HTMLファイルを編集して、Gitにプッシュ。Netlifyが自動的に再デプロイします。

### 法務ページの更新
`terms.html`、`tokusho.html`、`privacy.html`を編集して更新日を変更。

## サポート

お問い合わせ: otuki.3104@gmail.com

## ライセンス

© 2025 Lucid-SRD. All rights reserved.
