# 設計仕様書（Architect.md）：【初級編】ストアサイト（書店「Mag88」）

## 1. プロジェクト概要・完成仕様

本プロジェクトは、`position: absolute;` による背景画像上のテキストオーバーレイ、擬似要素 `::before` を用いたフッター箇条書きリストの装飾、並びに背景画像セクション（`height: 100vh;`, `height: 520px;`）の構築を習得するための**高クオリティな雑誌オンラインストアWEBサイト**です。

### 基本仕様パラメータ
* **コンテンツ最大幅 (`.wrapper`)**: `1200px`（左右パディング `5%`）
* **ヒーローヘッダー**: 背景画像 ＋ 高さ `100vh` ＋ 右上絶対配置ロゴ (`position: absolute; top: 30px; right: 30px;`)
* **カード内テキストオーバーレイ**: `position: absolute; top: 40%;` ＋ 半透明黒背景 `rgba(0, 0, 0, 0.5)`
* **レスポンシブ・ブレイクポイント**: `896px`（896px以下でスマホ縦積みレイアウト切替）
* **リセットCSS**: `ress.min.css`

---

## 2. ディレクトリ構造

```
06_store1/
 ├── architect.md             # 本設計仕様書
 ├── sample/                  # 模範解答用
 │    ├── index.html
 │    ├── css/style.css
 │    └── img/ (mainvisual.jpg, fashion.jpg, catalog.jpg, antique.jpg, magazine-archive.jpg, etc.)
 └── practice/                # 写経・練習用スターター
      ├── index.html
      ├── css/style.css
      └── img/
```

---

## 3. HTML構造設計とタグ選定の根拠

| セクション / 要素 | 使用タグ | クラス / ID | タグ選定の根拠・意図 |
| :--- | :--- | :--- | :--- |
| **ヒーローヘッダー** | `<header>` > `<h1>` | `#header`, `.site-title` | フルスクリーンのファーストビュー背景画像の上に、サイトロゴを配置。 |
| **Magazine セクション** | `<section>` > `<a>` | `#magazine`, `.flex-item`, `.item` | 2枚の画像カード全体を `<a>` タグでリンク化し、内部にオーバーレイテキストを配置。 |
| **Catalog / Antique** | `<section>` | `.catalog-antique` | 背景色 `#f5f5f5` を持つ左右交互の2列レイアウトセクション。 |
| **フッターリスト** | `<ul>` > `<li>` | `#footer` | CSS擬似要素 `::before` を活用して `"-"` 記号を自動付与するカスタム箇条書き。 |

---

## 4. CSSスタイル設計 ＆ ピュアCSSテクニック解説

### 1) 絶対配置ロゴ (`position: absolute;`)
```css
#header {
  height: 100vh;
  background-image: url(../img/mainvisual.jpg);
  background-size: cover;
  position: relative;
}
#header .site-title {
  position: absolute;
  top: 30px;
  right: 30px;
}
```
* **ポイント**: 親要素 `#header` に `position: relative;` を指定し、ロゴを右上から30pxの位置に固定配置します。

### 2) 画像カード上のテキスト中央オーバーレイ
```css
#magazine .flex-item .item {
  position: relative;
}
#magazine .flex-item .item .text {
  max-width: 290px;
  color: #fff;
  background-color: rgba(0, 0, 0, 0.5);
  position: absolute;
  top: 40%;
  left: 0;
  right: 0;
  margin: 0 auto;
}
```
* **ポイント**: `left: 0; right: 0; margin: 0 auto;` ＋ `top: 40%;` により、可変幅のカード画像中央に半透明テキストボックスを均等配置します。

### 3) 擬似要素 `::before` によるカスタムリスト記号
```css
#footer .item li::before {
  content: "-";
  margin-right: 5px;
}
```
* **ポイント**: 標準の箇条書きポッチではなくハイフン記号 `"-"` をCSSの擬似要素で自動挿入しデザイン性を向上させます。

---

## 5. レスポンシブ設計仕様 (`@media screen and (max-width: 896px)`)

```css
@media screen and (max-width: 896px) {
  #magazine .flex-item, .catalog-antique .flex-item, #footer .flex-item {
    flex-direction: column;
  }
  #magazine .flex-item .item, .catalog-antique .item, #footer .item {
    width: 100%;
  }
}
```
* タブレット以下（896px）で全セクションのFlex列を `flex-direction: column;` に統一変換し、1列縦積みに変更します。
