# Codejump Web制作 写経・練習リポジトリ

Web制作学習サイト「[Codejump](https://code-jump.com/)」の各種制作課題を実際に写経・実践練習するための学習リポジトリです。

---

## 📁 リポジトリの構成

各課題ディレクトリ（`01_profile`, `02_photo` ...）は、以下の3つの要素で構成されています。

```
0X_課題名/
 ├── architect.md               # 設計仕様書（ワイヤーフレーム、HTMLタグ選定理由、CSS解説）
 ├── sample/                    # 模範解答（完成版HTML/CSS + 画像アセット）
 └── practice/                  # 写経・練習用（誘導コメント付きスターターコード + 画像アセット）
```

---

## 🚀 収録課題一覧

| ディレクトリ | 課題名 | 難易度 | 主な学習テーマ |
| :--- | :--- | :--- | :--- |
| **[01_profile](./01_profile)** | プロフィールサイト | 入門編 | 1カラムレイアウト、`line-height: 1px` 隙間消去、3列カード均等配置 |
| **[02_photo](./02_photo)** | フォトサイト | 入門編 | 2層幅制御 (`container`/`inner`)、順序付きリスト (`ol`)、定義リスト (`dl/dt/dd`) 表組み |
| **[03_recipe](./03_recipe)** | レシピサイト（トップ） | 入門編 | `100vh` 全画面ファーストビュー、`calc(100%/3)` 3等分、`vertical-align: bottom;` |
| **[04_brand](./04_brand)** | ブランドサイト（ジュエリー）| 入門編 | `vw` 単位比例配置、Google Fonts、`flex-direction: column-reverse;` 順序反転 |
| **[05_portfolio1](./05_portfolio1)** | ポートフォリオサイト | 初級編 | `<picture>` デバイス画像切替、フォーム（`form`/`input`/`textarea`/`label`）デザイン |
| **[06_store1](./06_store1)** | ストアサイト（書店 Mag88）| 初級編 | `position: absolute;` テキストオーバーレイ、`::before` 擬似要素箇条書き |

---

## 💡 写経学習の使い方

1. 挑戦したい課題の `architect.md` を一読し、全体のレイアウト構成やCSS設計思想を把握します。
2. `practice/` フォルダ内の `index.html` および `css/style.css` をテキストエディタで開き、コメントのヒントに従ってコードを書き進めます。
3. 画像ファイルは `practice/img/` に既に展開されているため、書きながらブラウザで表示を確認できます。
4. 詰まった場合や答え合わせを行いたい場合は、`sample/` フォルダの模範解答コードと見比べます。

---

## 🔗 参考リンク
* **Codejump 公式サイト**: [https://code-jump.com/](https://code-jump.com/)
