[元リポジトリ：JA1XPM/oumugaeshi](https://github.com/JA1XPM/oumugaeshi)

# オウム返しプログラム

Windows 11 + Python 3.10.nで動作確認

- サウンドデバイスの入力を自動録音、自動再生します。
- 録音時間のデフォルト設定は30秒です。30秒たつと録音は強制終了、強制再生されます。
- 30秒前に3秒の無音状態があると、録音は終了します。
- COMポートを起動パラメーターで指定すると、音声再生時にそのポートのDTRをONにします。音声再生が終了したらDTRをOFFにします。
- `id.wav` が同じディレクトリにある場合、音声ファイルの後に再生します。なくても動作します。`id.wav` はほかのソフトで作成してください。

起動例：

```text
py oumugaeshi.py
```

COMポートを制御する場合：

```text
py oumugaeshi.py COM1
```

終了はCtrl+Cです。

アマチュア無線機に接続し、「音声デジピーター」「オウム返しレピーター」「parrot repeater」を作れます。必要に応じてIDも追加できます。

DTRのON/OFFをトランジスタスイッチ経由で利用し、オウムの模型に話すと羽根を動かしながら録音した声を返す展示などにも応用できます。

by JA1XPM

## ライセンス

本ソフトウェアはMITライセンスで公開されています。詳細は[元リポジトリのLICENSE](https://github.com/JA1XPM/oumugaeshi/blob/main/LICENSE)を参照してください。
