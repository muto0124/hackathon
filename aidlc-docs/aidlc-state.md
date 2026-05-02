# AI-DLC State Tracking

## Project Information

| Item | Value |
| --- | --- |
| Project Name | T-AI-DA |
| Project Type | Greenfield |
| Repository Purpose | AWS Summit Japan 2026 AI-DLC Hackathon の public GitHub 提出パッケージ |
| Product Concept | 低リスクな日常判断を委任する意思決定 OS |
| MVP Scope | 朝の生活プラン生成と即決ボタン |
| Target User | 仕事後の日常的な意思決定疲れを抱えた一人暮らしのビジネスパーソン |

## Workspace State

- 審査員向け `README.md` は作成済み。
- AI-DLC Inception フェーズの Requirements、User Stories、Workflow Planning、Application Design、Units Generation 成果物は作成済み。
- `AGENTS.md`、`.serena/`、ハッカソン参加規約 PDF は提出物作成の参照または作業環境ファイルであり、提出成果物の中心には含めない。

## Code Location Rules

- 成果物は `README.md` と `aidlc-docs/` 配下に集約する。
- 設計メモと実行計画は `docs/superpowers/` 配下に保持する。

## Extension Configuration

- AI-DLC フェーズ: Inception
- 現在参照する設計コンテキスト: `docs/superpowers/specs/2026-04-30-t-ai-da-design.md`
- 実行計画: `docs/superpowers/plans/2026-04-30-t-ai-da-documents.md`
- ドキュメント言語: 日本語。ただし AI-DLC ラベル、AWS、GitHub、ファイル名、技術用語は必要に応じて英語表記を維持する。

## Stage Progress

| Stage | Status | Notes |
| --- | --- | --- |
| Inception: Product Direction | Complete | T-AI-DA の対象ユーザー、MVP、人格、安全境界を決定済み。 |
| Inception: Requirements | Complete | Intent、FR、NFR、Data Context、Safety Guardrails、Out of Scope、Traceability を作成済み。 |
| Inception: User Stories | Complete | Personas、User Stories、Acceptance Criteria、Story Map Summary を作成済み。 |
| Inception: Workflow Planning | Complete | Execution Plan、Risk Assessment、Phase Determination、Workflow Visualization を作成済み。 |
| Inception: Application Design | Complete | Components、Methods、Services、Dependencies、Application Design を作成済み。 |
| Inception: Units Generation | Complete | Unit of Work、Unit Dependency、Unit Story Map を作成済み。 |

## Current Status

- Current Stage: INCEPTION - Units Generation Complete
- State Summary: public GitHub 提出パッケージとして、README と AI-DLC Inception 成果物一式を作成済み。
- Scope Guardrail: MVP は食事、服装、日々の予定提案、買い物候補、週末または夜の過ごし方など、低リスクな日常判断に限定する。
- High-Risk Boundary: 医療、法務、金銭、雇用、契約、人間関係に重大な影響を与える判断は対象外、または明示的な承認が必要な将来スコープとする。

## Next Recommended Step

書類審査提出に向けた準備は完了。次は Construction フェーズ Slice 1（Safe Instant Decision）から着手する。

実装順序: UOW-02（ユーザー文脈モック） → UOW-04（Safety Guardrails ルールベース分類） → UOW-01（Decision Core + Bedrock 呼び出し） → UOW-06（結果表示）
