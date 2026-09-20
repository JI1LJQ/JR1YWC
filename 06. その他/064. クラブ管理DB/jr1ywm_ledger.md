# jr1ywm_ledger

## 概要

JR1YWMの会計台帳VIEWです。

複数テーブルに保存されている

- 会費収入
- その他収入
- 支出

を時系列で統合し、残高推移を計算します。

会計帳簿として運用するためのVIEWです。

---

## 利用テーブル

### fees

会費収入

---

### members

会費のクラブ判定

---

### income

その他収入

---

### expenses

支出

---

## 対象クラブ

```sql
club_id = 1
```

JR1YWMのみを対象とします。

---

## データ生成方法

以下の3種類の取引を結合します。

### 1. 会費収入

```sql
fees
```

カテゴリは固定で

```text
会費
```

となります。

---

### 2. その他収入

```sql
income
```

---

### 3. 支出

```sql
expenses
```

---

## 出力項目

### date

取引日

---

### category

取引区分

例

```text
会費
寄付
備品購入
```

---

### note

備考

---

### account

管理口座

想定値

```text
cash
bank
```

---

### income

収入額

---

### expense

支出額

---

### cash_balance

現金残高

計算式

```text
cash収入
-
cash支出
```

の累積和

---

### bank_balance

銀行残高

計算式

```text
bank収入
-
bank支出
```

の累積和

---

### total_balance

総残高

計算式

```text
総収入
-
総支出
```

の累積和

---

## 並び順

以下の順序で取引を並べます。

```sql
date
category
income DESC
account
note
```

---

## row_idについて

内部的に

```sql
row_number()
```

を使用し取引順序を固定しています。

これにより同日取引が複数存在しても残高計算結果が安定します。

---

## 勘定区分

### cash

現金勘定

---

### bank

銀行口座勘定

---

## 残高の考え方

### cash_balance

現金のみの残高

---

### bank_balance

銀行口座のみの残高

---

### total_balance

クラブ全体の資産残高

```text
cash_balance
+
bank_balance
```

と一致します。

---

## 更新可否

読み取り専用

直接更新しません。

更新対象テーブル

- fees
- income
- expenses

---

## 作成目的

会計担当者が入出金状況を時系列で追跡できるようにするため。

以下を常時確認できます。

- 収入履歴
- 支出履歴
- 現金残高
- 銀行残高
- クラブ総残高

---

## 運用上の注意

会費データは members テーブルを参照してクラブ判定しています。

```sql
JOIN members m
ON m.id = f.member_id
```

会員の club_id を変更すると過去の会費データの集計結果にも影響する可能性があります。
