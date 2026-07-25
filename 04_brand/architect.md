# 設計仕様書（Architect.md）：【入門編】ブランドサイト（ジュエリー）

## 1. プロジェクト概要・完成仕様

本プロジェクトは、`vw` (Viewport Width) 単位による画面幅比例レイアウト、Google Fonts の読み込み・適用、`flex-direction: column-reverse;` によるレスポンシブ時の画像・テキスト順序逆転技法、およびメールリンク（`mailto:`）を習得するための**上質なジュエリーブランドWEBサイト**です。

### 基本仕様パラメータ
* **画面比例幅 (PC)**: `width: 90vw;`（メインビジュアル ＆ ヘッダー）
* **コンテンツ最大幅 (`.container`)**: `1000px`（左右パディング `18px`）
* **フォント**: Google Fonts『Crimson Text』（セリフ体）
* **レスポンシブ・ブレイクポイント**: `767px`（767px以下でスマホ縦積み＆Workセクションの順序逆転）
* **リセットCSS**: `ress.min.css`

---

## 2. ディレクトリ構造

```
04_brand/
 ├── architect.md             # 本設計仕様書
 ├── sample/                  # 模範解答用
 │    ├── index.html
 │    ├── css/style.css
 │    └── img/ (logo.svg, mainvisual.jpg, concept.jpg, work.jpg, favicon.ico)
 └── practice/                # 写経・練習用スターター
      ├── index.html
      ├── css/style.css
      └── img/
```

---

## 3. HTML構造設計とタグ選定の根拠

| セクション / 要素 | 使用タグ | クラス / ID | タグ選定の根拠・意図 |
| :--- | :--- | :--- | :--- |
| **Google Fonts** | `<link>` | `-` | HTML `<head>` 内で `Crimson Text` フォントファイルを非同期読み込み。 |
| **問い合わせリンク** | `<a>` | `-` | `mailto:address?subject=件名` 形式で、ユーザーの標準メール起動を提示。 |
| **Concept / Work** | `<section>` | `.content`, `#concept`, `#work` | ブランドの思想と実績を表すテーマの「章」として `<section>` を使用。 |
| **英語補助表記** | `<span>` | `.section-title-en` | 日本語見出しの補足表現であり独立文章ではないため `span` タグを指定し、CSSでインラインブロック化。 |

---

## 4. CSSスタイル設計 ＆ ピュアCSSテクニック解説

### 1) ビューポート幅単位 `vw` による比例レイアウト
```css
#mainvisual, #header {
  width: 90vw;
  margin: 0 auto;
}
```
* **ポイント**: 親要素のpx制限を受けず、端末画面の表示幅全体に対して常に90%のサイズ感でエレガントに配置します。

### 2) `flex-direction: column-reverse;` による表示順序逆転
```css
@media screen and (max-width: 767px) {
  #work {
    flex-direction: column-reverse;
  }
}
```
* **ポイント**: PCでは「テキスト(左) / 画像(右)」で配置していたWorkセクションを、スマホ表示時にHTMLの書き換えなしで「画像(上) / テキスト(下)」の美しい視覚順に反転させます。

### 3) `span` タグへの `display: inline-block;` 適用
```css
.section-title-en {
  display: inline-block;
  margin-bottom: 25px;
}
```
* **ポイント**: インライン要素の `span` に `display: inline-block;` を付与して `margin-bottom` を作用させます。

---

## 5. レスポンシブ設計仕様 (`@media screen and (max-width: 767px)`)

```css
@media screen and (max-width: 767px) {
  #mainvisual {
    width: 100%;
    margin: 0;
  }
  #mainvisual img {
    height: 50vh;
    object-fit: cover;
  }
  #work {
    flex-direction: column-reverse;
  }
  .content {
    flex-direction: column;
  }
  .content .img, .content .text {
    width: 100%;
    padding: 0;
  }
}
```
* スマホ表示時、メインビジュアルを `100%` 幅 ＋ 高さ `50vh`（画面高さの半分）に切り替え。
* `.content`（画像とテキスト）の各50%幅を `100%` へ展開します。
