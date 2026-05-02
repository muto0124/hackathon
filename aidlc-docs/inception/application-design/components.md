# Components

## Component Overview

| Component | Responsibility | Primary Inputs | Primary Outputs |
| --- | --- | --- | --- |
| Decision Orchestrator | 朝の生活プランと即決判断を組み立てる中核 | ユーザー文脈、要求、怠惰レベル、安全評価 | 一択の判断、理由、準備指示 |
| User Context | 天気、予定、好み、位置情報、予算、軽量フィードバック履歴を管理する | ユーザー設定、外部文脈、判断履歴 | 判断に使う正規化済み文脈 |
| T-AI-DA Persona | 過保護で少し皮肉な執事として応答を整える | 判断結果、理由、安全制限 | ユーザー向けメッセージ |
| Laziness Level | 提案型、半自動型、低リスク自動決定型の委譲度を制御する | 承認、却下、修正履歴、対象領域 | 委譲モード、許可範囲 |
| Safety Guardrails | 高リスク判断を検出し、自動決定を制限する | 判断対象、金額、影響領域、ユーザー要求 | 自動決定可、承認必須、対象外 |
| Preparation Assistant | 判断後の準備支援を生成する | 判断結果、場所、予算、外部候補 | 買い物リスト、店舗候補、ルート候補、注文リンク候補 |
| Notification and Delivery | 朝の通知と即決結果をユーザーへ届ける | 生成結果、配信タイミング、ユーザー設定 | 通知、画面表示、履歴保存 |

## AWS Mapping

| Component | Candidate AWS Services |
| --- | --- |
| Decision Orchestrator | AWS Lambda, Amazon Bedrock |
| User Context | Amazon DynamoDB, EventBridge Scheduler |
| T-AI-DA Persona | Amazon Bedrock |
| Laziness Level | AWS Lambda, Amazon DynamoDB |
| Safety Guardrails | AWS Lambda, Amazon Bedrock Guardrails candidate |
| Preparation Assistant | AWS Lambda, Amazon Bedrock, external API adapters |
| Notification and Delivery | Amazon API Gateway (in-app 配信), EventBridge Scheduler (朝の起動), Amazon CloudWatch (配信状態の観測), Future: Amazon SNS / Amazon Pinpoint (push 通知 / メール) |

MVP では、朝の生活プラン生成は EventBridge Scheduler から起動し、結果を Amazon DynamoDB に保存する。ユーザーは API Gateway 経由でアプリ内表示を参照する pull モデルを採用する。push 通知やメール配信は将来拡張として Amazon SNS または Amazon Pinpoint で追加できる構成にする。

## Component Boundaries

- Decision Orchestrator は判断を統合するが、ユーザー文脈の永続化は User Context に委譲する。
- Safety Guardrails は自動決定可否を判定する独立境界とし、他コンポーネントから上書きできない。
- T-AI-DA Persona は表現を整えるが、禁止された判断を許可する責務を持たない。
- Preparation Assistant は低リスクな準備候補を作るが、MVP では購入や予約の実行までは行わない。
