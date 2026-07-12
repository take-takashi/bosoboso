# bosoboso

`bosoboso`は、マイク音声を完全にローカルで継続的に文字起こしし、必要な文章を小窓からコピーするmacOS向けデスクトップアプリである。

最初の対象は、CodexやClaude Codeへ日本語のプロンプトを音声入力する開発者である。Whisperと利用者定義の辞書を使い、`mise`などの英字表記や専門用語の認識精度を高める。

現在は仕様策定段階であり、アプリケーションは未実装である。

## 開発環境

Apple Silicon搭載MacへXcode Command Line Toolsとmiseを用意した後、次のコマンドで固定済みの開発ツールをインストールして検証できる。

```shell
mise run setup
mise run check
```

詳細は[開発環境の準備](docs/development/setup.md)と[開発コマンド](docs/development/commands.md)を参照する。

## ドキュメント

- [PRD](docs/product/prd.md)
- [継続文字起こし仕様](docs/specs/transcription.md)
- [設定・辞書仕様](docs/specs/configuration.md)
- [アーキテクチャ概要](docs/architecture/overview.md)
- [技術スタック](docs/architecture/tech-stack.md)
- [テスト戦略](docs/development/testing.md)
