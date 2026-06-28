[元リポジトリ：JA1XPM/CWGAME](https://github.com/JA1XPM/CWGAME)

<!--
*********************************************
CWGAME Ver.1.1 by JA1XPM 2026.05.17
*********************************************
-->

# CWGAME Ver.1.1（日本語）

CWGAME Ver.1.1 は、Tkinterで作成したモールス信号入力ゲームです。

画面上部から英数字と対応するモールス信号が落ちてきます。左マウスボタンでモールス信号を入力します。

- 短いクリック: トン（・）
- 長いクリック: ツー（－）

入力したモールス信号が、赤いラインを越える前の落下中の文字と一致するとスコアが増えます。

## バージョン

Ver.1.1 は `cwgame.py` を正式ソースとして扱います。ウィンドウサイズを変更したとき、ゲームエリアを新しいサイズに合わせて再構成し、ゲームをリセットします。

## 必要環境

- Python 3.10以降
- Tkinter
- pynput

Python依存パッケージは次のコマンドでインストールします。

```powershell
pip install -r requirements.txt
```

## 実行

```powershell
python cwgame.py
```

## ビルド

PyInstaller用のspecファイルを含んでいます。

```powershell
pyinstaller cwgame.spec
```

ビルド生成物は `.gitignore` でGit管理対象外にしています。

## アーカイブ

過去の開発ファイルは `archive/` に参考用として残しています。正式なVer.1.1ソースではありません。

# CWGAME Ver.1.1

CWGAME Ver.1.1 is a Tkinter-based Morse code typing game.

Characters and their Morse code fall from the top of the window. Use the left mouse button to enter Morse code:

- Short click: dot
- Long click: dash

When the entered Morse code matches a falling character before it crosses the red line, the score increases.

## Version

Ver.1.1 is based on `cwgame.py`. It adds resizable game-area support: when the window size is changed, the game area is rebuilt for the new size and the game is reset.

## Requirements

- Python 3.10 or later
- Tkinter
- pynput

Install the Python dependency with:

```powershell
pip install -r requirements.txt
```

## Run

```powershell
python cwgame.py
```

## Build

A PyInstaller spec file is included for Ver.1.1:

```powershell
pyinstaller cwgame.spec
```

Build outputs are intentionally excluded from Git by `.gitignore`.

## Archive

Older development files are kept in `archive/` for reference. They are not treated as the formal Ver.1.1 source.
