# Unit of Work Plan

## Decision

Units Generation を実行する。

## Rationale

書類審査基準に Unit 分解の適切さが含まれるため、T-AI-DA の MVP を Construction フェーズで扱える作業単位に分解する。

## Decomposition Criteria

- ユーザー体験として独立して説明できる。
- Construction フェーズで作業単位にできる。
- Safety Guardrails との依存を明確にできる。
- User Stories と Requirements へのトレーサビリティを示せる。
- 各 Unit が責務を持ちすぎず、検証しやすい。

## Inputs

- `aidlc-docs/inception/requirements/requirements.md`
- `aidlc-docs/inception/user-stories/stories.md`
- `aidlc-docs/inception/application-design/application-design.md`
- `aidlc-docs/inception/application-design/component-dependency.md`

## Output Artifacts

- `aidlc-docs/inception/application-design/unit-of-work.md`
- `aidlc-docs/inception/application-design/unit-of-work-dependency.md`
- `aidlc-docs/inception/application-design/unit-of-work-story-map.md`

## Unit Strategy

MVP の中核は `Decision Core`、`Context and Preference Memory`、`Laziness Level and Delegation Control`、`Safety Guardrails`、`Preparation and Recommendation Delivery`、`User Experience Surface` の 6 Unit とする。

Safety Guardrails は全 Unit に横断するが、独立 Unit として扱い、自動決定の前に必ず評価される境界にする。
