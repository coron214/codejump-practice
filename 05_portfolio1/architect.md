# 設計仕様書（Architect.md）：【初級編】ポートフォリオサイト

## 1. プロジェクト概要・完成仕様

本プロジェクトは、HTML5の `<picture>` タグによるレスポンシブ画像切替、HTMLフォームタグ（`form/input/textarea/label`）のマークアップとスタイリング、およびマルチセクション構造を習得するための**実践的ポートフォリオWEBサイト**です。

### 基本仕様パラメータ
* **コンテンツ最大幅 (`.wrapper`)**: `960px`（左右パディング `4%`）
* **レスポンシブ・ブレイクポイント**: `600px`（600px以下でスマホ縦積みレイアウト切替）
* **画像切替**: `<picture>` タグ（600px以下で `mainvisual-sp.jpg`、PC時 `mainvisual-pc.jpg`）
* **フォーム構造**: `<form>`, `<input>`, `<textarea>`, `<label for="...">`
* **リセットCSS**: `ress.min.css`

---

## 2. ディレクトリ構造

```
05_portfolio1/
 ├── architect.md             # 本設計仕様書
 ├── sample/                  # 模範解答用
 │    ├── index.html
 │    ├── css/style.css
 │    └── img/ (mainvisual-pc.jpg, mainvisual-sp.jpg, works1~6.jpg, icon-instagram.png, etc.)
 └── practice/                # 写経・練習用スターター
      ├── index.html
      ├── css/style.css
      └── img/
```

---

## 3. HTML構造設計とタグ選定の根拠

| セクション / 要素 | 使用タグ | クラス / ID | タグ選定の根拠・意図 |
| :--- | :--- | :--- | :--- |
| **画像デバイス切替** | `<picture>` > `<source>` + `<img>` | `#mainvisual` | CSS背景画像切り替えに比べ、不要な画像のダウンロードを抑制し初期ロード表示速度（LCP）を最適化。 |
| **作品ギャラリー** | `<ul>` > `<li>` > `<img>` | `#works` | 6点の制作実績カードを一覧表示するグリッドリスト構造。 |
| **お知らせリスト** | `<dl>` > `<dt>` + `<dd>` | `#news` | 「日付（dt）」と「ニュース内容（dd）」の1対1対応データ構造。 |
| **問い合わせフォーム** | `<form>`, `<label>`, `<input>`, `<textarea>` | `#contact` | `label for="id"` で入力項目名とフォーム部品を関連付け、タップ可能領域を拡大してUXを改善。 |

---

## 4. CSSスタイル設計 ＆ ピュアCSSテクニック解説

### 1) `<picture>` タグによる画像の最適レスポンシブ
```html
<picture>
  <source media="(max-width: 600px)" srcset="img/mainvisual-sp.jpg">
  <img src="img/mainvisual-pc.jpg" alt="メインビジュアル">
</picture>
```
* **ポイント**: ブラウザがメディアクエリを自動判定し、最適な画像のみをダウンロードします。

### 2) フォーム部品のスタイルカスタマイズ
```css
#contact dd input, #contact dd textarea {
  width: 100%;
  border: solid 1px #c8c8c8;
  padding: 10px;
}
#contact .button input {
  width: 200px;
  background-color: #24292e;
  color: #fff;
  padding: 15px 0;
}
#contact .button input:hover {
  background-color: #fff;
  color: #24292e;
  border: solid 1px #24292e;
}
```
* **ポイント**: デフォルトのブラウザ標準フォームデザインをリセットし、サイトカラー（#24292e）に合わせたモダンなボタン・入力枠へカスタマイズ。

---

## 5. レスポンシブ設計仕様 (`@media screen and (max-width: 600px)`)

```css
@media screen and (max-width: 600px) {
  #header {
    flex-direction: column;
    height: auto;
    padding: 20px 0;
  }
  #works li {
    width: 100%;
  }
  #news dl, #contact dl {
    flex-direction: column;
  }
  #news dt, #news dd, #contact dt, #contact dd {
    width: 100%;
  }
}
```
* ヘッダー、Works（実績カード）、News（お知らせ）、Contact（問い合わせフォーム）の全てを縦積み 100% 幅へ一括切り替え。
