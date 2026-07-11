# 開発コマンド

## 方針

- すべての開発タスクをmise tasksとして`mise.toml`に定義する。
- README、開発ドキュメント、CIでは、原則として`mise run <task>`だけを案内・実行する。
- 引数を受け取るタスクは、miseの`usage`で引数、オプション、既定値、ヘルプを宣言する。
- シェルスクリプト内で独自に位置引数を解析しない。
- 内部で実行する`go`、Fyne、golangci-lintなどの生コマンドは、トラブルシューティング以外では利用者向けの入口にしない。

## 実装予定のタスク

現時点ではアプリケーションと`mise.toml`が未実装であるため、次のタスク名は設計上の予定であり、まだ実行できない。実装時に実在する定義と同期して、この表を確定する。

| 目的 | 予定する入口 | モデル | CI |
| --- | --- | --- | --- |
| 開発起動 | `mise run dev` | 必要 | 対象外 |
| フォーマット | `mise run format` | 不要 | 差分確認を実行 |
| Lint | `mise run lint` | 不要 | 実行 |
| ユニット・GUIテスト | `mise run test` | 不要 | 実行 |
| モデル不要ビルド | `mise run build` | 不要 | 実行 |
| Integration Test | `mise run integration` | 必要 | 対象外 |
| E2Eテスト | `mise run e2e` | 必要 | 対象外 |
| macOSアプリ作成 | `mise run package` | 不要 | MVPでは対象外 |
| 全軽量検証 | `mise run check` | 不要 | 実行 |

Integration TestとE2Eテストのタスクでは、少なくとも音声ファイルとWhisperモデルのパスを`usage`の必須引数として定義する。

## 更新ルール

- `mise.toml`へタスクを追加または変更した場合は、このファイルを同時に更新する。
- CIは独自の検証手順を持たず、対応するmiseタスクを呼び出す。
- 技術スタックやツールを変更した場合は、`docs/architecture/tech-stack.md`も更新する。
