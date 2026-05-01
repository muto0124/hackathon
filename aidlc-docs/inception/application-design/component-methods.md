# Component Methods

## Decision Orchestrator

- `generateMorningPlan(userId, date, context)`: 朝の生活プランを生成する。
- `decideNow(userId, decisionRequest, context)`: 即決ボタンの一択判断を生成する。
- `composeDecisionResult(decision, safetyResult, preparation)`: 判断、制限、準備支援を統合する。

## User Context

- `loadContext(userId, date)`: 予定、天気、好み、予算、位置情報を取得する。
- `loadFeedbackHistory(userId)`: 承認、却下、修正などの軽量フィードバック履歴を取得する。
- `saveDecisionHistory(userId, decisionResult)`: 判断履歴を保存し、後続の怠惰レベル判定に使える形にする。

## T-AI-DA Persona

- `renderButlerResponse(decisionResult)`: 過保護で少し皮肉な執事として結果を表現する。
- `renderGuardrailMessage(safetyResult)`: 自動決定できない理由を短く説明する。

## Laziness Level

- `calculateDelegationMode(userId, domain, feedbackHistory)`: 提案型、半自動型、低リスク自動決定型を判定する。
- `updateLazinessLevel(userId, feedbackSignal)`: 承認、却下、修正に基づいて委譲度を更新する。

## Safety Guardrails

- `evaluateDecisionRisk(decisionRequest, context)`: 判断対象が低リスクか、高リスクかを評価する。
- `requireApproval(reason)`: 承認必須の判断として結果を返す。
- `rejectOutOfScope(reason)`: MVP 対象外の判断として結果を返す。

## Preparation Assistant

- `generatePreparation(decision, context)`: 買い物リスト、店舗候補、ルート候補、注文リンク候補を生成する。
- `rankPreparationOptions(options, context)`: 候補を主推奨一つと補助情報に整理する。

## Notification and Delivery

- `scheduleMorningPlan(userId, schedule)`: 朝の生活プラン生成タイミングを設定する。
- `deliverDecision(userId, decisionResult)`: 生成結果を画面または通知に届ける。
- `recordDeliveryStatus(userId, deliveryResult)`: 配信状態を記録し、CloudWatch で観測可能にする。
