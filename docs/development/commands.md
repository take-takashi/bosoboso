# 開発コマンド

## 方針

- すべての開発タスクをmise tasksとして`mise.toml`に定義する。
- README、開発ドキュメント、CIでは、原則として`mise run <task>`だけを案内・実行する。
- 引数を受け取るタスクは、miseの`usage`で引数、オプション、既定値、ヘルプを宣言する。
- シェルスクリプト内で独自に位置引数を解析しない。
- 内部で実行する`go`、Fyne、golangci-lintなどの生コマンドは、トラブルシューティング以外では利用者向けの入口にしない。

## 利用できるタスク

| 目的 | 入口 | モデル | CI |
| --- | --- | --- | --- |
| ツールとGit hooksのセットアップ | `mise run setup` | 不要 | mise actionがツールを導入 |
| フォーマット | `mise run format` | 不要 | 対象外 |
| フォーマット確認 | `mise run format:check` | 不要 | 実行 |
| Lint | `mise run lint` | 不要 | 実行 |
| ユニットテスト | `mise run test` | 不要 | 実行 |
| モデル不要ビルド | `mise run build` | 不要 | 実行 |
| Go依存関係の整理 | `mise run tidy` | 不要 | 対象外 |
| 全軽量検証 | `mise run check` | 不要 | 実行 |
| TAKTでタスクを整理してキューへ登録 | `mise run takt` | 不要 | 対象外 |
| TAKTのキューを隔離worktreeで実行 | `mise run takt:run` | 不要 | 対象外 |
| TAKTのタスクブランチと結果を管理 | `mise run takt:list` | 不要 | 対象外 |

開発起動、Integration Test、E2Eテスト、macOSアプリ作成のタスクは、対応する実装がまだ存在しないため定義していない。Integration TestとE2Eテストを追加するときは、少なくとも音声ファイルとWhisperモデルのパスを`usage`の必須引数として定義する。

## 更新ルール

- `mise.toml`へタスクを追加または変更した場合は、このファイルを同時に更新する。
- 関連するタスクを分類する場合は、タスク名をハイフンではなくコロンでつなぐ。
- CIは独自の検証手順を持たず、対応するmiseタスクを呼び出す。
- 技術スタックやツールを変更した場合は、`docs/architecture/tech-stack.md`も更新する。
