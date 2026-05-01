# Application Design Plan

## Decision

Application Design を実行する。

## Rationale

- 書類審査では、Intent だけでなく Unit 分解の適切さが評価される。
- T-AI-DA は意思決定生成、ユーザー文脈、安全制御、準備支援を分けて説明する必要がある。
- AWS ベースの実現可能性を示すことで、アイデアだけでなく Construction へ進める構造を示せる。

## Design Inputs

- `aidlc-docs/inception/requirements/requirements.md`
- `aidlc-docs/inception/user-stories/stories.md`
- `aidlc-docs/inception/plans/execution-plan.md`

## Output Artifacts

- `aidlc-docs/inception/application-design/components.md`
- `aidlc-docs/inception/application-design/component-methods.md`
- `aidlc-docs/inception/application-design/services.md`
- `aidlc-docs/inception/application-design/component-dependency.md`
- `aidlc-docs/inception/application-design/application-design.md`

## Design Principles

- 低リスクな日常判断だけを MVP の自動化対象にする。
- Decision Orchestrator は必ず Safety Guardrails を経由する。
- Laziness Level は便利さを表現するが、安全境界を上書きしない。
- AWS サービスは Inception 段階の構成案として記載し、実装詳細に踏み込みすぎない。
