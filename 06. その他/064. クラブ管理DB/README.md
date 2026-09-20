# クラブ管理データベース

## 概要

本システムは複数のアマチュア無線クラブを管理するための PostgreSQL (Neon) ベースのデータベースです。

現在は以下のクラブを管理しています。

- JA1YTS
- JR1YWM

会員情報を中心に、

- 会費管理
- イベント管理
- 出席管理
- 収支管理
- 銀行口座情報管理

を統合的に扱います。

---

# 設計方針

## 基本思想

データは共通テーブルで管理し、クラブごとの表示や集計は VIEW で実現します。

```text
テーブル = 正規データ
VIEW     = 表示・集計用
```

原則として VIEW を更新対象とせず、更新はベーステーブルに対して行います。

---

# 主なテーブル

## clubs

クラブマスタ

|列名|内容|
|---|---|
|id|クラブID|
|name|クラブ名|
|note|備考|

---

## members

会員情報管理テーブル

システムの中心となるテーブルです。

|列名|
|---|
|id|
|club_id|
|name|
|callsign|
|license|
|email|
|phone|
|mobile_phone|
|joined_at|
|status|
|postal_code|
|address|
|role_rank|
|role_name|
|yomi|

---

## member_bank_info

会員の金融機関情報

|列名|
|---|
|id|
|kigo|
|bango|
|lastme|
|firstme|
|bank|
|branch|
|branch_code|
|note|

---

## fees

会費情報

|列名|
|---|
|id|
|member_id|
|year|
|amount|
|paid_at|
|account|
|note|

---

## unpaid_balance

未納管理

|列名|
|---|
|member_id|
|club_id|
|amount|
|note|

---

## events

行事・イベント管理

|列名|
|---|
|id|
|club_id|
|event_date|
|title|
|location|
|note|

---

## attendance

イベント参加管理

|列名|
|---|
|id|
|event_id|
|member_id|
|status|
|note|

---

## income

収入管理

|列名|
|---|
|id|
|club_id|
|date|
|category|
|amount|
|account|
|note|

---

## expenses

支出管理

|列名|
|---|
|id|
|club_id|
|date|
|category|
|amount|
|account|
|note|

---

# テーブル関係

```text
clubs
  │
  ├─ members
  │     │
  │     ├─ fees
  │     ├─ member_bank_info
  │     └─ attendance
  │
  ├─ events
  │     │
  │     └─ attendance
  │
  ├─ income
  └─ expenses
```

---

# 主なVIEW

## ja1yts_sorted

JA1YTS会員名簿

役職順位等を考慮して並べ替えた一覧。

---

## ja1yts_with_bankinfo

会員情報と口座情報を結合した一覧。

---

## ja1yts_events

JA1YTSイベント一覧。

---

## ja1yts_events_with_participants

イベント情報と参加者一覧を統合したVIEW。

参加人数と参加者名を取得可能。

---

## ja1yts_fee_dashboard

会費管理ダッシュボード。

以下を集約表示する。

- 納入状況
- 当年度未納
- 過年度未納
- 総未納額

---

## jr1ywm

JR1YWM会員一覧。

---

## jr1ywm_sorted

JR1YWM会員一覧（並び替え済）。

---

## jr1ywm_events_with_participants

JR1YWMイベント参加状況一覧。

---

## jr1ywm_ledger

収入・支出・会費情報から生成される会計台帳VIEW。

以下を算出する。

- 収入
- 支出
- 現金残高
- 口座残高
- 総残高

---

# 運用ルール

## データ更新

原則として以下のテーブルのみを更新します。

- members
- member_bank_info
- fees
- attendance
- events
- income
- expenses

VIEWは参照用途です。

---

# 今後の課題

以下は運用状況に応じて見直すこと。

- 認証機能
- 権限管理
- バックアップ手順
- データ移行手順
- ER図の整備
- VIEW定義書の整備

---

# 管理者向けメモ

会員管理だけではなく、クラブ運営全体を管理するための統合データベースとして設計されている。

クラブ別のデータ分離は物理テーブルではなく VIEW によって実現している。