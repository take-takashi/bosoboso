# Tech Stack

このドキュメントには、このプロジェクトで採用する技術スタック、主要ツール、バージョン方針を記録する。

テンプレートから新しいプロジェクトを作成するときは、実際の採用内容に合わせてこのファイルを更新する。

## 採用技術

| 領域 | 採用技術 | バージョン | 用途 | 備考 |
| --- | --- | --- | --- | --- |
| 言語 | TBD | TBD | TBD | TBD |
| ランタイム | TBD | TBD | TBD | TBD |
| フレームワーク | TBD | TBD | TBD | TBD |
| パッケージマネージャー | TBD | TBD | TBD | TBD |
| データストア | TBD | TBD | TBD | TBD |
| テスト | TBD | TBD | TBD | TBD |
| Lint | TBD | TBD | TBD | TBD |
| Format | TBD | TBD | TBD | TBD |
| CI | TBD | TBD | TBD | TBD |
| デプロイ | TBD | TBD | TBD | TBD |

## 採用理由

採用した技術ごとに、選定理由を簡潔に記載する。

- TBD

## バージョン管理方針

言語、ランタイム、パッケージマネージャー、主要ツールのバージョンをどこで固定するかを記載する。

例:

- `.tool-versions`
- `mise.toml`
- `package.json`
- `pnpm-lock.yaml`
- `uv.lock`
- `go.mod`
- `Dockerfile`

## 代替候補

検討したが採用しなかった候補と、その理由を記載する。

| 候補 | 不採用理由 | 備考 |
| --- | --- | --- |
| TBD | TBD | TBD |

## 更新ルール

- 技術スタックを変更した場合は、このファイルを更新する。
- 実行コマンドを変更した場合は、`docs/development/commands.md` も更新する。
- 採用理由が意思決定として重要な場合は、`docs/decisions/` に ADR を追加する。
