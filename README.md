# line-autofix-sandbox

`round-robin-scoreboard` の `www/`・`tests/` を複製した**試験専用**の案件リポジトリ。
[`Ryoseiimai/line-autofix`](https://github.com/Ryoseiimai/line-autofix) のクラウドループ
（LINE要望 → 仕様化 → 実装 → テスト/E2E → プレビュー → 承認「OK」→ 本番マージ）を、
本番の「スコアボード」グループ・本番リポジトリを一切汚さずに一周検証するための試験環境。

- 実データ・個人情報は含まない（本番アプリの静的な複製のみ）。
- `projects.json` では `groupId` が `TEST-` で始まる架空グループにのみ紐づく。
- Worker側 (`src/worker.mjs`) は `groupId` が `TEST-` で始まるリクエストを常に `test_mode=1` として扱い、
  実際のLINE API（reply/push）を一切呼ばない（ログ・管理者メールのみ）。設定ミスがあっても
  本番グループへ送信されることはない（コード側の多重防御）。
- 承認者IDも架空（`TESTU-...`）。実在のLINEユーザーとは無関係。
- E2E駆動スクリプトは共通repoの `scripts/e2e-sandbox.mjs`（`Ryoseiimai/line-autofix` 側）。

本番運用のドキュメントは `Ryoseiimai/line-autofix` の `SPEC.md` / `README.md` を参照。
