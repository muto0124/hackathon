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

`User Experience Surface` (UOW-06) は単独で価値を持つ Primary Story を持たず、すべての Story で Supporting Unit として現れる。それでも独立 Unit として残す理由は次の通り。

- T-AI-DA Persona と Notification and Delivery を集約する表示層であり、判断ロジックから分離して交換可能にしたい。
- 怠惰レベルの可視化、ガードレールメッセージ、準備支援表示など、横断的な UX 責務を一箇所に集約したい。
- Construction Slice 1〜3 のすべてで結果表示が必要であり、共通の UX 単位として再利用しやすい。
