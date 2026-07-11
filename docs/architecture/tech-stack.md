# 技術スタック

## 採用技術

| 領域 | 採用技術 | バージョン方針 | 用途 | 備考 |
| --- | --- | --- | --- | --- |
| 言語 | Go | 実装開始時の最新安定版を固定 | アプリケーション全体 | `go.mod`と`mise.toml`で固定する |
| GUI | Fyne | 実装開始時に固定 | クロスプラットフォームGUI | ヘッドレスなGUIテストに対応する |
| 音声入力 | `malgo` / miniaudio | 実装開始時に固定 | デバイス列挙とPCM取得 | cgoを使用し、macOSではCore Audioへ接続する |
| 音声認識 | `whisper.cpp`公式Goバインディング | 実装開始時に固定 | ローカルWhisper推論 | cgoとMetalを使用する |
| VAD | Silero VAD | 対応モデルを固定 | 発話区間の検出 | 約1 MiB未満のモデルをアプリへ同梱する |
| 設定 | TOML | スキーマ`version = 1` | 設定と辞書 | ライブラリは実装時に選定する |
| タスクランナー | mise tasks | `mise.toml`で固定 | 開発コマンドの統一 | 引数は`usage`で宣言する |
| Lint | golangci-lint | miseで固定 | Goの静的解析 | 有効なルールを明示する |
| テスト | Go標準テスト、Fyne test | Go依存として固定 | ユニット、GUIコンポーネント、結合テスト | モデル必須テストはローカルで実行する |
| CI | GitHub Actions | ワークフローで固定 | モデル不要の品質ゲート | Integration TestとE2Eは含めない |

## 採用理由

- Goをアプリケーションの中心とし、配布物と実行時依存を小さく保つ。
- Fyneによって、HTML、CSS、JavaScriptの別プロジェクトを持たず、小窓に必要なGUIとヘッドレステストを実現する。
- `malgo`は外部共有ライブラリを要求せず、将来のクロスプラットフォーム対応に利用できる。
- `whisper.cpp`はApple SiliconとMetalに対応し、Whisperモデルをローカルで実行できる。
- Silero VADは軽量で、単純な音量閾値より発話区間を安定して検出できることが期待できる。
- mise tasksをすべての開発コマンドの入口とし、開発者とCIの実行方法をそろえる。

## 実行時依存

`bosoboso.app`には、Fyne、`malgo`、miniaudio、`whisper.cpp`、Silero VADモデルを組み込む。Homebrew、Python、FFmpeg、Whisper CLIなどを実行時には要求しない。

Whisperモデルは品質と性能を利用者が選べるように同梱せず、設定ファイルでパスを指定する。対応形式はMVPでは`whisper.cpp`が扱えるGGML形式に限定する。

## バージョン管理方針

- Go、golangci-lint、パッケージ化ツールは`mise.toml`で固定する。
- Go依存関係は`go.mod`と`go.sum`で固定する。
- cgoで組み込む依存関係は、再現可能な取得方法とバージョンをリポジトリ内で明示する。
- 依存関係の更新時は、Apple Silicon上でビルド、GUIテスト、Integration Test、E2Eテストを行う。

## ライセンス

- `bosoboso`本体はAGPL-3.0を維持する。
- 配布物には、本体のライセンスと同梱依存物の著作権表示・ライセンス文を含める。
- アプリメニューから「bosobosoについて」と「ライセンス」を確認できるようにする。
- ソースコードの案内先は`https://github.com/take-takashi/bosoboso`とする。
- 依存物を追加または更新した場合は、配布条件を再確認する。

## 今後の候補

| 候補 | MVPで採用しない理由 |
| --- | --- |
| 別のローカルLLMによる校正 | モデルを二つ常駐させる負荷、遅延、意図しない文章変更を先に評価する必要がある |
| Core ML / Apple Neural Engine | 利用者指定モデルとは別の生成物が必要になり、セットアップが複雑になる |
| Wails | 今回の小窓にWebフロントエンドを追加する必要性がない |
| Whisper CLIの子プロセス実行 | 外部実行物とプロセス間通信が必要になり、配布とテストが複雑になる |
