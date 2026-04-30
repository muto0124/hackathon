# Requirements

## Intent Analysis

T-AI-DA は、仕事や生活で判断を重ねたユーザーが、朝や退勤後に残された小さな生活判断から解放されるための意思決定 OS / Life OS である。MVP では「何を食べるか」「何を着るか」「帰りに何を買うか」「夜をどう過ごすか」のような低リスクな日常判断に絞り、判断の選択肢を減らすことを価値の中心に置く。

中核体験は、朝の生活プランと即決ボタンである。T-AI-DA は過保護で少し皮肉っぽい執事として、ユーザーの文脈を読み、理由を添えて一択または少数の実行しやすい提案にまとめる。

## Business Intent

- AWS Summit Japan 2026 AI-DLC Hackathon の書類審査で、プロダクト意図、要求、ユニット、後続設計の追跡可能性を明確に示す。
- 「怠惰レベル」により、AI が提案から半自動、低リスク自動決定へ段階的に進むハッカソンテーマ適合性を示す。
- 一人ビジネスパーソンの仕事後の日常的な意思決定疲れを、具体的で低リスクな生活支援として解決する。
- 将来の購買、カレンダー、健康ログ、関係性提案などの拡張余地を残しつつ、MVP では安全な判断領域に限定する。

## Functional Requirements

| ID | Requirement | Description | Primary Unit |
| --- | --- | --- | --- |
| FR-001 | 朝の生活プランを生成する | 天気、予定、好み、位置情報、予算をもとに、食事、服装、予定の優先度、買い物候補、夜または週末の過ごし方を朝の生活プランとして提示する。 | Decision Orchestrator |
| FR-002 | 即決ボタンで小さな迷いに一択回答する | ユーザーが迷いを入力または選択したとき、低リスク領域であれば理由付きの一択回答を返す。 | Decision Orchestrator |
| FR-003 | 怠惰レベルに応じて提案型、半自動型、低リスク自動決定型を切り替える | ユーザーの許容度、対象領域、過去の反応に応じて、提案のみ、準備まで、低リスクな決定までの強さを制御する。 | Laziness Level |
| FR-004 | 買い物リスト、店舗候補、ルート、注文リンクなどの準備支援を生成する | 決定後に必要な買い物リスト、店舗候補、移動ルート、注文リンクなどをまとめ、ユーザーが実行しやすい状態にする。 | Preparation Assistant |
| FR-005 | 高リスク判断を検出して制限する | 高額購入、医療、法務、契約、雇用、退職、別れ、重大な金銭・健康・法律・人間関係判断を検出し、承認要求、専門家相談の案内、または拒否に切り替える。 | Safety Guardrails |
| FR-006 | 執事らしいプロダクトボイスを生成する | 過保護で少し皮肉っぽい執事の口調で、提案、理由、制限の説明を一貫して生成する。 | T-AI-DA Persona |
| FR-007 | MVP 向け文脈データを管理する | 天気、予定、好み、位置情報、予算を判断材料として保持し、各判断に必要な範囲で Decision Orchestrator に渡す。 | User Context |

## Non-Functional Requirements

| ID | Requirement | Description |
| --- | --- | --- |
| NFR-001 | 低リスク領域を明確に制限する安全性 | MVP の自動化対象は生活上の低リスク判断に限定し、高リスク領域は Safety Guardrails が必ず制限する。 |
| NFR-002 | ユーザーが理由を理解できる説明可能性 | 提案や一択回答には、天気、予定、好み、予算などの根拠を短く添える。 |
| NFR-003 | 朝の利用に耐える応答速度 | 朝の生活プランと即決ボタンは、忙しい時間帯でも待ち時間が負担にならない応答速度を目指す。 |
| NFR-004 | 個人文脈データのプライバシー保護 | 予定、位置情報、好み、予算などの個人文脈データは、目的を限定し、不要な保持や過剰な共有を避ける。 |
| NFR-005 | 将来の外部連携に耐える拡張性 | 購買、カレンダー、健康ログ、地図、注文サービスなどの将来連携を、コンポーネント単位で追加できる構成にする。 |

## Data and Context Requirements

| ID | Data / Context | MVP Usage | Notes |
| --- | --- | --- | --- |
| DCR-001 | 天気 | 服装、移動、外出、食事候補の判断に利用する。 | 例: 雨なら屋内寄り、暑ければ軽装を提案する。 |
| DCR-002 | 予定 | 朝の生活プラン、移動余裕、夜の過ごし方の判断に利用する。 | カレンダー連携は将来拡張可能にする。 |
| DCR-003 | 好み | 食事、服装、買い物、余暇提案の絞り込みに利用する。 | 明示設定と過去反応の両方を将来扱えるようにする。 |
| DCR-004 | 位置情報 | 店舗候補、移動ルート、近場の選択肢の判断に利用する。 | 必要時のみ利用し、プライバシーに配慮する。 |
| DCR-005 | 予算 | 買い物候補、食事候補、注文リンクの絞り込みに利用する。 | 高額購入は Safety Guardrails の対象にする。 |

## Safety and Guardrails

- MVP の判断対象は、食事、服装、日々の予定提案、買い物候補、週末または夜の過ごし方などの低リスクな日常領域に限定する。
- 高額な購入、医療診断や治療判断、法務、契約、雇用、退職、別れに関する判断は自動決定しない。
- 金銭、健康、法律、人間関係に重大な影響を与える判断を検出した場合、T-AI-DA は承認要求、専門家相談の案内、または拒否へ切り替える。
- 怠惰レベルが上がっても、安全境界を超える判断は自動化しない。
- 実購入、予約、注文確定、外部送信などの実行操作は、MVP では準備支援までに留める。

## Out of Scope

- 高額な購入の自動決定または購入確定。
- 医療診断、治療方針、服薬、健康上の重大判断。
- 法務、契約、雇用、退職、別れ、重大な人間関係判断。
- 金融投資、借入、保険、資産運用など重大な金銭判断。
- ユーザー承認なしの実購入、予約、注文確定、メッセージ送信。
- 本格的な外部サービス連携の実装。MVP では、リンクや候補の準備支援に留める。

## Traceability

| Requirement | Source Question | Related Unit | Later Artifact |
| --- | --- | --- | --- |
| FR-001 | Q-001, Q-002, Q-005, Q-007 | Decision Orchestrator, User Context | user-stories/stories.md, application-design/components.md |
| FR-002 | Q-002, Q-004, Q-007 | Decision Orchestrator, Laziness Level | user-stories/stories.md, application-design/component-methods.md |
| FR-003 | Q-004, Q-009 | Laziness Level | application-design/components.md, unit-of-work.md |
| FR-004 | Q-001, Q-008 | Preparation Assistant | application-design/services.md, unit-of-work-story-map.md |
| FR-005 | Q-010 | Safety Guardrails | application-design/component-dependency.md, unit-of-work-dependency.md |
| FR-006 | Q-003 | T-AI-DA Persona | user-stories/personas.md, application-design/components.md |
| FR-007 | Q-005 | User Context | application-design/services.md, component-dependency.md |
| NFR-001 | Q-001, Q-010 | Safety Guardrails | application-design/application-design.md |
| NFR-002 | Q-003, Q-005 | T-AI-DA Persona, User Context | user-stories/stories.md |
| NFR-003 | Q-002, Q-007 | Decision Orchestrator | execution-plan.md |
| NFR-004 | Q-005 | User Context | application-design/services.md |
| NFR-005 | Q-008 | Preparation Assistant, User Context | execution-plan.md |
