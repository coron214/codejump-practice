# 📅 Codejump Web制作 細分化ロードマップ ＆ 詳細ガントチャート

本リポジトリの全6課題を**1〜2時間単位の超細分化マイクロタスク（全32件のIssue）**に分解した詳細ガントチャートです。

---

## 📊 詳細ガントチャート（Mermaid表示）

```mermaid
gantt
    dateFormat  YYYY-MM-DD
    title Codejump Web制作 細分化ガントチャート (細密タスク分解)

    section 【01_profile】
    01-1: 骨組み・CSS初期化              :active, p1_1, 2026-07-26, 1d
    01-2: ヘッダー (ロゴ・ナビ)          :p1_2, after p1_1, 1d
    01-3: MV ＆ Aboutセクション          :p1_3, after p1_2, 1d
    01-4: Bicycle (3列Flex) ＆ フッター  :p1_4, after p1_3, 1d
    01-5: レスポンシブ (600px) ＆ 検証   :p1_5, after p1_4, 1d

    section 【02_photo】
    02-1: 2層幅制御 (.container/.inner)  :p2_1, after p1_5, 1d
    02-2: Index (ol目次) の構築          :p2_2, after p2_1, 1d
    02-3: Detail (dl/dt/dd Flex表組み)   :p2_3, after p2_2, 1d
    02-4: レスポンシブ (1024px) ＆ 検証  :p2_4, after p2_3, 1d

    section 【03_recipe】
    03-1: 100vh ヒーローイメージ         :p3_1, after p2_4, 1d
    03-2: テキスト ＆ ボタンデザイン     :p3_2, after p3_1, 1d
    03-3: calc(100%/3) 3等分ギャラリー   :p3_3, after p3_2, 1d
    03-4: レスポンシブ (834px) ＆ 検証   :p3_4, after p3_3, 1d

    section 【04_brand】
    04-1: vw単位 ＆ Google Fonts         :p4_1, after p3_4, 1d
    04-2: Concept ＆ Workレイアウト       :p4_2, after p4_1, 1d
    04-3: column-reverse 順序反転        :p4_3, after p4_2, 1d
    04-4: レスポンシブ (767px) ＆ 検証   :p4_4, after p4_3, 1d

    section 【05_portfolio1】
    05-1: pictureタグ 画像切替           :p5_1, after p4_4, 1d
    05-2: Works 6列 ＆ Newsリスト        :p5_2, after p5_1, 1d
    05-3: Contact フォーム設計           :p5_3, after p5_2, 1d
    05-4: レスポンシブ (600px) ＆ 検証   :p5_4, after p5_3, 1d

    section 【06_store1】
    06-1: position:absolute ヒーロー     :p6_1, after p5_4, 1d
    06-2: Magazine テキスト重ね          :p6_2, after p6_1, 1d
    06-3: Catalog/Antique ＆ ::before   :p6_3, after p6_2, 1d
    06-4: レスポンシブ (896px) ＆ 検証   :p6_4, after p6_3, 1d

    section 【Anki復習】
    Ankiカード全41問の反復演習           :active, anki, 2026-07-26, 25d
```

---

## 📋 細分化 Issue 管理テーブル

| 課題名 | サブタスク / 目的 | 対応 Issue |
| :--- | :--- | :--- |
| **01_profile** | 01-1: 骨組み・CSS初期化 | [#8](https://github.com/coron214/codejump-practice/issues/8) |
| | 01-2: ヘッダー (ロゴ・ナビ) | [#9](https://github.com/coron214/codejump-practice/issues/9) |
| | 01-3: MV ＆ Aboutセクション | [#10](https://github.com/coron214/codejump-practice/issues/10) |
| | 01-4: Bicycle (3列Flex) ＆ フッター | [#11](https://github.com/coron214/codejump-practice/issues/11) |
| | 01-5: レスポンシブ (600px) ＆ 検証 | [#12](https://github.com/coron214/codejump-practice/issues/12) |
| **02_photo** | 02-1: 2層幅制御 (.container/.inner) | [#13](https://github.com/coron214/codejump-practice/issues/13) |
| | 02-2: Index (ol目次) の構築 | [#14](https://github.com/coron214/codejump-practice/issues/14) |
| | 02-3: Detail (dl/dt/dd Flex表組み) | [#15](https://github.com/coron214/codejump-practice/issues/15) |
| | 02-4: レスポンシブ (1024px) ＆ 検証 | [#16](https://github.com/coron214/codejump-practice/issues/16) |
| **03_recipe** | 03-1: 100vh ヒーローイメージ | [#17](https://github.com/coron214/codejump-practice/issues/17) |
| | 03-2: テキスト ＆ ボタンデザイン | [#18](https://github.com/coron214/codejump-practice/issues/18) |
| | 03-3: calc(100%/3) 3等分ギャラリー | [#19](https://github.com/coron214/codejump-practice/issues/19) |
| | 03-4: レスポンシブ (834px) ＆ 検証 | [#20](https://github.com/coron214/codejump-practice/issues/20) |
| **04_brand** | 04-1: vw単位 ＆ Google Fonts | [#21](https://github.com/coron214/codejump-practice/issues/21) |
| | 04-2: Concept ＆ Workレイアウト | [#22](https://github.com/coron214/codejump-practice/issues/22) |
| | 04-3: column-reverse 順序反転 | [#23](https://github.com/coron214/codejump-practice/issues/23) |
| | 04-4: レスポンシブ (767px) ＆ 検証 | [#24](https://github.com/coron214/codejump-practice/issues/24) |
| **05_portfolio1** | 05-1: pictureタグ 画像切替 | [#25](https://github.com/coron214/codejump-practice/issues/25) |
| | 05-2: Works 6列 ＆ Newsリスト | [#26](https://github.com/coron214/codejump-practice/issues/26) |
| | 05-3: Contact フォーム設計 | [#27](https://github.com/coron214/codejump-practice/issues/27) |
| | 05-4: レスポンシブ (600px) ＆ 検証 | [#28](https://github.com/coron214/codejump-practice/issues/28) |
| **06_store1** | 06-1: position:absolute ヒーロー | [#29](https://github.com/coron214/codejump-practice/issues/29) |
| | 06-2: Magazine テキスト重ね | [#30](https://github.com/coron214/codejump-practice/issues/30) |
| | 06-3: Catalog/Antique ＆ ::before | [#31](https://github.com/coron214/codejump-practice/issues/31) |
| | 06-4: レスポンシブ (896px) ＆ 検証 | [#32](https://github.com/coron214/codejump-practice/issues/32) |

---

## 🔗 オンライン管理ボード
* **[GitHub Project #5 カンバン＆タイムライン](https://github.com/users/coron214/projects/5)**
