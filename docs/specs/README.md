# Specification Documents

このディレクトリには、機能がどのように振る舞うべきかを説明するドキュメントを配置する。

主な対象は、機能仕様、画面仕様、入力検証、権限ごとの挙動、状態遷移、受け入れ条件、例外時の挙動である。

機能単位、画面単位、業務オブジェクト単位など、作業しやすい粒度で Markdown ファイルを作成する。

状態遷移図やシーケンス図などの図は、原則として Markdown 内に Mermaid で記述する。

例:

- `docs/specs/account.md`
- `docs/specs/billing.md`
- `docs/specs/order.md`

## bosobosoの仕様

- `transcription.md`: 継続文字起こし、小窓、状態遷移、コピー、エラー処理を記載する。
- `configuration.md`: 設定ファイル、辞書、パス解決、検証規則を記載する。
