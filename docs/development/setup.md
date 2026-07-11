# 開発環境の準備

## 対象環境

- Apple Silicon搭載Mac
- macOS 14 Sonoma以降
- Xcode Command Line Tools
- mise

Go、golangci-lint、Fyneのパッケージ化に必要なツールは、実装開始時に`mise.toml`へバージョンを固定する。Homebrew、Python、FFmpeg、Whisper CLIはアプリの実行時依存にしない。

## 実装前の状態

現在はプロダクトドキュメントを確定した段階であり、Goモジュールとmise tasksはまだ存在しない。実装開始時に、実在するセットアップタスクとコマンドだけをこの文書へ追加する。

## ローカル利用に必要な外部ファイル

- `whisper.cpp`が扱えるGGML形式の多言語Whisperモデル
- `~/.config/bosoboso/config.toml`
- 設定ファイルから参照する辞書TOML

Whisperモデルはリポジトリとアプリへ含めない。モデル、設定、辞書のパスと形式は`docs/specs/configuration.md`を参照する。

## ローカルテストに必要な外部ファイル

Integration TestとE2Eテストでは、リポジトリ外にある次のファイルをmiseタスクの`usage`引数で指定する。

- テスト用音声ファイル
- Whisperモデル

音声ファイルとモデルをリポジトリへコミットしない。

## macOS固有の確認

- 初回起動時にはマイク権限が必要になる。
- Bundle IDは`io.github.take-takashi.bosoboso`で固定する。
- MVPではコード署名と公証を必須にせず、ローカルビルドした`bosoboso.app`を対象にする。
