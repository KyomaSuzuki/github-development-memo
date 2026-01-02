---
title: VS Code × GitHub でHPを作るときの開発フロー
tags:
  - GitHub
  - VSCode
  - 開発フロー
  - ホームページ制作
private: false
updated_at: '2026-01-02T15:34:20+09:00'
id: a8b004ddbfda6cd3b3d3
organization_url_name: null
slide: false
ignorePublish: false
---

## VS Code × GitHub でHPを作るときの開発フロー

## 前提

* VS CodeでHTML / CSS / JSを編集
* GitHubでリポジトリ管理
* `main` ブランチは **公開用（本番）**
* GitHub Pages を使用（`username.github.io`）

---

## ブランチ運用ルール（超重要）

* ❌ `main` で直接編集しない
* ✅ **作業ごとにブランチを切る**

```bash
main        ← 公開・安定版
feature/*  ← 各作業用ブランチ
```

---

## 基本フロー（ページ編集・追加）

### 1. 作業前に main を最新にする

```bash
git checkout main
git pull origin main
```

---

### 2. 作業用ブランチを作成

```bash
git checkout -b feature/add-works-page
```

※ 名前例

* `feature/update-top`
* `feature/add-blog-page`
* `fix/css-layout`

---

### 3. VS Codeで編集

#### 例

* HTML編集

  * `index.html`
  * `works.html`（新規作成OK）
* CSS編集

  * `stylesheet.css`
* 画像追加

  * `images/` フォルダ

💡 **mainに反映されるのはマージ後だけ**

---

### 4. 変更内容を確認

```bash
git status
git diff
```

---

### 5. コミット

```bash
git add .
git commit -m "Add works page"
```

#### コミットメッセージの例

* `Update top page layout`
* `Add profile section`
* `Fix mobile CSS`

---

### 6. GitHubに push

```bash
git push origin feature/add-works-page
```

---

### 7. Pull Request を作成

1. GitHubでリポジトリを開く
2. **Compare & pull request**
3. base: `main` ← compare: 作業ブランチ
4. Create pull request

---

### 8. マージ（公開）

* **Merge pull request**
* **Confirm merge**

🚀 → GitHub Pages が自動更新される

---

## ページ追加時の注意点

### HTMLファイルを追加

```text
index.html
works.html
about.html
```

### リンクを追加

```html
<a href="works.html">Works</a>
<a href="about.html">About</a>
```

⚠️ **相対パスを使う**

* ❌ `/works.html`
* ✅ `works.html`

---

## GitHub Pages 更新の確認

* URL: `https://ユーザー名.github.io`
* 反映まで **30秒〜数分**

---

## よくあるミスと回避策

### ❌ main で直接編集

→ 競合・事故の元
✅ 必ずブランチを切る

---

### ❌ 画像が表示されない

* ファイル名の大文字小文字
* パス間違い

```html
<img src="images/sample.png">
```

---

### ❌ pushしたのに反映されない

* main にマージしていない
* GitHub Pages のブランチ設定を確認

---

## GitHub Pages 設定確認

### Settings → Pages**

* Branch: `main`
* Folder: `/ (root)`

---

## 最小ルールまとめ（これだけ覚えればOK）

```text
1. main は触らない
2. 作業ごとにブランチ
3. PR経由で main にマージ
4. main が公開物
```

---

## おすすめファイル構成

```text
/
├─ index.html
├─ works.html
├─ about.html
├─ stylesheet.css
├─ images/
│  └─ sample.png
└─ README.md
```
