# 設計仕様書（Architect.md）：【入門編】プロフィールサイト

## 1. プロジェクト概要・完成仕様

本プロジェクトは、HTML5 / CSS3 の基礎学習を修了した学習者が、最初にWebサイト全体のコーディング手順・レスポンシブ設計・Flexboxレイアウトの組み立て方を習得するための**入門用1カラムWEBサイト**です。

### 基本仕様パラメータ
* **コンテンツ最大幅（PC）**: `960px`
* **画面左右パディング**: `4%`（画面幅に応じて自然に伸縮）
* **メインビジュアル高さ**: PC `600px` 固定 / SP `calc(100vh - 60px)`（ヘッダー引いた画面全高）
* **レスポンシブ・ブレイクポイント**: `600px`（600px以下でスマホ縦積みレイアウトへ切替）
* **リセットCSS**: `ress.min.css`（外部CDN経由）

---

## 2. ワイヤーフレーム ＆ ディレクトリ構造

### ディレクトリ構成
```
01_profile/
 ├── architect.md             # 本設計仕様書
 ├── sample/                  # 模範解答用ディレクトリ（完成コード）
 │    ├── index.html
 │    ├── css/style.css
 │    └── img/
 └── practice/                # 写経・練習用スターターディレクトリ
      ├── index.html
      ├── css/style.css
      └── img/
```

### ブロック階層構造
```
body
 ├── header#header.wrapper     [ロゴ + グローバルナビ]
 └── main
      ├── div#mainvisual        [ファーストビュー大画像]
      ├── section#about.wrapper [プロフィール画像 + 自己紹介テキスト]
      └── section#bicycle.wrapper[3カラム自慢の自転車紹介カードリスト]
 └── footer#footer             [コピーライト]
```

---

## 3. HTML構造設計とタグ選定の根拠

| セクション / 要素 | 使用タグ | クラス / ID | タグ選定の根拠・意図 |
| :--- | :--- | :--- | :--- |
| **全体枠組み** | `<header>`, `<main>`, `<footer>` | `-` | ページの構成要素をセマンティックに明確化。検索エンジンやスクリーンリーダーへ正しい文書構造を伝える。 |
| **ロゴ** | `<h1>` > `<a>` > `<img>` | `.site-title` | ページ内で最も重要な主題（ブランド/サイト名）であるため `h1` を指定。トップページへの戻りリンクを付与。 |
| **グローバルナビ** | `<nav>` > `<ul>` > `<li>` > `<a>` | `-` | 主要回遊リンクの集合体であるため `nav` タグで囲み、リスト構造 `ul/li` でグルーピング。 |
| **メインビジュアル** | `<div>` > `<img>` | `#mainvisual` | 文書上の章・節ではなく単なる画像配置ブロックであるため、意味を持たない `div` タグを選択。 |
| **About / Bicycle** | `<section>` | `#about`, `#bicycle`, `.wrapper` | 内部に独自のH2見出しを持つテーマの「章（Section）」であるため `<section>` を使用。共通幅用に `.wrapper` 付与。 |
| **見出しレベル** | `<h2>`, `<h3>` | `.section-title`, `.content-title` | H1（サイト名）の下位構造として、各セクション題名に `h2`、カードやブロック内の小見出しに `h3` を見出し順序を守って配置。 |

---

## 4. CSSスタイル設計 ＆ ピュアCSSテクニック解説

### 1) リセットCSSの読み込みと記述ルール
* `ress.min.css` を自作CSSより**先に**読み込みます。
* **理由**: CSSは後勝ち（カスケード）ルールで適用されるため、ブラウザごとの標準余白・装飾をリセットした後に独自の `style.css` を適用させる必要があります。

### 2) 共通レイアウトクラス `.wrapper`
```css
.wrapper {
  max-width: 960px;
  margin: 0 auto 100px;
  padding: 0 4%;
  text-align: center;
}
```
* **ポイント**: 
  - `max-width: 960px;` ＋ `margin: 0 auto;` で大画面時の中央寄せを実現。
  - `padding: 0 4%;` を指定することで、スマホ表示時に固定pxではなく画面幅に比例した自然な左右端の余白を維持。

### 3) ロゴ画像のベースライン隙間除去 (`line-height: 1px;`)
```css
.site-title {
  width: 120px;
  line-height: 1px; /* または line-height: 0; */
}
```
* **ポイント**: `img` はインライン要素のため、標準テキストのアルファベット下飛び出し（descender）用余白が生じます。`line-height: 1px;` や `display: block;` で隙間を完全に消去します。

### 4) 見出し下線のテキスト幅フィット (`display: inline-block;`)
```css
.section-title {
  display: inline-block;
  font-size: 2rem;
  margin-bottom: 60px;
  border-bottom: solid 1px #383e45;
}
```
* **ポイント**: `h2` は初期状態が `display: block` のため全幅に下線が伸びてしまいます。`display: inline-block` に変更することでテキストコンテンツ長さに下線幅を揃えます。

### 5) 画像のトリミング・アスペクト比保護 (`object-fit: cover;`)
```css
#mainvisual img {
  width: 100%;
  max-width: 1920px;
  height: 600px;
  object-fit: cover;
}
```
* **ポイント**: `height: 600px;` のように固定高を指定した際、画像のアスペクト比（縦横比）を歪ませずに枠全体を覆うように自動切り抜き表示します。

### 6) 正円プロフ画像の切り抜き (`border-radius: 50%;`)
```css
#about img {
  width: 100px;
  height: 100px;
  border-radius: 50%;
}
```
* **ポイント**: 正方形（100px × 100px）の要素に `border-radius: 50%;` を指定することで完全な正円アイコンを作成します。

### 7) 3カラムカードの均等配置 (`width: 32%;` + Flexbox)
```css
#bicycle ul {
  display: flex;
  justify-content: space-between;
}
#bicycle li {
  width: 32%;
}
```
* **ポイント**: `32% × 3 = 96%`。残り `4%` が `justify-content: space-between;` によりカード要素間の余白として自動分配されます。

---

## 5. レスポンシブ（スマホ化）設計仕様 (`@media screen and (max-width: 600px)`)

```css
@media screen and (max-width: 600px) {
  /* ① メインビジュアル画面高ピッタリ調整 */
  #mainvisual img {
    height: calc(100vh - 60px);
  }

  /* ② Aboutコンテンツの縦積み切替 */
  #about .content {
    flex-direction: column;
  }
  #about img {
    margin-right: 0;
  }

  /* ③ Bicycleカードの1列縦積み切替 */
  #bicycle ul {
    flex-direction: column;
  }
  #bicycle li {
    width: 100%;
    margin-bottom: 30px;
  }
}
```
* `flex-direction: column;` により、Flexboxの配置軸を横方向（row）から縦方向（column）へ切替。
* 各カードの幅を `width: 100%;` に引き伸ばし、各要素間に `margin-bottom: 30px;` の縦間隔を付与します。
