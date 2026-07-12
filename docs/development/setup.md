# 開発環境の準備

## 対象環境

- Apple Silicon搭載Mac
- macOS 14 Sonoma以降
- Xcode Command Line Tools
- mise

Go、golangci-lint、Node.js、Codex CLI、TAKTは`mise.toml`へバージョンを固定する。Fyneのパッケージ化に必要なツールは、パッケージ化の実装時に追加して固定する。Homebrew、Python、FFmpeg、Whisper CLIはアプリの実行時依存にしない。

## セットアップ

1. Xcode Command Line Toolsをインストールする。
2. miseをインストールする。
3. リポジトリのルートで次を実行する。

```shell
mise trust
mise run setup
mise run check
```

`mise run setup`は、`mise.toml`に固定された開発ツールをインストールし、Gitがリポジトリ管理下の`.githooks/`を使用するように`core.hooksPath`を設定する。シェルでmiseを有効化していない場合も、開発コマンドは`mise run <task>`で実行できる。

TAKTは、Codex SDKが起動するローカルのCodex CLIを利用する。OpenAI APIキーは使用せず、ChatGPTプランで認証したCodex CLIのログイン情報を利用する。初回だけ次を実行し、ブラウザーでChatGPTへログインする。

```shell
mise exec -- codex login
mise exec -- codex login status
```

`OPENAI_API_KEY`と`TAKT_OPENAI_API_KEY`は設定しない。すでにシェルへ設定している場合は、TAKTを実行する前に削除する。

現在はGoモジュールとモデル不要の品質ゲートだけを用意しており、アプリケーションは未実装である。GUI、音声入力、音声認識、パッケージ化に必要な依存関係は、各機能を実装するときに追加する。

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
