# 設計仕様書（Architect.md）：【入門編】フォトサイト

## 1. プロジェクト概要・完成仕様

本プロジェクトは、2層（全体と内部コンテンツ）の最大幅制御、定義リスト（`dl/dt/dd`）による表組み表現、および順序付きリスト（`ol`）のスタイリングを習得するための**1カラム・フォトギャラリーWEBサイト**です。

### 基本仕様パラメータ
* **全体外枠幅 (`.container`)**: `1000px`（中央寄せ `margin: 0 auto;`）
* **内部コンテンツ幅 (`.inner`)**: `600px`（中央寄せ `margin: 0 auto;`）
* **レスポンシブ・ブレイクポイント**: `1024px`（1024px以下で左右パディング確保および縦積みレイアウト切替）
* **背景色**: `#f4f9ff`（サイト全体淡いブルー） / `#fff`（Index背景白）
* **リセットCSS**: `ress.min.css`

---

## 2. ディレクトリ構造

```
02_photo/
 ├── architect.md             # 本設計仕様書
 ├── sample/                  # 模範解答用
 │    ├── index.html
 │    ├── css/style.css
 │    └── img/ (logo.svg, mainvisual.jpg, detail.jpg, favicon.ico)
 └── practice/                # 写経・練習用スターター
      ├── index.html
      ├── css/style.css
      └── img/
```

---

## 3. HTML構造設計とタグ選定の根拠

| セクション / 要素 | 使用タグ | クラス / ID | タグ選定の根拠・意図 |
| :--- | :--- | :--- | :--- |
| **全体外枠** | `<div>` | `.container` | サイト全体の最大幅（1000px）を制御する共通コンテナ。 |
| **内部中央幅** | `<div>` | `.inner` | テキスト・リスト部分の最大幅（600px）を制御する共通枠。 |
| **Index 目次** | `<ol>` > `<li>` | `.index-list` | 目次は1, 2, 3...と順に読む「順序性のあるリスト（Ordered List）」であるため `<ol>` を使用。 |
| **書籍スペック** | `<dl>` > `<dt>` + `<dd>` | `-` | 著者・出版社・発行年といった「項目名（dt）」と「値（dd）」の対構造を表す定義リストを使用。 |
| **外部ストアリンク** | `<a>` | `.link` | `target="_blank"` ＋ `rel="noopener noreferrer"` で安全な別タブ遷移を提供。 |

---

## 4. CSSスタイル設計 ＆ ピュアCSSテクニック解説

### 1) 2層レイアウト（`.container` ＆ `.inner`）
```css
.container {
  max-width: 1000px;
  margin: 0 auto;
}
.inner {
  max-width: 600px;
  margin: 0 auto;
}
```
* **ポイント**: コンテンツの目的に応じて「外側の最大幅」と「内側の絞り込み幅」を2段階で管理します。

### 2) 定義リスト（`dl/dt/dd`）のFlexbox表組み
```css
#detail .content dl {
  display: flex;
  flex-wrap: wrap;
  border-top: solid 1px #dedede;
  border-bottom: solid 1px #dedede;
}
#detail .content dt {
  width: 25%;
}
#detail .content dd {
  width: 75%;
}
```
* **ポイント**: `flex-wrap: wrap;` で折り返しを有効化し、`dt (25%)` ＋ `dd (75%) = 100%` ごとに改行させて綺麗な表構造を作成します。

### 3) リスト末尾要素のマージン消去 (`:last-child`)
```css
#index .index-list li {
  margin-bottom: 20px;
}
#index .index-list li:last-child {
  margin-bottom: 0;
}
```
* **ポイント**: `li:last-child` に `margin-bottom: 0;` を指定し、親要素の下パディングとの不要な重複を防ぎます。

---

## 5. レスポンシブ設計仕様 (`@media screen and (max-width: 1024px)`)

```css
@media screen and (max-width: 1024px) {
  .inner {
    padding: 0 40px;
  }
  #header, #mainvisual {
    padding: 0 10px;
  }
  #detail .content {
    flex-direction: column;
  }
  #detail .content .img {
    width: 100%;
    margin: 0 0 25px 0;
  }
}
```
* タブレット・スマホ画面幅になった際、`padding: 0 40px;` で内側画面端の余白を確保。
* `#detail .content` を `flex-direction: column;` に切り替えて、画像とテキストを縦並びに配置します。
