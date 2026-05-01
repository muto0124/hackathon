# T-AI-DA（タイダ）

## 一言で

T-AI-DA は、日常の小さな意思決定に疲れた一人暮らしのビジネスパーソンを、AI が徹底的に甘やかす意思決定代行サービスです。

朝の「今日の生活プラン」と、オンデマンドの「即決ボタン」によって、食事、服装、買い物、夜の過ごし方などの低リスクな判断を 1 つに絞って提示します。

## なぜ作るのか

仕事後の一人暮らしでは、食事、服装、買い物、移動、夜の過ごし方のような小さな判断が毎日積み重なります。選択肢が多すぎるほど比較は増え、意思決定疲れが起き、退勤後の認知負荷はさらに高まります。

T-AI-DA は、比較リストを増やすのではなく、低リスクな日常判断を AI に委任する体験を作ります。ユーザーは「どれにするか」を考える代わりに、T-AI-DA が決めた 1 つの提案を受け取り、必要な準備まで進められます。

## 対象ユーザー

- 仕事後に日常の判断をする気力が残っていない一人暮らしのビジネスパーソン
- 食事、服装、買い物、予定のような低リスクな判断に時間を使いたくない人
- 比較検討よりも「今日はこれでよい」と背中を押してほしい人

## MVP 体験

1. 朝の生活プラン生成
   - 天気、予定、好み、予算などのコンテキストをもとに、T-AI-DA がその日の食事、服装、買い物候補、夜の過ごし方を 1 つの生活プランとして決めます。
   - 比較リストではなく「今日はこれです」と 1 つの決定を提示し、買い物リスト、店舗候補、移動ルートなどの準備を支援します。

2. 即決ボタン
   - ユーザーが「夕飯どうする」「帰りに何を買う」などを入力すると、T-AI-DA が低リスクな範囲で 1 つの判断を返します。
   - 候補を並べるのではなく即決し、必要に応じて注文リンク、店舗候補、持ち物、移動ルートなどの準備を添えます。

## 怠惰レベル

怠惰レベルは、ユーザーが T-AI-DA にどれだけ判断を委任しているかを表す進行指標です。

- Level 1: 提案。T-AI-DA が 1 つの判断を提示し、ユーザーが実行する。
- Level 2: 半自動。T-AI-DA が判断に加えて、買い物リストや店舗候補などの準備を行う。
- Level 3: 低リスク自動化。承認済みの範囲で、低リスクな日常タスクをより強く委任する。

MVP では Level 1 から Level 2 を中心に扱い、高額購入、医療、法務、雇用、重大な人間関係などの高リスク領域は対象外または明示的な承認が必要です。

## AWS アーキテクチャ案

- Amazon Bedrock: 意思決定生成と人格応答
- AWS Lambda: 意思決定オーケストレーション
- Amazon API Gateway: API エントリポイント、in-app での結果配信
- Amazon DynamoDB: ユーザー設定、怠惰レベル、意思決定履歴、生成済み生活プランの保管
- Amazon EventBridge Scheduler: 朝の生活プラン生成トリガー
- Amazon S3: ドキュメント、静的アセット、将来の UI 配信候補
- Amazon CloudWatch: ログ、監視、意思決定実行状況の観測
- Future: Amazon SNS / Amazon Pinpoint: 朝のプラン通知や即決結果の push 配信

## AI-DLC Inception 成果物

### 状態とログ

- [AI-DLC 状態管理](aidlc-docs/aidlc-state.md)
- [監査ログ](aidlc-docs/audit.md)

### Requirements / User Stories

- [要求定義](aidlc-docs/inception/requirements/requirements.md)
- [要求検証質問](aidlc-docs/inception/requirements/requirement-verification-questions.md)
- [ペルソナ](aidlc-docs/inception/user-stories/personas.md)
- [ユーザーストーリー](aidlc-docs/inception/user-stories/stories.md)

### Workflow / Application Design / Units

- [実行計画](aidlc-docs/inception/plans/execution-plan.md)
- [アプリケーション設計](aidlc-docs/inception/application-design/application-design.md)
- [コンポーネント](aidlc-docs/inception/application-design/components.md)
- [コンポーネントメソッド](aidlc-docs/inception/application-design/component-methods.md)
- [サービス](aidlc-docs/inception/application-design/services.md)
- [コンポーネント依存関係](aidlc-docs/inception/application-design/component-dependency.md)
- [作業単位](aidlc-docs/inception/application-design/unit-of-work.md)
- [作業単位依存関係](aidlc-docs/inception/application-design/unit-of-work-dependency.md)
- [作業単位とストーリーの対応](aidlc-docs/inception/application-design/unit-of-work-story-map.md)

### AI-DLC 実行判断

- [User Stories 実行判断](aidlc-docs/inception/plans/user-stories-assessment.md)
- [Application Design 実行計画](aidlc-docs/inception/plans/application-design-plan.md)
- [Unit of Work 実行計画](aidlc-docs/inception/plans/unit-of-work-plan.md)

## 審査基準への対応

- 課題の明確さ: 仕事後の日常的な意思決定疲れ、選択肢過多、認知負荷を中心課題として定義します。
- テーマ適合性: 怠惰レベルにより、判断を委任するほど AI に甘やかされる体験を表現します。
- 実現可能性: MVP を朝の生活プラン生成と即決ボタンに絞り、AWS のマネージドサービスで構成します。
- トレーサビリティ: 要求、ストーリー、コンポーネント、作業単位、実行計画を `aidlc-docs/` 配下で追跡します。
- 安全性: MVP の自動化対象を低リスクな日常判断に限定し、高リスク領域は承認要求または拒否に切り替えます。

## 今後の展開

書類審査通過後の Construction フェーズで、以下を MVP プロトタイプとして実装します。

- Slice 1: Safe Instant Decision (即決ボタンと Safety Guardrails)
- Slice 2: Morning Lifestyle Plan (朝の生活プランと準備支援)
- Slice 3: Laziness Level (委譲モードと怠惰レベル可視化)

その後の拡張方針は次の通りです。

- カレンダー、位置情報、購買履歴などの連携によるコンテキスト精度の向上
- 怠惰レベルに応じた半自動化範囲の拡大
- 家族、チーム、旅行など複数人の低リスク判断への応用
- Amazon SNS / Pinpoint による朝の push 通知などの配信チャネル追加
