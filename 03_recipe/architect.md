# 設計仕様書（Architect.md）：【入門編】レシピサイト（トップページ）

## 1. プロジェクト概要・完成仕様

本プロジェクトは、ファーストビューでの全画面表示（`100vh`）、CSSの `calc()` 関数による正確な3分割レイアウト、画像下隙間の消去（`vertical-align: bottom;`）、ボタンデザイン、およびSNSリストのレイアウトを習得するための**モダンなレシピダイアリーWEBサイト**です。

### 基本仕様パラメータ
* **ファーストビュー高さ**: `height: 100vh;`（ビューポート縦幅いっぱい）
* **アスペクト比保護位置**: `object-fit: cover;` ＋ `object-position: center top;`
* **3分割画像グリッド**: `width: calc(100% / 3);`
* **レスポンシブ・ブレイクポイント**: `834px`（834px以下で3分割画像を1列縦積みへ切替）
* **リセットCSS**: `ress.min.css`

---

## 2. ディレクトリ構造

```
03_recipe/
 ├── architect.md             # 本設計仕様書
 ├── sample/                  # 模範解答用
 │    ├── index.html
 │    ├── css/style.css
 │    └── img/ (mainvisual.jpg, recipe1.jpg ~ 3.jpg, favicon.ico)
 └── practice/                # 写経・練習用スターター
      ├── index.html
      ├── css/style.css
      └── img/
```

---

## 3. HTML構造設計とタグ選定の根拠

| セクション / 要素 | 使用タグ | クラス / ID | タグ選定の根拠・意図 |
| :--- | :--- | :--- | :--- |
| **メイン枠** | `<main>` | `-` | ページの主たるコンテンツエリアを包括。 |
| **タイトル・説明** | `<div>` > `<h1>` + `<p>` | `.text`, `.site-title` | トップページのタイトルとして `h1` を指定。テキスト全体を中央寄せ用に `.text` でグループ化。 |
| **3連ギャラリー** | `<ul>` > `<li>` > `<img>` | `.flex` | 3枚のレシピ写真の集合であるためリスト構造 `ul/li` を使用。Flexbox用に `.flex` クラス付与。 |
| **ボタン** | `<a>` | `.btn` | ページ移動リンクのため `a` タグを使用。CSSでインラインブロック化し枠線付きボタンへ装飾。 |
| **SNSリンク** | `<ul>` > `<li>` > `<a>` | `.sns` | SNSアカウント集という共通の意味を持つリンク群のためリスト構造でアクセシブルに管理。 |

---

## 4. CSSスタイル設計 ＆ ピュアCSSテクニック解説

### 1) 全画面ヒーローイメージ (`height: 100vh;` ＋ `object-position`)
```css
#mainvisual img {
  width: 100%;
  height: 100vh;
  object-fit: cover;
  object-position: center top;
  margin-bottom: 80px;
}
```
* **ポイント**: 画面全高にフィットさせつつ、`object-position: center top;` で料理写真の上の美味しそうな部分を中心にトリミング保持します。

### 2) `calc()` 関数による正確な 3等分幅計算
```css
.flex li {
  width: calc(100% / 3);
}
```
* **ポイント**: 手動で `33.33%` と書く代わりに `calc(100% / 3)` を使うことで、ブラウザが端数まで精密に1/3幅を計算し隙間なくピッタリ横並びさせます。

### 3) 画像下のベースライン隙間消去 (`vertical-align: bottom;`)
```css
.flex li img {
  width: 100%;
  height: 500px;
  object-fit: cover;
  vertical-align: bottom;
}
```
* **ポイント**: `img` はインライン要素のため下部に数pxのベースライン隙間が発生します。`vertical-align: bottom;` で画像下端を揃えて隙間を完全に消します。

### 4) `a` タグのボタンデザイン (`display: inline-block;`)
```css
.text .btn {
  display: inline-block;
  border: solid 1px #2b2a27;
  font-size: 0.875rem;
  padding: 18px 60px;
  text-decoration: none;
}
```
* **ポイント**: インライン要素の `a` タグに `display: inline-block;` を付与することで、上下パディング（18px）やボーダーが正常に効くようになりボタン化します。

---

## 5. レスポンシブ設計仕様 (`@media screen and (max-width: 834px)`)

```css
@media screen and (max-width: 834px) {
  .flex {
    flex-direction: column;
  }
  .flex li {
    width: 100%;
  }
}
```
* タブレット以下（834px）で `flex-direction: column;` に切り替え、3枚の画像を1列縦積みに変更します。
