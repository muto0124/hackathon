# Unit of Work Story Map

## Story To Unit Mapping

| Story | Summary | Primary Unit | Supporting Units |
| --- | --- | --- | --- |
| US-001 | 朝の生活プランを受け取る | UOW-01 Decision Core | UOW-02, UOW-04, UOW-05, UOW-06 |
| US-002 | 食事を一択で決めてもらう | UOW-01 Decision Core | UOW-02, UOW-05, UOW-06 |
| US-003 | 服装を決めてもらう | UOW-02 Context and Preference Memory | UOW-01, UOW-06 |
| US-004 | 買い物候補と準備リストを受け取る | UOW-05 Preparation and Recommendation Delivery | UOW-01, UOW-02, UOW-04 |
| US-005 | 即決ボタンで迷いを投げる | UOW-01 Decision Core | UOW-02, UOW-04, UOW-06 |
| US-006 | 怠惰レベルが上がる | UOW-03 Laziness Level and Delegation Control | UOW-02, UOW-04 |
| US-007 | 高リスク判断で承認を求められる | UOW-04 Safety Guardrails | UOW-01, UOW-06 |
| US-008 | 低リスクな準備支援を受ける | UOW-05 Preparation and Recommendation Delivery | UOW-01, UOW-02, UOW-06 |

## Requirement To Unit Mapping

| Requirement | Unit Coverage |
| --- | --- |
| FR-001 | UOW-01, UOW-02, UOW-05, UOW-06 |
| FR-002 | UOW-01, UOW-02, UOW-04, UOW-06 |
| FR-003 | UOW-03, UOW-02, UOW-04 |
| FR-004 | UOW-05, UOW-02, UOW-06 |
| FR-005 | UOW-04, UOW-01, UOW-06 |
| NFR-001 | UOW-04, UOW-03 |
| NFR-002 | UOW-06, UOW-01 |
| NFR-003 | UOW-01, UOW-06 |
| NFR-004 | UOW-02, UOW-04 |
| NFR-005 | UOW-05, UOW-06 |
| DCR-001 - DCR-006 | UOW-02 |

## Construction Slice Recommendation

### Slice 1: Safe Instant Decision

- UOW-02: 固定ユーザー文脈
- UOW-04: 高リスク判定
- UOW-01: 即決判断
- UOW-06: 結果表示

### Slice 2: Morning Lifestyle Plan

- UOW-02: 予定、天気、好み、予算
- UOW-01: 朝の生活プラン
- UOW-05: 買い物、ルート、準備候補
- UOW-06: 朝の通知または表示

### Slice 3: Laziness Level

- UOW-02: 軽量フィードバック履歴
- UOW-03: 委譲モード判定
- UOW-04: 安全境界による上書き防止
- UOW-01: 判断結果への反映
