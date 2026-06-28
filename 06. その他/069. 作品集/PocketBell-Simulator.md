[元リポジトリ：JA1XPM/PocketBell-Simulator](https://github.com/JA1XPM/PocketBell-Simulator)

# PocketBell GUI

PocketBell GUI は、アマチュア無線の音声回線上でDTMFを使って、ポケベル風のメッセージ送受信を行うGUIアプリケーションです。

## 特徴

- ポケベル風GUI
- DTMFによる送受信
- `*2*2` フリーワード本文対応
- `*4*4NN` 定型文本文対応
- 自局コールサイン設定
- 着信音ON/OFFとCQ着信音ON/OFF
- 送受信履歴の保存とスクロール表示
- ポケベル標準の文字コードを使用しているため、本ソフトウェアを使わなくても受信・解読可能

## 必要環境

- Windows
- Python 3.10系
- `requirements.txt` に記載のライブラリ
- オーディオ入出力環境
- PTT制御用COMポート環境
- VOX運用時はCOMポート不要

## インストール

```powershell
py -3.10 -m pip install -r requirements.txt
```

## 起動

`start_tx_gui.bat` を実行します。起動前に `OUTDEV`、`INDEV`、`COM` を環境に合わせて設定してください。

オーディオデバイス番号確認：

```powershell
py dtmftest_pager.py devices
```

VOX（Signalinkを含む）を使う場合：

```bat
set COM=NONE
```

## 入力例

```text
CQ,*2*2こんにちは
JH1QSY,*2*2ａｂｃ１２３
JH1QSY,*4*402
```

一度に送れるメッセージは24文字までです。

`*2*2` 本文では以下を自動正規化します。

- ひらがな → カタカナ
- 全角英数字 → 半角英数字
- 英字小文字 → 英字大文字

## ドキュメント

- 詳しい使い方：`MANUAL.txt`
- 技術仕様：`SPEC.txt`

## ライセンス

本ソフトウェアはMIT Licenseの条件で配布されています。詳細は[元リポジトリ](https://github.com/JA1XPM/PocketBell-Simulator)のLICENSEを参照してください。
