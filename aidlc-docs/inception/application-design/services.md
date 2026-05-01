# Services

## Service Overview

| Service | Purpose | Uses |
| --- | --- | --- |
| Morning Plan Service | 朝の生活プランを生成する | Decision Orchestrator, User Context, Safety Guardrails, Preparation Assistant |
| Instant Decision Service | 即決ボタンの入力に一択で回答する | Decision Orchestrator, User Context, Safety Guardrails, T-AI-DA Persona |
| Laziness Progression Service | 怠惰レベルを判定、更新する | Laziness Level, User Context |
| Safety Evaluation Service | 高リスク領域を検出する | Safety Guardrails, User Context |
| Preparation Service | 判断後の準備支援を生成する | Preparation Assistant, User Context |

## Morning Plan Service

朝の定刻に EventBridge Scheduler から起動され、ユーザー文脈を取得して生活プランを生成する。生成結果は Safety Guardrails を通過した低リスク項目だけを主推奨として返す。

## Instant Decision Service

API Gateway 経由でユーザーの質問を受け取り、即決ボタンの結果を返す。曖昧な入力は User Context で補完するが、高リスク領域は自動決定しない。

## Laziness Progression Service

承認、却下、修正などの軽量フィードバック履歴をもとに、委譲度を提案型、半自動型、低リスク自動決定型へ調整する。安全境界を上書きする権限は持たない。

## Safety Evaluation Service

判断要求が医療、法務、雇用、契約、高額購入、重大な人間関係に該当するかを評価する。該当する場合は承認必須または対象外として返す。

## Preparation Service

判断結果に対して、買い物リスト、店舗候補、ルート候補、注文リンク候補を生成する。MVP では準備候補の提示に留め、購入や予約の実行は行わない。
