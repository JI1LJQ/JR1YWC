[元リポジトリ：JA1XPM/dvtextmonitor](https://github.com/JA1XPM/dvtextmonitor)

# DV text monitor Ver 3.3

Copyright (C) JA1XPM

## 読む前に

本ソフトは非公式の個人開発ツールであり、Icom Inc. および各関連団体とは無関係です。
“D-STAR”, “ICOM”, “IC-9700”, “RS-MS1A/RS-MS1I” などの名称は各権利者の商標・登録商標です。
本ソフトは実機観測に基づく互換実装であり、将来のファーム・アプリ更新等で動作しなくなる可能性があります。

このプログラムは、ICOM の RS-MS1A / RS-MS1I（スマホ用アプリ）とDVテキストで交信可能なWindows PC用アプリケーションです。
主な想定構成は IC-9700（USB(B)）とWindows PCです。本プログラムにより、IC-9700にスマホを接続せず、PCからテキストを送受信できます。

## 必要なもの

- Windows 11 PC
- ICOM IC-9700（DV Data I/FにUSB(B)を使用し、DVモードに設定）
- リグとPCを接続するUSBケーブル
- PC側のCOMポート番号

必要なデバイスドライバはICOMホームページを参照してください。

## 起動方法

```text
python dvtextmonitor.py
```

ログファイルに保存する場合：

```text
python dvtextmonitor.py log.txt
```

ログには相対パス・絶対パスのどちらも指定できます。ログの文字コードはUTF-8（BOM無し）です。

## 設定ファイル

起動時、プログラム本体と同じフォルダにある `dvtextmonitor.ini` を読み込みます。ファイルがない場合は初期値で自動作成します。

```ini
COM=COM1
SPEED=9600
MY=JA1XPM C
UR=CQCQCQ
```

- `COM`: COMポート名
- `SPEED`: 通信速度
- `MY`: 送信元コール
- `UR`: 宛先コール

## 基本的な使い方

起動すると受信表示が始まります。RS-MS1A / RS-MS1IからDVテキストが送信されると表示します。
DV画像に追加されたテキストメッセージも表示しますが、画像データは破棄します。
GNSS形式のGPS情報はGoogle Maps形式のURLで表示し、D-PRS形式のGPS情報はそのまま表示します。
コンソールに文字を入力してEnterを押すと相手局へ送信します。

実行中に送信元・宛先コールサインを確認、変更できます。

```text
/MY
/UR
/MY JA1XPM C
/UR W1AW A
```

## 終了

Ctrl+Cで終了します。

## 免責

本ソフトは無保証です。使用は自己責任でお願いします。電波法・各種ルールを守って運用してください。

## ライセンス

本ソフトはMIT Licenseで公開されています。詳細は[元リポジトリ](https://github.com/JA1XPM/dvtextmonitor)のLICENSEを参照してください。

## 技術解説

RS-MS1A系のDVテキストパケット、ID生成、UTF-8本文のエスケープ、チェックサム処理に対応しています。
詳しいパケット構造、計算例、制御バイトの扱いは元リポジトリのREADMEに記載されています。
