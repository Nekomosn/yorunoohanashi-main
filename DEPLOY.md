# よるのおはなしワーク デプロイガイド

## サイト構成

```
yorunoohanashi.work/          ← 本サイト（yorunowork）
yorunoohanashi.work/blog/     ← ブログ（yorunowork-blog）
```

---

## Cloudflare Pages デプロイ手順

### 1. GitHubリポジトリを作成

```bash
# 本サイト用
cd yorunowork
git init
git add .
git commit -m "Initial commit"
git remote add origin https://github.com/YOUR_USERNAME/yorunoohanashi-main.git
git push -u origin main
```

```bash
# ブログ用
cd yorunowork-blog
git add .
git commit -m "Initial commit"
git remote add origin https://github.com/YOUR_USERNAME/yorunoohanashi-blog.git
git push -u origin main
```

### 2. Cloudflare Pages でプロジェクト作成

#### 本サイト（yorunowork）
1. Cloudflare Dashboard → Pages → Create a project
2. Connect to Git → yorunoohanashi-main リポジトリを選択
3. Build settings:
   - Framework preset: `None`
   - Build command: （空欄）
   - Build output directory: `/`（ルート）
4. Deploy

#### ブログ（yorunowork-blog）
1. Cloudflare Dashboard → Pages → Create a project
2. Connect to Git → yorunoohanashi-blog リポジトリを選択
3. Build settings:
   - Framework preset: `Hugo`
   - Build command: `hugo --minify`
   - Build output directory: `public`
4. Environment variables:
   - `HUGO_VERSION`: `0.155.2`
5. Deploy

### 3. ドメイン設定

#### Cloudflare Registrar でドメイン取得
1. Cloudflare Dashboard → Registrar → Register Domain
2. `yorunoohanashi.work` を検索して購入

#### カスタムドメイン設定
1. 本サイトプロジェクト → Custom domains → Add
   - `yorunoohanashi.work`
   - `www.yorunoohanashi.work`
   
2. ブログプロジェクト → Custom domains → Add
   - `yorunoohanashi.work/blog` (サブパス)
   
   ※注：Cloudflare Pagesは同一ドメインのサブパスに別プロジェクトを割り当てられない場合があります。
   その場合は、1つのリポジトリにまとめる方法を推奨。

---

## 推奨：1つのリポジトリにまとめる

サブディレクトリ運用の場合、以下の構成を推奨：

```
yorunoohanashi-site/
├── index.html        ← 本サイト
├── about.html
├── protection.html
├── start.html
├── manual.html
├── tax.html
├── style.css
├── fonts/
└── blog/             ← Hugoでビルドした静的ファイル
    ├── index.html
    ├── posts/
    └── ...
```

### Hugoビルド後にマージ

```bash
cd yorunowork-blog
hugo --minify

# ビルド結果をコピー
cp -r public/* ../yorunowork/blog/
```

---

## URL一覧

| ページ | URL |
|--------|-----|
| トップ | https://yorunoohanashi.work/ |
| サービス詳細 | https://yorunoohanashi.work/about.html |
| 安心サポート | https://yorunoohanashi.work/protection.html |
| はじめ方 | https://yorunoohanashi.work/start.html |
| 稼働マニュアル | https://yorunoohanashi.work/manual.html |
| 税金について | https://yorunoohanashi.work/tax.html |
| ブログトップ | https://yorunoohanashi.work/blog/ |
| 記事一覧 | https://yorunoohanashi.work/blog/posts/ |
